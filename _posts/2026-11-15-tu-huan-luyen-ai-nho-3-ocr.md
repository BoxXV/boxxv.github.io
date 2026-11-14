---
layout: post
categories: ["Trí tuệ nhân tạo & Dữ liệu"]
title: "Tự huấn luyện mô hình AI nhỏ (3): Nhận diện ký tự quang học (OCR) tiếng Việt"
subtitle: "Fine-tune mô hình thị giác ngôn ngữ bằng LoRA và huấn luyện từ đầu Transformer OCR"
date: 2026-11-15 08:20:00 +0700
tags:
- AI
- OCR
- PaddleOCR
- VietOCR
- Vision Language Model
- Unsloth
- Fine-tuning
series: "Tự huấn luyện mô hình AI nhỏ"
series_order: 3
---

> Bài 3 của series. OCR là lĩnh vực mà mô hình nhỏ tự huấn luyện có lợi thế rõ nhất: biểu mẫu, hoá đơn, tem nhãn của mỗi công ty có bố cục và phông chữ riêng, và một mô hình vài chục triệu tham số được dạy đúng loại giấy tờ đó thường chính xác hơn mô hình dùng chung. Kiến thức nền nằm ở [bài 1](/2026/11/15/tu-huan-luyen-ai-nho-1-tong-quan/). Code là khung cốt lõi, chưa chạy kiểm chứng trên GPU thật.

