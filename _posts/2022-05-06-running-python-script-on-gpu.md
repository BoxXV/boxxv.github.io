---
layout: post
title: Chạy tập lệnh Python trên GPU bằng CUDA và Numba
subtitle: Running Python script on GPU using CUDA and Numba

tags:
- Python
- GPU
- CUDA
- Numba
---

![GPU](https://boxxv.github.io/img/posts/0_PIGh7ZJ-5mc0y2EJ.png "GPU")

GPU có nhiều lõi hơn CPU và do đó khi nói đến tính toán song song dữ liệu, GPU hoạt động tốt hơn đặc biệt so với CPU mặc dù GPU có tốc độ xung nhịp thấp hơn và nó thiếu một số tính năng quản lý lõi so với CPU.

What is clock speed?

Tốc độ của clock là tốc độ mà bộ xử lý có thể hoàn thành chu kỳ xử lý. Nó thường được đo bằng megahertz hoặc gigahertz. Một megahertz tương đương với một triệu chu kỳ mỗi giây, trong khi một gigahertz tương đương với một tỷ chu kỳ mỗi giây.

Chạy tập lệnh python trên GPU có thể xác minh là tương đối nhanh hơn CPU.
Nhưng nó sẽ luôn nhanh hơn CPU?
Câu trả lời là không!

Chạy tập lệnh python trên GPU có thể được chứng minh là tương đối nhanh hơn so với CPU. Tuy nhiên, cần lưu ý rằng để xử lý tập dữ liệu với GPU, dữ liệu trước tiên sẽ được chuyển vào bộ nhớ của GPU, điều này có thể cần thêm thời gian vì vậy nếu dữ liệu đặt nhỏ thì CPU có thể hoạt động tốt hơn GPU.

![GPU](https://boxxv.github.io/img/posts/0_rPr6XW638a1Ztd6N.png "GPU")

Ở đây trong hình này, bạn có thể thấy rằng ở tính toán ban đầu, GPU tiêu tốn nhiều thời gian tính toán hơn CPU. Điều này là do lời giải thích được đưa ra ở trên.

VÌ VẬY, ĐỪNG SỬ DỤNG GPU CHO CÁC DỮ LIỆU NHỎ!


### Bắt đầu

Trong bài viết này, chúng ta hãy xem cách sử dụng GPU để thực thi một tập lệnh Python. Chúng tôi sẽ sử dụng Compute Unified Device Architecture (CUDA) cho mục đích này.

CUDA là một nền tảng tính toán song song và mô hình lập trình được phát triển bởi NVIDIA để tính toán chung cho các đơn vị xử lý đồ họa (GPU).

Nhưng tại sao CUDA?

CUDA tập hợp một số thứ:
1. Phần cứng song song khổng lồ được xây dựng để vận hành mã chung (không đồ họa), với các trình điều khiển thích hợp để làm như vậy.
2. Ngôn ngữ lập trình dựa trên C để lập trình phần cứng nói trên và một hợp ngữ mà các ngôn ngữ lập trình khác có thể sử dụng làm mục tiêu.
3. Một bộ công cụ phát triển ứng dụng bao gồm các thư viện, các công cụ gỡ lỗi, biên dịch và biên dịch khác nhau và các ràng buộc cho phép các ngôn ngữ lập trình phía CPU gọi mã phía GPU.

Hiện tại, chỉ GPU NVIDIA được hỗ trợ và những thứ được liệt kê trên [trang này](https://developer.nvidia.com/cuda-gpus). Nếu card đồ họa của bạn có nhân CUDA, thì bạn có thể tiến hành thêm việc thiết lập mọi thứ.

### Cài đặt

Bạn có CUDA không? Bạn có GPU có đủ khả năng cung cấp CUDA không?

Kiểm tra nó trong CMD của bạn bằng cách thực hiện điều này.
```bat
nvidia-smi
```

![GPU](https://boxxv.github.io/img/posts/0_Xywbyr_Gn-4pIzoM.png "GPU")

Chà, bạn có một GPU hỗ trợ CUDA. Tiếp theo là gì? Kiểm tra phiên bản CUDA của bạn trong CMD của bạn bằng cách thực hiện điều này.

```bat
nvcc --version
```

Nếu bạn nhận được một cái gì đó như:
```bat
'nvcc' is not recognized as an internal or external command, operable program or batch file.
```

Thì bạn phải cài đặt Bộ công cụ CUDA. Bạn có thể tải Bộ công cụ CUDA mới nhất [tại đây](https://developer.nvidia.com/cuda-toolkit-32-downloads).

Khi bạn cài đặt đúng cách và nếu bạn đã định cấu hình PATH chính xác, khi bạn thực hiện cùng một lệnh, bạn sẽ nhận được kết quả như thế này.

![GPU](https://boxxv.github.io/img/posts/0_t0jTtPnAoWZ_W0iM.png "GPU")


Ngoài ra, bạn phải cài đặt Numba.

![Numba](https://boxxv.github.io/img/posts/0_3PUwcZM65hLFY-YZ.png "Numba")

Numba là một trình biên dịch tối ưu hóa Python mã nguồn mở, có nhận biết NumPy được tài trợ bởi Anaconda, Inc. Nó sử dụng dự án trình biên dịch LLVM để tạo mã máy từ cú pháp Python. Bạn có thể cài đặt Numba bằng cách sử dụng lệnh này trong CMD.

```bat
pip install numba
```

Bạn cũng có thể sử dụng môi trường Conda để cài đặt cả Bộ công cụ Numba và CUDA.

Trước tiên, hãy đảm bảo rằng trình điều khiển Nvidia đã được cập nhật và bạn có thể cài đặt cudatoolkit một cách rõ ràng [từ đây](https://developer.nvidia.com/cuda-downloads). Sau đó cài đặt [Anaconda](https://www.anaconda.com/products/distribution) thêm anaconda vào môi trường trong khi cài đặt.  
Sau khi hoàn thành tất cả các cài đặt, hãy chạy các lệnh sau trong command prompt.

```bat
conda install numba & conda install cudatoolkit
```

Bạn có thể kiểm tra phiên bản Numba bằng cách sử dụng các lệnh sau trong lời nhắc Python.
```bat
>>> import numba
>>> numba.__version__
```

![Numba](https://boxxv.github.io/img/posts/0_HEGMsUlzBCp51XsN.png "Numba")

LƯU Ý: Nếu Anaconda không được thêm vào môi trường, hãy điều hướng đến cài đặt anaconda và định vị thư mục Scripts và mở dấu nhắc lệnh ở đó.


### CODE

Chúng tôi sẽ sử dụng `numba.jit` decorator  cho chức năng chúng tôi muốn tính toán qua GPU. Decorator có một số tham số nhưng chúng tôi sẽ chỉ làm việc với tham số đích. Target yêu cầu `jit` biên dịch mã cho nguồn nào (“CPU” hoặc “Cuda”). “Cuda” tương ứng với GPU. Tuy nhiên, nếu CPU được chuyển làm đối số thì jit sẽ cố gắng tối ưu hóa mã chạy nhanh hơn trên CPU và cải thiện tốc độ.

```python
from numba import jit, cuda
import numpy as np
# to measure exec time
from timeit import default_timer as timer  
 
# normal function to run on cpu
def func(a):                               
    for i in range(10000000):
        a[i]+= 1     
 
# function optimized to run on gpu
@jit(target ="cuda")                        
def func2(a):
    for i in range(10000000):
        a[i]+= 1
if __name__=="__main__":
    n = 10000000                           
    a = np.ones(n, dtype = np.float64)
    b = np.ones(n, dtype = np.float32)
     
    start = timer()
    func(a)
    print("without GPU:", timer()-start)   
     
    start = timer()
    func2(a)
    print("with GPU:", timer()-start)
```

Output: dựa trên CPU = i3 6006u, GPU = 920M.
```bat
without GPU: 8.985259440999926
with GPU: 1.4247172560001218
```

#### Error when using numba and jit to run python with my gpu
```python
from numba import cuda
import code
code.interact(local=locals)

# function optimized to run on gpu 
@cuda.jit(target ="cuda")                         
def func2(a):
    for i in range(10000000):
        a[i]+= 1
```

[https://stackoverflow.com/questions/67155846/error-when-using-numba-and-jit-to-run-python-with-my-gpu](https://stackoverflow.com/questions/67155846/error-when-using-numba-and-jit-to-run-python-with-my-gpu)

#### Automatic parallelization with `@jit`

```python
from numba import njit, prange

@njit(parallel=True)
def prange_test(A):
    s = 0
    # Without "parallel=True" in the jit-decorator
    # the prange statement is equivalent to range
    for i in prange(A.shape[0]):
        s += A[i]
    return s
```

[https://numba.pydata.org/numba-doc/dev/user/parallel.html](https://numba.pydata.org/numba-doc/dev/user/parallel.html)


Tuy nhiên, phải lưu ý rằng mảng được sao chép đầu tiên từ ram sang GPU để xử lý và nếu hàm trả về bất kỳ thứ gì thì các giá trị trả về sẽ được sao chép từ GPU sang CPU trở lại. Do đó đối với các tập dữ liệu nhỏ, tốc độ của CPU tương đối nhanh hơn nhưng tốc độ có thể được cải thiện hơn nữa ngay cả đối với các tập dữ liệu nhỏ bằng cách chuyển mục tiêu là “CPU”. Cần đặc biệt chú ý khi hàm được viết dưới jit cố gắng gọi bất kỳ hàm nào khác thì hàm đó cũng phải được tối ưu hóa bằng jit nếu không hàm đó có thể tạo ra các mã chậm hơn.

Bạn có thể kiểm tra tab Hiệu suất tại Trình quản lý tác vụ trong khi thực thi mã mà GPU sẽ có đỉnh đột ngột từ 0 và sẽ quay trở lại 0, điều này cho thấy rằng GPU đã hoạt động.

Bạn có thể thử nhiều tập lệnh dựa trên GPU trong Windows 10 bằng cách tham [khảo tài liệu của Numba](https://numba.readthedocs.io/en/stable/cuda/index.html).

Chào mừng đến với thế giới máy tính song song.

Hy vọng bài viết có thể giúp ích. Chia sẻ suy nghĩ của bạn.


-----
Tham khảo:
- [Running Python script on GPU](https://www.geeksforgeeks.org/running-python-script-on-gpu/)
- [Executing a Python Script on GPU Using CUDA and Numba in Windows 10](https://medium.com/geekculture/executing-a-python-script-on-gpu-using-cuda-and-numba-in-windows-10-1a1b10c29c9)
- [How to run python on GPU with CuPy?](https://stackoverflow.com/questions/60027446/how-to-run-python-on-gpu-with-cupy)
- [GPU-Accelerated Computing with Python](https://developer.nvidia.com/how-to-cuda-python)
- [Python, Performance, and GPUs](https://towardsdatascience.com/python-performance-and-gpus-1be860ffd58d)