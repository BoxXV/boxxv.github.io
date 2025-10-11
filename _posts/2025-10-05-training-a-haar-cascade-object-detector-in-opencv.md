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

Hãy cùng xem xét việc tạo một bộ phát hiện khuôn mặt mèo. Để huấn luyện một bộ phát hiện như vậy, trước tiên bạn cần có tập dữ liệu. Một lựa chọn khả thi là Bộ dữ liệu Thú cưng Oxford-IIIT, tại địa chỉ này:

https://www.robots.ox.ac.uk/~vgg/data/pets/

Đây là một tập dữ liệu 800MB, khá nhỏ so với tiêu chuẩn của các tập dữ liệu thị giác máy tính. Các hình ảnh được chú thích theo định dạng Pascal VOC. Tóm lại, mỗi hình ảnh có một tệp XML tương ứng trông như sau:

```xml
<?xml version="1.0"?>
<annotation>
  <folder>OXIIIT</folder>
  <filename>Abyssinian_100.jpg</filename>
  <source>
    <database>OXFORD-IIIT Pet Dataset</database>
    <annotation>OXIIIT</annotation>
    <image>flickr</image>
  </source>
  <size>
    <width>394</width>
    <height>500</height>
    <depth>3</depth>
  </size>
  <segmented>0</segmented>
  <object>
    <name>cat</name>
    <pose>Frontal</pose>
    <truncated>0</truncated>
    <occluded>0</occluded>
    <bndbox>
      <xmin>151</xmin>
      <ymin>71</ymin>
      <xmax>335</xmax>
      <ymax>267</ymax>
    </bndbox>
    <difficult>0</difficult>
  </object>
</annotation>
```

Tệp XML cho bạn biết tệp hình ảnh nào đang được đề cập đến (Abyssinian_100.jpg trong ví dụ trên) và đối tượng nào được chứa trong đó, với khung giới hạn nằm giữa các thẻ <bndbox></bndbox>.

Để trích xuất các khung giới hạn từ tệp XML, bạn có thể sử dụng hàm sau:

```python
import xml.etree.ElementTree as ET

def read_voc_xml(xmlfile: str) -> dict:
    root = ET.parse(xmlfile).getroot()
    boxes = {"filename": root.find("filename").text,
             "objects": []}
    for box in root.iter('object'):
        bb = box.find('bndbox')
        obj = {
            "name": box.find('name').text,
            "xmin": int(bb.find("xmin").text),
            "ymin": int(bb.find("ymin").text),
            "xmax": int(bb.find("xmax").text),
            "ymax": int(bb.find("ymax").text),
        }
        boxes["objects"].append(obj)

    return boxes
```

Ví dụ về từ điển được trả về bởi hàm trên như sau:

```json
{'filename': 'yorkshire_terrier_160.jpg',
'objects': [{'name': 'dog', 'xmax': 290, 'xmin': 97, 'ymax': 245, 'ymin': 18}]}
```

Với những điều này, việc tạo tập dữ liệu để huấn luyện rất dễ dàng: Trong tập dữ liệu thú cưng Oxford-IIT, ảnh là mèo hoặc chó. Bạn có thể để tất cả ảnh chó làm mẫu âm tính. Sau đó, tất cả ảnh mèo sẽ là mẫu dương tính với bộ hộp giới hạn phù hợp.

“Tệp thông tin” mà OpenCV mong đợi cho các mẫu dương tính là một tệp văn bản thuần túy với mỗi dòng có định dạng sau:

```txt
filename N x0 y0 w0 h0 x1 y1 w1 h1 ...
```

Số theo sau tên tệp là số lượng khung giới hạn trên ảnh đó. Mỗi khung giới hạn là một mẫu dương. Tiếp theo là các khung giới hạn. Mỗi khung được xác định bởi tọa độ điểm ảnh ở góc trên bên trái, chiều rộng và chiều cao của khung. Để có kết quả tốt nhất của bộ phân loại Haar Cascade, khung giới hạn nên có cùng tỷ lệ khung hình như mô hình mong đợi.

