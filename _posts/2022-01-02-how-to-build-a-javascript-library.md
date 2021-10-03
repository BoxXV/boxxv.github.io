---
layout: post
title: Cách tạo Thư viện JavaScript
title: Cách xây dựng Thư viện JavaScript
subtitle: Viết thư viện Lightbox hình ảnh không có phụ thuộc đơn giản
image: "img/js.jpg"
tags:
- module
- npm
- JavaScript
- library
---

Nếu bạn là nhà phát triển, gần như chắc chắn rằng bạn đã sử dụng Thư viện. Nói một cách dễ hiểu, Thư viện là một tập hợp các mã có thể sử dụng lại mà bạn có thể sử dụng trong chương trình của mình.

Giống như hầu hết chúng ta, tôi biết cách cắm các thư viện vào chương trình của mình và sử dụng chúng, nhưng tôi thường thấy sợ mỗi khi xem qua mã nguồn thực của thư viện cụ thể đó. Sau đó, tôi bắt đầu học Vanilla JS và tất cả đều không còn đáng sợ nữa. Vanilla JS là mã JavaScript đơn giản mà bạn viết mà không cần sử dụng bất kỳ thư viện bên ngoài nào.

Khi nói đến việc xây dựng một thư viện JavaScript mà bạn sẽ sử dụng để tạo một trang web, điều quan trọng là bạn phải học thao tác DOM bằng cách sử dụng Vanilla JS trước khi cố gắng thực sự xây dựng nó. Lý do quan trọng là bạn sẽ không có bất kỳ phụ thuộc nào và thư viện của bạn sẽ chỉ là một plug-n-play cho người dùng của bạn. Bạn có thể quen với thao tác DOM bằng jQuery nhưng điều đó sẽ tạo ra sự phụ thuộc vào jQuery và thư viện của bạn sẽ không hoạt động trên trang web không bao gồm tham chiếu đến thư viện jQuery.

