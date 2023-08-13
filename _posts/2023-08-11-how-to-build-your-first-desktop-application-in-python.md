---
layout: post
title: Xây dựng Ứng dụng máy tính để bàn bằng Python
subtitle: How to build your first Desktop Application in Python
image: "img/technology.png"
author: "Ampofo Amoh"
tags:
- Python
- PyQt
- PyQt6
---

![Xây dựng Ứng dụng máy tính để bàn bằng Python](https://boxxv.github.io/img/2023/1__ZDAL3RJZSKSz8qb8sLBIw.webp "How to build your first Desktop Application in Python")

Tìm kiếm toàn bộ internet để sử dụng ngôn ngữ lập trình Python và họ liệt kê chúng với Ứng dụng dành cho máy tính để bàn được đánh dấu là không phù hợp lắm với python. Nhưng nhiều năm trước, vào năm 2016 khi tôi đang hy vọng chuyển từ phát triển web sang phát triển phần mềm, Google.com đã nói với tôi rằng tôi nên chọn python vì nó được sử dụng để xây dựng một số ứng dụng khoa học hiện đại và tiên tiến, sau đó họ đề cập đến blender3d. Tôi biết blender3d, nó là một phần mềm tạo 3d tuyệt vời.

Nhưng đó không phải là lỗi của họ, những thứ xấu xí mà mọi người đang sử dụng để trưng bày cho các GUI của python thật đáng ghét, những cửa sổ trông quá cũ và quá hạn sử dụng, không một bạn trẻ nào thích điều đó. Tôi hy vọng sẽ thay đổi quan niệm đó với hướng dẫn ứng dụng máy tính để bàn đơn giản này. Bắt đầu nào.

Chúng tôi sẽ sử dụng PyQt (sớm nói thêm về điều đó) thay vì Tkinter gần như đã bị xóa khỏi danh sách các thư viện tiêu chuẩn python vì đã lỗi thời.

PyQt là gì (phát âm: pie-cute). Nó là một trong hai cổng của một framework, Qt (phát âm là: dễ thương) từ C++, . Khung đó được gọi là khung cần thiết cho các nhà phát triển C++. Đó là khuôn khổ đằng sau máy xay sinh tố3d, Tableau, Telegram, Anaconda Navigator, IPython, Jupyter Notebook, VirtualBox, VLC, v.v. Chúng tôi sẽ sử dụng nó thay vì Tkinter đáng xấu hổ.

Hai cổng của Qt là PySide và PyQt. Cả 2 giống nhau đến 99%. PyQt là cách dễ nhất trong hai cách cài đặt.

-----

## Điều kiện cần
1. Bạn nên biết một số điều cơ bản về python
3. Bạn nên biết cách cài đặt các gói hoặc thư viện với pip
3. Tất nhiên, bạn nên cài đặt python.


-----

## Cài đặt
Điều duy nhất chúng ta cần cài đặt là PyQt. Vì vậy, hãy mở thiết bị đầu cuối của bạn, trên cửa sổ, đó sẽ là Dấu nhắc lệnh hoặc Powershell.

Nhập lệnh dưới đây vào terminal của bạn

```bat
pip install PyQt6
```

PyQt6 vì chúng tôi đang tải xuống phiên bản 6 của PyQt. Đợi quá trình cài đặt hoàn tất, sẽ chỉ mất khoảng một hoặc hai phút.

-----

## Tệp và thư mục dự án
Bây giờ chúng ta đã hoàn tất việc cài đặt. Chúng ta nên bắt đầu với dự án của mình. Tạo một thư mục dự án cho ứng dụng, chúng ta sẽ gọi nó là: helloApp. Tạo nó ở bất cứ đâu bạn muốn trên máy tính của mình, nhưng thật tốt khi được tổ chức.

-----

## Lets do a “Hello World”
Mở main.py, tốt nhất là trong vscode và nhập mã sau

`main.py`

```python
import sys
import os
from PyQt6.QtGui import QGuiApplication
from PyQt6.QtQml import QQmlApplicationEngine
from PyQt6.QtQuick import QQuickWindow

QQuickWindow.setSceneGraphBackend('software')
app = QGuiApplication(sys.argv)
engine = QQmlApplicationEngine()
engine.quit.connect(app.quit)
engine.load('./UI/main.qml')
sys.exit(app.exec())
```

Trong đoạn mã trên; chúng tôi nhập các mô-đun sys, os, QGuiApplication và QQmlApplication.

`QQuickWindow.setSceneGraphBackend('software')` nên được đưa vào mã của bạn dưới dạng tùy chọn dự phòng để sử dụng với thông số kỹ thuật phần cứng cũ, ngoài việc chúng sẽ thấy thông tin lỗi như bên dưới:

```python
>>> Failed to create vertex shader: Error 0x80070057: The parameter is incorrect.
>>> Failed to build graphics pipeline state
```

Ngoài ra, mã gọi QGuiApplication và QQmlApplicationEngine sẽ sử dụng Qml thay vì QtWidgets làm lớp giao diện người dùng cho Ứng dụng Qt. Sau đó, nó kết nối chức năng thoát lớp giao diện người dùng với chức năng thoát chính của ứng dụng. Vì vậy, cả hai có thể đóng khi người dùng đã đóng giao diện người dùng. Tiếp theo, nó tải tệp qml dưới dạng mã qml cho giao diện người dùng Qml. App.exec() là thứ chạy Ứng dụng, nó nằm trong sys.exit vì nó trả về mã thoát của Ứng dụng được chuyển vào sys.exit thoát khỏi hệ thống python.

Thêm mã này vào `main.qml`

```python
import QtQuick
import QtQuick.Controls.Basic
ApplicationWindow {
    visible: true
    width: 600
    height: 500
    title: "HelloApp"
    Text {
        anchors.centerIn: parent
        text: "Hello World"
        font.pixelSize: 24
    }
}
```

Đoạn mã trên tạo một Cửa sổ, đoạn mã hiển thị là rất quan trọng, nếu không có nó thì UI sẽ chạy nhưng sẽ ẩn đi, với chiều rộng và chiều cao như đã chỉ định, với tiêu đề là “HelloApp”. Và một Văn bản được căn giữa ở phần gốc (tình cờ là cửa sổ), văn bản được hiển thị là “Xin chào Thế giới”, kích thước pixel là 24px.

Trong Qt5 trước đó, các mã nhập ở trên sẽ bao gồm các số phiên bản như

```python
import QtQuick 2.15
import QtQuick.Controls 2.15
```

Ngoài ra, trong Qt6, chúng tôi khai báo rõ ràng một kiểu cho Điều khiển là

```python
import QtQuick.Controls.Basic
```

thêm về các kiểu Điều khiển sau

Nếu bạn có ở trên, bạn có thể chạy nó và xem kết quả của mình.

Điều hướng vào thư mục helloApp của bạn

```bat
cd helloApp
```

Bây giờ hãy chạy nó bằng cách thực hiện:

```bat
python main.py
```

Nếu mã của bạn chạy, bạn sẽ thấy:

![Xây dựng Ứng dụng máy tính để bàn bằng Python](https://boxxv.github.io/img/2023/1_MItXIJYQ8yHq3JtNTroXfA.webp "How to build your first Desktop Application in Python")


## Cập nhật giao diện người dùng
Bây giờ, hãy cập nhật giao diện người dùng một chút, hãy thêm hình ảnh làm nền và văn bản sẽ có thời gian

```python
import QtQuick
import QtQuick.Controls.Basic
ApplicationWindow {
    visible: true
    width: 400
    height: 600
    title: "HelloApp"
    Rectangle {
        anchors.fill: parent
        Image {
            sourceSize.width: parent.width
            sourceSize.height: parent.height
            source: "./images/playas.jpg"
            fillMode: Image.PreserveAspectCrop
        }
        Rectangle {
            anchors.fill: parent
            color: "transparent"
            Text {
                text: "16:38:33"
                font.pixelSize: 24
                color: "white"
            }
        }
    }
}
```

Ở trên có một loại ApplicationWindow, một loại Hình chữ nhật bên trong nó, thực sự lấp đầy tất cả không gian của cửa sổ. Có một Hình ảnh bên trong nó và một Hình chữ nhật khác trông giống như hình bên cạnh, nhưng do không tồn tại loại Bố cục nên nó thực sự nằm trên loại Hình ảnh. Hình chữ nhật có màu trong suốt vì theo mặc định, Hình chữ nhật có màu trắng, có một Văn bản bên trong hình chữ nhật có nội dung 16:38:33, để mô phỏng thời gian.

Nếu bạn chạy ứng dụng, văn bản sẽ xuất hiện ở góc trên cùng bên trái của Cửa sổ. Chúng tôi không thích điều đó, và vì vậy chúng tôi sẽ làm cho nó xuất hiện ở góc dưới cùng bên trái với một số lề thay thế.

Trong mã qml của bạn, hãy cập nhật loại Văn bản để bao gồm các ký tự neo như hình bên dưới:

```python
            ...
            Text {
                anchors {
                    bottom: parent.bottom
                    bottomMargin: 12
                    left: parent.left
                    leftMargin: 12
                }
                text: "16:38:33"
                font.pixelSize: 24
                ...
            }
            ...
```

Bây giờ hãy chạy nó bằng cách thực hiện

```bat
python main.py
```

Bạn sẽ thấy một cái gì đó tương tự như thế này.

![Xây dựng Ứng dụng máy tính để bàn bằng Python](https://boxxv.github.io/img/2023/1_F59PHhThOIYJvcXJDjhXjQ.webp "How to build your first Desktop Application in Python")

Bây giờ tôi muốn thời gian để cập nhật

-----

## Sử dụng thời gian thực
Hãy sử dụng một thời gian thực. Python cung cấp cho chúng ta các hàm gốc cung cấp cho chúng ta tất cả các loại hàm liên quan đến thời gian và ngày tháng. Chúng tôi muốn một chuỗi với thời gian hiện tại. gmtime cung cấp cho bạn cấu trúc thời gian toàn cầu với tất cả các loại thông tin và strftime xây dựng các phần thời gian nhất định dưới dạng một chuỗi bằng cách sử dụng hàm gmtime

nhập hàm strftime và gmtime

```python
import sys
import os
from time import strftime, gmtime
from PyQt6.QtGui import QGuiApplication
...
```

Sau đó, xây dựng chuỗi thời gian của bạn bên dưới các lần nhập, ở bất kỳ đâu trong tệp

```python
curr_time = strftime("%H:%M:%S", gmtime())
```

_%H, %M, %S_, cho biết **strftime** mà chúng ta muốn xem Giờ (loại 24 giờ), phút và giây. (Đọc thêm về mã định dạng cho strftime tại [đây](https://docs.python.org/3/library/datetime.html?highlight=strftime#strftime-and-strptime-format-codes)). Biến này sẽ được chuyển đến lớp qml.

Hãy tạo một thuộc tính trong qml mà chúng ta có thể sử dụng để nhận chuỗi thời gian. Biến này giúp thay đổi thời gian dễ dàng hơn. Hãy gọi thuộc tính này là currTime


`main.qml`
```python
...
ApplicationWindow {
    ...
    title: "HelloApp"
    property string currTime: "00:00:00"
    ...
```

Sử dụng thuộc tính này trong qml, vì vậy khi giá trị này thay đổi, tất cả những nơi khác mà nó đã được sử dụng cũng sẽ thay đổi.

```python
...
Text {
    ...
    text: currTime  // used to be; text: "16:38:33"
    font.pixelSize: 48
    color: "white"
}
...
```

Bây giờ hãy gửi biến curr_time mà chúng ta đã tạo trong python tới qml bằng cách đặt nó vào thuộc tính qml currTime.

```python
...
engine.load('./UI/main.qml')
engine.rootObjects()[0].setProperty('currTime', curr_time)
...
```

Đoạn mã trên sẽ đặt thuộc tính qml currTime thành giá trị của thuộc tính python curr_time. Đây là một cách chúng tôi chuyển thông tin từ python sang lớp giao diện người dùng.

Chạy ứng dụng và bạn sẽ không thấy lỗi nào và cũng sẽ có thời gian hiện tại. Hoan hô!!! Tiến lên!!!

-----

Updating...


[https://github.com/mikiereed/helloApp_python_desktop](https://github.com/mikiereed/helloApp_python_desktop)  
[https://github.com/DmPanf/SSD_FaceNet_PyQt5](https://github.com/DmPanf/SSD_FaceNet_PyQt5)  
[https://github.com/Rafael2026/python](https://github.com/Rafael2026/python)  
[https://github.com/codewithlennylen/Data-Engineering-Bootcamp](https://github.com/codewithlennylen/Data-Engineering-Bootcamp)  
[https://github.com/CodeForAsheville/pdf-case-compare](https://github.com/CodeForAsheville/pdf-case-compare)

-----
Tham khảo:
- [How to build your first Desktop Application in Python](https://medium.com/analytics-vidhya/how-to-build-your-first-desktop-application-in-python-7568c7d74311)
- [Tạo Ứng Dụng Desktop Đơn Giản Với Python](https://codelearn.io/sharing/tao-ung-dung-desktop-voi-python)
- [Xây dựng công cụ tự động cắt ảnh chỉ chứa khuôn mặt sử dụng MTCNN và PyQt5](https://viblo.asia/p/xay-dung-cong-cu-tu-dong-cat-anh-chi-chua-khuon-mat-su-dung-mtcnn-va-pyqt5-ORNZqpd8K0n)