---
layout: post
title: Đào tạo Trình phát hiện đối tượng Haar Cascade trong OpenCV
subtitle: Training a Haar Cascade Object Detector in OpenCV
date: 2025-10-05 01:00:00
tags:
- Haar
- Cascade
- OpenCV
- Detector
---

- [Tổng quan](#tổng-quan)
- [Vấn đề huấn luyện bộ phân loại theo tầng trong OpenCV](#vấn-đề-huấn-luyện-bộ-phân-loại-theo-tầng-trong-opencv)
- [Thiết lập môi trường](#thiết-lập-môi-trường)
- [Tổng quan về huấn luyện bộ phân loại Cascade](#tổng-quan-về-huấn-luyện-bộ-phân-loại-cascade)
- [Chuẩn bị dữ liệu đào tạo](#chuẩn-bị-dữ-liệu-đào-tạo)
- [Đào tạo phân loại Haar Cascade](#đào-tạo-phân-loại-haar-cascade)
- [Đọc thêm](#đọc-thêm)
  - [Sách](#sách)
  - [Trang web](#trang-web)
- [Tóm tắt](#tóm-tắt)


Sử dụng bộ phân loại Haar Cascade trong OpenCV rất đơn giản. Bạn chỉ cần cung cấp mô hình đã được huấn luyện trong tệp XML để tạo bộ phân loại. Tuy nhiên, việc huấn luyện một mô hình từ đầu không hề đơn giản. Trong hướng dẫn này, bạn sẽ thấy quá trình huấn luyện nên diễn ra như thế nào. Cụ thể, bạn sẽ học:

- Các công cụ để huấn luyện Haar Cascade trong OpenCV là gì?
- Cách chuẩn bị dữ liệu để huấn luyện
- Cách chạy huấn luyện

Hãy bắt đầu dự án của bạn với cuốn sách [Học Máy trong OpenCV](https://machinelearning.samcart.com/products/machine-learning-opencv/). Cuốn sách cung cấp các hướng dẫn tự học kèm theo mã nguồn.

Hãy bắt đầu nào.

![Training a Haar Cascade Object Detector in OpenCV](https://machinelearningmastery.com/wp-content/uploads/2023/12/adria-crehuet-cano-LIhB1_mAGhY-unsplash-1024x717.jpg "Photo by Adrià Crehuet Cano. Some rights reserved.")


# Tổng quan

Bài viết này được chia thành năm phần:

- Vấn đề huấn luyện bộ phân loại tầng trong OpenCV
- Thiết lập môi trường
- Tổng quan về huấn luyện bộ phân loại tầng
- Chuẩn bị dữ liệu huấn luyện
- Huấn luyện bộ phân loại Haar Cascade


# Vấn đề huấn luyện bộ phân loại theo tầng trong OpenCV

OpenCV đã tồn tại trong nhiều năm và có nhiều phiên bản. OpenCV 5 đang được phát triển tại thời điểm viết bài này và phiên bản được đề xuất là OpenCV 4, hay chính xác là phiên bản 4.8.0.

Đã có rất nhiều cải tiến giữa OpenCV 3 và OpenCV 4. Đáng chú ý nhất là một lượng lớn mã đã được viết lại. Sự thay đổi này rất đáng kể và khá nhiều hàm đã được thay đổi. Điều này bao gồm cả công cụ huấn luyện bộ phân loại theo tầng Haar.

Bộ phân loại theo tầng không phải là một mô hình đơn giản như SVM mà bạn có thể huấn luyện dễ dàng. Nó là một mô hình tập hợp sử dụng AdaBoost. Do đó, quá trình huấn luyện bao gồm nhiều bước. OpenCV 3 có một công cụ dòng lệnh để hỗ trợ việc huấn luyện như vậy, nhưng công cụ này đã bị lỗi trong OpenCV 4. Bản sửa lỗi hiện vẫn chưa có.

Do đó, chỉ có thể huấn luyện bộ phân loại Haar Cascade bằng OpenCV 3. May mắn thay, bạn có thể loại bỏ nó sau khi huấn luyện và quay lại OpenCV 4 sau khi lưu mô hình vào tệp XML. Đây là những gì bạn sẽ làm trong bài viết này.

Bạn không thể để OpenCV 3 và OpenCV 4 cùng tồn tại trong Python. Do đó, bạn nên tạo một môi trường riêng biệt để huấn luyện. Trong Python, bạn có thể sử dụng mô-đun venv để tạo một môi trường ảo, đơn giản là tạo một tập hợp các mô-đun đã cài đặt riêng biệt. Các lựa chọn thay thế khác là sử dụng Anaconda hoặc Pyenv, là những kiến ​​trúc khác nhau nhưng cùng chung một triết lý. Trong số tất cả các môi trường trên, bạn nên thấy môi trường Anaconda là dễ nhất cho nhiệm vụ này.


# Thiết lập môi trường

Sẽ dễ hơn nếu bạn sử dụng Anaconda, bạn có thể sử dụng lệnh sau để tạo và sử dụng môi trường mới và đặt tên là "cvtrain":

```bat
conda create -n cvtrain python 'opencv>=3,<4'
conda activate cvtrain
```

Bạn biết mình đã sẵn sàng nếu thấy lệnh `opencv_traincascade` khả dụng:

```bat
$ opencv_traincascade
Usage: opencv_traincascade
  -data <cascade_dir_name>
  -vec <vec_file_name>
  -bg <background_file_name>
  [-numPos <number_of_positive_samples = 2000>]
  [-numNeg <number_of_negative_samples = 1000>]
  [-numStages <number_of_stages = 20>]
  [-precalcValBufSize <precalculated_vals_buffer_size_in_Mb = 1024>]
  [-precalcIdxBufSize <precalculated_idxs_buffer_size_in_Mb = 1024>]
  [-baseFormatSave]
  [-numThreads <max_number_of_threads = 16>]
  [-acceptanceRatioBreakValue <value> = -1>]
--cascadeParams--
  [-stageType <BOOST(default)>]
  [-featureType <{HAAR(default), LBP, HOG}>]
  [-w <sampleWidth = 24>]
  [-h <sampleHeight = 24>]
--boostParams--
  [-bt <{DAB, RAB, LB, GAB(default)}>]
  [-minHitRate <min_hit_rate> = 0.995>]
  [-maxFalseAlarmRate <max_false_alarm_rate = 0.5>]
  [-weightTrimRate <weight_trim_rate = 0.95>]
  [-maxDepth <max_depth_of_weak_tree = 1>]
  [-maxWeakCount <max_weak_tree_count = 100>]
--haarFeatureParams--
  [-mode <BASIC(default) | CORE | ALL
--lbpFeatureParams--
--HOGFeatureParams--
```

Nếu bạn đang sử dụng pyenv hoặc venv, bạn cần thực hiện thêm các bước. Trước tiên, hãy tạo một môi trường và cài đặt OpenCV (bạn sẽ thấy tên gói khác với tên hệ sinh thái Anaconda):

```bat
# create an environment and install opencv 3
pyenv virtualenv 3.11 cvtrain
pyenv activate cvtrain
pip install 'opencv-python>=3,<4'
```

Điều này cho phép bạn chạy các chương trình Python bằng OpenCV nhưng không có công cụ dòng lệnh để đào tạo. Để có được các công cụ này, bạn cần biên dịch chúng từ mã nguồn bằng cách làm theo các bước sau:

1. Tải xuống mã nguồn OpenCV và chuyển sang nhánh 3.4

```bat
# download OpenCV source code and switch to 3.4 branch
git clone https://github.com/opencv/opencv
cd opencv
git checkout 3.4
cd ..
```

2. Tạo thư mục build riêng biệt với thư mục kho lưu trữ:

```bat
mkdir build
cd build
```

3. Chuẩn bị thư mục build bằng công cụ cmake và tham khảo kho lưu trữ OpenCV:

```bat
cmake ../opencv
```

4. Chạy make để biên dịch (có thể bạn cần cài đặt thư viện dành cho nhà phát triển trong hệ thống trước)

```bat
make
ls bin
```

5. Các công cụ bạn cần sẽ nằm trong thư mục bin/, như được hiển thị trong lệnh cuối cùng ở trên.

Các công cụ dòng lệnh cần thiết là `opencv_traincascade` và `opencv_createsamples`. Phần còn lại của bài viết này giả định rằng bạn đã có sẵn các công cụ này.


# Tổng quan về huấn luyện bộ phân loại Cascade

Bạn sẽ huấn luyện một bộ phân loại Cascade bằng các công cụ OpenCV. Bộ phân loại này là một mô hình tập hợp sử dụng AdaBoost. Đơn giản, nhiều mô hình nhỏ hơn được tạo ra, trong đó mỗi mô hình đều yếu về phân loại. Kết hợp lại, nó trở thành một bộ phân loại mạnh với độ chính xác và độ thu hồi tốt.

Mỗi bộ phân loại yếu là một bộ phân loại nhị phân. Để huấn luyện chúng, bạn cần một số mẫu dương và mẫu âm. Mẫu âm rất dễ: Bạn cung cấp một số ảnh ngẫu nhiên cho OpenCV và để OpenCV chọn một vùng hình chữ nhật (tốt hơn nếu không có đối tượng mục tiêu nào trong các ảnh này). Tuy nhiên, các mẫu dương được cung cấp dưới dạng ảnh và hộp giới hạn mà đối tượng nằm hoàn hảo trong hộp.

Sau khi cung cấp các tập dữ liệu này, OpenCV sẽ trích xuất các đặc trưng Haar từ cả hai và sử dụng chúng để huấn luyện nhiều bộ phân loại. Các đặc trưng Haar được tạo ra từ việc phân vùng các mẫu dương hoặc âm thành các vùng hình chữ nhật. Cách phân vùng được thực hiện có liên quan đến một số yếu tố ngẫu nhiên. Do đó, OpenCV cần thời gian để tìm ra cách tốt nhất để trích xuất các đặc trưng Haar cho tác vụ phân loại này.

Trong OpenCV, bạn chỉ cần cung cấp dữ liệu huấn luyện dưới dạng tệp hình ảnh ở định dạng mà OpenCV có thể đọc được (chẳng hạn như JPEG hoặc PNG). Đối với các mẫu âm tính, tất cả những gì nó cần là một tệp văn bản thuần túy chứa tên tệp của chúng. Đối với các mẫu dương tính, cần có một "tệp thông tin", là một tệp văn bản thuần túy chứa thông tin chi tiết về tên tệp, số lượng đối tượng trong ảnh và các khung giới hạn tương ứng.

Các mẫu dữ liệu dương tính để huấn luyện phải ở định dạng nhị phân. OpenCV cung cấp công cụ opencv_createsamples để tạo định dạng nhị phân từ "tệp thông tin". Sau đó, các mẫu dương tính này, cùng với các mẫu âm tính, được cung cấp cho một công cụ khác là opencv_traincascade để chạy huấn luyện và tạo ra đầu ra mô hình ở định dạng tệp XML. Đây là tệp XML bạn có thể tải vào bộ phân loại Haar theo tầng của OpenCV.

# Chuẩn bị dữ liệu đào tạo

# Đào tạo phân loại Haar Cascade

# Đọc thêm

Phần này cung cấp thêm tài liệu về chủ đề này nếu bạn muốn tìm hiểu sâu hơn.

## Sách

[Mastering OpenCV 4 with Python](https://www.amazon.com/Mastering-OpenCV-Python-practical-processing/dp/1789344913), 2019.

## Trang web

- OpenCV [tutorial on cascade classifier training](https://docs.opencv.org/4.x/dc/d88/tutorial_traincascade.html)
- [FAQ: OpenCV Haartraining](https://www.computer-vision-software.com/blog/2009/11/faq-opencv-haartraining/)
- [Tutorial: OpenCV Haartraining](https://web.archive.org/web/20220804065334/http://note.sonots.com/SciSoftware/haartraining.html)


# Tóm tắt

Trong bài viết này, bạn đã học cách huấn luyện bộ phát hiện đối tượng Haar cascade trong OpenCV. Cụ thể, bạn đã học:

- Cách chuẩn bị dữ liệu cho huấn luyện Haar cascade
- Cách chạy quy trình huấn luyện trên dòng lệnh
- Cách sử dụng OpenCV 3.x để huấn luyện bộ phát hiện và sử dụng mô hình đã huấn luyện trong OpenCV 4.x


-----
Tham khảo:
- [Training a Haar Cascade Object Detector in OpenCV](https://machinelearningmastery.com/training-a-haar-cascade-object-detector-in-opencv/)
- []()
