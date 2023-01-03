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


## II. Công cụ giám sát Node.js

![Monitoring](https://boxxv.github.io/img/2023/nodejs-monitoring-cover-5.png "Monitoring")

Tính năng quan trọng nhất mà ứng dụng Node.js của bạn có thể có là gì? Bạn có nghĩ rằng là tìm kiếm toàn văn (full-text search) hoặc có thể sử dụng sockets cho các cuộc trò chuyện thời gian thực? Với tôi, tính năng hấp dẫn nhất, tuyệt vời nhất và hấp dẫn nhất mà bạn có thể thêm vào ứng dụng Node.js là Hiệu suất cao không có thời gian chết. Các ứng dụng hiệu suất cần phải làm tốt ba điều.
- Đảm bảo thời gian chết tối thiểu
- Có mức sử dụng tài nguyên có thể dự đoán được
- Quy mô hiệu quả dựa trên tải

Trong Phần 1, [Các chỉ số chính cần theo dõi của Node.js](https://sematext.com/blog/top-nodejs-metrics-to-watch/), chúng ta đã nói về các chỉ số chính của Node.js mà bạn nên theo dõi để hiểu được tình trạng của ứng dụng và máy chủ của mình. Tôi cũng đã giải thích các thực tiễn không tốt trong Node.js mà bạn nên tránh, chẳng hạn như `blocking the thread` và tạo `memory leaks`, ngoài ra còn có một số thủ thuật nhỏ mà bạn có thể sử dụng để tăng hiệu suất của ứng dụng, chẳng hạn như sử dụng mô-đun cụm để tạo quy trình worker và rẽ nhánh các tiến trình chạy dài để chạy tách biệt với luồng chính.

Trong bài viết này, tôi sẽ giải thích cách thêm giám sát vào ứng dụng Node.js của bạn bằng các công cụ mã nguồn mở khác nhau. Chúng có thể không có các tính năng toàn diện như tích hợp giám sát Sematext Node.js hoặc Datadog, nhưng hãy nhớ rằng chúng là các sản phẩm nguồn mở và có thể hoạt động tốt.


### 1. [Appmetrics](https://www.npmjs.com/package/appmetrics-dash)

![Appmetrics](https://raw.githubusercontent.com/RuntimeTools/appmetrics-dash/HEAD/public/appmetrics.gif "Appmetrics")

[Node Application Metrics Dashboard](https://github.com/RuntimeTools/appmetrics-dash) hiển thị số liệu hiệu suất của ứng dụng Node.js đang chạy của bạn. Đó là một mô-đun đơn giản mà bạn cài đặt và yêu cầu ở đầu tệp nguồn Node.js chính của mình. Bạn cài đặt mô-đun từ npm bằng cách chạy lệnh sau trong terminal của mình.

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

### 2. [Express Status Monitor](https://github.com/RafalWilinski/express-status-monitor)

![Express Status Monitor](https://camo.githubusercontent.com/aed7a6d40880b02a4a0a09587e69f0e85df78a4127b87b7a6bcbcb80b1efd46a/687474703a2f2f692e696d6775722e636f6d2f4148697a4557712e676966 "Express Status Monitor")

[Express.js](https://expressjs.com) là framework thực tế được các nhà phát triển Node.js lựa chọn. [Express Status Monitor](https://github.com/RafalWilinski/express-status-monitor) là một mô-đun tự lưu trữ cực kỳ đơn giản, bạn thêm vào máy chủ Express của mình. Nó hiển thị tuyến `/status` báo cáo số liệu máy chủ thời gian thực với sự trợ giúp của [Socket.io](https://socket.io) và [Chart.js](https://www.chartjs.org).

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
```

Tuy nhiên, tôi khá lười biếng và tôi rất thích Docker. Vì vậy, cách tôi làm là chạy hình ảnh Prometheus Docker chính thức và tránh mọi rắc rối khi tải xuống.

#### [Monitoring Node.js with Prometheus and Docker](https://sematext.com/blog/nodejs-open-source-monitoring-tools/#4-monitoring-node-js-with-prometheus-and-docker)

### 4. [Clinic.js](https://clinicjs.org)

[Clinic.js](https://github.com/clinicjs) bao gồm ba công cụ giúp chẩn đoán và xác định các vấn đề về hiệu suất trong các ứng dụng Node.js. Nó rất dễ sử dụng. Tất cả những gì bạn cần làm là cài đặt mô-đun từ npm và chạy nó. Thao tác này sẽ tạo các báo cáo giúp bạn khắc phục sự cố dễ dàng hơn nhiều.

Để cài đặt Clinic.js, hãy chạy lệnh này trong terminal của bạn.

```bat
npm install clinic
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


### 5. PM2

### 6. Others
- [Atatus](https://www.atatus.com/for/nodejs)
- [Sematext](https://sematext.com/apm/)
- [Retrace](https://stackify.com/retrace-apm-nodejs/)


## Tổng kết



-----
Tham khảo:

- [Node.js Open Source Monitoring Tools](https://sematext.com/blog/nodejs-open-source-monitoring-tools/)
- [Best 7 Monitoring Tools for Node.js Application](https://www.atatus.com/blog/best-7-monitoring-tools-for-node-js-application/)
- [Node.js Performance Testing and Tuning: Step by Step Approach](https://www.atatus.com/blog/nodejs-performance-testing-and-tuning/)
- [Node.js Performance Testing and Tuning](https://stackify.com/node-js-performance-tuning/)
- [Testing Performance of NodeJs App? Try These 3 Proven Tools](https://www.systango.com/blog/nodejs-performance-testing-and-tuning)
- []()
- [NodeJS có thực sự nhanh như bạn nghĩ? 🤔](https://viblo.asia/p/nodejs-co-thuc-su-nhanh-nhu-ban-nghi-m68Z0Pe9ZkG)
- [Find bottlenecks in Node.js apps with Clinic Flame](https://dev.to/mpangrazzi/find-bottlenecks-in-nodejs-apps-with-clinic-flame-3i0h)