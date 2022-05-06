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

Do đó, chạy tập lệnh python trên GPU có thể được chứng minh là tương đối nhanh hơn so với CPU, tuy nhiên, cần lưu ý rằng để xử lý tập dữ liệu với GPU, dữ liệu trước tiên sẽ được chuyển vào bộ nhớ của GPU, điều này có thể cần thêm thời gian vì vậy nếu dữ liệu đặt nhỏ thì CPU có thể hoạt động tốt hơn GPU.

### Bắt đầu

Hiện tại, chỉ GPU NVIDIA được hỗ trợ và những thứ được liệt kê trên [trang này](https://developer.nvidia.com/cuda-gpus). Nếu card đồ họa của bạn có nhân CUDA, thì bạn có thể tiến hành thêm việc thiết lập mọi thứ.

### Cài đặt

Trước tiên, hãy đảm bảo rằng trình điều khiển Nvidia đã được cập nhật và bạn có thể cài đặt cudatoolkit một cách rõ ràng [từ đây](https://developer.nvidia.com/cuda-downloads). sau đó cài đặt [Anaconda](https://www.anaconda.com/products/distribution) thêm anaconda vào môi trường trong khi cài đặt.
Sau khi hoàn thành tất cả các cài đặt, hãy chạy các lệnh sau trong command prompt.

```bat
conda install numba & conda install cudatoolkit
```

LƯU Ý: Nếu Anaconda không được thêm vào môi trường, hãy điều hướng đến cài đặt anaconda và định vị thư mục Scripts và mở dấu nhắc lệnh ở đó.

### CODE






-----
Tham khảo:
- [Running Python script on GPU](https://www.geeksforgeeks.org/running-python-script-on-gpu/)
- [Executing a Python Script on GPU Using CUDA and Numba in Windows 10
](https://medium.com/geekculture/executing-a-python-script-on-gpu-using-cuda-and-numba-in-windows-10-1a1b10c29c9)