- [Hai kiểu hệ thống OCR](#hai-kiểu-hệ-thống-ocr)
- [Technical stack](#technical-stack)
- [Dữ liệu đầu vào](#dữ-liệu-đầu-vào)
- [Các cách làm xếp từ dễ đến khó](#các-cách-làm-xếp-từ-dễ-đến-khó)
- [Từng bước fine-tune mô hình thị giác ngôn ngữ bằng LoRA](#từng-bước-fine-tune-mô-hình-thị-giác-ngôn-ngữ-bằng-lora)
- [Từng bước huấn luyện bộ nhận dạng từ đầu với VietOCR](#từng-bước-huấn-luyện-bộ-nhận-dạng-từ-đầu-với-vietocr)
- [Lưu ý quan trọng](#lưu-ý-quan-trọng)
- [Nguồn tham khảo](#nguồn-tham-khảo)

## Hai kiểu hệ thống OCR

**Kiểu đường ống cổ điển** gồm các mô hình nhỏ nối tiếp: phát hiện vùng chữ (detection), xoay và cắt từng dòng, nhận dạng chữ trong dòng (recognition), rồi luật hoặc mô hình khác để rút trường thông tin. Mỗi khâu chỉ vài triệu đến vài chục triệu tham số, chạy được trên CPU. Bạn có thể huấn luyện lại riêng khâu yếu nhất, thường là khâu nhận dạng.

**Kiểu đầu cuối bằng mô hình thị giác ngôn ngữ (VLM)** nhận cả trang ảnh và sinh thẳng văn bản, Markdown hoặc JSON. Mô hình cỡ 1B đến 4B tham số, cần GPU khi chạy, đổi lại hiểu bố cục, bảng, chữ viết tay và rút trường thông tin trong một bước.

Chọn kiểu nào: dòng chữ in hoặc tem nhãn với số lượng lớn và cần tốc độ thì dùng đường ống cổ điển. Tài liệu bố cục phức tạp, cần đầu ra có cấu trúc, số lượng vừa phải thì dùng VLM.

## Technical stack

| Nhóm | Thành phần | Ghi chú |
|---|---|---|
| Đường ống cổ điển | PaddleOCR 3.x: PP-OCRv5 và PP-OCRv6 | PP-OCRv6 là mặc định từ bản 3.7 (tháng 6/2026), ba cỡ 1,5M, 7,7M và 34,5M tham số, 50 ngôn ngữ trong một mô hình. Kiểm tra bảng ngôn ngữ để chắc có tiếng Việt cho cỡ bạn chọn |
| | [VietOCR](https://github.com/pbcquoc/vietocr) | Bộ nhận dạng dòng chữ tiếng Việt (CNN kèm Transformer hoặc Seq2Seq), in và viết tay, dễ huấn luyện |
| | docTR, EasyOCR, Tesseract (gói `vie`) | Các lựa chọn khác. Tesseract chạy CPU, yếu với ảnh chụp |
| | TrOCR | Transformer nhận dạng dòng chữ, fine-tune qua transformers |
| VLM nhỏ cho OCR | PaddleOCR-VL 1.5 và 1.6 (khoảng 0,9B, 111 ngôn ngữ) | Chuyên phân tích tài liệu |
| | DeepSeek-OCR, Qwen3-VL (2B, 4B, 8B), Qwen3.5 cỡ nhỏ (0,8B đến 9B, có thị giác), Gemma 4 E2B và E4B | VLM đa dụng, fine-tune được bằng Unsloth |
| Phát hiện vùng chữ và bố cục | DBNet (trong PaddleOCR), YOLO, PP-DocLayout | Khi cần cắt dòng hoặc cắt vùng trước |
| Thư viện | PyTorch, transformers, peft, trl, Unsloth, PaddlePaddle | Huấn luyện |
| | OpenCV, Pillow, pdf2image, PyMuPDF | Tiền xử lý ảnh, chuyển PDF thành ảnh |
| | jiwer, python-Levenshtein | Tính CER, WER |
| Gán nhãn | PPOCRLabel, Label Studio | Vẽ khung và gõ nội dung |
| Sinh dữ liệu tổng hợp | TextRecognitionDataGenerator (trdg), SynthTIGER | Sinh ảnh dòng chữ từ văn bản và phông chữ |
| Dữ liệu tiếng Việt công khai | VinText (chữ trong ảnh cảnh), MC-OCR 2021 (hoá đơn), UIT-HWDB và VNOnDB (viết tay), dữ liệu mẫu của VietOCR | Đọc giấy phép từng bộ |
| Triển khai | ONNX Runtime, OpenVINO, PaddleOCR inference, Ollama hoặc vLLM cho VLM | Tuỳ kiểu hệ thống |

## Dữ liệu đầu vào

**Cho bộ nhận dạng dòng chữ:** ảnh đã cắt sát một dòng hoặc một ô, kèm chuỗi ký tự đúng. Tệp nhãn dạng mỗi dòng một cặp, ngăn cách bằng tab:

```text
crops/000001.jpg	Công ty TNHH Hệ thống FA
crops/000002.jpg	Số lượng: 1.250 cái
```

**Cho VLM:** ảnh cả trang hoặc cả vùng, kèm đầu ra mong muốn (văn bản thuần, Markdown, hoặc JSON các trường).

**Số lượng:** 500 đến 2000 ảnh thật có nhãn là đủ để LoRA một VLM hoặc fine-tune bộ nhận dạng cho một loại giấy tờ. Huấn luyện từ đầu cần vài trăm nghìn dòng, phần lớn là dữ liệu tổng hợp.

**Chất lượng nhãn:**

- Gõ đúng từng ký tự, đúng dấu, đúng hoa thường. Dùng Unicode dựng sẵn (NFC) thống nhất, vì cùng một chữ "ế" có thể được mã hoá theo hai cách và mô hình sẽ coi là hai chuỗi khác nhau.
- Quy ước rõ cho chữ mờ không đọc được: bỏ ảnh đó ra, đừng đoán.
- Ảnh huấn luyện phải giống ảnh thật lúc dùng: cùng máy quét hoặc camera, cùng độ phân giải, cùng mức nghiêng và mờ.
- Tách train và test theo tài liệu gốc. Hai dòng cắt từ cùng một trang không được nằm ở hai phía.

**Thước đo:** CER (tỷ lệ lỗi ký tự) là chính. Với rút trường thông tin, đo thêm tỷ lệ trường đúng hoàn toàn (exact match) vì một chữ số sai trong số tiền là sai cả trường.

## Các cách làm xếp từ dễ đến khó

| # | Cách làm | Độ khó | VRAM | Dữ liệu | Khi nào dùng |
|---|---|---|---|---|---|
| 1 | Dùng thẳng PP-OCRv6, VietOCR hoặc Tesseract | Rất dễ | CPU | Không | Chữ in rõ, lấy mốc so sánh |
| 2 | Dùng thẳng VLM nhỏ (PaddleOCR-VL, Qwen3.5 cỡ nhỏ) kèm prompt mô tả đầu ra | Dễ | 4 đến 8 GB để chạy | Không | Tài liệu bố cục phức tạp |
| 3 | Cải thiện tiền xử lý: nắn nghiêng, tăng tương phản, cắt vùng, phóng to | Dễ | Không | Không | Luôn nên làm trước khi huấn luyện |
| 4 | Fine-tune bộ nhận dạng VietOCR từ trọng số có sẵn | Dễ | 4 đến 6 GB | 1000 đến 10000 dòng | Phông chữ lạ, chữ viết tay, tem nhãn |
| 5 | Fine-tune bộ nhận dạng của PaddleOCR | Trung bình | 6 đến 8 GB | 5000 dòng trở lên | Cần tốc độ cao, triển khai CPU |
| 6 | LoRA trên VLM 2B đến 4B bằng Unsloth | Trung bình | 5 đến 12 GB | 500 đến 2000 trang | Độ chính xác cao nhất cho tài liệu có cấu trúc |
| 7 | Huấn luyện bộ nhận dạng từ đầu với dữ liệu tổng hợp | Khó | 6 đến 8 GB | 200000 dòng trở lên | Bộ ký tự riêng, cần giấy phép sạch, mô hình thật bé |
| 8 | Huấn luyện cả bộ phát hiện lẫn bộ nhận dạng từ đầu | Rất khó | 8 đến 16 GB | Hàng chục nghìn trang có khung | Hiếm khi cần |

Về mức cải thiện có thể kỳ vọng: một nghiên cứu fine-tune bộ nhận dạng PP-OCRv5 cho văn bản Hán Nôm báo cáo độ chính xác khớp hoàn toàn tăng từ 37,5% lên 50,0%. Tài liệu của Unsloth cho ví dụ fine-tune DeepSeek-OCR trên tiếng Ba Tư với 60 bước huấn luyện, CER trung bình giảm từ khoảng 149% xuống khoảng 60%. Ngôn ngữ và loại tài liệu càng xa dữ liệu gốc thì fine-tune càng có lợi.

## Từng bước fine-tune mô hình thị giác ngôn ngữ bằng LoRA

Lý do chọn: cho độ chính xác cao nhất trên tài liệu thật trong tầm VRAM vừa phải, một mô hình làm cả đọc chữ lẫn rút trường. Theo tài liệu Unsloth, LoRA 16-bit trên Qwen3.5-2B cần khoảng 5 GB và bản 4B khoảng 10 GB, và họ khuyên không dùng 4-bit với Qwen3.5. Máy 8 GB chọn bản 2B, máy 12 đến 16 GB chọn bản 4B.

**Bước 1. Xác định đầu ra.** Ví dụ rút trường từ phiếu giao hàng thành JSON:

```json
{"so_phieu": "GH-2026-01542", "ngay": "2026-11-15", "nha_cung_cap": "Công ty ABC", "tong_tien": 12500000}
```

Giữ khuôn JSON cố định, cùng thứ tự khoá ở mọi mẫu. Trường không có trên giấy thì ghi `null`.

**Bước 2. Thu và gán nhãn 500 đến 2000 ảnh.** Chụp hoặc quét đúng như cách sẽ dùng. Để gán nhanh: cho một mô hình lớn sinh nhãn nháp, người kiểm tra và sửa từng mẫu. Lưu thành `train.jsonl` và `test.jsonl`, mỗi dòng có `image` (đường dẫn) và `text` (chuỗi JSON đúng). Giữ riêng 100 đến 200 ảnh làm tập test.

**Bước 3. Cài đặt.**

```bash
pip install unsloth        # kéo theo torch, transformers, peft, trl
pip install jiwer pillow
```

Qwen3.5 yêu cầu transformers bản 5 trở lên.

**Bước 4. Nạp mô hình và gắn LoRA.**

```python
from unsloth import FastVisionModel

model, tokenizer = FastVisionModel.from_pretrained(
    "unsloth/Qwen3.5-4B",          # kiểm tra tên chính xác trên Hugging Face, máy 8 GB dùng bản 2B
    load_in_4bit=False,            # Qwen3.5: dùng LoRA 16-bit
    use_gradient_checkpointing="unsloth",
)

model = FastVisionModel.get_peft_model(
    model,
    finetune_vision_layers=True,
    finetune_language_layers=True,
    finetune_attention_modules=True,
    finetune_mlp_modules=True,
    r=16, lora_alpha=16, lora_dropout=0, bias="none",
    random_state=3407,
)
```

**Bước 5. Chuyển dữ liệu sang dạng hội thoại.**

```python
import json
from PIL import Image

PROMPT = "Đọc phiếu giao hàng trong ảnh và trả về JSON gồm các khoá: so_phieu, ngay, nha_cung_cap, tong_tien."

def to_conversation(path, answer):
    return {"messages": [
        {"role": "user", "content": [
            {"type": "image", "image": Image.open(path).convert("RGB")},
            {"type": "text", "text": PROMPT}]},
        {"role": "assistant", "content": [
            {"type": "text", "text": answer}]},
    ]}

rows = [json.loads(line) for line in open("train.jsonl", encoding="utf-8")]
train_data = [to_conversation(r["image"], r["text"]) for r in rows]
```

Thu ảnh về cạnh dài khoảng 1000 đến 1500 điểm ảnh trước khi đưa vào. Ảnh quá lớn làm số token ảnh tăng vọt và hết bộ nhớ, ảnh quá nhỏ làm mất dấu tiếng Việt.

**Bước 6. Đo mô hình gốc trên tập test.** Chạy suy luận với cùng prompt, tính CER và tỷ lệ trường đúng. Ghi lại.

**Bước 7. Huấn luyện.**

```python
from unsloth.trainer import UnslothVisionDataCollator
from trl import SFTTrainer, SFTConfig

FastVisionModel.for_training(model)
trainer = SFTTrainer(
    model=model, tokenizer=tokenizer,
    data_collator=UnslothVisionDataCollator(model, tokenizer),
    train_dataset=train_data,
    args=SFTConfig(
        per_device_train_batch_size=1, gradient_accumulation_steps=8,
        warmup_ratio=0.03, num_train_epochs=2,
        learning_rate=2e-4, lr_scheduler_type="cosine",
        optim="adamw_8bit", weight_decay=0.01, max_grad_norm=0.3,
        logging_steps=10, save_steps=200, output_dir="ocr-lora",
        remove_unused_columns=False, dataset_text_field="",
        dataset_kwargs={"skip_prepare_dataset": True},
        max_length=2048, seed=3407,
    ),
)
trainer.train()
model.save_pretrained("ocr-lora-final")
```

Lần chạy đầu có thể chậm vì thư viện biên dịch nhân tính toán. Với 1000 ảnh, 2 epoch thường mất dưới hai giờ trên GPU 12 đến 16 GB.

**Bước 8. Đánh giá.**

```python
import jiwer

FastVisionModel.for_inference(model)

def predict(path):
    msgs = [{"role": "user", "content": [{"type": "image"}, {"type": "text", "text": PROMPT}]}]
    text = tokenizer.apply_chat_template(msgs, add_generation_prompt=True)
    inputs = tokenizer(Image.open(path).convert("RGB"), text,
                       add_special_tokens=False, return_tensors="pt").to("cuda")
    out = model.generate(**inputs, max_new_tokens=512, do_sample=False)
    return tokenizer.decode(out[0][inputs["input_ids"].shape[1]:], skip_special_tokens=True)

test = [json.loads(line) for line in open("test.jsonl", encoding="utf-8")]
preds = [predict(r["image"]) for r in test]
print("CER:", jiwer.cer([r["text"] for r in test], preds))
```

Ngoài CER, phân tích JSON và đếm tỷ lệ đúng từng trường. Xem tận mắt 50 mẫu sai để biết thiếu loại dữ liệu nào, bổ sung rồi huấn luyện lại.

**Bước 9. Triển khai.** Gộp adapter và xuất GGUF để chạy bằng llama.cpp hoặc Ollama, hoặc phục vụ bằng vLLM bản hỗ trợ mô hình đó. Luôn kiểm tra đầu ra bằng luật nghiệp vụ: JSON hợp lệ, ngày đúng định dạng, tổng tiền bằng tổng các dòng.

## Từng bước huấn luyện bộ nhận dạng từ đầu với VietOCR

Lý do chọn: VietOCR là bộ nhận dạng dòng chữ kiểu CNN kèm Transformer, khoảng vài chục triệu tham số, huấn luyện được trên 6 đến 8 GB, có sẵn bộ ký tự tiếng Việt và cách dùng rất gọn. Đây là mốc "bài toán dễ" của series. Cùng đoạn mã này, đổi một tham số là thành fine-tune (cách 4 trong bảng).

**Bước 1. Cài đặt.**

```bash
pip install vietocr trdg
```

**Bước 2. Sinh dữ liệu tổng hợp.** Chuẩn bị tệp `lines.txt` chứa các dòng văn bản giống miền của bạn (tên hàng, địa chỉ, mã số, số tiền), và một thư mục phông chữ có đủ dấu tiếng Việt. Dùng trdg sinh ảnh với nền, độ nghiêng và độ mờ ngẫu nhiên:

```bash
trdg -i lines.txt -c 200000 -f 48 -fd fonts/ \
     -k 3 -rk -bl 1 -rbl -b 3 -na 2 --output_dir synth/
```

Ý nghĩa các cờ có thể khác giữa các phiên bản, xem `trdg --help`. Nguyên tắc: càng nhiều phông chữ, nền và kiểu nhiễu giống thực tế càng tốt. Dữ liệu tổng hợp chỉ toàn chữ đen nền trắng sẽ cho mô hình vô dụng với ảnh chụp.

**Bước 3. Trộn dữ liệu thật.** Cắt dòng từ tài liệu thật bằng bộ phát hiện của PaddleOCR, gán nhãn bằng PPOCRLabel. Vài nghìn dòng thật trộn vào vài trăm nghìn dòng tổng hợp cải thiện rõ rệt. Tập validation và test chỉ gồm dữ liệu thật.

Tạo `train_annotation.txt` và `test_annotation.txt` theo định dạng đường dẫn, tab, nội dung như ở phần dữ liệu đầu vào.

**Bước 4. Cấu hình và huấn luyện.**

```python
from vietocr.tool.config import Cfg
from vietocr.model.trainer import Trainer

config = Cfg.load_config_from_name("vgg_transformer")   # hoặc "vgg_seq2seq": nhẹ và nhanh hơn

config["dataset"].update({
    "name": "ocr_cua_toi",
    "data_root": "./data/",
    "train_annotation": "train_annotation.txt",
    "valid_annotation": "test_annotation.txt",
    "image_height": 32, "image_min_width": 32, "image_max_width": 512,
})
config["trainer"].update({
    "batch_size": 32,
    "print_every": 200, "valid_every": 4000, "iters": 200000,
    "checkpoint": "./checkpoint/ocr_checkpoint.pth",
    "export": "./weights/ocr_cua_toi.pth",
    "metrics": 5000,
})
config["device"] = "cuda:0"
# Nếu có ký tự ngoài bộ mặc định, thêm vào: config["vocab"] += "№€"

trainer = Trainer(config, pretrained=False)   # False: khởi tạo ngẫu nhiên, True: fine-tune từ trọng số có sẵn
trainer.visualize_dataset()                   # nhìn vài mẫu để chắc ảnh và nhãn khớp nhau
trainer.train()

acc_full_seq, acc_per_char = trainer.precision()
print(acc_full_seq, acc_per_char)
```

- Từ đầu cần khoảng 100 đến 200 nghìn vòng lặp. Fine-tune chỉ cần 10 đến 20 nghìn với learning rate thấp hơn.
- Hết bộ nhớ thì giảm `batch_size` hoặc `image_max_width`.
- `acc_full_seq` là tỷ lệ dòng đúng hoàn toàn, `acc_per_char` là độ chính xác theo ký tự.

**Bước 5. Suy luận.**

```python
from PIL import Image
from vietocr.tool.predictor import Predictor

config["weights"] = "./weights/ocr_cua_toi.pth"
config["cnn"]["pretrained"] = False
config["predictor"]["beamsearch"] = False
ocr = Predictor(config)
print(ocr.predict(Image.open("crops/000001.jpg")))
```

**Bước 6. Ghép thành hệ thống.** Dùng bộ phát hiện vùng chữ của PaddleOCR để lấy khung, cắt từng dòng, đưa vào bộ nhận dạng vừa huấn luyện, rồi sắp xếp kết quả theo toạ độ. Bộ phát hiện có sẵn thường đã đủ tốt, hiếm khi phải huấn luyện lại.

**Phương án thay thế với PaddleOCR.** Nếu cần tốc độ suy luận cao trên CPU, huấn luyện bộ nhận dạng của PaddleOCR bằng `tools/train.py` với tệp cấu hình của PP-OCRv5 hoặc PP-OCRv6, cùng định dạng nhãn tab ở trên, kèm tệp từ điển ký tự tiếng Việt. Khi đổi từ điển, lớp đầu ra được khởi tạo lại nên cần nhiều dữ liệu hơn fine-tune thông thường.

## Lưu ý quan trọng

- **Tiền xử lý thường thắng huấn luyện.** Nắn nghiêng, cắt đúng vùng, đủ độ phân giải (chiều cao chữ ít nhất khoảng 20 điểm ảnh) có thể giảm một nửa lỗi mà không cần GPU.
- **Dấu tiếng Việt là điểm yếu số một.** Ảnh nén mạnh hoặc thu nhỏ làm mất dấu hỏi, ngã, nặng. Giữ ảnh đủ nét và đo riêng lỗi dấu.
- **VLM có thể bịa.** Khi ảnh mờ, mô hình sinh ra chữ nghe hợp lý nhưng không có trên giấy, nguy hiểm nhất với số tiền và mã số. Kiểm chéo bằng luật, hoặc chạy song song bộ nhận dạng cổ điển cho các trường số và so sánh.
- **Dữ liệu nhạy cảm.** Căn cước, hoá đơn, hồ sơ y tế phải được phép sử dụng và nên huấn luyện hoàn toàn trên máy nội bộ.
- **Đừng đánh giá trên dữ liệu tổng hợp.** Con số đẹp trên ảnh tự sinh không nói lên điều gì về ảnh thật.
- **Giấy phép.** PaddleOCR và VietOCR dùng giấy phép Apache 2.0. Với VLM, xem giấy phép của từng mô hình gốc.

## Nguồn tham khảo

- [Lịch sử phát hành PaddleOCR 3.0 đến 3.7](https://paddleocr.dev/releases)
- [Enhancing OCR for Sino-Vietnamese Language Processing via Fine-tuned PaddleOCRv5](https://arxiv.org/html/2510.04003v2)
- [Unsloth: DeepSeek-OCR, cách chạy và fine-tune](https://unsloth.ai/docs/models/tutorials/deepseek-ocr-how-to-run-and-fine-tune)
- [Unsloth: Qwen3.5 fine-tune](https://unsloth.ai/docs/zh/mo-xing/qwen3.5/fine-tune)
- [Hugging Face: Supercharge your OCR Pipelines with Open Models](https://huggingface.co/blog/ocr-open-models)
