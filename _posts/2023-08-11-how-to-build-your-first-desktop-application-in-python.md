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

PyQt là gì (phát âm: pie-cute). Nó là một trong hai cổng của một framework, Qt (phát âm là: dễ thương) từ C++. Khung đó được gọi là khung cần thiết cho các nhà phát triển C++. Đó là khuôn khổ đằng sau máy xay sinh tố3d, Tableau, Telegram, Anaconda Navigator, IPython, Jupyter Notebook, VirtualBox, VLC, v.v. Chúng tôi sẽ sử dụng nó thay vì Tkinter đáng xấu hổ.

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

## Cập nhật thời gian
Để giữ cho thời gian của chúng tôi được cập nhật. Chúng ta sẽ cần sử dụng chủ đề. Tạo luồng trong python rất dễ dàng và đơn giản, chúng tôi sẽ sử dụng luồng đó thay vì luồng của Qt. Chủ đề sử dụng chức năng hoặc chủ đề gọi một chức năng. Tôi thích chúng tôi sử dụng một kỹ thuật trong Qt được gọi là tín hiệu, đây là một phương pháp chuyên nghiệp và việc nghiên cứu nó sẽ giúp bạn thích hơn và dễ dàng hơn. Hãy đặt mã thời gian hiện tại của chúng ta vào một hàm, sử dụng dấu gạch dưới (_) cho tên tệp. Tôi sẽ giải thích tại sao sau. Nó không phải là một yêu cầu hay bất cứ điều gì, nó chỉ là một thực hành tốt

Để sử dụng các tín hiệu, chúng tôi sẽ phải phân lớp QObject, đơn giản thôi.

Tạo một lớp con của QObject, gọi nó là bất cứ thứ gì bạn thích. Tôi sẽ gọi nó là Backend.

```python
...
from PyQt6.QtQuick import QQuickWindow
from PyQt6.QtCore import QObject, pyqtSignal

class Backend(QObject):
    def __init__(self):
        QObject.__init__(self)
QQuickWindow.setSceneGraphBackend('software')
...
```

Đoạn mã trên nhập QObject và pyqtSignal, trong pyside, đây được gọi là Tín hiệu. Đây là một trong số ít sự khác biệt giữa pyqt và pyside.

Chính thức, chúng ta đã có một chuỗi thuộc tính nhận chuỗi curr_time của chúng ta từ python, bây giờ chúng ta tạo một thuộc tính QtObject để nhận đối tượng Backend từ python. Không có nhiều loại. Qml chuyển đổi các loại cơ sở python thành bool, int, double, string, list, QtObject và var. var có thể xử lý mọi loại trăn, nhưng nó ít được yêu thích nhất.

main.qml
```python
...
property string currTime: "00:00:00"
property QtObject backend
...
```

Đoạn mã trên tạo một chương trình phụ trợ QtObject để giữ đối tượng python back_end của chúng ta. Tên được sử dụng là của tôi, vui lòng thay đổi chúng thành bất kỳ tên nào bạn thích

Trong python vượt qua nó trên

```python
...
engine.load('./UI/main.qml')
back_end = Backend()
engine.rootObjects()[0].setProperty('backend', back_end)
...
```

Trong đoạn mã trên, một đối tượng back_end đã được tạo từ lớp Backend. Sau đó, chúng tôi đặt nó thành thuộc tính qml có tên phụ trợ

Trong Qml, một QtObject có thể nhận nhiều chức năng (được gọi là tín hiệu) từ python thực hiện nhiều việc, nhưng chúng sẽ phải được tổ chức theo QtObject đó.

Tạo loại Kết nối và nhắm mục tiêu nó đến phụ trợ. Bây giờ bên trong loại Kết nối có thể có nhiều chức năng mà chúng tôi muốn nhận cho phần phụ trợ.

main.qml
```python
...
Rectangle {
    anchors.fill: parent
    Image {
    ...
    }
    ...
}
Connections {
    target: backend
}
...
```

