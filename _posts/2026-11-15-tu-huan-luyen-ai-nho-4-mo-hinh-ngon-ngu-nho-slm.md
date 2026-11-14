---
layout: post
categories: ["Trí tuệ nhân tạo & Dữ liệu"]
title: "Tự huấn luyện mô hình AI nhỏ (4): Mô hình ngôn ngữ nhỏ (SLM) tiếng Việt"
subtitle: "QLoRA trên Gemma 4 bằng Unsloth và tự xây một GPT 34 triệu tham số từ đầu"
date: 2026-11-15 08:30:00 +0700
tags:
- AI
- SLM
- LLM
- Gemma
- Qwen
- Unsloth
- QLoRA
- Fine-tuning
series: "Tự huấn luyện mô hình AI nhỏ"
series_order: 4
---

> Bài 4 của series. Mô hình ngôn ngữ nhỏ (Small Language Model, SLM) là các mô hình từ vài trăm triệu đến khoảng 10 tỷ tham số, chạy được trên laptop hoặc điện thoại. Bài này có hai hướng dẫn: fine-tune một SLM mở cho một việc cụ thể bằng tiếng Việt, và tự huấn luyện một mô hình GPT bé từ con số 0 để hiểu bản chất. Kiến thức nền nằm ở [bài 1](/2026/11/15/tu-huan-luyen-ai-nho-1-tong-quan/). Code là khung cốt lõi, chưa chạy kiểm chứng trên GPU thật.

