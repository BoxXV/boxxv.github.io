---
layout: post
title: Thiết kế 3D với Python và FreeCAD
subtitle: 3D design with Python and FreeCAD
tags:
- Anaconda
- Miniconda
- Conda
- Python
- FreeCAD
- Flask
- Django
- Docker
- Windows
- IIS
- CGI
- FastCGI
---

Các gói 3D CAD có thể là công việc khó khăn; có rất nhiều thứ để học, đó có thể là một vấn đề lớn đối với một người dùng không thường xuyên như tôi.

Hầu hết các gói hỗ trợ một số dạng tập lệnh, vậy tại sao không lập trình thiết kế hoàn chỉnh của tôi từ đầu mà không cần chạm vào GUI? FreeCAD là một gói thiết kế 3D (miễn phí), với giao diện Python toàn diện, vì vậy có vẻ là lý tưởng…

![placeholder](https://boxxv.github.io/img/posts/freecad.png "FreeCAD")

Điều này đơn giản về lý thuyết, nhưng hơi phức tạp trong thực tế; Tôi sẽ không tiếc cho bạn nhiều lần bắt đầu sai khó chịu mà tôi đã thực hiện và mô tả một số cách đơn giản để tạo các đối tượng 3D từ đầu bằng Python. Đây là một công việc đang được tiến hành, nhưng hy vọng sẽ cung cấp một số gợi ý hữu ích nếu bạn là một lập trình viên Python thỉnh thoảng thực hiện thiết kế 3D.

Các ví dụ ở đây đã được thử nghiệm với FreeCAD v0.16 và phiên bản hiện tại 0.18

# Install FreeCAD

### Download FreeCAD
[https://www.freecadweb.org/downloads.php](https://www.freecadweb.org/downloads.php)

**Windows**  
Dec 9, 2020  
[https://github.com/FreeCAD/FreeCAD/releases/download/0.18.4/FreeCAD-0.18.4.980bf90-WIN-x32-installer.exe](https://github.com/FreeCAD/FreeCAD/releases/download/0.18.4/FreeCAD-0.18.4.980bf90-WIN-x32-installer.exe)  
[https://github.com/FreeCAD/FreeCAD/releases/download/0.18.4/FreeCAD-0.18.4.980bf90-WIN-x64-installer.exe](https://github.com/FreeCAD/FreeCAD/releases/download/0.18.4/FreeCAD-0.18.4.980bf90-WIN-x64-installer.exe)

**Mac**  
Dec 9, 2020  
[https://github.com/FreeCAD/FreeCAD/releases/download/0.18.4/FreeCAD_0.18-16146-rev1-OSX-x86_64-conda-Qt5-Py3.dmg](https://github.com/FreeCAD/FreeCAD/releases/download/0.18.4/FreeCAD_0.18-16146-rev1-OSX-x86_64-conda-Qt5-Py3.dmg)

**Linux**  
Dec 9, 2020  
[https://github.com/FreeCAD/FreeCAD/releases/download/0.18.4/FreeCAD_0.18-16146-rev1-Linux-Conda_Py3Qt5_glibc2.12-x86_64.AppImage](https://github.com/FreeCAD/FreeCAD/releases/download/0.18.4/FreeCAD_0.18-16146-rev1-Linux-Conda_Py3Qt5_glibc2.12-x86_64.AppImage)


### Import FreeCAD to external python apps

Đảm bảo rằng `...\FreeCAD\bin\` có trong đường dẫn.

```python
import sys 
sys.path.append("C:\\Program Files\\FreeCAD 0.18\\bin") 
import FreeCAD
```

# Install FreeCAD by Conda

Cách nhanh nhất để có được `conda` là cài đặt [Miniconda](https://docs.conda.io/en/latest/miniconda.html), một phiên bản mini của [Anaconda](https://www.anaconda.com) chỉ bao gồm conda và các phụ thuộc của nó. Nếu bạn muốn có [conda](https://docs.conda.io/en/latest/) cộng với hơn 7.500 gói mã nguồn mở, hãy cài đặt [Anaconda](https://www.anaconda.com/products/individual).


```bat
conda create --name fcenv --channel conda-forge freecad

conda activate fcenv

where freecad
C:\Users\{username}\anaconda3\envs\fcenv\Library\bin\freecad.exe
or
C:\Users\{username}\.conda\envs\fcenv\Library\bin\freecad.exe
```

```python
import sys

# sys.path.append('C:\\Users\\computer\\anaconda3\\envs\\fcenv\\Library\\bin')
# or
# sys.path.append('C:\\Users\\computer\\.conda\\envs\\fcenv\\Library\\bin')

import FreeCAD
```




-----
Tham khảo:
- [3D design with Python and FreeCAD](https://iosoft.blog/2019/05/22/3d-design-python-freecad/)
- [How can I import FreeCAD to external python apps? *RESOLVED*](https://forum.freecadweb.org/viewtopic.php?t=4650)

