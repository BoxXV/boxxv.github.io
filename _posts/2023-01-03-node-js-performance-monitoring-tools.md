---
layout: post
categories: ["Kiến trúc & Kiểm thử"]
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

[PM2](https://pm2.keymetrics.io) là một công cụ quản lý tiến trình (Process Manager) free open source, hiện đại, hiệu quả, cross-platform và quan trọng là nó free cho ứng dụng sử dụng Node.js với tích hợp bộ cân bằng tải (load balencer). PM2 hoàn hảo cho bạn trong hầu hết trường hợp chạy ứng dụng NodeJS trên môi trường production.

PM2 đã hoạt động ổn định trên Linux, MacOS cũng như Windows. Nó hỗ trợ giám sát ứng dụng, quản lý, tracking hiệu quả các service/process, chạy các ứng dụng ở chế độ cluster (bạn có thể biết được PM2 ngốn hết bao nhiêu RAM, CPU cho mỗi cluster), start/stop ứng dụng Node.js rất dễ dàng, nhanh chóng. Nó giúp cho ứng dụng của bạn luôn ở trạng thái "sống" (alive forever). Nếu thứ mà server ứng dụng NodeJS của bạn đang cần là zero downtime thì PM2 chính là sự lựa chọn đúng đắn dành cho bạn vì PM2 có tính năng auto reload/restart với zero downtime.

PM2 được viết bằng NodeJS và Shell. Chúng ta có thể sử dụng PM2 thông qua giao diện command line hoặc cũng có thể sử dụng bằng giao diện web trên Key Metrics. Với giao diện trực quan như vậy thì việc quản lý của bạn sẽ trở nên dễ dàng hơn, hay bạn cũng có thể reload/restart mà không cần phải connect SSH tới server rồi dùng command line nữa.

Tích hợp giao diện web để theo dõi tình trạng ứng dụng là một trong những tính năng tốt nhất của PM2. Quản lý nhật ký ứng dụng và lỗi, tải lại nóng, truyền phát nhật ký và tự động phân cụm là một số tính năng khác. Quan trọng nhất, nó hỗ trợ quản lý nhiều ứng dụng Node.js.

Các tính năng của PM2:
- Giám sát ứng dụng
- Quản lý các process, logs của ứng dụng
- Tự động restart/reload app
- Tự động phân cụm cho các ứng dụng Node.js
- Khai báo cấu hình qua JSON file
- Tích hợp với Docker
- Cluster mode
- Chạy các kịch bản lệnh (Startup Scripts) cho hệ thống
- Cho phép tích hợp các module cho hệ thống
- Theo dõi việc sử dụng tài nguyên của ứng dụng (Keymetric Monitering)
- Điều khiển, giám sát các tiến trình trong một ứng dụng nodejs trực tiếp bằng code thông qua PM2 API
.v.v.

Bắt đầu bằng cách cài đặt [PM2](https://github.com/Unitech/pm2).

```bat
npm install pm2 -g
```

Sau khi nó được cài đặt, bạn sinh ra trình nền PM2 bằng cách chạy lệnh này trong terminal của mình, nếu tệp nguồn chính của bạn là app.js.

```bat
pm2 start app.js -i 0
```

Cờ -i 0 là viết tắt của các trường hợp. Điều này sẽ chạy ứng dụng Node.js của bạn ở chế độ cụm, trong đó 0 là viết tắt của một số lõi CPU. Bạn có thể đặt bất kỳ con số nào bạn muốn theo cách thủ công, nhưng để PM2 đếm số lõi và sinh ra số lượng công nhân đó sẽ dễ dàng hơn nhiều.

Câu lệnh giúp ứng dụng của bạn tự động reload khi code của bạn có thay đổi:
```bat
pm2 start app.js --watch
```

Giám sát Node.js với PM2 thật dễ dàng.

```bat
pm2 monit
```

Lệnh này sẽ mở một bảng điều khiển trong thiết bị đầu cuối. Tại đây, bạn có thể theo dõi nhật ký, quy trình, độ trễ vòng lặp, bộ nhớ xử lý và CPU của Node.js.

![PM2](https://boxxv.github.io/img/2023/Selection_458-1.png.webp "PM2")


Ngoài ra còn rất nhiều option khác để bạn dễ dàng tuỳ chỉnh việc quản lý ứng dụng như:

```bat
# Đặt tên cho ứng dụng
--name <app_name>

# Theo dõi và khởi động lại ứng dụng khi có file thay đổi
--watch

# Đặt ngưỡng bộ nhớ để tải lại ứng dụng
--max-memory-restart <200MB>

# Chỉ định file log cụ thể
--log <log_path>

# Độ trễ giữa các lần tự động khởi động lại
--restart-delay <delay in ms>

# Không tự động khởi động lại ứng dụng
--no-autorestart

# Chỉ định cron để bắt buộc khởi động lại
--cron <cron_pattern>

# Đính kèm vào log của ứng dụng
--no-daemon
```

#### Quản lý processes

Bạn có thể dùng các command sau đây để quản lý ứng dụng:

```bat
# Restart ứng dụng
$ pm2 restart app_name

# Reload ứng dụng
$ pm2 reload app_name

# Stop ứng dụng – nhưng vẫn giữ ứng dụng đó ở trong list process
$ pm2 stop app_name

# Stop ứng dụng, đồng thời xoá ứng dụng ra khỏi list process
$ pm2 delete app_name

# Liệt kê trạng thái của tất cả các ứng dụng được quản lý bởi PM2
$ pm2 [list|ls|status]

# Hiện thị log với realtime
$ pm2 logs // Mặc định PM2 sẽ lưu logs tại ./pm2/logs
```

#### Web based dashboard

Bằng cách truy cập vào https://app.pm2.io/ và setup theo hướng dẫn hoặc chạy lệnh sau từ ứng dụng của bạn:

![PM2](https://boxxv.github.io/img/2023/a0c99367-c307-4b89-abab-f3384089dd1d.webp "PM2")

Chúng ta sẽ có một giao diện Monitering trực quan như trên. Với giao diện web, gói miễn phí mặc định cho ta biết đầy đủ các thông tin monitoring cơ bản, còn rất nhiều thông tin chi tiết và phong phú hơn với gói PM2 Plus và PM2 Enterprise nếu có điều kiện thì bạn có thể trải nghiệm =))


#### Deployment

PM2 hỗ trợ chúng ta một file ecosystem.config.js để quan lý nhiều ứng dụng. file này chứa các thông tin như name, environments, scripts file, logs, node instances,... Để tạo file, dùng lệnh sau:

```bat
pm2 ecosystem
```

Sau khi chạy lệnh, PM2 sẽ tạo cho chúng ta file `ecosystem.config.js`:

```text
module.exports = {
apps : [{
    name: 'app', // application name 
    script: 'app.js', // script path to pm2 start

    // Options reference: https://pm2.io/doc/en/runtime/reference/ecosystem-file/
    args: 'one two', // string containing all arguments passed via CLI to script
    instances: 1, // number process of application
    autorestart: true, //auto restart if app crashes
    watch: false,
    max_memory_restart: '1G', // restart if it exceeds the amount of memory specified
    env: {
      NODE_ENV: 'development'
    },
    env_production: {
      NODE_ENV: 'production'
    }
  }, {
     name: 'worker',
     script: 'worker.js'
  }],
   
  // Deployment Configuration
  deploy : {
    production : {
       "user" : "ubuntu",
       "host" : ["192.168.0.13", "192.168.0.14", "192.168.0.15"],
       "ref"  : "origin/master",
       "repo" : "git@github.com:Username/repository.git",
       "path" : "/var/www/my-repository",
      "post-deploy" : 'npm install && pm2 reload ecosystem.config.js --env production'
    }
  }
};
```

Ở file trên, các bạn có thể thấy là chúng ta sẽ config deploy cho môi trường production, tương tự bạn cũng có thể config thêm môi trường staging hoặc khác. Mình có thêm một số attributes như `args`, `instances`, `autorestart`, `watch`, `max_memory_restart`,... Các bạn có thể tham khảo thêm các attributes khác [tại đây](https://pm2.keymetrics.io/docs/usage/application-declaration/#attributes-available).

Thay vì chạy `pm2 start app.js` như trước, giờ bạn sẽ chạy ứng dụng bằng command sau:

```bat
pm2 start ecosystem.config.js
```

Để deploy application thì tiên bạn cần chạy command:

```bat
$ pm2 deploy production setup // run remote setup commands

// or staging
$ pm2 deploy staging setup
```

Ở lần đầu thì nó sẽ pull source code của bạn về và setup. Ở các lần deploy tiếp theo, bạn chỉ cần chạy command:

```bat
$ pm2 deploy production update // update deploy to the latest release

// or
$ pm2 deploy staging update
```

Tham khảo thêm về PM2 Deployment [tại đây](https://pm2.keymetrics.io/docs/usage/deployment/).

#### Cluster Mode

Đối với các ứng dụng Node.js, PM2 bao gồm một bộ cân bằng tải tự động (automatic load balancer) sẽ chia sẻ tất cả các kết nối HTTP[s]/Websocket/TCP/UDP giữa mỗi processes được tạo ra. Cluster mode cho phép Node.js application sử dụng tất cả các CPUs của server. Điều này làm tăng đáng kể hiệu năng và độ tin cậy của các ứng dụng, tùy thuộc vào số lượng CPU có sẵn của server.

Để khởi động ứng dụng Cluster Mode thì bạn chỉ cần thêm options `-i` như sau:

```bat
pm2 start index.js -i max
```

Trong đó `max` có nghĩa là PM2 sẽ tự động phát hiện số lượng CPU có sẵn và chạy càng nhiều process càng tốt.


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
- [10+ Best MongoDB Monitoring Tools and Services 2022 Comparison](https://sematext.com/blog/mongodb-monitoring-tools/)

- [NodeJS có thực sự nhanh như bạn nghĩ? 🤔](https://viblo.asia/p/nodejs-co-thuc-su-nhanh-nhu-ban-nghi-m68Z0Pe9ZkG)
- [Tổng quan về PM2 – Trình quản lý các ứng dụng NodeJS](https://viblo.asia/p/tong-quan-ve-pm2-trinh-quan-ly-cac-ung-dung-nodejs-djeZ1EYYZWz)
- [Tổng quan về PM2](https://viblo.asia/p/tong-quan-ve-pm2-3P0lPkkmZox)
- [Sử dụng PM2 API để quản lý các tiến trình NodeJs](https://viblo.asia/p/su-dung-pm2-api-de-quan-ly-cac-tien-trinh-nodejs-bWrZnLMp5xw)
- [Auto deploy Node.js app lên server qua SSH với GitLab CI/CD và PM2](https://viblo.asia/p/auto-deploy-nodejs-app-len-server-qua-ssh-voi-gitlab-cicd-va-pm2-1Je5Ed44lnL)
- [Tạo Logger trong ứng dụng NodeJs với thư viện winston](https://viblo.asia/p/tao-logger-trong-ung-dung-nodejs-voi-thu-vien-winston-djeZ1G885Wz)
- [Find bottlenecks in Node.js apps with Clinic Flame](https://dev.to/mpangrazzi/find-bottlenecks-in-nodejs-apps-with-clinic-flame-3i0h)
- [Prometheus installation on Windows](http://www.liferaysavvy.com/2021/07/prometheus-installation-on-windows.html)
- [Add a Status Monitor to an Express App with express-status-monitor](https://javascript.plainenglish.io/add-a-status-monitor-to-an-express-app-with-express-status-monitor-35fd7f36a8e8)
- [How to run a node.js application permanently?](https://www.geeksforgeeks.org/how-to-run-a-node-js-application-permanently/)