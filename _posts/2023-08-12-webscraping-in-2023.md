---
layout: post
title: Crawling dữ liệu từ website
subtitle: Web scraping in 2023
author: "Deepak Bhardwaj"
tags:
- Web Scraping
- Web Data Scraping
- Data Scraping
- Crawl Data
- Data Mining
- Data Extraction
- Technology
---

![Web Scraping](https://boxxv.github.io/img/2023/9LFFMbOMFJ3P7xs2yGHrDQukzea6scjQ8E20oyx2.jpeg "Web Scraping")

Dữ liệu đã và đang trở thành một phần chính trong chiến lược tăng trưởng của mọi công ty. Các dữ liệu này bao gồm:
    Dữ liệu công khai.
    Dữ liệu thông tin người dùng.
    Dữ liệu của đối thủ cạnh tranh.
    Dữ liệu thị trường chứng khoán.
    Dữ liệu sản phẩm.
    Dữ liệu công việc.
    Dữ liệu dự báo thời tiết v...v...

## Crawl là gì? Web Crawler là gì?

`Crawl` là cào dữ liệu (`Crawl Data`)

Từ **crawl** (thu thập thông tin) trong cụm Trình thu thập thông tin web (`Web crawlers`) là thuật ngữ kỹ thuật dùng để chỉ quá trình tự động truy cập website và lấy dữ liệu thông qua một chương trình phần mềm.

Internet không ngừng thay đổi và mở rộng. Vì không thể biết tổng số website có trên Internet, web crawlers bắt đầu từ một danh sách các URL đã biết. Trước tiên, chúng thu thập dữ liệu webpage tại các URL đó. Từ các page này, chúng sẽ tìm thấy các siêu liên kết đến nhiều URL khác và thêm các liên kết mới tìm được vào danh sách các trang cần thu thập thông tin tiếp theo.

![Web Scraping](https://boxxv.github.io/img/2023/what-is-web-sraping-parsehub.jpeg "Web Scraping")

#### Tại sao Web Crawlers được gọi là ‘spiders’?

Internet, hoặc ít nhất là phần mà hầu hết người dùng truy cập, còn được gọi là World Wide Web – trên thực tế, đó là nơi xuất phát phần “www” của hầu hết các URL trang web. 

Việc gọi các bot của công cụ tìm kiếm là “spiders” là điều hoàn toàn tự nhiên, bởi vì chúng thu thập dữ liệu trên khắp các trang Web, giống như những con nhện bò trên mạng nhện.


## Scraping data là gì?

Scraping dữ liệu không nhất thiết phải liên quan đến web. Scraping có thể đề cập đến việc trích xuất thông tin từ một hệ thống cục bộ, cơ sở dữ liệu chung hoặc thậm chí từ internet. Web Scaping cũng thực hiện việc tìm kiếm và thu thập thông tin nhưng khác với Web Crawling, Web Scraping không thu thập toàn bộ thông tin của một trang web mà chỉ thu thập những thông tin cần thiết, phù hợp với mục đích của người dùng. Trong WebScraping chúng ta cũng phần nào sử dụng WebCrawler để thu thập dữ liệu, kết hợp với Data Extraction (trích xuất dữ liệu) để tập trung vào các nội dung cần thiết.

Ví dụ như đối với trang amazon.com, Web Crawling sẽ thu thập toàn bộ nội dung của trang web này (tên các sản phẩm, thông tin chi tiết, bảng giá, hướng dẫn sử dụng, các reviews và comments về sản phẩm,…). Tuy nhiên Web Scaping có thể chỉ thu thập thông tin về giá của các sản phẩm để tiến hành so sánh giá này với các trang bán hàng online khác.

#### Sự khác biệt giữa Web Crawling và Web Scraping

`Data scraping`, `web scraping` hoặc `content scraping` là hành động một bot tải xuống nội dung trên một trang web mà không được cho phép bởi chủ website, thường với mục đích sử dụng nội dung đó cho mục đích xấu.

Web scraping thường được target nhiều hơn web crawling. Web scrapers có thể chỉ theo dõi một số trang websites cụ thể, trong khi web crawlers sẽ tiếp tục theo dõi các liên kết và thu thập thông tin các trang liên tục.

Bên cạnh đó, web scraper bots có thể qua mặt máy chủ dễ dàng, trong khi web crawlers, đặc biệt là từ các công cụ tìm kiếm lớn, sẽ tuân theo tệp robots.txt và gia hạn các yêu cầu của chúng để không đánh lừa máy chủ web.

#### Anti-bot detection

Khi cào dữ liệu thì bạn có thể gặp những websites sử dụng các cơ chế chặn bot (dĩ nhiên họ sẽ ko chặn các Search engine nổi tiếng như Google, Bing,... rồi). Họ có thể sẽ sử dụng các cơ chế:

- Phát hiện user-agents truy cập nhiều —> Giải pháp: dùng user-agent khác nhau hoặc dùng SE agents nổi tiếng cho mỗi lần request. Danh sách 450 User-Agents download tại http://cafemmo.club/threads/chia-se-danh-sach-user-agent-thong-dung-nhat.1818/
- Phát hiện IPs truy cập nhiều, giả sử 5 requests/s --> Giải pháp: dùng các dịch vụ IP rotator cho mỗi lần request. Mình dùng stormproxies.com.
- Phát hiện người dùng thật qua Javascript, đa số bot ko hỗ trợ JS mà --> Giải pháp: dùng headless browser như Splash, Selenium, PhantomJS, Puppeter,... Có khá nhiều sites mình gặp dùng JS để detect robot như similarweb.com,...
- Sử dụng honeypot traps: ví dụ như các links bẩy đính kèm display:none, visibility: hidden,... --> cài đặt cơ chế phát hiện các traps thôi ^^
- Sử dụng cookie, captcha để chặn, đa số sites dùng Cloudflare để chặn bot --> có vài script bypass Cloudflare rồi, sử dụng như https://github.com/Anorov/cloudflare-scrape (script này bypass cookie của Cloudflare nhưng chưa có cơ chế bypass captcha của Cloudflare nhé).

#### Ghi kết quả dữ liệu (scraped data) quá nhiều

Khi bạn cào dữ liệu với nhiều spiders, ví dụ 1 spider cào được 1 record/2s, và bạn có 20 spiders thì bạn có 10 records/s, lúc này việc ghi dữ liệu quá nhiều và liên tục vào DB sẽ làm cho DB của bạn quá tải và giảm hiệu năng, có thể ảnh hưởng đến hiệu năng hoạt động. Khi đó, bạn nên cân nhắc dùng:

- Bulk insert query: tức spider chỉ cần thực hiện 1 query để insert nhiều records
- Bulk import file: tức là spider ghi dữ liệu vào 1 file với 1000 dữ liệu chẳng hạn, sau đó bạn sử dụng lệnh import file đó vào DB. Ví dụ: MySQL (LOAD DATA LOCAL INFILE), MongoDB (mongoimport) Các DB engines nào cũng hỗ trợ 2 dạng trên, ví dụ như MySQL, MongoDB,...

#### Cấu trúc site thay đổi

Ví dụ như site thay đổi layout, tức HTML tags thay đổi, lúc này bạn phải thay đổi các selectors để lấy đúng dữ liệu bạn cần. Trong tình huống này, spider cần có cơ chế phát hiện sự thay đổi cấu trúc site để thông báo cho chúng ta và dừng extract data của site đó. Khi đó, mỗi site ta cần hỗ trợ nhiều schemas để extract dữ liệu hơn.

#### Cách ngăn chặn site Scraping:

Bạn muốn ngăn chặn một công cụ ăn cắp tài sản trí tuệ của mình có thể sử dụng phương thức phát hiện các Scraping bot và giảm thiểu việc truy vấn dữ liệu

- Sử dụng công cụ phân tích
- Triển khai các challenge-based để đánh giá hành vi của người dùng nếu hỗ trợ cookie và javascript.
- Lựa chọn hành vi tiếp cận dữ liệu
- Sử dụng robots.txt để bảo vệ website trước scraping bot ( hướng dẫn các con bot thực hiện theo rules định sẵn ). Tuy nhiên phương pháp này không được 

![Web Scraping](https://boxxv.github.io/img/2023/0006f3f6-1ea1-4413-baa0-58a9862661f9.webp "Web Scraping")


## Crawl data - cào dữ liệu có gì khó?




-----
Tham khảo:
- [Crawling dữ liệu từ website, tìm hiểu về ScrapingWeb](https://viblo.asia/p/crawling-du-lieu-tu-website-tim-hieu-ve-scrapingweb-1VgZvGo9lAw)
- [Tìm hiểu về Web Scraping Bot là gì?](https://securitydaily.net/tim-hieu-ve-web-scraping-bot-la-gi/)
- [Web Data Crawling vs Web Data Scraping](https://www.promptcloud.com/blog/data-scraping-vs-data-crawling/)
- [Web scraping in 2023 — Breaking it down to basics](https://blog.devgenius.io/webscraping-in-2023-breaking-it-down-to-basics-programming-learning-scraping-python-web-data-science-10fa130cc8be)