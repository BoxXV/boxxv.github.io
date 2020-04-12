---
layout: post
title: Head First Design Patterns Tiếng Việt
subtitle: Your brain on Design Patterns
---

## Mục lục

✅ Chapter 1: Intro to Design Patterns

✅ Chapter 2: the Observer Pattern

✅ Chapter 3: the Decorator Pattern

✅ Chapter 4: the Factory Pattern

✅ Chapter 5: the Singleton Pattern

✅ Chapter 6: the Command Pattern

✅ Chapter 7: the Adapter and Facade Patterns

✅ Chapter 8: the Template Method Pattern

✅ Chapter 9: the Iterator and Composite Patterns

✅ Chapter 10: the State Pattern

✅ Chapter 11: the Proxy Pattern

✅ Chapter 12: Compound Patterns

✅ Chapter 13: Better Living with Patterns


-----
### Chương 1: Strategy Pattern (Mẫu chiến lược)

**Strategy Pattern – Chào mừng đến với Design Patterns**

Ai đó đã giải quyết những vấn đề của bạn. Trong chương này Strategy Pattern (Mẫu chiến lược), bạn sẽ học được lý do tại sao (và làm thế nào) bạn có thể khai thác kiến thức và kinh nghiệm của những developer khác. Trước khi chúng ta hoàn thành, chúng ta sẽ xem xét việc sử dụng và lợi ích của các mẫu thiết kế, xem xét một số nguyên tắc thiết kế OO chính và xem qua một ví dụ về cách một mẫu hoạt động. Cách tốt nhất để sử dụng các mẫu là suy nghĩ về chúng và sau đó nhận ra nơi nào cần sử dụng trong thiết kế của bạn và các ứng dụng hiện có, nơi bạn có thể áp dụng chúng. Thay vì tự viết code, với các mẫu thiết kế bạn có được kinh nghiệm sử dụng lại code (reuse code).

**Bắt đầu với một ứng dụng SimUDuck đơn giản**

Joe làm việc cho một công ty rất thành công trò chơi mô phỏng vịt, SimUDuck. Trò chơi có thể hiển thị rất nhiều loài vịt bơi và tạo ra âm thanh “quack quack”. Thiết kế ban đầu của hệ thống đã sử dụng các kỹ thuật OO tiêu chuẩn và tạo ra một superclass Duck mà tất cả các loại vịt khác sẽ kế thừa nó.

![tempsnip](http://boxxv.com/img/patterns/tempsnip.png "tempsnip")_tempsnip_

Trong năm ngoái, công ty đã chịu áp lực ngày càng tăng từ các đối thủ cạnh tranh. Sau một tuần “động não” ngoài sân golf, các giám đốc điều hành của công ty nghĩ rằng đây là thời gian cho một sự thay đổi lớn. Công ty cần một cái gì đó thực sự ấn tượng để trình bày tại cuộc họp cổ đông sắp tới ở Maui.

**Nhưng bây giờ chúng tôi cần những con vịt BAY**

Giám đốc điều hành đã quyết định rằng vịt biết bay là thứ mà trình giả lập cần để thổi bay các đối thủ cạnh tranh khác. Và tất nhiên, người quản lý của Joe, nói với anh rằng nó sẽ không có vấn đề gì nên chỉ cần làm gì đó trong một tuần. “Sau tất cả”, ông chủ của Joe nói, “Khi anh ấy là một lập trình viên OO … nó sẽ khó đến mức nào?”

“Tôi chỉ cần thêm một phương thức fly() trong lớp Duck và sau đó tất cả các con vịt sẽ thừa hưởng nó. Bây giờ, thời gian của tôi để thực sự thể hiện tài năng OO thực sự của tôi.” 

![pasted](http://boxxv.com/img/patterns/pastedimage0.png "pasted")_pasted_




Tham khảo:
- [Bài dịch Head First Design Patterns Tiếng Việt](https://toihocdesignpattern.com/dich-sach/head-first-design-patterns)
- [Head First Design Patterns: A Brain-Friendly Guide](https://www.amazon.com/Head-First-Design-Patterns-Brain-Friendly/dp/0596007124)