- [Khi nào nên fine-tune một SLM](#khi-nào-nên-fine-tune-một-slm)
- [Technical stack](#technical-stack)
- [Dữ liệu đầu vào](#dữ-liệu-đầu-vào)
- [Các cách làm xếp từ dễ đến khó](#các-cách-làm-xếp-từ-dễ-đến-khó)
- [Từng bước fine-tune Gemma 4 bằng QLoRA](#từng-bước-fine-tune-gemma-4-bằng-qlora)
- [Từng bước huấn luyện một GPT nhỏ từ đầu](#từng-bước-huấn-luyện-một-gpt-nhỏ-từ-đầu)
- [Lưu ý quan trọng](#lưu-ý-quan-trọng)
- [Nguồn tham khảo](#nguồn-tham-khảo)

## Khi nào nên fine-tune một SLM

Fine-tune dạy mô hình **cách làm** (định dạng, giọng văn, quy tắc phân loại, cách gọi công cụ). Nó không phải cách tốt để nạp **kiến thức thay đổi thường xuyên**, việc đó hợp với tra cứu tài liệu (RAG).

| Nhu cầu | Cách nên dùng |
|---|---|
| Trả lời dựa trên tài liệu nội bộ hay thay đổi | RAG, không huấn luyện |
| Đầu ra theo khuôn cố định (JSON, mã lỗi, nhãn phân loại) | Thử prompt kèm ví dụ trước, không ổn định thì fine-tune |
| Giọng văn, thuật ngữ riêng của công ty | Fine-tune |
| Việc hẹp lặp lại hàng triệu lần, cần rẻ và nhanh | Fine-tune mô hình thật nhỏ |
| Chạy ngoại tuyến trên thiết bị yếu | Fine-tune mô hình 1B đến 2B rồi lượng tử hoá |
| Suy luận nhiều bước, kiến thức rộng | Dùng mô hình lớn, SLM không hợp |

## Technical stack

| Nhóm | Thành phần | Ghi chú |
|---|---|---|
| Mô hình gốc | Gemma 4: E2B, E4B, 12B (Google, 4/2026) | Apache 2.0, hơn 140 ngôn ngữ, ngữ cảnh 128K, bản E nhận cả ảnh và âm thanh |
| | Qwen3.5 cỡ nhỏ: 0,8B, 2B, 4B, 9B (Alibaba, 3/2026) | Apache 2.0, có thị giác. Unsloth khuyên dùng LoRA 16-bit thay vì 4-bit |
| | Qwen3: 0,6B, 1,7B, 4B, 8B | Apache 2.0, 119 ngôn ngữ, bật tắt được chế độ suy nghĩ |
| | Phi-4-mini (3,8B), SmolLM3 (3B), Ministral 3 (3B, 8B, 14B), Granite 4.1 (3B, 8B) | Các lựa chọn khác, giấy phép mở |
| | Mô hình đã chuyên tiếng Việt: Vistral, PhoGPT, VinaLLaMA, SeaLLMs | Phần lớn dựa trên thế hệ mô hình cũ hơn. So sánh với Gemma 4 và Qwen3.5 trên dữ liệu của bạn trước khi chọn |
| Công cụ fine-tune | Unsloth | Nhanh, ít VRAM, có sổ tay Colab cho từng mô hình |
| | transformers, peft, trl, bitsandbytes | Bộ thư viện gốc, linh hoạt nhất |
| | LLaMA-Factory, Axolotl | Cấu hình bằng giao diện hoặc YAML |
| | MLX-LM | Cho máy Mac chip Apple Silicon |
| Dữ liệu | datasets, Distilabel | Nạp, xử lý và sinh dữ liệu tổng hợp |
| | Argilla, Label Studio | Rà soát và sửa mẫu |
| Dữ liệu tiếng Việt công khai | Wikipedia tiếng Việt, kho tin tức, UIT-ViQuAD (hỏi đáp), các bản dịch Alpaca sang tiếng Việt | Đọc giấy phép từng bộ. Dữ liệu dịch máy thường có chất lượng không đều |
| Đánh giá | Bộ câu hỏi riêng của bạn là chính. Bộ chuẩn công khai: VMLU | Chấm tự động bằng so khớp hoặc bằng một mô hình lớn làm giám khảo |
| Triển khai | llama.cpp và Ollama (GGUF), vLLM, LM Studio | GGUF mức Q4_K_M là điểm cân bằng phổ biến |
| Huấn luyện từ đầu | tokenizers, transformers (GPT2Config), hoặc nanoGPT | Tự xây bộ tách từ và mô hình |

## Dữ liệu đầu vào

Định dạng phổ biến nhất là JSONL, mỗi dòng một cuộc hội thoại:

```json
{"messages": [{"role": "system", "content": "Bạn là trợ lý phân loại yêu cầu bảo trì."}, {"role": "user", "content": "Băng tải số 3 kêu to và rung mạnh từ sáng nay."}, {"role": "assistant", "content": "{\"loai\": \"co_khi\", \"muc_do\": \"cao\", \"thiet_bi\": \"bang_tai_3\"}"}]}
```

- **Số lượng:** 200 đến 500 mẫu tốt cho việc định dạng đơn giản, 1000 đến 5000 cho phân loại nhiều lớp hoặc giọng văn, hơn 10000 cho việc phức tạp.
- **Nguồn:** nhật ký thật đã ẩn danh là tốt nhất. Thiếu thì dùng mô hình lớn sinh dữ liệu tổng hợp từ vài chục mẫu thật, rồi người rà lại. Đây chính là chưng cất: mô hình lớn làm thầy, mô hình nhỏ làm trò.
- **Đa dạng:** phủ đủ các trường hợp biên, câu sai chính tả, câu không dấu, câu lẫn tiếng Anh. Thêm cả các câu mà mô hình nên từ chối hoặc trả lời "không đủ thông tin".
- **Nhất quán:** cùng một kiểu đầu vào phải có cùng kiểu đầu ra. Mô hình nhỏ học rất nhanh cả những mâu thuẫn trong nhãn.
- **Tách tập:** 80% huấn luyện, 10% validation, 10% test. Tập test không được chứa mẫu gần trùng với tập huấn luyện.
- **Ẩn danh:** xoá tên, số điện thoại, số tài khoản trước khi huấn luyện.

Với huấn luyện từ đầu, dữ liệu là **văn bản thô**: vài trăm MB đến vài GB tiếng Việt sạch.

## Các cách làm xếp từ dễ đến khó

| # | Cách làm | Độ khó | VRAM | Dữ liệu | Ghi chú |
|---|---|---|---|---|---|
| 1 | Prompt kèm ví dụ, chạy bằng Ollama | Rất dễ | 2 đến 8 GB | 3 đến 10 ví dụ | Luôn làm trước để có mốc |
| 2 | RAG trên tài liệu riêng | Dễ | 2 đến 8 GB | Tài liệu | Không huấn luyện |
| 3 | LoRA trên mô hình dưới 1B (Qwen3.5-0.8B, Qwen3-0.6B) | Dễ | 3 đến 4 GB | 500 mẫu trở lên | Việc hẹp, cần tốc độ |
| 4 | LoRA trên mô hình 2B (Gemma 4 E2B, Qwen3.5-2B) | Dễ | 5 đến 8 GB | 500 đến 5000 | Mốc 8 GB của series |
| 5 | QLoRA trên Gemma 4 E4B hoặc LoRA trên Qwen3.5-4B | Trung bình | 10 đến 12 GB | 1000 đến 10000 | Cân bằng tốt nhất giữa chất lượng và VRAM |
| 6 | LoRA trên mô hình 9B đến 12B | Trung bình | 16 đến 24 GB | 1000 đến 10000 | Khi 4B chưa đủ thông minh |
| 7 | Fine-tune toàn bộ mô hình dưới 1B | Trung bình | 8 đến 12 GB | 10000 trở lên | Unsloth ước lượng cần khoảng 4 lần VRAM của LoRA |
| 8 | Huấn luyện tiếp trên văn bản thô (continued pretraining) rồi mới fine-tune | Khó | 12 đến 24 GB | Hàng trăm MB văn bản miền | Khi miền có nhiều thuật ngữ lạ |
| 9 | Chưng cất từ mô hình lớn sang mô hình nhỏ | Khó | Như cách 4 đến 7 | Hàng chục nghìn mẫu sinh tự động | Chất lượng phụ thuộc mô hình thầy |
| 10 | Huấn luyện từ đầu mô hình 10 đến 100 triệu tham số | Khó | 6 đến 8 GB | Vài trăm MB văn bản | Để học, hoặc cho việc cực hẹp |
| 11 | Huấn luyện từ đầu mô hình hàng tỷ tham số | Rất khó | Cụm GPU | Hàng trăm GB văn bản | Ngoài phạm vi cá nhân |

## Từng bước fine-tune Gemma 4 bằng QLoRA

Lý do chọn: Gemma 4 dùng giấy phép Apache 2.0, hỗ trợ tiếng Việt, và Unsloth có hướng dẫn riêng. Tài liệu của Unsloth khuyên **ưu tiên QLoRA trên E4B hơn LoRA trên E2B** vì mất mát do lượng tử hoá là nhỏ. Về VRAM, tài liệu ghi E2B huấn luyện được trên 8 GB. Với E4B, phần giới thiệu ghi khoảng 10 GB còn một mục khác ghi LoRA cần 17 GB, có thể hiểu là 4-bit khoảng 10 GB và 16-bit khoảng 17 GB. Vì vậy: máy 8 GB dùng E2B, máy 12 đến 16 GB dùng E4B ở chế độ 4-bit.

**Bước 1. Lấy mốc.** Chạy mô hình gốc trên tập test với prompt tốt nhất bạn viết được, ghi lại tỷ lệ đúng.

```bash
ollama run gemma4:e4b   # tên thẻ có thể khác, xem thư viện mô hình của Ollama
```

**Bước 2. Cài đặt.**

```bash
pip install unsloth
```

**Bước 3. Nạp mô hình 4-bit.**

```python
from unsloth import FastModel

model, tokenizer = FastModel.from_pretrained(
    model_name="unsloth/gemma-4-E4B-it",   # kiểm tra tên trên Hugging Face, máy 8 GB dùng unsloth/gemma-4-E2B-it
    max_seq_length=2048,
    load_in_4bit=True,
    full_finetuning=False,
)
```

`max_seq_length` nên vừa đủ phủ mẫu dài nhất của bạn. Con số nhỏ hơn tiết kiệm VRAM đáng kể.

**Bước 4. Gắn LoRA.**

```python
model = FastModel.get_peft_model(
    model,
    finetune_vision_layers=False,      # chỉ huấn luyện phần văn bản
    finetune_language_layers=True,
    finetune_attention_modules=True,
    finetune_mlp_modules=True,
    r=16, lora_alpha=16, lora_dropout=0, bias="none",
    random_state=3407,
)
```

Tài liệu Unsloth dùng `r=8` làm mặc định. Tăng lên 16 hoặc 32 nếu việc phức tạp và dữ liệu trên vài nghìn mẫu. Giảm nếu thấy học vẹt.

**Bước 5. Chuẩn bị dữ liệu theo khuôn hội thoại của Gemma 4.**

```python
from datasets import load_dataset
from unsloth.chat_templates import get_chat_template

tokenizer = get_chat_template(tokenizer, chat_template="gemma-4")   # khuôn không suy nghĩ cho mô hình nhỏ

ds = load_dataset("json", data_files={"train": "train.jsonl", "validation": "val.jsonl"})

def to_text(batch):
    texts = [tokenizer.apply_chat_template(m, tokenize=False, add_generation_prompt=False)
             for m in batch["messages"]]
    return {"text": texts}

ds = ds.map(to_text, batched=True)
print(ds["train"][0]["text"])   # nhìn tận mắt một mẫu sau khi áp khuôn
```

Luôn in một mẫu ra xem. Sai khuôn hội thoại là lỗi phổ biến nhất và không gây báo lỗi, chỉ làm mô hình kém đi.

**Bước 6. Huấn luyện.**

```python
from trl import SFTTrainer, SFTConfig
from unsloth.chat_templates import train_on_responses_only

trainer = SFTTrainer(
    model=model, tokenizer=tokenizer,
    train_dataset=ds["train"], eval_dataset=ds["validation"],
    args=SFTConfig(
        dataset_text_field="text",
        per_device_train_batch_size=1, gradient_accumulation_steps=4,
        warmup_steps=5, num_train_epochs=2,
        learning_rate=2e-4, lr_scheduler_type="linear",
        optim="adamw_8bit", weight_decay=0.001,
        logging_steps=10, eval_strategy="steps", eval_steps=100,
        output_dir="gemma4-vi-lora", seed=3407,
    ),
)
# Chỉ tính loss trên phần trả lời của trợ lý
trainer = train_on_responses_only(
    trainer,
    instruction_part="<|turn>user\n",
    response_part="<|turn>model\n",
)
trainer.train()
```

- Theo tài liệu Unsloth, loss của E2B và E4B ở mức khoảng 13 đến 15 là bình thường vì đây là mô hình đa phương thức. Loss hàng trăm thường do xử lý gradient accumulation sai.
- Với lần chạy dài, giảm learning rate xuống 2e-5.
- Dừng khi loss validation ngừng giảm. Với 1000 đến 3000 mẫu, 1 đến 3 epoch là đủ.

**Bước 7. Đánh giá trên tập test.**

```python
def ask(messages, max_new_tokens=256):
    inputs = tokenizer.apply_chat_template(messages, add_generation_prompt=True,
                                           return_tensors="pt", return_dict=True).to("cuda")
    out = model.generate(**inputs, max_new_tokens=max_new_tokens, do_sample=False)
    return tokenizer.decode(out[0][inputs["input_ids"].shape[1]:], skip_special_tokens=True)

test = load_dataset("json", data_files="test.jsonl")["train"]
correct = sum(ask(r["messages"][:-1]).strip() == r["messages"][-1]["content"].strip() for r in test)
print("Tỷ lệ đúng:", correct / len(test))
```

So với mốc ở bước 1. Với đầu ra tự do (tóm tắt, viết lại), so khớp chuỗi không dùng được, hãy cho một mô hình lớn chấm theo thang điểm kèm tiêu chí rõ, và tự đọc ít nhất 50 mẫu.

**Bước 8. Xuất GGUF và chạy bằng Ollama.**

```python
model.save_pretrained("gemma4-vi-lora-final")       # adapter, vài chục MB
tokenizer.save_pretrained("gemma4-vi-lora-final")
model.save_pretrained_gguf("gemma4-vi-gguf", tokenizer, quantization_method="q4_k_m")
```

```bash
cat > Modelfile <<'EOF'
FROM ./gemma4-vi-gguf/model.gguf
PARAMETER temperature 0.2
EOF
ollama create gemma4-vi -f Modelfile
ollama run gemma4-vi "Băng tải số 3 kêu to và rung mạnh từ sáng nay."
```

Tên tệp GGUF thực tế có thể khác, xem trong thư mục xuất ra. Nếu mô hình chạy trong Ollama kém hơn hẳn lúc đánh giá, nguyên nhân thường là khuôn hội thoại hoặc ký hiệu kết thúc không khớp với lúc huấn luyện. Đo lại trên tập test sau khi lượng tử hoá.

**Nếu chọn Qwen3.5 thay cho Gemma 4:** dùng `FastLanguageModel` với `load_in_4bit=False, load_in_16bit=True`. Theo Unsloth, LoRA 16-bit cần khoảng 3 GB cho bản 0,8B, 5 GB cho 2B, 10 GB cho 4B và 22 GB cho 9B. Cần transformers bản 5.

## Từng bước huấn luyện một GPT nhỏ từ đầu

Mục tiêu là một mô hình khoảng 34 triệu tham số viết được tiếng Việt trôi chảy ở mức câu. Nó sẽ không trả lời câu hỏi hay làm theo chỉ dẫn như các mô hình ở phần trên. Giá trị của nó là để hiểu toàn bộ đường ống (bộ tách từ, kiến trúc, vòng huấn luyện, sinh văn bản) và làm nền cho các việc cực hẹp. Chạy được trên GPU 8 GB.

**Bước 1. Cài đặt và lấy văn bản.**

```bash
pip install torch transformers datasets tokenizers accelerate
```

```python
from datasets import load_dataset

wiki = load_dataset("wikimedia/wikipedia", "20231101.vi", split="train")
wiki = wiki.filter(lambda x: len(x["text"]) > 500)
wiki = wiki.train_test_split(test_size=0.005, seed=42)

with open("corpus.txt", "w", encoding="utf-8") as f:
    for row in wiki["train"]:
        f.write(row["text"].replace("\n\n", "\n") + "\n")
```

Wikipedia tiếng Việt có nhiều bài tạo tự động rất ngắn nên cần lọc. Thêm văn bản tin tức hoặc truyện nếu muốn giọng văn đa dạng hơn.

**Bước 2. Huấn luyện bộ tách từ riêng.** Bộ tách từ của mô hình tiếng Anh cắt tiếng Việt có dấu rất vụn. Bộ tách từ riêng với 16000 mảnh sẽ gọn hơn nhiều.

```python
from tokenizers import ByteLevelBPETokenizer
from transformers import PreTrainedTokenizerFast

bpe = ByteLevelBPETokenizer()
bpe.train(files=["corpus.txt"], vocab_size=16000, min_frequency=2,
          special_tokens=["<s>", "<pad>", "</s>", "<unk>"])
bpe.save("tokenizer.json")

tokenizer = PreTrainedTokenizerFast(tokenizer_file="tokenizer.json",
    bos_token="<s>", eos_token="</s>", pad_token="<pad>", unk_token="<unk>")
print(tokenizer.tokenize("Hôm nay trời đẹp quá, chúng ta đi dạo nhé."))
```

**Bước 3. Mã hoá và cắt thành khối 512 token.**

```python
BLOCK = 512

def tokenize(batch):
    return tokenizer([t + "</s>" for t in batch["text"]])

def group(batch):
    ids = sum(batch["input_ids"], [])
    n = (len(ids) // BLOCK) * BLOCK
    chunks = [ids[i:i + BLOCK] for i in range(0, n, BLOCK)]
    return {"input_ids": chunks, "labels": [c[:] for c in chunks]}

tok = wiki.map(tokenize, batched=True, remove_columns=wiki["train"].column_names, num_proc=4)
lm = tok.map(group, batched=True, remove_columns=tok["train"].column_names, num_proc=4)
```

**Bước 4. Định nghĩa mô hình.**

```python
from transformers import GPT2Config, GPT2LMHeadModel

config = GPT2Config(
    vocab_size=tokenizer.vocab_size, n_positions=BLOCK,
    n_embd=512, n_layer=8, n_head=8,
    bos_token_id=tokenizer.bos_token_id, eos_token_id=tokenizer.eos_token_id,
)
model = GPT2LMHeadModel(config)      # khởi tạo ngẫu nhiên
print(sum(p.numel() for p in model.parameters()) / 1e6, "triệu tham số")   # khoảng 34
```

Tám khối Transformer, mỗi khối khoảng 3 triệu tham số, cộng bảng embedding khoảng 8 triệu. Muốn bé hơn thì giảm `n_layer` xuống 6 và `n_embd` xuống 384 (khoảng 17 triệu).

**Bước 5. Huấn luyện.**

```python
from transformers import Trainer, TrainingArguments, default_data_collator

args = TrainingArguments(
    output_dir="gpt-vi-34m",
    per_device_train_batch_size=32, gradient_accumulation_steps=2,
    learning_rate=5e-4, lr_scheduler_type="cosine", warmup_steps=1000,
    weight_decay=0.1, num_train_epochs=3, fp16=True,
    eval_strategy="steps", eval_steps=2000, save_steps=2000, logging_steps=100,
    report_to=["tensorboard"],
)
trainer = Trainer(model=model, args=args, data_collator=default_data_collator,
                  train_dataset=lm["train"], eval_dataset=lm["test"])
trainer.train()
```

- Mẹo kiểm tra đường ống: huấn luyện trên 200 khối trong vài phút, loss phải rơi xuống gần 0. Nếu không, dữ liệu hoặc nhãn đang sai.
- Loss ban đầu khoảng 9,7 (logarit tự nhiên của 16000). Sau vài nghìn bước sẽ xuống quanh 5, và với đủ dữ liệu sẽ về khoảng 3 đến 3,5. Perplexity bằng e mũ loss.
- Hết bộ nhớ: giảm batch xuống 16, tăng `gradient_accumulation_steps` lên 4.
- Thời gian: tuỳ lượng văn bản, từ vài giờ đến hơn một ngày trên GPU 8 GB.

**Bước 6. Sinh văn bản.**

```python
import torch

model.eval()
ids = tokenizer("Hà Nội là", return_tensors="pt").input_ids.to(model.device)
with torch.no_grad():
    out = model.generate(ids, max_new_tokens=100, do_sample=True,
                         temperature=0.8, top_k=50, repetition_penalty=1.1)
print(tokenizer.decode(out[0], skip_special_tokens=True))
```

Câu sinh ra sẽ đúng ngữ pháp và nghe như Wikipedia, nhưng nội dung thường sai sự thật. Đó là giới hạn tự nhiên của mô hình cỡ này.

**Bước 7. Đi tiếp.**

- **Dạy làm theo chỉ dẫn:** fine-tune tiếp trên dữ liệu hội thoại với các ký hiệu đặc biệt tự định nghĩa cho vai người dùng và trợ lý.
- **Việc cực hẹp:** huấn luyện cùng kiến trúc này trên dữ liệu chuyên biệt, ví dụ sửa lỗi dấu tiếng Việt, sinh mã sản phẩm, gợi ý từ tiếp theo. Ở việc hẹp, mô hình vài chục triệu tham số có thể rất tốt.
- **Chưng cất:** cho một mô hình lớn sinh hàng trăm nghìn ví dụ cho việc hẹp đó và huấn luyện mô hình bé trên chúng.
- **Kiến trúc hiện đại hơn:** thay mã hoá vị trí bằng RoPE, chuẩn hoá bằng RMSNorm, hàm kích hoạt SwiGLU. Đọc mã nanoGPT để thấy toàn bộ mô hình trong vài trăm dòng.

## Lưu ý quan trọng

- **Fine-tune không sửa được dữ liệu tồi.** Dành phần lớn thời gian cho việc đọc và sửa mẫu.
- **Quên kiến thức cũ.** Fine-tune mạnh trên việc hẹp làm mô hình kém đi ở việc khác. Nếu cần giữ khả năng chung, trộn thêm một phần dữ liệu hội thoại tổng quát và dùng rank thấp.
- **Chế độ suy nghĩ.** Với mô hình có chế độ suy nghĩ, Unsloth khuyên giữ ít nhất khoảng 75% mẫu có phần suy luận nếu muốn bảo toàn khả năng đó. Nếu không cần, huấn luyện toàn mẫu trả lời trực tiếp và dùng khuôn không suy nghĩ.
- **Khuôn hội thoại phải khớp** giữa lúc huấn luyện, lúc đánh giá và lúc triển khai.
- **Lượng tử hoá sau khi đánh giá, rồi đánh giá lại.** Q4_K_M thường mất rất ít, nhưng với mô hình dưới 1B thì mất nhiều hơn, khi đó dùng Q8.
- **Tiếng Việt không dấu và lẫn tiếng Anh** xuất hiện rất nhiều trong dữ liệu thật. Đưa chúng vào tập huấn luyện nếu người dùng của bạn gõ như vậy.
- **Giấy phép.** Gemma 4, Qwen3.5 và Qwen3 dùng Apache 2.0. Một số mô hình nhỏ khác chỉ cho phép phi thương mại, ví dụ Tiny Aya của Cohere.
- **An toàn.** Mô hình fine-tune thừa hưởng và có thể làm yếu các rào chắn của mô hình gốc. Kiểm thử với các đầu vào ác ý trước khi mở cho người dùng.

## Nguồn tham khảo

- [Unsloth: Gemma 4 Fine-tuning Guide](https://unsloth.ai/docs/models/gemma-4/train)
- [Unsloth: Qwen3.5 fine-tune](https://unsloth.ai/docs/zh/mo-xing/qwen3.5/fine-tune)
- [Gemma 4 và Qwen 3.5, 3.6, 3.8: so sánh (Codersera)](https://codersera.com/blog/gemma-3-vs-qwen-3-in-depth-comparison-of-two-leading-open-source-llms/)
- [Small Language Models in 2026: 10 to Know (Turing Post)](https://www.turingpost.com/p/slmslist)
- [Qwen3.5-0.8B trên Hugging Face](https://huggingface.co/Qwen/Qwen3.5-0.8B)
