---
layout: post
title: Kiến trúc Microservices đang giết chết hiệu năng của bạn
subtitle: và đây là số liệu thống kê
image: "img/2026/xpahcwyrj4grkljj25kz.jpg"
date: 2026-01-20 10:11:12
tags:
- Microservices
- Monolith
- Modular Monolith
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
- [Chi phí tuần tự hóa](#chi-phí-tuần-tự-hóa)
    - [JSON Serialization Cost](#json-serialization-cost)
- [Khi nào kiến ​​trúc Microservices thực sự có ý nghĩa?](#khi-nào-kiến-trúc-microservices-thực-sự-có-ý-nghĩa)
    - [1. Yêu cầu mở rộng độc lập](#1-yêu-cầu-mở-rộng-độc-lập)
    - [2. Giới hạn của nhóm](#2-giới-hạn-của-nhóm)
    - [3. Sự đa dạng về công nghệ](#3-sự-đa-dạng-về-công-nghệ)
    - [4. Yêu cầu tuân thủ](#4-yêu-cầu-tuân-thủ)
- [Giải pháp thay thế: Kiến ​​trúc nguyên khối dạng mô-đun (Modular Monolith)](#giải-pháp-thay-thế-kiến-trúc-nguyên-khối-dạng-mô-đun-modular-monolith)
    - [So sánh hiệu năng](#so-sánh-hiệu-năng)
- [Cách chuyển đổi](#cách-chuyển-đổi)
    - [Giai đoạn 1: Xác định ứng viên (Tháng 1)](#giai-đoạn-1-xác-định-ứng-viên-tháng-1)
    - [Giai đoạn 2: Trích xuất một dịch vụ (Tháng 2-3)](#giai-đoạn-2-trích-xuất-một-dịch-vụ-tháng-2-3)
    - [Giai đoạn 3: Nhổ răng dần dần (Tháng 4-6)](#giai-đoạn-3-nhổ-răng-dần-dần-tháng-4-6)
    - [Phân tích chi phí: Số liệu thực tế](#phân-tích-chi-phí-số-liệu-thực-tế)
    - [Gỡ lỗi \& Khả năng quan sát](#gỡ-lỗi--khả-năng-quan-sát)
- [Ma trận quyết định](#ma-trận-quyết-định)
- [Vấn đề thực sự mà kiến ​​trúc Microservices giải quyết](#vấn-đề-thực-sự-mà-kiến-trúc-microservices-giải-quyết)
- [Kết luận: Nghịch lý về hiệu suất](#kết-luận-nghịch-lý-về-hiệu-suất)
- [Tham khảo](#tham-khảo)
- [Tóm lại](#tóm-lại)


![Monolith vs Microservices vs Modular Monoliths](https://boxxv.github.io/img/2026/66d12ddc-2abe-4a98-82d5-ee177e80487c_1470x1600.png "Monolith vs Microservices vs Modular Monoliths")

![Modular Monolith](https://boxxv.github.io/img/2026/Modular-Monolith.webp "Modular Monolith")

<!-- ![Modular Monolith](https://boxxv.github.io/img/2026/c2a0e8e9-9f9b-43de-b067-bad366303919_1994x1010.png "Modular Monolith") -->

![Modular Monolith là gì và tại sao bạn nên cân nhắc sử dụng?](https://boxxv.github.io/img/2026/ntech-1.jpeg "Modular Monolith là gì và tại sao bạn nên cân nhắc sử dụng?")

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


## Chi phí tuần tự hóa

Mỗi cuộc gọi mạng đều yêu cầu quá trình tuần tự hóa/giải tuần tự hóa (serialization/deserialization).

#### JSON Serialization Cost

Kiểm tra: Chuyển đổi phản hồi API điển hình (đối tượng người dùng với dữ liệu lồng nhau) thành chuỗi tuần tự.

```java
const user = {
  id: 123,
  name: "John Doe",
  email: "john@example.com",
  profile: { /* 50 fields */ },
  orders: [ /* 10 orders */ ]
};
```

**Kiểm tra hiệu năng (Node.js):**

| Hoạt động     | Thời gian               |
| ------- | ------------------ |
| Truy cập đối tượng trong bộ nhớ | 0,001ms |
| JSON.stringify() | 0,15ms |
| JSON.parse() | 0,20ms |
| Truyền tải mạng | 0,50ms |
| **Tổng cộng mỗi cuộc gọi** | **0,85ms** |

Trong một chuỗi kiến ​​trúc vi dịch vụ với 6 dịch vụ:

```
Total serialization overhead: 6 × 0.85ms = 5.1ms
```

Như vậy, chỉ riêng việc chuyển đổi dữ liệu từ/sang định dạng JSON đã mất 5 mili giây.


## Khi nào kiến ​​trúc Microservices thực sự có ý nghĩa?

Tôi không nói rằng "đừng bao giờ sử dụng kiến ​​trúc microservices".

**Sử dụng kiến ​​trúc microservices khi:**

#### 1. Yêu cầu mở rộng độc lập

Ví dụ: Nền tảng phát video trực tuyến

```
Video Upload Service: CPU-intensive (encoding)
  → Needs: 8 CPU cores, 4GB RAM
  → Scale: 5 instances

Metadata Service: Memory-intensive (search)
  → Needs: 2 CPU cores, 16GB RAM
  → Scale: 3 instances

Video Playback Service: I/O-intensive (CDN)
  → Needs: 1 CPU core, 2GB RAM
  → Scale: 20 instances
```

**Mỗi dịch vụ có nhu cầu tài nguyên khác nhau. Kiến trúc nguyên khối lãng phí tài nguyên.**

#### 2. Giới hạn của nhóm

Ví dụ: Công ty có hơn 100 kỹ sư

```
Nhóm A: Quản lý người dùng (15 kỹ sư)
Nhóm B: Xử lý thanh toán (10 kỹ sư)
Nhóm C: Quản lý kho (12 kỹ sư)
Nhóm D: Đề xuất (8 kỹ sư)
```

Kiến trúc Monolith:
- 100 kỹ sư cùng sử dụng một mã nguồn.
- Giải quyết xung đột hàng ngày
- Triển khai cơn ác mộng phối hợp

Kiến trúc Microservices:
- Các nhóm triển khai độc lập
- Ranh giới sở hữu rõ ràng
- Lặp lại nhanh hơn

**Ngưỡng**: `Hơn 50 kỹ sư cùng làm việc trên một sản phẩm`.


#### 3. Sự đa dạng về công nghệ

Ví dụ: Ứng dụng sử dụng nhiều học máy

```
Web API: Node.js (quen thuộc với nhóm phát triển web)
ML Model Serving: Python (scikit-learn, TensorFlow)
Real-time Analytics: Go (hiệu năng)
Data Processing: Rust (an toàn bộ nhớ)
```

Kiến trúc Monolith:
- Khó kết hợp các ngôn ngữ lập trình khác nhau.

Kiến trúc Microservices:
- Mỗi dịch vụ sử dụng công cụ tối ưu nhất cho công việc của mình.


#### 4. Yêu cầu tuân thủ

Ví dụ: Ứng dụng chăm sóc sức khỏe

```
Thông tin sức khỏe được bảo mật (PHI):
→ Nhật ký kiểm toán nghiêm ngặt
→ Mã hóa khi lưu trữ
→ Kiểm soát truy cập
→ Cơ sở dữ liệu riêng biệt

Thông tin không phải PHI (Thanh toán, Tiếp thị):
→ Bảo mật thông thường
→ Cơ sở dữ liệu dùng chung
```

Các dịch vụ riêng biệt giúp đơn giản hóa phạm vi tuân thủ.


## Giải pháp thay thế: Kiến ​​trúc nguyên khối dạng mô-đun (Modular Monolith)

Sự kết hợp hoàn hảo: cấu trúc nguyên khối monolith với kỷ luật của kiến ​​trúc microservices.

Kiến trúc:
```
┌─────────────────────────────────────┐
│         Application (Monolith)      │
│                                     │
│  ┌─────────┐  ┌─────────┐           │
│  │  User   │  │ Product │           │
│  │ Module  │  │ Module  │           │
│  └────┬────┘  └────┬────┘           │
│       │            │                │
│  ┌────┴────────────┴────┐           │
│  │   Shared Database    │           │
│  └─────────────────────┘            │
└─────────────────────────────────────┘
```

**Nguyên tắc chính:**

- Các mô-đun giao tiếp với nhau thông qua các interfaces (không phải HTTP).
- Ranh giới rõ ràng (như kiến ​​trúc microservices)
- Cơ sở dữ liệu dùng chung (lợi ích giao dịch)
- Triển khai một lần duy nhất (không tốn tài nguyên mạng)

#### So sánh hiệu năng

| Số liệu     | Microservices | Modular Monolith | Sự cải tiến |
| ------------- | ------------- |:------------:| ------------:|
| Độ trễ (p50)  | 18ms          | 12ms         | Nhanh hơn 33%         |
| Độ trễ (p99)  | 120ms         | 50ms         | Nhanh hơn 58%         |
| Thông lượng   | 8.500 yêu cầu/giây | 10.000 yêu cầu/giây | Cao hơn 18% |
| Bộ nhớ        | 2GB                | 512MB      | Giảm 75%     |
| Độ phức tạp   | Cao                | Trung bình | Đơn giản hơn |

**Những lợi ích**:

✅ Nhanh (không cần gọi mạng)  
✅ Có cấu trúc mô-đun (ranh giới rõ ràng)  
✅ Có khả năng giao dịch (đảm bảo ACID)  
✅ Có thể gỡ lỗi (chỉ một dấu vết ngăn xếp)  
✅ Có thể kiểm thử (không cần giả lập dịch vụ)


**Sự đánh đổi**:

⚠️ Triển khai đơn lẻ (không thể mở rộng quy mô các mô-đun độc lập)  
⚠️ Chỉ sử dụng một ngôn ngữ (thường là vậy)  
⚠️ Cơ sở dữ liệu dùng chung (cần phối hợp lược đồ)


## Cách chuyển đổi

Đừng viết lại toàn bộ kiến ​​trúc monolith thành microservices chỉ sau một đêm.

#### Giai đoạn 1: Xác định ứng viên (Tháng 1)

Tiêu chuẩn:
- Nhu cầu mở rộng độc lập
- Các yêu cầu công nghệ khác nhau
- Giới hạn của nhóm
- cách ly tuân thủ

Ví dụ:
```
Giữ nguyên trong khối hệ thống:
- Quản lý người dùng
- Danh mục sản phẩm
- Xử lý đơn hàng

Tách ra thành các dịch vụ:
- Mã hóa video (tốn nhiều CPU)
- Gửi email (tốn nhiều I/O)
- Đề xuất dựa trên học máy (chỉ dành cho Python)
```

#### Giai đoạn 2: Trích xuất một dịch vụ (Tháng 2-3)

Hãy bắt đầu với dịch vụ có rủi ro thấp nhất:

```
Trước:
┌─────────────────┐
│   Monolith      │
│  - Người dùng   │
│  - Sản phẩm     │
│  - Email        │ ← Trích xuất phần này
└─────────────────┘

Sau:
┌─────────────────┐     ┌─────────────┐
│   Monolith      │────→│   Email     │
│  - Người dùng   │     │  Service    │
│  - Sản phẩm     │     └─────────────┘
└─────────────────┘
```

Đo lường:
- Tác động của độ trễ
- Thay đổi tỷ lệ lỗi
- Độ phức tạp trong vận hành

Nếu lợi ích < chi phí: Dừng lại ở đây.


#### Giai đoạn 3: Nhổ răng dần dần (Tháng 4-6)

Trích xuất 1 dịch vụ mỗi tháng:

- Theo dõi hiệu suất
- Đo lường chi phí vận hành
- Xác nhận lợi ích


Dừng lại khi:

- Sự phức tạp lấn át lợi ích.
- Nhóm không thể quản lý thêm dịch vụ nào nữa.
- Hiệu năng suy giảm


#### Phân tích chi phí: Số liệu thực tế

Tình huống: Ứng dụng xử lý 10.000 yêu cầu/giây

Cơ sở hạ tầng Monolith

```
Ứng dụng:
- 3x t3.large instances (4 CPU, 8GB) @ $0.0832/hr
  = $180/tháng

Cơ sở dữ liệu:
- 1x db.r5.xlarge (4 vCPU, 32GB) @ $0.29/hr
  = $210/tháng

Bộ cân bằng tải:
- 1x ALB @ $20/tháng
  = $20/tháng

Tổng cộng: $410/tháng
```

Cơ sở hạ tầng Microservices

```
Services (4 services × 3 instances):
- 12x t3.medium instances (2 CPU, 4GB) @ $0.0416/hr
  = $360/tháng

Service Mesh:
- 12x sidecar proxies (overhead)
  = +30% CPU = $108/tháng

Database:
- 1x db.r5.2xlarge (8 vCPU, 64GB) @ $0.58/hr
  (needs more capacity for connection overhead)
  = $420/tháng

Load Balancers:
- 1x ALB (external) @ $20/tháng
- 1x NLB (internal) @ $25/tháng
  = $45/tháng

Service Discovery:
- Consul cluster (3 nodes) @ $30/tháng
  = $30/tháng

Monitoring (per-service):
- Datadog/New Relic @ $100/tháng
  = $100/tháng

Tổng cộng: $1,063/tháng
```

Kiến trúc microservices có chi phí cao hơn 2,6 lần cho cùng một khối lượng công việc.


#### Gỡ lỗi & Khả năng quan sát


Kiến trúc Monolith: Single Stack Trace

```
Error: Payment failed
    at processPayment (payment.js:42)
    at createOrder (order.js:18)
    at handleCheckout (checkout.js:5)
    at Router.post (/api/checkout)
```
Thời gian gỡ lỗi: 5 phút (follow stack trace)

Kiến trúc Microservices: Yêu cầu theo dõi phân tán

```
Error: Payment failed

Service: order-service
Trace ID: abc123
Span: checkout

↓ HTTP call (2ms)

Service: payment-service  
Trace ID: abc123
Span: process_payment
  ↓ HTTP call (150ms)

Service: stripe-gateway
Trace ID: abc123
Error: Card declined

Total trace spans: 15
Services involved: 4
Debug time: 30 minutes (correlate logs across services)
```

Các công cụ bổ sung cần thiết:
- Truy tìm nguồn gốc phân tán (Jaeger, Zipkin)
- Tổng hợp nhật ký (ELK, Loki)
- Khả năng quan sát mạng lưới dịch vụ (Istio, Linkerd)

Chi phí: 200-500 đô la Mỹ/tháng cho hệ thống giám sát (observability stack)


## Ma trận quyết định

**Liệu có nên sử dụng kiến ​​trúc microservices?**

```
Do you have 50+ engineers? 
├─ No → Monolith
└─ Yes
   ├─ Do services need independent scaling?
   │  ├─ No → Modular Monolith
   │  └─ Yes
   │     ├─ Can you afford 2-3x infrastructure cost?
   │     │  ├─ No → Monolith
   │     │  └─ Yes
   │     │     ├─ Can you afford performance degradation?
   │     │     │  ├─ No → Monolith
   │     │     │  └─ Yes → Microservices ✅
```

```
Bạn có hơn 50 kỹ sư không?
├─ Không → Kiến trúc Monolith
└─ Có
   ├─ Các dịch vụ có cần mở rộng độc lập không?
   │  ├─ Không → Modular Monolith (Kiến trúc Monolith dạng mô-đun)
   │  └─ Có
   │     ├─ Bạn có đủ khả năng chi trả chi phí cơ sở hạ tầng gấp 2-3 lần không?
   │     │  ├─ Không → Monolith
   │     │  └─ Có
   │     │     ├─ Bạn có đủ khả năng chấp nhận sự suy giảm hiệu năng không?
   │     │     │  ├─ Không → Monolith
   │     │     │  └─ Có → Microservices ✅
```

Đối với 90% ứng dụng: Kiến trúc Monolith hoặc Monolith dạng mô-đun


## Vấn đề thực sự mà kiến ​​trúc Microservices giải quyết

Kiến trúc microservices không giải quyết được các vấn đề kỹ thuật.

Họ giải quyết các vấn đề về tổ chức:
✅ Tự chủ nhóm  
✅ Triển khai độc lập  
✅ Trách nhiệm rõ ràng  
✅ Đa dạng công nghệ

Nếu bạn không gặp phải những vấn đề về tổ chức này, bạn không cần đến kiến ​​trúc microservices.


## Kết luận: Nghịch lý về hiệu suất

Kiến trúc microservices hứa hẹn:
- Khả năng mở rộng
- Khả năng phục hồi
- Hiệu suất

Kiến trúc microservices mang lại:
- Độ trễ cao hơn (+50-150%)
- Nhiều sự cố hơn (thời gian ngừng hoạt động gấp 5 lần)
- Độ phức tạp cao hơn (chi phí vận hành gấp 10 lần)

Nhưng cũng có:
- Độc lập của đội
- Chu trình lặp lại nhanh hơn (đối với các nhóm lớn)
- Tính linh hoạt của công nghệ

> Sự đánh đổi là có thật. Hãy lựa chọn một cách có ý thức.


## Tham khảo

Sách:
- "Building Microservices" by Sam Newman
- "Monolith to Microservices" by Sam Newman (đúng vậy, cùng một tác giả, cả hai phía)

Công cụ dành cho các hệ thống nguyên khối:
- Module boundaries: NX, Turborepo
- Testing: Jest, Playwright
- Deployment: Docker, single container

Công cụ dành cho kiến ​​trúc Microservices:
- Service mesh: Istio, Linkerd
- Tracing: Jaeger, Zipkin, Honeycomb
- Service discovery: Consul, Eureka

So sánh hiệu suất:
- [k6](https://k6.io) - Load testing
- [Artillery](https://www.artillery.io/) - Performance testing


## Tóm lại

Kiến trúc microservices mang lại:
- Độ trễ +50-150% (chi phí mạng)
- Tăng 300% mức sử dụng tài nguyên (nhiều phiên bản)
- Độ phức tạp vận hành tăng +500% (hệ thống phân tán)
- Chi phí cơ sở hạ tầng gấp 2-3 lần

Sử dụng kiến ​​trúc microservices khi:
- Hơn 50 kỹ sư cùng làm việc trên một sản phẩm.
- Yêu cầu mở rộng độc lập
- Cần có sự đa dạng về công nghệ.
- Yêu cầu cách ly tuân thủ

Nếu không: Hãy sử dụng kiến ​​trúc nguyên khối dạng mô-đun (Modular Monolith).



---
Tham khảo:
- [Microservices Are Killing Your Performance (And Here's the Math)](https://dev.to/polliog/microservices-are-killing-your-performance-and-heres-the-math-21op)
- [Monolith vs Microservices vs Modular Monoliths: What's the Right Choice](https://blog.bytebytego.com/p/monolith-vs-microservices-vs-modular)
- [Architecture 101: Modular Monolith — A Primer](https://anjireddy-kata.medium.com/architecture-101-modular-monolith-a-primer-36864f045697)
- [What is a Modular Monolith?](https://newsletter.techworld-with-milan.com/p/what-is-a-modular-monolith)
- [What Is a Modular Monolith?](https://www.geeksforgeeks.org/system-design/what-is-a-modular-monolith)
- [Modular Monolith là gì và tại sao bạn nên cân nhắc sử dụng?](https://blog.ntechdevelopers.com/modular-monolith-la-gi-va-tai-sao-ban-nen-can-nhac-su-dung/)