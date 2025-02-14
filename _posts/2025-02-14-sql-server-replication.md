---
layout: post
title: SQL Server Replication
subtitle: Kỹ thuật Replication trong MS SQL Server
date: 2025-02-14 01:00:00
tags:
- SQL
- Replication
- SQL Server
---

10 năm trong lĩnh vực phát triển .NET đã dạy tôi nhiều điều hơn là chỉ viết mã sạch.

- [Giới thiệu SQL Server Replication](#giới-thiệu-sql-server-replication)
  - [1. SQL Server Replication là gì?](#1-sql-server-replication-là-gì)
  - [2. Khi nào cần sử dụng SQL server replication?](#2-khi-nào-cần-sử-dụng-sql-server-replication)
  - [3. Cách hoạt động của SQL Server Replication](#3-cách-hoạt-động-của-sql-server-replication)
  - [4. Các loại Replication trong SQL Server](#4-các-loại-replication-trong-sql-server)
    - [Snapshot Replication](#snapshot-replication)
    - [Transactional Replication](#transactional-replication)
    - [Merge Replication](#merge-replication)
  - [5. Ưu và nhược điểm của SQL Server Replication](#5-ưu-và-nhược-điểm-của-sql-server-replication)
  - [6. Khi nào nên sử dụng SQL Server Replication?](#6-khi-nào-nên-sử-dụng-sql-server-replication)
- [Các bước chuẩn bị trước khi cấu hình Replication](#các-bước-chuẩn-bị-trước-khi-cấu-hình-replication)
  - [1. Chia sẻ thư mục snapshot](#1-chia-sẻ-thư-mục-snapshot)
  - [2. Cấu hình Distribution](#2-cấu-hình-distribution)
- [Cấu hình Transactional Replication](#cấu-hình-transactional-replication)
  - [1. Sơ nét về transactional replication](#1-sơ-nét-về-transactional-replication)
  - [2. Các bước cấu hình transactional replication](#2-các-bước-cấu-hình-transactional-replication)
    - [Tại publisher](#tại-publisher)
    - [Tại subscriber](#tại-subscriber)
- [Cấu hình Merge Replication](#cấu-hình-merge-replication)
  - [1. Sơ nét về merge replication](#1-sơ-nét-về-merge-replication)
  - [2. Các bước cấu hình merge replication](#2-các-bước-cấu-hình-merge-replication)
    - [Tại publisher](#tại-publisher-1)
    - [Tại subscriber](#tại-subscriber-1)
- [Cấu hình Peer-to-Peer Replication](#cấu-hình-peer-to-peer-replication)
  - [1. Sơ nét về peer-to-peer replication](#1-sơ-nét-về-peer-to-peer-replication)
  - [2. Các bước cấu hình transactional replication](#2-các-bước-cấu-hình-transactional-replication-1)
    - [Tại VINAHOST1](#tại-vinahost1)
    - [Tại VINAHOST2](#tại-vinahost2)
- [Kết luận](#kết-luận)


# Giới thiệu SQL Server Replication

Trong hệ thống quản lý cơ sở dữ liệu, việc đảm bảo tính nhất quán và tính sẵn sàng của dữ liệu là vô cùng quan trọng, đặc biệt đối với các ứng dụng doanh nghiệp.

Một trong những giải pháp hữu hiệu mà SQL Server cung cấp để đáp ứng nhu cầu này là SQL Server Replication.

## 1. SQL Server Replication là gì?

SQL Server Replication là một tính năng cho phép sao chép và đồng bộ dữ liệu giữa nhiều cơ sở dữ liệu trong hệ thống. Mục tiêu chính của Replication là đảm bảo rằng dữ liệu ở các vị trí khác nhau luôn được cập nhật đồng nhất, phục vụ tốt cho các trường hợp như:

- Cung cấp dữ liệu cho các ứng dụng khác nhau.
- Tăng cường hiệu suất khi có nhiều người dùng truy cập đồng thời.
- Sao lưu và phục hồi dữ liệu một cách dễ dàng.

## 2. Khi nào cần sử dụng SQL server replication?

Replication là giải pháp được ứng dụng cho môi trường phân phối dữ liệu trên nhiều server, chính vì vậy mà sử dụng chúng khi:

- Sao chép và phân phối dữ liệu trên nhiều server khác nhau.
- Phân phối bản sao dữ liệu theo lịch trình nhất định.
- Phân phối dữ liệu vừa thay đổi trên nhiều server khác nhau.
- Cho phép nhiều người dùng và nhiều server kết hợp dữ liệu khác nhau một cách thống nhất mà không sợ mất dữ liệu.
- Xây dựng CSDL sử dụng cho những ứng dụng trực tuyến hay ngoại tuyến.
- Xây dụng ứng dụng web khi người dùng cần trình bày một số lượng lớn dữ liệu.

## 3. Cách hoạt động của SQL Server Replication

SQL Server Replication hoạt động dựa trên mô hình xuất bản (`Publish-Subscribe`). Trong đó, dữ liệu được xuất bản từ một máy chủ chính (Publisher) và được phân phối đến các máy chủ khác (Subscriber). Quá trình này có sự hỗ trợ từ `Distributor` – thành phần quản lý việc phân phối dữ liệu.

Các thành phần chính:

- **Publisher**: Máy chủ hoặc cơ sở dữ liệu cung cấp dữ liệu cần sao chép.
- **Subscriber**: Máy chủ hoặc cơ sở dữ liệu nhận dữ liệu được sao chép.
- **Distributor**: Đóng vai trò trung gian, quản lý quá trình phân phối dữ liệu từ Publisher đến Subscriber.
- **Article**: Là một bảng dữ liệu, một phần dữ liệu hay những đối tượng CSDL sẽ nhân bản. Một Article có thể là một bảng dữ liệu bao gồm column và row hay một stores produre…
- **Publication**: Là tập của một hay nhiều Article từ một CSDL. Chúng được nhóm lại với nhau một cách hệ thống thành một tâp dữ liệu cùng với các đối tượng CSDL mà bạn muốn nhân bản trên nhiều Server với nhau.

## 4. Các loại Replication trong SQL Server

SQL Server hỗ trợ ba loại hình Replication chính:

### Snapshot Replication

- Dữ liệu được sao chép nguyên trạng tại một thời điểm nhất định.
- Phù hợp cho các hệ thống yêu cầu cập nhật dữ liệu không liên tục hoặc khối lượng dữ liệu nhỏ.

### Transactional Replication

- Các thay đổi trong Publisher được sao chép ngay lập tức đến Subscriber.
- Phù hợp với các hệ thống yêu cầu tính nhất quán cao, thường xuyên cập nhật.

### Merge Replication

- Cho phép Publisher và Subscriber đều có thể chỉnh sửa dữ liệu. Các thay đổi được đồng bộ hóa theo chu kỳ.
- Phù hợp cho các ứng dụng cần đồng bộ dữ liệu giữa nhiều điểm không kết nối thường xuyên, ví dụ như hệ thống bán hàng di động.

## 5. Ưu và nhược điểm của SQL Server Replication

Ưu điểm:

- Đáp ứng tốt các nhu cầu sao chép và đồng bộ dữ liệu phức tạp.
- Tăng khả năng chịu lỗi nhờ việc lưu trữ dữ liệu ở nhiều nơi.
- Cải thiện hiệu suất truy cập nhờ phân phối dữ liệu đến các Subscriber.

Nhược điểm:

- Quản lý và triển khai Replication có thể phức tạp đối với hệ thống lớn.
- Tiêu tốn băng thông khi sao chép dữ liệu liên tục.
- Cần cấu hình đúng cách để tránh các lỗi như xung đột dữ liệu.

## 6. Khi nào nên sử dụng SQL Server Replication?

Bạn nên cân nhắc sử dụng Replication trong các tình huống sau:

- Dữ liệu cần được sao chép đến nhiều địa điểm để tăng khả năng truy cập.
- Yêu cầu đồng bộ hóa dữ liệu giữa các ứng dụng khác nhau.
- Đảm bảo dữ liệu dự phòng trong các hệ thống quan trọng.


# Các bước chuẩn bị trước khi cấu hình Replication

## 1. Chia sẻ thư mục snapshot

Thư mục snapshot là thư mục được dùng để tạo và lưu trữ snapshot của publication.

Các bước thực hiện như sau:

- Truy cập thư mục **C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQL SERVER\MSSQL**
- Nhấp chuột phải vào thư mục **repldata** và chọn **Properties** (nếu thư mục không tồn tại thì ta sẽ tự tạo thư mục **repldata**)
- Chọn tab **Sharing**, và nhấp vào **Advanced Sharing…**

![Replication](https://boxxv.github.io/img/2025/c4b354a2e3-vinahost-cac-buoc-chuan-bi-truoc-khi-cau-hinh-replication-1.png "Replication")

- Tại cửa sổ **Advanced Sharing**, ta đánh dấu check vào ô **Share this folder** và nhấp vào **Permission**

![Replication](https://boxxv.github.io/img/2025/8e1d248f0b-vinahost-cac-buoc-chuan-bi-truoc-khi-cau-hinh-replication-2.png "Replication")

- Tại cửa sổ **Permission for repldata**, ta đánh dấu check vào ô **Full control** và bấm **OK**

![Replication](https://boxxv.github.io/img/2025/756d47c829-vinahost-cac-buoc-chuan-bi-truoc-khi-cau-hinh-replication-3.png "Replication")


## 2. Cấu hình Distribution

Ở phần này, ta sẽ cấu hình Distribution sử dụng thư mục snapshot đã chia sẻ ở trên

Các bước thực hiện như sau:

- Mở phần mềm **SQL Server Management Studio**, kết nối tới Publisher
- Nhấp chuột phải vào **Replication**, chọn **Configure Distribution…**

![Replication](https://boxxv.github.io/img/2025/88a69653ec-vinahost-cac-buoc-chuan-bi-truoc-khi-cau-hinh-replication-4.png "Replication")

- Tất cả các bước ta để mặc định, riêng tại cửa sổ **Configure Distribution Wizard** ta thay Snapshot folder lại thành **\\<computer_name>\repldata** như hình sau:

![Replication](https://boxxv.github.io/img/2025/46a6ca79f8-vinahost-cac-buoc-chuan-bi-truoc-khi-cau-hinh-replication-5.png "Replication")

Vậy là ta đã hoàn tất các bước chuẩn bị cho việc cấu hình replication.


# Cấu hình Transactional Replication

## 1. Sơ nét về transactional replication

Transactional replication thường được dùng trong môi trường server – to – server, cơ chế hoạt động tương tự như master – slave. Một server ở trạng thái active (publisher) chạy chính, một server ở dạng read-only (subscriber) cập nhật CSDL từ publisher mỗi khi CSDL có sự thay đổi với tần suất cập nhật gần như realtime.

Transactional replication thường được dùng trong các trường hợp sau:

- Người dùng có nhu cầu cập nhật các thay đổi tới subscriber ngay khi chúng xảy ra
- Ứng dụng yêu cầu độ trễ thấp giữa các lần thay đổi dữ liệu
- Ứng dụng yêu cầu truy cập dữ liệu tức thời. Ví dụ một row bị thay đổi 5 lần, transactional replication cho phép ứng dụng nhận được dữ liệu tại mỗi lần thay đổi, thay vì nhận lần thay đổi cuối cùng
- Publisher có tần suất thực hiện INSERT, DELETE và UPDATE cao
- CSDL tại publisher hoặc subscriber không phải là SQL server, ví dụ như Oracle

## 2. Các bước cấu hình transactional replication

Ở bài hướng dẫn này, `Vinahost` sẽ thực hiện cấu hình transactional replication trên 2 máy **Windows server 2012 R2 Datacenter** có cài đặt **SQL Server 2012 Enterprise**.

Để các bạn tiện theo dõi, server được dùng làm publisher là VINAHOST1, và subscriber là VINAHOST2.

### Tại publisher

- Nhấp chuột phải vào **Replication**, chọn **New -> Publication…**

![Replication](https://boxxv.github.io/img/2025/877ff2b246-vinahost-huong-dan-cau-hinh-transactional-replication-1.png "Replication")

- Ở bước **Publication Database**, ta chọn CSDL sẽ thực hiện nhân bản

![Replication](https://boxxv.github.io/img/2025/10acd4ebd8-vinahost-huong-dan-cau-hinh-transactional-replication-2.png "Replication")

- Ở bước **Publication Type**, ta chọn **Transactional publication**

![Replication](https://boxxv.github.io/img/2025/fb5d922c7f-vinahost-huong-dan-cau-hinh-transactional-replication-3.png "Replication")

- Ở bước **Articles**, ta chọn các bảng sẽ thực hiện nhân bản

![Replication](https://boxxv.github.io/img/2025/0ba39894a3-vinahost-huong-dan-cau-hinh-transactional-replication-4.png "Replication")

- Ở bước **Filter Table Rows**, ta có thể thêm các điều kiện lọc để loại bỏ các dòng không mong muốn ra khỏi bảng
- Ở bước **Snapshot Agent**, ta nhấp chọn **Create a snapshot immediately and keep the snapshot available to initialize supscriptions** để yêu cầu Snapshot agent tạo một bản snapshot ngay lập tức

![Replication](https://boxxv.github.io/img/2025/2d4f0c0beb-vinahost-huong-dan-cau-hinh-transactional-replication-5.png "Replication")

- Ở bước **Agent Security**, ta nhấp chọn **Security Settings…** và nhập tài khoản Windows sẽ dùng để chạy Snapshot agent

![Replication](https://boxxv.github.io/img/2025/b4f657c2ef-vinahost-huong-dan-cau-hinh-transactional-replication-6.png "Replication")

- Do ta để ô **Use the security settings from the Snapshot Agent** được chọn ở mặc định, nên Log Reader Agent cũng sẽ dùng tài khoản ở trên để chạy

![Replication](https://boxxv.github.io/img/2025/722f551eff-vinahost-huong-dan-cau-hinh-transactional-replication-7.png "Replication")

- Bước cuối cùng, ta đặt tên cho publication và bấm **Finish**

![Replication](https://boxxv.github.io/img/2025/12c865a1b0-vinahost-huong-dan-cau-hinh-transactional-replication-8.png "Replication")

Các bước không được liệt kê ở trên, ta giữ ở cấu hình mặc định

### Tại subscriber

- Nhấp chuột phải vào **Replication**, chọn **New -> Supscriptions…**

![Replication](https://boxxv.github.io/img/2025/8a88f13ad3-vinahost-huong-dan-cau-hinh-transactional-replication-9.png "Replication")

- Ở bước **Publication**, ta chọn publisher đã cấu hình ở trên, nếu không xuất hiện trong danh sách, ta chọn **<Find SQL Server Publisher…>** và kết nối tới publisher đã cấu hình từ trước

![Replication](https://boxxv.github.io/img/2025/88f3524e6a-vinahost-huong-dan-cau-hinh-transactional-replication-10.png "Replication")

- Ở bước **Subscribers**, ta chọn **<New database…>**

![Replication](https://boxxv.github.io/img/2025/ad5c4823ae-vinahost-huong-dan-cau-hinh-transactional-replication-11-1.png "Replication")

- Tại cửa sổ **New Database**, ta nhập tên của CSDL và bấm **OK**

![Replication](https://boxxv.github.io/img/2025/2f28dc37b0-vinahost-huong-dan-cau-hinh-transactional-replication-12.png "Replication")

- Ở bước Distribution Agent Security, ta nhập tài khoản sẽ dùng để chạy distribution agent

![Replication](https://boxxv.github.io/img/2025/3551fe04be-vinahost-huong-dan-cau-hinh-transactional-replication-13.png "Replication")

Các bước không được liệt kê ở trên, ta giữ ở cấu hình mặc định

Vậy là ta đã hoàn tất quá trình cấu hình Transactional replication trên Windows Server 2012.


# Cấu hình Merge Replication

## 1. Sơ nét về merge replication

Merge replication cho phép nhiều server làm việc độc lập (online hay ofline) sau đó hợp nhất dữ liệu đã thay đổi lại dựa vào độ ưu tiên, thời điểm chỉnh sửa hoặc do người dùng tự quy định. Subscriber sẽ đồng bộ với publisher khi được kết nối vào mạng và sẽ chuyển giao tất cả các row đã thực hiện thay đổi giữa publisher và subscriber kể từ lần đồng bộ cuối cùng.

Merge replication thường được dùng trong các trường hợp sau:

- Nhiều subscriber cập nhật cùng một dữ liệu nhiều lần và muốn phân phối những thay đổi đó tới publisher và các subscriber khác
- Subscriber có nhu cầu nhận dữ liệu, thay đổi dữ liệu offline, sau đó đồng bộ hóa những thay đổi tới publisher và các subscriber khác
- Mỗi subscriber yêu cầu một phân vùng dữ liệu khác nhau
- Có nhu cầu giải quyết xung đột khi chúng xảy ra
- Ứng dụng yêu cầu thay đổi dữ liệu lần cuối cùng thay vì dữ liệu tức thời. Ví dụ một row bị thay đổi 5 lần tại một subscriber trước khi đồng bộ tới publisher, vậy thì row đó sẽ chỉ thay đổi 1 lần tại publisher (tức là sẽ nhận giá trị thứ 5)

## 2. Các bước cấu hình merge replication

Ở bài hướng dẫn này, Vinahost sẽ thực hiện cấu hình merge replication trên 2 máy Windows server 2012 R2 Datacenter có cài đặt SQL Server 2012 Enterprise.

Để các bạn tiện theo dõi, server được dùng làm publisher là VINAHOST1, và subscriber là VINAHOST2.

### Tại publisher

- Nhấp chuột phải vào **Replication**, chọn **New -> Publication…**

![Replication](https://boxxv.github.io/img/2025/46a18605af-vinahost-huong-dan-cau-hinh-merge-replication-1.png "Replication")

- Ở bước **Publication Database**, ta chọn CSDL sẽ thực hiện nhân bản

![Replication](https://boxxv.github.io/img/2025/e56e00e322-vinahost-huong-dan-cau-hinh-merge-replication-2.png "Replication")

- Ở bước **Publication Type**, ta chọn **Merge publication**

![Replication](https://boxxv.github.io/img/2025/3bee33f842-vinahost-huong-dan-cau-hinh-merge-replication-3.png "Replication")

- Ở bước **Articles**, ta chọn các bảng sẽ thực hiện nhân bản

![Replication](https://boxxv.github.io/img/2025/f87636cc8d-vinahost-huong-dan-cau-hinh-merge-replication-4.png "Replication")

- Ở bước **Filter Table Rows**, ta có thể thêm các điều kiện lọc để loại bỏ các dòng không mong muốn ra khỏi bảng
- Ở bước **Agent Security**, ta nhấp chọn **Security Settings…** và nhập tài khoản Windows sẽ dùng để chạy Snapshot agent

![Replication](https://boxxv.github.io/img/2025/86954ff03c-vinahost-huong-dan-cau-hinh-merge-replication-5.png "Replication")

- Bước cuối cùng, ta đặt tên cho publication và bấm **Finish**

![Replication](https://boxxv.github.io/img/2025/5906ff93ee-vinahost-huong-dan-cau-hinh-merge-replication-6.png "Replication")

Các bước không được liệt kê ở trên, ta giữ ở cấu hình mặc định

### Tại subscriber

- Nhấp chuột phải vào **Replication**, chọn **New -> Supscriptions…**

![Replication](https://boxxv.github.io/img/2025/53027b0b42-vinahost-huong-dan-cau-hinh-merge-replication-7.png "Replication")

- Ở bước **Publication**, ta chọn publisher đã cấu hình ở trên, nếu không xuất hiện trong danh sách, ta chọn **<Find SQL Server Publisher…>** và kết nối tới publisher đã cấu hình từ trước

![Replication](https://boxxv.github.io/img/2025/6ad7571cba-vinahost-huong-dan-cau-hinh-merge-replication-8.png "Replication")

- Ở bước **Subscribers**, ta chọn **<New database…>**

![Replication](https://boxxv.github.io/img/2025/82e03dddd4-vinahost-huong-dan-cau-hinh-merge-replication-9.png "Replication")

- Tại cửa sổ **New Database**, ta nhập tên của CSDL và bấm **OK**

![Replication](https://boxxv.github.io/img/2025/9d66eaf3ce-vinahost-huong-dan-cau-hinh-merge-replication-10.png "Replication")

- Ở bước **Distribution Agent Security**, ta nhập tài khoản sẽ dùng để chạy distribution agent

![Replication](https://boxxv.github.io/img/2025/a3fc8b1885-vinahost-huong-dan-cau-hinh-merge-replication-11.png "Replication")

- Ở bước **Synchronization Schedule**, ta sửa Agent Schedule thành **Run continuously**

![Replication](https://boxxv.github.io/img/2025/d23e71915b-vinahost-huong-dan-cau-hinh-merge-replication-12.png "Replication")

Các bước không được liệt kê ở trên, ta giữ ở cấu hình mặc định

Vậy là ta đã hoàn tất quá trình cấu hình Merge replication trên Windows server 2012.

# Cấu hình Peer-to-Peer Replication

## 1. Sơ nét về peer-to-peer replication

Peer-to-peer replication cung cấp một giải phải có tính sẵn sàng cao và có khả năng mở rộng thông qua việc duy trì các bản sao của dữ liệu trên nhiều server (hay còn gọi là node). Được xây dựng dựa trên transactional, peer-to-peer replication thực hiện việc cập nhật các thay đối với tốc độ gần với thời gian thực.

Peer-to-peer replication thường được dùng trong các trường hợp sau:

- Chia tải các hành động truy vấn và đọc dữ liệu ra nhiều node, giúp tăng hiệu suất hoạt động và duy trì tính nhất quán khi nhu cầu đọc dữ liệu tăng
- Nếu một trong các node gặp sự cố, các node còn lại vẫn còn hoạt động và có thể đảm nhận chức năng của node gặp sự cố, giúp tăng tính sẵn sàng của hệ thống
- Nếu một node cần được bảo trì hoặc nâng cấp, node đó hoàn toàn có thể offline và được thêm trở lại vào hệ thống mà không bị ảnh hưởng tới tính sẵn sàng của ứng dụng

## 2. Các bước cấu hình transactional replication

Ở bài hướng dẫn này, Vinahost sẽ thực hiện cấu hình peer-to-peer replication trên 2 máy Windows server 2012 R2 Datacenter có cài đặt SQL Server 2012 Enterprise.

(Lưu ý: Peer-to-peer replication chỉ có thể được cài đặt trên SQL Server phiên bản Enterprise)

Trong mô hình peer-to-peer replication, các server vừa đóng vai trò là publisher, vừa là subscriber, nên ta thực hiện các bước chuẩn bị ở link sau ở cả 2 server

Để các bạn tiện theo dõi, các server được đặt tên lần lượt là VINAHOST1 và VINAHOST2. Cả 2 server đều phải có sẵn CSDL mà ta cần đồng bộ. Và việc cấu hình chỉ cần thực hiện trên 1 server

### Tại VINAHOST1

- Nhấp chuột phải vào **Replication**, chọn **New -> Publication…**

![Replication](https://boxxv.github.io/img/2025/226d2d4a03-vinahost-huong-dan-cau-hinh-peer-to-peer-replication-1.png "Replication")

- Ở bước **Publication Database**, ta chọn CSDL sẽ thực hiện nhân bản

![Replication](https://boxxv.github.io/img/2025/5ceb31c98a-vinahost-huong-dan-cau-hinh-peer-to-peer-replication-2.png "Replication")

- Ở bước **Publication Type**, ta chọn **Peer-to-Peer publication**

![Replication](https://boxxv.github.io/img/2025/8b7f9b7cf8-vinahost-huong-dan-cau-hinh-peer-to-peer-replication-3.png "Replication")

- Ở bước **Articles**, ta chọn các bảng sẽ thực hiện nhân bản

![Replication](https://boxxv.github.io/img/2025/905e11ea54-vinahost-huong-dan-cau-hinh-peer-to-peer-replication-4.png "Replication")

- Bước cuối cùng, ta đặt tên cho publication và bấm **Finish**

![Replication](https://boxxv.github.io/img/2025/c9e8a9787b-vinahost-huong-dan-cau-hinh-peer-to-peer-replication-5.png "Replication")

- Sau khi đã tạo xong publication, ta nhấp chuột phải vào publication vừa tạo, chọn **Configure Peer-To-Peer Topology…**

![Replication](https://boxxv.github.io/img/2025/8979f0008b-vinahost-huong-dan-cau-hinh-peer-to-peer-replication-6.png "Replication")

- Ở bước **Publication**, ta chọn publication ta vừa tạo khi nãy rồi bấm **Next**

![Replication](https://boxxv.github.io/img/2025/a7c4924119-vinahost-huong-dan-cau-hinh-peer-to-peer-replication-7.png "Replication")

- Ở bước **Configure Topology**, ta nhấp chuột phải vào một vùng bất kì, chọn **Add a New Peer Node**

![Replication](https://boxxv.github.io/img/2025/5f579ffbd5-vinahost-huong-dan-cau-hinh-peer-to-peer-replication-8.png "Replication")

### Tại VINAHOST2

- Tiếp theo, ta kết nối tới server thứ 2 (ở đây là VINAHOST2)

![Replication](https://boxxv.github.io/img/2025/0dab0c1feb-vinahost-huong-dan-cau-hinh-peer-to-peer-replication-9.png "Replication")

- Tại cửa sổ **Add a New Peer Node**, ta chọn CSDL sẽ đồng bộ, thay đổi **Peer Originator ID** (do ID 1 đã được sử dụng), và bấm vào dấu check **Connect to ALL displayed nodes** và để ở mặc định để node chuẩn bị thêm vào mô hình sẽ tự động kết nối với các node có sẵn

![Replication](https://boxxv.github.io/img/2025/106340e290-vinahost-huong-dan-cau-hinh-peer-to-peer-replication-10.png "Replication")

- Sau khi bấm **OK**, ta quay lại cửa sổ **Configure Peer-To-Peer Topology Wizard** và xác nhận rằng đã có 2 node trong mô hình và 2 node này đã kết nối với nhau. Ta tiếp tục bấm **Next**

![Replication](https://boxxv.github.io/img/2025/c5c9d29962-vinahost-huong-dan-cau-hinh-peer-to-peer-replication-11.png "Replication")

- Ở bước **Log Reader Agent Security**, ta nhập thông tin tài khoản sẽ dùng để chạy Log Reader Agent trên VINAHOST2 (node ta vừa thêm vào mô hình)

![Replication](https://boxxv.github.io/img/2025/0520da4dab-vinahost-huong-dan-cau-hinh-peer-to-peer-replication-12.png "Replication")

- Ở bước **Distribution Agent Security**, ta cũng thực hiện nhập thông tin tài khoản sẽ dùng để chạy Distribution Agent trên cả 2 node

![Replication](https://boxxv.github.io/img/2025/09fe301014-vinahost-huong-dan-cau-hinh-peer-to-peer-replication-13.png "Replication")

Các bước không được liệt kê ở trên, ta giữ ở cấu hình mặc định.

Vậy là ta đã hoàn tất quá trình cấu hình Peer-to-peer replication trên Windows server 2012.

# Kết luận

SQL Server Replication là một giải pháp mạnh mẽ giúp doanh nghiệp quản lý dữ liệu hiệu quả, nâng cao tính sẵn sàng và hiệu suất của hệ thống.

Chúc bạn thành công!


-----
Tham khảo:
- [Giới thiệu SQL Server Replication](https://blogs.nhquydev.net/sql-server/sql-server-replication/gioi-thieu-sql-server-replication)
- [Hướng dẫn cấu hình và quản lý SQL Server Replication với Distribution Agent](https://blogs.nhquydev.net/sql-server/sql-server-replication/huong-dan-cau-hinh-va-quan-ly-sql-server-replication-voi-distribution-agent)
- [[SQL Server] - Kỹ thuật Replication trong MS SQL Server | Học lập trình](https://youtu.be/K899pyz3z4U)
- [Cấu hình replication sql server – Phần 1](https://toiyeuit.com/cau-hinh-replication-sql-server-p1/)
- []()
- [Tăng performance của SQL Database với replication [Phần 1]](https://viblo.asia/p/tang-performance-cua-sql-database-voi-replication-phan-1-aNj4vxlOL6r)
- [Tăng performance của SQL Database với replication [Phần 2]](https://viblo.asia/p/tang-performance-cua-sql-database-voi-replication-phan-2-y37LdvMg4ov)
- []()
- [Giới thiệu SQL server replication](https://blog.vinahost.vn/gioi-thieu-sql-server-replication/)
- [Các bước chuẩn bị trước khi cấu hình replication](https://vinahost.info/cac-buoc-chuan-bi-truoc-khi-cau-hinh-replication)
- [Hướng dẫn cấu hình transactional replication](https://blog.vinahost.vn/huong-dan-cau-hinh-transactional-replication/)
- [Hướng dẫn cấu hình merge replication](https://blog.vinahost.vn/huong-dan-cau-hinh-merge-replication/)
- [Hướng dẫn cấu hình peer-to-peer replication](https://blog.vinahost.vn/huong-dan-cau-hinh-peer-to-peer-replication/)
- [Nhân bản và đồng bộ dữ liệu với SQL Server](https://r2s.edu.vn/nhan-ban-va-dong-bo-du-lieu-voi-sql-server/)
- []()
- [SQL Server Replication](https://learn.microsoft.com/en-us/sql/relational-databases/replication/sql-server-replication)

https://www.sql.edu.vn/microsoft-sql-server/replication/

https://bartoszlewandowski.blog/tag/sql-server-repl/

https://www.mssqltips.com/sqlservertip/3287/sql-server-transactional-replication-error-could-not-find-stored-procedure-error-and-how-to-recover-it-by-using-spscriptpublicationcustomprocs/

https://learn.microsoft.com/en-us/sql/relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated

https://sqlserver-dba.co.uk/sql-server/sql-server-error-14151-severity-18-replication-s-agen.html