Nếu bạn đã quen với jQuery và muốn tìm hiểu thêm về thao tác DOM bằng Vanilla JS, bạn có thể đọc thêm về nó [tại đây](https://faisalrashid.tech/blogs/JavaScript-vs-jQuery).

Với tất cả những gì đã nói, hãy đi sâu vào việc tạo Thư viện JavaScript từ đầu.

Chúng tôi sẽ xây dựng `Image Lightbox`. Lightbox là một thư viện được sử dụng để xem hình ảnh trên trang web bằng cách lấp đầy trang bằng hình ảnh và giảm làm nổi nền. Đây là những gì chúng tôi sẽ xây dựng.

![Image Lightbox](https://boxxv.github.io/img/posts/fs-ligthbox.gif "Image Lightbox")

Nếu bạn muốn tiếp tục và xem mã, bạn có thể tìm thấy kho lưu trữ GitHub [tại đây](https://github.com/FaisalST32/fs-lightbox).

Khi xây dựng Thư viện JavaScript, có một số điều bạn muốn lưu ý.

Mã của bạn không được can thiệp vào mã hiện có do người dùng viết.
Để làm điều này, chúng tôi sẽ đóng gói tất cả mã của chúng tôi trong một đối tượng Hàm duy nhất.

{% highlight js %}
function FsLightbox() {
	// all the code goes here 
}
{% endhighlight %}

Tất cả mã mà chúng tôi viết trong hướng dẫn này sẽ được viết trong phần thân hàm đó. Điều này sẽ xử lý việc đóng gói.

Bây giờ chúng ta phải tạo một danh sách tất cả các phương thức mà người dùng sẽ được cấp quyền truy cập và điều đó sẽ hữu ích cho người dùng. Trong thư viện này, chúng tôi sẽ có bốn phương pháp như vậy

`.render()`, `.next()`, `.prev()` và `.hideLightbox()`

Do đó, đối tượng `FsLightbox` sẽ có bốn thành viên công khai này. Đối với các thành viên công khai, chúng tôi có nghĩa là tất cả các phương thức và thuộc tính được đặt trước từ khóa `this`.

{% highlight js %}
function FsLightbox() {
	let _this = this;
	// all the code goes here 
}
{% endhighlight %}

Điều này sẽ loại bỏ tất cả sự nhầm lẫn và cho phép chúng tôi sử dụng đối tượng context mà không có bất kỳ lo lắng nào.

Không còn cách nào khác, hãy xem qua chiến lược mà chúng tôi sẽ sử dụng để làm cho lightbox hoạt động.
- Người dùng sẽ chỉ định các hình ảnh sẽ sử dụng lightbox bằng cách thêm một lớp cụ thể vào các thẻ <img> đó. Vì vậy, mỗi khi DOM tải, chúng tôi sẽ có thể chụp những hình ảnh đó và lưu các tham chiếu của chúng trong một mảng.
- Sau đó, chúng tôi sẽ thêm trình nghe nhấp chuột vào mỗi hình ảnh để đảm bảo rằng mỗi khi người dùng nhấp vào hình ảnh đó, hình ảnh đó sẽ được hiển thị trong lightbox. Chúng tôi sẽ tận dụng cả JavaScript cũng như CSS để đạt được điều này.
- Chúng tôi cũng sẽ cần các điều khiển điều hướng cho `Hình trước`, `Hình tiếp theo` và một nút để `Đóng` lightbox. Chúng tôi sẽ kết nối các điều khiển này với trình nghe nhấp chuột tương ứng của chúng.
- Chúng tôi cũng sẽ hiển thị một số thông tin meta như `Bộ đếm hình ảnh` và `Chú thích` (chúng tôi sẽ lấy thông tin này từ văn bản thay thế `Alt`)

Như bạn có thể đã nhận ra rằng thư viện JavaScript mà chúng tôi sẽ tạo sẽ sử dụng rất nhiều CSS và do đó, chúng tôi cũng sẽ đưa vào một tệp CSS.

Nói đủ rồi, chúng ta hãy viết một số mã. Đầu tiên, chúng ta cần theo dõi một số dữ liệu và do đó, chúng ta sẽ khai báo một số biến sẽ có sẵn trong Hàm nhỏ của chúng ta. Đây sẽ là những điều sau đây:

{% highlight js %}
let imagesArray = [];    // Array containing the reference of all the images that have the specified class (fs-lightbox)
let currentImage;        // Image being displayed currently in the lightbox
let isLightbox = false;  // Boolean to tell you whether the image is being displayed in the lightbox or not
{% endhighlight %}

Sau đó, chúng tôi sẽ viết phương thức công khai đầu tiên của chúng tôi, `.render()`. Ở đây, chúng tôi sẽ khởi tạo các biến "toàn cục" và nhận tham chiếu của tất cả các hình ảnh được lưu trữ trong mảng. Phương thức này sẽ cần được chạy để thực sự khởi tạo lightbox của chúng ta. Đây là mã:

{% highlight js %}
this.render = () => {
	imagesArray = [];
	currentImage = null;
	isLightbox = false;

	document.querySelectorAll('img.fs-lightbox').forEach((img_el, index) => {
		imagesArray.push(img_el);
		img_el.setAttribute("data-lightbox-index", index);
		img_el.addEventListener('click', () => {
			_this.lightbox(img_el);
		});
	});

	addKeyListeners();
}
{% endhighlight %}

Như đã thấy, chúng tôi đang sử dụng một hàm `addKeyListaries()` ở đây. Phương pháp này được sử dụng để kết nối tất cả các thao tác bàn phím cho lightbox `Tiếp theo`, `Trước đó` và `Đóng`. Chúng tôi sẽ làm cho nó sau. Trình xử lý sự kiện mà chúng tôi đang thêm ở đây là `_this.lightbox()`. Phương thức này sẽ thực sự chịu trách nhiệm hiển thị hình ảnh trong hộp đèn. Đây là cách thực hiện.

{% highlight js %}
this.lightbox = _el => {
	this.hideLightbox();
	this.currentImage = _el;
	this.isLightbox = true;

	var overlay = document.createElement('div');
	overlay.classList.add('lightbox-overlay');
	var imageContainer = document.createElement('div');
	imageContainer.classList.add('lightbox-image');

	var image = document.createElement('img');
	image.src = _el.src;

	imageContainer.appendChild(image);

	document.querySelector('body').appendChild(overlay);
	document.querySelector('body').appendChild(imageContainer);

	prepareControls(_el);
}
{% endhighlight %}

Như rõ ràng trong phương thức `render()`, phương thức này mong đợi phần tử image `_el` như một tham số phương thức. Đây sẽ là một tham chiếu đến phần tử `img` cần được hiển thị trong hộp đèn. Nếu chúng ta phân tích thêm phương pháp này, chúng ta thấy rằng đầu tiên chúng ta `hideLightbox()` nếu nó đã hiển thị một số hình ảnh khác. Sau đó, chúng tôi lưu tham chiếu của hình ảnh trong biến toàn cục `currentImage` của chúng tôi và cũng thay đổi biến `isLightbox` thành true. Sau đó, thao tác DOM thực sự bắt đầu.

Chúng tôi tạo lớp phủ div `overlay` bằng cách sử dụng phương thức `createElement` và thêm lớp `lightbox-image` vào đó. Tệp CSS mà chúng tôi tạo sẽ chứa tất cả CSS cần thiết cho lớp phủ như vị trí và màu nền. Tôi sẽ không đi sâu vào mã đó vì đó không phải là điểm của bài đăng này. Điều đó đang được nói, đây là một đoạn trích chi tiết giống nhau:

{% highlight css %}
.lightbox-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100vw;
	height: 100vh;
	background-color: rgba(0,0,0,0.7);
	z-index: 10000;
}
{% endhighlight %}

Sau khi tạo lớp phủ, chúng ta cần tạo vùng chứa cho hình ảnh thực tế. Biến `imageContainer` sẽ chứa như vậy. Biến sẽ là một tham chiếu đến một div mà chúng ta tạo và sau đó chúng ta sẽ tạo một hình ảnh phần tử `img` và nối nó vào cùng một div. Với tham số hàm `_el` được cung cấp, chúng ta sẽ có src của hình ảnh được nhấp và sẽ đặt phần tử `src` của hình ảnh thành cùng một giá trị. Sau đó, chúng tôi nối các phần tử, `overlay` và `imageContainer` mới được tạo này vào DOM. Đó là nó! Giờ đây, mỗi khi người dùng nhấp vào hình ảnh có thêm lớp `fs-lightbox`, nó sẽ kích hoạtphương thức `lightbox()` và hình ảnh sẽ được hiển thị trong hộp đèn.

Đó là hầu hết những công việc khó khăn được thực hiện. Bây giờ đến việc đánh bóng. Đó chỉ là chúng tôi làm cho thư viện của chúng tôi thân thiện hơn với người dùng. Điều này rất quan trọng khi tạo một thư viện. Luôn suy nghĩ từ góc độ của người dùng. Nó càng thuận tiện cho người dùng, nó sẽ được nhận tốt hơn.

Vì vậy, chúng ta hãy bắt đầu nó sau đó. Hãy nhớ rằng, trước đó trong bài đăng, tôi đã đề cập đến tất cả bốn phương pháp công khai sẽ có sẵn cho người dùng. Chúng tôi vừa thực hiện một trong bốn phương thức đó `render()`. Chúng ta cần triển khai phần còn lại `next()`, `prev()` và `hideLightbox()`.

Điều này sẽ được thực hiện trong phương thức `readyControls()`. Bạn có thể thấy trong  phương thức `lightbox()` mà chúng tôi đang gọi phương thức này. Phương pháp này sẽ xử lý cả việc hiển thị Phần tử giao diện người dùng, tức là các nút cho các hành động trên cũng như gắn trình nghe nhấp chuột vào chúng. Đây là cách thực hiện.

{% highlight js %}
function prepareControls(imgElement) {
	let controls = document.createElement('div');
	controls.innerHTML += controlsHtml;

	document.querySelector('body').appendChild(controls.querySelector('.lightbox-controls'));

	let imgIndex = getCurrentImageIndex();
	if (imgIndex > 0) {
		document.querySelector(".lb-prev").addEventListener('click', () => {
			_this.prev();
		})
	} else {
		document.querySelector(".lb-prev").classList.add(['lb-disabled'])
	}

	if (imgIndex < _this.imagesArray.length - 1)
		 document.querySelector(".lb-next").addEventListener('click', () => {
			_this.next();
		})
	} else {
		document.querySelector(".lb-next").classList.add(['lb-disabled'])
	}

	document.querySelector('.lb-close').addEventListener('click', () => {
		_this.hideLightbox();
	})

	showCounter();
}
{% endhighlight %}

Như tôi đã nói, việc tạo điều khiển và kết nối chúng với trình nghe nhấp chuột là tất cả những gì đang được thực hiện ở đây. Các trình xử lý `this.next()` và `this.prev()` được triển khai như sau:

{% highlight js %}
this.next = () => {
	let imgIndex = getCurrentImageIndex();
	if (imgIndex === _this.imagesArray.length - 1)
		return;
	_this.lightbox(_this.imagesArray[getCurrentImageIndex() + 1]);
}

this.prev = () => {
	let imgIndex = getCurrentImageIndex();
	if (imgIndex === 0)
		return;
	_this.lightbox(_this.imagesArray[getCurrentImageIndex() - 1]);
}

this.hideLightbox = () => {
	let overlay = document.querySelector('.lightbox-overlay');
	let image = document.querySelector('.lightbox-image');
	let controls = document.querySelector('.lightbox-controls');
	if (overlay)
		document.querySelector('body').removeChild(overlay);
	if (image)
		document.querySelector('body').removeChild(image);
	if (controls)
		document.querySelector('body').removeChild(controls);
	this.isLightbox = false;
};
{% endhighlight %}


-----
Tham khảo:
- [How to build a JavaScript Library](https://faisalrashid.tech/blogs/How-to-build-a-JavaScript-Library)
- [How to build a JavaScript Library](https://levelup.gitconnected.com/how-to-build-a-javascript-library-6b7161315f3d)
- [39 of the best JavaScript libraries and frameworks to try in 2021](https://getflywheel.com/layout/best-javascript-libraries-frameworks-2020/)
