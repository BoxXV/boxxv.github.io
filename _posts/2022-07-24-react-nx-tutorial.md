---
layout: post
title: Hướng dẫn sử dụng React với Nx 
subtitle: React Nx Tutorial

tags:
- Front-End
- Back-End
- React
- Nx
- Monorepos
---

Microservices hiện nay được đề cập tới trong thế giới phần mềm, công nghệ được kỳ vọng cao và đánh giá như một xu hướng cho tương lai (Open API, service provider, …). Một số ý kiến cho rằng, microservices không có gì mới lạ, chẳng qua nó là SOA (kiến trúc hướng dịch vụ) được đánh bóng, đổi tên mà thôi. Mặc dù việc triển khai microservices dưới dạng multi-repo mang lại nhiều lợi ích tuy nhiên theo một số ý kiển, cách triển khai mã nguồn này có thể gây khó khăn trong một số trường hợp và thay vì triển khai cấu trúc mã nguồn dưới dạng chia thành nhiều repo riêng biệt, họ chọn cách tổ chức chỉ trong một repository duy nhất hay còn gọi là monorepo. Bài viết này sẽ nói về hai cách triển khai mã nguồn này cũng như so sánh các đặc điểm của chúng và cuối cùng là giới thiệu về Nx - một công cụ phát triển được giới thiệu rằng có thể dễ dàng mở rộng thường được sử dụng Monorepos.

# Multiple repositories và Mono repositories

