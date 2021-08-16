---
layout: post
title: Tạo một thư viện JavaScript hiện đại
subtitle: Creating a modern JS library
tags:
- Tips
- Tricks
- JavaScript
- library
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

Tham khảo thêm : https://dev.to/medaymentn/securing-your-node-js-api-with-json-web-token-5o5 

Source code: https://github.com/medaymenTN/JWTNodeJS

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
 - ✔ Tại sao phải là hai token mà không phải là một token?
 - ✔ Xác thực Access Token và Refresh Token khác biệt gì?
 - ✔ Vậy có thể nói Refresh Token tồn tại mãi mãi không?
Như vậy những bài viết về JSON Web Token chúng tôi đã nhận được rất nhiều phản hồi qua Email về việc sử dụng Token như thế nào? Và tại sao chúng ta lại phải sử dụng Refresh Token khi mà có token rồi? Và đây chính là bài viết sẽ làm sáng tỏ những thắc mắc của bạn.

Ở bài trước tôi đã hướng dẫn các bạn cách xác thực REST API với JWT(JSON Web Token) thông qua một Access Token, và hôm nay chúng ta tiếp tục tìm hiểu về Refresh Token. Tại sao lại có thêm Refresh Token? Và Refresh Token dùng để làm gì? 

-----
### 3. Bảo mật RESTful API với JWT và Cookie httpOnly, Secure.
Ở bài viết trước, chúng ta đã làm rõ về cách lưu trữ token ở đâu trên Client. Và cách nào an toàn hơn và hạn chế được các XSS attack. Do đó ở bài này chúng ta sẽ triển khai xây dựng một RESTful APIs bảo mật token hạn chế việc đánh cắp khi mà càng ngày hackers luôn luôn rình mò ở quanh ta :D. 

Để đọc và hiểu bài này thì những bạn chứ đọc bài trước "JSON Web Token: Lưu trữ và bảo mật tokens trên client như thế nào?" thì nên lướt qua để hiểu vì sao lại có bài viết này. Bắt đầu tạo cho mình một rest api thôi nào. Code full tôi sẽ post sau bài viết. Nhưng các bạn nên theo dõi từng bước trước để hiểu cách run một api thế nào rồi lúc đó download source về cũng chưa muộn nhé. 
Code Full:

Phía Back-End: https://github.com/anonystick/demo-jwt-token 

Phía Client: https://github.com/anonystick/demo-jwt-token-client



-----
Tham khảo:
- [JSON Web Token: Vấn đề xác thực REST API với JWT](https://anonystick.com/blog-developer/json-web-token-van-de-xac-thuc-rest-api-voi-jwtjson-web-token-201906074991365.jsx)
- [JSON Web Token: Lưu trữ và bảo mật tokens trên client như thế nào?](https://anonystick.com/blog-developer/json-web-token-luu-tru-va-bao-mat-tokens-tren-client-nhu-the-nao-2019062144827814.jsx)
- [Authorization Framework: Access Token, Refresh Token cũng giống việc sinh viên thuê nhà trọ](https://anonystick.com/blog-developer/authorization-framework-access-token-refresh-token-cung-giong-viec-sinh-vien-thue-nha-tro-2019061161976500.jsx)
- [JSON Web Token: Bảo mật RESTful API với JWT và Cookie httpOnly, Secure.](https://anonystick.com/blog-developer/json-web-token-bao-mat-restful-api-voi-jwt-va-cookie-httponly-secure-201906223285306.jsx)

https://stormpath.com/blog/where-to-store-your-jwts-cookies-vs-html5-web-storage

https://stackoverflow.com/questions/42286781/jwt-token-with-ajax-non-ajax-jquery
{% highlight js %}
$.ajax({
    type: "POST", //GET, POST, PUT
    url: '/authenticatedService'  //the url to call
    data: yourData,     //Data sent to server
    contentType: contentType,           
    beforeSend: function (xhr) {   //Include the bearer token in header
        xhr.setRequestHeader("Authorization", 'Bearer '+ jwt);
    }
}).done(function (response) {
    //Response ok. process reuslt
}).fail(function (err)  {
    //Error during request
});
{% endhighlight %}