Bây giờ, đó là cách chúng tôi kết nối với các tín hiệu trăn.

Nếu chúng tôi không sử dụng phân luồng, giao diện người dùng của chúng tôi sẽ bị đóng băng. Khá rõ ràng khi nói rằng những gì chúng ta cần ở đây là phân luồng chứ không phải đa xử lý.

Tạo hai chức năng, một cho luồng một cho chức năng thực sự. Đây là nơi dấu gạch dưới có ích.

```python
...
import threading
from time import sleep
...
class Backend(QObject):

    def __init__(self):
        QObject.__init__(self)
    def bootUp(self):
        t_thread = threading.Thread(target=self._bootUp)
        t_thread.daemon = True
        t_thread.start()
    def _bootUp(self):
        while True:
            curr_time = strftime("%H:%M:%S", gmtime())
            print(curr_time)
            sleep(1)
...
```

Đoạn mã trên có chức năng gạch dưới thực hiện công việc tạo thời gian cập nhật.

Tạo một pyqtsignal được gọi là cập nhật và gọi nó từ một chức năng gọi là trình cập nhật

```python
...
from PyQt6.QtCore import QObject, pyqtSignal
...
    def __init__(self):
        QObject.__init__(self)
    updated = pyqtSignal(str, arguments=['updater'])
    def updater(self, curr_time):
        self.updated.emit(curr_time)
    ...
```

Trong đoạn mã trên, pyqtSignal, được cập nhật, có tham số đối số là danh sách chứa tên của hàm 'updater'. Từ chức năng cập nhật này, qml sẽ nhận dữ liệu. Trong chức năng cập nhật, chúng tôi gọi (phát ra) tín hiệu được cập nhật và truyền dữ liệu (curr_time) cho nó

Cập nhật qml, nhận tín hiệu bằng cách tạo bộ xử lý tín hiệu, tên bộ xử lý tín hiệu là dạng viết hoa của tên tín hiệu đứng trước 'bật'. Vì vậy, 'mySignal' trở thành 'onMySignal' và 'mysignal' trở thành 'onMysignal'.

```python
...
    target: backend
    function onUpdated(msg) {
        currTime = msg;
    }
...
```

Trong đoạn mã trên, bạn có thể thấy trình xử lý tín hiệu cho tín hiệu cập nhật được gọi là onUpdated. Nó cũng có curr_time được truyền cho nó dưới dạng msg.

Tất cả đều ổn nhưng chúng tôi vẫn chưa gọi chức năng cập nhật. Có một chức năng riêng biệt để gọi tín hiệu là không cần thiết cho một ứng dụng nhỏ như thế này. Nhưng trong một ứng dụng lớn, đó là cách nên làm. Thay đổi giây trễ thành 1/10 giây. Tôi đã tìm thấy con số này là tốt nhất để cập nhật thời gian.

```python
...
            curr_time = strftime("%H:%M:%S", gmtime())
            self.updater(curr_time)
            sleep(0.1)
...
```

Chức năng bootUp nên được gọi ngay sau khi giao diện người dùng được tải.

```python
...
engine.rootObjects()[0].setProperty('backend', back_end)
back_end.bootUp()
sys.exit(app.exec())
```

Tất cả đã xong!!!

Chạy mã:

```bat
python main.py
```

