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
  - [Bước 1](#bước-1)
  - [Bước 2](#bước-2)
  - [Bước 3](#bước-3)
  - [Bước 4](#bước-4)
  - [Bước 5](#bước-5)
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

## Bước 1

Để có được ảnh dương, chúng ta sẽ sử dụng Cơ sở dữ liệu hình ảnh để phát hiện xe, có sẵn [tại đây](https://cogcomp.seas.upenn.edu/Data/Car/). Bạn có thể tải xuống và trích xuất nội dung vào thư mục của mình. Sau khi trích xuất, bạn sẽ thấy ảnh âm và ảnh dương nằm trong thư mục TrainImages — 500 Ảnh âm, 550 Ảnh dương. Hãy trích xuất cả hai vào các thư mục riêng biệt như sau:

![TrainImages](https://boxxv.github.io/img/2025/1_2CFnl8gZEwt0GkVAmXTYZQ.png "TrainImages")


## Bước 2

Để tạo ra chuỗi phản hồi, bây giờ chúng ta cần tạo tệp cars.info chứa thông tin cần thiết để đào tạo hình ảnh tích cực.

![Cars.info](https://boxxv.github.io/img/2025/1_LIOdqXyEFXn0DHzKmHpctw.webp "Cars.info")


`pos/pos-0.pgm` → Vị trí của ảnh dương.

`1` → Số lượng vật thể có trong ảnh

`0 0 100 40` → Vị trí của ảnh. 0 0 là tọa độ x và y, 100 40 là chiều rộng và chiều cao sao cho ảnh trải dài từ (0,0) đến chiều rộng = 100 và chiều cao = 40.

Nếu bạn có 2 hoặc nhiều đối tượng, hình ảnh cụ thể của bạn trong cars.info sẽ trở thành

```txt
pos/pos-1.pgm 2 0 0 100 40 1 1 80 60

For Object 1, (0,0) to Width = 100, Height =40

For Object 2, (1,1) to Width = 80, Height = 60
```

Tôi đã tạo tệp cars.info và bạn có thể tải xuống [tại đây](https://s3.ap-south-1.amazonaws.com/mediumarticlebucketclassifer/cars.info).


## Bước 3

Để mô tả tất cả các hình ảnh tiêu cực, chúng tôi chỉ cần thu thập tên của chúng trong tệp bg.txt. Bạn có thể tìm thấy tệp này [tại đây](https://s3.ap-south-1.amazonaws.com/mediumarticlebucketclassifer/bg.txt).


## Bước 4

Bây giờ chúng ta tạo một tệp vec bằng OpenCV. Trong dấu nhắc lệnh (trong thư mục gốc), hãy chạy lệnh:

```bat
opencv_createsamples -info cars.info -num 550 -w 48 -h 24 -vec cars.vec
```

`num` → số lượng đối tượng chúng ta có.

`w,h` → chiều rộng và chiều cao của dữ liệu huấn luyện mà chúng ta muốn tạo.

Thao tác này sẽ tạo `cars.vec` trong thư mục gốc.

> Nếu bạn gặp lỗi ở đây về “opencv_createsamples is not recognized…”, hãy giải nén tệp [zip](https://s3.ap-south-1.amazonaws.com/mediumarticlebucketclassifer/OpenCV_Dependencies.rar) này vào cấu trúc thư mục của dự án.

![folder structure of your project](https://boxxv.github.io/img/2025/1_bhnOnG7UR6WvZntMutBllw.webp "folder structure of your project")

Để kiểm tra `cars.vec` đã tạo xem có hợp lệ không, hãy chạy lệnh

```bat
opencv_createsamples -vec cars.vec -w 48 -h 24
```

## Bước 5

Để đào tạo cascade, bây giờ chúng ta sẽ tạo một thư mục có tên là data và chạy

```bat
opencv_traincascade -data data -vec cars.vec -bg bg.txt -numPos 500 -numNeg 500 -numStages 10-w 48 -h 24 -featureType LBP
```

Số lượng numStages càng nhiều thì mô hình của chúng ta càng tốt.

## Bước 6

Bây giờ, trong thư mục dữ liệu, chúng ta có `cascade.xml`, đây là cascade cuối cùng và có thể được sử dụng để phát hiện xe. Nó cũng chứa các tệp xml theo từng giai đoạn sau mỗi giai đoạn.

![car detection](https://boxxv.github.io/img/2025/1__VyzPUivE6Z7HdcWPlkw9A.webp "car detection")

Hãy tự kiểm tra chuỗi sự kiện của riêng bạn và cho tôi biết kết quả nhé.

Hãy vỗ tay nếu câu chuyện này hữu ích với bạn nhé.


-----
Tham khảo:
- [Training a Haar Cascade Object Detector in OpenCV](https://machinelearningmastery.com/training-a-haar-cascade-object-detector-in-opencv/)
- [Official tutorial on training a Cascade Classifier](https://docs.opencv.org/4.12.0/dc/d88/tutorial_traincascade.html)
- [Training a Cascade Classifier - OpenCV Object Detection in Games #8](https://youtu.be/XrCAvs9AePM)
- [OpenCV Object Detection in Games](https://www.youtube.com/playlist?list=PL1m2M8LQlzfKtkKq2lK5xko4X-8EZzFPI)
- [How to install OpenCV on Windows | 2025](https://youtu.be/EqoH3gspQGg)
- [Training your own Cascade/Classifier/Detector — OpenCV](https://dikshit18.medium.com/training-your-own-cascade-classifier-detector-opencv-9ea6055242c2)
- []()