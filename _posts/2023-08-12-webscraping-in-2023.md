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

Dữ liệu đã và đang trở thành một phần chính trong chiến lược tăng trưởng của mọi công ty. Các dữ liệu này bao gồm:
- Dữ liệu công khai.
- Dữ liệu thông tin người dùng.
- Dữ liệu của đối thủ cạnh tranh.
- Dữ liệu thị trường chứng khoán.
- Dữ liệu sản phẩm.
- Dữ liệu công việc.
- Dữ liệu dự báo thời tiết v...v...

![Web Scraping](https://boxxv.github.io/img/2023/9LFFMbOMFJ3P7xs2yGHrDQukzea6scjQ8E20oyx2.jpeg "Web Scraping")

## Crawl là gì? Web Crawler là gì?

`Crawl` là cào dữ liệu (`Crawl Data`)

Từ **crawl** (thu thập thông tin) trong cụm Trình thu thập thông tin web (`Web crawlers`) là thuật ngữ kỹ thuật dùng để chỉ quá trình tự động truy cập website và lấy dữ liệu thông qua một chương trình phần mềm.

Internet không ngừng thay đổi và mở rộng. Vì không thể biết tổng số website có trên Internet, web crawlers bắt đầu từ một danh sách các URL đã biết. Trước tiên, chúng thu thập dữ liệu webpage tại các URL đó. Từ các page này, chúng sẽ tìm thấy các siêu liên kết đến nhiều URL khác và thêm các liên kết mới tìm được vào danh sách các trang cần thu thập thông tin tiếp theo.


#### Tại sao Web Crawlers được gọi là ‘spiders’?

Internet, hoặc ít nhất là phần mà hầu hết người dùng truy cập, còn được gọi là World Wide Web – trên thực tế, đó là nơi xuất phát phần “www” của hầu hết các URL trang web. 

Việc gọi các bot của công cụ tìm kiếm là “spiders” là điều hoàn toàn tự nhiên, bởi vì chúng thu thập dữ liệu trên khắp các trang Web, giống như những con nhện bò trên mạng nhện.


![Web Scraping](https://boxxv.github.io/img/2023/what-is-web-sraping-parsehub.jpeg "Web Scraping")

## Scraping data là gì?

Scraping dữ liệu không nhất thiết phải liên quan đến web. Scraping có thể đề cập đến việc trích xuất thông tin từ một hệ thống cục bộ, cơ sở dữ liệu chung hoặc thậm chí từ internet. Web Scaping cũng thực hiện việc tìm kiếm và thu thập thông tin nhưng khác với Web Crawling, Web Scraping không thu thập toàn bộ thông tin của một trang web mà chỉ thu thập những thông tin cần thiết, phù hợp với mục đích của người dùng. Trong WebScraping chúng ta cũng phần nào sử dụng WebCrawler để thu thập dữ liệu, kết hợp với Data Extraction (trích xuất dữ liệu) để tập trung vào các nội dung cần thiết.

Ví dụ như đối với trang amazon.com, Web Crawling sẽ thu thập toàn bộ nội dung của trang web này (tên các sản phẩm, thông tin chi tiết, bảng giá, hướng dẫn sử dụng, các reviews và comments về sản phẩm,…). Tuy nhiên Web Scaping có thể chỉ thu thập thông tin về giá của các sản phẩm để tiến hành so sánh giá này với các trang bán hàng online khác.

### Sự khác biệt giữa Web Crawling và Web Scraping

`Data scraping`, `web scraping` hoặc `content scraping` là hành động một bot tải xuống nội dung trên một trang web mà không được cho phép bởi chủ website, thường với mục đích sử dụng nội dung đó cho mục đích xấu.

Web scraping thường được target nhiều hơn web crawling. Web scrapers có thể chỉ theo dõi một số trang websites cụ thể, trong khi web crawlers sẽ tiếp tục theo dõi các liên kết và thu thập thông tin các trang liên tục.

Bên cạnh đó, web scraper bots có thể qua mặt máy chủ dễ dàng, trong khi web crawlers, đặc biệt là từ các công cụ tìm kiếm lớn, sẽ tuân theo tệp robots.txt và gia hạn các yêu cầu của chúng để không đánh lừa máy chủ web.

### Anti-bot detection

Khi cào dữ liệu thì bạn có thể gặp những websites sử dụng các cơ chế chặn bot (dĩ nhiên họ sẽ ko chặn các Search engine nổi tiếng như Google, Bing,... rồi). Họ có thể sẽ sử dụng các cơ chế:

- Phát hiện user-agents truy cập nhiều —> Giải pháp: dùng user-agent khác nhau hoặc dùng SE agents nổi tiếng cho mỗi lần request. Danh sách 450 User-Agents download tại: [Chia sẻ danh sách User Agent thông dụng nhất](http://cafemmo.club/threads/chia-se-danh-sach-user-agent-thong-dung-nhat.1818/)
- Phát hiện IPs truy cập nhiều, giả sử 5 requests/s --> Giải pháp: dùng các dịch vụ IP rotator cho mỗi lần request. Mình dùng stormproxies.com.
- Phát hiện người dùng thật qua Javascript, đa số bot ko hỗ trợ JS mà --> Giải pháp: dùng headless browser như Splash, Selenium, PhantomJS, Puppeter,... Có khá nhiều sites mình gặp dùng JS để detect robot như similarweb.com,...
- Sử dụng honeypot traps: ví dụ như các links bẩy đính kèm display:none, visibility: hidden,... --> cài đặt cơ chế phát hiện các traps thôi ^^
- Sử dụng cookie, captcha để chặn, đa số sites dùng Cloudflare để chặn bot --> có vài script bypass Cloudflare rồi, sử dụng như https://github.com/Anorov/cloudflare-scrape (script này bypass cookie của Cloudflare nhưng chưa có cơ chế bypass captcha của Cloudflare nhé).

### Ghi kết quả dữ liệu (scraped data) quá nhiều

Khi bạn cào dữ liệu với nhiều spiders, ví dụ 1 spider cào được 1 record/2s, và bạn có 20 spiders thì bạn có 10 records/s, lúc này việc ghi dữ liệu quá nhiều và liên tục vào DB sẽ làm cho DB của bạn quá tải và giảm hiệu năng, có thể ảnh hưởng đến hiệu năng hoạt động. Khi đó, bạn nên cân nhắc dùng:

- Bulk insert query: tức spider chỉ cần thực hiện 1 query để insert nhiều records
- Bulk import file: tức là spider ghi dữ liệu vào 1 file với 1000 dữ liệu chẳng hạn, sau đó bạn sử dụng lệnh import file đó vào DB. Ví dụ: MySQL (LOAD DATA LOCAL INFILE), MongoDB (mongoimport) Các DB engines nào cũng hỗ trợ 2 dạng trên, ví dụ như MySQL, MongoDB,...

### Cấu trúc site thay đổi

Ví dụ như site thay đổi layout, tức HTML tags thay đổi, lúc này bạn phải thay đổi các selectors để lấy đúng dữ liệu bạn cần. Trong tình huống này, spider cần có cơ chế phát hiện sự thay đổi cấu trúc site để thông báo cho chúng ta và dừng extract data của site đó. Khi đó, mỗi site ta cần hỗ trợ nhiều schemas để extract dữ liệu hơn.

### Cách ngăn chặn site Scraping:

Bạn muốn ngăn chặn một công cụ ăn cắp tài sản trí tuệ của mình có thể sử dụng phương thức phát hiện các Scraping bot và giảm thiểu việc truy vấn dữ liệu

- Sử dụng công cụ phân tích
- Triển khai các challenge-based để đánh giá hành vi của người dùng nếu hỗ trợ cookie và javascript.
- Lựa chọn hành vi tiếp cận dữ liệu
- Sử dụng robots.txt để bảo vệ website trước scraping bot ( hướng dẫn các con bot thực hiện theo rules định sẵn ). Tuy nhiên phương pháp này không được 

![Web Scraping](https://boxxv.github.io/img/2023/0006f3f6-1ea1-4413-baa0-58a9862661f9.webp "Web Scraping")


# Crawl data - cào dữ liệu có gì khó?

Vai trò của dữ liệu thì chúng ta không cần bàn luận nữa. Hôm nay mình sẻ chia sẻ một vài phương pháp và khó khăn khi cào dữ liệu (crawl data) từ những phương pháp, công cụ mình đã ứng dụng và một số vấn đề gặp phải trong quá trình làm luận văn. (có 2 khái niệm là data crawling và data scraping nhưng mình chỉ nói nôn na là thu thập dữ liệu, các bạn có thể đọc thêm để phân biệt)

Cào ở dữ liệu ở đây mình đề cập là dùng một công cụ (tool) để đi thu thập dữ liệu ở một số website mà chúng ta cần, đơn thuần cũng chỉ là gởi một request HTTP/HTTPS trực tiếp hoặc dùng một browser driver truy cập đến trang đích để lấy nội dung trang về rồi tiến hành parse nội dung để lấy dữ liệu. Hầu hết các trang web đều không thể ngăn cấm việc bot ghé thăm vì trong đó có bot của các search engine như google, bing,… tuy nhiên họ cũng không thể nào cho phép truy cập thỏa mái vì điều này làm giảm hiệu năng hoặc thậm chí sập cả server. Chính vì vậy đa số các website đều quy định và tìm cách hạn chế, ngăn chặn việc crawler quá mức, thậm chí có cả bẫy (traps) để chặn crawler khiến cho việc thu thập dữ liệu của chúng ta cũng gặp không ít khó khăn.

Trước hết mình sẽ giới thiệu qua một số `tool`/`lib`/`framework` phổ biến để thực hiện thu thập dữ liệu, mặc dù việc cào dữ liệu chỉ đơn thuần là gởi request để lấy nội dung nhưng bạn cũng nên dùng thư viện sẵn có để thu thập (trừ khi các bạn muốn phát triển 1 thư viện mới) thay vì tự gởi request bằng thư viện HTTP trong các ngôn ngữ sẵn có vì các bạn sẽ phải handle rất nhiều thứ từ đa luồng, kiểm soát request, parsing,… rất tốn thời gian để viết lại. Sử dụng các thư viện sẵn có thì bạn cũng không cần lo về khả năng mở rộng, tùy biến của mình, các thư viện đa số đã thiết kế theo kiến trúc mở cung cấp các `middlewares`, `pipelines` cho người dùng tùy biến.

|  | Scrapy | Selenium |
| -- | -- | -- |
| Advantages | Bất đồng bộ chính là thứ giúp cho scrapy có hiệu năng tuyệt vời. Sử dụng rất ít RAM, CPU. Tài liệu đầy đủ, plugins rất nhiều. Thiết kế theo một kiến trúc khá tốt, dev có thể dễ dàng tùy chỉnh middlewares, pipelines và thêm các function tùy ý. | Dễ tiếp cận cho beginer. Có thể lấy được nội dung trang render bằng javascript. Có thể thao tác như một người dùng |
| Disadvantages | Hơi phức tạp cho beginer. Quá dư thừa chức năng nếu chỉ dùng cho 1 project nhỏ và đơn giản. Không thể lấy nội dung trang được render bằng js, tuy nhiên chúng ta có thể kết hợp với Splash. | Tiêu tốn nhiều tài nguyên vì nó cần đến một browser driver (tưởng tượng như bạn mở 1 tab chrome thì sẽ tốn bao nhiêu RAM, CPU). Rất chậm, nên selenium không phù hợp với một project cào dữ liệu lớn. |
| Homepage | [scrapy.org](https://scrapy.org) | [selenium.dev](https://www.selenium.dev) |

|  | Cheerio | Puppeteer |
| -- | -- | -- |
| Advantages | Hỗ trợ parse DOM giống như jquery. Bất đồng bộ, khá nhanh | Giống như selenium, puppeteer cũng sử dụng browser driver để lấy nội dung trang nên có thể lấy được nội dung các trang render bằng js và thao tác như một người dùng. |
| Disadvantages | Chỉ đơn thuần là trình phân tích (parser). Không thể lấy nội dung trang được render bằng js | Tiêu tốn RAM, CPU. Chậm |
| Homepage | [cheerio.js.org](https://cheerio.js.org) | [pptr.dev](https://pptr.dev) |

#### [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/) (BS4)

Beautiful Soup (BS4) là một thư viện phân tích cú pháp có thể sử dụng các parsers khác nhau từ đó có thể trích xuất dữ liệu từ các tài liệu HTML và XML một cách dễ dàng. Về mặc định, Beautiful Soup sử dụng parser cơ bản của Python. Mặc dù khá linh hoạt và dễ sử dụng, parser này là có hiệu năng khá kém do tốc độ xử lý khá chậm. Tin tốt là bạn hoàn toàn có thể hoán đổi trình phân tích cú pháp của nó bằng một trình phân tích cú pháp nhanh hơn nếu bạn cần cải thiện nhiều tốc độ của ứng dụng.

Sau khi phân tích các HTML cũng như XML đầu vào, Beautiful Soup cho phép chúng ta dễ dàng di chuyển, tìm kiếm, thay đổi cũng như trích xuất dữ liệu từ cây cú pháp. Cú pháp rõ ràng linh hoạt tương tự cách chúng ta tương tác với DOM bằng các thư viện JavaScript là một trong những lý do khiến Beautiful Soup trở thành một trong những công cụ phổ biến nhất cho việc thu thập dữ liệu web, bên cạnh sự mạnh mẽ của nó.

#### Selenium

Selenium là một trong những công cụ kiểm thử phần mềm tự động mã nguồn mở mạnh nhất hiện nay cho việc kiểm thử ứng dụng Web. Selenium script có thể chạy được trên hầu hết các trình duyệt như IE, Mozilla FireFox, Chrome, Safari, Opera; và hầu hết các hệ điều hành như Windows, Mac, Linux. Về cơ bản mà nói, quá trình scraping cũng tương tự như quá trình kiểm thử ứng dụng tự động bởi chúng đều thực hiện một chuỗi thao tác tương tác với các trang web một cách tự động và liên tục. Bởi vậy, Selenium thường xuyên được sử dụng nhất là khi cần thu thập từ các trang web SPA - thứ mà khó có thể thu thập được dữ liệu từ nó nếu như phần mã JavaScript của chúng không được thực thi.

#### Scrapy

Về mặt kỹ thuật, Scrapy không phải một thư viện mà là một framework phục vụ mục đích thu thập dữ liệu. Điều đó có nghĩa là bạn có thể sử dụng nó để quản lý các yêu cầu, duy trì các phiên của người dùng, theo dõi chuyển hướng và xử lý các pipelines đầu ra. Nó cũng có nghĩa là bạn có thể hoán đổi các mô-đun riêng lẻ với các thư viện duyệt web Python khác. Ví dụ: nếu bạn cần chèn Selenium để quét các trang web động, bạn có thể làm điều đó.

Hầu hết các ngôn ngữ lập trình đều có những thư viện hỗ trợ thu thập dữ liệu, tuy nhiên `Python` sẽ là ngôn ngữ  mà mình gợi ý các bạn nên chọn cho dự án thu thập dữ liệu của mình, `Scrapy` là một framework trong python hỗ trợ thu thập dữ liệu cực mạnh, hơn nữa python có hỗ trợ khá nhiều thư viện để xử lý dữ liệu.

### Nhập môn thu thập dữ liệu

Kiến trúc chung của một crawler sẽ gồm 3 phần:
1. queue chứa URL
2. downloader
3. parser

Luồng hoạt động sẽ diễn ra như sau:
- Cung cấp một URL để start (hoặc một list URL)
- Downloader tiến hành tải xuống nội dung trang
- Parser rút trích dữ liệu (store nếu cần) và đồng thời rút trích ra URL kế tiếp và thêm vào queue URL
- Quá trình sẽ lặp lại cho đến hết URL trong queue

![Web Scraping](https://boxxv.github.io/img/2023/crawler_simple.png "Web Scraping")

Để làm quen với việc thu thập dữ liệu, mình khuyên các bạn nên làm qua 10 bài thực hành trên trang [Scrapingclub](https://scrapingclub.com) (Learn Web Scraping Using Python For Free) theo bất kỳ thư viện hỗ trợ thu thập dữ liệu nào bạn muốn, solutions thì mình cũng đã làm từ lúc mình học cơ bản [https://github.com/lhsang/Spiders](https://github.com/lhsang/Spiders) (sử dụng scrapy) các bạn có thể tham khảo.

Về vấn đề thu thập thông tin để tránh vi phạm các tiêu chuẩn, quy định thì các bạn nên phân tích file `http://domain.com/robots.txt` trước khi cào, file robots.txt sẽ định quy cho biết Crawler của bạn được truy cập những trang nào, không được truy cập trang nào và thời gian delay mỗi request. Ngoài ra user-agent là một header bạn có thể tùy ý, tuy nhiên về vấn đề đạo đức nghề nghiệp các bạn không nên fake giá trị này.

Phần tiếp theo mình sẽ nói về một số khó khăn đã gặp và giải pháp trong quá trình thu thập dữ liệu phục vụ cho luận văn tốt nghiệp:

- Các trang hạn chế số lượng truy cập trong một khoảng thời gian: để tránh việc một IP làm quá tải server, các trang thường phải giới hạn số request của một IP trong một phút (thường sẽ họ sẽ cho biết thời gian deplay mỗi request trong file robots.txt), có một số lượng lớn trang cần thu thập thì môi phút vài request thì quá ít cho nhu cầu của mình và thậm chí nếu gửi nhiều hơn quy định, crawler còn có thể bị ban trong vài phút. Giải pháp là mình đã sử dụng thêm proxy server, giá proxy cũng không quá mắc (tầm $0.4 IP/tháng, khuyên các bạn không nên mua của các nhà cung cấp từ Việt Nam - người từng trải), mỗi request mình sẽ đổi IP liên tục thì sẽ tránh được ban IP. Nếu không cần thiết phải đổi IP thì ban có thể tăng thời gian DELAY_REQUEST để cách biệt các request, giảm CONCURRENT_REQUESTS (số request đồng thời) và có thể cheat nhẹ user-agent bất chấp đạo đức :))
- Nội dung trang render bằng Javascript: vì nhu cầu mình crawl nhiều nên mình chọn Scrapy, tuy nhiên scrapy lại không hỗ trợ lấy dữ liệu ở các trang render bằng js (Ajax, React,…) để biết rằng trang này có render bằng js ra nội dung không, bạn chỉ cần Ctrl+U rồi xem có nội dung html như hiển thị không, hay chỉ là một thẻ body rồi js chèn vào sau. Như đã đề cập scrapy có thể sử dụng kèm với headless browser như Splash để chờ trang web render ra nội dung và cookie, việc này làm tốn thêm một ít thời gian chờ nhưng vẫn nhanh hơn các lựa chọn khác scrapy.
- Cấu trúc trang thay đổi: đôi lúc sites thay đôỉ cấu trúc (HTML tags thay đổi), chúng ta phải xác định đúng thẻ thì mới lấy được dữ liệu. Nên cài đặt cho crawler cơ chế phát hiện cấu trúc thay đổi và thông báo để chúng ta biết và chỉnh sửa hoặc áp dụng cấu trúc mới để parse đúng dữ liệu.
- Required đủ cookie, headers: đa số các trang đều yêu cầu một số headers và cookie là phải có trong request, chúng ta có thể dùng Chrome DevTools để xem các header và cookie này, tuy nhiên ở nhiều trang headers, cookie này không được set ngay từ đầu mà trong quá trình request sẽ gởi request đến một URL khác để lấy thông tin headers, cookie hoặc ngay địa chỉ URL của bạn nhưng lần đầu là để lấy headers, cookie lần sau mới lấy nội dung (trường hợp này, nếu không có đủ headers server sẽ buộc crawler request vô hạn). Giải pháp là chúng ta phải biết quan sát mà lấy headers, cookie phù hợp để gắn vào request thôi =))
- Bất đồng bộ và multithread vẫn chưa đủ: mỗi ngày mình phải gởi hơn vài chục triệu request, scrapy hỗ trợ bất đồng bộ, tuy nhiên một process chưa đủ đáp ứng nhu cầu lớn như vậy trong một ngày, giải pháp là tăng số process lên (có thể cho chạy ở nhiều server), liên quan đến vấn đề xử lý song song các bạn phải tính toán để chia URL ra cho các process hợp lý nhất.
- Lưu trữ dữ liệu: tùy nhu cầu bạn sẽ chọn hệ quản trị cơ sở dữ liệu phù hợp, với project của mình vì nhu cầu lưu trữ lớn (hơn 11 triệu record mỗi ngày đổ vào database) và cần tốc độ truy vẫn nhanh thì mình chọn mongodb. MongoDB thuộc loại NoSQL lưu trữ theo dạng document (BSON), schema linh hoạt, không phải join, kết hợp với đánh indexes thì tốc độ khá là nhanh (dữ liệu 1 tỷ records mình có thể truy vấn dưới 1s) hơn nữa mongodb còn thiết kế để đáp ứng nhu cầu phân tán nên có thể sharding hay replication để mở rộng, tăng hiệu năng và đảm bảo tính available cho hệ thống. Vấn đề lưu xuống liên tục cũng có thể quá tải database, bạn có thể cache tạm một nơi rồi insert_many thay vì insert_one.

# Xây dựng sơ bộ một hệ thống crawler

## 1. Lấy xpath như thế nào?

Để lấy được một đoạn mã xpath như thế này:

```html
//*[@id="aspnetForm"]/div[5]/div[1]/div[1]/div[1]/div[1]/div[1]/div[2]/h2/a
```

mình hay dùng extension [Xpath Helper](https://chrome.google.com/webstore/detail/xpath-helper/hgimnogjllphhhkhlmebbmlgjoejdpjl). Tất nhiên mình có clone repo của extension này về và custome lại để cho thuận tiện việc lấy và insert template vào hệ thống. Trong 1 website, 1 xpath có thể đúng với page này nhưng lại không đúng với page kia nên bạn cần tối ưu xpath được suggest từ Xpath Helper sao cho phù hợp với nhiều page nhất.

## 2. Hệ thống quản lý template

### a, Backend

Có thể dùng luôn [Flask](https://flask.palletsprojects.com/en/2.3.x/) để tạo hệ thống api với các chức năng thêm, xóa, sửa, generate file, start, stop một spider cho đỡ mất công học thêm thứ khác. Flask của python dùng thì max nhanh và đơn giản, chỉ cần import là sài thôi. Nên dùng databases NoSQL để lưu trữ thông tin các template vì tính linh động của chúng.

### b, Frontend

React hoặc Angularjs xx . Mình làm backend là chính nên cũng không quan tâm lắm, cứ dễ dùng, nhiều support thì mình sài thôi. Trước thì mình có dùng React, nhưng giờ chuyển qua Angularjs xx rồi (xx là version của Angular nhé 😄)

### c, Quản lý các máy crawler

Khi hệ thống của bạn mở rộng có 2K, 3K site cần crawl mỗi ngày thì bạn sẽ cần phải có nhiều hơn 1 máy crawler. Lúc này cần thêm một việc là quản lý các máy crawler sao cho chúng chạy tối đa công suất có thể và không xảy ra tình trạng 1 site được crawl ở 2 máy khác nhau. Lúc này bạn có thể nghĩ tới Celery, nó sẽ giúp bạn đồng bộ giữa các máy crawler, quản lý dễ hơn và cũng tăng hiệu suất của server hơn. Hoặc to tay thì có thể tự code cũng được, vì về cơ bản thì mỗi máy có 1 cấu hình riêng, công suất riêng nên cứ ném riêng cho 1 file config, cho chúng sync được với một thằng master nào đấy rồi từ thằng master chỉ đạo thằng nào làm gì qua api thôi.

### d, Giám sát hiệu năng của hệ thống

Mình đã dùng [Datadog](https://viblo.asia/p/datadog-cai-dat-va-cau-hinh-cho-rails-application-vyDZOW87Zwj) để tracking xem một ngày hệ thống mình crawl được bao nhiêu item, so sánh với các ngày trước đó. Khi có 1 máy crawler lăn ra chết sẽ có mail báo từ datadog, khi hight CPU..v.v

# Thu thập dữ liệu bằng các ngôn ngữ khác nhau.



# Crawl Data với Chrome Extension

- [Web Scraper](https://chrome.google.com/webstore/detail/web-scraper-free-web-scra/jnhgnonknehpejjnehehllkliplmbmhn?hl=en)
- [Web Scraper intro tutorial](https://youtu.be/n7fob_XVsbY)
- App [HttpCanary](https://m.apkpure.com/vn/httpcanary-%E2%80%94-http-sniffer-capture-analysis/com.guoshi.httpcanary) để xem phần network của api

# Thu thập dữ liệu webbằng các ngôn ngữ khác nhau

- [Python](#python)
- [Java](#java)
- [C#](#c)
- [JavaScript](#javascript)
- [PHP](#php)
- [C++](#c-1)
- [C](#c-2)
- [Ruby](#ruby)
- [Rust](#rust)
- [R](#r)
- [Erlang](#erlang)
- [Perl](#perl)
- [Go](#go)
- [Scala](#scala)

## Python 
* [Scrapy](https://github.com/scrapy/scrapy) - Framework quét màn hình và thu thập dữ liệu web cấp cao nhanh chóng.
    * [django-dynamic-scraper](https://github.com/holgerd77/django-dynamic-scraper) - Tạo Scrapy Scraper thông qua giao diện quản trị Django.
    * [Scrapy-Redis](https://github.com/rolando/scrapy-redis) - Các thành phần (components) dựa trên Redis cho Scrapy.
    * [scrapy-cluster](https://github.com/istresearch/scrapy-cluster) - Sử dụng Redis và Kafka để tạo cụm thu thập dữ liệu phân tán theo yêu cầu.
    * [distribute_crawler](https://github.com/gnemoug/distribute_crawler) - Sử dụng Scrapy, Redis, Mongodb,graphite để tạo ra một con nhện phân tán.
* [pyspider](https://github.com/binux/pyspider) - Một hệ thống spider mạnh mẽ.
* [CoCrawler](https://github.com/cocrawler/cocrawler) - Trình thu thập dữ liệu web đa năng được xây dựng bằng các công cụ hiện đại và đồng thời.
* [cola](https://github.com/chineking/cola) - Framework thu thập thông tin phân tán.
* [Demiurge](https://github.com/matiasb/demiurge) - Micro-framework quét dựa trên PyQuery.
* [Scrapely](https://github.com/scrapy/scrapely) - Thư viện quét màn hình HTML thuần Python.
* [feedparser](http://pythonhosted.org/feedparser/) - Trình phân tích cú pháp nguồn cấp dữ liệu phổ quát.
* [you-get](https://github.com/soimort/you-get) -  Trình tải xuống Dumb scrapes trang web.
* [MechanicalSoup](https://github.com/hickford/MechanicalSoup) - Thư viện Python để tự động hóa tương tác với các trang web.
* [portia](https://github.com/scrapinghub/portia) - Quét hình ảnh cho Scrapy.
* [crawley](https://github.com/jmg/crawley) - Framework thu thập dữ liệu / thu thập dữ liệu Pythonic dựa trên các hoạt động I/O không chặn.
* [RoboBrowser](https://github.com/jmcarp/robobrowser) - Một thư viện Pythonic đơn giản để duyệt web mà không cần trình duyệt web độc lập.
* [MSpider](https://github.com/manning23/MSpider) - Một con nhện đơn giản, dễ dàng sử dụng gevent và js render.
* [brownant](https://github.com/douban/brownant) - Framework trích xuất dữ liệu web nhẹ.
* [PSpider](https://github.com/xianhu/PSpider) - Một framework nhện đơn giản trong Python3.
* [Gain](https://github.com/gaojiuli/gain) - Framework thu thập dữ liệu web dựa trên asyncio cho mọi người.
* [sukhoi](https://github.com/iogf/sukhoi) - Trình thu thập dữ liệu web tối giản và mạnh mẽ.
* [spidy](https://github.com/rivermont/spidy) - Trình thu thập dữ liệu web dòng lệnh đơn giản, dễ sử dụng.
* [newspaper](https://github.com/codelucas/newspaper) - Trích xuất siêu dữ liệu tin tức, toàn văn và bài viết bằng Python 3
* [aspider](https://github.com/howie6879/aspider) - Một micro-framework quét web không đồng bộ dựa trên asyncio.

## Java
* [ACHE Crawler](https://github.com/ViDA-NYU/ache) - Trình thu thập dữ liệu web dễ sử dụng để tìm kiếm theo tên miền cụ thể.
* [Apache Nutch](http://nutch.apache.org/) - Trình thu thập dữ liệu web có khả năng mở rộng cao, có khả năng mở rộng cao cho môi trường sản xuất.
    * [anthelion](https://github.com/yahoo/anthelion) - Một plugin dành cho Apache Nutch để thu thập thông tin các chú thích ngữ nghĩa trong các trang HTML.
* [Crawler4j](https://github.com/yasserg/crawler4j) - Trình thu thập dữ liệu web đơn giản và nhẹ.
* [JSoup](http://jsoup.org/) - Quét, phân tích, thao tác và làm sạch HTML.
* [websphinx](http://www.cs.cmu.edu/~rcm/websphinx/) - Bộ xử lý dành riêng cho trang web để trích xuất thông tin HTML.
* [Open Search Server](http://www.opensearchserver.com/) - Tập hợp đầy đủ các chức năng tìm kiếm. Xây dựng chiến lược lập chỉ mục của riêng bạn. Trình phân tích cú pháp trích xuất dữ liệu toàn văn. Trình thu thập thông tin có thể lập chỉ mục mọi thứ.
* [Gecco](https://github.com/xtuhcy/gecco) - Trình thu thập dữ liệu web nhẹ dễ sử dụng
* [WebCollector](https://github.com/CrawlScript/WebCollector) - Giao diện đơn giản để thu thập dữ liệu trên Web, bạn có thể thiết lập trình thu thập dữ liệu web đa luồng trong vòng chưa đầy 5 phút.
* [Webmagic](https://github.com/code4craft/webmagic) - Framework thu thập thông tin có thể mở rộng.
* [Spiderman](https://git.oschina.net/l-weiwei/spiderman) - Trình thu thập dữ liệu web đa luồng, có thể mở rộng, có thể mở rộng.
    * [Spiderman2](http://git.oschina.net/l-weiwei/Spiderman2) - Framework thu thập dữ liệu web phân tán, hỗ trợ kết xuất js.
* [Heritrix3](https://github.com/internetarchive/heritrix3) -  Dự án trình thu thập dữ liệu web có chất lượng lưu trữ, có quy mô web, có thể mở rộng
* [SeimiCrawler](https://github.com/zhegexiaohuozi/SeimiCrawler) - Một framework thu thập thông tin phân tán, linh hoạt.
* [StormCrawler](http://github.com/DigitalPebble/storm-crawler/) -  Bộ sưu tập tài nguyên nguồn mở để xây dựng trình thu thập dữ liệu web có độ trễ thấp, có thể mở rộng trên Apache Storm
* [Spark-Crawler](https://github.com/USCDataScience/sparkler) - Đang phát triển Apache Nutch để chạy trên Spark.
* [webBee](https://github.com/pkwenda/webBee) - Một con nhện web DFS.
* [spider-flow](https://github.com/ssssssss-team/spider-flow) - Một framework nhện trực quan, tốt đến mức bạn `không cần phải viết bất kỳ mã nào` để thu thập dữ liệu trang web.


## C# 
* [ccrawler](http://www.findbestopensource.com/product/ccrawler) - Được xây dựng trong phiên bản C# 3.5. nó chứa một phần mở rộng đơn giản của trình phân loại nội dung web, có thể phân tách giữa các trang web tùy thuộc vào nội dung của chúng.
* [SimpleCrawler](https://github.com/lei-zhu/SimpleCrawler) - Spider đơn giản dựa trên biểu thức đa luồng, regluar.
* [DotnetSpider](https://github.com/zlzforever/DotnetSpider) - Đây là một spider đa nền tảng, nhẹ được phát triển bởi C#.
* [Abot](https://github.com/sjdirect/abot) - Trình thu thập dữ liệu web C# được xây dựng để có tốc độ và tính linh hoạt.
* [Hawk](https://github.com/ferventdesert/Hawk) - Công cụ thu thập thông tin nâng cao và ETL được viết bằng C#/WPF.
* [SkyScraper](https://github.com/JonCanning/SkyScraper) - Trình quét web / trình thu thập dữ liệu web không đồng bộ sử dụng không đồng bộ / chờ đợi Reactive Extensions.
* [Infinity Crawler](https://github.com/TurnerSoftware/InfinityCrawler) - Thư viện trình thu thập dữ liệu web đơn giản nhưng mạnh mẽ trong C#.

## JavaScript
* [scraperjs](https://github.com/ruipgil/scraperjs) - Một công cụ quét web hoàn chỉnh và linh hoạt.
* [scrape-it](https://github.com/IonicaBizau/scrape-it) - Một công cụ cạp Node.js dành cho con người.
* [simplecrawler](https://github.com/cgiffard/node-simplecrawler) - Trình thu thập dữ liệu web hướng sự kiện.
* [node-crawler](https://github.com/bda-research/node-crawler) - Trình thu thập thông tin nút có api đơn giản, rõ ràng.
* [js-crawler](https://github.com/antivanov/js-crawler) - Trình thu thập thông tin web cho Node.JS, cả HTTP và HTTPS đều được hỗ trợ.
* [webster](https://github.com/zhuyingda/webster) - Một khung thu thập dữ liệu web đáng tin cậy có thể quét nội dung được hiển thị bằng ajax và js trong một trang web.
* [x-ray](https://github.com/lapwinglabs/x-ray) - Trình quét web có hỗ trợ phân trang và trình thu thập thông tin.
* [node-osmosis](https://github.com/rchipka/node-osmosis) - Trình phân tích cú pháp HTML/XML và trình quét web cho Node.js.
* [web-scraper-chrome-extension](https://github.com/martinsbalodis/web-scraper-chrome-extension) - Công cụ trích xuất dữ liệu web được triển khai dưới dạng tiện ích mở rộng của chrome.
* [supercrawler](https://github.com/brendonboshell/supercrawler) - Xác định trình xử lý tùy chỉnh để phân tích nội dung. Tuân theo robots.txt, giới hạn tốc độ và giới hạn tương tranh.
* [headless-chrome-crawler](https://github.com/yujiosaka/headless-chrome-crawler) - Thu thập dữ liệu Headless Chrome với sự hỗ trợ của jQuery
* [Squidwarc](https://github.com/n0tan3rd/squidwarc) - Trình thu thập thông tin lưu trữ, có độ chính xác cao, có thể sử dụng tập lệnh, sử dụng Chrome hoặc Chrome có hoặc không có phần head
* [crawlee](https://github.com/apify/crawlee) - Thư viện tự động hóa trình duyệt và quét web dành cho Node.js giúp bạn xây dựng các trình thu thập thông tin đáng tin cậy. Nhanh. 


## PHP
* [Goutte](https://github.com/FriendsOfPHP/Goutte) - Thư viện quét màn hình và thu thập dữ liệu web cho PHP.
    * [laravel-goutte](https://github.com/dweidner/laravel-goutte) - Laravel 5 Facade cho Goutte.
* [dom-crawler](https://github.com/symfony/dom-crawler) - Thành phần DomCrawler giúp dễ dàng điều hướng DOM cho các tài liệu HTML và XML.
* [QueryList](https://github.com/jae-jae/QueryList) - Framework thu thập thông tin PHP lũy tiến.
* [pspider](https://github.com/hightman/pspider) - Trình thu thập dữ liệu web song song được viết bằng PHP.
* [php-spider](https://github.com/mvdbos/php-spider) - Một spider web PHP có thể định cấu hình và mở rộng.
* [spatie/crawler](https://github.com/spatie/crawler) - Một trình thu thập thông tin mạnh mẽ, dễ sử dụng được triển khai trong PHP. Có thể thực thi Javascript.
* [crawlzone/crawlzone](https://github.com/crawlzone/crawlzone) - Crawlzone là một khung thu thập dữ liệu internet không đồng bộ nhanh chóng dành cho PHP.
* [PHPScraper](https://github.com/spekulatius/PHPScraper) - PHPScraper là một trình thu thập thông tin & thu thập thông tin được xây dựng để đơn giản hóa.

## C++
* [open-source-search-engine](https://github.com/gigablast/open-source-search-engine) - Một công cụ tìm kiếm nguồn mở phân tán và trình thu thập thông tin/trình thu thập dữ liệu được viết bằng C/C++.

## C
* [httrack](https://github.com/xroche/httrack) - Sao chép trang web vào máy tính của bạn.

## Ruby
* [Nokogiri](https://github.com/sparklemotion/nokogiri) - Rubygem cung cấp trình phân tích cú pháp HTML, XML, SAX và Reader với hỗ trợ bộ chọn XPath và CSS.
* [upton](https://github.com/propublica/upton) - Một framework bao gồm pin (batteries-included) để quét web dễ dàng. Chỉ cần thêm CSS (Hoặc làm nhiều hơn).
* [wombat](https://github.com/felipecsl/wombat) - Trình thu thập dữ liệu/quét web Ruby nhẹ với DSL thanh lịch giúp trích xuất dữ liệu có cấu trúc từ các trang.
* [RubyRetriever](https://github.com/joenorton/rubyretriever) - RubyRetriever là Trình thu thập dữ liệu web, Trình thu thập dữ liệu & Trình thu thập tệp.
* [Spidr](https://github.com/postmodern/spidr) - Tìm kiếm một trang web, nhiều tên miền, liên kết nhất định hoặc `vô cùng`.
* [Cobweb](https://github.com/stewartmckee/cobweb) - Trình thu thập dữ liệu web với các tùy chọn thu thập thông tin rất linh hoạt, độc lập hoặc sử dụng sidekiq.
* [mechanize](https://github.com/sparklemotion/mechanize) - Tương tác và thu thập dữ liệu web tự động.

## Rust
* [spider](https://github.com/spider-rs/spider) - Trình thu thập thông tin và lập chỉ mục web nhanh nhất.
* [crawler](https://github.com/a11ywatch/crawler) - Trình lập chỉ mục web gRPC được tính phí cho hiệu suất.

## R
* [rvest](https://github.com/hadley/rvest) - Quét web đơn giản cho R.

## Erlang 
* [ebot](https://github.com/matteoredaelli/ebot) - Trình thu thập dữ liệu web có khả năng mở rộng, phân tán và có cấu hình cao.

## Perl
* [web-scraper](https://github.com/miyagawa/web-scraper) - Bộ công cụ quét web sử dụng Bộ chọn HTML và CSS hoặc biểu thức XPath.

## Go
* [pholcus](https://github.com/henrylee2cn/pholcus) -  Trình thu thập dữ liệu web mạnh mẽ, có tính đồng thời cao và phân tán.
* [gocrawl](https://github.com/PuerkitoBio/gocrawl) - Trình thu thập dữ liệu web lịch sự, mỏng và đồng thời.
* [fetchbot](https://github.com/PuerkitoBio/fetchbot) - Trình thu thập dữ liệu web đơn giản và linh hoạt tuân theo các chính sách của robots.txt và độ trễ thu thập dữ liệu.
* [go_spider](https://github.com/hu17889/go_spider) - Một framework tuyệt vời dành cho Go concurrent Crawler(spider).
* [dht](https://github.com/shiyanhui/dht) - Giao thức BitTorrent DHT && DHT Spider.
* [ants-go](https://github.com/wcong/ants-go) - Một công cụ thu thập thông tin mã nguồn mở, phân tán, restful ở golang.
* [scrape](https://github.com/yhat/scrape) - Một giao diện đơn giản, cấp độ cao hơn để quét web trên Go.
* [creeper](https://github.com/wspl/creeper) - Framework thu thập thông tin thế hệ tiếp theo (Go).
* [colly](https://github.com/asciimoo/colly) - Framework quét nhanh và thanh lịch dành cho Gophers.
* [ferret](https://github.com/MontFerret/ferret) - Declarative web scraping.
* [Dataflow kit](https://github.com/slotix/dataflowkit) - Trích xuất dữ liệu có cấu trúc từ các trang web. Các trang web cạo. Web sites scraping.
* [Hakrawler](https://github.com/hakluke/hakrawler) - Trình thu thập dữ liệu web đơn giản, nhanh chóng được thiết kế để khám phá dễ dàng, nhanh chóng các điểm cuối và nội dung trong ứng dụng web

## Scala
* [crawler](https://github.com/bplawler/crawler) - Scala DSL để thu thập dữ liệu web.
* [scrala](https://github.com/gaocegege/scrala) - Khung trình thu thập dữ liệu Scala (nhện), lấy cảm hứng từ Scrapy.
* [ferrit](https://github.com/reggoodwin/ferrit) - Ferrit là dịch vụ thu thập dữ liệu web được viết bằng Scala sử dụng Akka, Spray và Cassandra.


## Tổng kết

Về cơ bản để xây dựng một ứng dụng crawler, có rất nhiều cách và trên đây là cách mình đã tiếp cận. Hy vọng sẽ giúp được bạn xây dựng được một hệ thống crawler như mong muốn.


-----
Tham khảo:
- [Crawling dữ liệu từ website, tìm hiểu về ScrapingWeb](https://viblo.asia/p/crawling-du-lieu-tu-website-tim-hieu-ve-scrapingweb-1VgZvGo9lAw)
- [[Bàn tiếp về Crawling] Quét dữ liệu bất động sản bằng Python](https://viblo.asia/p/ban-tiep-ve-crawling-quet-du-lieu-bat-dong-san-bang-python-RnB5pzo6ZPG)
- [Data Scraping Tools for Scraping Real Estate Data Using Python](https://www.promptcloud.com/blog/scraping-real-estate-data-from-zillow-using-python/)
- [Crawl data - cào dữ liệu có gì khó?](https://www.lhsang.dev/posts/technique/scraping-data-from-websites/)
- [Tìm hiểu chung về Web Scraping và các vấn đề cần quan tâm](https://viblo.asia/p/tim-hieu-chung-ve-web-scraping-va-cac-van-de-can-quan-tam-djeZ1yXJZWz)
- [Tìm hiểu về Web Scraping Bot là gì?](https://securitydaily.net/tim-hieu-ve-web-scraping-bot-la-gi/)
- [Xây dựng sơ bộ một hệ thống crawler](https://viblo.asia/p/xay-dung-so-bo-mot-he-thong-crawler-aWj538BQK6m)
- [Panther - thư viện dùng để scrape website](https://viblo.asia/p/panther-thu-vien-dung-de-scrape-website-ORNZqp3bK0n)
- [Cách mình "hack" được vào hẹ thống của SMAS để xem điểm.](https://viblo.asia/p/cach-minh-hack-duoc-vao-he-thong-cua-smas-de-xem-diem-LzD5d2rYZjY)
- [Một vài công cụ dò quét lỗ hổng XSS hiệu quả khi săn bug](https://viblo.asia/p/mot-vai-cong-cu-do-quet-lo-hong-xss-hieu-qua-khi-san-bug-x7Z4Djm0LnX)
- [Cách crawl data "no code" đơn giản với Chrome Extension](https://viblo.asia/p/cach-crawl-data-no-code-don-gian-voi-chrome-extension-obA4660w4Kv)

-----
Python - [Scrapy](https://scrapy.org), [pyspider](http://docs.pyspider.org), [CoCrawler](https://github.com/cocrawler/cocrawler), [cola](https://github.com/qinxuye/cola), [Demiurge](http://demiurge.readthedocs.org/), [Scrapely](https://github.com/scrapy/scrapely) .v.v.

- [Cào dữ liệu với Scrapy](https://phocode.com/python/scrapy/scrapy-gioi-thieu/)
- [Làm một con Crawler đơn giản để cào ebooks với Scrapy và python](https://viblo.asia/p/lam-mot-con-crawler-don-gian-de-cao-ebooks-voi-scrapy-va-python-maGK7qPDlj2)
- [Thu thập và lưu trữ dữ liệu với scrapy và mysql](https://viblo.asia/p/thu-thap-va-luu-tru-du-lieu-voi-scrapy-va-mysql-yMnKMA9EK7P)
- [Thu thập dữ liệu tự động cùng với Scrapy, Mongodb và Crontab](https://viblo.asia/p/thu-thap-du-lieu-tu-dong-cung-voi-scrapy-mongodb-va-crontab-RQqKLNrml7z)
- [Tập tành crawl dữ liệu với Scrapy Framework](https://viblo.asia/p/tap-tanh-crawl-du-lieu-voi-scrapy-framework-bWrZnW7rlxw)
- [Crawl dữ liệu trang web với Scrapy](https://viblo.asia/p/crawl-du-lieu-trang-web-voi-scrapy-E375zWr1KGW)
- [Sự kết hợp hoàn hảo của Scrapy và Splash - Giải pháp tối ưu với trang web sử dụng Javascript?](https://viblo.asia/p/su-ket-hop-hoan-hao-cua-scrapy-va-splash-giai-phap-toi-uu-voi-trang-web-su-dung-javascript-Qbq5Qa8w5D8)
- [Sự kết hợp hoàn hảo của Scrapy và Splash (Phần 2)](https://viblo.asia/p/su-ket-hop-hoan-hao-cua-scrapy-va-splash-phan-2-1VgZvVApZAw)
- [Thu thập dữ liệu với Scrapy, Splash - Nội dung được tạo bởi JavaScript](https://viblo.asia/p/thu-thap-du-lieu-voi-scrapy-splash-noi-dung-duoc-tao-boi-javascript-3Q75wBbMlWb)
- [Ví dụ về việc thu thập dữ liệu Web với Scrapy](https://viblo.asia/p/vi-du-ve-viec-thu-thap-du-lieu-web-voi-scrapy-aWj53kBY56m)
- [Giới thiệu/hướng dẫn về Crawler với Scrapy Framework](https://viblo.asia/p/gioi-thieuhuong-dan-ve-crawler-voi-scrapy-framework-ByEZkWoEZQ0)
- [Giới thiệu/hướng dẫn về Crawler với Scrapy Framework (Phần 2)](https://viblo.asia/p/gioi-thieuhuong-dan-ve-crawler-voi-scrapy-framework-phan-2-YWOZry7pKQ0)
- [Giới thiệu/hướng dẫn về Crawler với Scrapy Framework (Phần 3)](https://viblo.asia/p/gioi-thieuhuong-dan-ve-crawler-voi-scrapy-framework-phan-3-gDVK2kovZLj)
- [Scraping và crawling Web với Scrapy và SQLAlchemy](https://viblo.asia/p/scraping-va-crawling-web-voi-scrapy-va-sqlalchemy-6BkGyxOLM5aV)
- [Kỹ thuật scraping và crawling Web nâng cao với Scrapy và SQLAlchemy](https://viblo.asia/p/ky-thuat-scraping-va-crawling-web-nang-cao-voi-scrapy-va-sqlalchemy-6BkGyxzeM5aV)
- [Sử dụng proxy trong Scrapy](https://viblo.asia/p/su-dung-proxy-trong-scrapy-maGK780LZj2)
- [Tìm hiểu cách cào dữ liệu đơn giản với Scapy](https://viblo.asia/p/tim-hieu-cach-cao-du-lieu-don-gian-voi-scapy-3P0lPDA4lox)

#### Scrapy for Beginners
- _John Watson Rooney &#9679; [15 video](https://www.youtube.com/playlist?list=PLRzwgpycm-Fjvdf7RpmxnPMyJ80RecJjv) &#9679; Dec 10, 2020_

#### Scrapy
- _codeRECODE &#9679; [40 video](https://www.youtube.com/playlist?list=PLj4hN6FewnwoUArmA8kifDHZYvRn6egg5) &#9679; Jun 7, 2023_

#### The Python Scrapy Playbook
- _ScrapeOps &#9679; [20 video](https://www.youtube.com/playlist?list=PLkhQp3-EGsIi39YF-BE306DDX1xVSTHmn) &#9679; Dec 12, 2020_

#### Python Web Scraping & Crawling using Scrapy
- _buildwithpython &#9679; [25 video](https://www.youtube.com/playlist?list=PLhTjy8cBISEqkN-5Ku_kXG4QW33sxQo0t) &#9679; Feb 25, 2019_

- [Scrapy Course – Python Web Scraping for Beginners](https://youtu.be/mBoX_JCKZTE)
- [Scraping LinkedIn Profiles with Python Scrapy (2022)](https://youtu.be/fg8ZGzueHLk)


Python - Beautiful Soup
- [PyMOTM: Argparse](https://viblo.asia/p/pymotm-argparse-l5XRBVeVRqPe)
- [PyMOTM: Requests](https://viblo.asia/p/pymotm-requests-zb7vD8wKvjKd)
- [PyMOTM: Beautiful Soup 4 (Part I)](https://viblo.asia/p/pymotm-beautiful-soup-4-part-i-DljMbVZZMVZn)
- [PyMOTM: Beautiful Soup 4 (Part II)](https://viblo.asia/p/pymotm-beautiful-soup-4-part-ii-amoG81yOvz8P)
- [PyMOTM: Beautiful Soup 4 (Part III)](https://viblo.asia/p/pymotm-beautiful-soup-4-part-iii-XqaGEBJEeWK)
- [Cách scrape một trang web bằng python và BeautifulSoup](https://viblo.asia/p/cach-scrape-mot-trang-web-bang-python-va-beautifulsoup-vyDZODwPlwj)

-----
JavaScript
- ["Đào mỏ" với Puppeteer](https://viblo.asia/p/dao-mo-voi-puppeteer-924lJEg6ZPM)
- [Web Scraping với Nuxtjs sử dụng Puppeteer](https://viblo.asia/p/web-scraping-voi-nuxtjs-su-dung-puppeteer-gDVK2L8vlLj)
- [Crawl website sử dụng Node.js và Puppeteer - phần 1](https://viblo.asia/p/crawl-website-su-dung-nodejs-va-puppeteer-phan-1-L4x5xv2wZBM)
- [Crawl website sử dụng Node.js và Puppeteer - phần 2](https://viblo.asia/p/crawl-website-su-dung-nodejs-va-puppeteer-phan-2-3P0lP1kn5ox)
- [Crawl data using laravel , proxy and simple html dom](https://viblo.asia/p/crawl-data-using-laravel-proxy-and-simple-html-dom-Az45bojwKxY)
- [[P1] Tìm hiểu Headless browser & Puppeteer](https://viblo.asia/p/p1-tim-hieu-headless-browser-puppeteer-63vKjngdK2R)
- [[P2] - Lấy dữ liệu website bằng puppeteer](https://viblo.asia/p/p2-lay-du-lieu-website-bang-puppeteer-YWOZryPvKQ0)
- [Build extension to check timesheet on WSM (P1)](https://viblo.asia/p/build-extension-to-check-timesheet-on-wsm-p1-aWj538N1K6m)
- [Xây dựng extension để check timesheet trên WSM (P2)](https://viblo.asia/p/xay-dung-extension-de-check-timesheet-tren-wsm-p2-OeVKB4JMlkW)

-----
PHP
- [Crawl dữ liệu Website sử dụng kỹ thuật phân tích cú pháp XML bằng PHP](https://itnavi.com.vn/blog/crawl-du-lieu-website-su-dung-ky-thuat-phan-tich-cu-phap-xml-bang-php)
- [Crawl Data bằng Laravel và Goutte](https://viblo.asia/p/crawl-data-bang-laravel-va-goutte-L4x5x3ewlBM)

-----
Ruby - Nokogiri, upton, wombat, RubyRetriever, Spidr, Cobweb, mechanize
- [Crawl Data và Scrape Data](https://viblo.asia/p/ruby-crawl-data-va-scrape-data-yZjJY9RbJOE)
- [Crawl dữ liệu trong Rails với gem Mechanize](https://viblo.asia/p/crawl-du-lieu-trong-rails-voi-gem-mechanize-LzD5dLv05jY)
- [Thử crawling dữ liệu Viblo bằng Mechanize gem](https://viblo.asia/p/thu-crawling-du-lieu-viblo-bang-mechanize-gem-RQqKLLLrK7z)
- [Xây dựng web crawler cơ bản với mechanize](https://viblo.asia/p/xay-dung-web-crawler-co-ban-voi-mechanize-RnB5pnJYZPG)
- [Scrape websites with Ruby & Mechanize](https://viblo.asia/p/scrape-websites-with-ruby-mechanize-DzVkpmoKvnW)
- [Web crawler và scrape data với gem Mechanize](https://viblo.asia/p/web-crawler-va-scrape-data-voi-gem-mechanize-eBYjv410RxpV)
- [Web crawler nâng cao với Mechanize (P1)](https://viblo.asia/p/web-crawler-nang-cao-voi-mechanize-p1-YrEBRAQLR8Zj)
- [Web crawler nâng cao với Mechanize (P2)](https://viblo.asia/p/web-crawler-nang-cao-voi-mechanize-p2-ojaqG0nVREKw)

-----
Go - pholcus, gocrawl, fetchbot, go_spider, dht, ants-go, scrape, creeper, colly, ferret, Dataflow kit, Hakrawler
- [Thu thập dữ liệu với Golang Colly](https://viblo.asia/p/thu-thap-du-lieu-voi-golang-colly-924lJ3y85PM)
- [Sử dụng chromedp với golang để crawl các trang web có nội dung được tạo bởi javascript](https://viblo.asia/p/su-dung-chromedp-voi-golang-de-crawl-cac-trang-web-co-noi-dung-duoc-tao-boi-javascript-4P856GWLKY3)

-----
- [Awesome-Crawler](https://github.com/BruceDone/awesome-crawler)
- [https://viblo.asia/tags/crawl](https://viblo.asia/tags/crawl)
- [https://viblo.asia/tags/crawling](https://viblo.asia/tags/crawling)
- [https://viblo.asia/tags/web-crawler](https://viblo.asia/tags/web-crawler)
- [https://viblo.asia/tags/scraping](https://viblo.asia/tags/scraping)
- [https://viblo.asia/tags/scrapy](https://viblo.asia/tags/scrapy)
- [https://viblo.asia/tags/selenium](https://viblo.asia/tags/selenium)
- [https://viblo.asia/search?q=Cheerio](https://viblo.asia/search?q=Cheerio)
- [https://viblo.asia/tags/puppeteer](https://viblo.asia/tags/puppeteer)
- [https://viblo.asia/tags/mechanize](https://viblo.asia/tags/mechanize)

-----
- [Web Data Crawling vs Web Data Scraping](https://www.promptcloud.com/blog/data-scraping-vs-data-crawling/)
- [Web scraping in 2023 — Breaking it down to basics](https://blog.devgenius.io/webscraping-in-2023-breaking-it-down-to-basics-programming-learning-scraping-python-web-data-science-10fa130cc8be)

-----
eBook:

- [Getting Started with Python Web Scraping](https://www.oreilly.com/library/view/getting-started-with/9781787283244/), [Code samples](https://github.com/PacktPublishing/Getting-Started-with-Python-Web-Scraping-V-)
- [Web Scraping Tutorial with Scrapy and Python for Beginners](https://www.oreilly.com/library/view/web-scraping-tutorial/9781804615317/), [Code samples](https://github.com/PacktPublishing/Web-Scraping-Tutorial-with-Scrapy-and-Python-for-Beginners-)
- [Web Scraping with Python](https://www.linkedin.com/learning/web-scraping-with-python), [Code samples](https://github.com/LinkedInLearning/web-scraping-with-python-2848331)
- [Web Scraping with Python, 2nd Edition](https://www.oreilly.com/library/view/web-scraping-with/9781491985564/), [Code samples](https://github.com/REMitchell/python-scraping)
- [Hands-On Web Scraping with Python](https://packt.link/free-ebook/9781789533392), [Code samples](https://github.com/PacktPublishing/Hands-On-Web-Scraping-with-Python)
- [Python Web Scraping Cookbook](https://www.oreilly.com/library/view/python-web-scraping/9781787285217/), [Code samples](https://github.com/PacktPublishing/Python-Web-Scraping-Cookbook/)
- [Go Web Scraping Quick Start Guide](https://www.oreilly.com/library/view/go-web-scraping/9781789615708/), [Code samples](https://github.com/PacktPublishing/Go-Web-Scraping-Quick-Start-Guide)
- [Website Scraping with Python: Using BeautifulSoup and Scrapy](https://www.oreilly.com/library/view/website-scraping-with/9781484239254/), [Code samples](https://github.com/sanikamal/web-scraping-with-python)
- [Instant PHP Web Scraping](https://www.amazon.com/Instant-PHP-Scraping-Jacob-Ward/dp/1782164766), [Code samples](https://github.com/freelancerwebro/web-scraping-instant)
- [50 Hours of Big Data, PySpark, AWS, Scala, and Scraping](https://www.oreilly.com/library/view/50-hours-of/9781803237039/), [Code samples](https://github.com/PacktPublishing/50-Hours-of-Big-Data-PySpark-AWS-Scala-and-Scraping)
- [R Web Scraping Quick Start Guide](https://www.oreilly.com/library/view/r-web-scraping/9781789138733/), [Code samples](https://github.com/PacktPublishing/R-Web-Scraping-Quick-Start-Guide)
- [Learning Scrapy - Second Edition](https://www.packtpub.com/product/learning-scrapy-second-edition/9781788627450), [Code samples](https://github.com/scalingexcellence/scrapybook-2nd-edition)

-----

<img align="right" src="https://learning.oreilly.com/library/cover/9781804615317/250w/" alt="Web Scraping Tutorial with Scrapy and Python for Beginners" title="Web Scraping Tutorial with Scrapy and Python for Beginners">

<img align="right" src="https://learning.oreilly.com/library/cover/9781098145347/250w/" alt="Web Scraping with Python, 3rd Edition" title="Web Scraping with Python, 3rd Edition">

<img align="right" src="https://learning.oreilly.com/library/cover/9781491985564/250w/" alt="Web Scraping with Python, 2nd Edition" title="Web Scraping with Python, 2nd Edition">

<img align="right" src="https://learning.oreilly.com/library/cover/9781782164364/250w/" alt="Web Scraping with Python" title="Web Scraping with Python">

<img align="right" src="https://learning.oreilly.com/library/cover/9781789533392/250w" alt="Hands-On Web Scraping with Python" title="Hands-On Web Scraping with Python">

<img align="right" src="https://learning.oreilly.com/library/cover/9781787285217/250w/" alt="Python Web Scraping Cookbook" title="Python Web Scraping Cookbook">

![Go Web Scraping Quick Start Guide](https://learning.oreilly.com/library/cover/9781789615708/250w/ "Go Web Scraping Quick Start Guide")

-----