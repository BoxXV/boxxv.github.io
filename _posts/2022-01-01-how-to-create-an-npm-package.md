---
layout: post
title: Tạo gói npm sẵn sàng phân phối từ đầu
subtitle: Tạo thư viện JavaScript hiện đại
tags:
- module
- npm
- JavaScript
- library
---

## Npm là gì và tại sao nó lại quan trọng?

`Node Package Manager`, hoặc `npm` (thường được viết bằng chữ thường) là một trong những công cụ tạo và quản lý các thư viện được sử dụng phổ biến nhất trong các dự án JavaScript. Nó được xây dựng trên Node và rất mạnh mẽ nên hầu như tất cả mọi người đều đang sử dụng nó.

### Công cụ quản lý thư viện là gì?

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

### Có bất kỳ mặt trái nào của việc sử dụng trình quản lý gói không?

Nguyên nhân chính là các nhà phát triển mất quyền kiểm soát mã nào họ đang đưa vào các dự án của họ. Mối quan tâm về bảo mật đã xuất hiện trong quá khứ và các hệ thống quan trọng đòi hỏi một cây phụ thuộc được kiểm soát chặt chẽ và nghiêm ngặt.

Lấy ví dụ sau: một dự án mới được tạo trong React Native có hơn 1500 phụ thuộc. Không chắc có nhiều hơn một vài người biết tất cả. Nếu ai đó giới thiệu một số mã độc hại - hoặc chỉ là một lỗi - thì rất nhiều nhà phát triển có thể sẽ áp dụng mã này mà không hề hay biết.

