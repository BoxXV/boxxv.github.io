---
layout: post
title: Tìm hiểu về Automation Testing
subtitle: 7 bước để trở thành một Automation Testing Engineer
image: "img/projects-bg.jpg"
tags:
- Automation
- Testing
- PerformanceTest
---

![Automation Testing](https://boxxv.github.io/img/2023/1-2.png "Automation Testing")

Làm thế nào để trở thành một Automation Testing Engineer? Như mọi người đều biết răng, kiểm thử tự động đang dần trở thành một xu hướng HOT để các bạn tìm hiểu, cũng như thị trường việc làm của công việc này ngày càng tăng. Vậy thì các bạn cần tìm hiểu những kiến thức gì, và cần có những kỹ năng gì để bước vào lĩnh vực này.

## I. Automation Test là gì? Khi nào nên sử dụng Automation Test?

Khi khái niệm Automation Test (kiểm tra tự động) ra đời, Tester chỉ cần viết một đoạn code hoặc sử dụng một số công cụ như Selenium, Test Complete, Jmetter… để chạy tự động tất cả các bước bao gồm nhập thông tin, click, kiểm tra kết quả, so sánh kết quả thực tế với kết quả giả định.

Nhiều loại test có thể làm auto, ví dụ như functional testing, performance/load testing, unit testing.

### Ưu điểm của Automation Test

![Automation Testing](https://boxxv.github.io/img/2023/MVP.png "Automation Testing")

1. Đáng tin cậy. Test chạy chính xác theo quy trình đã định sẵn. vì vậy tránh được nhiều lỗi do con người tạo ra, ví dụ như nhập sai dữ liệu.
2. Mình có thể test cách phần mềm xử lý (tính năng/hiệu năng) khi gặp tình huống chạy lặp đi lặp lại nhiều lần (cùng lúc) trên cùng script test. Đây còn gọi là performance/load testing.
3. Mình có thể lập trình nhiều test tinh vi hơn để thu về những thông tin ẩn từ ứng dụng. Ở điểm này thì Manual Test không thể làm được.
4. Test mang tính toàn diện cao. Mình có thể tạo ra một bộ test để bao quát hết tất cả tính năng trong ứng dụng.
5. Mình có thể tái sử dụng test trên nhiều phiên bản khác nhau của ứng dụng, ngay cả khi có sự thay đổi giao diện. Nếu chạy Manual Test thì một test case mất một tiếng, ba môi trường tốn ba tiếng. Mà trong suốt quá trình phát triển sản phẩm, chúng ta phải lặp lại quá trình test vô số lần, dẫn đến mất thời gian nếu làm Manual Test. Thay vào đó, chỉ cần viết một script test thì mỗi lần deploy lên môi trường mới, mình chỉ cần thay đổi URL là test tự chạy được.
6. Chất lượng và hiệu suất phần mềm tốt hơn bởi vì mình có thể chạy nhiều test trong thời gian ngắn hơn với ít resource nhất.
7. Automation Testing Tools giúp chạy test nhanh hơn test bằng tay.
8. Có tính kinh  tế cao vì có thể giảm thiểu nguồn nhân lực làm kiểm tra hồi quy.

### Nhược điểm của Automation Test

1. Nhiều tool có chi phí rất cao, ví dụ như commercial tool: HP Quick Test Pro.
2. Thường thì lương trả cho Automation Tester nhiều hơn Manual Tester, vì công việc đòi hỏi họ có kỹ năng cao hơn, ví dụ như phải biết code, phải viết được script.
3. Chi phí để phát triển và bảo trì test script cao. Ví dụ một test case nếu Manual Test thì mất 1 tiếng. Nhưng nếu đổi sang chạy Automation Test, cần chuẩn bị test script (mà trong trường hợp khó) thì phải mất 6-7 tiếng để viết test script. Người viết test script cần có kỹ năng lập trình và tool để chạy test. Vì vậy chi phí cho Automation Test cao hơn Manual Test.
4. Đòi hỏi Tester phải có kinh nghiệm technical và kỹ năng lập trình.
5. Đòi hỏi thời gian chuẩn bị dài hơn để thiết kế, cài đặt kỹ càng trước khi cần đưa dự án đi test.
6. Có những dự án không nên chạy Automation Test, nhưng nhiều Tester vẫn hiểu nhầm và chạy Automation Test, dẫn đến mất thời gian, resource, công sức. Ví dụ như khi test một chức năng quá phức tạp của một ứng dụng hoặc một GUI object thì phải chạy Manual Test.






## Tổng kết




-----
Tham khảo:

- [Automation Test là gì? Khi nào nên sử dụng Automation Test?](https://itviec.com/blog/automation-test/)
- [7 bước để trở thành một Automation Testing Engineer](https://viblo.asia/p/7-buoc-de-tro-thanh-mot-automation-testing-engineer-4P856XBGZY3)
- [Automation Test là gì? Khi nào nên sử dụng Automation Test?](https://itviec.com/blog/automation-test/)
- [NHỮNG CÂU HỎI PHỎNG VẤN QC // MANUAL TESTER // FRESHER](https://viblo.asia/p/nhung-cau-hoi-phong-van-qc-manual-tester-fresher-ddtcmt-n1j4l3vlVwl)
- [Top 10 Benefits of Automated Testing](https://testinium.com/blog/top-10-benefits-of-automated-testing-2/)
- [Test automation 101](https://bootcamp.uxdesign.cc/test-automation-264d219ac83)
- [What Is Full Stack QA or Tester? 4 Steps Guide For Beginners](https://www.opencodez.com/software-testing/become-full-stack-qa-engineer.htm)
- [ROADMAP TO QA AUTOMATION ENGINEER](https://synapse-qa.com/2020/11/15/roadmap-to-qa-automation-engineer/)
