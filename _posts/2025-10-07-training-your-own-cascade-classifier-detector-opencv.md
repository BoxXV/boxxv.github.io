---
layout: post
title: "Đào tạo Cascade/Classifier/Detector của riêng bạn trong OpenCV"
subtitle: "Training your own Cascade/Classifier/Detector — OpenCV"
date: 2025-10-07 01:00:00
tags:
- Haar
- Cascade
- OpenCV
- Classifier
- Detector
- Python
---

- [Điều kiện tiên quyết:](#điều-kiện-tiên-quyết)
- [Các bước](#các-bước)
  - [Bước 1: Chuẩn bị dữ liệu](#bước-1-chuẩn-bị-dữ-liệu)
  - [Bước 2: Tạo file mô tả (description file)](#bước-2-tạo-file-mô-tả-description-file)
    - [Sử dụng công cụ chú thích tích hợp của OpenCV](#sử-dụng-công-cụ-chú-thích-tích-hợp-của-opencv)
  - [Bước 3: Tạo file .txt mô tả đường dẫn đến các ảnh negative](#bước-3-tạo-file-txt-mô-tả-đường-dẫn-đến-các-ảnh-negative)
  - [Bước 4: Tạo file vector từ ảnh positive](#bước-4-tạo-file-vector-từ-ảnh-positive)
  - [Bước 5: Huấn luyện mô hình Haar Cascade](#bước-5-huấn-luyện-mô-hình-haar-cascade)
  - [Bước 6](#bước-6)


Khuôn mặt ở khắp mọi nơi! Từ ảnh tự sướng cơ bản đến hệ thống nhận dạng khuôn mặt thông minh.

OpenCV tích hợp một số tầng cơ bản có ứng dụng thực tế rất tốt như Nhận diện Khuôn mặt, Nhận dạng Biển số xe, v.v.

Bạn đã bao giờ tự hỏi rằng mình có thể tạo tầng của riêng mình để phát hiện bất kỳ vật thể nào bạn muốn chưa? Vật thể có thể đơn giản là bất cứ thứ gì như trái cây, quả bóng, cây bút, chai, v.v. miễn là bạn có một số hình ảnh dương của vật thể đó.

Hình ảnh dương là hình ảnh chứa vật thể của chúng ta. Ví dụ: hình ảnh dương của quả chuối nên có hình quả chuối trong mỗi hình ảnh, bất kể nền là gì. Ví dụ:

![Training a Haar Cascade Object Detector in OpenCV](https://boxxv.github.io/img/2025/1_EW1kZtcOaoiY_UiSM_DFQw.jpg "Photo by Adrià Crehuet Cano. Some rights reserved.")

Ảnh âm bản có thể là bất kỳ hình ảnh nào miễn là nó không chứa vật thể cụ thể. Đối với ví dụ về quả chuối, nó có thể là bất kỳ hình ảnh nào miễn là không có quả chuối.

Để có một bộ phân loại/phân tầng mạnh mẽ hơn, bạn sẽ cần rất nhiều ảnh dương bản và âm bản.

Chúng ta sẽ tập trung vào việc tạo một bộ phân loại/phân tầng/bộ dò cho một chiếc ô tô. Tôi sẽ sử dụng các thuật ngữ phân tầng/phân loại/bộ dò thay thế cho nhau.


# Điều kiện tiên quyết:

- Python (trình độ sơ cấp)
- OpenCV (trình độ sơ cấp)


# Các bước

## Bước 1: Chuẩn bị dữ liệu

Để có được ảnh dương, chúng ta sẽ sử dụng Cơ sở dữ liệu hình ảnh để phát hiện xe, có sẵn [tại đây](https://cogcomp.seas.upenn.edu/Data/Car/). Bạn có thể tải xuống và trích xuất nội dung vào thư mục của mình. Sau khi trích xuất, bạn sẽ thấy ảnh âm và ảnh dương nằm trong thư mục TrainImages — 500 Ảnh âm, 550 Ảnh dương. Hãy trích xuất cả hai vào các thư mục riêng biệt như sau:

![TrainImages](https://boxxv.github.io/img/2025/1_2CFnl8gZEwt0GkVAmXTYZQ.png "TrainImages")


> [CarData.tar.gz](https://github.com/stackprogramer/ObjectDetectorProject.github.io/blob/master/database%20std/CarData.tar.gz)

## Bước 2: Tạo file mô tả (description file)

Để tạo ra chuỗi phản hồi, bây giờ chúng ta cần tạo tệp cars.info chứa thông tin cần thiết để đào tạo hình ảnh tích cực.

![Cars.info](https://boxxv.github.io/img/2025/1_LIOdqXyEFXn0DHzKmHpctw.webp "Cars.info")

> [cars.info.txt](https://github.com/stackprogramer/ObjectDetectorProject.github.io/blob/master/database%20std/cars.info.txt)

`pos/pos-0.pgm` → Vị trí của ảnh dương.

`1` → Số lượng vật thể có trong ảnh

`0 0 100 40` → Vị trí của ảnh. 0 0 là tọa độ x và y, 100 40 là chiều rộng và chiều cao sao cho ảnh trải dài từ (0,0) đến chiều rộng = 100 và chiều cao = 40.

Nếu bạn có 2 hoặc nhiều đối tượng, hình ảnh cụ thể của bạn trong cars.info sẽ trở thành

```txt
pos/pos-1.pgm 2 0 0 100 40 1 1 80 60

For Object 1, (0,0) to Width = 100, Height =40

For Object 2, (1,1) to Width = 80, Height = 60
```

Tôi đã tạo tệp cars.info và bạn có thể tải xuống [tại đây](https://github.com/abhi-kumar/CAR-DETECTION/blob/master/cars.info).


Data Annotation Tools:
0. opencv_annotation
1. LabelImg
2. RectLabel
3. VGG Image Annotator (VIA)
4. Labelbox
5. Supervisely
6. Annotator
7. CVAT (Computer Vision Annotation Tool)
8. LabelMe
9. Sloth
10. TagTog
11. ImageTagger
12. GATE (General Architecture for Text Engineering)
13. Siafoo
14. doccano

### Sử dụng công cụ chú thích tích hợp của OpenCV

Kể từ OpenCV 3.x, cộng đồng đã cung cấp và duy trì một công cụ chú thích nguồn mở, được sử dụng để tạo -infotệp. Công cụ này có thể được truy cập bằng lệnh opencv_annotation nếu các ứng dụng OpenCV được xây dựng.

Việc sử dụng công cụ này khá đơn giản. Công cụ chấp nhận một số tham số bắt buộc và một số tham số tùy chọn:

- `--annotations` **(bắt buộc)**: đường dẫn đến tệp txt chú thích, nơi bạn muốn lưu trữ chú thích của mình, sau đó được truyền đến -info tham số [ví dụ - /data/annotations.txt]
- `--images` **(bắt buộc)**: đường dẫn đến thư mục chứa hình ảnh có đối tượng của bạn [ví dụ - /data/testimages/]
- `--maxWindowHeight` (tùy chọn): nếu hình ảnh đầu vào có chiều cao lớn hơn độ phân giải được cung cấp ở đây, hãy thay đổi kích thước hình ảnh để chú thích dễ dàng hơn bằng cách sử dụng `--resizeFactor`.
- `--resizeFactor` (tùy chọn): hệ số được sử dụng để thay đổi kích thước hình ảnh đầu vào khi sử dụng `--maxWindowHeight` tham số.

Lưu ý rằng các tham số tùy chọn chỉ có thể được sử dụng cùng nhau. Ví dụ về lệnh có thể được sử dụng có thể được xem bên dưới.

```bat
opencv_annotation --annotations=/path/to/annotations/file.txt --images=/path/to/image/folder/
opencv_annotation -a=/path/to/annotations/file.txt -i=/path/to/image/folder/
```

Lệnh này sẽ mở ra một cửa sổ chứa hình ảnh đầu tiên và con trỏ chuột của bạn, được sử dụng để chú thích. Video hướng dẫn sử dụng công cụ chú thích có thể được tìm thấy tại đây . Về cơ bản, có một số phím tắt kích hoạt một hành động. Nút chuột trái được sử dụng để chọn góc đầu tiên của đối tượng, sau đó tiếp tục vẽ cho đến khi bạn hoàn tất, và dừng lại khi nhấp chuột trái lần thứ hai. Sau mỗi lần chọn, bạn có các lựa chọn sau:

- Nhấn c: xác nhận chú thích, chuyển chú thích sang màu xanh lá cây và xác nhận chú thích đã được lưu trữ
- Nhấn d: xóa chú thích cuối cùng khỏi danh sách chú thích (dễ dàng để xóa chú thích sai)
- Nhấn n: tiếp tục đến hình ảnh tiếp theo
- Nhấn ESC: thao tác này sẽ thoát khỏi phần mềm chú thích

Cuối cùng, bạn sẽ có được một tệp chú thích có thể sử dụng được và có thể truyền vào `-info` đối số của opencv_createsamples.


## Bước 3: Tạo file .txt mô tả đường dẫn đến các ảnh negative

Để mô tả tất cả các hình ảnh tiêu cực, chúng tôi chỉ cần thu thập tên của chúng trong tệp bg.txt. Bạn có thể tìm thấy tệp này [tại đây](https://github.com/abhi-kumar/CAR-DETECTION/blob/master/bg.txt).


## Bước 4: Tạo file vector từ ảnh positive

Bây giờ chúng ta tạo một tệp vec bằng OpenCV. Trong dấu nhắc lệnh (trong thư mục gốc), hãy chạy lệnh:

```bat
opencv_createsamples -info cars.info -num 550 -w 48 -h 24 -vec cars.vec
```

Với windows 11 24H2

```bat
.\opencv_createsamples -info cars.info -num 550 -w 48 -h 24 -vec cars.vec
```

`num` → số lượng đối tượng chúng ta có.

`w,h` → chiều rộng và chiều cao của dữ liệu huấn luyện mà chúng ta muốn tạo.

Thao tác này sẽ tạo `cars.vec` trong thư mục gốc.

> Nếu bạn gặp lỗi ở đây về “opencv_createsamples is not recognized…”, hãy giải nén tệp [zip](https://github.com/tankvn/opencv/blob/main/opencv/3.4.16/build/x64/vc15/bin/OpenCV_Dependencies.zip) này vào cấu trúc thư mục của dự án.

![folder structure of your project](https://boxxv.github.io/img/2025/1_bhnOnG7UR6WvZntMutBllw.webp "folder structure of your project")

Để kiểm tra `cars.vec` đã tạo xem có hợp lệ không, hãy chạy lệnh

```bat
opencv_createsamples -vec cars.vec -w 48 -h 24
```

Với windows 11 24H2

```bat
.\opencv_createsamples.exe -vec cars.vec -w 48 -h 24
```

## Bước 5: Huấn luyện mô hình Haar Cascade

Để đào tạo cascade, bây giờ chúng ta sẽ tạo một thư mục có tên là data và chạy

```bat
opencv_traincascade -data data -vec cars.vec -bg bg.txt -numPos 500 -numNeg 500 -numStages 10 -w 48 -h 24 -featureType LBP
.\opencv_traincascade -data data -vec cars.vec -bg bg.txt -numPos 500 -numNeg 500 -numStages 10 -w 48 -h 24 -featureType Haar
```

Số lượng numStages càng nhiều thì mô hình của chúng ta càng tốt.

Phân tích từng tham số:

| Tham số | Upvotes |
| -- | -- |
| opencv_traincascade  | Công cụ training cascade classifier |
| -data data | Thư mục lưu model đã train (output) |
| -vec cars.vec | File chứa ảnh positive samples (ảnh có xe) |
| -bg bg.txt | File text liệt kê đường dẫn ảnh negative (không có xe) |
| -numPos 500 | Số ảnh positive dùng mỗi stage |
| -numNeg 500 | Số ảnh negative dùng mỗi stage |
| -numStages 10 | Số stages của cascade (10 tầng lọc) |
| -w 48 | Chiều rộng cửa sổ training (48 pixels) |
| -h 24 | Chiều cao cửa sổ training (24 pixels) |
| -featureType LBP | Dùng LBP features (nhanh hơn Haar) |

Quy trình hoạt động:
1. **Load dữ liệu**: Đọc 500 ảnh positive từ `cars.vec` và 500 ảnh negative từ `bg.txt`
2. **Training 10 stages**: Mỗi stage học phân biệt xe/không phải xe
3. **Tạo cascade**: Các stage xếp tầng - ảnh phải qua hết 10 stage mới được xác định là xe
4. **Output**: File `cascade.xml` trong thư mục `data/` để dùng cho detection

Thời gian training:
- **LBP**: ~vài giờ đến 1 ngày
- **Haar**: ~vài ngày đến 1 tuần

Haartraining được cho là mang lại kết quả tốt hơn traincascade nhưng lại cực kỳ chậm. Đôi khi có thể mất một đến hai tuần để đào tạo một bộ phân loại.

🧰 Công cụ hỗ trợ  
Bạn có thể dùng script Python như `opencv_traincascade_gui` hoặc các công cụ như:  
https://amin-ahmadi.com/cascade-trainer-gui/  (GUI cho việc huấn luyện Haar Cascade)

## Bước 6

Bây giờ, trong thư mục dữ liệu, chúng ta có `cascade.xml`, đây là cascade cuối cùng và có thể được sử dụng để phát hiện xe. Nó cũng chứa các tệp xml theo từng giai đoạn sau mỗi giai đoạn.

![car detection](https://boxxv.github.io/img/2025/1__VyzPUivE6Z7HdcWPlkw9A.webp "car detection")

Hãy tự kiểm tra chuỗi sự kiện của riêng bạn và cho tôi biết kết quả nhé.

Hãy vỗ tay nếu câu chuyện này hữu ích với bạn nhé.


-----
Tham khảo:
- [Training a Haar Cascade Object Detector in OpenCV](https://machinelearningmastery.com/training-a-haar-cascade-object-detector-in-opencv/)
- [OpenCV Tutorial: Training your own detector packtpub.com](https://youtu.be/WEzm7L5zoZE)
- [Official tutorial on training a Cascade Classifier](https://docs.opencv.org/4.12.0/dc/d88/tutorial_traincascade.html)
- [Training a Cascade Classifier - OpenCV Object Detection in Games #8](https://youtu.be/XrCAvs9AePM)
- [OpenCV Object Detection in Games](https://www.youtube.com/playlist?list=PL1m2M8LQlzfKtkKq2lK5xko4X-8EZzFPI)
- [How to install OpenCV on Windows 2025](https://youtu.be/EqoH3gspQGg)
- [Training your own Cascade/Classifier/Detector — OpenCV](https://dikshit18.medium.com/training-your-own-cascade-classifier-detector-opencv-9ea6055242c2)
- [TRAINCASCADE AND CAR DETECTION USING OPENCV](https://abhishek4273.wordpress.com/2014/03/16/traincascade-and-car-detection-using-opencv/)
- [Haar Cascade là gì? Luận về một kỹ thuật chuyên dùng để nhận biết các khuôn mặt trong ảnh](https://viblo.asia/p/haar-cascade-la-gi-luan-ve-mot-ky-thuat-chuyen-dung-de-nhan-biet-cac-khuon-mat-trong-anh-E375zamdlGW)
- [Phát hiện đối tượng – P1: lý thuyết](https://thigiacmaytinh.com/phat-hien-doi-tuong-p1-ly-thuyet/)
- [Phát hiện vật thể – P2: thực hành](https://thigiacmaytinh.com/phat-hien-vat-the-p2-thuc-hanh/)
- [OpenCV With Python Part 1](https://viblo.asia/p/opencv-with-python-part-1-924lJXQaKPM)
- [OpenCV With Python Part 2](https://viblo.asia/p/opencv-with-python-part-2-L4x5xRRBZBM)
- [OpenCV With Python Part 3](https://viblo.asia/p/opencv-with-python-part-3-RQqKLn90l7z)
- [OpenCV With Python Part 4](https://viblo.asia/p/opencv-with-python-part-4-yMnKM3Qjl7P)
- [OpenCV With Python Part 5](https://viblo.asia/p/opencv-with-python-part-5-eW65GoYL5DO)
- [OpenCV With Python Part 6](https://viblo.asia/p/opencv-with-python-part-6-XL6lAP8mZek)
- [OpenCV With Python Part 7](https://viblo.asia/p/opencv-with-python-part-7-E375zezWlGW)
- [OpenCV With Python Part 8](https://viblo.asia/p/opencv-with-python-part-8-924lJYgWZPM)
- [OpenCV With Python Part 9 (Làm mờ và làm mịn)](https://viblo.asia/p/opencv-with-python-part-9-lam-mo-va-lam-min-yMnKM1LQK7P)
- [OpenCV With Python Part 10 (Biến đổi hình thái học)](https://viblo.asia/p/opencv-with-python-part-10-bien-doi-hinh-thai-hoc-naQZR1LGKvx)
- [OpenCV With Python Part 11 (Canny Edge Detection và Gradients)](https://viblo.asia/p/opencv-with-python-part-11-canny-edge-detection-va-gradients-OeVKBR02KkW)
- [OpenCV With Python Part 12 (Template Matching)](https://viblo.asia/p/opencv-with-python-part-12-template-matching-RQqKLv14l7z)
- [OpenCV With Python Part 13 (Interactive Foreground Extraction using GrabCut Algorithm)](https://viblo.asia/p/opencv-with-python-part-13-interactive-foreground-extraction-using-grabcut-algorithm-bWrZnpEv5xw)
- [OpenCV With Python Part 14 (Corner Detection)](https://viblo.asia/p/opencv-with-python-part-14-corner-detection-6J3ZgOGgZmB)
- [OpenCV With Python Part 15 (Feature Matching Brute Force)](https://viblo.asia/p/opencv-with-python-part-15-feature-matching-brute-force-gGJ59kzpZX2)
- [OpenCV With Python Part 16 (MOG Background Reduction And Subtractor)](https://viblo.asia/p/opencv-with-python-part-16-mog-background-reduction-and-subtractor-vyDZODnklwj)
- [OpenCV With Python Part 16 (Haar Cascade Object Detection Facer)](https://viblo.asia/p/opencv-with-python-part-16-haar-cascade-object-detection-face-07LKXmWeZV4)
- [OpenCV Haar Cascades](https://pyimagesearch.com/2021/04/12/opencv-haar-cascades/)
- [OpenCV Face Detection: Cascade Classifier vs. YuNet](https://opencv.org/blog/opencv-face-detection-cascade-classifier-vs-yunet/)
- []()