Giả sử tập dữ liệu Pet bạn đã tải xuống nằm trong thư mục dataset/, bạn sẽ thấy các tệp được sắp xếp như sau:

```
dataset
|-- annotations
|   |-- README
|   |-- list.txt
|   |-- test.txt
|   |-- trainval.txt
|   |-- trimaps
|   |   |-- Abyssinian_1.png
|   |   |-- Abyssinian_10.png
|   |   ...
|   |   |-- yorkshire_terrier_98.png
|   |   `-- yorkshire_terrier_99.png
|   `-- xmls
|       |-- Abyssinian_1.xml
|       |-- Abyssinian_10.xml
|       ...
|       |-- yorkshire_terrier_189.xml
|       `-- yorkshire_terrier_190.xml
`-- images
    |-- Abyssinian_1.jpg
    |-- Abyssinian_10.jpg
    ...
    |-- yorkshire_terrier_98.jpg
    `-- yorkshire_terrier_99.jpg
```

Với điều này, bạn có thể dễ dàng tạo “tệp thông tin” cho các mẫu dương tính và danh sách các tệp mẫu âm tính bằng cách sử dụng chương trình sau:

```python
import pathlib
import xml.etree.ElementTree as ET

import numpy as np

def read_voc_xml(xmlfile: str) -> dict:
    """read the Pascal VOC XML and return (filename, object name, bounding box)
    where bounding box is a vector of (xmin, ymin, xmax, ymax). The pixel
    coordinates are 1-based.
    """
    root = ET.parse(xmlfile).getroot()
    boxes = {"filename": root.find("filename").text,
             "objects": []
            }
    for box in root.iter('object'):
        bb = box.find('bndbox')
        obj = {
            "name": box.find('name').text,
            "xmin": int(bb.find("xmin").text),
            "ymin": int(bb.find("ymin").text),
            "xmax": int(bb.find("xmax").text),
            "ymax": int(bb.find("ymax").text),
        }
        boxes["objects"].append(obj)

    return boxes

# Read Pascal VOC and write data
base_path = pathlib.Path("dataset")
img_src = base_path / "images"
ann_src = base_path / "annotations" / "xmls"

negative = []
positive = []
for xmlfile in ann_src.glob("*.xml"):
    # load xml
    ann = read_voc_xml(str(xmlfile))
    if ann['objects'][0]['name'] == 'dog':
        # negative sample (dog)
        negative.append(str(img_src / ann['filename']))
    else:
        # positive sample (cats)
        bbox = []
        for obj in ann['objects']:
            x = obj['xmin']
            y = obj['ymin']
            w = obj['xmax'] - obj['xmin']
            h = obj['ymax'] - obj['ymin']
            bbox.append(f"{x} {y} {w} {h}")
        line = f"{str(img_src/ann['filename'])} {len(bbox)} {' '.join(bbox)}"
        positive.append(line)

# write the output to `negative.dat` and `postiive.dat`
with open("negative.dat", "w") as fp:
    fp.write("\n".join(negative))

with open("positive.dat", "w") as fp:
    fp.write("\n".join(positive))
