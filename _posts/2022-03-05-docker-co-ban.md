---
layout: post
categories: ["DevOps & Hạ tầng"]
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

**Dockerfile**: Là một file dạng text không có phần đuôi mở rộng, chứa các đặc tả về môi trường thực thi phần mềm, cấu trúc cho Docker image. Docker image có thể được tạo ra tự động bằng cách đọc các chỉ dẫn trong Dockerfile. Từ những câu lệnh đó, Docker sẽ build ra Docker image

**Docker images**: nó là cấu trúc chính của Docker Container. Nó bao gồm tất cả những thứ cần thiết để dự án của bạn có thể chạy được như một hệ điều hành hay các dependencies. Các Image được chia sẻ công khai ở Docker Hub để tất cả mọi người có thể cùng nhau sử dụng và phát triển.

**Docker container**: là đơn vị phần mềm cung cấp cơ chế đóng gói ứng dụng, mã nguồn, thiết lập, thư viện... vào một đối tượng duy nhất. Nó là một môi trường hoàn hảo cung cấp mọi thứ để chương trình có thể hoạt động được, không chịu sự tác động từ môi trường của hệ thống cũng như không làm ảnh hưởng ngược lại về phía hệ thống chứa nó.

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


## Bắt đầu với Docker trong một vài bước đơn giản!

```bat
docker run --name repo alpine/git clone https://github.com/docker/getting-started.git

Unable to find image 'alpine/git:latest' locally
latest: Pulling from alpine/git
530afca65e2e: Pull complete
a5ac19059327: Extracting [========================>                          ]  8.258MB/16.52MB
edc29284a664: Download complete
Digest: sha256:760aaf0d59c93f87572ec40dee1efd10a7ea13a78dff1f59a904e908449329ae
Status: Downloaded newer image for alpine/git:latest
Cloning into 'getting-started'...
```

```bat
docker cp repo:/git/getting-started/ .

cd getting-started

docker build -t docker101tutorial .
```

