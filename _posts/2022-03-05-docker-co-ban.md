---
layout: post
title: Docker cơ bản
subtitle: Docker và những điều cần biết

tags:
- Docker
---

![Docker](https://boxxv.github.io/img/posts/docker.jpg "Docker")

## Docker là gì?

Docker là một dự án mã nguồn mở giúp tự động triển khai các ứng dụng Linux và Windows vào trong các container ảo hóa. Docker cung cấp một lớp trừu tượng và tự động ảo hóa dựa trên LinuxDocker là một dự án mã nguồn mở giúp tự động triển khai các ứng dụng Linux và Windows vào trong các container ảo hóa. Docker cung cấp một lớp trừu tượng và tự động ảo hóa dựa trên Linux

Docker giúp ta có thể chạy project ở một môi trường cụ thể, được định sẵn rõ ràng, độc lập với môi trường gốc. Docker cung cấp cách để building, deploying và running ứng dụng dễ dàng hơn bằng cách sử dụng các containers (trên nền tảng ảo hóa) để đóng gói ứng dụng.

## Lợi ích của Docker

Trước đây, việc setup và deploy application lên một hoặc nhiều server rất vất vả từ việc phải cài đặt các công cụ, môi trường cần cho application đến việc chạy được ứng dụng chưa kể việc không đồng nhất giữa các môi trường trên nhiều server khác nhau.

Docker cho phép các developers tạo các môi trường độc lập và tách biệt để khởi chạy và phát triển ứng dụng và môi trường này được gọi là container. Khi cần deploy lên bất kỳ server nào chỉ cần run container của Docker thì application của bạn sẽ được khởi chạy ngay lập tức.

### Những điều Docker mang lại
1. Docker cho các bạn 1 môi trường mục tiêu cụ thể, ví dụ các bạn cần môi trường Ubuntu, có PHP 7.2 có NodeJS 8.0, có mysql 5.2. Docker sẽ giúp bạn có được điều đó.
2. Môi trường trong Docker độc lập so với môi trường gốc: Docker sẽ tạo ra cho các bạn môi trường "ảo" trong đó các bạn có thể chạy project của mình, bất kể hệ điều hành gốc của các bạn có là gì. Do đó, kể cả bạn ở Win hay Mac thì vẫn có thể chạy project dưới môi trường Ubuntu hay bất cứ môi trường nào (mà hiện tại Docker support) bạn cần.
3. Một môi trường Docker sau khi được định nghĩa nó sẽ là "bất biến". Bạn có thể setup ở bất kì đâu bất kì máy nào với môi trường giống hệt bạn đã định nghĩa.
4. Mỗi một project sẽ có một file cấu hình cụ thể, 10 năm sau bạn đọc lại project thì vẫn biết để chạy được project đó thì cần những gì và cần làm gì. Bạn chỉ cần đưa file cấu hình cho người khác là họ sẽ tự biết phải làm gì để chạy
5. Vì mỗi project chúng ta có thể setup ở một môi trường riêng, nên các project sẽ không bị xung đột, chia sẻ tài nguyên lằng nhằng (nếu như ta không muốn). Từ đó giảm thiểu tối đa sự phụ thuộc lẫn nhau, cài đặt, thêm bớt sửa xóa các thư viện, cấu hình cũng sẽ không bị ảnh hưởng tới các project khác.
6.Docker có thể giúp tự động Heal (tự hồi phục, khởi động lại) nếu trong trường hợp có lỗi.

### Lợi ích khi sử dụng Docker
1. Với sự hỗ trợ của docker, việc coding, testing, deploying trở nên đơn giản hơn.
2. Khả năng di động (portable): môi trường develop được dựng lên bằng docker có thể chuyển từ người này sang người khác mà không làm thay đổi cấu hình ở trong. Trong kỹ thuật, được gọi là provisioning.
3. Application-centric: docker được dùng trên nhiều môi trường, đặc biệt tương thích trên môi trường develop, hướng đến việc coding thuận tiện nhất.
4. Versioning: docker được tích hợp VCS-git, để tracking các dòng lệnh thiết lập, hay đánh dấu version.
5. Component re-use: nghĩa là docker có khả năng sử dụng lại resource trước đó, bằng cách đánh dấu những resources giống nhau bằng một mã ID. Các môi trường được dựng lên sau đó sẽ kiểm tra các mã ID trước đó, nếu trùng docker sẽ sử dụng lại.
6. Sharing: với Docker Hub (public registry), các developer có thể tìm và sử dụng các môi trường được dựng sẵn.

### Lý do sử dụng Docker
- Khi project của chúng ta có nhiều người cùng làm, người dùng Win, người dùng Mac, người dùng Linux, nhưng cách để cài các phần mềm, thư viện để có thể chạy được project lại khác nhau ở mỗi nền tảng, đồng thời khi cài có thể làm thay đổi project. Dẫn tới việc project chạy không đúng, sai ở các nền tảng khác nhau.
- Sự sợ hãi nhất của mình ngày xưa đó là code Local ngon lắm rồi, nhưng lên server thì ngủm củ tỏi 😄.
- Mỗi project cần rất nhiều thứ đi kèm: MySQL, Redis, các extensions,... Và việc nhớ cài cho đúng từng cái đã rất mệt, nhớ cách cấu hình cho đúng lại càng mệt hơn. Và sự SỢ HÃI lớn nhất là khi cài mà bị lỗi, mà lỗi xong xóa đi cài lại lại không được như cũ.
- Khi chúng ta có nhiều project, dùng chung nhiều thứ, dẫn tới khi muốn thay đổi, sửa đổi 1 tài nguyên dùng chung nào đó sẽ làm các project liên quan ảnh hưởng.
- Và 1 trường hợp mình thấy đau khổ nhất. Đó là khi ta chuyển môi trường (chuyển server chẳng hạn), ta cần bê nguyên cục project cũ và chuyển sang môi trường mới. Lúc này NỖI SỢ 😈 mới thực sự hiện rõ. Làm sao để có thể chuyển toàn bộ data, cấu hình lại từ đầu với hàng tỉ bước, cài hàng tỉ thứ
- .... bla và blo

Tất cả những điều trên Docker sẽ giúp các bạn giải quyết một các rất chi là đơn giản, dễ dàng

### OS nào có thể dùng Docker:
1. Linux: Ubuntu 12.04+, Fedora 19/20+, RHEL 6.5+, CentOS 6+, Gentoo, ArchLinux, openSUSE 12.3+, CRUX 3.0+
2. Cloud: Amazon EC2m Google Compute Engine, Microsoft Azure,…
3. Max OS X
4. Windows: Windows 7+


## Các thành phần chính, khái niệm của Docker

![Docker](https://boxxv.github.io/img/posts/0_CP98BIIBgMG2K3u5.png "Docker")

**Docker images**: nó là cấu trúc chính của Docker Container. Nó bao gồm tất cả những thứ cần thiết để dự án của bạn có thể chạy được như một hệ điều hành hay các dependencies. Các Image được chia sẻ công khai ở Docker Hub để tất cả mọi người có thể cùng nhau sử dụng và phát triển.

**Docker container**: là đơn vị phần mềm cung cấp cơ chế đóng gói ứng dụng, mã nguồn, thiết lập, thư viện... vào một đối tượng duy nhất. Nó là một môi trường hoàn hảo cung cấp mọi thứ để chương trình có thể hoạt động được, không chịu sự tác động từ môi trường của hệ thống cũng như không làm ảnh hưởng ngược lại về phía hệ thống chứa nó.

**Dockerfile**: Là một file dạng text không có phần đuôi mở rộng, chứa các đặc tả về môi trường thực thi phần mềm, cấu trúc cho Docker image. Docker image có thể được tạo ra tự động bằng cách đọc các chỉ dẫn trong Dockerfile. Từ những câu lệnh đó, Docker sẽ build ra Docker image

**Dockerhub**: là dịch vụ cloud lưu trữ các image của các cá nhân hoặc công ty. Nó cho phép người dùng sử dụng và phát triển

**Port**: Vì môi trường trong Docker độc lập hoàn toàn so với môi trường gốc. Nên để có thể sử dụng được ứng dụng chạy trong Docker thì ta cần mở port từ Docker để bên ngoài có thể gọi vào được.

**Volume**: Vì môi trường Docker độc lập nên hệ thống file của ứng dụng chạy trong Docker cũng độc lập, mà thực tế thì hầu như ta luôn cần lưu lại file: lưu trữ DB, lưu trữ log, ảnh,... Do đó để môi trường gốc truy cập được vào file system của ứng dụng chạy trong Docker thì ta cần tới Volume


## Cài đặt

#### Docker
- Cài đặt cho Windows: [Install Docker Desktop on Windows](https://docs.docker.com/desktop/install/windows-install/)
- Cài đặt cho Ubuntu: [Install Docker Desktop on Linux](https://docs.docker.com/desktop/install/linux-install/)
- Cài đặt cho Mac: [Install Docker Desktop on Mac](https://docs.docker.com/desktop/install/mac-install/)

Cài xong nhớ check xem đã thành công hay chưa nhé. Chạy thử command để check:
```bat
docker --version
```

#### Docker-compose

Để chạy các project trong Docker thì ta có thể dùng command sau để chạy từng container cần thiết:
```bat
docker run containerA
docker run containerB
....
```

NHƯNG khi chạy dự án thực tế thì hầu như ta sẽ sử dụng docker-compose để chạy project, vì thực tế hầu như ta luôn cần nhiều hơn 1 container cho 1 project. Do đó trong series này mình sẽ dùng `docker-compose` để chạy các project demo trong các bài. Yên tâm đi dùng docker-compose không cần thêm nhiều não đâu các bạn nhé, giống nhau cả thôi 😉

Docker-compose là tool để cấu hình và chạy nhiều docker container cùng lúc. Dùng docker-compose sẽ giúp ta dễ dàng hơn trong việc chạy cùng lúc 1 hoặc 1 số container cần thiết cho project, đồng thời giúp ta dễ dàng visualize (nhìn) tổng quan về project.

Cài đặt:
- Với Win và Mac thì Docker-compose đã được tích hợp sẵn với Docker ở trên, các bạn không cần làm gì thêm
- Với Ubuntu, các bạn xem hướng dẫn [ở đây](https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-16-04) (nhớ đọc thật kĩ phần hướng dẫn, cài bản mới nhất và làm hết Step 1 là xong nhé)

Cài xong cũng check xem đã thành công hay chưa nhé. Chạy thử command để check:

```bat
docker-compose --version
```

## Cách tạo Docker Image từ Dockerfile

Một số câu lệnh trong Dockerfile

`FROM <base_image>:<phiên_bản>`: đây là câu lệnh bắt buộc phải có trong bất kỳ Dockerfile nào. Nó dùng để khai báo base Image mà chúng ta sẽ build mới Image của chúng ta.

`MAINTAINER <tên_tác_giả>`: câu lệnh này dùng để khai báo trên tác giả tạo ra Image, chúng ta có thể khai báo nó hoặc không.

`RUN <câu_lệnh>`: chúng ta sử dụng lệnh này để chạy một command cho việc cài đặt các công cụ cần thiết cho Image của chúng ta.

`CMD <câu_lệnh>`: trong một Dockerfile thì chúng ta chỉ có duy nhất một câu lệnh CMD, câu lệnh này dùng để xác định quyền thực thi của các câu lệnh khi chúng ta tạo mới Image.

`ENTRYPOINT <câu_lệnh>`: định nghĩa những command mặc định, cái mà sẽ được chạy khi container running.

Để tạo ra một image từ Dockerfile, chúng ta tạo một thư mục rỗng. Tạo một file tên Dockerfile nội dung như sau:

Build image từ Dockerfile đã tạo :

Với Dockerfile đã tạo ở trên, chúng ta có thể tiến hành build một image. Các bạn trỏ đường dẫn đến thư mục lưu Dockerfile và gõ lệnh:
```bat
docker build -t ubuntu:v1 -f Dockerfile .
```

Sau khi build thành công, thực hiện run image bằng lệnh:
```bat
docker run --name ubuntu-v1 93b103068d3f
```


## Cách tạo Docker Image trên Docker Hub

1. Tạo tài khoản và đăng nhập vào trang hub.docker.com

2. Tìm và click Create Repository

3. Điền các thông tin cần thiết và chọn public

4. Đăng nhập Docker Hub bằng command line:
```bat
docker login --username=<your_docker_hub_username>
```

5. Kiểm tra ID của image cần sử dụng:
```bat
docker images
```
Nếu image chưa được gắn tag thì hãy gắn tag cho nó bằng câu lệnh:
```bat
docker tag <image_id> <your_hub_username>/<your_repository>:<tag>
```
6. Để đưa Image lên Docker Hub bạn cần sử dụng câu lệnh:
```bat
docker push <your_hub_username>/<your_repository>:tag_name
```


## Tổng kết

Trong bài viết này mình đã giới thiệu cơ bản về docker cùng một số khái niệm quan trọng như Dockerfile, Docker Images, Docker Container... Mình rất mong nhận được sự góp ý từ mọi người.


-----
Tham khảo:
- [Docker cơ bản](https://viblo.asia/p/docker-co-ban-6J3Zgavq5mB)
- [Giới thiệu Docker](https://labs.flinters.vn/devops/gioi-thieu-docker/)
- [Giới thiệu và cài đặt WSL trên Windows](https://viblo.asia/p/gioi-thieu-va-cai-dat-wsl-tren-windows-1VgZvP025Aw)
- [Docker – Hãy hiểu theo cách của bạn](https://viblo.asia/p/docker-hay-hieu-theo-cach-cua-ban-Az45bnk65xY)
- [Dockerfile đơn giản hơn bạn nghĩ](https://viblo.asia/p/dockerfile-don-gian-hon-ban-nghi-jvEla16Dlkw)
- [Docker và những command nên nhớ](https://viblo.asia/p/docker-va-nhung-command-nen-nho-yMnKMvwaZ7P)
- [Docker compose có gì khó](https://viblo.asia/p/docker-compose-co-gi-kho-RQqKLLGOK7z)
- [Tìm hiểu docker compose qua các ví dụ cụ thể](https://viblo.asia/p/tim-hieu-docker-compose-qua-cac-vi-du-cu-the-yMnKMvQEZ7P)
- [Sử dụng environment variables trong docker](https://viblo.asia/p/su-dung-environment-variables-trong-docker-gDVK24aelLj)
- [Những câu hỏi hay khi phỏng vấn docker](https://viblo.asia/p/nhung-cau-hoi-hay-khi-phong-van-docker-phan-1-jvElaoGKkw)
- [Docker là gì? Kiến thức cơ bản về Docker](https://trungtq.com/2020/11/17/docker-la-gi-kien-thuc-co-ban-ve-docker/)
- [Docker – Những lý do bạn nên sử dụng Docker cho triển khai ứng dụng của bạn](https://viblo.asia/p/docker-nhung-ly-do-ban-nen-su-dung-docker-cho-trien-khai-ung-dung-cua-ban-gDVK2OJXZLj)
- [Docker là gì? Tại sao lập trình viên nên biết cách sử dụng docker?](http://tutorials.aiclub.cs.uit.edu.vn/index.php/2020/05/30/docker-co-ban-bai-1-docker-la-gi-tai-sao-lai-su-dung-docker/)
- [Lí do tôi yêu Docker](https://viblo.asia/p/li-do-toi-yeu-docker-ORNZqxRMK0n)
- [Docker: Deploy Nginx, Let's Encrypt web service có SSL đơn giản nhất](https://200lab.io/blog/docker-nginx-lets-encrypt-web-service-ssl/)
- [Dockerizing a Node.js web app](https://viblo.asia/p/dockerizing-a-nodejs-web-app-ByEZky0W5Q0)
- [Dockerize ứng dụng NodeJS](https://viblo.asia/p/dockerize-ung-dung-nodejs-RnB5pxEG5PG)
- [Dockerize ứng dụng VueJS, ReactJS](https://viblo.asia/p/dockerize-ung-dung-vuejs-reactjs-ORNZqxwNK0n)
- [[VueJS] Hướng dẫn deploy VueJS bằng docker](https://viblo.asia/p/vuejs-huong-dan-deploy-vuejs-bang-docker-gAm5yDGOldb)
- [Dev hiện đại phần 1: Setup môi trường dev với docker](https://viblo.asia/p/dev-hien-dai-phan-1-setup-moi-truong-dev-voi-docker-djeZ1RpQlWz)
- [Dev hiện đại phần 2: Chạy ứng dụng trên... localhost](https://viblo.asia/p/dev-hien-dai-phan-2-chay-ung-dung-tren-localhost-OeVKBDJ0lkW)
- [Run a React app in a docker](https://www.bogotobogo.com/DevOps/Docker/Docker-React-App.php)
- [Run a React app in a docker II](https://www.bogotobogo.com/DevOps/Docker/Docker-React-App-2-SnapShot.php)
- [Use Docker with a React Single-page App in Visual Studio](https://docs.microsoft.com/en-us/visualstudio/containers/container-tools-react?view=vs-2022)
- [Utilizing the power of Docker while building MERN Apps using mern-docker](https://dev.to/sujaykundu777/utilizing-the-power-of-docker-while-building-mern-apps-using-mern-docker-4olb)

- [mern-docker](https://github.com/sujaykundu777/mern-docker)
- [mern-docker-starter](https://github.com/joshdcuneo/mern-docker-starter)
- [mern-docker-compose](https://github.com/sidpalas/mern-docker-compose)
- [docker-mern](https://github.com/vladilenm/docker-mern)
- [docker-mern-nginx](https://github.com/bezkoder/docker-mern-nginx)
- [mern-stack](https://github.com/t-ho/mern-stack)