---
layout: post
title: Inter-Process Communication với C#
subtitle: Local Machine Interprocess Communication with .NET
image: "img/technology.png"
tags:
- IPC
- .NET
- C#
---

![IPC](https://boxxv.github.io/img/2023/Interprocess.png "IPC")

Để có thể hiểu sau hơn chút về sự giao tiếp này, hãy cùng lật lại về mô hình chúng ta thường làm - mô hình Nguyên Khối (Monolithic Architecture). Chúng ta đều biết, trong mô hình Nguyên Khối, các thành phần đều được liên kết đến nhau thông qua các lời gọi hàm hay các phương thức tùy ngôn ngữ. Điều này làm nó ít hay nhiều phụ thuộc vào ngôn ngữ hoặc chí ít là sẽ phụ thuộc lẫn nhau.

Đi ngược lại với quan điểm xây dựng chung trên cùng một khối, mô hình Microservice lại xây dựng nhiều khối phân tán trên các máy khác nhau. Mà thường mỗi một khối là một quá trình. Do đó các quá trình này sẽ cần một cơ chế giao tiếp giữa các quá trình (Inter‑Process Communication hay IPC) này để tương tác được với nhau.


## I. Un


-----
Tham khảo:

- []()
- []()