```bat
[+] Building 97.7s (25/25) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                                                                                             1.5s 
 => => transferring dockerfile: 1.12kB                                                                                                                                                                                                           0.0s 
 => [internal] load .dockerignore                                                                                                                                                                                                                1.8s 
 => => transferring context: 52B                                                                                                                                                                                                                 0.0s 
 => [internal] load metadata for docker.io/library/nginx:alpine                                                                                                                                                                                  5.8s 
 => [internal] load metadata for docker.io/library/python:alpine                                                                                                                                                                                 5.9s 
 => [internal] load metadata for docker.io/library/node:12-alpine                                                                                                                                                                                6.3s 
 => [app-base 1/5] FROM docker.io/library/node:12-alpine@sha256:d4b15b3d48f42059a15bd659be60afe21762aae9d6cbea6f124440895c27db68                                                                                                                32.8s 
 => => resolve docker.io/library/node:12-alpine@sha256:d4b15b3d48f42059a15bd659be60afe21762aae9d6cbea6f124440895c27db68                                                                                                                          0.6s 
 => => sha256:d4b15b3d48f42059a15bd659be60afe21762aae9d6cbea6f124440895c27db68 1.43kB / 1.43kB                                                                                                                                                   0.0s 
 => => sha256:df9b9388f04ad6279a7410b85cedfdcb2208c0a003da7ab5613af71079148139 2.81MB / 2.81MB                                                                                                                                                   2.9s 
 => => sha256:31f0fb9de071269230cb0f786012ae4e81d26e489b1fe922e57b5201e6bc9ab0 451B / 451B                                                                                                                                                       4.4s 
 => => extracting sha256:3bf6d738020517f4622814e8c21db4b4aaa78ae7cab4e4f872c11696886c6285                                                                                                                                                        1.2s 
 => => extracting sha256:7939e601ee5e4737cf7fdb6d1dfe31ca4c2697109290462f694710761450aef0                                                                                                                                                        0.1s 
 => => extracting sha256:31f0fb9de071269230cb0f786012ae4e81d26e489b1fe922e57b5201e6bc9ab0                                                                                                                                                        0.0s 
 => [internal] load build context                                                                                                                                                                                                                2.0s 
 => => transferring context: 10.45MB                                                                                                                                                                                                             0.1s 
 => [stage-6 1/3] FROM docker.io/library/nginx:alpine@sha256:87fb6f4040ffd52dd616f360b8520ed4482930ea75417182ad3f76c4aaadf24f                                                                                                                   27.5s 
 => => resolve docker.io/library/nginx:alpine@sha256:87fb6f4040ffd52dd616f360b8520ed4482930ea75417182ad3f76c4aaadf24f                                                                                                                            1.2s 
 => => sha256:87fb6f4040ffd52dd616f360b8520ed4482930ea75417182ad3f76c4aaadf24f 1.65kB / 1.65kB                                                                                                                                                   0.0s 
 => => sha256:323a7915bc0486f17181676df748e5c3571103eb8ac38137aa60ea87e9d70b19 7.39MB / 7.39MB                                                                                                                                                  10.1s 
 => => sha256:b5b558620e4027e2a918abda48eb0d3ecae77b6ced0f5244a55d78a02bcea87b 602B / 602B                                                                                                                                                       6.9s 
 => => sha256:a46fd6a16a7c6563c064f8ad9197db0bcf1191095cc3af29e75fb5e9b007f168 1.39kB / 1.39kB                                                                                                                                                  10.2s 
 => => extracting sha256:323a7915bc0486f17181676df748e5c3571103eb8ac38137aa60ea87e9d70b19                                                                                                                                                        0.3s 
 => => extracting sha256:b5b558620e4027e2a918abda48eb0d3ecae77b6ced0f5244a55d78a02bcea87b                                                                                                                                                        0.0s 
 => => extracting sha256:ba036c7f95ecc063c84fbe789765b97feefdbc331a31abf90153da5e16fe7264                                                                                                                                                        0.0s 
 => => extracting sha256:a46fd6a16a7c6563c064f8ad9197db0bcf1191095cc3af29e75fb5e9b007f168                                                                                                                                                        0.0s 
 => [base 1/4] FROM docker.io/library/python:alpine@sha256:ba6cfcca463537621aac63ffda4f93cd73e1f3dea59a83287603fbebd02444e4                                                                                                                     37.0s 
 => => resolve docker.io/library/python:alpine@sha256:ba6cfcca463537621aac63ffda4f93cd73e1f3dea59a83287603fbebd02444e4                                                                                                                           1.2s 
 => => sha256:ba6cfcca463537621aac63ffda4f93cd73e1f3dea59a83287603fbebd02444e4 1.65kB / 1.65kB                                                                                                                                                   0.0s 
 => => sha256:eb1dfcc4f9e9884135653d74000b3a174fd77cc76a557601e9b763a064ba67ef 7.04kB / 7.04kB                                                                                                                                                   0.0s 
 => => sha256:bd99fa58365b603cbeb71c93c19182410b640606f36158c10d7ee09d63c1a4f6 12.18MB / 12.18MB                                                                                                                                                19.3s 
 => => extracting sha256:bd99fa58365b603cbeb71c93c19182410b640606f36158c10d7ee09d63c1a4f6                                                                                                                                                        0.4s 
 => => extracting sha256:777a82aef5431a7852c25deef1cc9e479a3be2c2a9f49e41306b9da78184f1ef                                                                                                                                                        0.0s 
 => => extracting sha256:1ef14832cf3c6d891726d458ea44fb7be8662b778048035236efe234a7c2699f                                                                                                                                                        0.2s 
 => [app-base 2/5] WORKDIR /app                                                                                                                                                                                                                  4.7s 
 => [base 2/4] WORKDIR /app                                                                                                                                                                                                                      2.0s 
 => [app-base 3/5] COPY app/package.json app/yarn.lock ./                                                                                                                                                                                        3.3s 
 => [base 3/4] COPY requirements.txt .                                                                                                                                                                                                           3.3s 
 => [app-base 4/5] COPY app/spec ./spec                                                                                                                                                                                                          2.6s 
 => [base 4/4] RUN pip install -r requirements.txt                                                                                                                                                                                              34.2s 
 => [app-base 5/5] COPY app/src ./src                                                                                                                                                                                                            2.6s 
 => [app-zip-creator 1/4] COPY app/package.json app/yarn.lock ./                                                                                                                                                                                 1.9s 
 => [app-zip-creator 2/4] COPY app/spec ./spec                                                                                                                                                                                                   1.5s 
 => [app-zip-creator 3/4] COPY app/src ./src                                                                                                                                                                                                     2.1s 
 => [app-zip-creator 4/4] RUN apk add zip &&     zip -r /app.zip /app                                                                                                                                                                            7.4s 
 => [stage-6 2/3] COPY --from=app-zip-creator /app.zip /usr/share/nginx/html/assets/app.zip                                                                                                                                                      1.7s 
 => [build 1/2] COPY . .                                                                                                                                                                                                                         2.2s 
 => [build 2/2] RUN mkdocs build                                                                                                                                                                                                                 4.0s 
 => [stage-6 3/3] COPY --from=build /app/site /usr/share/nginx/html                                                                                                                                                                              1.9s 
 => exporting to image                                                                                                                                                                                                                           2.1s 
 => => exporting layers                                                                                                                                                                                                                          1.5s 
 => => writing image sha256:647aecfd59a6b7dc27737d1c79fa21fc1fda649a319c7cb28fa70dc872e126f7                                                                                                                                                     0.1s 
 => => naming to docker.io/library/docker101tutorial                                                                                                                                                                                             0.1s

Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them
```

