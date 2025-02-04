---
layout: post
title: Cách chạy Stable Video Diffusion img2vid
subtitle: How to run Stable Video Diffusion img2vid
date: 2025-02-02 11:00:00
tags:
- img2vid
- Stable Video Diffusion
---

- [Stable Video Diffusion là gì](#stable-video-diffusion-là-gì)
  - [Nó làm gì](#nó-làm-gì)
  - [Mô hình và đào tạo](#mô-hình-và-đào-tạo)
  - [Stable Stable Video Models weights](#stable-stable-video-models-weights)
  - [Các thông số mô hình](#các-thông-số-mô-hình)
  - [Hiệu suất của Stable Video Diffusion so với các mô hình video AI khác như thế nào?](#hiệu-suất-của-stable-video-diffusion-so-với-các-mô-hình-video-ai-khác-như-thế-nào)
  - [Yêu cầu tính toán để chạy Stable Video Diffusion là gì?](#yêu-cầu-tính-toán-để-chạy-stable-video-diffusion-là-gì)
- [Sử dụng Stable Video Diffusion trên Colab](#sử-dụng-stable-video-diffusion-trên-colab)
  - [Bước 1: Mở Sổ tay Colab](#bước-1-mở-sổ-tay-colab)
  - [Bước 2: Xem lại tùy chọn sổ ghi chép](#bước-2-xem-lại-tùy-chọn-sổ-ghi-chép)
  - [Bước 3: Chạy sổ ghi chép](#bước-3-chạy-sổ-ghi-chép)
  - [Bước 4: Khởi động GUI](#bước-4-khởi-động-gui)
  - [Bước 5: Tải lên hình ảnh ban đầu](#bước-5-tải-lên-hình-ảnh-ban-đầu)
  - [Bước 6: Bắt đầu tạo video](#bước-6-bắt-đầu-tạo-video)
  - [Tùy chỉnh video của bạn](#tùy-chỉnh-video-của-bạn)
- [Sử dụng Stable Video Diffusion với ComfyUI](#sử-dụng-stable-video-diffusion-với-comfyui)
  - [Bước 1: Tải quy trình làm việc chuyển văn bản thành video](#bước-1-tải-quy-trình-làm-việc-chuyển-văn-bản-thành-video)
  - [Bước 2: Cập nhật ComfyUI](#bước-2-cập-nhật-comfyui)
  - [Bước 3: Tải xuống mô hình](#bước-3-tải-xuống-mô-hình)
  - [Bước 4: Chạy quy trình làm việc](#bước-4-chạy-quy-trình-làm-việc)
- [Cài đặt Stable Video Diffusion trên Windows](#cài-đặt-stable-video-diffusion-trên-windows)
  - [Bước 1: Sao chép kho lưu trữ](#bước-1-sao-chép-kho-lưu-trữ)
  - [Bước 2: Tạo môi trường ảo](#bước-2-tạo-môi-trường-ảo)
  - [Bước 3: Xóa gói triton trong yêu cầu](#bước-3-xóa-gói-triton-trong-yêu-cầu)
  - [Bước 4: Cài đặt các thư viện cần thiết](#bước-4-cài-đặt-các-thư-viện-cần-thiết)
  - [Bước 5: Tải xuống mô hình video](#bước-5-tải-xuống-mô-hình-video)
  - [Bước 6: Chạy GUI](#bước-6-chạy-gui)
  - [Bước 7: Tạo video](#bước-7-tạo-video)
  - [Bắt đầu lại GUI](#bắt-đầu-lại-gui)
- [Tài nguyên](#tài-nguyên)


Stable Video Diffusion là mô hình Stable Diffusion đầu tiên được thiết kế để tạo video. Bạn có thể sử dụng nó để tạo hiệu ứng hình ảnh động được tạo ra bởi Stable Diffusion, tạo ra hiệu ứng hình ảnh tuyệt đẹp.

Sau đây là một số video mẫu:

[Realistic Egyptian princess](https://stable-diffusion-art.com/realistic-egyptian-princess/)

https://stable-diffusion-art.com/wp-content/uploads/2023/11/060b3b1a23282c2811b4984c06087a12827316242103d23f161fe86f.mp4

[Biomechanical animal](https://stable-diffusion-art.com/biomechanical-animal/)

https://stable-diffusion-art.com/wp-content/uploads/2023/11/tiger.mp4

[Castle in Fall](https://stable-diffusion-art.com/castle-in-fall/)

https://stable-diffusion-art.com/wp-content/uploads/2023/11/f26f4f5d8a1cc09c8f28eaea0fb78393915ab7686fea1be551384b4e-1.mp4

Trong bài viết này, bạn sẽ tìm hiểu về

- Stable Video Diffusion là gì?
- Cách sử dụng trên Google Colab trực tuyến.
- Cách sử dụng quy trình chuyển đổi văn bản thành video trong ComfyUI.
- Cách cài đặt và sử dụng cục bộ trên Windows.

## Stable Video Diffusion là gì

Stable Video Diffusion (SVD) là [mô hình video nền tảng](https://stability.ai/news/stable-video-diffusion-open-ai-video-model) đầu tiên được Stability AI, người tạo ra Stable Diffusion, phát hành. Đây là mô hình mã nguồn mở, với [mã](https://github.com/Stability-AI/generative-models) và [trọng số mô hình](https://huggingface.co/stabilityai/stable-video-diffusion-img2vid-xt) có sẵn miễn phí.

### Nó làm gì

SVD là mô hình chuyển đổi hình ảnh thành video (img2vid). Bạn cung cấp khung hình đầu tiên và mô hình sẽ tạo ra một đoạn video clip ngắn. Dưới đây là ví dụ về đầu vào và đầu ra của mô hình.

![Stable Video Diffusion](https://boxxv.github.io/img/2025/16158-967991111-photo-of-25-year-old-woman-windy-hair-blowing-1024x683.png "Stable Video Diffusion")

https://stable-diffusion-art.com/wp-content/uploads/2023/11/000003.mp4

### Mô hình và đào tạo

Mô hình và đào tạo được mô tả trong bài viết [Stable Video Diffusion: Scaling Latent Video Diffusion Models to Large Dataset](https://stability.ai/research/stable-video-diffusion-scaling-latent-video-diffusion-models-to-large-datasets) (2023) của Andreas Blattmann và các cộng sự.

Mô hình SVD đã trải qua 3 giai đoạn đào tạo.

1. Đào tạo **mô hình hình ảnh**.
2. Mở rộng mô hình hình ảnh thành mô hình video , sau đó được đào tạo trước với bộ dữ liệu video lớn.
3. Tinh chỉnh mô hình video bằng tập dữ liệu video chất lượng cao nhỏ hơn.

Việc tuyển chọn và cải thiện bộ dữ liệu là chìa khóa thành công của mô hình video.

Mô hình hình ảnh là [Stable Diffusion 2.1](https://stable-diffusion-art.com/install-stable-diffusion-2-1/), tiền thân bị lãng quên của mô hình [SDXL](https://stable-diffusion-art.com/sdxl-model/). Mô hình hình ảnh được đào tạo trước tạo thành xương sống hình ảnh của mô hình video.

Các lớp tích chập thời gian và chú ý được thêm vào [bộ ước tính nhiễu U-Net](https://stable-diffusion-art.com/how-stable-diffusion-work/) để tạo mô hình video. Bây giờ, tenxơ tiềm ẩn biểu diễn video thay vì hình ảnh. Tất cả các khung hình đều được khử nhiễu bằng khuếch tán ngược cùng một lúc. Mô hình khuếch tán thời gian này giống với [mô hình VideoLDM](https://research.nvidia.com/labs/toronto-ai/VideoLDM/).

![Stable Video Diffusion](https://boxxv.github.io/img/2025/image-137-1024x702.webp "Stable Video Diffusion")

Mô hình video có 1,5B tham số và được đào tạo bằng một tập dữ liệu video lớn. Cuối cùng, mô hình video được tinh chỉnh bằng một tập dữ liệu nhỏ hơn nhưng chất lượng cao hơn.

### Stable Stable Video Models weights

Có hai trọng số mô hình SVD được công bố rộng rãi.

- [SVD](https://huggingface.co/stabilityai/stable-video-diffusion-img2vid/blob/main/svd.safetensors) – được đào tạo để tạo ra 14 khung hình ở độ phân giải 576×1024.
- [SVD XT](https://huggingface.co/stabilityai/stable-video-diffusion-img2vid-xt/blob/main/svd_xt.safetensors) – được đào tạo để tạo ra 25 khung hình ở độ phân giải 576×1024.

Trong bài viết này, chúng tôi sẽ tập trung vào việc sử dụng mô hình SVD XT.

### Các thông số mô hình

Dưới đây là danh sách các thông số quan trọng kiểm soát đầu ra video.

**Motion bucket id**

Motion bucket id kiểm soát lượng chuyển động trong video. Giá trị càng cao thì chuyển động càng nhiều. Chấp nhận giá trị từ 0 đến 255.

**FPS**

Tham số `khung hình trên giây` (fps) kiểm soát số khung hình mà mô hình tạo ra. Giữ trong khoảng từ 5 đến 30 để có hiệu suất tối ưu.

**Mức độ tăng cường** (Augmentation level)

Mức tăng cường là lượng nhiễu được thêm vào hình ảnh ban đầu. Sử dụng mức này để thay đổi hình ảnh ban đầu nhiều hơn hoặc khi tạo video lệch khỏi kích thước mặc định.


### Hiệu suất của Stable Video Diffusion so với các mô hình video AI khác như thế nào?

Stability AI đã tự thực hiện nghiên cứu sâu rộng và so sánh mô hình tạo video của mình với các công cụ khác. Theo nghiên cứu, `Stable Video Diffusion` được so sánh với các mô hình như `Runway` và `Pika Labs`.

![Stable Video Diffusion](https://boxxv.github.io/img/2025/stable-video-diffusion-7.jpg "Stable Video Diffusion")

| Model | Strength | Weakness |
| -- | -- | -- |
| Stable Video Diffusion | Kết quả thực tế và mạch lạc, phù hợp cho video ngắn từ hình ảnh tĩnh | Chiều dài hạn chế, chất lượng thay đổi, khả năng sáng tạo hạn chế |
| Google Video Diffusion | Có thể tạo video dài hơn, tốt cho việc tạo văn bản thành video | Có thể tạo ra lỗi, cần phải tinh chỉnh (không ổn định lắm) |
| DALL-E 2 | Rất sáng tạo và thử nghiệm | Có thể kém ổn định hơn |
| Runway ML | Dễ sử dụng và tốt cho người mới bắt đầu | Khả năng hạn chế và không mạnh bằng các mẫu khác |
| Pika Labs | Mã nguồn mở | Cơ sở người dùng hạn chế, vẫn đang trong quá trình phát triển |

### Yêu cầu tính toán để chạy Stable Video Diffusion là gì?

Sau đây là một số yêu cầu để chạy `Stable Video Diffusion`:

| Yêu cầu | Tối thiểu | Khuyến khích |
| -- | -- | -- |
| Bộ xử lý đồ họa | Bộ nhớ RAM 6GB | 10 GB VRAM (hoặc cao hơn) |
| Bộ vi xử lý | 4 core | 8 lõi (hoặc cao hơn) |
| RAM | 16GB | 32GB (hoặc cao hơn) |
| Storage | 10GB | 20GB (hoặc cao hơn) |

Ngoài ra, bạn nên cài đặt Python 3.10 (hoặc cao hơn) trên hệ thống của mình trước.


## Sử dụng Stable Video Diffusion trên Colab

Bạn cần card GPU NVidia VRAM cao để chạy Stable Video Diffusion cục bộ. Nếu bạn không có, lựa chọn tốt nhất là Google Colab trực tuyến. Máy tính xách tay hoạt động với tài khoản miễn phí.

### Bước 1: Mở Sổ tay Colab

Đi đến trang [GitHub](https://github.com/sagiodev/stable-video-diffusion-img2vid/) của sổ tay Colab. Cho tôi một ngôi sao (Được rồi, tùy chọn này là tùy chọn…). Nhấp vào biểu tượng **Open in Colab** để mở sổ tay.

Đây là [liên kết trực tiếp](https://colab.research.google.com/github/sagiodev/stable-diffusion-img2vid/blob/main/stable_video_diffusion_img2vid.ipynb) đến sổ tay.

### Bước 2: Xem lại tùy chọn sổ ghi chép

Cài đặt mặc định là tốt. Nhưng bạn có thể tùy chọn không lưu video cuối cùng vào Google Drive của mình.

![Stable Video Diffusion](https://boxxv.github.io/img/2025/image-138-1024x327.png "Stable Video Diffusion")

### Bước 3: Chạy sổ ghi chép

Nhấp vào nút chạy để bắt đầu chạy sổ ghi chép.

### Bước 4: Khởi động GUI

Sau khi tải xong, bạn sẽ thấy liên kết `gradio.live` . Nhấp vào liên kết để bắt đầu GUI.

### Bước 5: Tải lên hình ảnh ban đầu

Thả một hình ảnh bạn muốn sử dụng làm khung hình đầu tiên của video.

Điều chỉnh độ lệch cắt (crop offset) để điều chỉnh vị trí cắt.

![Stable Video Diffusion](https://boxxv.github.io/img/2025/image-139-1024x484.webp "Stable Video Diffusion")

### Bước 6: Bắt đầu tạo video

Nhấp vào **Run** để bắt đầu tạo video. Video sẽ xuất hiện trên GUI khi hoàn tất.

https://stable-diffusion-art.com/wp-content/uploads/2023/11/000003.mp4

Mất khoảng 9 phút trên GPU T4 (tài khoản miễn phí) và 2 phút trên GPU V100.

### Tùy chỉnh video của bạn

Bạn có thể tăng thông số **ID Motion Bucket** trong cài đặt nâng cao để tăng chuyển động trong video.

Sử dụng một số nguyên cố định cho tham số hạt giống (seed) để tạo ra cùng một video.


## Sử dụng Stable Video Diffusion với ComfyUI

ComfyUI hiện hỗ trợ các mô hình Stable Video Diffusion SVD. Thực hiện theo các bước dưới đây để cài đặt và sử dụng quy trình làm việc [text-to-video](https://comfyanonymous.github.io/ComfyUI_examples/video/) (txt2vid). Nó tạo ra hình ảnh ban đầu bằng mô hình [Stable Diffusion XL](https://stable-diffusion-art.com/sdxl-model/) và một đoạn video clip bằng mô hình SVD XT.

Đọc [hướng dẫn cài đặt ComfyUI](https://stable-diffusion-art.com/how-to-install-comfyui/) và [hướng dẫn dành cho người mới bắt đầu sử dụng ComfyUI](https://stable-diffusion-art.com/comfyui/) nếu bạn mới sử dụng ComfyUI.

Nếu bạn sử dụng [sổ tay ComfyUI Colab](https://stable-diffusion-art.com/comfyui-colab/) của tôi , hãy chọn các mẫu **Stable_Video_Diffusion** và **SDXL_1** trước khi chạy sổ tay.

![Stable Video Diffusion](https://boxxv.github.io/img/2025/image-184-2048x931.png "Stable Video Diffusion")

### Bước 1: Tải quy trình làm việc chuyển văn bản thành video

Tải xuống quy trình làm việc ComfyUI bên dưới.

![Stable Video Diffusion](https://boxxv.github.io/img/2025/SDXL-text-to-video-2048x1005.png "Stable Video Diffusion")

> [Donwload](https://stable-diffusion-art.com/wp-content/uploads/2023/11/text_to_video_SDXL.json)

Kéo và thả nó vào ComfyUI.

### Bước 2: Cập nhật ComfyUI

[Cập nhật ComfyUI](https://stable-diffusion-art.com/comfyui/#How_to_update_ComfyUI), [cài đặt các nút tùy chỉnh bị thiếu](https://stable-diffusion-art.com/comfyui/#How_to_install_missing_custom_nodes) và [cập nhật tất cả các nút tùy chỉnh](https://stable-diffusion-art.com/comfyui/#How_to_update_custom_nodes). Sử dụng [trình quản lý ComfyUI](https://stable-diffusion-art.com/comfyui/#ComfyUI_Manager) sẽ giúp bước này dễ dàng hơn.

Khởi động lại ComfyUI hoàn toàn và tải lại quy trình làm việc văn bản thành video. ComfyUI sẽ không có khiếu nại nào nếu mọi thứ được cập nhật chính xác.

### Bước 3: Tải xuống mô hình

Tải xuống mô hình [SVD XT](https://huggingface.co/stabilityai/stable-video-diffusion-img2vid-xt/blob/main/svd_xt.safetensors). Đặt nó vào thư mục **ComfyUI > models > checkpoints**.

Làm mới trang ComfyUI và chọn mô hình SVD_XT trong nút **Image Only Checkpoint Loader**.

![Stable Video Diffusion](https://boxxv.github.io/img/2025/image-155.png "Stable Video Diffusion")

Quy trình làm việc sử dụng mô hình [SDXL 1.0](https://stable-diffusion-art.com/sdxl-model/). [Tải xuống mô hình](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0/blob/main/sd_xl_base_1.0.safetensors) nếu bạn chưa tải. Đặt nó vào thư mục **ComfyUI > models > checkpoints**.

Làm mới trang ComfyUI và chọn mô hình SDXL trong nút **Load Checkpoint**.

![Stable Video Diffusion](https://boxxv.github.io/img/2025/image-154.webp "Stable Video Diffusion")

### Bước 4: Chạy quy trình làm việc

Nhấp vào **Queue Prompt** để chạy quy trình làm việc. Một video sẽ được tạo ra.

**Các tham số**

**video_frame**: Số khung hình. Giữ nguyên ở mức 25 vì đây là số khung hình mà mô hình được đào tạo.

**motion_bucket_id**: Kiểm soát lượng chuyển động trong video. Giá trị càng cao thì chuyển động càng nhiều.

**fps**: Khung hình mỗi giây.

**Augmentation_level**: Lượng nhiễu được thêm vào hình ảnh ban đầu. Càng cao, video càng khác so với khung hình ban đầu. Tăng khi bạn sử dụng kích thước video khác với kích thước mặc định.

**min_cfg**: Đặt tỷ lệ CFG ở đầu video. Tỷ lệ CFG thay đổi tuyến tính theo giá trị `cfg` được xác định trong nút KSampler ở cuối video. Trong ví dụ này, min_cfg được đặt thành 1.0 và cfg được đặt thành 2.5. Tỷ lệ CFG là 1.0 cho khung hình đầu tiên, 2.5 cho khung hình cuối cùng và thay đổi tuyến tính ở giữa. Càng xa khung hình đầu tiên, tỷ lệ CFG càng cao.


## Cài đặt Stable Video Diffusion trên Windows

Bạn có thể chạy Stable Video Difusion cục bộ nếu bạn có card GPU RAM cao. Quy trình cài đặt sau đây được thử nghiệm với card RTX4090 24GB.

Rất khó để cài đặt phần mềm này cục bộ. Bạn có thể gặp phải các vấn đề không được mô tả trong phần này. Vì vậy, chỉ tiến hành nếu bạn am hiểu công nghệ hoặc muốn…

Bạn sẽ cần git và Python 3.10 để cài đặt và sử dụng phần mềm. Xem [hướng dẫn cài đặt](https://stable-diffusion-art.com/install-windows/) Stable Diffusion để biết các bước cài đặt.

### Bước 1: Sao chép kho lưu trữ

Mở ứng dụng `PowerShell`. KHÔNG sử dụng Command Prompt (cmd). Nó sẽ không hoạt động với các hướng dẫn này.

Để mở ứng dụng PowerShell, hãy nhấn phím Windows và tìm kiếm “PowerShell”. Nhấp vào ứng dụng `Windows PowerShell` để bắt đầu.

![Stable Video Diffusion](https://boxxv.github.io/img/2025/image-156.png "Stable Video Diffusion")

Trước khi bắt đầu, hãy xác nhận bạn có Python 3.10 bằng cách chạy lệnh sau.

```bash
python --version
```

Bạn có thể tiếp tục nếu nó hiển thị “Python 3.10.x”.

Bạn có thể thay đổi thư mục đến nơi bạn muốn cài đặt phần mềm.

```bash
git clone https://github.com/Stability-AI/generative-models
```

### Bước 2: Tạo môi trường ảo

Vào thư mục vừa được sao chép.

```bash
cd generative-models
```

Tạo môi trường ảo.

```bash
python -m venv venv
```

Bạn sẽ thấy thư mục có tên `venv` được tạo.  
Kích hoạt môi trường ảo.

```bash
.\venv\Scripts\Activate.ps1
```

Nếu lệnh này thành công, bạn sẽ thấy (venv) ở phía trước dấu nhắc lệnh. Điều này cho biết bạn hiện đang ở trong môi trường ảo.

Bạn phải ở trong môi trường ảo khi cài đặt hoặc chạy phần mềm.

Nếu bạn không thấy nhãn (venv) ở bước sau, hãy chạy tập lệnh activate.ps1 để vào môi trường ảo.

### Bước 3: Xóa gói triton trong yêu cầu

Trong ứng dụng **File Explorer**, điều hướng đến thư mục **generative-models > requirements**.

Mở tệp yêu cầu **pt2.txt** bằng ứng dụng **Notepad**.

Xóa dòng “triton==2.0.0”. Điều này không thực sự cần thiết và sẽ gây ra lỗi trong Windows.

Lưu và đóng tệp.

### Bước 4: Cài đặt các thư viện cần thiết

Quay lại ứng dụng `PowerShell`. Đảm bảo bạn vẫn thấy nhãn (venv).

Chạy lệnh sau để cài đặt PyTorch.

```bash
pip3 install torch==2.0.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

Chạy lệnh sau để cài đặt các thư viện cần thiết.

```bash
pip3 install -r .\requirements\pt2.txt
```

Chạy lệnh sau để cài đặt phần mềm mô hình tạo sinh.

```bash
pip3 install .
```

Chạy lệnh sau để cài đặt thư viện cần thiết.

```bash
pip3 install -e git+https://github.com/Stability-AI/datapipelines.git@main#egg=sdata
```

### Bước 5: Tải xuống mô hình video

Trong ứng dụng **File Explorer**, hãy điều hướng đến thư mục **generative-models** và tạo một thư mục có tên là “checkpoints”.

Điều hướng đến thư mục **generative-models > checkpoints**.

Tải xuống mô hình [safetensors](https://huggingface.co/stabilityai/stable-video-diffusion-img2vid-xt/blob/main/svd_xt.safetensors) (svd_xt.safetensors) và đặt nó vào thư mục mô hình điểm kiểm tra.

### Bước 6: Chạy GUI

Quay lại ứng dụng PowerShell. Bạn sẽ ở trong thư mục generative-models và trong môi trường ảo.

Chạy lệnh sau để thiết lập đường dẫn Python.

```bash
$ENV:PYTHONPATH=$PWD
```

Chạy lệnh sau để khởi động GUI.

```bash
streamlit run scripts/demo/video_sampling.py
```

Một trang web mới sẽ được mở. Nếu không, hãy xem bản in của thiết bị đầu cuối PowerApp. Đi đến URL cục bộ. Nó sẽ giống như thế này:

>http://localhost:8501

### Bước 7: Tạo video

Trong menu thả xuống **Model Version**, chọn **svd_xt**.

Nhấp vào hộp kiểm **Load Model**.

![Stable Video Diffusion](https://boxxv.github.io/img/2025/image-140.webp "Stable Video Diffusion")

Hãy chú ý đến lỗi của thiết bị đầu cuối PowerShell.

Nó có thể hiển thị thông báo lỗi trong GUI. Nhưng không sao miễn là phần **Input** mới xuất hiện.

![Stable Video Diffusion](https://boxxv.github.io/img/2025/image-141.png "Stable Video Diffusion")

Thả một hình ảnh làm khung ban đầu vào hộp **Input**.

Cuộn xuống và tìm trường **Decode t frames at a time**. Đặt thành 1.

![Stable Video Diffusion](https://boxxv.github.io/img/2025/image-142.webp "Stable Video Diffusion")

Nhấp vào **Sample** để bắt đầu tạo video.

Theo dõi tiến trình trên thiết bị đầu cuối PowerShell.

Khi hoàn tất, video sẽ hiển thị trên GUI.

![Stable Video Diffusion](https://boxxv.github.io/img/2025/image-143.png "Stable Video Diffusion")

Đóng ứng dụng PowerShell khi bạn thực hiện xong.

### Bắt đầu lại GUI

Để khởi động lại GUI, hãy mở Ứng dụng PowerShell.

Điều hướng đến thư mục generative-models.

```bash
cd generative-models
```

Kích hoạt môi trường ảo.

```bash
.\venv\Scripts\Activate.ps1
```

Chạy lệnh sau để thiết lập đường dẫn Python.

```bash
$ENV:PYTHONPATH=$PWD
```

Chạy lệnh sau để khởi động GUI.

```bash
streamlit run scripts/demo/video_sampling.py
```


## Tài nguyên

[Stable Video Diffusion Colab notebook](https://github.com/sagiodev/stable-video-diffusion-img2vid/)

[Introducing Stable Video Diffusion](https://stability.ai/news/stable-video-diffusion-open-ai-video-model) – Official press release of SVD.

[Stable Video Diffusion: Scaling Latent Video Diffusion Models to Large Datasets](https://stability.ai/research/stable-video-diffusion-scaling-latent-video-diffusion-models-to-large-datasets) – The research paper.

[Stability-AI/generative-models: Generative Models by Stability AI](https://github.com/Stability-AI/generative-models) – code on GitHub page.

[stabilityai/stable-video-diffusion-img2vid-xt](https://huggingface.co/stabilityai/stable-video-diffusion-img2vid-xt) – Model weights on Hugging Face.


-----
Tham khảo:
- [How to run Stable Video Diffusion img2vid](https://stable-diffusion-art.com/stable-video-diffusion-img2vid/)
- [Stable Video Diffusion: Here’s Everything You Need to Know](https://www.ifoto.ai/blog/stable-video-diffusion/)
- []()