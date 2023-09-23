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

## Mục lục

- [Mục lục](#mục-lục)
- [Hướng dẫn đầy đủ về Google Analytics 4](#hướng-dẫn-đầy-đủ-về-google-analytics-4)
  - [1. Trước Google Analytics 4](#1-trước-google-analytics-4)
  - [2. Hits vs. Events](#2-hits-vs-events)
  - [3. Bạn có thể theo dõi những gì bằng sự kiện trong Google Analytics 4?](#3-bạn-có-thể-theo-dõi-những-gì-bằng-sự-kiện-trong-google-analytics-4)
  - [4. Thông số sự kiện trong Google Analytics 4](#4-thông-số-sự-kiện-trong-google-analytics-4)
  - [5. Sự kiện tự động trong Google Analytics 4](#5-sự-kiện-tự-động-trong-google-analytics-4)
  - [6. Đo lường nâng cao](#6-đo-lường-nâng-cao)
  - [7. Sự kiện được đề xuất trong Google Analytics 4](#7-sự-kiện-được-đề-xuất-trong-google-analytics-4)
  - [8. Sự kiện tùy chỉnh trong Google Analytics 4](#8-sự-kiện-tùy-chỉnh-trong-google-analytics-4)
  - [9. Gửi sự kiện tới Google Analytics 4](#9-gửi-sự-kiện-tới-google-analytics-4)
  - [10. Tạo sự kiện mới trong giao diện](#10-tạo-sự-kiện-mới-trong-giao-diện)
  - [11. Sửa đổi sự kiện trong giao diện](#11-sửa-đổi-sự-kiện-trong-giao-diện)
  - [12. Gửi sự kiện bằng Trình quản lý thẻ của Google](#12-gửi-sự-kiện-bằng-trình-quản-lý-thẻ-của-google)
  - [13. Báo cáo về sự kiện của bạn trong Google Analytics 4](#13-báo-cáo-về-sự-kiện-của-bạn-trong-google-analytics-4)
  - [14. Chuyển đổi dựa trên sự kiện](#14-chuyển-đổi-dựa-trên-sự-kiện)
  - [15. Liên kết các sự kiện Universal Analytics với các sự kiện Google Analytics 4](#15-liên-kết-các-sự-kiện-universal-analytics-với-các-sự-kiện-google-analytics-4)
  - [16. Các giới hạn đối với Sự kiện Google Analytics 4](#16-các-giới-hạn-đối-với-sự-kiện-google-analytics-4)
  - [17. Tóm tắt thiết lập sự kiện](#17-tóm-tắt-thiết-lập-sự-kiện)
    - [1. Bạn đã theo dõi các sự kiện trong Universal Analytics chưa?](#1-bạn-đã-theo-dõi-các-sự-kiện-trong-universal-analytics-chưa)
    - [2. Tính năng theo dõi sự kiện tự động (bao gồm cả Đo lường nâng cao) đã đủ chưa?](#2-tính-năng-theo-dõi-sự-kiện-tự-động-bao-gồm-cả-đo-lường-nâng-cao-đã-đủ-chưa)
    - [3. Các sự kiện được đề xuất có bao gồm những gì bạn muốn theo dõi không?](#3-các-sự-kiện-được-đề-xuất-có-bao-gồm-những-gì-bạn-muốn-theo-dõi-không)
    - [4. Các sự kiện tùy chỉnh của bạn có tuân theo quy ước đặt tên của Google không?](#4-các-sự-kiện-tùy-chỉnh-của-bạn-có-tuân-theo-quy-ước-đặt-tên-của-google-không)
    - [5. Bạn có thể sử dụng trình kích hoạt hiện có trong Trình quản lý thẻ của Google để kích hoạt thẻ sự kiện mới không?](#5-bạn-có-thể-sử-dụng-trình-kích-hoạt-hiện-có-trong-trình-quản-lý-thẻ-của-google-để-kích-hoạt-thẻ-sự-kiện-mới-không)
    - [6. Liệu sự kiện bạn đang muốn theo dõi có cung cấp những hiểu biết có giá trị không?](#6-liệu-sự-kiện-bạn-đang-muốn-theo-dõi-có-cung-cấp-những-hiểu-biết-có-giá-trị-không)
- [Cách xem thông số sự kiện trong báo cáo Google Analytics 4](#cách-xem-thông-số-sự-kiện-trong-báo-cáo-google-analytics-4)


![Google Analytics 4](https://boxxv.github.io/img/posts/google-analytics-4.jpg "Google Analytics 4")

Với sự ra đời của Google Analytics 4 (GA4), nhóm tại Google cũng đã giới thiệu một mô hình dữ liệu mới. Điều này cho phép bạn kiểm soát nhiều hơn và linh hoạt hơn đối với dữ liệu bạn thu thập về khán giả, hành động của họ và trang web của bạn.

Nhiều tùy chọn hơn và tính linh hoạt cao hơn cũng có nghĩa là các sự kiện có thể trở nên khó hiểu. Nhanh. Vì vậy, hãy giải nén các sự kiện trong Google Analytics 4 và hiểu chúng là gì và cách bạn có thể sử dụng chúng để thu thập thông tin chi tiết bạn cần.

Ồ, và nếu bạn đã sử dụng Google Analytics một thời gian, thì có lẽ bạn đã quen thuộc với theo dõi sự kiện, tính năng này đã có từ năm 2007. Chúng ta sẽ bắt đầu bằng cách nói về các sự kiện mà chúng ta có thể theo dõi trong phiên bản trước của Google Analytics (được gọi là Universal Analytics) và so sánh chúng với các sự kiện mới trong Google Analytics 4.

## Hướng dẫn đầy đủ về Google Analytics 4

### 1. Trước Google Analytics 4

Trước Google Analytics 4, các sự kiện được thiết kế để theo dõi các hành động trong các trang của trang web (hoặc trong ứng dụng của bạn). Ví dụ: nếu bạn muốn theo dõi số lần mọi người tải xuống tệp từ trang web của mình, bạn sẽ triển khai theo dõi sự kiện và sử dụng báo cáo sự kiện để xem số lượt tải xuống.

Hai vấn đề chính với phiên bản trước của theo dõi sự kiện là các giới hạn về lượng thông tin bạn có thể thu thập và các ràng buộc xung quanh việc báo cáo.

Khi bạn triển khai theo dõi sự kiện với phiên bản trước của Google Analytics, bạn có thể đặt tên cho danh mục sự kiện, đặt tên cho hành động, bao gồm nhãn tùy chọn (để nắm bắt thông tin bổ sung) và chỉ định một giá trị tùy chọn (như giá trị đô la).

Dưới đây là ví dụ về sự kiện `Universal Analytics` để theo dõi video:

- **Event category:** Video
- **Event action:** Play
- **Event label:** https://www.youtube.com/watch?v=4nXYvFXzxV4
- **Event value:** 0

Nếu bạn muốn nắm bắt thông tin bổ sung, bạn sẽ cần phải thay thế một trong các giá trị hiện có hoặc chèn thêm thông tin vào. Ví dụ: nếu bạn muốn sử dụng theo dõi sự kiện để báo cáo các lần nhấp vào các biểu ngữ quảng cáo khác nhau, bạn có thể xác định danh mục sự kiện là "Khuyến mãi", sau đó là hành động sự kiện là "Nhấp chuột" và nhãn sự kiện là "Ưu đãi mùa hè", như chúng ta có thể thấy ở đây:

- **Event category:** Promotion
- **Event action:** Click
- **Event label:** Summer Specials
- **Event value:**

Nhưng nếu bạn có hai biểu ngữ cho chương trình khuyến mãi thì sao?

Sau đó, bạn sẽ cần quyết định xem bạn sẽ đổi tên thông số sự kiện nào. Ví dụ: bạn có thể có một nhãn sự kiện cho "summer specials top" và một nhãn sự kiện khác cho "summer specials sidebar". Điều này không sao cả, nhưng nó không linh hoạt, đặc biệt là khi nói đến báo cáo. Nếu bạn muốn báo cáo về hiệu suất của chương trình khuyến mại, bạn cần phải bao gồm cả hai nhãn. Nếu không, bạn sẽ bị thiếu dữ liệu.

Sau khi bạn triển khai theo dõi sự kiện trên trang web của mình, tất cả các sự kiện sẽ được đưa vào báo cáo sự kiện.

![Google Analytics 4](https://boxxv.github.io/img/posts/google-analytics-4-events.png "Google Analytics 4")

Trong Google Analytics 4, mọi thứ sẽ được gửi đến báo cáo của bạn dưới dạng sự kiện, không chỉ những hành động bạn đã theo dõi trên một trang, do đó, báo cáo của bạn có thể linh hoạt hơn. Chúng ta sẽ nói nhiều hơn về báo cáo sau.

### 2. Hits vs. Events

Vì vậy, trong Universal Analytics, các sự kiện được thiết kế để theo dõi hành động trong một trang. Ngược lại, trong Google Analytics 4, sự kiện được dùng để gửi tất cả các loại dữ liệu đến báo cáo của bạn. Điều này bao gồm các hành động, chi tiết về người dùng của bạn và thông tin khác về trang web của bạn.

Nếu chúng tôi so sánh điều này với Universal Analytics thì dữ liệu luôn được gửi dưới dạng 'lần truy cập'. Và có những loại lần truy cập được xác định trước mà bạn có thể gửi, điều đó có nghĩa là bạn sẽ không gặp may nếu muốn thu thập thông tin tùy chỉnh không khớp với một trong các loại lần truy cập được xác định trước. Các loại lần truy cập trong Universal Analytics là:

- Lượt xem trang
- Lần truy cập sự kiện
- Lượt truy cập thương mại điện tử
- Tương tác xã hội đạt được
- Lần truy cập ngoại lệ
- Lần truy cập thời gian của người dùng
- Lượt truy cập màn hình (đối với ứng dụng)

Các lượt truy cập được thay thế bằng các sự kiện trong Google Analytics 4, nghĩa là bạn có thể thu thập dữ liệu cho bất cứ điều gì bạn muốn. Bạn không còn bị hạn chế đối với các tùy chọn được xác định trước này. Điều này đưa chúng ta đến chủ đề tiếp theo.

### 3. Bạn có thể theo dõi những gì bằng sự kiện trong Google Analytics 4?

Trong Google Analytics 4, bạn có thể sử dụng các sự kiện để theo dõi bất kỳ hành động hoặc thông tin nào bạn muốn. Từ các trang mọi người xem (được theo dõi tự động) đến các lần nhấp vào nút hoặc thậm chí thông tin bạn đã thu thập trong nền tảng khác (như nền tảng tiếp thị qua email hoặc CRM của bạn). Bạn có thể gửi dữ liệu tới Google Analytics bằng cách sử dụng sự kiện.

Chúng tôi sẽ đề cập đến những cách khác nhau mà bạn có thể sử dụng sự kiện ngay lập tức nhưng đây là một số ví dụ về những gì bạn có thể theo dõi bằng sự kiện:

- Các trang mọi người tải trên trang web của bạn
- Hành động mọi người thực hiện trong một trang
- Các yếu tố mọi người đã nhấp vào
- Thông tin từ URL của trang
- Chi tiết giao dịch và sản phẩm
- Các phần tử hiển thị trên trình duyệt
- Thông tin chi tiết bạn đã thu thập về người dùng

Có rất nhiều cách để sử dụng sự kiện và điều đó tùy thuộc vào doanh nghiệp, đối tượng, mục tiêu của bạn cũng như loại báo cáo và phân tích mà bạn muốn thực hiện.

### 4. Thông số sự kiện trong Google Analytics 4

Sự kiện có thể được gửi tới Google Analytics kèm theo thông số. Tham số là những thông tin bổ sung gắn liền với sự kiện. Ví dụ: sự kiện page_view được gửi đến báo cáo của bạn với thông số `page_location` và `page_referrer`. Tham số page_location cho phép bạn xem URL của trang mà ai đó đã xem và tham số page_referrer cho phép bạn xem URL của trang trước đó họ đã xem.

Đây là sự kiện page_view trông như thế nào trong Google Analytics, cùng với các thông số:

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events.gif "Google Analytics 4")

Google Analytics sẽ tự động gửi thông số theo từng sự kiện. Chúng có thể bao gồm:

- Thông số `ga_session_id` bao gồm mã nhận dạng duy nhất do Google Analytics chỉ định cho phiên của người dùng.
- Tham số `page_location` gửi URL của trang hiện đang được xem.
- Tham số `page_title` gửi tiêu đề của trang hiện đang được xem.
- Tham số `page_referrer` gửi URL mà ai đó đã xem trước trang hiện tại. Điều này có thể bao gồm các trang khác trên trang web của bạn hoặc trang web của bên thứ ba (nếu ai đó nhấp qua trang web của bạn từ một trang web khác).

Đối với các sự kiện được Google Analytics tự động theo dõi, các thông số bổ sung cũng được gửi. Điều này đưa chúng ta đến các sự kiện tự động.

### 5. Sự kiện tự động trong Google Analytics 4

Khi bạn thêm thẻ Google Analytics 4 vào trang web của mình, thẻ này sẽ tự động theo dõi một số sự kiện khi ai đó xem một trang. Ví dụ: Google Analytics sẽ tự động theo dõi sự kiện khi ai đó dành ít nhất 10 giây trên trang web của bạn.

Các sự kiện được theo dõi tự động bao gồm:

- Sự kiện `first_visit` được thu thập vào lần đầu tiên ai đó truy cập trang web của bạn. Sự kiện này cũng được sử dụng để tính chỉ số 'Người dùng mới' trong báo cáo của bạn.
- Sự kiện `page_view` được sử dụng để báo cáo về trang mà người dùng đang xem.
- Sự kiện `session_start` được sử dụng để xác định thời điểm phiên của người dùng bắt đầu. Sự kiện session_start mới được kích hoạt khi có khoảng thời gian không hoạt động là 30 phút.
- Sự kiện `user_engagement` có thể được thu thập định kỳ và dùng để báo cáo khi ai đó đã dành ít nhất 10 giây trên trang web của bạn.

Không thể tắt hoặc vô hiệu hóa những sự kiện tự động này. Chúng là những thành phần quan trọng cần thiết cho Google Analytics, vì vậy bạn sẽ tìm thấy chúng trong tất cả thuộc tính Google Analytics 4.

### 6. Đo lường nâng cao

Ngoài các sự kiện tự động mà chúng ta vừa đề cập, bạn còn có tùy chọn sử dụng tính năng Đo lường nâng cao để tự động thu thập dữ liệu bổ sung. Tính năng Đo lường nâng cao được định cấu hình cho từng luồng dữ liệu dùng để gửi dữ liệu đến Google Analytics.

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-2.gif "Google Analytics 4")

Cách tốt nhất để nghĩ về tính năng Đo lường nâng cao là tính năng này cho phép bạn theo dõi các sự kiện tự động không bắt buộc (trong khi các sự kiện tự động mà chúng tôi đề cập trước đây là bắt buộc). Vì vậy, với tính năng Đo lường nâng cao, bạn có thể chọn 'bật' hoặc 'tắt' các sự kiện tự động cụ thể tùy thuộc vào nội dung bạn muốn thấy trong báo cáo của mình.

Tính năng Đo lường nâng cao cho phép bạn tự động theo dõi một hoặc nhiều hành động sau:

- `Scrolls` dành cho những người cuộn ít nhất 90% trang.
- `Outbound clicks` từ trang web của bạn đến các trang web khác.
- `Site search` cho các từ khóa được nhập vào chức năng tìm kiếm trên trang web của bạn.
- `Video engagement` của những người xem video YouTube được nhúng.
- `Files downloads` cho những người tải xuống tệp từ trang web của bạn.

Những hành động này được theo dõi bằng cách sử dụng các sự kiện sau trong báo cáo Google Analytics của bạn:

- Sự kiện `click` được thu thập khi ai đó nhấp vào liên kết ngoài.
- Sự kiện `file_download` được thu thập khi ai đó nhấp để tải xuống tệp từ trang web của bạn. Sự kiện được kích hoạt cho các định dạng tệp phổ biến, bao gồm các phần mở rộng tệp sau: pdf, xls, xlsx, doc, docx, txt, csv, key, ppt, pkg, zip, Mov, mp4, mp3, wav, v.v.
- Sự kiện `scroll` được thu thập khi ai đó cuộn 90% trang.
- Sự kiện `video_start` khi ai đó bắt đầu phát video YouTube được nhúng.
- Sự kiện `video_progress` khi 10%, 25%, 50% và 75% thời lượng video được phát.
- Sự kiện `video_complete` khi video kết thúc.
- Sự kiện `view_search_results` khi mọi người xem một trang có tham số truy vấn là 'q', 's', 'tìm kiếm', 'truy vấn' hoặc 'từ khóa'.

Tính năng Đo lường nâng cao cũng cung cấp các tùy chọn cài đặt nâng cao cho các sự kiện xem trang và sự kiện tìm kiếm trang web được thu thập tự động. Đối với lượt xem trang, bạn có thể tắt tùy chọn 'Thay đổi trang dựa trên sự kiện lịch sử trình duyệt'.

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-3.gif "Google Analytics 4")

Theo mặc định, tùy chọn này sẽ tự động theo dõi lượt xem trang khi URL của trang thay đổi mà không tải lại trang hoặc nếu nội dung được tải vào trang hiện có mà không tải lại trang. Ví dụ: nếu JavaScript được sử dụng để bao gồm nội dung bổ sung trên một trang. Nó đang tìm kiếm các sự kiện lịch sử trong trình duyệt.

Tùy chọn khác mà bạn có thể điều chỉnh trong Đo lường nâng cao là cấu hình cho sự kiện Tìm kiếm trang web.

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-4.gif "Google Analytics 4")

Ngoài các tham số truy vấn mặc định, bạn cũng có thể điều chỉnh các tham số truy vấn mà Google Analytics sử dụng để xác định từ khóa mà mọi người đang sử dụng để tìm kiếm trong trang web của bạn. Và bạn cũng có tùy chọn thêm các tham số truy vấn bổ sung để thu thập thêm thông tin chi tiết.

Ví dụ: nếu chức năng tìm kiếm của bạn cho phép mọi người tinh chỉnh tìm kiếm của họ bằng cách chọn danh mục tìm kiếm, bạn có thể thêm danh mục này vào 'Tham số truy vấn bổ sung'.

Nếu bạn mới bắt đầu, tôi khuyên bạn nên xem video về [cách bắt đầu với Google Analytics 4](https://youtu.be/iJyGEuiIjOk) về Đo lường nâng cao.

### 7. Sự kiện được đề xuất trong Google Analytics 4

Được rồi, chúng tôi đã đề cập đến các sự kiện được tự động theo dõi trong báo cáo của bạn, nhưng nếu bạn muốn theo dõi điều gì khác thì sao? Một cái gì đó nhiều hơn một chút, à, tùy chỉnh?

Nơi tốt nhất để bắt đầu là xem lại [danh sách các sự kiện được đề xuất của Google](https://support.google.com/analytics/answer/9267735). Danh sách các sự kiện được đề xuất của Google được thiết kế nhằm cung cấp cho bạn điểm khởi đầu cho bất kỳ sự kiện tùy chỉnh nào bạn muốn theo dõi trong Google Analytics 4. Chúng được nhóm theo ngành nhưng bạn có thể sử dụng bất kỳ sự kiện được đề xuất nào phù hợp với nhu cầu của mình. Các sự kiện được đề xuất được đưa ra cho:

- Sự kiện áp dụng cho tất cả thuộc tính
- Sự kiện bán hàng trực tuyến
- Sự kiện dành cho trò chơi

Ví dụ: nếu xem xét đề xuất cho các trang web (và ứng dụng) bán đồ trực tuyến, chúng ta sẽ thấy `generate_lead` được đưa vào danh sách sự kiện. Tuy nhiên, chúng tôi không cần phải điều hành một trang web thương mại điện tử để sự kiện này trở nên hữu ích. Bất kỳ trang web nào muốn thu hút khách hàng tiềm năng đều nên sử dụng sự kiện này để báo cáo số lượng người nhập thông tin liên hệ của họ.

Điều chính cần nhớ là bạn có thể sử dụng bất kỳ sự kiện nào được đề xuất trên trang web của mình nếu chúng phù hợp.

Lựa chọn hàng đầu của tôi từ danh sách các sự kiện được đề xuất bao gồm:

- Sự kiện `select_content` để theo dõi các hành động trong một trang
- Sự kiện `select _promotion` để theo dõi số lần nhấp vào ưu đãi đặc biệt
- Sự kiện `view_promotion` để hiểu số lần hiển thị của một ưu đãi đặc biệt
- Sự kiện `generate_lead` để theo dõi số lượng khách hàng tiềm năng bạn đã thu hút được
- Sự kiện `view_item` để hiểu thời điểm mọi người xem các sản phẩm cụ thể
- Sự kiện `add_to_cart` để theo dõi những người thêm mặt hàng vào giỏ hàng của họ
- Sự kiện `purchase` hàng cho các giao dịch thương mại điện tử thành công

Cùng với tên sự kiện được đề xuất, Google cũng cung cấp các thông số đề xuất cho từng sự kiện này. Sau khi tìm thấy tên sự kiện cho những gì bạn cần theo dõi, bạn có thể chọn từ các thông số được đề xuất để gửi chi tiết bổ sung tới báo cáo của mình.

Nếu bạn muốn tìm hiểu thêm về các sự kiện được đề xuất, hãy xem hướng dẫn của tôi về [theo dõi nhấp chuột, nút và biểu mẫu](https://youtu.be/gn5aEaD_P9k). Trong video, tôi chỉ cho bạn cách theo dõi các yếu tố này và bạn sẽ thấy các sự kiện (và thông số) được đề xuất đang được định cấu hình trong Trình quản lý thẻ của Google.

> [Google Tag Manager Tutorial // Lesson 7 // Bonus Tips and Resources](https://youtu.be/gn5aEaD_P9k)

### 8. Sự kiện tùy chỉnh trong Google Analytics 4

Nếu bạn đã xem lại các sự kiện được theo dõi tự động (bao gồm cả tùy chọn Đo lường nâng cao) và đã kiểm tra danh sách các sự kiện được đề xuất thì tùy chọn cuối cùng là tạo sự kiện tùy chỉnh. Đây là nơi bạn quyết định cách đặt tên cho sự kiện của mình.

Bạn nên hướng tới một quy ước đặt tên nhất quán. Và lý tưởng nhất là nó phải tuân theo tên sự kiện do Google đề xuất. Điều này sẽ giúp mọi thứ rõ ràng và hợp lý trong báo cáo của bạn.

Ví dụ: bạn có thể cho phép mọi người xếp hạng sản phẩm trên trang web của mình. Sau đó, bạn có thể tạo một sự kiện mới có tên là `product-rating` để thu thập các lựa chọn xếp hạng của mọi người. Mặc dù bạn có thể đặt tên cho sự kiện của mình theo bất kỳ tên nào bạn thích nhưng tốt hơn hết bạn nên tuân theo quy ước đặt tên của Google.

Nếu quay lại các [sự kiện được đề xuất](#7-sự-kiện-được-đề-xuất-trong-google-analytics-4), chúng ta sẽ thấy quy ước đặt tên cho các sản phẩm bao gồm `view_item` và `select_item`, vì vậy chúng ta sẽ thấy hành động hoặc hành vi được sử dụng trước tiên, sau đó là dấu gạch dưới, sau đó là 'item'. Điều này không hoàn toàn phù hợp với sự kiện tùy chỉnh của chúng tôi về `product-rating`. Thay vào đó, có lẽ chúng ta nên xem xét một sự kiện tùy chỉnh có tên `rate_item` để tuân theo quy ước đặt tên tương tự với các sự kiện khác đã có sẵn trong báo cáo của chúng tôi.

Sau đó, bạn có thể thực hiện theo cách tiếp cận tương tự cho bất kỳ thông số nào bạn gửi cùng với sự kiện tùy chỉnh của mình. Ví dụ: chúng tôi sẽ sử dụng các thông số được đề xuất như items và item_id cũng như xếp hạng thông số tùy chỉnh (hoặc tương tự) cho xếp hạng thực tế mà những người đã chọn.

Điều này có nghĩa là cuối cùng chúng tôi sẽ gửi sự kiện sau tới Google Analytics cho người đã xếp hạng sản phẩm 5/5:

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-5.png "Google Analytics 4")

Và nếu bạn muốn xem các thông số sự kiện trong báo cáo của mình, bạn cũng sẽ cần phải đăng ký chúng dưới dạng thứ nguyên hoặc chỉ số tùy chỉnh. Chúng tôi sẽ đề cập đến việc [đăng ký các định nghĩa tùy chỉnh](#13-báo-cáo-về-sự-kiện-của-bạn-trong-google-analytics-4) sau trong bài đăng này.

### 9. Gửi sự kiện tới Google Analytics 4

Có nhiều cách khác nhau để bạn có thể tạo sự kiện mới và gửi chúng đến Google Analytics 4. Tùy chọn đầu tiên là tạo sự kiện mới dựa trên sự kiện hiện có. Ví dụ: nếu bạn muốn tạo sự kiện cho những người xem một trang cảm ơn cụ thể trên trang web của bạn. Bạn có thể tạo sự kiện mới bằng sự kiện `page_view` hiện có như thế này:

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-6.gif "Google Analytics 4")

Sự kiện mới này sẽ được báo cáo mỗi khi thông số `page_location` từ sự kiện `page_view` hiện có chứa `thank-you`.

Nếu bạn không thể căn cứ sự kiện mới của mình vào sự kiện đã được gửi tới Google Analytics, bạn có thể tạo thẻ sự kiện mới trong Trình quản lý thẻ của Google. Điều này cho phép bạn gửi các sự kiện mới cho bất kỳ hành động nào diễn ra trên trang web của bạn. Chúng tôi sẽ xem xét tùy chọn này trong giây lát.

Bạn cũng có thể gửi sự kiện bằng cách sửa đổi mã theo dõi Google Analytics (gtag.js). Tuy nhiên, tôi khuyên bạn nên sử dụng Trình quản lý thẻ của Google cho các sự kiện tùy chỉnh. Điều này mang đến cho bạn giải pháp quản lý thẻ mạnh mẽ giúp bạn kiểm soát các thẻ của mình ở cấp độ toàn trang web thay vì mã hóa cứng các sự kiện riêng lẻ. Vì lý do này, chúng tôi sẽ bỏ qua phiên bản mã theo dõi cho các sự kiện nhưng bạn có thể xem một ví dụ trên [Google Developers](https://developers.google.com/analytics/devguides/collection/ga4/events#example).

### 10. Tạo sự kiện mới trong giao diện

Để tạo sự kiện mới dựa trên sự kiện hiện có, bạn cần có quyền chỉnh sửa trong Google Analytics. Sau đó, bạn có thể điều hướng đến '`Events`' và chọn '`Create Event`' ở góc trên bên phải.

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-7.png "Google Analytics 4")

Sau khi chọn luồng dữ liệu chứa sự kiện hiện có, bạn có thể đặt tên cho sự kiện mới, nhập các điều kiện bạn muốn sử dụng để so khớp, sau đó chọn xem bạn có muốn sao chép (hoặc sửa đổi) các thông số cho sự kiện mới của mình hay không.

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-8.gif "Google Analytics 4")

Khi các điều kiện cho sự kiện mới của bạn khớp với sự kiện sắp tới hiện có, bạn sẽ bắt đầu thấy sự kiện mới của mình trong báo cáo 'Sự kiện'. Đây là một ví dụ:

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-9.png "Google Analytics 4")

Bây giờ chúng ta có thể thấy rằng sự kiện `generate_lead` mới được đưa vào báo cáo của chúng ta.

### 11. Sửa đổi sự kiện trong giao diện

Ngoài việc tạo sự kiện mới, bạn cũng có thể sửa đổi các sự kiện hiện có. Tùy chọn này cho phép bạn sửa đổi các sự kiện, thông số và giá trị trước khi chúng có sẵn trong báo cáo của bạn.

Để sửa đổi các sự kiện sắp tới, hãy điều hướng đến 'Sự kiện' và chọn 'Sửa đổi sự kiện' ở góc trên bên phải.

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-10.png "Google Analytics 4")

Bạn sẽ cần chọn luồng dữ liệu bao gồm sự kiện bạn muốn sửa đổi, đặt tên cho sửa đổi, nhập điều kiện và thực hiện sửa đổi. Trong ví dụ sau, chúng tôi đang sửa đổi sự kiện `click`, sự kiện này được sử dụng tự động để theo dõi các liên kết ngoài:

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-11.gif "Google Analytics 4")

Từ nay trở đi, sự kiện `click` sẽ được báo cáo là `outbound_link`.

### 12. Gửi sự kiện bằng Trình quản lý thẻ của Google

Cách tốt nhất để gửi sự kiện tùy chỉnh đến Google Analytics 4 là sử dụng Trình quản lý thẻ của Google. Bạn có thể tạo thẻ mới bằng loại thẻ "GA4 Event":

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-12.gif "Google Analytics 4")

Sau đó, bạn có thể đặt tên cho sự kiện và thêm thông số (và giá trị) mà bạn muốn gửi đến báo cáo của mình. Ví dụ này sẽ gửi một sự kiện khi mọi người nhấp vào biểu ngữ quảng cáo nổi bật trên trang web:

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-13.gif "Google Analytics 4")

Nếu bạn muốn tìm hiểu thêm về cách tạo các loại thẻ này, tôi khuyên bạn nên xem loạt bài hướng dẫn về [Trình quản lý thẻ của Google](https://youtu.be/4nXYvFXzxV4?list=PL1vNrn711L8SnLqvJ_W0sofsVST7ldXXV) trên YouTube và xem [Khóa học về Trình quản lý thẻ của Google](https://www.lovesdata.com/courses/google-tag-manager) của tôi.

### 13. Báo cáo về sự kiện của bạn trong Google Analytics 4

Điều quan trọng nhất cần chỉ ra là nếu bạn muốn xem giá trị của các thông số bạn đã gửi cùng với sự kiện của mình, bạn sẽ cần phải đăng ký chúng trong Google Analytics. Nếu bạn không đăng ký tham số, bạn sẽ không thấy chúng trong báo cáo của mình.

Để đăng ký thông số, hãy điều hướng đến '`Custom Definitions`', chọn '`Custom Dimensions`' hoặc '`Custom Metrics`', sau đó chọn '`Create`'.

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-14.png "Google Analytics 4")

Thứ nguyên tùy chỉnh thường được sử dụng để báo cáo thông tin dựa trên văn bản. Ví dụ: tên Quốc gia hoặc URL của liên kết mà ai đó đã nhấp vào. Để so sánh, số liệu tùy chỉnh được sử dụng để báo cáo giá trị số, như số lượng hoặc phần trăm. Ví dụ: nếu bạn đang gửi giá trị đô la dưới dạng tham số thì bạn sẽ đăng ký giá trị này dưới dạng số liệu.

Đối với một thứ nguyên, bạn sẽ cần đặt tên cho nó, chọn xem bạn muốn nó gắn với sự kiện riêng lẻ (hoặc được gán cho người dùng), nhập mô tả rồi chọn tên của thông số bạn muốn đăng ký.

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-15.gif "Google Analytics 4")

Sau khi đăng ký thông số, bạn sẽ tìm thấy thông số đó trong các báo cáo Google Analytics 4 về sau. Và bạn cũng sẽ có thể sử dụng nó khi tạo báo cáo tùy chỉnh (trong 'Phân tích' và sau đó là 'Trung tâm phân tích').

Chúng tôi sẽ trình bày các báo cáo chi tiết hơn trong các khóa học GA4 của tôi nếu bạn muốn tìm hiểu thêm.

### 14. Chuyển đổi dựa trên sự kiện

Khi các sự kiện có sẵn trong Google Analytics, bạn có thể kích hoạt chúng dưới dạng chuyển đổi trong giao diện. Điều này cho phép bạn xác định các hành động quan trọng dưới dạng chuyển đổi. Để thực hiện việc này, hãy điều hướng đến 'Tất cả sự kiện' rồi sử dụng nút chuyển đổi 'Đánh dấu là chuyển đổi' ở bên phải.

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-16.png "Google Analytics 4")

Khi bạn đã đánh dấu một sự kiện là chuyển đổi, sự kiện đó sẽ được đưa vào báo cáo 'Chuyển đổi'.

Điều chính cần làm nổi bật là sự kiện này sẽ được báo cáo dưới dạng chuyển đổi trong tương lai. Và trong một số trường hợp, bạn có thể cần tạo một sự kiện mới trước khi bật sự kiện đó làm chuyển đổi (như chúng tôi đã đề cập trước đó trong bài đăng này trong phần tạo sự kiện ). Ví dụ: nếu bạn muốn theo dõi một trang cảm ơn riêng lẻ trên trang web của mình dưới dạng chuyển đổi thì việc bật sự kiện 'page_view' làm chuyển đổi sẽ có nghĩa là TẤT CẢ các trang của bạn sẽ được coi là một chuyển đổi.

Tìm hiểu thêm về cách định cấu hình lượt chuyển đổi trong Google Analytics 4 để có hướng dẫn đầy đủ hoặc xem hướng dẫn này:

> [Google Analytics 4 Conversion Tracking // How to setup and track conversions in GA4 // 2020 Tutorial](https://youtu.be/OD6kj7awY9s)

### 15. Liên kết các sự kiện Universal Analytics với các sự kiện Google Analytics 4

Nếu bạn đang sử dụng tính năng theo dõi sự kiện với Universal Analytics thì tôi khuyên bạn nên ghi lại các sự kiện hiện tại. Để bắt đầu, bạn có thể kiểm tra báo cáo sự kiện trong thuộc tính Universal Analytics của mình bằng cách chuyển đến "Hành vi", sau đó đến "Sự kiện" rồi đến "Sự kiện hàng đầu".

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-17.png "Google Analytics 4")

Sau đó, bạn nên kiểm tra xem liệu có bất kỳ sự kiện nào trong số này sẽ được thay thế bằng tính năng theo dõi tự động có sẵn trong Google Analytics 4 hay không (đọc phần mà chúng tôi đã đề cập đến [Đo lường nâng cao]((#6-đo-lường-nâng-cao))). Nếu tất cả các sự kiện của bạn từ Universal Analytics được theo dõi tự động thì bạn sẽ sẵn sàng. Ví dụ: nếu bạn đã triển khai các sự kiện Universal Analytics để theo dõi các video YouTube được nhúng thì Đo lường nâng cao sẽ tự động xử lý việc này cho bạn.

Tuy nhiên, nếu có những sự kiện không được theo dõi tự động thì bạn cần tạo sự kiện được đề xuất hoặc sự kiện tùy chỉnh. Bạn cần dành thời gian suy nghĩ về cách chuyển các sự kiện của mình từ Universal Analytics sang các sự kiện trong Google Analytics 4.

Ví dụ: bạn có thể đã triển khai các sự kiện để theo dõi tiện ích trò chuyện trên trang web của mình. Đây là cách bạn có thể đặt tên cho một sự kiện:

- `Event category`: Tiện ích trò chuyện
- `Event action`: Đã mở tiện ích
- `Event label`: 
- `Event value`: 

Và sau đó, nếu ai đó gửi tin nhắn cho bạn bằng tiện ích trò chuyện, bạn có thể đã gửi một sự kiện khác cho:

- `Event category`: Tiện ích trò chuyện
- `Event action`: Đã đóng tiện ích
- `Event label`: 
- `Event value`: 

Nếu chuyển điều này sang các sự kiện trong Google Analytics 4 thì chúng tôi sẽ linh hoạt hơn. Ví dụ: chúng tôi có thể sử dụng sự kiện sau khi mọi người mở tiện ích trò chuyện:

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-18.png "Google Analytics 4")

Và sự kiện này khi mọi người hoàn tất cuộc trò chuyện của họ:

![Google Analytics 4](https://boxxv.github.io/img/2023/google-analytics-4-events-19.png "Google Analytics 4")

Điều này tốt hơn việc sao chép cấu trúc danh mục, hành động và nhãn trước đó từ Universal Analytics. Ngoài ra còn có cơ hội thu thập thông tin chi tiết phong phú hơn về hành động mà mọi người thực hiện và trải nghiệm của họ trên trang web của bạn.

### 16. Các giới hạn đối với Sự kiện Google Analytics 4

Có một số giới hạn khi nói đến các sự kiện Google Analytics 4. Hầu hết mọi người sử dụng Google Analytics có thể sẽ không đạt đến những giới hạn này, nhưng vì các sự kiện rất linh hoạt nên bạn nên biết các ràng buộc.

Giới hạn sự kiện:

- Bạn có thể theo dõi tới 500 sự kiện độc đáo.
- Tên của mỗi sự kiện có thể dài tối đa 40 ký tự.

Giới hạn tham số:

- Bạn có thể gửi tối đa 25 thông số với mỗi sự kiện.
- Tên của mỗi tham số có thể dài tối đa 40 ký tự và giá trị của tham số có thể dài tối đa 100 ký tự.
- Bạn có thể đăng ký tối đa 50 tham số dựa trên văn bản và tối đa 50 tham số bằng số từ các sự kiện của mình. Bạn cần đăng ký một tham số để nó có sẵn trong báo cáo của bạn. (Bạn cũng có thể đăng ký tối đa 25 tham số trong phạm vi người dùng.)

Chúng là những giới hạn quan trọng nhất cần lưu ý khi tham gia các sự kiện nhưng bạn cũng có thể xem danh sách đầy đủ [các giới hạn thu thập và cấu hình của Google](https://support.google.com/analytics/answer/9267744).

### 17. Tóm tắt thiết lập sự kiện

Trước khi bắt đầu định cấu hình các sự kiện mới trong Google Analytics 4, tôi khuyên bạn nên dành thời gian xem lại cách triển khai hiện tại và quyết định những sự kiện nào bạn cần theo dõi. Luôn luôn là một ý tưởng hay khi gắn thiết lập Google Analytics với các mục tiêu của tổ chức bạn.

Dưới đây là một số câu hỏi quan trọng cần hỏi:

#### 1. Bạn đã theo dõi các sự kiện trong Universal Analytics chưa?

Nếu đúng như vậy, hãy ghi lại các sự kiện đã được sử dụng trước khi trả lời câu hỏi tiếp theo.

Và nếu bạn không có thuộc tính Universal Analytics trong Google Analytics, bạn có thể chuyển thẳng sang câu hỏi tiếp theo.

#### 2. Tính năng theo dõi sự kiện tự động (bao gồm cả Đo lường nâng cao) đã đủ chưa?

Nếu bạn muốn theo dõi các lần cuộn, số lần nhấp ra ngoài, tìm kiếm trang web, video YouTube được nhúng hoặc tải xuống tệp, tất cả chúng đều có thể được theo dõi tự động. Bạn sẽ cần kiểm tra cấu hình Đo lường nâng cao cho từng luồng dữ liệu của mình trong Google Analytics.

Nếu có những hành vi hoặc thông tin khác mà bạn muốn xem trong báo cáo của mình thì đã đến lúc trả lời câu hỏi tiếp theo.

#### 3. Các sự kiện được đề xuất có bao gồm những gì bạn muốn theo dõi không?

Xem lại phần [sự kiện được đề xuất](#7-sự-kiện-được-đề-xuất-trong-google-analytics-4) trong bài đăng này. Xem liệu sự kiện bạn muốn theo dõi có thể sử dụng một trong các quy ước đặt tên được đề xuất hay không. Nếu một trong những sự kiện được đề xuất có hiệu quả, hãy chuyển thẳng sang câu hỏi số năm.

Và nếu sự kiện của bạn không phù hợp với bất kỳ sự kiện nào được đề xuất, bạn sẽ cần đặt tên cho các sự kiện tùy chỉnh của mình rồi chuyển sang câu hỏi tiếp theo.

#### 4. Các sự kiện tùy chỉnh của bạn có tuân theo quy ước đặt tên của Google không?

Lý tưởng nhất là các sự kiện tùy chỉnh của bạn sẽ tuân theo quy ước đặt tên của Google. Xem lại phần [sự kiện tùy chỉnh](#8-sự-kiện-tùy-chỉnh-trong-google-analytics-4) trong bài đăng này để biết ví dụ. Sau đó là lúc triển khai theo dõi sự kiện trên trang web của bạn.

#### 5. Bạn có thể sử dụng trình kích hoạt hiện có trong Trình quản lý thẻ của Google để kích hoạt thẻ sự kiện mới không?

Sau khi bạn hài lòng với cách đặt tên cho sự kiện và các thông số của sự kiện, đã đến lúc tạo thẻ sự kiện. Trong hầu hết các trường hợp, bạn nên nhắm đến việc triển khai sự kiện bằng Trình quản lý thẻ của Google. Nếu bạn đã triển khai các thẻ khác trên trang web của mình thì bạn nên dành thời gian để xem liệu trình kích hoạt hiện có có thể được sử dụng với thẻ sự kiện mới hay không.

#### 6. Liệu sự kiện bạn đang muốn theo dõi có cung cấp những hiểu biết có giá trị không?

Cuối cùng, bạn cần phải đảm bảo rằng những gì bạn theo dõi phù hợp với mục tiêu của mình. Bạn có thể theo dõi hầu hết mọi thứ trên trang web (hoặc trong ứng dụng của mình), vì vậy hãy dành chút thời gian để tự hỏi liệu dữ liệu có cung cấp thông tin chi tiết có giá trị hay không. Nếu không, hãy cân nhắc việc bỏ qua sự kiện cụ thể đó.


## Cách xem thông số sự kiện trong báo cáo Google Analytics 4


-----
Tham khảo:
- [Google Analytics 4 Event Tracking: Your Complete Guide](https://www.lovesdata.com/blog/google-analytics-4-events)
- [How to See Event Parameters in Google Analytics 4 Reports](https://www.optizent.com/how-to-see-event-parameters-in-google-analytics-4-reports/)