```bat
docker run -d -p 80:80 --name docker-tutorial docker101tutorial
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
- [[Series] Học Docker, CICD từ cơ bản đến áp dụng vào thực tế](https://viblo.asia/s/series-hoc-docker-cicd-tu-co-ban-den-ap-dung-vao-thuc-te-jeZ103QgKWz)
- [Lí do tôi yêu Docker](https://viblo.asia/p/li-do-toi-yeu-docker-ORNZqxRMK0n)
- [Làm thế nào để dockerize ứng dụng của bạn](https://viblo.asia/p/lam-the-nao-de-dockerize-ung-dung-cua-ban-maGK7pBLZj2)
- [Dockerizing a Node.js web app](https://viblo.asia/p/dockerizing-a-nodejs-web-app-ByEZky0W5Q0)
- [Dockerize ứng dụng NodeJS](https://viblo.asia/p/dockerize-ung-dung-nodejs-RnB5pxEG5PG)
- [Dockerize ứng dụng VueJS, ReactJS](https://viblo.asia/p/dockerize-ung-dung-vuejs-reactjs-ORNZqxwNK0n)
- [[VueJS] Hướng dẫn deploy VueJS bằng docker](https://viblo.asia/p/vuejs-huong-dan-deploy-vuejs-bang-docker-gAm5yDGOldb)
- [Dockerize ứng dụng Python, Flask](https://viblo.asia/p/dockerize-ung-dung-python-flask-bWrZnxbY5xw)
- [Dockerize ứng dụng Laravel](https://viblo.asia/p/dockerize-ung-dung-laravel-vyDZOao75wj)
- [Docker and MongoDB](https://www.mongodb.com/compatibility/docker)
- [Dockerize Project NodeJS, MongoDB, Redis, Passport](https://viblo.asia/p/dockerize-project-nodejs-mongodb-redis-passport-4P856NXW5Y3)
- [Dockerize ứng dụng chat realtime với Laravel, Nginx, VueJS, Laravel Echo, Redis, SocketIO](https://viblo.asia/p/dockerize-ung-dung-chat-realtime-voi-laravel-nginx-vuejs-laravel-echo-redis-socketio-bJzKmxgY59N)
- [Deploy ứng dụng Docker Laravel Realtime Chat](https://viblo.asia/p/deploy-ung-dung-docker-laravel-realtime-chat-aWj53WJ156m)
- [Deploy ứng dụng Docker, NodeJS, Mongo, Redis](https://viblo.asia/p/deploy-ung-dung-docker-nodejs-mongo-redis-1VgZvMzYKAw)
- [Bảo mật ứng dụng Docker NodeJS, Mongo, Redis](https://viblo.asia/p/bao-mat-ung-dung-docker-nodejs-mongo-redis-GrLZDaaVlk0)
- [Deploy Node.js app đơn giản với Docker và Gitlab Registry](https://viblo.asia/p/deploy-nodejs-app-don-gian-voi-docker-va-gitlab-registry-ORNZq1nNZ0n)
- [Auto deploy với Docker và Gitlab CI](https://viblo.asia/p/auto-deploy-voi-docker-va-gitlab-ci-E375z4eRZGW)
- [Nhập môn CICD với Gitlab](https://viblo.asia/p/nhap-mon-cicd-voi-gitlab-07LKX9WPZV4)
- [GitLab CI/CD](https://viblo.asia/tags/gitlab-cicd)
- [Gitlab CI](https://viblo.asia/tags/gitlab-ci)
- [CI/CD](https://viblo.asia/tags/cicd)
- [How To Install Docker on Ubuntu](https://viblo.asia/p/how-to-install-docker-on-ubuntu-4P856p33ZY3)
- [How To Install Docker on Ubuntu](https://viblo.asia/p/how-to-install-docker-on-ubuntu-RnB5pmJ7KPG)
- [Automation Test với Docker và Gitlab CI](https://viblo.asia/p/automation-test-voi-docker-va-gitlab-ci-yMnKMv2DZ7P)
- [Tối ưu Docker image](https://viblo.asia/p/toi-uu-docker-image-Eb85o9D4Z2G)
- [Tăng tốc độ build và tối giản Docker image](https://viblo.asia/p/tang-toc-do-build-va-toi-gian-docker-image-Eb85oODB52G)
- [Giới thiệu Docker Network và HEALTHCHECK - 2 công cụ hữu ích từ Docker](https://viblo.asia/p/gioi-thieu-docker-network-va-healthcheck-2-cong-cu-huu-ich-tu-docker-bJzKmxXY59N)
- [Giám sát ứng dụng Docker với cAdvisor, Prometheus và Grafana](https://viblo.asia/p/giam-sat-ung-dung-docker-voi-cadvisor-prometheus-va-grafana-RQqKLevMZ7z)
- [Docker: Deploy Nginx, Let's Encrypt web service có SSL đơn giản nhất](https://200lab.io/blog/docker-nginx-lets-encrypt-web-service-ssl/)
- [Dev hiện đại phần 1: Setup môi trường dev với docker](https://viblo.asia/p/dev-hien-dai-phan-1-setup-moi-truong-dev-voi-docker-djeZ1RpQlWz)
- [Dev hiện đại phần 2: Chạy ứng dụng trên... localhost](https://viblo.asia/p/dev-hien-dai-phan-2-chay-ung-dung-tren-localhost-OeVKBDJ0lkW)
- [Từ phát triển tới triển khai](https://viblo.asia/s/tu-phat-trien-toi-trien-khai-dbZN7QzylYM)
- [https://github.com/minhpq331/docker-node-api](https://github.com/minhpq331/docker-node-api)
- [Từ phát triển tới triển khai phần 1: Backend, NodeJS, API](https://kipalog.com/posts/Tu-phat-trien-toi-trien-khai-phan-1--Backend--NodeJS--API)
- [Từ phát triển tới triển khai phần 1: Backend, NodeJS, API](https://viblo.asia/p/tu-phat-trien-toi-trien-khai-phan-1-backend-nodejs-api-djeZ1ReJlWz)
- [Từ phát triển tới triển khai phần 2: Frontend, VueJS, SPA - SSR](https://viblo.asia/p/tu-phat-trien-toi-trien-khai-phan-2-frontend-vuejs-spa-ssr-ByEZkN8AKQ0)
- [Docker image in production - câu chuyện 1GB hay 100MB](https://viblo.asia/p/docker-image-in-production-cau-chuyen-1gb-hay-100mb-LzD5dXyE5jY)
- [Thiết lập môi trường phát triển PHP với Docker](https://viblo.asia/p/thiet-lap-moi-truong-phat-trien-php-voi-docker-RQqKLqz0Z7z)
- [Deploy Serverless với Express và MongoDB](https://viblo.asia/p/deploy-serverless-voi-express-va-mongodb-GrLZDDagZk0)

-----

- [Run a React app in a docker](https://www.bogotobogo.com/DevOps/Docker/Docker-React-App.php)
- [Run a React app in a docker II](https://www.bogotobogo.com/DevOps/Docker/Docker-React-App-2-SnapShot.php)
- [Use Docker with a React Single-page App in Visual Studio](https://docs.microsoft.com/en-us/visualstudio/containers/container-tools-react?view=vs-2022)
- [Utilize Docker with this MERN Stack Tutorial Solution](https://adamtheautomator.com/mern-stack-tutorial/)
- [Utilizing the power of Docker while building MERN Apps using mern-docker](https://dev.to/sujaykundu777/utilizing-the-power-of-docker-while-building-mern-apps-using-mern-docker-4olb)
- [Migrating Full-Stack Apps from Poly-Repo to Mono-Repo](https://dev.to/martzcodes/migrating-full-stack-apps-from-poly-repo-to-mono-repo-17go)
- [How to use Docker in your Node and React Applications](https://dev.to/andrewbaisden/how-to-use-docker-in-your-node-and-react-applications-597e)
- [Build and Dockerize a Full-stack React app with Node.js, MySQL and Nginx](https://www.section.io/engineering-education/build-and-dockerize-a-full-stack-react-app-with-nodejs-and-nginx/)

-----

- [Nx, NestJs, React — Docker Deploys](https://medium.com/swlh/nx-nestjs-react-docker-deploys-928a55fc19fd)
- [Nx and Node Microservices](https://blog.nrwl.io/nx-and-node-microservices-b6df3cd1bad6)
- [Going TypeStack with NX Monorepo and Docker (Part 1)](https://blog.devgenius.io/going-typestack-with-nx-monorepo-and-docker-part-1-d5ff257981f2)
- [Going TypeStack with NX Monorepo and Docker (Part 2)](https://medium.com/dev-genius/going-typestack-with-nx-monorepo-and-docker-part-2-f66c543c7d8f)

-----

- [VIDEO - Docker Compose in 6 minutes! Mongo, Express, React, Node (MERN) Application Tutorial](https://youtu.be/0B2raYYH2fE)
- [VIDEO - Full MERN Website React Nodejs w/ GraphQL Tailwind and Docker From Zero To Deployment + GIVEAWAY](https://youtu.be/4ELH8CT4J0A)

-----

- [mern-docker](https://github.com/sujaykundu777/mern-docker)
- [mern-docker-starter](https://github.com/joshdcuneo/mern-docker-starter)
- [mern-docker-compose](https://github.com/sidpalas/mern-docker-compose)
- [docker-mern](https://github.com/vladilenm/docker-mern)
- [docker-mern-nginx](https://github.com/bezkoder/docker-mern-nginx)
- [mern-stack](https://github.com/t-ho/mern-stack)

- [https://www.npmjs.com/package/@nx-tools/nx-docker](https://www.npmjs.com/package/@nx-tools/nx-docker)