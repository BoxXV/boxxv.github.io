---
layout: post
title: Bộ cài đặt tốt nhất cho máy Windows
subtitle: Best installers for Windows machine
image: "img/2024/1277070923.png"
tags:
- Mạt Code
- lập trình
---

## Mục lục

- [Mục lục](#mục-lục)
- [Tâm sự cùng AI](#tâm-sự-cùng-ai)
- [Wix](#wix)
- [Inno Setup](#inno-setup)
- [NSIS](#nsis)
- [MS Visual Studio Installer Projects](#ms-visual-studio-installer-projects)
- [Kết luận](#kết-luận)


## Tâm sự cùng AI

`Người dùng bình thường`: Best installers for Windows machine

`Claude-3-Sonnet`: Khi cài đặt phần mềm trên máy tính Windows, có một số tùy chọn trình cài đặt phổ biến sau đây:

1. [**MSI (Microsoft Installer)**](https://learn.microsoft.com/en-us/windows/win32/msi/windows-installer-portal): MSI là một định dạng gói cài đặt phần mềm và dịch vụ được Microsoft phát triển. Đây là định dạng được khuyến nghị để cài đặt ứng dụng trên hệ thống Windows, vì nó cung cấp trải nghiệm cài đặt nhất quán và đáng tin cậy. Các gói MSI có thể được tùy chỉnh và triển khai thông qua các phương thức khác nhau, bao gồm cài đặt cục bộ, triển khai qua mạng hoặc các công cụ phân phối phần mềm như System Center Configuration Manager (SCCM) hoặc Microsoft Endpoint Manager.
2. [**NSIS (Nullsoft Scriptable Install System)**](https://nsis.sourceforge.io/Main_Page): NSIS là một hệ thống cài đặt mã nguồn mở miễn phí dựa trên kịch bản cho Windows. Nó nhẹ, có khả năng tùy chỉnh cao và hỗ trợ nhiều tính năng như nén, hỗ trợ đa ngôn ngữ và cài đặt im lặng. NSIS thường được sử dụng bởi các nhà phát triển và nhà cung cấp phần mềm để phân phối ứng dụng của họ.
3. [**Inno Setup**](https://jrsoftware.org/isinfo.php): Inno Setup là một trình cài đặt miễn phí khác phổ biến cho Windows. Nó nổi tiếng với giao diện thân thiện, khả năng lập trình kịch bản và hỗ trợ các tính năng hiện đại của Windows như UAC (User Account Control) và ký mã. Inno Setup thường được sử dụng cho các dự án nguồn mở và các nhà cung cấp phần mềm nhỏ.
4. [**WiX (Windows Installer XML)**](https://wixtoolset.org): WiX là một bộ công cụ để xây dựng các gói Windows Installer từ mã nguồn XML. Nó đặc biệt hữu ích để tạo các cài đặt tùy chỉnh cao và phức tạp, đặc biệt là cho phần mềm doanh nghiệp. WiX thường được sử dụng bởi các công ty phần mềm lớn và các tổ chức.
5. [**InstallShield**](https://www.revenera.com/install/products/installshield) và [**Advanced Installer**](https://www.advancedinstaller.com): Đây là các công cụ tạo trình cài đặt thương mại cung cấp một suite tính năng toàn diện để tạo trình cài đặt cho ứng dụng Windows. Chúng cung cấp giao diện thân thiện, tùy chọn tùy chỉnh nâng cao và hỗ trợ cho các kịch bản cài đặt khác nhau. Các công cụ này thường được sử dụng bởi các nhà cung cấp phần mềm và doanh nghiệp yêu cầu khả năng cài đặt nâng cao và hỗ trợ.
6. **Ứng dụng Portable**: Ngoài các trình cài đặt truyền thống, nhiều ứng dụng cho Windows cũng có sẵn ở định dạng "di động". Ứng dụng di động không cần cài đặt và có thể chạy trực tiếp từ ổ USB hoặc thư mục cục bộ, làm cho chúng thuận tiện cho người dùng cần chạy ứng dụng trên nhiều máy hoặc có quyền cài đặt hạn chế.

Việc lựa chọn trình cài đặt thường phụ thuộc vào các yếu tố như mức độ phức tạp của ứng dụng, đối tượng khách hàng mục tiêu và các yêu cầu triển khai. Cuối cùng, trình cài đặt tốt nhất cho máy tính Windows sẽ phụ thuộc vào nhu cầu cụ thể và sở thích của nhà cung cấp phần mềm hoặc tổ chức triển khai ứng dụng.

## [Wix](https://wixtoolset.org)

WiX Toolset (Windows Installer XML Toolset) là một bộ công cụ mã nguồn mở được sử dụng để tạo ra các gói cài đặt phần mềm cho hệ điều hành Windows. WiX sử dụng XML để định nghĩa cấu hình và các thành phần của gói cài đặt. Dưới đây là một số điểm chính về WiX Toolset:

![Wix](https://learn.microsoft.com/en-us/dotnet/core/extensions/media/workers/new-wix-setup-project.png "Wix")

`HeatWave` là tiện ích mở rộng Visual Studio của `FireGiant` dành cho **WiX v4, v5** và phiên bản mới hơn. Phiên bản Cộng đồng HeatWave được cung cấp miễn phí và cung cấp:

Download [HeatWave for Visual Studio 2022 here](https://marketplace.visualstudio.com/items?itemName=FireGiant.FireGiantHeatWaveDev17).
Download [HeatWave for Visual Studio 2019 here](https://marketplace.visualstudio.com/items?itemName=FireGiant.FireGiantHeatWaveDev16).

- Mã nguồn mở: WiX là một dự án mã nguồn mở, điều này có nghĩa là nó miễn phí và có thể được cộng đồng phát triển và cải tiến.
- Ngôn ngữ XML: WiX sử dụng ngôn ngữ XML để mô tả cấu trúc và các thành phần của gói cài đặt. Điều này cho phép các nhà phát triển dễ dàng quản lý và tùy chỉnh các tệp cài đặt của họ.
- Hỗ trợ đầy đủ cho MSI: WiX hỗ trợ việc tạo ra các gói cài đặt MSI (Microsoft Installer), MSM (Merge Module) và MSP (Patch).
- Tích hợp với Visual Studio: WiX có thể tích hợp tốt với Microsoft Visual Studio, cho phép các nhà phát triển tạo và quản lý các dự án cài đặt trực tiếp từ môi trường phát triển.
- Tính linh hoạt cao: Với WiX, bạn có thể tạo ra các gói cài đặt phức tạp với nhiều điều kiện, quy tắc và tùy chọn cài đặt khác nhau.
- Cộng đồng và Tài liệu: WiX có một cộng đồng lớn và nhiều tài liệu hướng dẫn, giúp người dùng dễ dàng tìm hiểu và giải quyết các vấn đề khi sử dụng.
- Sử dụng rộng rãi: WiX Toolset được sử dụng rộng rãi trong cả cộng đồng mã nguồn mở và doanh nghiệp, đặc biệt là tại Microsoft, nơi nhiều sản phẩm chính thức sử dụng WiX để tạo các gói cài đặt.

WiX Toolset thường được sử dụng bởi các nhà phát triển phần mềm chuyên nghiệp để tạo ra các bộ cài đặt tiêu chuẩn và chất lượng cao cho ứng dụng Windows của họ.

## [Inno Setup](https://jrsoftware.org/isinfo.php)

INNO SETUP là một trong những công cụ đáng để bạn lựa chọn vì sự chuyên nghiệp của nó và hơn nữa là hoàn toàn miễn phí.

![Inno Setup](https://jrsoftware.org/images/is-ide-dark.png "Inno Setup")

- Hỗ trợ cho mọi bản phát hành Windows kể từ năm 2006, bao gồm: Windows 11, Windows 10, Windows 11 trên Arm, Windows 10 trên Arm, Windows Server 2019, Windows Server 2016, Windows 8.1, Windows 8, Windows Server 2012, Windows 7 và Windows Server 2008 R2. (Không cần gói dịch vụ.)
- Hỗ trợ mở rộng để cài đặt các ứng dụng 64 bit trên phiên bản Windows 64 bit. Các kiến ​​trúc x64, ARM64 và Itanium đều được hỗ trợ.
- Hỗ trợ mở rộng cho cả cài đặt quản trị và phi hành chính.
- Hỗ trợ tạo một EXE duy nhất để cài đặt chương trình của bạn nhằm phân phối trực tuyến dễ dàng. Mở rộng đĩa cũng được hỗ trợ.
- Giao diện thuật sĩ Windows tiêu chuẩn.
- Các loại thiết lập có thể tùy chỉnh, ví dụ: Đầy đủ, tối thiểu, tùy chỉnh.
- Hoàn thành khả năng `gỡ cài đặt`.
- Cài đặt các tập tin:
  + Bao gồm hỗ trợ tích hợp cho nén tệp "deflate", bzip2 và 7-Zip LZMA/LZMA2. Trình cài đặt có khả năng so sánh thông tin phiên bản tệp, thay thế các tệp đang sử dụng, sử dụng tính năng đếm tệp được chia sẻ, đăng ký thư viện loại và DLL/OCX cũng như cài đặt phông chữ.
- Tạo lối tắt ở mọi nơi, kể cả trong Start Menu và trên màn hình nền.
- Tạo các mục đăng ký và .INI.
- Chạy các chương trình khác trước, trong hoặc sau khi cài đặt.
- Hỗ trợ cài đặt đa ngôn ngữ, bao gồm hỗ trợ ngôn ngữ từ phải sang trái.
- Hỗ trợ cài đặt bằng mật khẩu và mã hóa.
- Hỗ trợ cài đặt và gỡ cài đặt được ký điện tử, bao gồm ký kép (SHA1 & SHA256).
- Cài đặt và gỡ cài đặt im lặng.
- Cài đặt Unicode.
- Tùy chọn tiền xử lý tích hợp để tùy chỉnh thời gian biên dịch nâng cao.
- Tùy chọn công cụ tập lệnh Pascal tích hợp để tùy chỉnh cài đặt và gỡ cài đặt trong thời gian chạy nâng cao.
- Mã nguồn đầy đủ có sẵn từ [GitHub](https://github.com/jrsoftware/issrc).
- Dấu chân nhỏ: chi phí chỉ khoảng 1,5 mB với tất cả các tính năng được bao gồm.
- Tất cả các tính năng đều được [ghi chép đầy đủ](https://jrsoftware.org/ishelp.php).
- Được sử dụng bởi [Microsoft Visual Studio Code](https://code.visualstudio.com/) và [Embarcardero Delphi](https://www.embarcadero.com/products/delphi).

## [NSIS]((https://nsis.sourceforge.io/Main_Page))

Giới thiệu sơ qua về NSIS (Nullsoft Scriptable Install System) được phát triển bởi Nullsoft (cha đẻ của Winamp) phát hành lần đầu vào năm 2002. Đây là phần mềm tạo ra trình cài đặt dựa trên script-driven dành cho Microsoft Windows và được hỗ trợ bởi Nullsoft. Nó được nhiều công ty lớn sử dụng như Google, Ubisoft, McAfee, v.v.

NSIS có thể tạo các trình cài đặt Windows có khả năng cài đặt, gỡ cài đặt, thiết lập cài đặt hệ thống, giải nén tệp, v.v. Vì NSIS dựa trên các tệp tập lệnh nên bạn có thể tạo cả trình cài đặt đơn giản và nâng cao.

![NSIS](https://nsis.sourceforge.io/mediawiki/images/d/dd/NSISScreenshot3.png "NSIS")

- Kích thước overhead nhỏ
- Tương thích với tất cả các phiên bản Windows chính
- Phương pháp nén độc đáo
- Dựa trên kịch bản
- Nhiều ngôn ngữ trong một trình cài đặt
- Nhiều tính năng và kiểm tra hệ thống mục tiêu
- Hộp thoại và giao diện tùy chỉnh
- Hệ thống Plug-in
- Hỗ trợ cài đặt web, file patching
- Tích hợp dự án, các bản phát hành khác nhau và bản dựng tự động
- Các định dạng tệp dễ đọc
- Trình biên dịch Portable

Danh sách tính năng lớn hơn

- Tạo trình cài đặt thực thi độc lập
- Hỗ trợ nén dữ liệu ZLib, BZip2 và LZMA (các tệp có thể được nén riêng lẻ hoặc cùng nhau)
- Hỗ trợ gỡ cài đặt (trình cài đặt có thể tạo trình gỡ cài đặt)
- Giao diện người dùng có thể tùy chỉnh (hộp thoại, phông chữ, hình nền, biểu tượng, văn bản, dấu kiểm, hình ảnh, v.v.)
- Giao diện thuật sĩ cổ điển và hiện đại
- Hoàn toàn đa ngôn ngữ, hỗ trợ nhiều ngôn ngữ (bao gồm cả ngôn ngữ RTL) trong một trình cài đặt. Hơn 40 bản dịch đã có sẵn nhưng bạn cũng có thể tạo bản dịch của riêng mình.
- Hệ thống trang: Bạn có thể thêm các trang hướng dẫn tiêu chuẩn hoặc các trang tùy chỉnh
- Người dùng lựa chọn các thành phần cài đặt, cây lựa chọn thành phần
- Nhiều cấu hình cài đặt (thường là Tối thiểu, Điển hình, Đầy đủ) và cấu hình tùy chỉnh
- Tự xác minh trình cài đặt bằng tổng kiểm tra CRC32
- Chi phí nhỏ so với kích thước dữ liệu nén (34 KB với các tùy chọn mặc định)
- Khả năng hiển thị thỏa thuận cấp phép ở định dạng văn bản hoặc RTF
- Khả năng phát hiện thư mục đích từ sổ đăng ký
- Hệ thống plug-in dễ sử dụng (bao gồm rất nhiều plug-in để tạo hộp thoại tùy chỉnh, kết nối internet, tải xuống HTTP, vá tệp, gọi API Win32, v.v.)
- Trình cài đặt có thể lớn tới 2GB
- Chế độ im lặng tùy chọn để cài đặt tự động
- Bộ tiền xử lý có hỗ trợ các ký hiệu, macro được xác định, biên dịch có điều kiện, tiền xác định tiêu chuẩn
- Trải nghiệm mã hóa thú vị với các thành phần PHP và tập hợp (bao gồm các biến người dùng, ngăn xếp, kiểm soát luồng thực, v.v.)
- Trình cài đặt có máy ảo riêng cho phép bạn viết mã có thể hỗ trợ:
	+ Trích xuất tệp (với các tham số ghi đè có thể định cấu hình)
	+ Sao chép tập tin/thư mục, đổi tên, xóa, tìm kiếm
	+ Cuộc gọi DLL plug-in
	+ Đăng ký/hủy đăng ký kiểm soát DLL/ActiveX
	+ Thực thi có thể thực thi (tùy chọn thực thi và chờ shell)
	+ Tạo lối tắt
	+ Đọc/cài đặt/liệt kê/xóa khóa đăng ký
	+ Đọc/ghi tệp INI
	+ Đọc/ghi tệp văn bản chung
	+ Thao tác chuỗi và số nguyên mạnh mẽ
	+ Tìm cửa sổ dựa trên tên lớp hoặc tiêu đề
	+ Thao tác giao diện người dùng (cài đặt phông chữ/văn bản)
	+ Gửi tin nhắn cửa sổ
	+ Tương tác của người dùng với hộp thông báo hoặc trang tùy chỉnh
	+ Phân nhánh, so sánh, v.v.
	+ Kiểm tra lỗi
	+ Hỗ trợ khởi động lại, bao gồm xóa hoặc đổi tên khi khởi động lại
	+ Các lệnh hành vi của trình cài đặt (chẳng hạn như hiển thị/ẩn/chờ/v.v.)
	+ Chức năng người dùng trong tập lệnh
	+ Chức năng gọi lại cho hành động của người dùng
- Hoàn toàn miễn phí cho mọi mục đích sử dụng. Xem [Giấy phép](https://nsis.sourceforge.io/License).
- Và nhiều hơn nữa

## MS Visual Studio Installer Projects

Các dự án trình cài đặt (.vdproj) cho các phiên bản hiện tại của Visual Studio yêu cầu bạn cài đặt tiện ích mở rộng.

Dành cho VS2022: [Microsoft Visual Studio Installer Projects 2022](https://marketplace.visualstudio.com/items?itemName=VisualStudioClient.MicrosoftVisualStudio2022InstallerProjects)  
Dành cho VS2017 và VS2019: [Microsoft Visual Studio Installer Projects](https://marketplace.visualstudio.com/items?itemName=visualstudioclient.MicrosoftVisualStudio2017InstallerProjects)

![Microsoft Visual Studio Installer](https://lukhezo.com/wp-content/uploads/2015/01/setup.png "Microsoft Visual Studio Installer")

## Kết luận

[`vdproj`](https://learn.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2010/2kt85ked(v%3dvs.100)), [`Wix`](https://wixtoolset.org/), [`Install Shield`](https://www.revenera.com/install/products/installshield) tất cả đều tạo file MSI.

[`Inno Setup`](https://jrsoftware.org/isinfo.php), [`NSIS`](https://nsis.sourceforge.io/Main_Page), [`Squirrel`](https://github.com/Squirrel/Squirrel.Windows) có hệ thống riêng.

Wix gần như là tiêu chuẩn và đối với một dự án đơn giản thì không quá khó.

Advanced Installer có [phiên bản miễn phí](https://www.advancedinstaller.com/user-guide/create-msi-package-video-tutorial.html) và phiên bản trả phí có nhiều tính năng hơn, tạo cơ sở dữ liệu trình cài đặt MSI tiêu chuẩn và IMO rất dễ sử dụng. Tôi đã sử dụng nó cách đây vài năm cho một dự án thương mại tại nơi làm việc và chắc chắn sẽ sử dụng lại nó. Cấu hình trình cài đặt được lưu trữ dưới dạng tệp XML và rất dễ tùy chỉnh bằng cách sử dụng các bước xây dựng tùy chỉnh.

-----
- [Best installers for Windows machine](https://www.reddit.com/r/csharp/comments/b49son/best_installers_for_windows_machine/)
- [Installers: WIX or Inno Setup?](https://stackoverflow.com/questions/6245260/installers-wix-or-inno-setup)
- [WiX ToolSet là cái gì?](https://mn.com.vn/hoc-net/wix-toolset-la-cai-gi/)
- [Inno Setup](https://jrsoftware.org/isinfo.php)
- [Đóng gói, tạo file exe bằng Inno Setup](https://thuthuat.taimienphi.vn/dong-goi-tao-file-exe-bang-inno-setup-2084n.aspx)
- [Hướng dẫn đóng gói chương trình chuyên nghiệp với INNO SETUP](https://nguyenduydai.wordpress.com/2013/11/09/huong-dan-dong-goi-phan-mem-chuyen-nghiep-voi-inno-setup/)
- [Việt hóa inno setup](https://innosetup03.wordpress.com/viet-hoa-inno-setup/)
- [Hướng dẫn đóng gói phần mềm với NSIS (Nullsoft Scriptable Install System)](https://trungnhan.name.vn/huong-dan-dong-goi-phan-mem-voi-nsis-nullsoft-scriptable-install-system/)
- [UserBenchmark bị hiểu lầm là phần mềm độc hại](https://thanhnien.vn/userbenchmark-bi-hieu-lam-la-phan-mem-doc-hai-1851404092.htm)
- [How to Create A Windows Installer for Dynamsoft Service and .NET Document Scanner Application](https://dev.to/yushulx/how-to-create-a-windows-installer-for-dynamsoft-service-and-net-document-scanner-application-1mhp)
- [3 cách tạo File cài đặt EXE đơn giản không cần lập trình 2024](https://anonyviet.com/3-cach-tao-file-cai-dat-exe-don-gian-khong-can-lap-trinh/)
- [Đóng gói ứng dụng ngay trong phiên bản Visual Studio 2019](https://youtu.be/v26TVMtPHlI)
- [Cách đóng gói code Project thành file EXE bằng MS Visual Studio](https://blogchiasekienthuc.com/thu-thuat-hay/cach-dong-goi-code-project-thanh-file-exe.html)
- [Create a User's Desktop Shortcut and User's Program Menu by using VS setup and Deployment Project - Step by Step](https://www.dotnetfunda.com/articles/show/2334/create-a-user39s-desktop-shortcut-and-user39s-program-menu-by-using-vs)
- [Microsoft Visual Studio Installer Projects 2022](https://marketplace.visualstudio.com/items?itemName=VisualStudioClient.MicrosoftVisualStudio2022InstallerProjects)
- [Visual Studio Installer Deployment](https://learn.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2010/2kt85ked(v%3dvs.100))

-----
- [How to create Setup file for Windows Service](https://youtu.be/86Y9WhQc4TQ)
- [Create a Windows Service installer](https://learn.microsoft.com/en-us/dotnet/core/extensions/windows-service-with-installer?tabs=wix)
- [C# - How to Create a Setup Project to Deploy Windows Services - Part 3/3](https://youtu.be/cp2aFNtcZfk?list=PLt2cGgt6G8WrItA7KTI5m6EFniMfphWJC)
- [Create Simple Windows Service And Setup Project With Installation](https://www.c-sharpcorner.com/UploadFile/b7531b/create-simple-window-service-and-setup-project-with-installa/)
- [Creating a Windows Service and Installer](https://www.developer.com/design/creating-a-windows-service-and-installer/)
- [Automating Windows Service Installation](https://www.endpointdev.com/blog/2021/04/automating-windows-service-installation/)
- []()
- [Tutorial: Create a Windows service app](https://learn.microsoft.com/en-us/dotnet/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer)
- [Advanced Installer](https://www.advancedinstaller.com/how-to-create-an-installer-for-a-net-windows-service.html) - [How to create an installer for a .net Windows service app using Visual Studio](https://youtu.be/jNbI2r5YNYs)
- [How to create Setup file for Windows Service](https://www.google.com/search?q=How+to+create+Setup+file+for+Windows+Service)