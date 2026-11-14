---
layout: post
categories: ["Trí tuệ nhân tạo & Dữ liệu"]
title: "Tự huấn luyện mô hình AI nhỏ (5): Tạo sinh hình ảnh"
subtitle: "Huấn luyện LoRA cho FLUX.2 klein 4B và tự xây một mô hình khuếch tán từ đầu"
date: 2026-11-15 08:40:00 +0700
tags:
- AI
- Image Generation
- Diffusion
- LoRA
- FLUX
- SDXL
- AI-Toolkit
- Fine-tuning
series: "Tự huấn luyện mô hình AI nhỏ"
series_order: 5
---

> Bài 5 của series. Với tạo sinh hình ảnh, "tự huấn luyện" trong thực tế gần như luôn là huấn luyện LoRA: dạy một mô hình có sẵn vẽ đúng một nhân vật, một sản phẩm hoặc một phong cách từ vài chục tấm ảnh. Bài này hướng dẫn cách đó, và thêm phần tự huấn luyện một mô hình khuếch tán bé từ đầu để hiểu cơ chế. Kiến thức nền nằm ở [bài 1](/2026/11/15/tu-huan-luyen-ai-nho-1-tong-quan/). Code và cấu hình là khung cốt lõi, chưa chạy kiểm chứng trên GPU thật.