![Xây dựng Ứng dụng máy tính để bàn bằng Python](https://boxxv.github.io/img/2023/1_F59PHhThOIYJvcXJDjhXjQ.webp "How to build your first Desktop Application in Python")

## Bonus:
Làm cho cửa sổ không khung Frameless

Bạn có thể làm cho cửa sổ không có khung và dán nó vào phía dưới bên phải của Màn hình.

```python
...
height: 600
x: screen.desktopAvailableWidth - width - 12
y: screen.desktopAvailableHeight - height - 48
title: "HelloApp"
flags: Qt.FramelessWindowHint | Qt.Window
...
```

Đoạn mã trên đặt x, y cho cửa sổ và thêm các cờ để làm cho cửa sổ không có khung. Cờ Qt.Window đảm bảo rằng mặc dù cửa sổ không có khung nhưng chúng tôi vẫn nhận được nút Tác vụ

Chạy nó, và bạn nên vui mừng với những gì bạn nhìn thấy.

```bat
python main.py
```

![Xây dựng Ứng dụng máy tính để bàn bằng Python](https://boxxv.github.io/img/2023/1__ZDAL3RJZSKSz8qb8sLBIw.webp "How to build your first Desktop Application in Python")

Cuối cùng, mã hóa đã kết thúc và đây là mã cuối cùng.

```python
import sys
import os
from time import strftime, gmtime
import threading
from time import sleep
from PyQt6.QtGui import QGuiApplication
from PyQt6.QtQml import QQmlApplicationEngine
from PyQt6.QtQuick import QQuickWindow
from PyQt6.QtCore import QObject, pyqtSignal

class Backend(QObject):

    def __init__(self):
        QObject.__init__(self)
    updated = pyqtSignal(str, arguments=['updater'])
    def updater(self, curr_time):
        self.updated.emit(curr_time)
    def bootUp(self):
        t_thread = threading.Thread(target=self._bootUp)
        t_thread.daemon = True
        t_thread.start()
    def _bootUp(self):
        while True:
            curr_time = strftime("%H:%M:%S", gmtime())
            self.updater(curr_time)
            sleep(0.1)

QQuickWindow.setSceneGraphBackend('software')
app = QGuiApplication(sys.argv)
engine = QQmlApplicationEngine()
engine.quit.connect(app.quit)
engine.load('./UI/main.qml')
back_end = Backend()
engine.rootObjects()[0].setProperty('backend', back_end)
back_end.bootUp()
sys.exit(app.exec())
```

`main.qml`

```python
import QtQuick
import QtQuick.Controls.Basic
ApplicationWindow {
    visible: true
    width: 360
    height: 600
    x: screen.desktopAvailableWidth - width - 12
    y: screen.desktopAvailableHeight - height - 48
    title: "HelloApp"
    flags: Qt.FramelessWindowHint | Qt.Window
    property string currTime: "00:00:00"
    property QtObject backend
    Rectangle {
        anchors.fill: parent
        Image {
            sourceSize.width: parent.width
            sourceSize.height: parent.height
            source: "./images/playas.jpg"
            fillMode: Image.PreserveAspectFit
        }
        Text {
            anchors {
                bottom: parent.bottom
                bottomMargin: 12
                left: parent.left
                leftMargin: 12
            }
            text: currTime
            font.pixelSize: 48
            color: "white"
        }
    }

    Connections {
        target: backend
        function onUpdated(msg) {
            currTime = msg;
        }
    }
}
```

Ngoài những cái tên mà bạn có thể đã thay đổi, mọi thứ sẽ giống nhau.

-----

## Xây dựng và các bước tiếp theo
Xây dựng một ứng dụng pyqt có thể là dễ dàng nhất vì nó được biết đến rộng rãi.

Để xây dựng, hãy cài đặt pyinstaller, vì xây dựng là một phần của phần thưởng nên chúng tôi không cài đặt nó trước đây.

```bat
pip install pyinstaller
```

Chúng tôi có thể dễ dàng thực hiện việc chạy đoạn mã sau trong thư mục ứng dụng (helloApp), nhưng chúng tôi phải quản lý các tài nguyên mà chúng tôi đã sử dụng.

```bat
pyinstaller main.py
```

Thay vào đó, trước tiên hãy làm:

```bat
pyi-makespec main.py
```

Nó tạo ra một tệp thông số kỹ thuật để bạn cập nhật trước, sau đó bạn có thể chạy lại pyinstaller

Tham số datas có thể được sử dụng để bao gồm các tệp dữ liệu trong Ứng dụng hoặc thư mục Ứng dụng của bạn. Đó là một danh sách các bộ dữ liệu và bộ dữ liệu luôn có hai mục, đường dẫn đích, chúng tôi sẽ đưa vào và đường dẫn đích, nơi nó sẽ được lưu trữ trong thư mục của Ứng dụng. Đường dẫn đích phải tương đối. Nếu bạn muốn nó được đặt ngay tại đó cùng với các tệp thực thi của ứng dụng, bạn đặt nó thành một chuỗi rỗng (''), nếu bạn muốn nó nằm trong một thư mục lồng trong thư mục của ứng dụng, bạn chỉ định thư mục lồng nhau ('nest/nested/really_nested ')

Cập nhật tham số dữ liệu như bạn thấy bên dưới để khớp với đường dẫn đến thư mục giao diện người dùng của helloApp trên máy tính của bạn.

Đặt tham số bảng điều khiển thành Sai, vì đây là Gui và chúng tôi không kiểm tra nó.

`main.spec`

```python
...
a = Analysis(['main.py'],
             ...
             datas=[('I:/path/to/helloApp/UI', 'UI')],
             hiddenimports=[],
...
exe = EXE(pyz,
          a.scripts,
          [],
          ...
          name='main',
          debug=False,
          ...
          console=False )
coll = COLLECT(exe,
               ...
               upx_exclude=[],
               name='main')
```

Tham số tên trong lệnh gọi EXE là tên của chính tệp thực thi. ví dụ. main.exe hoặc main.dmg nhưng tham số tên trong lệnh gọi COLLECT dành cho tên thư mục chứa tệp thực thi và tất cả các tệp đi kèm của nó sẽ được lưu trữ, cả hai đều có thể thay đổi được. Nhưng các tên được dựa trên tệp chúng tôi đã sử dụng để tạo thông số kỹ thuật, hãy nhớ: 'main.py'

Cuối cùng, xây dựng ứng dụng của bạn bằng cách sử dụng

```bat
pyinstaller main.spec
```

Bây giờ, bạn sẽ thấy một thư mục có tên 'dist' với một thư mục khác bên trong có tên 'chính' chứa các tệp ứng dụng. Tìm kiếm main.exe hoặc tệp thực thi chính và chạy nó. TADAAA! Và tất cả đều tốt.

![Xây dựng Ứng dụng máy tính để bàn bằng Python](https://boxxv.github.io/img/2023/1_3TCec53425IT4gmvoUtZ5w.webp "How to build your first Desktop Application in Python")

## Bước tiếp theo
Ngoài cách thư mục giao diện người dùng được đưa vào và sử dụng trong ứng dụng, tất cả những thứ chúng tôi đã nói đến đều được sử dụng trong sản xuất. Tài nguyên được đóng gói trước khi được triển khai trong sản xuất.

Nhưng Tín hiệu, cách hình nền được sử dụng, cửa sổ không khung đều là những kỹ thuật được sử dụng trong sản xuất và có thể nói là trong thế giới thực. Nó chỉ là có nhiều hơn cho nó. Vâng, có nhiều thứ hơn đối với Windows không khung, bạn phải xử lý thanh tiêu đề, thay đổi kích thước và kéo cửa sổ trong số những thứ khác nếu bạn không sử dụng nó làm màn hình giật gân, không phức tạp lắm, nhưng nó vượt ra ngoài phạm vi của điều này hướng dẫn.

Qml không chỉ là Hình ảnh, Hình chữ nhật và Văn bản, và hệ thống Bố cục có bốn loại. Chúng rất dễ học, nhưng cách tiếp cận thực tế là tốt nhất, vì vậy tôi không buồn giải thích chúng.

Tiếp tục với PyQt và Qml, nó sẽ dẫn đến sự nghiệp phát triển phần mềm, hệ thống nhúng và trong tương lai là Trực quan hóa dữ liệu. Thích nó hơn TKinter, mức độ phổ biến của nó ngày càng tăng.

-----

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