Đừng lo lắng. Đây là một điều rất hiếm khi xảy ra. Tuy nhiên [nó đã xảy ra](https://www.zdnet.com/article/microsoft-spots-malicious-npm-package-stealing-data-from-unix-systems/) một vài lần.

Một ví dụ khác là [tranh chấp vào năm 2019 giữa một nhà phát triển mã nguồn mở và một công ty Mỹ](https://arstechnica.com/information-technology/2016/03/rage-quit-coder-unpublished-17-lines-of-javascript-and-broke-the-internet/) đã gần như phá vỡ mạng internet của thế giới. Một câu chuyện ngắn, nhà phát triển quyết định xóa một thư viện khá tầm thường nhưng vẫn thường được sử dụng khỏi npm và đột nhiên cây phụ thuộc của hàng nghìn dự án trên khắp thế giới bị phá vỡ.


## Tại sao bạn nên tạo thư viện gói npm của riêng mình?

Cách nhanh nhất và an toàn nhất để viết mã là _không_ viết nó. Nếu bạn thường cần sao chép-dán một số tính năng giữa các dự án khác nhau, bạn có thể muốn tạo một thư viện JavaScript mới và viết các tính năng đó chỉ một lần.

Sau đó, vào lần tiếp theo bạn cần sử dụng các tính năng đó, bạn không cần sao chép-dán hoặc viết lại chúng - bạn chỉ cần sử dụng lại thư viện của mình. Hơn nữa, nếu bạn tìm thấy một lỗi, bạn có thể giải quyết nó một lần và phân phối bản sửa lỗi cho các dự án còn lại của bạn.

Khi bạn đã viết mô-đun node của mình, một trong những cách dễ nhất và nhanh nhất để đưa chúng vào các dự án của bạn là sử dụng npm.

Đó chính xác là những gì chúng tôi nghĩ khi giới thiệu trình ghi nhật ký từ xa [BugfenderJS](https://bugfender.com/platforms/javascript/). SDK của chúng tôi có thể được đưa vào theo cách thủ công, nhưng hầu hết người dùng của chúng tôi chỉ cần cài đặt nó bằng npm:

```bat
npm install @bugfender/sdk
```


## Tạo gói npm của riêng bạn

### 1. Tạo một kho lưu trữ Git mới

Nếu bạn đã tạo một số mã, bạn có thể bỏ qua phần này. Tuy nhiên, nếu bạn đang bắt đầu lại từ đầu, đã đến lúc phải thực hiện. Sau đó, bạn có thể truy cập GitHub và tạo một git repo mới.

### 2. Tạo tệp package của bạn

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

### 3. Thêm mã vào dự án JavaScript của bạn và thiết lập API công khai

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

#### Thêm tệp README.md

Bước đơn giản nhất và nhỏ nhất cũng là một trong những bước quan trọng nhất. Có một tệp `Readme` tốt đảm bảo rằng những người khác sẽ có thể hiểu được nội dung của thư viện của bạn - và cách sử dụng nó.

Bạn không cần phải quá sáng tạo về nó, chỉ cần sử dụng một mẫu như [thế này](https://www.makeareadme.com) và cố gắng điền vào tất cả các trường một cách rõ ràng.

Người dùng thư viện npm của bạn sẽ đánh giá cao việc bạn đã tiết kiệm thời gian cho họ. Ngay cả một phiên bản trong tương lai của bạn cũng sẽ rất vui khi có tài liệu rõ ràng!

#### Commit

Bây giờ thư viện của bạn đã sẵn sàng và bạn có thể tiếp tục với commit đầu tiên của mình.

Tương tự như tệp Readme, đã có rất nhiều tài liệu về [cách viết các commit git có ý nghĩa](https://chris.beams.io/posts/git-commit/).


### 4. Xuất bản trên npm

Đăng ký đến npm

Nếu bạn chưa có tài khoản npm, đã đến lúc [đăng ký](https://www.npmjs.com/signup).

npm là một công cụ dòng lệnh. Mở bảng điều khiển và viết:

{% highlight js %}
npm login # you will be prompted your mail and password
{% endhighlight %}

Bạn có thể kiểm tra xem bạn đã đăng nhập chính xác với

{% highlight js %}
npm whoami
{% endhighlight %}

Mẹo: trước khi xuất bản gói npm mới, hãy đảm bảo rằng bạn đã đăng nhập với người dùng thích hợp. Điều này đặc biệt quan trọng nếu bạn sử dụng cùng một máy cho công việc và các dự án phụ.

#### Kiểm tra Framework của bạn

Chúng tôi gần như đã sẵn sàng để xuất bản. Nhưng ngay trước khi thực hiện, chúng tôi có thể chạy thử nghiệm cục bộ nhanh.

Đầu tiên, điều hướng đến đường dẫn tệp thư viện của bạn, cùng đường dẫn mà bạn đã đặt `package.json` và sử dụng lệnh `npm link`.

{% highlight js %}
cd ./route-to-your-library/
npm link # This adds the project to your local npm registry
{% endhighlight %}

Bây giờ, hãy tạo một dự án JavaScript mới trong hệ thống của bạn và sử dụng lại `npm link`, nhưng chỉ định tên của gói - giống như tên mà bạn đã chỉ định trong bước `npm init`.

{% highlight js %}
cd ./route-to-a-new-javascript-project/
npm link [name-of-the-package] # This installs the library in the project
{% endhighlight %}

Bạn có thể sử dụng quy trình này trong tương lai khi định cập nhật thư viện của mình để không cần xuất bản mỗi khi muốn thử nghiệm các thay đổi mới.

#### Công bố

Bây giờ bạn đã tạo thư viện và bạn đã thử nghiệm nó cục bộ, đã đến lúc chia sẻ nó với mọi người.

{% highlight js %}
cd ./route-to-your-library/
npm publish
{% endhighlight %}

npm sẽ bắt đầu làm việc để xuất bản thư viện của bạn lên kho lưu trữ chính thức.

Khi nó hoàn tất, thư viện sẽ có sẵn trong https://www.npmjs.com và mọi người dùng trên thế giới đều có thể cài đặt nó bằng cách sử dụng `npm install <package-name>`.


### 5. Cập nhật thư viện của bạn

Chúng ta sẽ đến phần cuối của bài viết, nhưng nó mới chỉ là phần mở đầu của thư viện của bạn.

Nếu bạn bắt đầu sử dụng nó và những người dùng khác chấp nhận nó, bạn cũng sẽ cần phải duy trì nó. Đôi khi, bạn sẽ phải giới thiệu các tính năng mới hoặc cập nhật mã không dùng nữa. Bất cứ khi nào bạn làm điều đó, hãy nhớ sử dụng [Phiên bản ngữ nghĩa](https://semver.org) (major.minor.patch).

npm giúp giảm bớt quá trình duy trì mã của bạn bằng các công cụ lập phiên bản npm:

{% highlight js %}
npm version patch # From 0.0.1 to 0.0.2
npm version minor # From 0.1.0 to 0.2.0
npm version major # From 1.0.0 to 2.0.0
{% endhighlight %}

Hãy lưu ý rằng `npm version` cập nhật `package.json`, tạo commit và thêm TAG vào git.


## Một điều cuối cùng

Tại Bugfender, chúng tôi là nhà phát triển phần mềm và chúng tôi biết những hướng dẫn này có giá trị như thế nào. Nếu bạn thấy bài đăng này hữu ích, bạn có thể giúp chúng tôi đổi lại bằng cách chia sẻ nó với đồng nghiệp của bạn.

Bugfender là trình ghi nhật ký bảng điều khiển từ xa được tạo cho các nhà phát triển, bởi các nhà phát triển. SDK Javascript mới giúp bạn tìm ra lỗi nhanh hơn và cung cấp hỗ trợ khách hàng tốt hơn cho khách hàng của bạn.

Bạn có thể [đăng ký miễn phí](https://dashboard.bugfender.com/signup) trong vòng chưa đầy 20 giây và thêm SDK vào trang web của mình trong 10 giây nữa bằng cách sử dụng `npm install @bugfender/sdk` (không tệ trong nửa phút ;-).

Chúng tôi xuất bản các hướng dẫn và các câu chuyện gỡ lỗi thường xuyên trên blog của chúng tôi. Đừng quên ghé thăm chúng tôi theo thời gian hoặc tốt hơn nữa là đăng ký nhận bản tin không spam hàng quý của chúng tôi để có được cái nhìn tổng quan về các bài viết mới.


-----
Tham khảo:
- [How to Create an npm Package Ready to Distribute From Scratch](https://bugfender.com/blog/how-to-create-an-npm-package/)