---
layout: post
title: Kiến trúc Microservices đang giết chết hiệu năng của bạn
subtitle: và đây là số liệu thống kê
image: "img/2026/xpahcwyrj4grkljj25kz.jpg"
date: 2026-01-01 11:11:11
tags:
- Microservices
- 
- 
---

**Lời hứa**: Kiến trúc microservices giúp hệ thống của bạn dễ mở rộng, dễ bảo trì và nhanh chóng.

**Thực tế là**: Đối với hầu hết các hệ thống, kiến ​​trúc microservices làm tăng **độ trễ, độ phức tạp và các điểm lỗi** mà không mang lại lợi ích đáng kể nào.

Hãy cùng xem xét các con số thực tế.

- [Chi phí hiệu năng của các cuộc gọi mạng Lan trong cùng trung tâm dữ liệu](#chi-phí-hiệu-năng-của-các-cuộc-gọi-mạng-lan-trong-cùng-trung-tâm-dữ-liệu)
    - [So sánh độ trễ](#so-sánh-độ-trễ)
    - [Ví dụ thực tế](#ví-dụ-thực-tế)
- [Vấn đề dịch vụ N+1](#vấn-đề-dịch-vụ-n1)
    - [Ví dụ: Hiển thị bảng điều khiển người dùng](#ví-dụ-hiển-thị-bảng-điều-khiển-người-dùng)
- [Chi phí ẩn: Tiêu chuẩn thực tế](#chi-phí-ẩn-tiêu-chuẩn-thực-tế)
    - [Kiến trúc 1: Monolith](#kiến-trúc-1-monolith)
    - [Kiến trúc 2: Microservices](#kiến-trúc-2-microservices)
- [Phân tích chi phí mạng](#phân-tích-chi-phí-mạng)
- [Vấn đề thất bại dây chuyền](#vấn-đề-thất-bại-dây-chuyền)
- [Tranh chấp cơ sở dữ liệu](#tranh-chấp-cơ-sở-dữ-liệu)
    - [Tác động đến hiệu suất](#tác-động-đến-hiệu-suất)



---

## Chi phí hiệu năng của các cuộc gọi mạng Lan trong cùng trung tâm dữ liệu


**Vấn đề cốt lõi**: Các microservice giao tiếp qua mạng. Mạng thì chậm.

#### So sánh độ trễ

Gọi hàm nội bộ (kiến trúc nguyên khối monolith):
```
Function call: 0.001ms (1 microsecond)
```

Cuộc gọi HTTP trong cùng trung tâm dữ liệu (kiến trúc microservices):
```
HTTP request: 1-5ms (1,000-5,000 microseconds)
```

`Chậm hơn từ 1.000 đến 5.000 lần.`


#### Ví dụ thực tế

**Tình huống**: Quy trình thanh toán thương mại điện tử

Các thao tác cần thiết:

1. Xác thực phiên người dùng
2. Kiểm tra tồn kho sản phẩm
3. Tính toán chi phí vận chuyển
4. Xử lý thanh toán
5. Tạo bản ghi đơn hàng
6. Gửi email xác nhận

Kiến trúc nguyên khối:
```
Total time: 6 function calls × 0.001ms = 0.006ms
Database queries: 3 × 2ms = 6ms
External API (payment): 150ms
Total: ~156ms
```

Kiến trúc microservices:
```
Service calls:
- User service: 2ms
- Inventory service: 3ms  
- Shipping service: 2ms
- Payment service: 2ms + 150ms (external API)
- Order service: 3ms
- Notification service: 2ms

Each call includes:
- Serialization/deserialization: 0.5ms
- Network latency: 1-2ms
- Service processing: 1-2ms

Total service overhead: 6 services × 3ms = 18ms
Database queries: 6 services × 1 query × 2ms = 12ms
External API: 150ms
Total: ~180ms
```

**Kết quả:** Kiến trúc microservices `chậm hơn 15%` đối với luồng xử lý đơn giản này.


## Vấn đề dịch vụ N+1

Trong cơ sở dữ liệu, chúng ta biết về truy vấn N+1. Kiến trúc microservices có N+1 dịch vụ.

#### Ví dụ: Hiển thị bảng điều khiển người dùng

Yêu cầu:
- Hiển thị hồ sơ người dùng
- Hiển thị 10 đơn hàng gần nhất
- Hiển thị các đề xuất dựa trên lịch sử đơn hàng

Kiến trúc nguyên khối:

```sql
-- Single query with JOIN
SELECT 
  users.*,
  orders.*,
  recommendations.*
FROM users
LEFT JOIN orders ON orders.user_id = users.id
LEFT JOIN recommendations ON recommendations.user_id = users.id
WHERE users.id = $1
LIMIT 10;
```

Thời gian thực thi: ~5ms


Kiến trúc microservices (thực tế):

```java
// 1. Get user
const user = await userService.getUser(userId);        // 3ms

// 2. Get orders (requires user_id from step 1)
const orders = await orderService.getOrders(userId);   // 3ms

// 3. Get recommendations (requires orders from step 2)
const orderIds = orders.map(o => o.id);
const recommendations = await recommendationService
  .getByOrders(orderIds);                              // 3ms

// Total: 9ms (sequential)
// Can't parallelize due to data dependencies
```

Thời gian thực thi: ~9ms (chậm hơn 80%)

Và điều này giả định rằng:
- Điều kiện mạng hoàn hảo
- Không có lỗi dịch vụ nào xảy ra
- Không có logic thử lại
- Không có cầu dao ngắt mạch


## Chi phí ẩn: Tiêu chuẩn thực tế

Hãy đo lường chi phí gián tiếp thực tế bằng một thí nghiệm có kiểm soát.

**Thiết lập thử nghiệm**

**Hệ thống**: Ứng dụng CRUD đơn giản

- 4 thực thể: Người dùng, Sản phẩm, Đơn hàng, Thanh toán
- Tải 10.000 yêu cầu/giây
- Các phiên bản AWS EC2 t3.medium

#### Kiến trúc 1: Monolith

```
┌─────────────────┐
│   Application   │
│   (Node.js)     │
│                 │
│  ┌───────────┐  │
│  │ Database  │  │
│  │ (Postgres)│  │
│  └───────────┘  │
└─────────────────┘
```

Cấu hình:
- Một tiến trình Node.js duy nhất
- Gộp kết nối (20 kết nối)
- Bộ nhớ đệm Redis (cùng một phiên bản)

#### Kiến trúc 2: Microservices

```
┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐
│  User    │  │ Product  │  │  Order   │  │ Payment  │
│ Service  │  │ Service  │  │ Service  │  │ Service  │
└────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘
     │             │             │             │
     └─────────────┴─────────────┴─────────────┘
                   │
            ┌──────┴──────┐
            │  Postgres   │
            │  (shared)   │
            └─────────────┘
```

Cấu hình:
- 4 dịch vụ Node.js
- Mạng lưới dịch vụ (Istio)
- Cùng một cơ sở dữ liệu Postgres
- Bộ nhớ đệm Redis (dùng chung)

Kết quả so sánh

| Số liệu       | Monolith      | Microservices | Sự khác biệt |
| ------------- | ------------- |:-------------:| ------------:|
| Độ trễ p50    | 12ms          | 18ms          | +50%         |
| Độ trễ p95    | 25ms          | 45ms          | +80%         |
| Độ trễ p99    | 50ms          | 120ms         | +140%        |
| Thông lượng   | 10.000 yêu cầu/giây | 8.500 yêu cầu/giây | -15% |
| Mức sử dụng CPU | 45%         | 65%           | +44%         |
| Mức sử dụng bộ nhớ | 512MB    | 2GB           | +300%        |
| Network I/O   | 50 MB/s       | 180 MB/s      | +260%        |

Những phát hiện chính:

- Độ trễ ở đuôi bị ảnh hưởng nhiều nhất (trang 99: +140%)
- Việc sử dụng tài nguyên tăng lên đáng kể
- Hiệu suất giảm bất chấp khả năng "mở rộng".


## Phân tích chi phí mạng

Hãy cùng phân tích xem thời gian được tiêu tốn ở những bước nào trong một lời gọi microservice.

**Cấu trúc của một cuộc gọi giữa các dịch vụ**

Tổng thời gian: ~3ms

```
DNS resolution: 0.1ms (cached)
TCP handshake: 0.5ms (within datacenter)
TLS handshake: 1.0ms (if using HTTPS)
HTTP headers: 0.2ms
Request serialization: 0.3ms (JSON)
Network transmission: 0.5ms
Service processing: 0.5ms
Response serialization: 0.3ms
Network transmission: 0.5ms
Response parsing: 0.2ms
────────────────────────────
Total: ~3.0ms
```

Trong một Monolith:

```
Function call: 0.001ms
────────────────────────
Total: 0.001ms
```

Như vậy, chi phí vận hành sẽ cao gấp 3.000 lần so với cùng một thao tác.


## Vấn đề thất bại dây chuyền

Kiến trúc microservices làm tăng tỷ lệ lỗi.

**Toán học thất bại**

Các giả định:
- Mỗi dịch vụ đều có thời gian hoạt động ổn định 99,9% (ba số chín - khá tốt!).
- Yêu cầu này cần 5 dịch vụ.

Kiến trúc Monolith:
```
Availability: 99.9%
Downtime: 43 minutes/month
```

Kiến trúc Microservices (5 dịch vụ nối tiếp nhau):
```
Availability: 0.999^5 = 0.995 = 99.5%
Downtime: 3.6 hours/month
```

Như vậy thời gian ngừng hoạt động sẽ tăng gấp 5 lần.

Real-World Cascade
```
User Request
    ↓
API Gateway (99.9%)
    ↓
Auth Service (99.9%)
    ↓
Product Service (99.9%)
    ↓
Inventory Service (99.9%)
    ↓
Price Service (99.9%)
    ↓
Response

Combined availability: 99.5%
```

Thêm vào:
- Bộ ngắt mạch (làm tăng độ trễ)
- Thử lại (3 lần gọi mạng khi thất bại)
- Phương án dự phòng (suy giảm một phần)

**Kết quả**: Phức tạp, chậm chạp, và vẫn thường xuyên gặp lỗi hơn.


## Tranh chấp cơ sở dữ liệu

Kiến trúc microservices không giải quyết được vấn đề tắc nghẽn cơ sở dữ liệu - mà ngược lại, nó làm cho vấn đề trở nên tồi tệ hơn.

**Vấn đề**

Kiến trúc Monolith:
```
Application → Connection Pool (20) → Database
```

Kiến trúc Microservices:
```
User Service → Pool (20) ───┐
Product Service → Pool (20) ├→ Database (max 100 connections)
Order Service → Pool (20) ──┤
Payment Service → Pool (20) ┘

Total connections: 80 (near database limit)
```

Vấn đề:
1. Sự cạn kiệt kết nối nhanh hơn
2. Tình trạng tranh chấp khóa gia tăng (nhiều giao dịch đồng thời hơn)
3. Bộ nhớ đệm truy vấn kém hiệu quả hơn (mô hình truy cập khác nhau tùy theo dịch vụ)

#### Tác động đến hiệu suất

Thử nghiệm: 1.000 người dùng đồng thời

| Kiến trúc     | Các kết nối được sử dụng | Thời gian chờ khóa | Thời gian truy vấn |
| ------------- | ------------- |:------------:| ------------:|
| Monolith      | 20-30         | 5ms          | 10ms         |
| Microservices | 60-80         | 25ms         | 18ms         |

**Kiến trúc microservices sử dụng 3 kết nối và có mức độ tranh chấp khóa gấp 5 lần.**






---
Tham khảo:
- [Microservices Are Killing Your Performance (And Here's the Math)](https://dev.to/polliog/microservices-are-killing-your-performance-and-heres-the-math-21op)
