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

|  | Scrapy | Selenium | Cheerio | Puppeteer |
| -- | -- | -- | -- | -- |
| Advantages | - Bất đồng bộ chính là thứ giúp cho scrapy có hiệu năng tuyệt vời. Sử dụng rất ít RAM, CPU. Tài liệu đầy đủ, plugins rất nhiều. Thiết kế theo một kiến trúc khá tốt, dev có thể dễ dàng tùy chỉnh middlewares, pipelines và thêm các function tùy ý. | - Dễ tiếp cận cho beginer. Có thể lấy được nội dung trang render bằng javascript. Có thể thao tác như một người dùng | - Hỗ trợ parse DOM giống như jquery. Bất đồng bộ, khá nhanh | - Giống như selenium, puppeteer cũng sử dụng browser driver để lấy nội dung trang nên có thể lấy được nội dung các trang render bằng js và thao tác như một người dùng. |
| Disadvantages | - Hơi phức tạp cho beginer. Quá dư thừa chức năng nếu chỉ dùng cho 1 project nhỏ và đơn giản. Không thể lấy nội dung trang được render bằng js, tuy nhiên chúng ta có thể kết hợp với Splash. | - Tiêu tốn nhiều tài nguyên vì nó cần đến một browser driver (tưởng tượng như bạn mở 1 tab chrome thì sẽ tốn bao nhiêu RAM, CPU). Rất chậm, nên selenium không phù hợp với một project cào dữ liệu lớn. | - Chỉ đơn thuần là trình phân tích (parser). Không thể lấy nội dung trang được render bằng js | - Tiêu tốn RAM, CPU. Chậm |
| Homepage | [scrapy.org](https://scrapy.org) | [selenium.dev](https://www.selenium.dev) | [cheerio.js.org](https://cheerio.js.org) | [pptr.dev](https://pptr.dev) |

Hầu hết các ngôn ngữ lập trình đều có những thư viện hỗ trợ thu thập dữ liệu, tuy nhiên `Python` sẽ là ngôn ngữ  mà mình gợi ý các bạn nên chọn cho dự án thu thập dữ liệu của mình, Scrapy là một framework trong python hỗ trợ thu thập dữ liệu cực mạnh, hơn nữa python có hỗ trợ khá nhiều thư viện để xử lý dữ liệu.

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

Trên là những chia sẻ mà mình rút trích được từ những vấn đề gặp phải trong quá trình làm luận văn mà mình gặp phải, ngoài ra vẫn còn kha khá issues mà mình chưa gặp phải nữa nếu biết các bạn có thể chia sẻ thêm dưới phần bình luận để cùng tranh luận, cảm ơn các bạn.

-----
eBook:

![Web Scraping Tutorial with Scrapy and Python for Beginners](https://learning.oreilly.com/library/cover/9781804615317/250w/ "Web Scraping Tutorial with Scrapy and Python for Beginners") 
![Web Scraping with Python, 3rd Edition](https://learning.oreilly.com/library/cover/9781098145347/250w/ "Web Scraping with Python, 3rd Edition") 
![Web Scraping with Python, 2nd Edition](https://learning.oreilly.com/library/cover/9781491985564/250w/ "Web Scraping with Python, 2nd Edition") 
![Web Scraping with Python](https://learning.oreilly.com/library/cover/9781782164364/250w/ "Web Scraping with Python") 
![Hands-On Web Scraping with Python](https://learning.oreilly.com/library/cover/9781789533392/250w/ "Hands-On Web Scraping with Python")
![Python Web Scraping Cookbook](https://learning.oreilly.com/library/cover/9781787285217/250w/ "Python Web Scraping Cookbook")
![Go Web Scraping Quick Start Guide](https://learning.oreilly.com/library/cover/9781789615708/250w/ "Go Web Scraping Quick Start Guide")

- [Getting Started with Python Web Scraping](https://www.oreilly.com/library/view/getting-started-with/9781787283244/)
- Getting Started with Python Web Scraping, [Code samples](https://github.com/PacktPublishing/Getting-Started-with-Python-Web-Scraping-V-)
- [Web Scraping Tutorial with Scrapy and Python for Beginners](https://www.oreilly.com/library/view/web-scraping-tutorial/9781804615317/)
- Web Scraping Tutorial with Scrapy and Python for Beginners, [Code samples](https://github.com/PacktPublishing/Web-Scraping-Tutorial-with-Scrapy-and-Python-for-Beginners-)
- [Web Scraping with Python](https://www.linkedin.com/learning/web-scraping-with-python)
- Web Scraping with Python, [Code samples](https://github.com/LinkedInLearning/web-scraping-with-python-2848331)
- [Web Scraping with Python, 2nd Edition](https://www.oreilly.com/library/view/web-scraping-with/9781491985564/)
- Web Scraping with Python, [Code samples](https://github.com/REMitchell/python-scraping)
- [Hands-On Web Scraping with Python](https://packt.link/free-ebook/9781789533392)
- Hands-On Web Scraping with Python, [Code samples](https://github.com/PacktPublishing/Hands-On-Web-Scraping-with-Python)
- [Python Web Scraping Cookbook](https://www.oreilly.com/library/view/python-web-scraping/9781787285217/)
- Python Web Scraping Cookbook, [Code samples](https://github.com/PacktPublishing/Python-Web-Scraping-Cookbook/)
- [Go Web Scraping Quick Start Guide](https://www.oreilly.com/library/view/go-web-scraping/9781789615708/)
- Go Web Scraping Quick Start Guide, [Code samples](https://github.com/PacktPublishing/Go-Web-Scraping-Quick-Start-Guide)
- [Website Scraping with Python: Using BeautifulSoup and Scrapy](https://www.oreilly.com/library/view/website-scraping-with/9781484239254/)
- Website Scraping with Python: Using BeautifulSoup and Scrapy, [Code samples](https://github.com/sanikamal/web-scraping-with-python)
- [Instant PHP Web Scraping](https://www.amazon.com/Instant-PHP-Scraping-Jacob-Ward/dp/1782164766)
- Instant PHP Web Scraping, [Code samples](https://github.com/freelancerwebro/web-scraping-instant)
- [50 Hours of Big Data, PySpark, AWS, Scala, and Scraping](https://www.oreilly.com/library/view/50-hours-of/9781803237039/)
- 50 Hours of Big Data, PySpark, AWS, Scala, and Scraping, [Code samples](https://github.com/PacktPublishing/50-Hours-of-Big-Data-PySpark-AWS-Scala-and-Scraping)
- [R Web Scraping Quick Start Guide](https://www.oreilly.com/library/view/r-web-scraping/9781789138733/)
- R Web Scraping Quick Start Guide, [Code samples](https://github.com/PacktPublishing/R-Web-Scraping-Quick-Start-Guide)


-----
Tham khảo:
- [Crawling dữ liệu từ website, tìm hiểu về ScrapingWeb](https://viblo.asia/p/crawling-du-lieu-tu-website-tim-hieu-ve-scrapingweb-1VgZvGo9lAw)
- [Crawl data - cào dữ liệu có gì khó?](https://www.lhsang.dev/posts/technique/scraping-data-from-websites/)
- [Tìm hiểu về Web Scraping Bot là gì?](https://securitydaily.net/tim-hieu-ve-web-scraping-bot-la-gi/)

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

-----
- [Web Data Crawling vs Web Data Scraping](https://www.promptcloud.com/blog/data-scraping-vs-data-crawling/)
- [Web scraping in 2023 — Breaking it down to basics](https://blog.devgenius.io/webscraping-in-2023-breaking-it-down-to-basics-programming-learning-scraping-python-web-data-science-10fa130cc8be)