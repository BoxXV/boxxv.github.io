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
- [Sử dụng Stable Video Diffusion trên Colab](#sử-dụng-stable-video-diffusion-trên-colab)
  - [Bước 1: Mở Sổ tay Colab](#bước-1-mở-sổ-tay-colab)
  - [Bước 2: Xem lại tùy chọn sổ ghi chép](#bước-2-xem-lại-tùy-chọn-sổ-ghi-chép)
  - [Bước 3: Chạy sổ ghi chép](#bước-3-chạy-sổ-ghi-chép)
  - [Bước 4: Khởi động GUI](#bước-4-khởi-động-gui)
  - [Bước 5: Tải lên hình ảnh ban đầu](#bước-5-tải-lên-hình-ảnh-ban-đầu)
  - [Bước 6: Bắt đầu tạo video](#bước-6-bắt-đầu-tạo-video)
  - [Tùy chỉnh video của bạn](#tùy-chỉnh-video-của-bạn)
- [Sử dụng Stable Video Diffusion với ComfyUI](#sử-dụng-stable-video-diffusion-với-comfyui)
  - [Bước 1: Mở Sổ tay Colab](#bước-1-mở-sổ-tay-colab-1)
  - [Bước :](#bước-)
  - [Bước :](#bước--1)
  - [Bước :](#bước--2)
  - [](#)
- [Cài đặt Stable Video Diffusion trên Windows](#cài-đặt-stable-video-diffusion-trên-windows)
  - [Bước 1: Mở Sổ tay Colab](#bước-1-mở-sổ-tay-colab-2)
  - [Bước :](#bước--3)
  - [Bước :](#bước--4)
  - [Bước :](#bước--5)
  - [](#-1)
- [Tổng kết](#tổng-kết)


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

### Bước 1: Mở Sổ tay Colab

### Bước :

### Bước :

### Bước :

### 


## Cài đặt Stable Video Diffusion trên Windows

### Bước 1: Mở Sổ tay Colab

### Bước :

### Bước :

### Bước :

### 

## Tổng kết




-----
Tham khảo:
- [How to run Stable Video Diffusion img2vid](https://stable-diffusion-art.com/stable-video-diffusion-img2vid/)
- [Stable Video Diffusion: Here’s Everything You Need to Know](https://www.ifoto.ai/blog/stable-video-diffusion/)
- []()