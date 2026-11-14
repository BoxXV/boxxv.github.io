---
layout: post
categories: ["Trí tuệ nhân tạo & Dữ liệu"]
title: "Tự huấn luyện mô hình AI nhỏ (2): Text-to-Speech, Voice Clone và ASR tiếng Việt"
subtitle: "Fine-tune F5-TTS và Whisper, huấn luyện từ đầu Piper và Conformer-CTC"
date: 2026-11-15 08:10:00 +0700
tags:
- AI
- Text-to-Speech
- Voice Clone
- ASR
- Whisper
- F5-TTS
- Piper
- Fine-tuning
series: "Tự huấn luyện mô hình AI nhỏ"
series_order: 2
---

> Bài 2 của series. Hai chiều của giọng nói: chữ thành tiếng (TTS, kèm nhân bản giọng) và tiếng thành chữ (ASR). Mỗi chiều có một bảng các cách làm từ dễ đến khó, rồi hai hướng dẫn từng bước: fine-tune và huấn luyện từ đầu. Kiến thức nền về LoRA và VRAM nằm ở [bài 1](/2026/11/15/tu-huan-luyen-ai-nho-1-tong-quan/). Code là khung cốt lõi, chưa chạy kiểm chứng trên GPU thật.

- [Technical stack](#technical-stack)
- [Dữ liệu đầu vào](#dữ-liệu-đầu-vào)
- [Các cách làm TTS và nhân bản giọng](#các-cách-làm-tts-và-nhân-bản-giọng)
- [Từng bước fine-tune F5-TTS theo giọng riêng](#từng-bước-fine-tune-f5-tts-theo-giọng-riêng)
- [Từng bước huấn luyện Piper từ đầu](#từng-bước-huấn-luyện-piper-từ-đầu)
- [Các cách làm ASR](#các-cách-làm-asr)
- [Từng bước fine-tune Whisper bằng LoRA](#từng-bước-fine-tune-whisper-bằng-lora)
- [Từng bước huấn luyện ASR từ đầu với Conformer-CTC](#từng-bước-huấn-luyện-asr-từ-đầu-với-conformer-ctc)
- [Lưu ý quan trọng](#lưu-ý-quan-trọng)
- [Nguồn tham khảo](#nguồn-tham-khảo)

## Technical stack

| Nhóm | Thành phần | Ghi chú |
|---|---|---|
| Mô hình TTS mở | F5-TTS và bản [F5-TTS-Vietnamese](https://github.com/nguyenthienhy/F5-TTS-Vietnamese) (giấy phép mã nguồn MIT) | Flow matching, nhân bản giọng từ vài giây mẫu. Bản tiếng Việt được fine-tune trên khoảng 1000 giờ |
| | [VieNeu-TTS](https://huggingface.co/pnnbao-ump/vieneu-tts) 0.5B và 0.3B | Chuyên tiếng Việt, chạy được trên CPU qua GGUF, nhân bản giọng từ 3 đến 5 giây. Bản 0.5B Apache 2.0, bản 0.3B chỉ phi thương mại |
| | Piper (VITS) | Rất nhẹ, chạy thời gian thực trên CPU và Raspberry Pi, mỗi mô hình một giọng |
| | ZipVoice, XTTS-v2, Kokoro, StyleTTS 2 | Các lựa chọn khác, mức hỗ trợ tiếng Việt khác nhau |
| Mô hình ASR mở | Whisper (tiny đến large-v3, large-v3-turbo 809M), giấy phép MIT | Đa ngôn ngữ, có tiếng Việt, dễ fine-tune nhất |
| | PhoWhisper (VinAI), 5 cỡ từ tiny đến large | Whisper đã fine-tune trên 844 giờ tiếng Việt nhiều vùng miền |
| | wav2vec 2.0 tiếng Việt, Conformer và FastConformer (NeMo), Zipformer (k2) | Mô hình CTC hoặc transducer, nhẹ, hợp truyền phát thời gian thực |
| | Qwen3-ASR, Parakeet, Nemotron ASR, Cohere Transcribe | Mới và mạnh ở tiếng Anh, tiếng Trung. Kiểm tra danh sách ngôn ngữ trước khi dùng cho tiếng Việt |
| Thư viện | PyTorch, torchaudio, transformers, datasets, peft, accelerate | Nền chung |
| | faster-whisper (CTranslate2), whisperX | Suy luận nhanh, căn chỉnh thời gian từng từ |
| | NVIDIA NeMo, icefall (k2), ESPnet | Huấn luyện ASR từ đầu |
| | jiwer | Tính WER, CER |
| Xử lý âm thanh | ffmpeg, sox, Audacity | Chuyển định dạng, cắt, chuẩn hoá âm lượng |
| | Silero VAD, pyannote | Tách đoạn có tiếng nói, tách người nói |
| | Demucs, UVR, DeepFilterNet | Tách nhạc nền, khử nhiễu |
| Chuẩn hoá văn bản | Tự viết luật, hoặc thư viện như vinorm, underthesea | Đọc số, ngày tháng, viết tắt, từ mượn thành chữ |
| Dữ liệu tiếng Việt công khai | VIVOS (khoảng 15 giờ), Common Voice tiếng Việt, FLEURS, VLSP | Nhỏ, sạch, hợp để đánh giá |
| | Bud500 (khoảng 500 giờ), viVoice (khoảng 1000 giờ), PhoAudiobook, VieNeu-TTS-1000h, GigaSpeech 2 | Lớn. Nhiều bộ chỉ cho phép nghiên cứu, đọc giấy phép từng bộ |

## Dữ liệu đầu vào

**Cho TTS và nhân bản giọng**

- Tệp WAV mono, 22,05 kHz hoặc 24 kHz, 16-bit, mỗi đoạn 2 đến 15 giây, một người nói.
- Thu trong phòng yên tĩnh, cùng một micro, cùng khoảng cách. Không nhạc nền, không vang.
- Bản chép lời khớp từng chữ với âm thanh, kể cả từ đệm. Số và viết tắt được viết ra thành chữ như cách đọc.
- Lượng dữ liệu: 3 đến 10 giây cho nhân bản zero-shot, 30 phút đến 2 giờ để fine-tune một giọng, 10 đến 20 giờ để huấn luyện từ đầu một giọng.

**Cho ASR**

- Tệp âm thanh 16 kHz mono, mỗi đoạn dưới 30 giây (giới hạn cửa sổ của Whisper), kèm bản chép lời.
- Âm thanh nên giống điều kiện sử dụng thật: cùng loại micro, cùng mức nhiễu, cùng vùng miền, cùng thuật ngữ.
- Lượng dữ liệu: 5 đến 20 giờ đủ để LoRA thích nghi theo miền, vài trăm giờ trở lên để huấn luyện từ đầu.
- Thống nhất quy ước chép lời: chữ thường hay có hoa, có dấu câu hay không, số viết bằng chữ hay chữ số. Quy ước lẫn lộn là nguồn lỗi WER lớn nhất.

Mẹo tạo dữ liệu nhanh: dùng một mô hình ASR mạnh chép lời tự động, sau đó người nghe lại và sửa. Nhanh hơn chép tay từ đầu khoảng 5 đến 10 lần.

## Các cách làm TTS và nhân bản giọng

| # | Cách làm | Độ khó | VRAM | Dữ liệu | Chất lượng |
|---|---|---|---|---|---|
| 1 | Nhân bản zero-shot bằng VieNeu-TTS hoặc F5-TTS-Vietnamese, không huấn luyện | Rất dễ | CPU đến 4 GB | 3 đến 10 giây giọng mẫu | Giống giọng khá, ngữ điệu đôi khi lệch |
| 2 | LoRA trên VieNeu-TTS theo hướng dẫn trong thư mục `finetune` của dự án | Dễ | Khoảng 8 GB (ước lượng) | 30 phút đến vài giờ | Tốt, mô hình vẫn nhẹ |
| 3 | Fine-tune Piper (VITS) từ checkpoint có sẵn | Trung bình | 6 đến 8 GB | 1 đến 2 giờ | Rõ ràng, ổn định, ít biểu cảm |
| 4 | Fine-tune F5-TTS-Vietnamese theo một giọng | Trung bình | 12 đến 16 GB | 1 đến 10 giờ | Cao nhất trong các cách vừa sức |
| 5 | Huấn luyện Piper từ đầu, một giọng | Khó | 8 GB, vài ngày | 10 đến 20 giờ | Tốt nếu dữ liệu sạch |
| 6 | Huấn luyện F5-TTS hoặc mô hình tương tự từ đầu cho nhiều giọng | Rất khó | Nhiều GPU 24 GB trở lên, nhiều tuần | Hàng trăm đến hàng nghìn giờ | Ngoài phạm vi máy cá nhân |

Luôn thử cách 1 trước. Mã dùng thư viện `vieneu` rất ngắn:

```python
from vieneu import Vieneu

tts = Vieneu()
audio = tts.infer(text="Xin chào, đây là giọng đọc thử nghiệm.")
tts.save(audio, "output.wav")
```

Nếu giọng zero-shot đã đủ giống thì không cần huấn luyện. Phần dưới dành cho khi bạn cần giọng ổn định qua hàng giờ nội dung.

## Từng bước fine-tune F5-TTS theo giọng riêng

Lý do chọn: bắt đầu từ checkpoint đã biết tiếng Việt, chỉ cần vài giờ dữ liệu, cho giọng tự nhiên nhất trong tầm 12 đến 16 GB.

**Bước 1. Thu và cắt dữ liệu.** Thu 1 đến 3 giờ đọc văn bản đa dạng (tin tức, hội thoại, câu hỏi, câu cảm thán). Dùng Silero VAD hoặc Audacity cắt thành đoạn 3 đến 12 giây tại chỗ ngắt hơi.

```bash
# Chuẩn hoá mọi tệp về WAV mono 24 kHz, cân âm lượng
mkdir -p data/giong_toi/wavs
for f in raw/*.wav; do
  ffmpeg -y -i "$f" -ac 1 -ar 24000 -af loudnorm=I=-23:LRA=7:TP=-2 "data/giong_toi/wavs/$(basename "$f")"
done
```

**Bước 2. Chép lời và chuẩn hoá văn bản.** Chép tự động rồi sửa tay. Tạo `data/giong_toi/metadata.csv`:

```text
audio_file|text
wavs/0001.wav|hôm nay là ngày mười lăm tháng mười một năm hai nghìn không trăm hai mươi sáu
wavs/0002.wav|bạn có muốn uống một tách cà phê không
```

Viết số, ngày tháng, đơn vị, từ viết tắt thành chữ đúng như cách đọc. Loại các đoạn có tiếng ồn, nói vấp, hoặc bản chép lời không chắc chắn.

**Bước 3. Cài đặt.**

```bash
git clone https://github.com/nguyenthienhy/F5-TTS-Vietnamese
cd F5-TTS-Vietnamese
python -m venv .venv && source .venv/bin/activate   # Python 3.10
pip install torch torchaudio      # chọn bản khớp CUDA của máy
pip install -e .
sudo apt install -y sox ffmpeg
```

Tải checkpoint tiếng Việt và tệp `vocab.txt` đi kèm từ trang Hugging Face của tác giả (có bản yêu cầu đồng ý điều khoản trước khi tải).

**Bước 4. Chuẩn bị đặc trưng và kiểm tra bộ ký tự.** Kho mã có sẵn `fine_tuning.sh` gói các bước: tạo metadata, kiểm tra ký tự nào trong dữ liệu chưa có trong bộ từ vựng của checkpoint, mở rộng lớp embedding nếu cần, trích đặc trưng, rồi huấn luyện. Mở tệp này, sửa đường dẫn dữ liệu và checkpoint, rồi chạy từng khối một lần đầu để hiểu.

Nếu dùng kho F5-TTS gốc, bước tương đương là:

```bash
python src/f5_tts/train/datasets/prepare_csv_wavs.py data/giong_toi data/giong_toi_char
```

**Bước 5. Huấn luyện.**

```bash
python src/f5_tts/train/finetune_cli.py \
  --exp_name F5TTS_Base \
  --dataset_name giong_toi \
  --finetune \
  --pretrain ckpts/vi/model_last.pt \
  --tokenizer custom --tokenizer_path ckpts/vi/vocab.txt \
  --learning_rate 1e-5 \
  --batch_size_type frame --batch_size_per_gpu 1600 \
  --grad_accumulation_steps 2 \
  --epochs 50 \
  --num_warmup_updates 200 \
  --save_per_updates 1000 \
  --log_samples
```

- `--exp_name` phải khớp kiến trúc của checkpoint (bản Base hoặc v1 Base). Sai tên sẽ báo lệch kích thước trọng số.
- `--batch_size_per_gpu` tính theo số khung âm thanh. 1600 hợp với 12 GB, 3200 với 16 đến 24 GB. Hết bộ nhớ thì giảm một nửa và tăng `--grad_accumulation_steps`.
- Learning rate thấp (1e-5) để không phá kiến thức tiếng Việt sẵn có.
- Có thể dùng giao diện `f5-tts_finetune-gradio` nếu không muốn gõ lệnh.

**Bước 6. Nghe thử và chọn checkpoint.** Với `--log_samples`, mỗi lần lưu sẽ kèm mẫu âm thanh. Nghe trên 20 câu cố định chưa có trong dữ liệu: câu dài, câu hỏi, câu có số, tên riêng, từ tiếng Anh. Chọn checkpoint nghe tự nhiên nhất, không nhất thiết là cái cuối. Huấn luyện quá lâu trên ít dữ liệu làm giọng đều đều và hay nuốt chữ.

**Bước 7. Suy luận.** Dùng một đoạn mẫu dưới 10 giây, rõ, kèm đúng bản chép lời của đoạn đó. Nếu để trống bản chép lời, công cụ sẽ tự chép bằng Whisper và có thể sai với tiếng Việt, làm giảm chất lượng. Với văn bản dài, tách thành câu khoảng 20 từ rồi ghép âm thanh lại.

**Đánh giá.** Độ rõ: cho mô hình ASR chép lại âm thanh sinh ra và tính WER so với văn bản gốc. Độ giống giọng: so embedding người nói (ví dụ bằng mô hình ECAPA) hoặc cho 5 người nghe chấm điểm 1 đến 5.

## Từng bước huấn luyện Piper từ đầu

Lý do chọn: VITS trong Piper chỉ khoảng 15 đến 30 triệu tham số, huấn luyện được trên 8 GB, kết quả chạy thời gian thực trên CPU. Cái giá là cần nhiều dữ liệu một giọng và vài ngày huấn luyện.

**Bước 1. Dữ liệu.** 10 đến 20 giờ một người đọc, WAV mono 22,05 kHz. Tệp `metadata.csv` không có dòng tiêu đề:

```text
0001.wav|Hôm nay trời đẹp quá.
0002.wav|Bạn đã ăn cơm chưa?
```

Piper dùng espeak-ng để chuyển chữ thành âm vị, nên giữ dấu câu và không cần tự phiên âm. Số vẫn nên viết thành chữ.

**Bước 2. Cài đặt.**

```bash
sudo apt install -y espeak-ng build-essential cmake ninja-build
git clone https://github.com/OHF-voice/piper1-gpl && cd piper1-gpl
python -m venv .venv && source .venv/bin/activate
pip install -e '.[train]'
./build_monotonic_align.sh
espeak-ng -v vi "xin chào" --ipa   # kiểm tra espeak đọc được tiếng Việt
```

**Bước 3. Huấn luyện.**

```bash
python -m piper.train fit \
  --data.voice_name "vi_giong_toi" \
  --data.csv_path data/metadata.csv \
  --data.audio_dir data/wavs/ \
  --model.sample_rate 22050 \
  --data.espeak_voice "vi" \
  --data.cache_dir cache/ \
  --data.config_path out/vi_giong_toi.onnx.json \
  --data.batch_size 16
```

- Không truyền `--ckpt_path` nghĩa là khởi tạo ngẫu nhiên, tức huấn luyện từ đầu. Thêm `--ckpt_path` trỏ tới checkpoint của một giọng có sẵn thì thành fine-tune (cách 3 trong bảng), nhanh hơn nhiều và chỉ cần 1 đến 2 giờ dữ liệu.
- Batch 16 hợp với 8 GB. Giảm xuống 8 nếu hết bộ nhớ.
- Từ đầu cần vài nghìn epoch với bộ dữ liệu cỡ này, tương đương vài ngày trên một GPU phổ thông. Theo dõi bằng TensorBoard và nghe mẫu định kỳ.

**Bước 4. Xuất ONNX và chạy.**

```bash
python -m piper.train.export_onnx --checkpoint lightning_logs/version_0/checkpoints/last.ckpt \
  --output-file out/vi_giong_toi.onnx
echo "Xin chào, đây là giọng Piper tự huấn luyện." | piper -m out/vi_giong_toi.onnx -f test.wav
```

Tệp `.onnx` và `.onnx.json` phải nằm cạnh nhau. Lưu ý kho `piper1-gpl` dùng giấy phép GPL.

## Các cách làm ASR

| # | Cách làm | Độ khó | VRAM | Dữ liệu | Độ chính xác |
|---|---|---|---|---|---|
| 1 | Dùng thẳng PhoWhisper hoặc Whisper large-v3-turbo qua faster-whisper | Rất dễ | 2 đến 6 GB, chạy được trên CPU | Không | Tốt với giọng phổ thông, yếu với thuật ngữ riêng |
| 2 | Thêm gợi ý từ vựng (`initial_prompt`, hotwords) | Rất dễ | Như trên | Danh sách thuật ngữ | Cải thiện tên riêng, thuật ngữ |
| 3 | LoRA trên Whisper small hoặc PhoWhisper-small | Dễ | 4 đến 6 GB | 5 đến 20 giờ | Khá, mô hình nhẹ |
| 4 | LoRA trên PhoWhisper-medium | Trung bình | Khoảng 8 GB | 10 đến 50 giờ | Cao |
| 5 | LoRA trên Whisper large-v3-turbo | Trung bình | 10 đến 12 GB | 10 đến 50 giờ | Cao nhất trong các cách vừa sức |
| 6 | Fine-tune toàn bộ Whisper small hoặc medium | Trung bình | 8 đến 16 GB | 50 giờ trở lên | Cao, dễ quên các miền khác |
| 7 | Huấn luyện từ đầu Conformer-CTC hoặc Zipformer cỡ nhỏ | Khó | 8 GB | 100 giờ trở lên | Phụ thuộc lượng dữ liệu, mô hình rất nhẹ và nhanh |

Cách 1 và 2 để lấy con số gốc:

```python
from faster_whisper import WhisperModel

model = WhisperModel("large-v3-turbo", device="cuda", compute_type="float16")
segments, info = model.transcribe(
    "hop_giao_ban.wav", language="vi", vad_filter=True,
    initial_prompt="Cuộc họp về hệ thống WMS, PLC, SCADA, băng tải.",
)
print(" ".join(s.text for s in segments))
```

## Từng bước fine-tune Whisper bằng LoRA

Lý do chọn: Whisper large-v3-turbo chỉ có 4 lớp giải mã nên nhanh, LoRA giữ được khả năng đa ngôn ngữ, và vừa trong 12 GB. Với máy 8 GB, đổi `model_id` thành `vinai/PhoWhisper-medium` hoặc `vinai/PhoWhisper-small`, các bước giữ nguyên.

**Bước 1. Cài đặt.**

```bash
pip install torch transformers datasets[audio] peft accelerate jiwer evaluate ctranslate2 faster-whisper
```

**Bước 2. Chuẩn bị dữ liệu.** Một thư mục âm thanh và hai tệp `train.csv`, `test.csv` có cột `file_name`, `sentence`. Tách theo người nói hoặc theo buổi ghi âm.

```python
import torch
from datasets import load_dataset, Audio
from transformers import WhisperProcessor

model_id = "openai/whisper-large-v3-turbo"
processor = WhisperProcessor.from_pretrained(model_id, language="vi", task="transcribe")

ds = load_dataset("csv", data_files={"train": "train.csv", "test": "test.csv"})
ds = ds.cast_column("file_name", Audio(sampling_rate=16000))

def prepare(batch):
    audio = batch["file_name"]
    batch["input_features"] = processor.feature_extractor(
        audio["array"], sampling_rate=16000).input_features[0]
    batch["labels"] = processor.tokenizer(batch["sentence"]).input_ids
    return batch

ds = ds.map(prepare, remove_columns=ds["train"].column_names, num_proc=4)
```

**Bước 3. Đo mô hình gốc** trên tập test bằng đoạn mã faster-whisper ở trên và ghi lại WER. Đây là mốc so sánh.

**Bước 4. Nạp mô hình và gắn LoRA.**

```python
from transformers import WhisperForConditionalGeneration
from peft import LoraConfig, get_peft_model

model = WhisperForConditionalGeneration.from_pretrained(model_id)
model.generation_config.language = "vi"
model.generation_config.task = "transcribe"
model.generation_config.forced_decoder_ids = None
model.config.use_cache = False
model.gradient_checkpointing_enable()

lora = LoraConfig(r=32, lora_alpha=64, lora_dropout=0.05, bias="none",
                  target_modules=["q_proj", "v_proj"])
model = get_peft_model(model, lora)
model.print_trainable_parameters()   # thường dưới 2% tổng tham số
```

**Bước 5. Bộ gom batch và thước đo.**

```python
import evaluate
from dataclasses import dataclass

@dataclass
class Collator:
    processor: WhisperProcessor
    def __call__(self, features):
        inputs = [dict(input_features=f["input_features"]) for f in features]
        batch = self.processor.feature_extractor.pad(inputs, return_tensors="pt")
        labels = [dict(input_ids=f["labels"]) for f in features]
        labels = self.processor.tokenizer.pad(labels, return_tensors="pt")
        ids = labels["input_ids"].masked_fill(labels.attention_mask.ne(1), -100)
        if (ids[:, 0] == self.processor.tokenizer.bos_token_id).all():
            ids = ids[:, 1:]
        batch["labels"] = ids
        return batch

wer = evaluate.load("wer")

def compute_metrics(pred):
    label_ids = pred.label_ids
    label_ids[label_ids == -100] = processor.tokenizer.pad_token_id
    hyp = processor.tokenizer.batch_decode(pred.predictions, skip_special_tokens=True)
    ref = processor.tokenizer.batch_decode(label_ids, skip_special_tokens=True)
    return dict(wer=100 * wer.compute(predictions=hyp, references=ref))
```

Trước khi tính WER nên chuẩn hoá cả hai phía theo cùng một quy ước (chữ thường, bỏ dấu câu) để con số phản ánh lỗi nghe thật sự.

**Bước 6. Huấn luyện.**

```python
from transformers import Seq2SeqTrainingArguments, Seq2SeqTrainer

args = Seq2SeqTrainingArguments(
    output_dir="whisper-turbo-vi-lora",
    per_device_train_batch_size=8, gradient_accumulation_steps=2,
    learning_rate=1e-4, warmup_steps=200, num_train_epochs=3,
    fp16=True,
    eval_strategy="steps", eval_steps=500, save_steps=500,
    per_device_eval_batch_size=8,
    predict_with_generate=True, generation_max_length=225,
    logging_steps=25, report_to=["tensorboard"],
    load_best_model_at_end=True, metric_for_best_model="wer", greater_is_better=False,
    label_names=["labels"],
)
trainer = Seq2SeqTrainer(model=model, args=args,
                         train_dataset=ds["train"], eval_dataset=ds["test"],
                         data_collator=Collator(processor),
                         compute_metrics=compute_metrics)
trainer.train()
```

Hết bộ nhớ: giảm batch xuống 4 và tăng `gradient_accumulation_steps` lên 4. Với dữ liệu dưới 10 giờ, 2 đến 3 epoch là đủ, nhiều hơn dễ học vẹt.

**Bước 7. Gộp adapter và chuyển sang CTranslate2 để chạy nhanh.**

```python
merged = model.merge_and_unload()
merged.save_pretrained("whisper-turbo-vi-merged")
processor.save_pretrained("whisper-turbo-vi-merged")
```

```bash
ct2-transformers-converter --model whisper-turbo-vi-merged \
  --output_dir whisper-turbo-vi-ct2 --quantization float16 \
  --copy_files tokenizer.json preprocessor_config.json
```

Sau đó `WhisperModel("whisper-turbo-vi-ct2")` trong faster-whisper dùng được ngay. Đo lại WER trên tập test và so với mốc ở bước 3. Kiểm tra thêm trên một tập ngoài miền (ví dụ VIVOS) để chắc rằng mô hình không kém đi ở giọng phổ thông.

## Từng bước huấn luyện ASR từ đầu với Conformer-CTC

Lý do chọn: Conformer-CTC cỡ nhỏ khoảng 13 triệu tham số, huấn luyện được trên 8 GB, suy luận rất nhanh và truyền phát được. Cần ít nhất khoảng 100 giờ có nhãn, vài trăm giờ thì tốt (Bud500, VLSP, Common Voice gộp lại, chú ý giấy phép).

**Bước 1. Cài đặt.**

```bash
pip install "nemo_toolkit[asr]"
git clone https://github.com/NVIDIA/NeMo
```

**Bước 2. Tạo manifest.** Mỗi dòng một đối tượng JSON, âm thanh WAV 16 kHz mono, văn bản chữ thường không dấu câu:

```json
{"audio_filepath": "/data/wav/0001.wav", "duration": 4.2, "text": "hôm nay trời đẹp quá"}
```

Tạo ba tệp `train.json`, `dev.json`, `test.json`, tách theo người nói. Bỏ đoạn dài hơn 20 giây.

**Bước 3. Huấn luyện bộ tách từ.** Tiếng Việt có ít âm tiết nên bộ từ vựng 256 đến 512 mảnh là đủ.

```bash
python NeMo/scripts/tokenizers/process_asr_text_tokenizer.py \
  --manifest=train.json --data_root=tokenizers/vi \
  --vocab_size=256 --tokenizer=spe --spe_type=bpe --log
```

**Bước 4. Huấn luyện.**

```bash
python NeMo/examples/asr/asr_ctc/speech_to_text_ctc_bpe.py \
  --config-path=../conf/conformer --config-name=conformer_ctc_bpe \
  model.train_ds.manifest_filepath=train.json \
  model.validation_ds.manifest_filepath=dev.json \
  model.tokenizer.dir=tokenizers/vi/tokenizer_spe_bpe_v256 model.tokenizer.type=bpe \
  model.encoder.d_model=176 model.encoder.n_heads=4 model.encoder.n_layers=16 \
  model.train_ds.batch_size=16 trainer.accumulate_grad_batches=4 \
  trainer.devices=1 trainer.precision=16 trainer.max_epochs=100
```

- Ba tham số `d_model=176`, `n_heads=4`, `n_layers=16` là cấu hình cỡ nhỏ ghi trong chú thích của tệp cấu hình.
- Cấu hình có sẵn SpecAugment. Với dữ liệu ít, thêm tăng cường tốc độ (0,9 và 1,1 lần) và trộn nhiễu nền.
- WER trên tập dev giảm chậm trong vài chục epoch đầu là bình thường với CTC.

**Bước 5. Đánh giá và cải thiện.**

```bash
python NeMo/examples/asr/speech_to_text_eval.py \
  model_path=nemo_experiments/Conformer-CTC-BPE/checkpoints/Conformer-CTC-BPE.nemo \
  dataset_manifest=test.json batch_size=16
```

Hai cách tăng độ chính xác mà không cần thêm dữ liệu có nhãn: ghép mô hình ngôn ngữ n-gram (KenLM) vào bước giải mã, và dùng Whisper đã fine-tune ở phần trên để gán nhãn tự động cho âm thanh chưa có nhãn rồi huấn luyện tiếp (chưng cất). Mô hình xuất được sang ONNX để chạy trên CPU.

## Lưu ý quan trọng

- **Sự đồng ý.** Chỉ nhân bản giọng của mình hoặc của người đã đồng ý rõ ràng. Gắn nhãn nội dung là giọng tổng hợp khi công bố.
- **Giấy phép.** F5-TTS gốc được huấn luyện trên dữ liệu phi thương mại, checkpoint thừa hưởng ràng buộc đó dù mã nguồn là MIT. VieNeu-TTS bản 0.3B là phi thương mại. Piper bản mới là GPL. Kiểm tra từng trang mô hình.
- **Chuẩn hoá văn bản là nửa công việc của TTS tiếng Việt.** "15/11", "2.5kg", "TP.HCM", "Dr." phải thành chữ trước khi đưa vào mô hình, cả lúc huấn luyện lẫn lúc dùng.
- **Vùng miền.** Mô hình học giọng vùng nào thì đọc và nghe tốt vùng đó. ASR cần dữ liệu đủ ba miền nếu người dùng đa dạng.
- **Whisper hay bịa chữ trên đoạn im lặng.** Luôn bật VAD khi suy luận.
- **Đừng trộn tần số lấy mẫu.** Một bộ dữ liệu một tần số, đúng với tần số mô hình yêu cầu.

## Nguồn tham khảo

- [F5-TTS-Vietnamese trên GitHub](https://github.com/nguyenthienhy/F5-TTS-Vietnamese)
- [VieNeu-TTS trên Hugging Face](https://huggingface.co/pnnbao-ump/vieneu-tts) và [gói vieneu trên PyPI](https://pypi.org/project/vieneu/1.2.4/)
- [PhoWhisper: Automatic Speech Recognition for Vietnamese](https://arxiv.org/pdf/2406.02555)
- [So sánh các mô hình ASR chạy cục bộ năm 2026 (Voconly)](https://www.voconly.com/en/blog/local-ai-asr/local-asr-model-comparison-2026/)