```

Chương trình này quét tất cả các tệp XML từ tập dữ liệu, sau đó trích xuất các hộp giới hạn từ mỗi tệp nếu đó là ảnh mèo. Danh sách negative sẽ chứa các đường dẫn đến ảnh chó. Danh sách positive sẽ chứa các đường dẫn đến ảnh mèo cũng như các hộp giới hạn theo định dạng được mô tả ở trên, mỗi dòng là một chuỗi. Sau vòng lặp, hai danh sách này được ghi vào đĩa dưới dạng các tệp negative.dat và positive.dat.

Nội dung của negative.dat rất đơn giản. Nội dung của postiive.dat như sau:

```dat
dataset/images/Siamese_102.jpg 1 154 92 194 176
dataset/images/Bengal_152.jpg 1 84 8 187 201
dataset/images/Abyssinian_195.jpg 1 8 6 109 115
dataset/images/Russian_Blue_135.jpg 1 228 90 103 117
dataset/images/Persian_122.jpg 1 60 16 230 228
```

Bước trước khi chạy chương trình huấn luyện là chuyển đổi positive.dat sang định dạng nhị phân. Việc này được thực hiện bằng dòng lệnh sau:

```
opencv_createsamples -info positive.dat -vec positive.vec -w 30 -h 30
```

Lệnh này nên được chạy trong cùng thư mục với positive.dat để có thể tìm thấy ảnh tập dữ liệu. Đầu ra của lệnh này sẽ là positive.vec. Nó còn được gọi là "tệp vec". Khi thực hiện, bạn cần chỉ định chiều rộng và chiều cao của cửa sổ bằng các tham số -w và -h. Điều này sẽ thay đổi kích thước ảnh được cắt bởi hộp giới hạn thành kích thước pixel này trước khi ghi vào tệp vec. Kích thước này cũng phải khớp với kích thước cửa sổ được chỉ định khi bạn chạy huấn luyện.


# Đào tạo phân loại Haar Cascade

Việc huấn luyện một bộ phân loại cần thời gian. Quá trình này được thực hiện qua nhiều giai đoạn. Các tệp trung gian sẽ được viết ở mỗi giai đoạn, và sau khi tất cả các giai đoạn hoàn tất, bạn sẽ có mô hình đã được huấn luyện được lưu trong một tệp XML. OpenCV mong muốn tất cả các tệp được tạo ra này được lưu trữ trong một thư mục.

Việc chạy quá trình huấn luyện thực sự rất đơn giản. Hãy xem xét việc tạo một thư mục mới cat_detect để lưu trữ các tệp đã tạo. Sau khi thư mục được tạo, bạn có thể chạy huấn luyện bằng công cụ dòng lệnh opencv_traincascade:

```bat
# need to create the data dir first
mkdir cat_detect
# then run the training
opencv_traincascade -data cat_detect -vec positive.vec -bg negative.dat -numPos 900 -numNeg 2000 -numStages 10 -w 30 -h 30
```

Lưu ý việc sử dụng positive.vec làm mẫu dương và negative.dat làm mẫu âm. Cũng lưu ý rằng, các tham số -w và -h giống với những gì bạn đã sử dụng trước đó trong lệnh opencv_createsamples. Các đối số dòng lệnh khác được giải thích như sau:

- -data <tên thư mục>: Nơi lưu trữ bộ phân loại đã được huấn luyện. Thư mục này phải tồn tại.
- -vec <tên tệp>: Tệp vec chứa các mẫu dương.
- -bg <tên tệp>: Danh sách các mẫu âm, còn được gọi là ảnh "nền"
- -numPos <N>: số lượng mẫu dương được sử dụng trong quá trình huấn luyện cho mỗi giai đoạn.
- -numNeg <N>: số lượng mẫu âm được sử dụng trong quá trình huấn luyện cho mỗi giai đoạn.
- -numStages <N>: số lượng giai đoạn xếp tầng cần được huấn luyện.
- -w <chiều rộng> và -h <chiều cao>: Kích thước pixel của một đối tượng. Kích thước này phải giống với kích thước pixel được sử dụng trong quá trình tạo mẫu huấn luyện bằng công cụ opencv_createsamples.
- -minHitRate <tỷ lệ>: Tỷ lệ dương thực mong muốn tối thiểu cho mỗi giai đoạn. Quá trình huấn luyện sẽ không kết thúc cho đến khi đạt được điều kiện này.
- -maxFalseAlarmRate <rate>: Tỷ lệ dương tính giả mong muốn tối đa cho mỗi giai đoạn. Quá trình huấn luyện sẽ không kết thúc cho đến khi đạt được điều kiện này.
- -maxDepth <N>: Độ sâu tối đa của một cây yếu
- -maxWeakCount <N>: Số lượng cây yếu tối đa cho mỗi giai đoạn

Không phải tất cả các đối số này đều bắt buộc. Tuy nhiên, bạn nên thử các kết hợp khác nhau để xem liệu bạn có thể huấn luyện một bộ phát hiện tốt hơn hay không.

Trong quá trình huấn luyện, bạn sẽ thấy màn hình sau:

```bat
$ opencv_traincascade -data cat_detect -vec positive.vec -bg negative.dat -numPos 900 -numNeg 2000 -numStages 10 -w 30 -h 30
PARAMETERS:
cascadeDirName: cat_detect
vecFileName: positive.vec
bgFileName: negative.dat
numPos: 900
numNeg: 2000
numStages: 10
precalcValBufSize[Mb] : 1024
precalcIdxBufSize[Mb] : 1024
acceptanceRatioBreakValue : -1
stageType: BOOST
featureType: HAAR
sampleWidth: 30
sampleHeight: 30
boostType: GAB
minHitRate: 0.995
maxFalseAlarmRate: 0.5
weightTrimRate: 0.95
maxDepth: 1
maxWeakCount: 100
mode: BASIC
Number of unique features given windowSize [30,30] : 394725