![Monorepos](https://boxxv.github.io/img/posts/6ed2d04e-dde1-485a-a10c-7dc6d9a887a8.webp "Monorepos")

Không phải mỗi ứng dụng nào cũng được phát triển dưới dạng microservices. Tuy nhiên, dù có phải tái cấu trúc mã nguồn từ một khối nguyên khối hay không, chúng ta đều sẽ phải lựa chọn cách thức lưu trữ và quản lý mã nguồn theo kiểu multiple repositories (multirepo) hay mono repositories (monorepo). Sơ lược của hai kiểu cách thức lưu trữ và quản lý này như sau:
- Monorepo là kiểu cấu trúc project trong đó tất cả module (hoặc project con) đều nằm trong cùng 1 git repository.
- Multirepo, ngược lại, là kiểu cấu trúc project trong đó mỗi module (hoặc project con) chứa ở những git repository riêng lẻ.

Không thể phủ nhận rằng, việc lưu trữ và quản lý mã nguồn có một số các ưu điểm như sau:
- Phong cách mã nguồn linh hoạt và dễ dàng kiểm thử cho từng repositories
- Phân quyền rõ ràng cho người tham gia phát triển và bảo trì
- Codebase không quá lớn do đó dễ dàng quản lý

Tuy nhiên việc phát triển phần mềm thường hướng đến một ứng dụng tổng thể. Khi đó việc chia nhỏ ứng dụng thành nhiều phần riêng biệt có thể khiến cho việc nhầm lẫn về phạm vi cũng như mục đích và cách hoạt động của các module giữa các team trong toàn bộ tổ chức. Khi đó, các nhóm trở nên phân tán và có thể không biết rõ mục tiêu chính của dự án mà mình tham gia và do đó không bận tâm về những gì người khác đang làm miễn là công việc của họ được hoàn thành. Bên cạnh đó, một số nhận định rằng cách lưu trữ và quản lý này mất khá nhiều thời gian cũng như tài nguyên cùng với đó, trong một số trường hợp các phần của ứng dụng đều sử dụng cùng một ngôn ngữ thì việc có được phong cách mã nguồn linh hoạt không còn quá quan trong. Bởi vậy, họ cho rằng vấn đề này cũng như một số vấn đề kể trên và một số khác chưa kể đến có thể được giải quyết bằng cách sử dụng một phương pháp khác - monorepo.

Trong vài năm qua, Babel, Angular, React, Jest và nhiều dự án mã nguồn mở khác đã chuyển sang sử dụng monorepos. Monorepos không chỉ hữu ích cho các dự án nguồn mở. Chúng thậm chí còn phù hợp hơn cho các tổ chức đang phát triển các ứng dụng thực tế. Google, Facebook, Uber, Twitter đều làm được điều đó và họ đều có các công cụ dành cho nhà phát triển dễ dàng tùy chỉnh cung cấp vô vàn chức năng. Không phải tự nhiên, monorepo được sử dụng nhiều đến vậy và sau đây là một số ưu điểm có thể được kể đến:

- Tổ chức liền mạch: Với mono repo, các dự án có thể được tổ chức và nhóm lại với nhau theo bất kỳ cách nào bạn thấy là nhất quán về mặt logic nhất. Sử dụng một repo duy nhất cũng làm giảm chi phí quản lý các phần dependencies.
- Cải thiện văn hóa làm việc chung giữa các nhóm: Với việc áp dụng mono repo, mọi cá nhân trong tổ chức đều nhận thức được các mục tiêu của ứng dụng và điều này làm cho cả tổ chức trở thành một nhóm thống nhất và do đó có thể đóng góp cụ thể hơn cho các mục tiêu và mục tiêu của tổ chức.
- Phối hợp tốt hơn giữa các nhà phát triển: Các nhà phát triển có thể dễ dàng chạy toàn bộ nền tảng trên máy của họ và điều này giúp họ hiểu tất cả các dịch vụ và cách chúng làm việc cùng nhau. Điều này đã khiến các nhà phát triển tìm thấy nhiều lỗi cục bộ hơn trước khi gửi một pull request.
- Tái cấu trúc dễ dàng: Bất kỳ lúc nào chúng ta muốn đổi tên một cái gì đó, việc tái cấu trúc trở nên vô cùng dễ dàng. Việc tái cấu trúc cũng dễ dàng hơn vì mọi thứ đều gọn gàng ở một nơi và dễ hiểu hơn.

Lưu ý rằng việc triển khai dưới dạng mono-repo không hề đồng nhất với kiến trúc nguyên khối (monolith)

Nói tóm lại thì monorepos không chỉ duy trì được hầu hết các ưu điểm khi triển khai dưới dạng microservices mà còn đơn giản hóa việc chia sẻ mã và tái cấu trúc dự án chéo, chúng giảm đáng kể chi phí tạo libs, microservices và microfrontends. Vì vậy, việc áp dụng monorepo thường cho phép triển khai linh hoạt hơn.

# Công cụ Nx

### Giới thiệu chung

Nx là một bộ công cụ dùng để tạo các monorepos. Theo như đội ngũ phát triển giới thiệu, Nx được học phát triển dựa trên những kinh nghiệm của họ trong quá trình làm việc ở các tập đoàn lớn như Google, Facebook và Microsoft. Bởi vậy họ kì vọng rằng Nx sẽ alf công cụ đắc lực hỗ trợ các lập trình viên tạo cũng như phát triển các hệ thống một cách dễ dàng với vô vàn các công nghệ frontend cũng như backend đang có hiện nay.

Do đặc thù phát triển cho ngôn ngữ Javascript nên hiện nay Nx đang hỗ trợ Angular, React và Node.js. Tuy nhiên có thể trong tương lai không xa Nx có thể hỗ trợ các framework khác như Vue hoặc Svelte, ...

### Sử dụng

Nx sử dụng khái niệm `workspace` để chỉ một ứng dụng toàn thể được triển khai monorepos. Bởi vậy khi bắt đầu sử dụng chúng ta tạo một workspace mới bằng `npx` như sau:
```bat
npx create-nx-workspace
```

Ngoài việc sử dụng npx chúng ta có thể dùng `npm init` bằng `npm init nx-workspace` hoặc `yarn create` với `yarn create nx-workspace`. Ngay sau khi chạy lệnh trên, Nx sẽ hỏi chúng ta một số thứ chẳng hạn như muốn tạo workspace theo mẫu sẵn có nào hay không, ... như sau:

```bat
Workspace name (e.g., org name)     demo
What to create in the new workspace react
Application name                    demo
Default stylesheet format           CSS
```

![workspace](https://boxxv.github.io/img/posts/b08a0b55-015a-496f-8cd0-39ca3bcf9b25.png "workspace")

##### Cài đặt Nx CLI với dòng lệnh sau:
```bat
npm install -g nx
```

##### Xem Nx có hỗ trợ sẵn các framework
```bat
npx nx list
```

##### Chạy ứng dụng ở local
```bat
npx nx serve <application-name>
```

##### Build the app
```bat
npx nx build <application-name>
```

##### Running multiple applications
```bat
npx nx run-many --target=serve --projects=<application-name>,<application-name> --parallel
npx nx run-many --target=serve --projects=api,html --parallel
```

##### Run a linter for the application
```bat
npx nx lint <application-name>
```

##### Run unit tests for the application
```bat
npx nx test <application-name>
```

##### Run e2e tests for the application
```bat
npx nx e2e <application-name>-e2e
```

##### Thể hiện một cách trực quan quan hệ giữa các module
```bat
npx nx dep-graph
```


# Building Docker images

[https://blog.nrwl.io/nx-and-node-microservices-b6df3cd1bad6](https://blog.nrwl.io/nx-and-node-microservices-b6df3cd1bad6)

Khi tạo Docker images cho các ứng dụng Node, chúng ta cần đảm bảo rằng có sẵn `package.json`. Chúng tôi cần package.json để cài đặt các phụ thuộc ứng dụng trong image.

`Nx` có các cơ chế để tự động tạo một package.json dựa trên các phụ thuộc mà ứng dụng đang sử dụng. Để kích hoạt điều này, chúng ta cần sửa đổi tệp `workspace.json` và kích hoạt tạo `package.json`.

Thêm thuộc tính `generatePackageJson` vào từng app targets xây dựng:

```json
@@ -15,7 +15,8 @@
             "outputPath": "dist/apps/api",
             "main": "apps/api/src/main.ts",
             "tsConfig": "apps/api/tsconfig.app.json",
-            "assets": ["apps/api/src/assets"]
+            "assets": ["apps/api/src/assets"],
+            "generatePackageJson": true
           },
           "configurations": {
             "production": {
@@ -67,7 +68,8 @@
             "outputPath": "dist/apps/html",
             "main": "apps/html/src/main.ts",
             "tsConfig": "apps/html/tsconfig.app.json",
-            "assets": ["apps/html/src/assets"]
+            "assets": ["apps/html/src/assets"],
+            "generatePackageJson": true
           },
           "configurations": {
             "production": {
```

Bây giờ chúng ta có thể chạy lệnh sau để xây dựng các ứng dụng:
```bat
nx run-many --target=build --projects=api,html --parallel
```

Bây giờ chúng ta sẽ có một vài thư mục trong thư mục `dist/`. Chúng tôi cũng có thể xem các tệp package.json đã tạo.

Nếu chúng ta so sánh hai tệp package.json, chúng ta có thể thấy rằng dự án `html` chứa nhiều phụ thuộc hơn. Điều này là do chúng tôi đang sử dụng chúng một cách rõ ràng trong ứng dụng `html`.

Tiếp theo, chúng ta sẽ tạo một vài `Dockerfiles`.

Tạo phần sau trong đường dẫn `apps/api/Dockerfile`:
```bat
FROM node:lts-alpine
WORKDIR /app
COPY ./dist/apps/api .
ENV PORT=3333
EXPOSE ${PORT}
RUN npm install --production
# dependencies that nestjs needs
RUN npm install reflect-metadata tslib rxjs @nestjs/platform-express
CMD node ./main.js
```

Và một trong các `apps/html/Dockerfile`:
```bat
FROM node:lts-alpine
WORKDIR /app
COPY ./dist/apps/html .
ENV PORT=3334
EXPOSE ${PORT}
RUN npm install --production
RUN npm install reflect-metadata tslib rxjs hbs
CMD node ./main.js
```

Có một lệnh `RUN npm install` bổ sung trong mỗi tệp Docker. Đây là những phần phụ thuộc mà NestJs cần nhưng không được sử dụng rõ ràng trong các ứng dụng của chúng tôi.

Chúng tôi có thể xác nhận rằng docker images xây dựng bằng cách chạy các lệnh sau trong thư mục gốc của không gian làm việc workspace:

```bat
docker build -f ./apps/api/Dockerfile . -t api
docker build -f ./apps/html/Dockerfile . -t html
```

## Deploy command

Việc phải nhớ tất cả các lệnh này có thể gây nhầm lẫn. Rất may, Nx có một cơ chế khác, nơi chúng ta có thể kết hợp nhiều lệnh với nhau. Điều này được cung cấp bởi `@nrwl/workspace:run-command` executor.

Hãy sửa đổi tệp `workspace.json` và thêm một target mới: deploy.

```json
@@ -8,6 +8,15 @@
       "prefix": "api",
       "schematics": {},
       "targets": {
+        "deploy": {
+          "builder": "@nrwl/workspace:run-commands",
+          "options": {
+            "commands": [
+              "nx build api",
+              "docker build -f ./apps/api/Dockerfile . -t api"
+            ]
+            "parallel": false
+          }
+        },
         "build": {
           "builder": "@nrwl/node:build",
           "outputs": ["{options.outputPath}"],
@@ -61,6 +70,15 @@
       "prefix": "html",
       "schematics": {},
       "targets": {
+        "deploy": {
+          "builder": "@nrwl/workspace:run-commands",
+          "options": {
+            "commands": [
+              "nx build html",
+              "docker build -f ./apps/html/Dockerfile . -t html"
+            ],
+            "parallel": false
+          }
+        },
         "build": {
           "builder": "@nrwl/node:build",
           "outputs": ["{options.outputPath}"],
```


-----
Tham khảo:
- [Monorepos là gì và tạo nhanh một Monorepos bằng Nx](https://viblo.asia/p/monorepos-la-gi-va-tao-nhanh-mot-monorepos-bang-nx-RnB5pWwblPG)
- [React Nx Tutorial](https://nx.dev/react-tutorial/01-create-application)
- [Scale React Development with Nx](https://egghead.io/courses/scale-react-development-with-nx-4038)
- []()
