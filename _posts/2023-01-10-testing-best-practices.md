---
layout: post
title: Testing Best Practices
subtitle: Kiến thức cần biết để kỹ sư kiểm thử phần mềm
image: "img/tdd.png"
tags:
- Testing
- QA
- Automation
- Best Practices
- TDD
---

Công việc của một Tester phần mềm không phải là một công việc dễ dàng. Nó chứa đầy những thách thức, cũng nhiều đòi hỏi không kém. Tester có nghĩa vụ phải cảnh giác và nhiệt tình trong từng giai đoạn của vòng đời ứng dụng.

Vai trò của một tester bắt đầu từ rất sớm. Và ngay từ khi khái niệm hóa dự án, tester đã tham gia vào các cuộc thảo luận với product owner, người quản lý dự án và các bên liên quan (stakeholders) khác nhau.

# I. Các khái niệm cơn bản

## Các mô hình quy trình kiểm thử phần mềm:
1. Traditional Waterfall Development Model (Thác nước truyền thống)
2. Agile Development Model
3. V Model
4. Spiral Model (Mô hình xoắn ốc)

![Testing](https://boxxv.github.io/img/test/software-testing-process-models-1.svg "Testing")

## Các Phương pháp/Cách tiếp cận Kiểm thử phần mềm:

![Testing](https://boxxv.github.io/img/test/types-of-software-testing.png "Testing")

1. `Kiểm thử hộp trắng`
2. `Kiểm tra hộp đen`
3. `Kiểm tra hộp xám`

![Testing](https://boxxv.github.io/img/test/blackbox-whitebox-test.jpg "Testing")

## Các Level/Cấp độ kiểm thử phần mềm:
1. `Unit Testing` (Kiểm tra đơn vị)
2. `Integration Testing` (Thử nghiệm hội nhập)
3. `System Testing` (Thử nghiệm hệ thống)
4. `Acceptance Testing` (Kiểm tra chấp nhận)


### Functional Testing - Kiểm thử phi chức năng
Tập trung vào việc xác minh hệ thống hoạt động theo đúng các yêu cầu nghiệp vụ.

![Testing](https://boxxv.github.io/img/test/functional-testing-intro4.png "Testing")

Các loại kiểm thử chức năng:
- `Unit Testing` (Kiểm thử đơn vị)
- `Sanity Testing`
- `Smoke Testing`
- `System Testing` (Kiểm thử hệ thống)
- `Acceptance Testing` (Kiểm thử chấp nhận)
- Installation Testing (Kiểm thử cài đặt)
- Interface Testing (Kiểm thử giao diện)
- Integration Testing (Kiểm thử tích hợp)
- Regression Testing (Kiểm thử hồi quy)
- Usability Testing (Kiểm tra khả năng sử dụng)
- Localization Testing
- .v.v.

> [8 Functional Testing Types Explained With Examples](https://www.simform.com/blog/functional-testing-types/)


### Non Functional Testing -  Kiểm thử chức năng
Tập trung vào việc xác minh hệ thống hoạt động theo đúng, mức độ sẵn sàng theo các tham số phi chức năng như:
1. `Security` (Bảo mật): Tham số xác định cách hệ thống được bảo vệ an toàn trước các cuộc tấn công có chủ ý và đột ngột từ các nguồn bên trong và bên ngoài.
2. `Reliability` (Độ tin cậy): Mức độ mà bất kỳ hệ thống phần mềm nào liên tục thực hiện các chức năng được chỉ định mà không gặp sự cố.
3. `Survivability` (Khả năng sống sót): Tham số kiểm tra rằng hệ thống phần mềm tiếp tục hoạt động và tự phục hồi trong trường hợp lỗi hệ thống.
4. `Availability` (Tính sẵn có): Tham số xác định mức độ mà người dùng có thể phụ thuộc vào hệ thống trong quá trình hoạt động.
5. `Usability` (Khả năng sử dụng): Người dùng có thể dễ dàng học hỏi, vận hành, chuẩn bị đầu vào và đầu ra thông qua tương tác với một hệ thống.
6. `Scalability` (Khả năng mở rộng): Thuật ngữ này đề cập đến mức độ mà bất kỳ ứng dụng phần mềm nào cũng có thể mở rộng khả năng xử lý của nó để đáp ứng nhu cầu gia tăng.
7. `Interoperability` (Khả năng tương tác): Tham số phi chức năng này kiểm tra giao diện hệ thống phần mềm với các hệ thống phần mềm khác.
8. `Efficiency` (Tính hiệu quả): Mức độ mà bất kỳ hệ thống phần mềm nào cũng có thể xử lý dung lượng, số lượng và thời gian đáp ứng.
9. `Flexibility` (Tính linh hoạt): Thuật ngữ này đề cập đến sự dễ dàng mà ứng dụng có thể hoạt động trong các cấu hình phần cứng và phần mềm khác nhau. Giống như RAM tối thiểu, yêu cầu CPU.
10. `Portability` (Tính di động): Tính linh hoạt của phần mềm để chuyển từ môi trường phần cứng hoặc phần mềm hiện tại của nó.
11. `Reusability` (Tái sử dụng): Nó đề cập đến một phần của hệ thống phần mềm có thể được chuyển đổi để sử dụng trong một ứng dụng khác.

Các loại kiểm thử phi chức năng
- Performance Testing (Kiểm thử hiệu năng)
- Load Testing (Kiểm thử tải)
- Failover Testing (Kiểm thử chuyển đổi dự phòng)
- Compatibility Testing (Kiểm thử tương thích)
- Usability Testing (Kiểm thử khả năng sử dụng)
- Stress Testing (Kiểm thử về áp lực)
- Maintainability Testing (Kiểm thử bảo trì)
- Scalability Testing (Kiểm thử khả năng mở rộng)
- Volume Testing (Kiểm thử khối lượng)
- Security Testing (Kiểm thử bảo mật)
- Disaster Recovery Testing (Kiểm thử khắc phục thảm họa)
- Compliance Testing (Kiểm thử tuân thủ)
- Portability Testing (Kiểm thử tính di động)

## Các công cụ kiểm thử phần mềm
- [Selenium](https://www.selenium.dev)
- [Appium](https://appium.io)
- [Katalon](https://katalon.com)
- [Cucumber](https://cucumber.io)
- HPE Unified Functional Testing
- Worksoft
- IBM Rational Functional Tester
- Teleric Test Studio
- Soap UI
- TestComplete


## Các thành phẩm kiểm thử phần mềm

![Software Testing Life Cycle (STLC) - Phases of Software Testing](https://boxxv.github.io/img/test/ppp10.png "Software Testing Life Cycle (STLC) - Phases of Software Testing")

- Test Strategy (Chiến lược test)
- Test Plan and Estimation
- Test Scenario
- Test Cases
- Test Data
- Requirement Traceability Matrix
- Test Summary Report
- Test Closure Report
- Incident Report

![Software Testing Life Cycle (STLC)](https://boxxv.github.io/img/test/STLC.png "Software Testing Life Cycle (STLC)")

-----
Tham khảo:

- [A COMPLETE GUIDE ON SOFTWARE TESTING](https://www.leewayhertz.com/software-testing-process/)
- [Types of Software Testing](https://www.javatpoint.com/types-of-software-testing)
- [A Quick Guide to the Software Testing Life Cycle (STLC)](https://jelvix.com/blog/software-testing-life-cycle)
- [The Evolution of the Testing Pyramid](https://www.james-willett.com/the-evolution-of-the-testing-pyramid/)
- [Test Pyramid In Practice](https://www.pgs-soft.com/blog/test-pyramid-in-practice/)
- [Restructuring Frontend Testing Pyramid: alternative to Unit/Integration/E2E approach](https://dev.to/hiroyone/frontend-testing-no-more-unitintegratione2e-categorizations-and-priorities-5358)
- [The Testing Pyramid](https://www.devopsgroup.com/insights/resources/diagrams/all/the-testing-pyramid/)
- [The Agile Testing Pyramid](https://www.agilecoachjournal.com/2014-01-28/the-agile-testing-pyramid)
- [System tests: an objective look at the product](https://blog.atinternet.com/en/system-tests-an-objective-look-at-the-product/)
- [Total Test Best Practices](https://devops.api.bmc.com/guidelines/ttt/ttt_best_practices.html)
- [Test Automation Pyramid: 2021 Version](https://medium.com/software-qe/test-automation-pyramid-2021-version-c299cb224c80)
- [Test Approach](https://www.you-getapptester.com/home/features-benefits/test-approach/)
- [Testing Strategies For Microservices](https://semaphoreci.com/blog/test-microservices)
- [The 5 Main Strategies for Testing a Microservices App](https://www.teaminternational.com/5-main-strategies-testing-microservices-app/)
- [Microservices Testing Strategies, Types & Tools: A Complete Guide](https://www.simform.com/blog/microservice-testing-strategies/)
- [Testing a Spring Boot Microservices: Tools and Techniques](https://medium.com/kth-distributed-systems/testing-microservices-in-spring-boot-applications-tools-and-techniques-b9c27d865f88)
- [Acceptance test with gauge and spring boot](https://mesutyakut.medium.com/acceptance-test-with-gauge-and-spring-boot-f675655d8e)

-----
- [Phương pháp kiểm thử phần mềm - Nguyên lý kiểm thử phần mềm](https://viblo.asia/p/phuong-phap-kiem-thu-phan-mem-nguyen-ly-kiem-thu-phan-mem-OeVKB3kJZkW)
- [CÁC PHƯƠNG PHÁP KIỂM THỬ.](https://viblo.asia/p/cac-phuong-phap-kiem-thu-1Je5EjV0KnL)
- [Kiểm thử hộp trắng](https://viblo.asia/p/kiem-thu-hop-trang-PaLGDBNMklX)
- [Kiểm Thử Hộp Trắng](https://viblo.asia/p/kiem-thu-hop-trang-jvElaLGAZkw)
- [Kỹ thuật kiểm thử hộp trắng - White-box testing](https://viblo.asia/p/ky-thuat-kiem-thu-hop-trang-white-box-testing-maGK7MpOlj2)
- [Tìm hiểu về kiểm thử hộp trắng(Phần 1)](https://viblo.asia/p/tim-hieu-ve-kiem-thu-hop-trangphan-1-924lJpm0KPM)
- [Tìm hiểu về kiểm thử hộp trắng (phần 2)](https://viblo.asia/p/tim-hieu-ve-kiem-thu-hop-trang-phan-2-E375z83RZGW)
- [Kiểm thử chuyển đổi cơ sở dữ liệu: Hộp Đen hay Hộp Trắng?](https://viblo.asia/p/kiem-thu-chuyen-doi-co-so-du-lieu-hop-den-hay-hop-trang-NPVMax9wRQOk)
- [KIỂM THỬ HỘP ĐEN](https://viblo.asia/p/kiem-thu-hop-den-4P856x31ZY3)
- [Kiểm Thử Hộp Đen - Black box Testing](https://viblo.asia/p/kiem-thu-hop-den-black-box-testing-Do754NYBZM6)
- [Kỹ thuật kiểm thử hộp đen (Black-Box Testing)](https://viblo.asia/p/ky-thuat-kiem-thu-hop-denblack-box-testing-ByEZk0qElQ0)
- [Kỹ thuật kiểm thử hộp đen - Black box Testing](https://viblo.asia/p/ky-thuat-kiem-thu-hop-den-black-box-testing-WrJvYADwvVO)
- [Các kỹ thuật kiểm thử hộp đen (Phần 1)](https://viblo.asia/p/cac-ky-thuat-kiem-thu-hop-den-phan-1-MdZGAjVbeox)
- [Các kỹ thuật kiểm thử hộp đen (Phần 2)](https://viblo.asia/p/cac-ky-thuat-kiem-thu-hop-den-phan-2-rQOvPNyYeYj)
- [Kiểm thử hộp xám là gì?](https://viblo.asia/p/kiem-thu-hop-xam-la-gi-E375zgp1KGW)

-----
- [Unit Test - Kiểm thử đơn vị](https://viblo.asia/p/unit-test-la-gi-maGK7m3Llj2)
- [Integration testing - Kiểm thử tích hợp](https://viblo.asia/p/kiem-thu-tich-hop-integration-testing-Qpmle71DKrd)
- [System Testing - Kiểm thử hệ thống](https://viblo.asia/p/system-testing-kiem-thu-he-thong-aWj53pOPK6m)
- [System Testing - Kiểm thử hệ thống](https://viblo.asia/p/system-testing-kiem-thu-he-thong-GrLZDywBlk0)
- [Acceptance Testing - Kiểm thử chấp nhận](https://anhtester.com/blog/acceptance-testing-kiem-thu-chap-nhan-b298.html)
- [Acceptance Test là gì, được thực hiện như thế nào?](https://itnavi.com.vn/blog/acceptance-test-la-gi)
- [Acceptance Testing là gì? Phân loại Acceptance Testing](https://vn.got-it.ai/blog/acceptance-testing-la-gi-phan-loai-acceptance-testing)
- [Test level](https://viblo.asia/p/test-level-istqb-foudation-gAm5ybGDKdb)
- [Tìm hiểu về các loại Test Level](https://viblo.asia/p/tim-hieu-ve-cac-loai-test-level-DXOkRZXakdZ)
- [Tìm hiểu về các loại test type (phần 1)](https://viblo.asia/p/tim-hieu-ve-cac-loai-test-type-phan-1-eXoKWkowKLO)
- [System testing và End-to-End testing](https://viblo.asia/p/system-testing-va-end-to-end-testing-gDVK28A2lLj)
- [Sự khác nhau giữa System Testing Và End-To-End Testing](https://viblo.asia/p/su-khac-nhau-giua-system-testing-va-end-to-end-testing-YWOZrdQY5Q0)
- [Kiểm thử phi chức năng là gì?](https://viblo.asia/p/kiem-thu-phi-chuc-nang-la-gi-924lJxvbKPM)
- [Tìm hiểu về kiểm thử chức năng (Functionality Testing)](https://viblo.asia/p/tim-hieu-ve-kiem-thu-chuc-nang-functionality-testing-bJzKmLVB59N)
- [Tìm hiểu về kiểm thử chức năng (Functional Testing) trong kiểm thử phần mềm](https://viblo.asia/p/tim-hieu-ve-kiem-thu-chuc-nang-functional-testing-trong-kiem-thu-phan-mem-yMnKM9kmK7P)
- [Kiểm thử phi chức năng](https://viblo.asia/p/kiem-thu-phi-chuc-nang-924lJpX6KPM)
- [Giới thiệu về kiểm thử phi chức năng](https://viblo.asia/p/gioi-thieu-ve-kiem-thu-phi-chuc-nang-Qbq5Q39JZD8)
- [Non-functional Testing là gì?](https://viblo.asia/p/non-functional-testing-la-gi-GrLZDvwE5k0)
- [Sự khác nhau giữa Functional Testing và Non-Functional Testing](https://viblo.asia/p/su-khac-nhau-giua-functional-testing-va-non-functional-testing-XL6lAv4D5ek)
- [Tìm hiểu về IOT testing](https://viblo.asia/p/tim-hieu-ve-iot-testing-gDVK29Bw5Lj)
- [What is IoT Testing? Types & Tools](https://www.guru99.com/iot-testing-challenges-tools.html)
- [Nên kiểm thử tự động hay kiểm thử thủ công](https://viblo.asia/p/nen-kiem-thu-tu-dong-hay-kiem-thu-thu-cong-LzD5dD1d5jY)
- [Chiến lược kiểm thử Round Earth](https://viblo.asia/p/chien-luoc-kiem-thu-round-earth-maGK7kxLKj2)
- [https://viblo.asia/tags/test-level](https://viblo.asia/tags/test-level)
- [https://viblo.asia/tags/unit-test](https://viblo.asia/tags/unit-test)
- [https://viblo.asia/tags/integration-test](https://viblo.asia/tags/integration-test)
- [https://viblo.asia/tags/system-test](https://viblo.asia/tags/system-test)
- [https://viblo.asia/tags/functional-testing](https://viblo.asia/tags/functional-testing)
- [https://viblo.asia/tags/non-functional-testing](https://viblo.asia/tags/non-functional-testing)
- [https://viblo.asia/tags/testcase](https://viblo.asia/tags/testcase)

-----
- [Tìm hiểu về test plan](https://viblo.asia/p/tim-hieu-ve-test-plan-naQZReO0Kvx)
- [Test Strategy](https://viblo.asia/p/test-strategy-YWOZreRNKQ0)
- [Kỹ thuật kiểm thử - Kiểm thử hộp đen(Black box testing)](https://viblo.asia/p/ky-thuat-kiem-thu-kiem-thu-hop-denblack-box-testing1-V3m5WQEwZO7)
- [QA Engineer là gì? QC Engineer là gì?](https://isocert.org.vn/qa-engineer-la-gi-qc-engineer-la-gi-tim-hieu-ve-qa-engineer-va-qc-engineer)
- [Tất tần tật về QA - All about QA job Description, Roles, Duties and Career path.](https://viblo.asia/p/tat-tan-tat-ve-qa-all-about-qa-job-description-roles-duties-and-career-path-Az45byvqlxY)
- [How to Write Test Cases ( Hướng dẫn cách viết Testcases)](https://viblo.asia/p/how-to-write-test-cases-huong-dan-cach-viet-testcases-eW65GRY9lDO)
- [Làm thế nào để viết testcase cho người mới bắt đầu - Khái niệm và các loại test case](https://viblo.asia/p/lam-the-nao-de-viet-testcase-cho-nguoi-moi-bat-dau-khai-niem-va-cac-loai-test-case-V3m5Wj6WlO7)
- [Cách viết test case cho phần mềm](https://viblo.asia/p/cach-viet-test-case-cho-phan-mem-LzD5dx1w5jY)
- [Cách viết test case cho phần mềm - Viết Test Case từ User Story & Acceptance Criteria](https://viblo.asia/p/cach-viet-test-case-cho-phan-mem-viet-test-case-tu-user-story-acceptance-criteria-yMnKMMeNK7P)
- [Làm thế nào để quản lý test case tốt](https://viblo.asia/p/lam-the-nao-de-quan-ly-test-case-tot-gDVK23z0ZLj)
- [Hướng dẫn xây dựng Testcase Chức năng](https://viblo.asia/p/huong-dan-xay-dung-testcase-chuc-nang-Qbq5Qq1G5D8)
- [Tìm hiểu về Kiểm thử chức năng đăng xuất - Logout Functionality](https://viblo.asia/p/tim-hieu-ve-kiem-thu-chuc-nang-dang-xuat-logout-functionality-gAm5yV1DKdb)
- [Mẫu Test Case tốt nhất kèm ví dụ](https://viblo.asia/p/mau-test-case-tot-nhat-kem-vi-du-bWrZnvnwZxw)
- [Kiểm thử độ bền là gì?](https://viblo.asia/p/kiem-thu-do-ben-la-gi-ORNZqbMMl0n)
- [Software Testing Metric - Chìa khoá để giải quyết mọi bài toán của Test Leaders](https://viblo.asia/p/software-testing-metric-chia-khoa-de-giai-quyet-moi-bai-toan-cua-test-leaders-naQZRREQZvx)
- [Cucumber (P1) - Giới thiệu tổng quan](https://viblo.asia/p/cucumber-p1-gioi-thieu-tong-quan-YWOZrD8v5Q0)
- [Cucumber (P2) - Tạo project bằng Eclipse và quản lý thư viện với Maven](https://viblo.asia/p/cucumber-p2-tao-project-bang-eclipse-va-quan-ly-thu-vien-voi-maven-Ljy5VdOGZra)
- [Cucumber (P3) - Parameters và Scenario Outline](https://viblo.asia/p/cucumber-p3-parameters-va-scenario-outline-ByEZk7bEZQ0)
- [Cucumber (P4) - Cucumber Options & Report](https://viblo.asia/p/cucumber-p4-cucumber-options-report-LzD5dNOEZjY)
- [Test API sử dụng Pytest (Phần 1: Kiến thức cơ bản)](https://viblo.asia/p/test-api-su-dung-pytest-phan-1-kien-thuc-co-ban-GrLZDr435k0)
- [Test API sử dụng Pytest (Phần 2: Testcase Template và Dynamic Testing Function)](https://viblo.asia/p/test-api-su-dung-pytest-phan-2-testcase-template-va-dynamic-testing-function-1VgZvAvMKAw)
- [Sự khác nhau giữa Sanity Testing và Smoke Testing](https://viblo.asia/p/su-khac-nhau-giua-sanity-testing-va-smoke-testing-4dbZNJRLZYM)
- [Agile Testing là gì?](https://viblo.asia/p/agile-testing-la-gi-YWOZragEKQ0)
- [Góc nhìn của một Tester về các dự án Agile](https://viblo.asia/p/goc-nhin-cua-mot-tester-ve-cac-du-an-agile-bWrZn4zO5xw)
- [Agile & Scrum](https://viblo.asia/p/agile-scrum-3Q75w8PQKWb)
- [V model trong kiểm thử phần mềm là gì? Tìm hiểu với ví dụ SDLC& STLC.](https://viblo.asia/p/v-model-trong-kiem-thu-phan-mem-la-gi-tim-hieu-voi-vi-du-sdlc-stlc-Qbq5QMEL5D8)
- [Vòng đời kiểm thử trong một vài mô hình phát triển phần mềm phổ biến hiện nay](https://viblo.asia/p/vong-doi-kiem-thu-trong-mot-vai-mo-hinh-phat-trien-phan-mem-pho-bien-hien-nay-WAyK8R6klxX)
- [https://viblo.asia/tags/cypress](https://viblo.asia/tags/cypress)
- [https://viblo.asia/u/oanhnguyen2403](https://viblo.asia/u/oanhnguyen2403)
- [https://viblo.asia/u/nguyen.hong.minh](https://viblo.asia/u/nguyen.hong.minh)
- [https://viblo.asia/u/tran.thi.tra.giang](https://viblo.asia/u/tran.thi.tra.giang)
- [https://viblo.asia/u/ngocyanl2k1](https://viblo.asia/u/ngocyanl2k1)
- [https://viblo.asia/u/thaoltp](https://viblo.asia/u/thaoltp)

-----
- [7 nguyên tắc quan trọng trong kiểm thử phần mềm](https://viblo.asia/p/7-nguyen-tac-quan-trong-trong-kiem-thu-phan-mem-Qbq5QrPEKD8)
- [7 cách đơn giản để trở thành một kiểm thử phần mềm hiệu quả](https://viblo.asia/p/7-cach-don-gian-de-tro-thanh-mot-kiem-thu-phan-mem-hieu-qua-maGK74gBZj2)
- [7 cách dễ dàng để việc kiểm thử trở nên hiệu quả](https://viblo.asia/p/7-cach-de-dang-de-viec-kiem-thu-tro-nen-hieu-qua-gDVK28zAlLj)
- [7 Kỹ năng để trở thành một automation tester thành công trong năm 2019](https://viblo.asia/p/7-ky-nang-de-tro-thanh-mot-automation-tester-thanh-cong-trong-nam-2019-aWj534vYK6m)
- [Các hướng dẫn để trở thành một người kiểm thử](https://viblo.asia/p/cac-huong-dan-de-tro-thanh-mot-nguoi-kiem-thu-Qpmle7oNKrd)
- [Trở thành Kiểm thử viên: 9 lời đồn và sự thật](https://viblo.asia/p/tro-thanh-kiem-thu-vien-9-loi-don-va-su-that-bWrZnv7QZxw)
- [Làm thế nào để trở thành người kiểm thử hiệu năng tốt hơn](https://viblo.asia/p/lam-the-nao-de-tro-thanh-nguoi-kiem-thu-hieu-nang-tot-hon-MJykjxzJGPB)
- [Làm thế nào để trở thành 1 kiểm thử viên phần mềm? (Part 1)](https://viblo.asia/p/lam-the-nao-de-tro-thanh-1-kiem-thu-vien-phan-mem-part-1-XL6lAkG4Kek)
- [Làm thế nào để trở thành 1 kiểm thử viên phần mềm? (Part 2)](https://viblo.asia/p/lam-the-nao-de-tro-thanh-1-kiem-thu-vien-phan-mem-part-2-m68Z0RYX5kG)
- [Chỉ số chất lượng của một tester: 22 giá trị cốt lõi để trở thành người kiểm thử tốt](https://viblo.asia/p/chi-so-chat-luong-cua-mot-tester-22-gia-tri-cot-loi-de-tro-thanh-nguoi-kiem-thu-tot-63vKjawM52R)
- [Thành kiến nhận thức trong kiểm thử phần mềm. Tại sao kiểm thử viên lại để sót bug?](https://viblo.asia/p/thanh-kien-nhan-thuc-trong-kiem-thu-phan-mem-tai-sao-kiem-thu-vien-lai-de-sot-bug-Do754joBZM6)
- [Chìa khóa kiểm thử đơn vị thành công - Làm thế nào các nhà phát triển kiểm thử mã code của họ?](https://viblo.asia/p/chia-khoa-kiem-thu-don-vi-thanh-cong-lam-the-nao-cac-nha-phat-trien-kiem-thu-ma-code-cua-ho-RQqKLq0rZ7z)
- [5 mẹo đơn giản để việc kiểm thử của bạn trở lên đơn giản](https://viblo.asia/p/5-meo-don-gian-de-viec-kiem-thu-cua-ban-tro-len-don-gian-YWOZraJPKQ0)
- [Cách để trở thành người kiểm thử phần mềm giỏi](https://viblo.asia/p/cach-de-tro-thanh-nguoi-kiem-thu-phan-mem-gioi-RQqKLQp6Z7z)
- [Những yếu tố cần thiết để trở thành kỹ sư kiểm thử phần mềm giỏi](https://viblo.asia/p/nhung-yeu-to-can-thiet-de-tro-thanh-ky-su-kiem-thu-phan-mem-gioi-maGK7kBaKj2)
- [Những kỹ năng cần thiết của một Tester](https://viblo.asia/p/nhung-ky-nang-can-thiet-cua-mot-tester-bWrZnBwbZxw)
- [10 điều bạn nên làm nếu muốn trở thành một tester giỏi](https://viblo.asia/p/10-dieu-ban-nen-lam-neu-muon-tro-thanh-mot-tester-gioi-xQMkJRpLkam)
- [Học gì để trở thành một Tester?](https://viblo.asia/p/hoc-gi-de-tro-thanh-mot-tester-L4x5xQbOKBM)
- [Cách trở thành một tester beta giỏi](https://viblo.asia/p/cach-tro-thanh-mot-tester-beta-gioi-oOVlY11zl8W)
- [TRỞ THÀNH TESTER XUẤT SẮC NHƯ THẾ NÀO?](https://viblo.asia/p/tro-thanh-tester-xuat-sac-nhu-the-nao-RnB5pB8wZPG)
- [Làm thế nào để trở thành test leader?](https://viblo.asia/p/lam-the-nao-de-tro-thanh-test-leader-m68Z08wAZkG)
- [9 bước để trở thành một QA leader tuyệt vời](https://viblo.asia/p/9-buoc-de-tro-thanh-mot-qa-leader-tuyet-voi-XQZGxdPMGwA)
- [Thiếu những kỹ năng mềm sẽ cản trở con đường tới thành công của Test Manager như thế nào? (Phần 1)](https://viblo.asia/p/thieu-nhung-ky-nang-mem-se-can-tro-con-duong-toi-thanh-cong-cua-test-manager-nhu-the-nao-phan-1-WrJeYAOaeVO)
- [Thiếu những kỹ năng mềm sẽ cản trở con đường tới thành công của Test Manager như thế nào? (Phần 2)](https://viblo.asia/p/thieu-nhung-ky-nang-mem-se-can-tro-con-duong-toi-thanh-cong-cua-test-manager-nhu-the-nao-phan-2-gVQvlQznGZJ)
- [10 kỹ năng để trở thành 1 great tester](https://viblo.asia/p/10-ky-nang-de-tro-thanh-1-great-tester-oOVlY1O4l8W)
- [Tester có cần phải biết code??](https://viblo.asia/p/tester-co-can-phai-biet-code-qzakzJAakyO)
- [Một "chớt" tâm sự của một Tester quèn gửi tới Dev team, PM, DM, PO,...](https://viblo.asia/p/mot-chot-tam-su-cua-mot-tester-quen-gui-toi-dev-team-pm-dm-po-ORNZqnXrl0n)
- [NHỮNG CÂU HỎI PHỎNG VẤN QC // MANUAL TESTER // FRESHER](https://viblo.asia/p/nhung-cau-hoi-phong-van-qc-manual-tester-fresher-ddtcmt-n1j4l3vlVwl)
- [Bộ câu hỏi phỏng vấn tuyển dụng Tester](https://viblo.asia/p/bo-cau-hoi-phong-van-tuyen-dung-tester-vyDZOkEkZwj)
- [What Is Full Stack QA or Tester? 4 Steps Guide For Beginners](https://www.opencodez.com/software-testing/become-full-stack-qa-engineer.htm)
- [ROADMAP TO QA AUTOMATION ENGINEER](https://synapse-qa.com/2020/11/15/roadmap-to-qa-automation-engineer/)
- [https://toolsqa.com/](https://toolsqa.com/)
- [Roadmap QA Engineer](https://roadmap.sh/qa/)