===== TRAINING 0-stage =====
<BEGIN
POS count : consumed   900 : 900
NEG count : acceptanceRatio    2000 : 1
Precalculation time: 3
+----+---------+---------+
|  N |    HR   |    FA   |
+----+---------+---------+
|   1|        1|        1|
+----+---------+---------+
|   2|        1|        1|
+----+---------+---------+
|   3|        1|        1|
+----+---------+---------+
|   4|        1|   0.8925|
+----+---------+---------+
|   5| 0.998889|   0.7785|
...
|  19| 0.995556|    0.503|
+----+---------+---------+
|  20| 0.995556|    0.492|
+----+---------+---------+
END>
...
Training until now has taken 0 days 2 hours 55 minutes 44 seconds.

===== TRAINING 9-stage =====
<BEGIN
POS count : consumed   900 : 948
NEG count : acceptanceRatio    2000 : 0.00723552
Precalculation time: 4
+----+---------+---------+
|  N |    HR   |    FA   |
+----+---------+---------+
|   1|        1|        1|
+----+---------+---------+
|   2|        1|        1|
+----+---------+---------+
|   3|        1|        1|
+----+---------+---------+
|   4|        1|        1|
+----+---------+---------+
|   5| 0.997778|   0.9895|
...
|  50| 0.995556|   0.5795|
+----+---------+---------+
|  51| 0.995556|   0.4895|
+----+---------+---------+
END>
Training until now has taken 0 days 3 hours 25 minutes 12 seconds.
```

ạn nên lưu ý rằng quá trình huấn luyện cho các giai đoạn 𝑁 được đánh số từ 0 đến 𝑁 − 1. Một số giai đoạn có thể mất nhiều thời gian hơn để huấn luyện. Ban đầu, các tham số huấn luyện được hiển thị để làm rõ chức năng của nó. Sau đó, ở mỗi giai đoạn, một bảng sẽ được in ra, mỗi hàng một bảng. Bảng hiển thị ba cột: Số đặc trưng N, tỷ lệ trúng HR (tỷ lệ dương tính thật) và tỷ lệ cảnh báo sai FA (tỷ lệ dương tính giả).

Trước giai đoạn 0, bạn sẽ thấy minHitRate là 0,995 và maxFalseAlarmRate là 0,5. Do đó, mỗi giai đoạn sẽ tìm thấy nhiều đặc trưng Haar cho đến khi bộ phân loại có thể giữ tỷ lệ trúng trên 0,995 trong khi tỷ lệ cảnh báo sai dưới 0,5. Lý tưởng nhất là bạn muốn tỷ lệ trúng là 1 và tỷ lệ cảnh báo sai là 0. Vì Haar cascade là một tập hợp, bạn sẽ nhận được dự đoán chính xác nếu bạn đúng trong đa số. Xấp xỉ, bạn có thể xem xét bộ phân loại 𝑛 các giai đoạn với tỷ lệ trúng 𝑝 và tỷ lệ báo động giả 𝑞 để có tỷ lệ trúng tổng thể 𝑝𝑛
và tỷ lệ báo động giả tổng thể 𝑞<sup>𝑛</sup>. Trong thiết lập trên, 𝑛 = 10, 𝑝 > 0,995, 𝑞 < 0,5. Do đó, tỷ lệ báo động giả tổng thể sẽ dưới 0,1% và tỷ lệ trúng tổng thể trên 95%.

Lệnh huấn luyện này mất hơn 3 giờ để hoàn thành trên một máy tính hiện đại. Đầu ra sẽ được đặt tên là cascade.xml trong thư mục đầu ra. Bạn có thể kiểm tra kết quả bằng mã mẫu như sau:

```python
import cv2

