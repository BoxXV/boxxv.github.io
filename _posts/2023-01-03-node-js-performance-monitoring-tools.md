---
layout: post
title: Công cụ giám sát và kiểm tra hiệu suất mã nguồn mở Node.js
subtitle: Node.js Open Source Monitoring, Performance Testing and Tuning
image: "img/projects-bg.jpg"
tags:
- Node.js
- Performance
- PerformanceTest
- Monitoring
---

![Node.js Tools](https://boxxv.github.io/img/2023/node-js-diagram.svg "Node.js Tools")

Node.js nổi tiếng với hiệu suất cực nhanh. Tuy nhiên, như với bất kỳ ngôn ngữ lập trình nào, bạn có thể phát triển mã Node.js hoạt động kém cho với người dùng của mình. Thử nghiệm hiệu suất thích hợp là cần thiết để chống lại điều này.
1. Làm sao có thể tránh tình trạng, 1 Request nặng làm ảnh hưởng đến tất cả Request khác trên 1 Ứng dụng Web bằng NodeJS? (#1)
2. Tại sao NodeJS chạy nhanh, nhưng đôi lúc lại thấy chậm ở các API khác nhau? (#2)
3. Có những API, NodeJS cần con số ở hàng chục đơn vị giây để có thể Response? (#3)

Đôi khi, các ứng dụng không hoạt động tốt như bình thường. Các nhà phát triển ứng dụng chịu trách nhiệm thực hiện giám sát và bảo trì. Khách hàng sử dụng ứng dụng của bạn với tư cách là nhà phát triển có thể lãng phí rất nhiều tiền khi cố gắng khôi phục ứng dụng mà không có sự hỗ trợ của bạn. Để theo dõi các hoạt động của ứng dụng, tốt nhất bạn nên so sánh để sử dụng một hệ thống giám sát hiệu quả.

## I. Công cụ kiểm tra và điều chỉnh hiệu suất Node.js

![Performance](https://boxxv.github.io/img/2023/Improving-Node-.Js-Performance-768x351.png "Performance")

> Updating...


## II. Công cụ giám sát Node.js

![Monitoring](https://boxxv.github.io/img/2023/nodejs-monitoring-cover-5.png "Monitoring")

Tính năng quan trọng nhất mà ứng dụng Node.js của bạn có thể có là gì? Bạn có nghĩ rằng là tìm kiếm toàn văn (full-text search) hoặc có thể sử dụng sockets cho các cuộc trò chuyện thời gian thực? Với tôi, tính năng hấp dẫn nhất, tuyệt vời nhất và hấp dẫn nhất mà bạn có thể thêm vào ứng dụng Node.js là Hiệu suất cao không có thời gian chết. Các ứng dụng hiệu suất cần phải làm tốt ba điều.
- Đảm bảo thời gian chết tối thiểu
- Có mức sử dụng tài nguyên có thể dự đoán được
- Quy mô hiệu quả dựa trên tải

Trong Phần 1, [Các chỉ số chính cần theo dõi của Node.js](https://sematext.com/blog/top-nodejs-metrics-to-watch/), chúng ta đã nói về các chỉ số chính của Node.js mà bạn nên theo dõi để hiểu được tình trạng của ứng dụng và máy chủ của mình. Tôi cũng đã giải thích các thực tiễn không tốt trong Node.js mà bạn nên tránh, chẳng hạn như `blocking the thread` và tạo `memory leaks`, ngoài ra còn có một số thủ thuật nhỏ mà bạn có thể sử dụng để tăng hiệu suất của ứng dụng, chẳng hạn như sử dụng mô-đun cụm để tạo quy trình worker và rẽ nhánh các tiến trình chạy dài để chạy tách biệt với luồng chính.

Trong bài viết này, tôi sẽ giải thích cách thêm giám sát vào ứng dụng Node.js của bạn bằng các công cụ mã nguồn mở khác nhau. Chúng có thể không có các tính năng toàn diện như tích hợp giám sát Sematext Node.js hoặc Datadog, nhưng hãy nhớ rằng chúng là các sản phẩm nguồn mở và có thể hoạt động tốt.


### 1. [PM2](https://www.npmjs.com/package/pm2)

Việc chạy các ứng dụng Node.js trong production trở nên dễ dàng hơn rất nhiều với `PM2`. Đó là trình quản lý quy trình dễ dàng cho phép bạn chạy các ứng dụng ở chế độ cụm. Hoặc, bằng tiếng Anh, nó sẽ tạo ra một quy trình cho mọi lõi CPU mà máy chủ của bạn có.

PM2 là trình quản lý quy trình daemon cho phép các nhà phát triển Node.js quản lý và duy trì các ứng dụng của họ khi họ trực tuyến. Để bắt đầu với dịch vụ này, trước tiên các nhà phát triển phải cài đặt NPM, việc này có thể được thực hiện bằng lệnh npm –version.

Tích hợp giao diện web để theo dõi tình trạng ứng dụng là một trong những tính năng tốt nhất của PM2. Quản lý nhật ký ứng dụng và lỗi, tải lại nóng, truyền phát nhật ký và tự động phân cụm là một số tính năng khác. Quan trọng nhất, nó hỗ trợ quản lý nhiều ứng dụng Node.js.

Các tính năng của PM2:
- Quản lý nhật ký
- Tự động phân cụm cho các ứng dụng Node.js
- Tích hợp vùng chứa

Bắt đầu bằng cách cài đặt [PM2](https://github.com/Unitech/pm2).

```bat
npm install pm2 -g
```

Sau khi nó được cài đặt, bạn sinh ra trình nền PM2 bằng cách chạy lệnh này trong terminal của mình, nếu tệp nguồn chính của bạn là app.js.

```bat
pm2 start app.js -i 0
```

Cờ -i 0 là viết tắt của các trường hợp. Điều này sẽ chạy ứng dụng Node.js của bạn ở chế độ cụm, trong đó 0 là viết tắt của một số lõi CPU. Bạn có thể đặt bất kỳ con số nào bạn muốn theo cách thủ công, nhưng để PM2 đếm số lõi và sinh ra số lượng công nhân đó sẽ dễ dàng hơn nhiều.

Giám sát Node.js với PM2 thật dễ dàng.

```bat
pm2 monit
```

Lệnh này sẽ mở một bảng điều khiển trong thiết bị đầu cuối. Tại đây, bạn có thể theo dõi nhật ký, quy trình, độ trễ vòng lặp, bộ nhớ xử lý và CPU của Node.js.

![PM2](https://boxxv.github.io/img/2023/Selection_458-1.png.webp "PM2")


### 2. [Express Status Monitor](https://github.com/RafalWilinski/express-status-monitor)

![Express Status Monitor](https://camo.githubusercontent.com/aed7a6d40880b02a4a0a09587e69f0e85df78a4127b87b7a6bcbcb80b1efd46a/687474703a2f2f692e696d6775722e636f6d2f4148697a4557712e676966 "Express Status Monitor")

[Express.js](https://expressjs.com) là framework thực tế được các nhà phát triển Node.js lựa chọn. [Express Status Monitor](https://github.com/RafalWilinski/express-status-monitor) là một mô-đun tự lưu trữ cực kỳ đơn giản, bạn thêm vào máy chủ Express của mình. Nó hiển thị tuyến `/status` báo cáo số liệu máy chủ thời gian thực với sự trợ giúp của [Socket.io](https://socket.io) và [Chart.js](https://www.chartjs.org).

Các tính năng của Express Status Monitor:
- Theo dõi thời gian phản hồi
- Tần suất yêu cầu
- Sử dụng bộ nhớ & CPU
- Trạng thái mã

Cài đặt công cụ từ npm đơn giản như thế này.

```bat
npm install express-status-monitor
```

Sau khi bạn đã cài đặt mô-đun, bạn cần thêm nó trước bất kỳ `middleware` hoặc `router` nào khác.

```js
app.use(require('express-status-monitor')())
```

Khi bạn chạy máy chủ của mình, hãy chuyển đến tuyến `/status` để theo dõi các chỉ số Node.js của bạn.

### 3. [Prometheus](https://prometheus.io)

![Prometheus](https://boxxv.github.io/img/2023/nodejs-grafana.webp--1000-562--and-1-more-page---Personal---Microsoft--Edge-02_06_2021-11_29_53.png "Prometheus")

Trừ khi bạn đang sống dưới một tảng đá, bạn hẳn đã nghe nói về [Prometheus](https://github.com/prometheus). Đây là công cụ giám sát nguồn mở nổi tiếng và đáng chú ý nhất mà bạn có thể sử dụng ngày nay. Prometheus là nguồn mở 100% và hướng đến cộng đồng. Tất cả các thành phần đều có sẵn theo Giấy phép Apache 2 trên GitHub. Nó cũng là một dự án thành viên tốt nghiệp của Cloud Native Computing Foundation, bên cạnh các dự án như Kubernetes và Fluentd.

Các tính năng của Prometheus:
- Hình dung tuyệt vời
- Nhiều tích hợp
- Cảnh báo chính xác
- Nhiều thư viện khách hàng
- Lưu trữ hiệu quả

Để bắt đầu theo dõi Node.js bằng Prometheus, bạn cần [tải xuống bản phát hành mới nhất](https://prometheus.io/download/) và cài đặt nó.

```bat
tar xvfz prometheus-*.tar.gz
cd prometheus-*
```

Sau đó, bạn khởi động nó bằng cách chạy tệp thực thi nhưng trước khi chạy lệnh này, bạn cần tạo một tệp prometheus.yml. Đó là một tệp cấu hình để thu thập số liệu từ các mục tiêu được giám sát bằng cách cạo các điểm cuối HTTP của số liệu trên các mục tiêu này.

```text
# prometheus.yml
scrape_configs:
    - job_name: 'prometheus'
      scrape_interval: 1s
      static_configs:
            - targets: ['127.0.0.1:3000']
              labels:
                service: 'test-prom'
                group: 'production'
```

Bây giờ bạn có thể chạy Prometheus.

```bat
$ ./prometheus --config.file=prometheus.yml

hoặc

prometheus.exe --config.file prometheus.yml --web.listen-address ":9090" --storage.tsdb.path "data"
```

Truy cập giao diện web “Prometheus” với URL sau và nó chạy trên cổng `9090`.

[http://localhost:9090](http://localhost:9090)

Tuy nhiên, tôi khá lười biếng và tôi rất thích Docker. Vì vậy, cách tôi làm là chạy hình ảnh Prometheus Docker chính thức và tránh mọi rắc rối khi tải xuống.

#### [Monitoring Node.js with Prometheus and Docker](https://sematext.com/blog/nodejs-open-source-monitoring-tools/#4-monitoring-node-js-with-prometheus-and-docker)

### 4. [Clinic.js](https://clinicjs.org)

[Clinic.js](https://github.com/clinicjs) bao gồm ba công cụ giúp chẩn đoán và xác định các vấn đề về hiệu suất trong các ứng dụng Node.js. Nó rất dễ sử dụng. Tất cả những gì bạn cần làm là cài đặt mô-đun từ npm và chạy nó. Thao tác này sẽ tạo các báo cáo giúp bạn khắc phục sự cố dễ dàng hơn nhiều.

Để cài đặt Clinic.js, hãy chạy lệnh này trong terminal của bạn.

```bat
npm install -g clinic
npm install -g autocannon
```

Khi bạn đã cài đặt xong, tất cả sẽ tùy thuộc vào việc chọn loại báo cáo sẽ tạo. Bạn có thể chọn giữa ba.

**Doctor**
- Thu thập số liệu bằng cách tiêm đầu dò
- Đánh giá sức khỏe và kinh nghiệm
- Tạo đề xuất

**Bubbleprof**
– một cách tiếp cận mới, hoàn toàn độc đáo để lược tả mã Node.js của bạn
- Thu thập số liệu bằng cách sử dụng async_hooks
- Theo dõi độ trễ giữa các hoạt động
- Tạo biểu đồ bong bóng

**Flame**
– phát hiện ra các nút cổ chai `bottlenecks` và đường dẫn nóng trong mã của bạn bằng biểu đồ ngọn lửa
- Thu thập số liệu bằng cách lấy mẫu CPU
- Theo dõi tần suất top-of-stack
- Tạo biểu đồ ngọn lửa

Hãy bắt đầu bằng cách chạy Doctor và tải thử nghiệm ứng dụng Node.js.

```bat
clinic doctor -- node app.js
clinic doctor --autocannon [ / ] -- node app.js
clinic bubbleprof --autocannon [ / ] -- node app.js
clinic flame --autocannon [ / ] -- node app.js
```

Trong khi nó đang chạy, hãy chạy thử tải với công cụ bạn muốn.

```bat
loadtest -n 1000 -c 100 http://localhost:3000/api
```

Sau khi chạy xong, hãy dừng máy chủ và Clinic.js Doctor sẽ mở một báo cáo mà bạn có thể kiểm tra.

![Clinic.js Doctor](https://boxxv.github.io/img/2023/screencapture-file-home-raha-code-sandbox-node-nodejs-monitoring-clinic-2961-clinic-doctor-html-2019-04-29-13_59_42-1.png.webp "Clinic.js Doctor")

Sử dụng phương pháp tương tự này, bạn có thể chạy Bubbleprof hoặc Flame và nhận đồ thị cho các công cụ tương ứng.

![Clinic.js Bubbleprof](https://boxxv.github.io/img/2023/screencapture-file-home-raha-code-sandbox-node-nodejs-monitoring-clinic-3954-clinic-bubbleprof-html-2019-04-29-14_04_33-1.png.webp "Clinic.js Bubbleprof")

![Clinic.js Flame](https://boxxv.github.io/img/2023/Selection_456-1.png.webp "Clinic.js Flame")


### 5. [Appmetrics](https://www.npmjs.com/package/appmetrics-dash)

![Appmetrics](https://raw.githubusercontent.com/RuntimeTools/appmetrics-dash/HEAD/public/appmetrics.gif "Appmetrics")

[Node Application Metrics Dashboard](https://github.com/RuntimeTools/appmetrics-dash) hiển thị số liệu hiệu suất của ứng dụng Node.js đang chạy của bạn. Đó là một mô-đun đơn giản mà bạn cài đặt và yêu cầu ở đầu tệp nguồn Node.js chính của mình.

IBM đã phát triển và duy trì App Metrics, một sáng kiến mã nguồn mở. Mục tiêu chính của nó là cung cấp một khuôn khổ cho các số liệu ứng dụng nổi bật có thể được áp dụng cho nhiều công việc khác nhau. Tốc độ mạng, giao dịch dữ liệu, hiệu suất truy vấn cơ sở dữ liệu, cấu hình CPU và mức sử dụng bộ nhớ cũng như thu gom rác là một số nhiệm vụ này.

Các tính năng của Số liệu ứng dụng:
- AppMetrics-dash plugin để giám sát ứng dụng
- Một công cụ mã nguồn mở và miễn phí
- Giao dịch dữ liệu
- Tốc độ mạng

Bạn cài đặt mô-đun từ npm bằng cách chạy lệnh sau trong terminal của mình.

```bat
npm install appmetrics-dash
```

Appmetrics cung cấp bảng điều khiển giám sát dựa trên web rất dễ sử dụng. Mọi thứ bạn cần làm để có được bảng điều khiển cho tất cả các máy chủ HTTP do ứng dụng của bạn tạo là thêm đoạn mã này vào tệp app.js của bạn hoặc bất kỳ thứ gì bạn gọi là tệp nguồn chính của mình.

```js
// Before all other 'require' statements
require('appmetrics-dash').attach()
```

Giờ đây, bạn sẽ có một tuyến máy chủ mới `/appmetrics-dash` nơi bạn có thể xem rất nhiều chỉ số hữu ích.
- CPU Profiling
- HTTP Incoming Requests
- HTTP Throughput
- Average Response Times (top 5)
- CPU
- Memory
- Heap
- Event Loop Times
- Environment
- Other Requests
- HTTP Outbound Requests

Công cụ giám sát Node.js này không chỉ hiển thị số liệu. Nó cho phép bạn tạo Báo cáo Node và Ảnh chụp nhanh Heap trực tiếp từ bảng điều khiển giám sát. Ngoài ra, bạn có quyền truy cập vào Flame Graphs. Khá tuyệt cho một công cụ mã nguồn mở.


### 6. Others
[Atatus](https://www.atatus.com/for/nodejs) $0.07 /Host/Hour/Month - 14-day free trial
- Chẩn đoán transaction  đầy đủ
- Phân tích hiệu suất
- Phân tích nguyên nhân gốc rễ
- Giám sát máy chủ
- Theo dõi các giao dịch cá nhân

[Sematext](https://sematext.com/apm/) [Sematext open source](https://github.com/sematext)
- Bảo mật ứng dụng
- Giám sát băng thông
- Lập kế hoạch năng lực
- Theo dõi tuân thủ

[Retrace](https://stackify.com/retrace-apm-nodejs/)
- Tích hợp lỗi và nhật ký
- Triển khai và xác nhận triển khai
- Thông tin chuyên sâu lấy nhà phát triển làm trung tâm để nhanh chóng sửa lỗi


## Tổng kết

Giám sát thường bị bỏ qua, mặc dù tầm quan trọng của nó trong việc đảm bảo tính khả dụng của ứng dụng. Các công cụ đánh giá mã, theo dõi hiệu suất và cung cấp thông tin chi tiết về các lỗi chắc chắn sẽ được sử dụng đáng kể, đặc biệt khi chi phí phát triển là một vấn đề cần cân nhắc chính. Họ hỗ trợ bạn đáp ứng SLA bằng cách đưa ra giải pháp nhanh hơn cho khách hàng, giúp bạn tiết kiệm thời gian và công sức.

Số liệu hiệu suất rất quan trọng để giữ cho người dùng của bạn hài lòng. Trong bài viết này, tôi đã chỉ cho bạn cách thêm giám sát vào ứng dụng Node.js của bạn bằng 5 công cụ mã nguồn mở khác nhau. Tìm hiểu cách chọn công cụ phù hợp cho chiến lược giám sát hiệu quả từ hướng dẫn của chúng tôi về cảnh báo và giám sát.

Nếu bạn muốn xem mã mẫu, [đây là một repo](https://github.com/adnanrahic/nodejs-monitoring-sematext/tree/develop) với tất cả các mẫu. Bạn cũng có thể sao chép repo và chọn bất kỳ công cụ nào ngay lập tức.

Hy vọng các bạn thích bài viết này nhiều như tôi thích viết nó. Nếu bạn thích nó, hãy nhấn nút chia sẻ nhỏ đó để nhiều người sẽ thấy hướng dẫn này. Cho đến lần sau, hãy tò mò và vui vẻ.


-----
Tham khảo:

- [Node.js Open Source Monitoring Tools](https://sematext.com/blog/nodejs-open-source-monitoring-tools/)
- [Best 7 Monitoring Tools for Node.js Application](https://www.atatus.com/blog/best-7-monitoring-tools-for-node-js-application/)
- [Node.js Performance Testing and Tuning: Step by Step Approach](https://www.atatus.com/blog/nodejs-performance-testing-and-tuning/)
- [Node.js Performance Testing and Tuning](https://stackify.com/node-js-performance-tuning/)
- [Testing Performance of NodeJs App? Try These 3 Proven Tools](https://www.systango.com/blog/nodejs-performance-testing-and-tuning)
- [10+ Best MongoDB Monitoring Tools and Services 2022 Comparison]](https://sematext.com/blog/mongodb-monitoring-tools/)
- [NodeJS có thực sự nhanh như bạn nghĩ? 🤔](https://viblo.asia/p/nodejs-co-thuc-su-nhanh-nhu-ban-nghi-m68Z0Pe9ZkG)
- [Tạo Logger trong ứng dụng NodeJs với thư viện winston](https://viblo.asia/p/tao-logger-trong-ung-dung-nodejs-voi-thu-vien-winston-djeZ1G885Wz)
- [Find bottlenecks in Node.js apps with Clinic Flame](https://dev.to/mpangrazzi/find-bottlenecks-in-nodejs-apps-with-clinic-flame-3i0h)
- [Prometheus installation on Windows](http://www.liferaysavvy.com/2021/07/prometheus-installation-on-windows.html)
- [Add a Status Monitor to an Express App with express-status-monitor](https://javascript.plainenglish.io/add-a-status-monitor-to-an-express-app-with-express-status-monitor-35fd7f36a8e8)
- [How to run a node.js application permanently?](https://www.geeksforgeeks.org/how-to-run-a-node-js-application-permanently/)