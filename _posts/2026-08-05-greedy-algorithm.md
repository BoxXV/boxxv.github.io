---
layout: post
title: Thuật toán sắp xếp sản xuất
subtitle: "Production Scheduling Algorithms: A Practical Guide"
date: 2026-08-05 10:11:12
tags:
- Algorithm
- Greedy
- Scheduling
- Load Balancing
- Job Assignment
- Constraint Scheduling
- Backtracking
- Optimization Problem
---


## Mô tả bài toán

Bài toán lập lịch (Scheduling / Load Balancing / Job Assignment) với các ràng buộc:

- Mỗi linh kiện (Job) có thể gia công trên nhiều máy (MachineNo1 → MachineNo5).
- Có **thứ tự ưu tiên máy** (MachineNo1 cao nhất → MachineNo2 → MachineNo3 → MachineNo4 → MachineNo5).
- Có **giới hạn thời gian**: không được để máy gia công vượt quá `22:00`.
- Cần **tối ưu lại toàn bộ kế hoạch** khi các máy phụ cũng bị quá tải.
- Có khả năng phải **đổi máy của các linh kiện đã phân công trước đó** để giải cứu các linh kiện cuối cùng.

Đây không còn là thuật toán tuần tự đơn giản mà là `Constraint Scheduling` / `Backtracking` / `Optimization Problem`.

![Scheduling](https://boxxv.github.io/img/2026/so_do_gan_may_uu_tien.svg "Scheduling")

![Load Balancing](https://boxxv.github.io/img/2026/so_do_can_bang_tai_khi_qua_tai.svg "Load Balancing")

## Gởi ý

### Cách 1: Thuật toán tham lam (Greedy)

### Cách 2: Load Balancing thông minh

### Cách 3: Backtracking (Giải cứu các linh kiện cuối)

### Cách 4: Bipartite Matching / Min-Cost Max-Flow

### Cách 5: Constraint Programming (Khuyến nghị)

### Thuật toán thực tế đề xuất


## Kết luận

| Giải pháp                         | Mức tối ưu      | Độ khó     |
| --------------------------------- | --------------- | ---------- |
| Greedy                            | Thấp            | Dễ         |
| Load Balancing                    | Trung bình      | Dễ         |
| Greedy + Reassignment             | Cao             | Trung bình |
| Backtracking                      | Rất cao         | Khó        |
| Min-Cost Max-Flow                 | Tối ưu toàn cục | Khó        |
| Constraint Programming (OR-Tools) | Tối ưu nhất     | Khó        |

Đối với hệ thống sản xuất thực tế (100–10.000 linh kiện/ngày), tôi khuyến nghị `Greedy` + `Reassignment` + Sắp xếp theo số lượng máy khả dụng. Vì đạt khoảng 90–98% hiệu quả của thuật toán tối ưu nhưng vẫn triển khai đơn giản, chạy rất nhanh và dễ bảo trì.


-----
Tham khảo:
- [Thuật toán tham lam - Greedy Algorithm](https://viblo.asia/p/thuat-toan-tham-lam-greedy-algorithm-XQZGxozlvwA)
- []()
- []()