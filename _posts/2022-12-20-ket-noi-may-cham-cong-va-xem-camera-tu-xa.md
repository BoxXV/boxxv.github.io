---
layout: post
title: Kết nối máy chấm công và xem camera từ xa
subtitle: Giải pháp chấm công đa điểm qua mạng internet
image: "img/projects-bg.jpg"
tags:
- máy chấm công
- camera
- attendance machine
- timekeeper
---

![Chấm công đa điểm](https://boxxv.github.io/img/timekeeper/mo-hinh-hoat-dong-ket-noi-thiet-bi-f18.png "Chấm công đa điểm")

Hiện nay nhu cầu lấy dữ liệu chấm công từ xa qua mạng internet từ máy chấm công vân tay là hết sức cần thiết đối mỗi doanh nghiệp tại Việt Nam. Sau đây là các cách lấy dữ liệu chấm từ xa qua mạng thông dụng nhất hiện nay.

## I. Tổng quan

### 1. Lấy dữ liệu chấm công online server

Đối với cách lấy dữ liệu chấm công online server là giải pháp chấm công tiên tiến nhất hiện nay tiết kiệm chi phí và đem lại khá nhiều hiệu quả cho doanh nghiệp muốn quản lý dữ liệu tập trung về văn phòng trung tâm.

Yêu cầu giải pháp chỉ cần 1 IP tĩnh hoặc 1 tên miền tại văn phòng trung tâm nơi nhận dữ liệu chấm công.

`Ưu điểm`:
- Không mở port máy chấm công vân tay chúng có sử máy chấm công vân tay kết 3g, 4g, wifi  miễn sao có internet.
- Quản lý chấm công nhân viên trực tuyến theo thời gian thực dữ liệu tự động tải về server.
- Quản lý nhân viên mọi nơi mọi lúc bằng thiết bị di động như điện thoại hoặc máy tính bảng.
- Tại các chi nhánh nơi lắp máy chấm công vân tay không cần cài phần mềm chấm công.
- Thông báo trình máy chấm công có đang kết nối máy tính hay không.
- Chỉ cần 1 tên miền hoặc 1 IP tĩnh dùng được cho tất cả các máy chấm công.

`Nhược điểm`: chỉ áp dụng cho những dòng máy chấm công có chức năng cloud server.

Khác với những phương pháp chấm công mà trước đây nhiều doanh nghiệp vẫn sử dụng như nhân viên chấm công hàng ngày, tới cuối tháng thì bộ phận nhân sự sẽ copy ra và tính toán một cách vất vả cũng như không quản lý được nhân viên trực tiếp. Nếu như muốn lấy dữ liệu thì lại phải mở port của máy chấm công tại chi nhánh làm tốn không ít chi phí cũng như gây khó khăn cho việc bảo trì và còn phải sử dụng tên miền. Vậy khác với phương pháp này, chấm công online với thật nhiều ưu điểm vượt trội.

- Quản lý chấm công online giúp bộ phận nhân sự có thể xem chấm công ngay lập tức khi nhân viên chấm công tại các chi nhánh. Dữ liệu load theo kiểu online trực tuyến
- Quản lý máy chấm công và các chức năng  thêm hoặc xóa, sửa… hay luân chuyển nhân viên từ nơi này sang nơi khác và bộ phận nhân sự chỉ cần ngồi tại văn phòng và thực hiện các thao tác.
- Giúp báo cáo nhân viên đi sớm, về muộn, hay đi làm trễ hoặc về sớm và vắng mặt.
- Nhân viên có thể tự quản lý chấm công của mình tại các máy tính đặt ở các chi nhánh


Máy chấm công hỗ trợ truy xuất dữ liệu online từ xa (cloud server)
- Zkteco K14 - 1.899.000₫
- Ronald Jack T8 - 2.399.000₫
- Ronald Jack X628pro - 2.999.000₫
- Ronald Jack 4000TID-C - 3.399.000₫
.v.v.

![Chấm công đa điểm](https://boxxv.github.io/img/timekeeper/giai-phap-cham-cong-nhieu-diem.jpg "Chấm công đa điểm")


### 2. Mở port modem ADSL tại chi nhánh lấp máy chấm công

`Ưu điểm`: dùng được cho tất cả các loại máy chấm công.

`Nhược điểm`:
- Vị trí lắp máy chấm công phải có đường truyền internet ADSL
- Phải sử dụng rất nhiều tên miền hoặc IP tĩnh, mỗi máy chấm công là 1 tên miền hoặc 1 ip tĩnh tốn chi phí cao khó bảo trì
- Bảo mật kém, Việc mở port 4370 trên modem để lấy dữ liệu từ xa được ví như chúng ta đưa chìa khóa cho trộm vào nhà.

Để khắc phục các lỗ hổng này, các tổ chức nên quy hoạch
1. Không cho phép các kết nối Internet Incoming và Outgoing cho thiết bị này với port 4370 được open trên Modem.
2. Sử dụng giải pháp cloud mà AZZA cung cấp, khách hàng không phải mở bất kỳ port nào trên modem hoặc thay đổi cấu hình bảo mật mạng vẫn có thể lấy dữ liệu từ xa thông qua phương thức get/post đã được mã hóa.


### 3. Dùng phần mềm chấm công Ronald Jack Server cài ở máy chủ

`Ưu điểm`: dùng được cho tất cả các loại máy chấm công.

`Nhược điểm`: phải cài phần mềm chấm công lên máy tính tại các chi nhánh nơi lắp đặt máy chấm công vân tay, nhân viên ở tại chi nhánh tự thực hiện tải dữ liệu chấm công về văn phòng trung tâm. Không quản lý nhân viên trực tiếp, bảo mật kém,…

### 4. Lấy dữ liệu chấm công qua USB.

`Ưu điểm`: dùng được cho tất cả các loại máy chấm công.
`Nhược điểm`: thao tác thủ công, bảo mật kém, không quản lý chấm công nhân viên trực tiếp.


## II. Giải pháp chấm công đa điểm qua mạng di động 3G/4G

Công nghệ Internet 3G không còn quá xa lạ với mọi người. Ngày nay công nghệ Internet 3G không chỉ nhanh hơn mà giá thành đã rẻ hơn rất nhiều. Internet 3G thường được ứng dụng trong các thiết bị di động như smartphone, ipad, hoặc laptop,…. Ngoài ra, Internet 3G còn có thể chạy được với những thiết bị mạng router để cung cấp Internet cho những nơi không thể kéo cáp. Internet 3G được sử dụng nhiều trong các phương tiện vận tải để phát Wi-Fi cho hành khách sử dụng.

Với những doanh nghiệp đang tìm kiếm giải pháp để quản lí, giám sát bằng hình ảnh trên những phương tiện thường xuyên di chuyển như xe khách, xe chở hàng, xà lang,…hay các công trường, láng trại; Và nơi đó tất nhiên không thể lắp internet cố định được. Truyền dẫn bằng internet 3G là giải pháp tối ưu nhất.

Một khó khăn không nhỏ khi triển khai giải pháp này là do các ISP chỉ cung cấp địa chỉ IP private cho internet 3G (IP sau NAT device) nên ta không thể nào xem trực tiếp hình ảnh từ Máy Chấm Công / Camera bằng các mở port truyền thống được. Có giải pháp nào cho vấn đề này?

DrayTek đã đưa ra giải pháp để khắc phục vấn đề này bằng cách tạo một đường hầm VPN (Virtual Private network) và cho phép “Mở port thông qua đường hầm VPN”.

![Chấm công đa điểm](https://boxxv.github.io/img/timekeeper/so-do-ket-noi-may-cham-cong-va-camera-qua-internet-mang-3g.png "Chấm công đa điểm")_Sơ đồ kết nối máy chấm công và xem Máy Chấm Công / Camera từ xa qua mạng Internet 3G_

**Bước 1**: Tạo kết nối VPN LAN-to-LAN giữa Site Trung tâm và Site 3G (Có thể sử dụng IPSec / PPTP / SSL)

**Bước 2**: Mở port từ Site Trung tâm về Máy Chấm Công / Camera tại Site 3G thông qua đường hầm VPN

**Bước 3**: Người dùng xem Máy Chấm Công / Camera bằng IP WAN của Trung tâm + Port vừa mở (Hoặc DDNS)

**Để triển khai giải pháp trên chúng ta cần chuẩn bị và hiểu rõ các vấn đề sau:**

**Site Trung Tâm**: Có thể là Văn phòng CTY, nhà riêng,..Nơi có internet truyền thống (ADSL, cáp quang)
- Thiết bị Sử dụng Vigor2860, Vigor2925, Vigor2960 hoặcVigor3900 (Hỗ trợ “Mở port thông qua đường hầm VPN”)
- Internet: Cáp quang hoặc ADLS

**Site 3G**:
- Thiết bị: Những model hỗ trợ cổng USB cho 3G và VPN như Vigor2912/ V2860 / V2925 / V2920 / V2910
- Internet: Sử dụng các USB 3G tương thích với các model trên.

> Chúng ta không mở port trực tiếp từ Site 3G mà mở port từ Site Trung tâm về Máy Chấm Công / Camera tại Site 3G thông qua đường hầm VPN

**Ưu điểm**:
- Khi đã triển khai, chỉ cần bạn ở nơi có internet là bạn có thể truy cập được dữ liệu, xem Máy Chấm Công / Camera,…
- Triển khai được Máy Chấm Công / Camera ở những nơi chỉ có internet 3G
- Không lệ thuộc vào các dịch vụ Máy Chấm Công / Camera Cloud của bên thứ 3
- Triển khai được với tất cả các loại Máy Chấm Công / Camera (IP / Analog)
- Bảo mật cao do dữ liệu hình ảnh được truyền trên kênh tuyền riêng được mã hóa
- Ít tốn dung lượng 3G do hình ảnh được lưu tại đầu ghi và chỉ tốn dung lượng 3G khi bạn xem trực tuyến

**Nhược điểm**:
- Phải trang bị đồng bộ thiết bị VPN DrayTek hoặc Atrie
- Chất lượng hình ảnh khi xem trực tuyến phụ thuộc vào tốc độ 3G và chất lượng internet tại trung tâm
- Chi phí 3G hàng tháng còn cao (Khoảng 200.000/tháng)
- Người quản trị (triển khai) hệ thống nên có kiến thức cơ bản về mạng

### Hướng dẫn cấu hình:

**Bước 1**: Tạo kết nối VPN lan to lan giữa site trung tâm và site 3G
- Bạn có thể tham khảo các Hướng dẫn VPN LAN-to-LAN giữa Site Trung tâm và Site 3G (V2960/V3900  vs V2912)

**Bước 2**: Thực hiện mở port xem Máy Chấm Công / Camera qua đường hầm VPN từ Site Trung tâm về IP Máy Chấm Công / Camera tại Site 3G

- Trên Vigor2960/3900: Vào **Nat** >>> **Port Redirection**
- Tạo **Profile Nat**
	+ Profile: Đặt tên cho profile Nat
	+ Chọn **Enable**
	+ Port Redirection Mode: Chọn **One to one**
	+ Protocol: Chọn **TCP/UDP**
	+ Private IP: Điền địa chỉ IP của Máy Chấm Công / Camera bên Site 3G
	+ Private Port: Điền port để xem Máy Chấm Công / Camera
	+ Public port: Điền port để xem Máy Chấm Công / Camera
	+ Nếu Máy Chấm Công / Camera cần nhiều port để xem, bạn có thể add thêm bằng cách Click nút Add ở More port và add thêm port
	+ Nhấn **Apply**

Sau khi thực hiện xong hai bước trên bạn có thể sử dụng điện thoại hoặc laptop truy cập Máy Chấm Công / Camera ở bất kì nơi đâu có internet bằng IP wan của Site Trung tâm và port Máy Chấm Công / Camera vừa mở

-----
Tham khảo:

- [Giải pháp kết nối máy chấm công và xem camera từ xa qua mạng Internet 3G](https://dienmayvanphong.com/giai-phap-ket-noi-may-cham-cong-va-xem-camera-tu-xa-qua-mang-internet-3g/)
- [Hướng dẫn cách lấy dữ liệu máy chấm công từ xa](https://tft.vn/du-lieu-may-cham-cong-tu-xa)
- [Rủi ro từ lỗ hổng máy chấm công khi lấy dữ liệu từ xa qua public IP wan và NAT Port](https://azza.vn/rui-ro-tu-lo-hong-may-cham-cong-khi-lay-du-lieu-tu-xa-qua-public-ip-wan-va-nat-port/)
- [Giải pháp kết nối máy chấm công và xem camera từ xa qua mạng Internet 3G](https://dienmayvanphong.com/giai-phap-ket-noi-may-cham-cong-va-xem-camera-tu-xa-qua-mang-internet-3g/)