- [Technical stack](#technical-stack)
- [Dữ liệu đầu vào](#dữ-liệu-đầu-vào)
- [Các cách làm xếp từ dễ đến khó](#các-cách-làm-xếp-từ-dễ-đến-khó)
- [Từng bước huấn luyện LoRA cho FLUX.2 klein 4B](#từng-bước-huấn-luyện-lora-cho-flux2-klein-4b)
- [Từng bước huấn luyện mô hình khuếch tán từ đầu](#từng-bước-huấn-luyện-mô-hình-khuếch-tán-từ-đầu)
- [Lưu ý quan trọng](#lưu-ý-quan-trọng)
- [Nguồn tham khảo](#nguồn-tham-khảo)

## Technical stack

| Nhóm | Thành phần | Ghi chú |
|---|---|---|
| Mô hình gốc | FLUX.2 klein 4B Base (Black Forest Labs) | Apache 2.0. BFL khuyên dùng cho đa số người dùng vì nhẹ. Cần GPU 12 GB và RAM 32 GB |
| | FLUX.2 klein 9B Base | Chất lượng cao hơn, giấy phép phi thương mại, cần 22 GB VRAM và RAM 64 GB |
| | Z-Image và Z-Image-Turbo (Alibaba) | Nhẹ, công cụ LoRAlab ghi mức tối thiểu 8 GB ở chế độ 4-bit |
| | Qwen-Image 2.1, Krea 2 | Các mô hình mới khác, cũng được ghi mức tối thiểu 8 GB ở chế độ 4-bit |
| | SDXL và các nhánh Illustrious, Pony, NoobAI | Đời cũ hơn nhưng hệ sinh thái lớn nhất, LoRA từ 4 GB (4-bit) đến 12 GB |
| | Stable Diffusion 1.5 | Rất nhẹ (4 đến 6 GB), độ phân giải 512, chất lượng thấp hơn |
| Công cụ huấn luyện | [AI-Toolkit](https://github.com/ostris/ai-toolkit) (ostris) | Giao diện web và dòng lệnh, hỗ trợ sớm các mô hình mới, nhắm tới GPU phổ thông |
| | kohya sd-scripts và giao diện kohya_ss | Chuẩn lâu đời cho SD 1.5, SDXL |
| | OneTrainer, SimpleTuner, musubi-tuner | Các lựa chọn khác |
| | diffusers (Hugging Face) | Thư viện gốc, có sẵn mã mẫu DreamBooth, LoRA và huấn luyện từ đầu |
| | AcademiaSD LoRAlab | Gói chín bộ huấn luyện LoRA sau một trình khởi chạy trong ComfyUI |
| Viết chú thích ảnh | Florence-2, JoyCaption, một VLM nhỏ (Qwen3-VL, Gemma 4), WD14 tagger cho ảnh anime | Sinh chú thích tự động rồi sửa tay |
| Xử lý ảnh | Pillow, OpenCV, rembg, bộ phóng to ảnh | Cắt, lọc, tách nền |
| Sinh ảnh và kiểm thử | ComfyUI, diffusers | Nạp LoRA và so sánh các checkpoint |
| Huấn luyện từ đầu | diffusers (UNet2DModel, DDPMScheduler), accelerate | Mô hình khuếch tán nhỏ |

## Dữ liệu đầu vào

**Số lượng:** 15 đến 30 ảnh cho một nhân vật hoặc sản phẩm, 30 đến 100 ảnh cho một phong cách. Nhiều ảnh trung bình không bằng ít ảnh tốt.

**Chất lượng ảnh:**

- Độ phân giải từ 1024 điểm ảnh trở lên ở cạnh ngắn, nét, không vỡ do nén, không có chữ chìm.
- Đa dạng ở mọi thứ **không phải** điều bạn muốn dạy: góc chụp, ánh sáng, bối cảnh, trang phục, cự ly (cận cảnh lẫn toàn thân). Nếu mọi ảnh đều có nền trắng, mô hình sẽ coi nền trắng là một phần của khái niệm.
- Nhất quán ở điều bạn muốn dạy: cùng một nhân vật, cùng một sản phẩm, cùng một phong cách.
- Không cần cắt vuông. Các công cụ hiện nay tự gom ảnh theo tỷ lệ khung hình.

**Chú thích (caption):** mỗi ảnh một tệp `.txt` cùng tên.

```text
data/sp_binhgom/
  001.jpg
  001.txt   ->  bgxv01, một chiếc bình gốm đặt trên bàn gỗ, ánh sáng cửa sổ từ bên trái, nền tường xám
  002.jpg
  002.txt   ->  bgxv01, một người phụ nữ cầm chiếc bình gốm trong vườn, chụp toàn thân, trời nắng
```

Nguyên tắc theo hướng dẫn của BFL: dùng một **từ kích hoạt** nhất quán và mô tả mọi thứ nhìn thấy được **ngoại trừ** chính khái niệm bạn muốn dạy. Những gì bạn mô tả sẽ thành thứ thay đổi được bằng prompt sau này. Những gì bạn không mô tả sẽ dính vào từ kích hoạt. Chọn từ kích hoạt là một chuỗi hiếm, không có nghĩa sẵn (ví dụ `bgxv01`).

Về ngôn ngữ: bộ mã hoá văn bản của các mô hình này hiểu tiếng Anh tốt nhất. Viết chú thích tiếng Anh thường cho kết quả ổn định hơn tiếng Việt, ví dụ trên dùng tiếng Việt chỉ để dễ đọc.

**Ảnh điều chuẩn (regularization):** vài chục đến vài trăm ảnh chung của cùng lớp đối tượng (ví dụ các bình gốm khác) giúp mô hình không quên lớp đó trông thế nào. Hữu ích với DreamBooth và SDXL, thường không cần với LoRA trên các mô hình mới.

## Các cách làm xếp từ dễ đến khó

| # | Cách làm | Độ khó | VRAM | Dữ liệu | Ghi chú |
|---|---|---|---|---|---|
| 1 | Không huấn luyện: dùng ảnh tham chiếu (chỉnh sửa theo ảnh mẫu, IP-Adapter) | Rất dễ | 8 đến 12 GB để chạy | 1 đến 4 ảnh | Thử trước. Nhiều mô hình mới giữ được đối tượng từ ảnh tham chiếu khá tốt |
| 2 | Textual Inversion trên SD 1.5 hoặc SDXL | Dễ | 6 đến 8 GB | 5 đến 15 ảnh | Chỉ học một embedding, tệp vài KB, độ giống hạn chế |
| 3 | LoRA trên SD 1.5 | Dễ | 4 đến 6 GB | 15 đến 30 ảnh | Nhanh nhất, chất lượng đời cũ |
| 4 | LoRA trên SDXL bằng sd-scripts | Trung bình | 8 đến 12 GB | 15 đến 50 ảnh | Mốc 8 GB của bài này |
| 5 | LoRA trên Z-Image bằng AI-Toolkit | Trung bình | 8 đến 12 GB | 15 đến 50 ảnh | Mô hình mới, nhẹ |
| 6 | LoRA trên FLUX.2 klein 4B Base bằng AI-Toolkit | Trung bình | 12 GB | 15 đến 50 ảnh | Cân bằng tốt nhất giữa chất lượng, VRAM và giấy phép |
| 7 | LoRA trên FLUX.2 klein 9B Base | Trung bình | 22 đến 24 GB | 20 đến 100 ảnh | Chất lượng cao nhất, phi thương mại |
| 8 | DreamBooth hoặc fine-tune toàn bộ SDXL | Khó | 16 đến 24 GB | 50 đến hàng nghìn ảnh | Tệp kết quả vài GB, dễ học vẹt |
| 9 | Huấn luyện từ đầu mô hình khuếch tán không điều kiện, 64 điểm ảnh | Khó | 6 đến 8 GB | 5000 ảnh trở lên của một miền hẹp | Để học cơ chế, hoặc sinh dữ liệu cho miền hẹp |
| 10 | Huấn luyện từ đầu mô hình văn bản thành ảnh | Rất khó | Cụm GPU, nhiều tuần | Hàng triệu đến hàng tỷ cặp ảnh và chú thích | Ngoài phạm vi cá nhân |

## Từng bước huấn luyện LoRA cho FLUX.2 klein 4B

Lý do chọn: bản 4B Base dùng giấy phép Apache 2.0, là bản chưa chưng cất nên hợp để fine-tune, cần 12 GB VRAM theo tài liệu của BFL, và BFL có bài hướng dẫn huấn luyện LoRA trong dưới 60 phút. Các tham số dưới đây lấy theo khuyến nghị của họ.

**Bước 1. Chọn và làm sạch ảnh.** Chọn 20 đến 30 ảnh tốt nhất theo các tiêu chí ở trên. Loại ảnh mờ, ảnh trùng lặp, ảnh có nhiều đối tượng gây nhiễu. Đặt vào `data/sp_binhgom/`.

**Bước 2. Viết chú thích.** Sinh tự động bằng Florence-2, JoyCaption hoặc một VLM, sau đó đọc và sửa từng tệp: thêm từ kích hoạt ở đầu, xoá các từ mô tả chính khái niệm cần dạy, sửa chỗ mô hình mô tả sai.

**Bước 3. Cài AI-Toolkit.**

```bash
git clone https://github.com/ostris/ai-toolkit && cd ai-toolkit
python -m venv venv && source venv/bin/activate
pip install torch torchvision          # bản khớp CUDA của máy
pip install -r requirements.txt
huggingface-cli login                  # nếu mô hình yêu cầu đồng ý điều khoản
```

Công cụ có giao diện web (chạy từ thư mục `ui`) cho phép tạo tác vụ, xem ảnh mẫu và theo dõi loss. Phần dưới dùng tệp cấu hình để dễ lưu lại và so sánh.

**Bước 4. Tạo tệp cấu hình.** Sao chép tệp mẫu cho FLUX.2 klein trong `config/examples/` của kho mã rồi sửa. Khung các trường quan trọng:

```yaml
job: extension
config:
  name: "binhgom_klein4b_v1"
  process:
    - type: "sd_trainer"
      training_folder: "output"
      device: cuda:0
      trigger_word: "bgxv01"
      network:
        type: "lora"
        linear: 16            # rank: 16 cho đối tượng, 32 cho phong cách phức tạp
        linear_alpha: 16
      save:
        dtype: float16
        save_every: 250
        max_step_saves_to_keep: 8
      datasets:
        - folder_path: "data/sp_binhgom"
          caption_ext: "txt"
          caption_dropout_rate: 0.05
          cache_latents_to_disk: true
          resolution: [512, 768, 1024]
      train:
        batch_size: 1
        steps: 2000
        gradient_checkpointing: true
        optimizer: "adamw8bit"
        lr: 1e-4
        dtype: bf16
      model:
        # Giữ nguyên các trường name_or_path và arch từ tệp mẫu của FLUX.2 klein 4B Base
        quantize: true
        low_vram: true
      sample:
        sample_every: 250
        width: 1024
        height: 1024
        seed: 42
        prompts:
          - "bgxv01, a ceramic vase on a marble kitchen counter, morning light"
          - "bgxv01, held by a man in a workshop, close-up"
          - "a ceramic vase on a wooden table"   # không có từ kích hoạt, để kiểm tra rò rỉ
```

Các giá trị theo khuyến nghị của BFL:

- **Learning rate:** 8e-5 đến 1e-4 cho LoRA. Thấp hơn cho phong cách, cao hơn cho nhân vật.
- **Số bước:** 1500 đến 2500 cho phong cách, 1500 đến 3000 cho nhân vật. Theo dõi ảnh mẫu để phát hiện học vẹt.
- **Độ phân giải:** bắt đầu ở 512 để thử nhanh, huấn luyện bản cuối ở 1024 trở lên.

**Bước 5. Chạy thử ngắn.** Đặt `steps: 200` và độ phân giải chỉ 512, chạy một lần để chắc đường ống hoạt động, không hết bộ nhớ và ảnh mẫu được sinh ra.

```bash
python run.py config/binhgom_klein4b_v1.yaml
watch -n 1 nvidia-smi    # ở cửa sổ khác, theo dõi VRAM
```

Nếu hết bộ nhớ ở 12 GB: giữ `quantize` và `low_vram`, bỏ mức 1024 khỏi `resolution`, đóng mọi ứng dụng dùng GPU khác (trình duyệt cũng chiếm VRAM).

**Bước 6. Huấn luyện thật và chọn checkpoint.** Chạy đủ 2000 bước. Cứ 250 bước công cụ lưu một checkpoint và sinh ảnh từ các prompt mẫu với cùng seed. Xếp các ảnh cạnh nhau và tìm điểm cân bằng:

| Dấu hiệu | Ý nghĩa | Xử lý |
|---|---|---|
| Đối tượng chưa giống | Học chưa đủ | Dùng checkpoint muộn hơn, hoặc tăng số bước, tăng rank |
| Giống nhưng mọi ảnh cùng một tư thế, cùng nền như ảnh huấn luyện | Học vẹt | Dùng checkpoint sớm hơn, giảm learning rate, thêm ảnh đa dạng |
| Ảnh cháy màu, nhiễu, méo | Huấn luyện quá mức | Dùng checkpoint sớm hơn |
| Prompt không có từ kích hoạt cũng ra đối tượng của bạn | Rò rỉ khái niệm vào lớp chung | Sửa chú thích, giảm số bước |
| Không đổi được bối cảnh bằng prompt | Chú thích thiếu mô tả bối cảnh | Viết chú thích kỹ hơn |

Checkpoint tốt nhất thường nằm ở khoảng 60 đến 80% số bước, không phải cái cuối.

**Bước 7. Dùng LoRA.** Chép tệp `.safetensors` vào thư mục `models/loras` của ComfyUI và nạp bằng nút Load LoRA, thử cường độ 0,7 đến 1,0. Hoặc bằng diffusers:

```python
import torch
from diffusers import DiffusionPipeline

pipe = DiffusionPipeline.from_pretrained("<repo của FLUX.2 klein 4B>", torch_dtype=torch.bfloat16)
pipe.load_lora_weights("output/binhgom_klein4b_v1", weight_name="binhgom_klein4b_v1.safetensors")
pipe.enable_model_cpu_offload()      # giảm VRAM khi sinh ảnh
image = pipe("bgxv01, a ceramic vase on a beach at sunset",
             num_inference_steps=28, generator=torch.Generator().manual_seed(0)).images[0]
image.save("test.png")
```

LoRA huấn luyện trên bản Base thường dùng được với bản chưng cất của cùng kích thước để sinh ảnh nhanh hơn, hãy thử cả hai.

**Phương án cho máy 8 GB: LoRA trên SDXL bằng sd-scripts.**

```bash
accelerate launch sdxl_train_network.py \
  --pretrained_model_name_or_path="stabilityai/stable-diffusion-xl-base-1.0" \
  --train_data_dir="data" --caption_extension=".txt" \
  --resolution="1024,1024" --enable_bucket \
  --network_module=networks.lora --network_dim=16 --network_alpha=8 \
  --network_train_unet_only \
  --train_batch_size=1 --max_train_steps=2000 \
  --learning_rate=1e-4 --optimizer_type="AdamW8bit" --lr_scheduler="cosine" \
  --mixed_precision="fp16" --gradient_checkpointing \
  --cache_latents --cache_text_encoder_outputs \
  --save_every_n_steps=250 --save_model_as=safetensors \
  --output_dir="output" --output_name="binhgom_sdxl_v1"
```

Với sd-scripts, ảnh nằm trong thư mục con đặt tên theo dạng `số_lần_lặp tên` (ví dụ `data/10_bgxv01 vase/`). Các cờ đệm sẵn latent và đầu ra bộ mã hoá văn bản, cùng với việc chỉ huấn luyện U-Net, là thứ giúp SDXL vừa trong 8 GB.

## Từng bước huấn luyện mô hình khuếch tán từ đầu

Mục tiêu: một mô hình khuếch tán **không điều kiện** sinh ảnh 64 x 64 của một miền hẹp, ví dụ hoa văn gạch, biểu tượng, khuôn mặt hoạt hình, ảnh bề mặt sản phẩm. Không có prompt văn bản. Mô hình học phân bố của tập ảnh và sinh ra ảnh mới cùng loại. Chạy được trên GPU 8 GB.

Giá trị thực tế: hiểu cơ chế thêm nhiễu và khử nhiễu, và sinh thêm dữ liệu cho miền hẹp, ví dụ ảnh bề mặt để huấn luyện mô hình phát hiện lỗi.

**Bước 1. Dữ liệu.** Từ 5000 ảnh trở lên của cùng một loại, càng đồng nhất càng dễ học. Cắt vuông, đặt vào một thư mục. Với ít hơn vài nghìn ảnh, mô hình sẽ nhớ nguyên các ảnh huấn luyện.

**Bước 2. Cài đặt.**

```bash
git clone https://github.com/huggingface/diffusers && cd diffusers
pip install -e . && pip install accelerate datasets torchvision tensorboard
cd examples/unconditional_image_generation
```

**Bước 3. Hiểu việc mô hình học.** Mỗi bước huấn luyện: lấy một ảnh sạch, chọn ngẫu nhiên một mức nhiễu trong 1000 mức, cộng nhiễu Gauss vào ảnh, cho mạng U-Net đoán chính phần nhiễu đã cộng, và phạt theo sai số bình phương. Phần cốt lõi của vòng lặp:

```python
import torch
import torch.nn.functional as F
from diffusers import UNet2DModel, DDPMScheduler

model = UNet2DModel(
    sample_size=64, in_channels=3, out_channels=3, layers_per_block=2,
    block_out_channels=(128, 128, 256, 256, 512, 512),
    down_block_types=("DownBlock2D", "DownBlock2D", "DownBlock2D", "DownBlock2D", "AttnDownBlock2D", "DownBlock2D"),
    up_block_types=("UpBlock2D", "AttnUpBlock2D", "UpBlock2D", "UpBlock2D", "UpBlock2D", "UpBlock2D"),
)
scheduler = DDPMScheduler(num_train_timesteps=1000)

def training_step(clean_images):
    noise = torch.randn_like(clean_images)
    t = torch.randint(0, 1000, (clean_images.shape[0],), device=clean_images.device)
    noisy = scheduler.add_noise(clean_images, noise, t)
    pred = model(noisy, t).sample
    return F.mse_loss(pred, noise)
```

Mạng với cấu hình này có khoảng một trăm triệu tham số. Giảm các số trong `block_out_channels` đi một nửa nếu muốn nhẹ và nhanh hơn.

**Bước 4. Huấn luyện bằng mã mẫu có sẵn.**

```bash
accelerate launch train_unconditional.py \
  --train_data_dir="/data/hoa_van" \
  --resolution=64 --center_crop --random_flip \
  --output_dir="ddpm-hoa-van-64" \
  --train_batch_size=16 --gradient_accumulation_steps=2 \
  --num_epochs=150 \
  --learning_rate=1e-4 --lr_warmup_steps=500 \
  --mixed_precision="fp16" --use_ema \
  --save_images_epochs=10 --save_model_epochs=10 \
  --logger="tensorboard"
```

- `--use_ema` giữ một bản trung bình trượt của trọng số, cho ảnh ổn định hơn rõ rệt.
- Loss giảm nhanh lúc đầu rồi gần như đi ngang. Với mô hình khuếch tán, loss không phản ánh chất lượng ảnh, phải nhìn ảnh mẫu mỗi 10 epoch.
- Thời gian: vài giờ đến một ngày tuỳ số ảnh. Tăng lên 128 điểm ảnh thì cần giảm batch và thời gian tăng khoảng bốn lần.

**Bước 5. Sinh ảnh.**

```python
from diffusers import DDPMPipeline, DDIMScheduler

pipe = DDPMPipeline.from_pretrained("ddpm-hoa-van-64").to("cuda")
pipe.scheduler = DDIMScheduler.from_config(pipe.scheduler.config)   # lấy mẫu nhanh hơn
images = pipe(batch_size=16, num_inference_steps=50).images
for i, im in enumerate(images):
    im.save(f"sample_{i:02d}.png")
```

**Bước 6. Đánh giá.** Nhìn bằng mắt là chính. So ảnh sinh với ảnh huấn luyện gần nhất để chắc mô hình không chép lại. Thước đo định lượng phổ biến là FID, cần vài nghìn ảnh sinh ra để có ý nghĩa.

**Đi tiếp:**

- **Có điều kiện theo lớp:** thêm `num_class_embeds` vào U-Net và truyền nhãn lớp, để chọn được loại ảnh muốn sinh.
- **Khuếch tán trong không gian ẩn:** dùng một VAE có sẵn nén ảnh 256 xuống latent 32 x 32 rồi huấn luyện U-Net hoặc DiT nhỏ trên latent. Đây là cách các mô hình lớn làm.
- **Văn bản thành ảnh:** cần thêm bộ mã hoá văn bản và hàng triệu cặp ảnh kèm chú thích. Ở quy mô cá nhân, fine-tune luôn là lựa chọn đúng.

## Lưu ý quan trọng

- **Giấy phép.** FLUX.2 klein 4B là Apache 2.0, bản 9B là phi thương mại. LoRA huấn luyện trên mô hình nào thì chịu giấy phép của mô hình đó. SDXL và các nhánh của nó có giấy phép riêng, đọc trước khi dùng thương mại.
- **Quyền với ảnh huấn luyện.** Dùng ảnh bạn tự chụp, ảnh sản phẩm của mình, hoặc ảnh được cấp phép. Huấn luyện trên khuôn mặt người thật cần sự đồng ý của người đó. Bắt chước phong cách của hoạ sĩ còn sống là vấn đề cả về đạo đức lẫn pháp lý.
- **Không tạo ảnh mạo danh người thật.**
- **LoRA không dùng chéo giữa các họ mô hình.** LoRA của SDXL không nạp được vào FLUX.2 và ngược lại.
- **RAM hệ thống.** Mô hình ảnh cần nhiều RAM khi nạp và lượng tử hoá: 32 GB cho klein 4B, 64 GB cho 9B theo BFL.
- **Lưu lại cấu hình và seed** của mỗi lần chạy. Không có chúng thì không so sánh hay lặp lại được.
- **Một thay đổi mỗi lần.** Đổi cùng lúc learning rate, rank và dữ liệu thì không biết cái nào tạo ra khác biệt.

## Nguồn tham khảo

- [Black Forest Labs: FLUX.2 klein training](https://docs.bfl.ai/flux_2/flux2_klein_training)
- [Fine-tune FLUX.2 klein with a LoRA under 60 minutes](https://huggingface.co/blog/black-forest-labs/flux-2-klein-lora)
- [AcademiaSD LoRAlab: Nine LoRA Trainers Behind One Launcher](https://comfyui-wiki.com/en/news/2026-10-06-academiasd-loralab)
- [Best practices for training LoRA models with Z-Image](https://dev.to/gary_yan_86eb77d35e0070f5/best-practices-for-training-lora-models-with-z-image-complete-2026-guide-4p7h)
