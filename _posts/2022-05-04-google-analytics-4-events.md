---
layout: post
title: Google Analytics 4 Event Tracking
subtitle: Cách xem các thông số sự kiện trong báo cáo Google Analytics 4

tags:
- Analytics
- Tracking
- Event
- GA4
---

![Google Analytics 4](https://boxxv.github.io/img/posts/google-analytics-4.jpg "Google Analytics 4")

Với sự ra đời của Google Analytics 4 (GA4), nhóm tại Google cũng đã giới thiệu một mô hình dữ liệu mới. Điều này cho phép bạn kiểm soát nhiều hơn và linh hoạt hơn đối với dữ liệu bạn thu thập về khán giả, hành động của họ và trang web của bạn.

Nhiều tùy chọn hơn và tính linh hoạt cao hơn cũng có nghĩa là các sự kiện có thể trở nên khó hiểu. Nhanh. Vì vậy, hãy giải nén các sự kiện trong Google Analytics 4 và hiểu chúng là gì và cách bạn có thể sử dụng chúng để thu thập thông tin chi tiết bạn cần.

Ồ, và nếu bạn đã sử dụng Google Analytics một thời gian, thì có lẽ bạn đã quen thuộc với theo dõi sự kiện, tính năng này đã có từ năm 2007. Chúng ta sẽ bắt đầu bằng cách nói về các sự kiện mà chúng ta có thể theo dõi trong phiên bản trước của Google Analytics (được gọi là Universal Analytics) và so sánh chúng với các sự kiện mới trong Google Analytics 4.

### 1. Trước Google Analytics 4

Trước Google Analytics 4, các sự kiện được thiết kế để theo dõi các hành động trong các trang của trang web (hoặc trong ứng dụng của bạn). Ví dụ: nếu bạn muốn theo dõi số lần mọi người tải xuống tệp từ trang web của mình, bạn sẽ triển khai theo dõi sự kiện và sử dụng báo cáo sự kiện để xem số lượt tải xuống.

Hai vấn đề chính với phiên bản trước của theo dõi sự kiện là các giới hạn về lượng thông tin bạn có thể thu thập và các ràng buộc xung quanh việc báo cáo.

Khi bạn triển khai theo dõi sự kiện với phiên bản trước của Google Analytics, bạn có thể đặt tên cho danh mục sự kiện, đặt tên cho hành động, bao gồm nhãn tùy chọn (để nắm bắt thông tin bổ sung) và chỉ định một giá trị tùy chọn (như giá trị đô la).

Dưới đây là ví dụ về sự kiện `Universal Analytics` để theo dõi video:

- **Event category:** Video
- **Event action:** Play
- **Event label:** https://www.youtube.com/watch?v=4nXYvFXzxV4
- **Event value:** 0

Nếu bạn muốn nắm bắt thông tin bổ sung, bạn sẽ cần phải thay thế một trong các giá trị hiện có hoặc chèn thêm thông tin vào. Ví dụ: nếu bạn muốn sử dụng theo dõi sự kiện để báo cáo các lần nhấp vào các biểu ngữ quảng cáo khác nhau, bạn có thể xác định danh mục sự kiện là "khuyến mãi", sau đó là hành động sự kiện là "nhấp chuột" và nhãn sự kiện là "đặc biệt mùa hè", như chúng ta có thể thấy ở đây:

- **Event category:** Promotion
- **Event action:** Click
- **Event label:** Summer Specials
- **Event value:**

Nhưng nếu bạn có hai biểu ngữ cho chương trình khuyến mãi thì sao?

Sau đó, bạn sẽ cần quyết định xem bạn sẽ đổi tên thông số sự kiện nào. Ví dụ: bạn có thể có một nhãn sự kiện cho "summer specials top" và một nhãn sự kiện khác cho "summer specials sidebar". Điều này không sao cả, nhưng nó không linh hoạt, đặc biệt là khi nói đến báo cáo. Nếu bạn muốn báo cáo về hiệu suất của chương trình khuyến mại, bạn cần phải bao gồm cả hai nhãn. Nếu không, bạn sẽ bị thiếu dữ liệu.

Sau khi bạn triển khai theo dõi sự kiện trên trang web của mình, tất cả các sự kiện sẽ được đưa vào báo cáo sự kiện.

![Google Analytics 4](https://boxxv.github.io/img/posts/google-analytics-4-events.png "Google Analytics 4")



-----
Tham khảo:
- [Google Analytics 4 Event Tracking: Your Complete Guide](https://www.lovesdata.com/blog/google-analytics-4-events)
- [How to See Event Parameters in Google Analytics 4 Reports](https://www.optizent.com/how-to-see-event-parameters-in-google-analytics-4-reports/)