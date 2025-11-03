---
layout: post
title: "Cách tạo ứng dụng React/Express/MongoDB đầy đủ bằng Docker"
subtitle: "How to create a full stack React/Express/MongoDB app using Docker"
date: 2025-11-01 01:00:00
tags:
- Docker
- React
- Express
- MongoDB
---

- [Tại sao bạn nên quan tâm tới Docker?](#tại-sao-bạn-nên-quan-tâm-tới-docker)
- [Chuẩn bị nào!](#chuẩn-bị-nào)
- [Dockerfile](#dockerfile)
- [Container Docker ở khắp mọi nơi!](#container-docker-ở-khắp-mọi-nơi)
- [Container hóa Client](#container-hóa-client)
- [Container hóa API của bạn](#container-hóa-api-của-bạn)


![Docker](https://boxxv.github.io/img/2025/MERN-Tech-Visual.png "MERN")

Trong hướng dẫn này, tôi sẽ hướng dẫn bạn quy trình chứa React FrontEnd, Node/Express API và cơ sở dữ liệu MongoDB bằng cách sử dụng container Docker theo cách rất đơn giản.

> Tôi sẽ không đi sâu vào chi tiết về cách làm việc với bất kỳ công nghệ nào. Thay vào đó, tôi sẽ để lại các liên kết, phòng trường hợp bạn muốn tìm hiểu thêm về bất kỳ công nghệ nào.
> Mục tiêu là cung cấp cho bạn hướng dẫn thực tế về cách đóng gói ứng dụng Full-Stack đơn giản này, làm nền tảng để bạn bắt đầu xây dựng ứng dụng của riêng mình.


## Tại sao bạn nên quan tâm tới Docker?

Docker đơn giản là một trong những công nghệ quan trọng nhất hiện nay. Nó cho phép bạn chạy các ứng dụng bên trong các container gần như tách biệt khỏi "mọi thứ".

Mỗi container giống như một máy ảo riêng biệt, loại bỏ mọi thứ không cần thiết để chạy ứng dụng. Điều này làm cho container rất nhẹ, nhanh và an toàn.

Container cũng được thiết kế để có thể dùng một lần. Nếu một container bị lỗi, bạn có thể dễ dàng xóa nó và tạo một container khác giống hệt mà không tốn công sức nhờ hệ thống hình ảnh container.

Một điều tuyệt vời khác của Docker là ứng dụng bên trong container sẽ chạy giống nhau trên mọi hệ thống (Windows, Mac hoặc Linux). Điều này thật tuyệt vời nếu bạn đang phát triển trên máy của mình và sau đó muốn triển khai nó lên một nhà cung cấp đám mây nào đó như GCP hoặc AWS.


## Chuẩn bị nào!

1. Hãy đảm bảo bạn đã chạy Node và Docker trên máy.
2. Tôi sẽ sử dụng ứng dụng React/Express mà chúng ta đã xây dựng trong hướng dẫn trước có tên là Tạo React FrontEnd, Node/Express BackEnd và kết nối chúng lại với nhau. Bạn có thể làm theo hướng dẫn đó trước hoặc sao chép kho lưu trữ GitHub này với boilerplate nếu bạn không quan tâm đến quá trình tạo ứng dụng React và Express.
3. Nếu bạn chọn sử dụng kho lưu trữ, đừng quên npm install bên trong thư mục Client và API để cài đặt tất cả các dependency cần thiết.
4. Và… vậy là xong. Bạn đã sẵn sàng để bắt đầu đóng gói mọi thứ :)


## Dockerfile

Theo tài liệu:

> Dockerfile là một tài liệu văn bản chứa tất cả các lệnh mà người dùng có thể gọi trên dòng lệnh để lắp ráp một hình ảnh. Docker có thể tự động xây dựng hình ảnh bằng cách đọc hướng dẫn từ Dockerfile.


## Container Docker ở khắp mọi nơi!

Việc container hóa ứng dụng của bạn với Docker cũng đơn giản như việc tạo một Dockerfile cho mỗi ứng dụng, trước tiên là build một image, sau đó chạy từng image để container hoạt động.


## Container hóa Client

Để build image Client, bạn sẽ cần một Dockerfile. Hãy cùng tạo một cái:

1. Mở ứng dụng React/Express trong trình soạn thảo mã yêu thích của bạn (tôi đang sử dụng VS Code).
2. Điều hướng đến thư mục Client.
3. Tạo một file mới có tên Dockerfile.
4. Đặt đoạn mã sau vào file:

```txt
# Use a lighter version of Node as a parent image
FROM mhart/alpine-node:8.11.4

# Set the working directory to /client
WORKDIR /client

# copy package.json into the container at /client
COPY package*.json /client/

# install dependencies
RUN npm install

# Copy the current directory contents into the container at /client
COPY . /client/

# Make port 3000 available to the world outside this container
EXPOSE 3000

# Run the app when the container launches
CMD ["npm", "start"]
```

Lệnh này sẽ hướng dẫn Docker xây dựng một image (sử dụng các cấu hình này) cho Client của chúng ta. Bạn có thể đọc toàn bộ về Dokerfile [tại đây](https://docs.docker.com/reference/dockerfile#usage).


## Container hóa API của bạn

Để xây dựng image API, bạn sẽ cần một Dockerfile khác. Hãy cùng tạo nó:

1. Điều hướng đến thư mục API.
2. Tạo một tệp mới có tên Dockerfile.
3. Chèn đoạn mã sau vào bên trong:

```txt
# Use a lighter version of Node as a parent image
FROM mhart/alpine-node:8.11.4

# Set the working directory to /api
WORKDIR /api

# copy package.json into the container at /api
COPY package*.json /api/

# install dependencies
RUN npm install

# Copy the current directory contents into the container at /api
COPY . /api/

# Make port 80 available to the world outside this container
EXPOSE 80

# Run the app when the container launches
CMD ["npm", "start"]
```

Lệnh này sẽ hướng dẫn Docker xây dựng một image (sử dụng các cấu hình này) cho API của chúng ta. Bạn có thể đọc toàn bộ về Dokerfile [tại đây](https://docs.docker.com/reference/dockerfile#usage).


# Docker-Compose

Bạn có thể chạy từng container riêng lẻ bằng Dokerfiles. Trong trường hợp này, chúng ta có 3 container cần quản lý, vì vậy chúng ta sẽ sử dụng docker-compose. Compose là một công cụ để định nghĩa và chạy các ứng dụng Docker đa container.

Để tôi chỉ cho bạn cách sử dụng nó đơn giản như thế nào:

1. Mở ứng dụng React/Express trong trình soạn thảo mã của bạn.
2. Trong thư mục chính của ứng dụng, hãy tạo một tệp mới và đặt tên là docker-compose.yml.
3. Viết đoạn mã này vào tệp docker-compose.yml:


```yml
version: "2"
services:
    client:
        image: webapp-client
        restart: always
        ports:
            - "3000:3000"
        volumes:
            - ./client:/client
            - /client/node_modules
        links:
            - api
        networks:
            webappnetwork
    api:
        image: webapp-api
        restart: always
        ports:
            - "9000:9000"
        volumes:
            - ./api:/api
            - /api/node_modules
        depends_on:
            - mongodb
        networks:
            webappnetwork
```

Đó là phép thuật gì vậy?

Bạn nên đọc tất cả về docker-compose [tại đây](https://docs.docker.com/compose/).

Về cơ bản, tôi đang nói với Docker rằng tôi muốn xây dựng một container có tên là **client**, sử dụng image **webapp-client** (là image chúng ta đã định nghĩa trong Client Dockerfile) sẽ lắng nghe trên cổng 3000. Sau đó, tôi nói với nó rằng tôi muốn xây dựng một container có tên là api bằng image **webapp-api** (là image chúng ta đã định nghĩa trong API Dockerfile) sẽ lắng nghe trên cổng 9000.

> Lưu ý rằng có nhiều cách để viết tệp docker-compose.yml. Bạn nên tìm hiểu tài liệu và sử dụng cách nào phù hợp nhất với nhu cầu của mình.


## Thêm cơ sở dữ liệu MongoDB

Để thêm cơ sở dữ liệu MongoDB, bạn chỉ cần thêm các dòng mã sau vào tệp docker-compose.yml:

```yml
    mongodb:
        image: mongo
        restart: always
        container_name: mongodb
        volumes:
            - ./data-node:/data/db
        ports:
            - 27017:27017
        command: mongod --noauth --smallfiles
        networks:
            - webappnetwork
```

Thao tác này sẽ tạo một container sử dụng [image MongoDB chính thức](https://hub.docker.com/_/mongo/).


## Tạo một mạng chia sẻ cho các container của bạn

Để tạo mạng chia sẻ cho vùng chứa của bạn, chỉ cần thêm đoạn mã sau vào tệp docker-compose.yml:

```yml
networks:
    webappnetwork:
        driver: bridge
```

Lưu ý rằng bạn đã định nghĩa từng vùng chứa của ứng dụng để sử dụng mạng này.

Cuối cùng, tệp docker-compose.yml của bạn sẽ trông như thế này:

![docker-compose.yml](https://boxxv.github.io/img/2025/1_fvR6-pUlGRddeCJKFnoTsg.png "MERN")

Trong tệp `docker-compose.yml`, thụt lề rất quan trọng. Hãy lưu ý điều này.


## Chạy các container của bạn

1. Bây giờ bạn đã có tệp docker-compose.yml, hãy bắt đầu build image. Vào terminal và chạy lệnh sau trên thư mục chính của ứng dụng:

```bat
docker-compose build
```

2. Bây giờ, để Docker khởi động các container, chỉ cần chạy:

```bat
docker-compose up
```

Và… thật kỳ diệu, giờ đây bạn có Client, API và Database, tất cả đều chạy trong các container riêng biệt chỉ với một lệnh. Thật tuyệt phải không?


## Kết nối API của bạn với MongoDB

Trước tiên, hãy cài đặt Mongoose để hỗ trợ kết nối với MongoDB. Trên terminal, hãy nhập:

```bat
npm install mongoose
```

1. Bây giờ hãy tạo một tệp có tên testDB.js trong thư mục tuyến API của bạn và chèn đoạn mã này:

```javascript
const express = require("express");
const router = express.Router();
const mongoose = require("mongoose");

// Variable to be sent to Frontend with Database status
let databaseConnection = "Waiting for Database response...";
router.get("/", function(req, res, next) {
    res.send(databaseConnection);
});

// Connecting to MongoDB
mongoose.connect("mongodb://mongodb:27017/test");

// If there is a connection error send an error message
mongoose.connection.on("error", error => {
    console.log("Database connection error:", error);
    databaseConnection = "Error connecting to Database";
});

// If connected to MongoDB send a success message
mongoose.connection.once("open", () => {
    console.log("Connected to Database!");
    databaseConnection = "Connected to Database";
});

module.exports = router;
```

Được rồi, hãy xem đoạn mã này đang làm gì. Đầu tiên, tôi import Express, ExpressRouter và Mongoose để sử dụng trên route /testDB của chúng ta. Sau đó, tôi tạo một biến sẽ được gửi dưới dạng phản hồi cho biết điều gì đã xảy ra với yêu cầu. Tiếp theo, tôi kết nối với cơ sở dữ liệu bằng Mongoose.connect(). Tiếp theo, tôi kiểm tra xem kết nối có hoạt động hay không và thay đổi biến (tôi đã tạo trước đó) cho phù hợp. Cuối cùng, tôi sử dụng module.exports để xuất route này để có thể sử dụng nó trên tệp app.js.

2. Bây giờ bạn phải "yêu cầu" Express sử dụng route bạn vừa tạo. Trong thư mục API, hãy mở tệp app.js và chèn hai dòng mã này:

```javascript
var testDBRouter = require("./routes/testDB");
app.use("/testDB", testDBRouter);
```

Điều này sẽ "báo" cho Express biết rằng mỗi khi có yêu cầu đến điểm cuối /testDB, nó sẽ sử dụng hướng dẫn trên tệp testDB.js.

3. Bây giờ, hãy kiểm tra xem mọi thứ đã hoạt động bình thường chưa. Vào terminal và nhấn control + C để tắt các container. Sau đó, chạy docker-compose up để khởi động lại chúng. Sau khi mọi thứ hoạt động bình thường, nếu bạn truy cập http://localhost:9000/testDB, bạn sẽ thấy thông báo "Connected to Database" (Đã kết nối với cơ sở dữ liệu).

Cuối cùng, tệp app.js của bạn sẽ trông như thế này:

![api/app.js](https://boxxv.github.io/img/2025/1_Qoe3NkYi8ON1ZOg5Z8sMUw.png "MERN")

Vâng… điều đó có nghĩa là API hiện đã được kết nối với cơ sở dữ liệu. Nhưng FrontEnd của bạn vẫn chưa biết. Hãy cùng xử lý vấn đề đó ngay bây giờ.


## Gửi yêu cầu từ React đến Cơ sở dữ liệu

Để kiểm tra xem ứng dụng React có thể truy cập Cơ sở dữ liệu hay không, hãy tạo một yêu cầu đơn giản đến điểm cuối bạn đã xác định ở bước trước.

1. Truy cập thư mục Client và mở tệp App.js.
2. Bây giờ, hãy chèn đoạn mã này bên dưới phương thức callAPI():

```javascript
callDB() {
    fetch("http://localhost:9000/testDB")
        .then(res => res.text())
        .then(res => this.setState({ dbResponse: res }))
        .catch(err => err);
}
```

Phương thức này sẽ lấy điểm cuối bạn đã xác định trước đó trên API và lấy phản hồi. Sau đó, nó sẽ lưu trữ phản hồi trong trạng thái của thành phần.

4. Thêm một biến vào trạng thái của thành phần để lưu trữ phản hồi:

```javascript
<p className="App-intro">{this.state.dbResponse}</p>
```

Cuối cùng, tệp App.js của bạn sẽ trông như thế này:

![client/App.js](https://boxxv.github.io/img/2025/1_mdxiukwWZ1SfggB_FYgUnQ.png "MERN")


## Cuối cùng, chúng ta hãy xem mọi thứ có hoạt động không

Trên trình duyệt, hãy truy cập http://localhost:3000/ và nếu mọi thứ hoạt động bình thường, bạn sẽ thấy ba thông báo sau:

Chào mừng đến với React
API đang hoạt động bình thường
Đã kết nối với Cơ sở dữ liệu
Đại loại như thế này:

![http://localhost:3000](https://boxxv.github.io/img/2025/11_0fTn6ATAKntrKlBqcwjawg.png "MERN")


## Xin chúc mừng!!!

Giờ đây, bạn đã có một ứng dụng full-stack với React FrontEnd, Node/Express API và cơ sở dữ liệu MongoDB. Tất cả đều chạy trong các container Docker riêng lẻ được điều phối bằng một tệp docker-compose đơn giản.

Ứng dụng này có thể được sử dụng như một mẫu để xây dựng ứng dụng mạnh mẽ hơn.

Bạn có thể tìm thấy tất cả mã tôi đã viết trong [kho lưu trữ dự án](https://github.com/Joao-Henrique/Docker_Medium_Tutorial).

Hãy mạnh mẽ và tiếp tục viết code!!!

…và đừng quên thể hiện thật xuất sắc hôm nay nhé ;)


-----
Tham khảo:
- [How to create a full stack React/Express/MongoDB app using Docker](https://medium.com/free-code-camp/create-a-fullstack-react-express-mongodb-app-using-docker-c3e3e21c4074)
- [Containerizing a Slack Clone App Built with the MERN Stack](https://www.docker.com/blog/containerizing-a-slack-clone-app-built-with-the-mern-stack/)
- [Dockerizing a Node.js, Express, MongoDB App with NGINX Reverse Proxy using Docker Compose](https://youtu.be/4zUQEkDdNR0)
- [Docker cơ bản](https://boxxv.github.io/2022/03/05/docker-co-ban/)
- []()