image = 'dataset/images/Abyssinian_88.jpg'
model = 'cat_detect/cascade.xml'

classifier = cv2.CascadeClassifier(model)
img = cv2.imread(image)

# Convert the image to grayscale
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Perform object detection
objects = classifier.detectMultiScale(gray,
                                      scaleFactor=1.1, minNeighbors=5,
                                      minSize=(30, 30))

# Draw rectangles around detected objects
for (x, y, w, h) in objects:
    cv2.rectangle(img, (x, y), (x+w, y+h), (255, 0, 0), 2)

# Display the result
cv2.imshow('Object Detection', img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

Kết quả sẽ phụ thuộc vào mức độ huấn luyện mô hình của bạn, và cũng phụ thuộc vào các đối số bạn đã truyền vào detectMultiScale(). Xem bài viết trước để biết cách thiết lập các đối số này.

Đoạn mã trên chạy bộ dò tìm trên một hình ảnh từ tập dữ liệu. Bạn có thể thấy kết quả như sau:

![cat detection](https://boxxv.github.io/img/2025/cascade_cat.jpg "cat detection")

Bạn thấy một số kết quả dương tính giả, nhưng khuôn mặt của con mèo đã được phát hiện. Có nhiều cách để cải thiện chất lượng. Ví dụ, tập dữ liệu huấn luyện bạn đã sử dụng ở trên không sử dụng hộp giới hạn hình vuông, trong khi bạn đã sử dụng hình vuông để huấn luyện và phát hiện. Việc điều chỉnh tập dữ liệu có thể cải thiện chất lượng. Tương tự, các tham số khác bạn đã sử dụng trên dòng lệnh huấn luyện cũng ảnh hưởng đến kết quả. Tuy nhiên, bạn nên lưu ý rằng bộ phát hiện Haar Cascade rất nhanh, nhưng bạn càng sử dụng nhiều giai đoạn thì tốc độ sẽ càng chậm.

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
- [Official tutorial on training a Cascade Classifier](https://docs.opencv.org/4.12.0/dc/d88/tutorial_traincascade.html)
- [Training a Cascade Classifier - OpenCV Object Detection in Games #8](https://youtu.be/XrCAvs9AePM)
- [OpenCV Object Detection in Games](https://www.youtube.com/playlist?list=PL1m2M8LQlzfKtkKq2lK5xko4X-8EZzFPI)
- [How to install OpenCV on Windows | 2025](https://youtu.be/EqoH3gspQGg)
- [Training your own Cascade/Classifier/Detector — OpenCV](https://dikshit18.medium.com/training-your-own-cascade-classifier-detector-opencv-9ea6055242c2)
- [TRAINCASCADE AND CAR DETECTION USING OPENCV](https://abhishek4273.wordpress.com/2014/03/16/traincascade-and-car-detection-using-opencv/)
- []()