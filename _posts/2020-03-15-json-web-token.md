---
layout: post
title: Series JSON Web Token
subtitle: Thực tiễn hiện đại, Hướng dẫn đầy đủ
tags:
- JSON Web Token
- JWT
- Tips
- Tricks
- Session Storage
- Session Cookie Storage
---

https://anonystick.com/search?category=home&key=JSON+Web+Token


### 1. Vấn đề xác thực REST API với JWT(JSON Web Token)
Nội dung bài viết:
 - Restful api là gì?
 - JWT là gì?
 - Tại sao lại xác thực REST API (Nodejs) với JWT(JSON Web Token)?
 - ✔ Quy trình việc xác thực JWT và restful nodejs.
 - ✔ Build một resful api với JWT(JSON Web Token)
JWT là gì? JSON Web Token.  Ở phần trước chúng ta đang nói đến việc xác thực Token trong firebase. Nhưng nhiều bạn quay sang hỏi về việc xác thực JWT (JSON Web Token). Chắc do các bạn sử dụng JWT nhiều hơn, cho nên hôm nay, trong bài viết này tôi sẽ viết một module nhỏ để giúp các bạn nào chưa hiểu thì có thể hiểu thêm. 

-----
### 2. Lưu trữ và bảo mật tokens trên client như thế nào?
Lưu trữ và bảo mật tokens. Sau những bài viết về JSON Web Token(JWT) đa số các bạn cũng đã hiểu và đã apply cho các ứng dụng của mình. Các luồng đi của việc create và verify một tokens xem như đã xong, nhưng có có một vấn đề quan trọng mà các bạn bỏ qua. Đó là việc khi client nhận được tokens thì việc storage ở đâu và việc bảo mật nó như thế nào để tránh bị đánh cắp. Vậy thì trong bài viết này tôi sẽ trình bày cho các bạn hiểu rõ hơn về vấn đề này. Tất nhiên có nhiều cách khác, nhưng bài viết này giúp bạn có thể hiểu sâu hơn và có thể bạn tìm thấy phương pháp này ở đây. 

-----
### 3. Authorization Framework: Access Token, Refresh Token cũng giống việc sinh viên thuê nhà trọ
Nội dung bài viết:
 - Oauth2 và jwt
 - Access token và refresh token là gì?
 - Access Token là gì?
 - Refresh Token là gì?
 - Create refresh token
 - # Tại sao phải là hai token mà không phải là một token?
 - # Xác thực Access Token và Refresh Token khác biệt gì?
 - # Vậy có thể nói Refresh Token tồn tại mãi mãi không?


-----
Tham khảo:
- [JSON Web Token: Vấn đề xác thực REST API với JWT](https://anonystick.com/blog-developer/json-web-token-van-de-xac-thuc-rest-api-voi-jwtjson-web-token-201906074991365.jsx)
- [JSON Web Token: Lưu trữ và bảo mật tokens trên client như thế nào?](https://anonystick.com/blog-developer/json-web-token-luu-tru-va-bao-mat-tokens-tren-client-nhu-the-nao-2019062144827814.jsx)
- [Invoke, InvokeRequired trong C# có nghĩa là gì?](https://anonystick.com/blog-developer/authorization-framework-access-token-refresh-token-cung-giong-viec-sinh-vien-thue-nha-tro-2019061161976500.jsx)
