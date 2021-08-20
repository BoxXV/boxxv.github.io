---
layout: post
title: Tạo thư viện JavaScript hiện đại
subtitle: Tạo gói npm sẵn sàng phân phối từ đầu
tags:
- Tips
- Tricks
- JavaScript
- library
---

### Npm là gì và tại sao nó lại quan trọng?

`Node Package Manager`, hoặc `npm` (thường được viết bằng chữ thường) là một trong những công cụ tạo và quản lý các thư viện được sử dụng phổ biến nhất trong các dự án JavaScript. Nó được xây dựng trên Node và rất mạnh mẽ nên hầu như tất cả mọi người đều đang sử dụng nó.

#### Công cụ quản lý thư viện là gì?

Hãy tưởng tượng rằng bạn bao gồm thư viện **A** để tùy chỉnh một trường văn bản. Thư viện đó sử dụng thư viện **B** để định dạng văn bản và thư viện **C** để hiển thị các bản dịch.

Hãy tưởng tượng rằng, cùng một lúc, thư viện **C** sử dụng năm thư viện khác nhau để xử lý các ngôn ngữ khác nhau và bạn kết thúc với một lược đồ như thế này.

![npm](https://boxxv.github.io/img/posts/dependency-tree.png "Node Package Manager")

Đó được gọi là _cây phụ thuộc_ của ứng dụng của bạn.

Không sớm thì muộn, dự án của bạn sẽ kết thúc với hàng tá phụ thuộc (bạn thậm chí sẽ không nhận thức được một số trong số chúng). Và điều tồi tệ hơn nữa, mỗi phụ thuộc đó sẽ chỉ tương thích với một số phiên bản cụ thể nhất định.

Tình huống này sẽ là một cơn ác mộng để quản lý thủ công. Một bản cập nhật đơn giản trong một mô-đun con có thể phá vỡ cây phụ thuộc của bạn và ứng dụng của bạn có thể không biên dịch. Đó chính xác là vấn đề mà `npm` giải quyết.

![npm](https://boxxv.github.io/img/posts/dependency-tree-wrong.png "Node Package Manager")

Khi bạn tạo một thư viện `npm`, bạn sẽ tạo một tệp json được gọi `package.json` trong đó bạn chỉ định những phụ thuộc nào mà thư viện JS của bạn có.

Đồng thời, các phụ thuộc trong thư viện của bạn sẽ có các `package.json` tệp riêng của chúng , tạo ra một cây phụ thuộc đầy đủ.

Nếu ai đó muốn thêm thư viện của bạn vào dự án của họ, thì họ sẽ chỉ cần chạy:

```bat
npm install <your-library-package-name>
```

Thật kỳ diệu, tất cả các phụ thuộc của cây sẽ được tải xuống và cài đặt. Hệ thống này thật tuyệt vời vì trong thực tế, bạn không cần quan tâm đến các phụ thuộc.

#### Có bất kỳ mặt trái nào của việc sử dụng trình quản lý gói không?

Nguyên nhân chính là các nhà phát triển mất quyền kiểm soát mã nào họ đang đưa vào các dự án của họ. Mối quan tâm về bảo mật đã xuất hiện trong quá khứ và các hệ thống quan trọng đòi hỏi một cây phụ thuộc được kiểm soát chặt chẽ và nghiêm ngặt.

Lấy ví dụ sau: một dự án mới được tạo trong React Native có hơn 1500 phụ thuộc. Không chắc có nhiều hơn một vài người biết tất cả. Nếu ai đó giới thiệu một số mã độc hại - hoặc chỉ là một lỗi - thì rất nhiều nhà phát triển có thể sẽ áp dụng mã này mà không hề hay biết.

Đừng lo lắng. Đây là một điều rất hiếm khi xảy ra. Tuy nhiên [nó đã xảy ra](https://www.zdnet.com/article/microsoft-spots-malicious-npm-package-stealing-data-from-unix-systems/) một vài lần.

Một ví dụ khác là [tranh chấp vào năm 2019 giữa một nhà phát triển mã nguồn mở và một công ty Mỹ](https://arstechnica.com/information-technology/2016/03/rage-quit-coder-unpublished-17-lines-of-javascript-and-broke-the-internet/) đã gần như phá vỡ mạng internet của thế giới. Một câu chuyện ngắn, nhà phát triển quyết định xóa một thư viện khá tầm thường nhưng vẫn thường được sử dụng khỏi npm và đột nhiên cây phụ thuộc của hàng nghìn dự án trên khắp thế giới bị phá vỡ.


### Tại sao bạn nên tạo thư viện gói npm của riêng mình?

Cách nhanh nhất và an toàn nhất để viết mã là _không_ viết nó. Nếu bạn thường cần sao chép-dán một số tính năng giữa các dự án khác nhau, bạn có thể muốn tạo một thư viện JavaScript mới và viết các tính năng đó chỉ một lần.

Sau đó, vào lần tiếp theo bạn cần sử dụng các tính năng đó, bạn không cần sao chép-dán hoặc viết lại chúng - bạn chỉ cần sử dụng lại thư viện của mình. Hơn nữa, nếu bạn tìm thấy một lỗi, bạn có thể giải quyết nó một lần và phân phối bản sửa lỗi cho các dự án còn lại của bạn.

Khi bạn đã viết mô-đun nút của mình, một trong những cách dễ nhất và nhanh nhất để đưa chúng vào các dự án của bạn là sử dụng npm.

Đó chính xác là những gì chúng tôi nghĩ khi giới thiệu trình ghi nhật ký từ xa [BugfenderJS](https://bugfender.com/platforms/javascript/). SDK của chúng tôi có thể được đưa vào theo cách thủ công, nhưng hầu hết người dùng của chúng tôi chỉ cần cài đặt nó bằng npm:

```bat
npm install @bugfender/sdk
```


### Tạo gói npm của riêng bạn

#### 1. Tạo một kho lưu trữ Git mới

Nếu bạn đã tạo một số mã, bạn có thể bỏ qua phần này. Tuy nhiên, nếu bạn đang bắt đầu lại từ đầu, đã đến lúc phải thực hiện. Sau đó, bạn có thể truy cập GitHub và tạo một git repo mới.

#### 2. Tạo tệp package của bạn

Bây giờ, hãy mở terminal và điều hướng đến dự án của bạn

```bat
cd folder/to/your project
```

Và gõ

```bat
npm init
```

Công cụ này sẽ giúp bạn tạo mới `package.json` yêu cầu bạn cung cấp dữ liệu cơ bản cần thiết. Một số mẹo nhanh:

- Package name: hãy nhớ sử dụng kebab-case vì đây là quy ước trong cộng đồng npm.
- Version: bạn sẽ được khuyên nên bắt đầu dự án của mình trong phiên bản 1.0.0, tuy nhiên nếu bạn chỉ mới bắt đầu dự án của mình, bạn có thể nên bắt đầu với một cái gì đó giống như 0.0.1 và chuyển sang 1.0.0 khi mã đã được kiểm tra thêm. Ngoài ra, các nhà phát triển khác sử dụng thư viện của bạn sẽ đánh giá cao việc lập phiên bản của bạn phản ánh trạng thái mã của bạn.
- Description: đi thẳng vào vấn đề và dễ hiểu.
- Entry point: đây là tệp nhập cho thư viện của bạn. Đây là tệp mà các nhà phát triển khác sử dụng thư viện của bạn sẽ phải viết khi đưa nó vào cùng `reguire('your-package')`. Nếu bạn chỉ sử dụng một tệp, `index.js` là đủ. Tuy nhiên, nếu dự án của bạn sắp có nhiều tệp hơn, tốt hơn hết là bạn nên sử dụng `src/index.js`.

Nếu bạn không muốn điền phần còn lại của các trường ngay bây giờ, bạn có thể bỏ qua chúng và quay lại sau để thêm chúng vào tệp package.json .

![npm](https://boxxv.github.io/img/posts/npm-package-creation-console-1.png "Node Package Manager")

#### 3. Thêm mã vào dự án JavaScript của bạn và thiết lập API công khai

Thông thường, bạn có một số mã mà bạn đã sao chép-dán giữa các dự án khác nhau và bạn đang chuyển nó sang mô-đun npm để sử dụng lại trong tương lai.

Nếu đúng như vậy, bây giờ đã đến lúc thêm mã này vào dự án npm. Tiếp theo, bạn sẽ cần nghĩ về API mà bạn sẽ tiếp xúc với thế giới.

Xác định `API` công khai của bạn với `module.exports`

Cách mà bạn cho npm biết thư viện của bạn đang hiển thị những gì bằng cách sử dụng `module.exports`, một đối tượng phải có mặt trong điểm nhập của thư viện của bạn (thường là `index.js` ).

Bạn có thể chỉ định bất cứ điều gì bạn muốn trong `module.exports`. Nó có thể là một số, một hàm, một lớp… Hãy tưởng tượng bạn đang xây dựng mô-đun từ _bugfender-coffee-machine_ mẫu trước đó . Khi người dùng nhập:

{% highlight js %}
const coffeMachine = require('bugfender-coffee-machine');
{% endhighlight %}

Sau đó, mã của bạn sẽ chuyển đến index.js và sẽ xác định giá trị của mô-đun. Ví dụ: nếu bên trong index.js của bạn, bạn đặt:

{% highlight js %}
module.exports = 42;
{% endhighlight %}

Khi đó _coffeMachine_ sẽ là một số có giá trị 42.

Một cách tiếp cận thực tế hơn sẽ là đặt giá trị này thành một thể hiện của một lớp:

{% highlight js %}
// index.js
module.exports = BugfenderCoffeeMachine; 

// In your app
const CoffeeMachine = require('bugfender-coffee-machine');
const coffeeMachine = new CoffeeMachine();
{% endhighlight %}

`coffeeMachine` hiện là một phiên bản của `BugfenderCoffeeMachine` và bây giờ bạn có thể làm:

{% highlight js %}
coffeeMachine.prepareCoffee()
{% endhighlight %}

Thêm tệp README.md






-----
Tham khảo:
- [How to Create an npm Package Ready to Distribute From Scratch](https://bugfender.com/blog/how-to-create-an-npm-package/)