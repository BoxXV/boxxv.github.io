---
layout: post
title: Mọi thứ bạn cần biết để bắt đầu với React
subtitle: Everything you need to know to get started in React

tags:
- Front-End
- Back-End
- React
---

![React](https://boxxv.github.io/img/posts/react.png "React")

React là thư viện Front End phổ biến nhất hiện nay. React JS là một framework hiển thị view chú ý đến hiệu năng (performance-minded) được tạo ra bởi Facebook. Rất nhiều đối thủ nặng ký về framework MVVM (Model-View-ViewModel) mất một thời gian lớn để hiển thị những lượng data lớn, như trong trường hợp những danh sách (list) và tương tự. Nhưng React đó không còn là vấn đề, vì nó chỉ hiển thị những gì thay đổi.

Ví dụ, nếu chúng ta đang xem một danh sách có 20 products được hiển thị bởi React, và chúng ta thay đổi product thứ 2, thì chỉ product đó được hiển thị lại, và 19 products còn lại vẫn giữ nguyên (không cần hiển thị lại). React cũng dùng cái gọi là “DOM ảo” (“virtual DOM”) để tăng hiệu năng bằng cách xuất ra một hiển thị ảo, sau đó kiểm tra sự khác biệt giữa hiển thị ảo và những gì có trên DOM và tạo một bản vá (a patch).

Nhưng bắt đầu học React có thể đôi lúc gặp khó khăn. Gồm những Component, states, props and functional programming. Bài viết này cố gắng giải quyết vấn đề này, bằng cách chỉ ra cho bạn cách bắt đầu tốt và dễ dàng trong React. Vì vậy, không lãng phí thêm thời gian nữa, hãy tới luôn nào.

## Môi Trường

Chúng ta sẽ sử dụng một tệp HTML đơn giản trong bài viết này. Chỉ cần include các thẻ scritpt sau trong phần head file HTML của bạn.

```html
<script src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/6.26.0/babel.js"></script>
```

## Components

Components là thịt và khoai tây của một ứng dụng React.
Chúng là các khối mã độc lập và có thể tái sử dụng để xây dựng ứng dụng React.
Hãy xem xét component đầu tiên của chúng ta có.

```javascript
class App extends React.Component{
	render(){
		return <h3>Hello React World.</h3>
	}
}
ReactDOM.render(            
	<App />,
	document.getElementById('root')
);
```

Component của chúng ta là một lớp ES6 được extent từ class Component của React. Nó có một phương thức duy nhất hiện được gọi là `render()`, trả về một phần tử h3 trả về văn bản ‘Hello React World’. Trình duyệt sẽ chỉ hiển thị các phần tử được trả về bởi phương thức `render()`.


## JavaScript Syntax Extension (JSX)

Phần tử h3 mà chúng ta đã khai báo trong component App không phải là HTML, đó là JavaScript Syntax Extension (JSX). JSX là một phần mở rộng cú pháp trong JavaScript. Nó cho phép chúng ta viết HTML như JavaScript Objects (JSX) trong JavaScript.

```javascript
class App extends React.Component{
	render(){
		const element = <h3>Hello React World</h3>;
		return <div>{element}</div>;
	}
}
```

JSX cho chúng ta sức mạnh của JavaScript khi viết HTML. Các dấu ngoặc nhọn {} trong ví dụ trên cho trình biên dịch React biết rằng phần tử là một biến JavaScript.

## Props

Props là một attribute của Component. Là các thuộc tính được truyền bởi thành phần cha cho các thành phần con.

Đó là một mô hình chung trong React để trừu tượng hóa logic UI phổ biến trong các components con. Trong những trường hợp đó, nó là dùng chung cho component cha để truyền một số dữ liệu như các thuộc tính trong các component con.

```javascript
class App extends React.Component {
	render() {
		return <Greet greeting="Hello" />;  
	}
}
class Greet extends React.Component{
	render(){
		return <h3>{this.props.greeting} World</h3>;
	}
}
```

Trong ví dụ trên, chúng ta đã thông qua "Hello" gọi đến component `Greet` và sử dụng nó trong component App của chúng tôi. Chúng ta có thể truy cập tất cả các `props` từ đối tượng `this.props` của class chúng ta. Trong trường hợp này, chúng ta đang truy cập `greeting` như `this.props.greeting`.

Khá nhiều cấu trúc dữ liệu mặc định trong JavaScript: string literals, numbers, array, objects, and even functions.


#### PropTypes

Khi bạn muốn validate props, hãy sử dụng PropTypes để làm việc đó.

```javascript
var Image = React.createClass({
      propTypes: {
        name:   React.PropTypes.string.isRequired,
        width:  React.PropTypes.number.isRequired,
        height: React.PropTypes.number.isRequired,
        alt:    React.PropTypes.string
      },
      render() {
        var src = 'http://www.keenthemes.com/preview/metronic/theme/assets/global/plugins/jcrop/demos/demo_files/image1.jpg';
        return (
          <div>
          <img src={src} width={this.props.width} height={this.props.height} alt={this.props.alt} />
          <span>{this.props.name}</span>
          </div>
        );
      }
    });
React.render(<Image name="good Image" height={100} alt={"fdf"} />,document.body);
```

Nhìn vào `propTypes` thì ta sẽ thấy các giá trị được validate như là name phải là require, width với height là number ...

#### Giá trị Prop mặc định

React cung cấp cho bạn cách define default valuse cho props rất rõ ràng

```javascript
getDefaultProps() {
	return {
		name: "Test"
	};
},
```

#### setProps và replaceProps

- `setProps`: sẽ thay đổi (merge) properties của Component và trigger một `re-render`. Ngoài ra, chúng ta cũng có thể đưa vào một callback function mà sẽ được thực thi một khi setProps được hoàn thành.

- `replaceProps`: delete các props tồn tại trước đó và thay bởi properties mới.


## State

State của một class React cho phép chúng ta theo dõi được nhưng sự thay đổi bên trong view. State nắm giữ dữ liệu private, dynamic của component. State giữ dữ liệu thay đổi giữa nhiều render của component.

Props được chuyển đến component (như tham số chức năng), trong khi state được quản lý trong component (như các biến được khai báo bên trong một hàm)

#### Sự giống và khác nhau props, state
- props và state đều là plain JS objects
- props và state đều trigger render update khi thay đổi

| Thuộc tính | Props | State |
| -- | -- | -- |
| Có thể nhận giá trị ban đầu từ Component cha không? | Có | Có |
| Có thể được thay đổi bởi Component cha? | Có | Không |
| Có thể đặt giá trị default bên trong Component không? | Có  | Có |
| Có thể thay đổi bên trong Component? | Không | Có |
| Có thể đặt giá trị initial cho các Component con không? | Có | Có |
| Có thể thay đổi trong các Component con không? | Có | Không |

```javascript
class App extends React.Component {
	constructor(){
		super();
		this.state = {name :"Abdul Moiz"};
	}
	changeName(){
		this.setState({name : "John Doe"});
	}

	render(){
		return (
			<div>
				<h3>Hello {this.state.name}</h3>
				<button type='button' onClick=this.changeName.bind(this)}>
					Change
				</button>
			</div>
		);
	}
}
```

Chúng ta phải khởi tạo `state` trong một constructor và sau đó chúng ta có thể sử dụng nó trong phương thức render. Giống như props, chúng ta đang truy cập `state` với đối tượng `‘this.state’` này. Và trên sự kiện nhấp chuột của thay đổi button, chúng ta đang thay đổi giá trị của tên trong state thành 'John Doe'.

Chúng ta đang sử dụng phương thức `setState()` để thay đổi state của chúng ta. setState () có sẵn theo mặc định trong React Component và là cách duy nhất để thay đổi state.

## Event Handlers

Event handlers trong React không khác với các trình xử lý sự kiện trong DOM. Nhưng họ có một số khác biệt nhỏ nhưng lại quan trọng.

Trong DOM, event handlers là lowercase, nhưng trong React, trình xử lý sự kiện là camelCase. Thứ hai, trong DOM, các trình xử lý sự kiện có giá trị như một chuỗi, nhưng trong React, các trình xử lý sự kiện lấy tham chiếu hàm làm giá trị.

Sau đây là ví dụ về cách chúng ta sẽ xử lý sự kiện trong DOM:
```javascript
<button type="submit" onclick="doSomething()"></button>
```

Và đây là cách nó được thực hiện trong React:
```javascript
<button type="submit" onClick=doSomething></button>
```

Nếu bạn nhận thấy, trong DOM, chúng tôi đang xử lý sự kiện nhấp chuột bằng cách sử dụng thuộc tính DOM onclick (lowercase). Trong React, chúng ta đang sử dụng trình xử lý sự kiện onClick (camelCase) từ React. Ngoài ra, chúng ta đang chuyển một giá trị chuỗi doSomething () trong DOM. Nhưng trong React, chúng ta chuyển tham chiếu của hàm doSomething làm giá trị.


## Life Cycle Methods (Life Cycle Hooks)

React cho chúng ta một số phương pháp đặc biệt gọi là Life Cycle Hooks. Những Life Cycle Hooks này chạy vào những thời điểm cụ thể trong life cycle của một component. May mắn thay, chúng ta có thể đặt chức năng riêng của chúng ta vào những Life Cycle Hookss, bằng cách ghi đè chúng trong thành phần của chúng ta. Hãy xem xét một số Life Cycle Hooks thường được sử dụng.

Mounting là thời điểm thành phần được hiển thị lần đầu tiên trong trình duyệt.

#### componentWillMount()
Thực hiện một số tác vụ, khi component sẽ được mount. hàm này chỉ thực hiện 1 lần duy nhất

#### componentDidMount()
Chạy sau khi component được mounted, hàm này chỉ thực hiện 1 lần duy nhất. Đó là một không gian tốt để lấy bất kỳ dữ liệu hoặc bắt đầu bất cứ điều gì. 

Hàm này được gọi để thông báo component đã tồn tại trên DOM. Tức là hàm render đã chạy, từ đó các thao tác trên DOM sẽ có thể thực hiện bình thường đối với component này.

#### shouldComponentUpdate(nextProps, nextState)
Hàm này thực hiện khi state và props thay đổi. Hàm này sẽ trả về kết quả true/false. Bạn sẽ cần sử dụng đến hàm này để xử lý xem có cần update component không

#### componentWillUpdate(nextProps, nextState)
Hàm này thực hiện dựa vào kết quả của hàm trên (shouldComponentUpdate). Nếu hàm trên trả về false, thì React sẽ không gọi hàm này.

#### componentDidUpdate(prevProps, prevState) {
Như tên gọi của nó, componentDidUpdate () chạy sau khi component được cập nhật, được render lại. Đây là nơi xử lý các thay đổi dữ liệu. Có thể bạn muốn xử lý một số yêu cầu mạng hoặc thực hiện các phép tính dựa trên dữ liệu đã thay đổi. componentDidUpdate () là nơi để làm tất cả điều đó.

#### componentWillReceiveProps(nextProps)
Hàm này thực hiện liên tục mỗi khi props thay đổi
Có thể sử dụng với mục đích:
- (1) Sử dụng để thay đổi trạng thái (state) của component phụ thuộc props.
- (2) Sử dụng các kết quả, khởi tạo biến có tính chất async (bất đồng bộ).

#### componentWillUnmount()
Khi component sẽ unmount, hàm này thực hiện một lần duy nhất. Hàm này hữu dụng khi bạn cần xoá các timer hoặc EventListener không còn sử dụng.

![React](https://boxxv.github.io/img/posts/16317e21-fb30-4dd1-880e-18fbefa69e27.webp "React")

### Khởi tạo Component
1. Khởi tạo Class (đã thừa kế từ class Component của React)
2. Khởi tạo giá trị mặc định cho Props (`defaultProps`)
3. Khởi tạo giá trị mặc định cho State (trong hàm `constuctor`)
4. Gọi hàm `componentWillMount()`
5. Gọi hàm `render()`
6. Gọi hàm `componentDidMount()`

### Khi State thay đổi
1. Cập nhật giá trị cho `state`
2. Gọi hàm `shouldComponentUpdate()`
3. Gọi hàm `componentWillUpdate()` – với điều kiện hàm `shouldComponentUpdate()` trả về true
4. Gọi hàm `render()`
5. Gọi hàm `componentDidUpdate()`

### Khi Props thay đổi
1. Cập nhật giá trị cho `props`
2. Gọi hàm `componentWillReceiveProps()`
3. Gọi hàm `shouldComponentUpdate()`
4. Gọi hàm `componentWillUpdate()` – với điều kiện hàm `shouldComponentUpdate()` trả về true
4. Gọi hàm `render()`
5. Gọi hàm `componentDidUpdate()`


Hãy xem điều đó trong thực tế:

```javascript
class App extends React.Component {
	constructor(){
		super(); 
		this.state = {
			person : {name : "" , city : ""}
		};
	}
	componentDidMount(){
		//make any ajax request
	 this.setState({
			person : {name : "Abdul Moiz",city : "Karachi"}
		});
	}
	componentDidUpdate(){
		//because I could'nt come up with a simpler example of //componentDidUpdate
		console.log('component has been updated',this.state);
	}
	render(){
		return (
			<div>
				<p>Name : {this.state.person.name}</p>
				<p>City : {this.state.person.city}</p>
			</div>
		);
	}
}
```

Trạng thái ban đầu của chúng ta có hai thuộc tính, name và city, và cả hai đều có một chuỗi rỗng làm giá trị. Trong componentDidMount(), chúng ta đặt state và đổi name thành 'Abdul Moiz' và city thành 'Karachi'. Bởi vì chúng ta đã thay đổi state, component được cập nhật như là kết quả của việc thực thi componentDidUpdate().


-----
Tham khảo:
- [React homepage](https://reactjs.org)
- [React roadmap](https://roadmap.sh/react)

- [Tất cả mọi thứ bạn cần biết để bắt đầu học React](https://viblo.asia/p/tat-ca-moi-thu-ban-can-biet-de-bat-dau-hoc-react-Qbq5QAPR5D8)
- [Everything you need to know to get started in React](https://www.freecodecamp.org/news/everything-you-need-to-know-to-get-started-in-react-11311ae997cb)
- [80 Videos học ReactJS 2022](https://www.youtube.com/playlist?list=PL_-VfJajZj0UXjlKfBwFX73usByw3Ph9Q)
- [Tìm hiểu về ReactJs](https://viblo.asia/p/tim-hieu-ve-reactjs-ogBG2lo5RxnL)
- [ReactJS cho người mới bắt đầu](https://viblo.asia/p/reactjs-cho-nguoi-moi-bat-dau-LzD5dP9e5jY)
- [Một số thứ cần biết trước khi tìm hiểu về ReactJS ( Phần 1 )](https://viblo.asia/p/mot-so-thu-can-biet-truoc-khi-tim-hieu-ve-reactjs-phan-1-YWOZrg0YlQ0)
- [Một số thứ cần biết trước khi tìm hiểu về ReactJS ( Phần 2 )](https://viblo.asia/p/mot-so-thu-can-biet-truoc-khi-tim-hieu-ve-reactjs-phan-2-GrLZDXXwZk0)
- [Bắt đầu với ReactJs (Phần 1)](https://viblo.asia/p/bat-dau-voi-reactjs-phan-1-3P0lPOE8Zox)
- [Bắt đầu với ReactJs (Phần 2)](https://viblo.asia/p/bat-dau-voi-reactjs-phan-2-1Je5EMGA5nL)
- [Học React.js trong 5 phút!](https://viblo.asia/p/hoc-reactjs-trong-5-phut-E375zRwq5GW)
- [Tập tọe những bước chân đầu tiên ReactJS](https://viblo.asia/p/tap-toe-nhung-buoc-chan-dau-tien-reactjs-gAm5yqpV5db)
- [Basic ReactJs (P1) ](https://viblo.asia/p/basic-reactjs-p1-4dbZNDdq5YM)
- [Basic ReactJs (P2) ](https://viblo.asia/p/basic-reactjs-p2-ORNZqoRG50n)
- [Tìm hiểu react - part 1](https://viblo.asia/p/tim-hieu-react-part-1-djeZ1g3j5Wz)
- [Tìm hiểu react - part 2](https://viblo.asia/p/tim-hieu-react-part-2-Qbq5QqJm5D8)
- [Những khái niệm cơ bản trong ReactJS cho người mới bắt đầu](https://viblo.asia/p/nhung-khai-niem-co-ban-trong-reactjs-cho-nguoi-moi-bat-dau-WAyK8pDpKxX)
- [Những khái niệm cơ bản trong ReactJS cho người mới bắt đầu (Phần 2)](https://viblo.asia/p/nhung-khai-niem-co-ban-trong-reactjs-cho-nguoi-moi-bat-dau-phan-2-eW65GP9aKDO)
- [Conditional Rendering](https://reactjs.org/docs/conditional-rendering.html)
- [Tìm hiểu ReactJS từ con số 0](https://viblo.asia/p/tim-hieu-reactjs-tu-con-so-0-63vKjvn6K2R)
- [Học ReactJs từ số 0 - P1](https://viblo.asia/p/hoc-reactjs-tu-so-0-p1-jvElaPaoZkw)
- [Học ReactJs từ số 0 - P2 - Getting Started With Introducing JSX](https://viblo.asia/p/hoc-reactjs-tu-so-0-p2-getting-started-with-introducing-jsx-E375zWJ1KGW)
- [Học ReactJs từ số 0 - P3 - Rendering Elements](https://viblo.asia/p/hoc-reactjs-tu-so-0-p3-rendering-elements-1Je5Ee7A5nL)
- [Học ReactJs từ số 0 - P4 - Components and Props](https://viblo.asia/p/hoc-reactjs-tu-so-0-p4-components-and-props-bJzKmyBEK9N)
- [Học ReactJs từ số 0 - P5 - State and Lifecycle](https://viblo.asia/p/hoc-reactjs-tu-so-0-p5-state-and-lifecycle-oOVlYGPBK8W)
- [Học ReactJs từ số 0 - P6 - Handling Events](https://viblo.asia/p/hoc-reactjs-tu-so-0-p6-handling-events-1VgZv1N2KAw)
- [Học ReactJs từ số 0 - P7 - Conditional Rendering](https://viblo.asia/p/hoc-reactjs-tu-so-0-p7-conditional-rendering-gAm5yWrqZdb)
- [Học ReactJs từ số 0 - P8 - Lists and Keys](https://viblo.asia/p/hoc-reactjs-tu-so-0-p8-lists-and-keys-4dbZNYEaKYM)
- [Học ReactJs từ số 0 - P9 - Form](https://viblo.asia/p/hoc-reactjs-tu-so-0-p9-form-63vKjXLVl2R)
- [Học ReactJs từ số 0 - P10 - Lifting State Up](https://viblo.asia/p/hoc-reactjs-tu-so-0-p10-lifting-state-up-naQZRDDX5vx)
- [Học ReactJs từ số 0 - P11 - Composition vs Inheritance](https://viblo.asia/p/hoc-reactjs-tu-so-0-p11-composition-vs-inheritance-WAyK8PgeKxX)
- [Học ReactJs từ số 0 - Advance - P1 - Context](https://viblo.asia/p/hoc-reactjs-tu-so-0-advance-p1-context-XL6lAQnRlek)
- [Học ReactJs từ số 0 - Advance - P1 - Context - P2](https://viblo.asia/p/hoc-reactjs-tu-so-0-advance-p1-context-p2-Qbq5Qyz35D8)
- [Học ReactJs từ số 0 - Advance - P2 - Error Boundaries](https://viblo.asia/p/hoc-reactjs-tu-so-0-advance-p2-error-boundaries-WAyK822olxX)
- [Học ReactJs từ số 0 - Advance - P3 - Forwarding Refs](https://viblo.asia/p/hoc-reactjs-tu-so-0-advance-p3-forwarding-refs-WAyK82wnlxX)
- [Học ReactJs từ số 0 - Advance - P4 - Fragments](https://viblo.asia/p/hoc-reactjs-tu-so-0-advance-p4-fragments-L4x5x3dYlBM)
- [Học reactjs thông qua ví dụ phần 1](https://viblo.asia/p/hoc-reactjs-thong-qua-vi-du-phan-1-yMnKMnGaZ7P)
- [Học reactjs thông qua ví dụ phần 2](https://viblo.asia/p/hoc-reactjs-thong-qua-vi-du-phan-2-eW65Ge2RZDO)
- [Học reactjs thông qua ví dụ phần 3](https://viblo.asia/p/hoc-reactjs-thong-qua-vi-du-phan-3-4dbZNwkLlYM)
- [Học reactjs thông qua ví dụ phần 4](https://viblo.asia/p/hoc-reactjs-thong-qua-vi-du-phan-4-ByEZkyQ25Q0)
- [Học reactjs thông qua ví dụ phần 5](https://viblo.asia/p/hoc-reactjs-thong-qua-vi-du-phan-5-YWOZrwd7lQ0)
- [Học reactjs thông qua ví dụ phần 6](https://viblo.asia/p/hoc-reactjs-thong-qua-vi-du-phan-6-4P856kgRKY3)
- [Học reactjs thông qua ví dụ phần 7](https://viblo.asia/p/hoc-reactjs-thong-qua-vi-du-phan-7-slider-Qbq5QpVzlD8)
- [Học reactjs thông qua ví dụ phần 8](https://viblo.asia/p/hoc-reactjs-thong-qua-vi-du-phan-8-slideshow-gallery-YWOZrBdPZQ0)
- [Học reactjs thông qua ví dụ phần 9](https://viblo.asia/p/hoc-reactjs-thong-qua-vi-du-phan-9-modal-image-maGK7OBAKj2)
- [Học reactjs thông qua ví dụ phần 10](https://viblo.asia/p/hoc-reactjs-thong-qua-vi-du-phan-10-light-box-bJzKmxJ659N)
- [Học reactjs thông qua ví dụ phần 11](https://viblo.asia/p/hoc-reactjs-thong-qua-vi-du-phan-11-tab-gallery-L4x5xMGbKBM)

Redux
- [Tìm hiểu về Redux trong ReactJS](https://viblo.asia/p/tim-hieu-ve-redux-trong-reactjs-GrLZDe7Olk0)
- [Tìm hiểu Redux qua ví dụ thực tế](https://viblo.asia/p/tim-hieu-redux-qua-vi-du-thuc-te-gAm5yaNO5db)
- [Từng bước để xây dựng một ứng dụng React Redux](https://viblo.asia/p/tung-buoc-de-xay-dung-mot-ung-dung-react-redux-gGJ59jgPKX2)
- [Làm sao để áp dụng typescript vào dự án React Redux](https://viblo.asia/p/lam-sao-de-ap-dung-typescript-vao-du-an-react-redux-924lJpxXKPM)
- [Thiết lập ứng dụng React - TypeScript từ A-Z](https://viblo.asia/p/thiet-lap-ung-dung-react-typescript-tu-a-z-4dbZN1NkKYM)
- [Tản mạn về Redux và React Hooks](https://viblo.asia/p/tan-man-ve-redux-va-react-hooks-Az45br9o5xY)
- [Tìm hiểu về Redux saga](https://viblo.asia/p/tim-hieu-ve-redux-saga-bWrZnODmlxw)
- [Tìm hiểu redux-toolkit phần 1](https://viblo.asia/p/tim-hieu-redux-toolkit-phan-1-YWOZrN3vZQ0)
- [Tìm hiểu redux-toolkit phần 2](https://viblo.asia/p/tim-hieu-redux-toolkit-phan-2-QpmlejPD5rd)
- [Reflux vs. Redux](https://viblo.asia/p/reflux-vs-redux-7prv31XOMKod)
- [React bỏ Redux](https://viblo.asia/p/messi-con-roi-barca-thi-code-react-ma-bo-redux-co-gi-dau-ma-bat-ngo-1VgZvrW7ZAw)
- [Quản lý state trong React bằng Mobx - Part 1](https://viblo.asia/p/quan-ly-state-trong-react-bang-mobx-part-1-OeVKB9aM5kW)
- [Quản lý state trong React bằng Mobx - Part 2](https://viblo.asia/p/mobx-quan-ly-state-trong-react-part-2-07LKXkE25V4)
- [Giới thiệu về MobX và React trong mười phút](https://viblo.asia/p/gioi-thieu-ve-mobx-va-react-trong-muoi-phut-bJzKmyrEK9N)


- [The React Cheatsheet for 2020 (Phần 1)](https://viblo.asia/p/the-react-cheatsheet-for-2020-phan-1-WAyK8PY6KxX)
- [The React Cheatsheet for 2020 (Phần 2)](https://viblo.asia/p/the-react-cheatsheet-for-2020-phan-2-4P856oBAKY3)
- [The React Cheatsheet for 2020 (Phần cuối)](https://viblo.asia/p/the-react-cheatsheet-for-2020-phan-cuoi-oOVlYMxBl8W)
- [Các cách truyền data giữa các components trong ReactJS](https://viblo.asia/p/cac-cach-truyen-data-giua-cac-components-trong-reactjs-924lJjV0lPM)
- [Server-side Rendering trong React](https://viblo.asia/p/server-side-rendering-trong-react-yMnKMYozK7P)


- [React.js - Những Câu Hỏi Phỏng Vấn Thường Gặp - Phần 1](https://viblo.asia/p/reactjs-nhung-cau-hoi-phong-van-thuong-gap-phan-1-Ljy5VDkbZra)
- [React.js - Những Câu Hỏi Phỏng Vấn Thường Gặp - Phần 2](https://viblo.asia/p/reactjs-nhung-cau-hoi-phong-van-thuong-gap-phan-2-bWrZno8plxw)
- [React.js - Những Câu Hỏi Phỏng Vấn Thường Gặp - Phần 3](https://viblo.asia/p/reactjs-nhung-cau-hoi-phong-van-thuong-gap-phan-3-924lJBV8lPM)
- [15 câu hỏi phỏng vấn React phổ biến](https://viblo.asia/p/15-cau-hoi-phong-van-react-pho-bien-V3m5W0PwKO7)
- [15 thư viện UI Components tốt nhất cho ReactJS](https://viblo.asia/p/15-thu-vien-ui-components-tot-nhat-cho-reactjs-maGK7pDMZj2)
- [7 lần code React của bạn bốc mùi ???](https://viblo.asia/p/7-lan-code-react-cua-ban-boc-mui-bWrZnm2QKxw)
- [5 thu viện PDF cho react](https://viblo.asia/p/top-5-thu-vien-pdf-cho-react-gGJ597bPZX2)
- [3 lời khuyên nhỏ giúp tăng preformance trong ReactJS](https://viblo.asia/p/3-loi-khuyen-nho-giup-tang-preformance-trong-reactjs-V3m5WxY8KO7)
- [Tìm hiểu Props và State trong React](https://viblo.asia/p/tim-hieu-props-va-state-trong-react-GrLZD8RBZk0)
- [Sự khác nhau giữa Props và State trong ReactJS](https://viblo.asia/p/su-khac-nhau-giua-props-va-state-trong-reactjs-OeVKBvrJKkW)
- [Nested attributes with Reactjs](https://viblo.asia/p/nested-attributes-with-reactjs-924lJM4NZPM)
- [ReactJS Components: Type, Nesting, and Lifecycle](https://www.simplilearn.com/tutorials/reactjs-tutorial/reactjs-components)
- [Nesting Components](https://riptutorial.com/reactjs/example/3846/nesting-components)
- [Immutability và Immutable.js trong ReactJs](https://viblo.asia/p/immutability-va-immutablejs-trong-reactjs-m68Z0OrdKkG)
- [So sánh Server Side Rendering và Client Side Rendering trong React](https://viblo.asia/p/so-sanh-server-side-rendering-va-client-side-rendering-trong-react-V3m5WBrylO7)
- [Một số feature ES6 thường dùng với Reactjs](https://viblo.asia/p/mot-so-feature-es6-thuong-dung-voi-reactjs-E375zb7R5GW)
- [React Lifecycle Methods](https://viblo.asia/p/react-lifecycle-methods-WAyK81vkZxX)
- [[ReactJS] Higher-Order Component](https://viblo.asia/p/reactjs-higher-order-component-E375zkybKGW)
- [Book: Learning React](https://www.oreilly.com/library/view/learning-react/9781491954614/)
- [Cái nhìn tổng quan về State trong React](https://viblo.asia/p/cai-nhin-tong-quan-ve-state-trong-react-6J3ZggjAZmB)
- [Tự tạo Calendar bằng React với day.js](https://viblo.asia/p/tu-tao-calendar-bang-react-voi-dayjs-Az45brLw5xY)
- [ReactJS Unit testing](https://viblo.asia/p/reactjs-unit-testing-rEBRAarrR8Zj)
- [Test Component với Jest và Emzyme](https://viblo.asia/p/test-component-voi-jest-va-emzyme-ORNZqBXMl0n)
- [How To Write Better Code In React](https://viblo.asia/p/how-to-write-better-code-in-react-L4x5xpaq5BM)
- [Lí do để sử dụng Typescript với React](https://viblo.asia/p/li-do-de-su-dung-typescript-voi-react-aWj53bVbl6m)
- [Nhúng TypeScript vào ReactJS](https://viblo.asia/p/sai-gon-thi-dau-long-nhung-nhung-typescript-vao-reactjs-thi-chua-chac-4dbZNGgQlYM)
- [Life cycle của Component trong Reactjs](https://viblo.asia/p/co-ban-life-cycle-cua-component-trong-reactjs-QpmleM39lrd)
- [Routing trong reactjs](https://viblo.asia/p/phan-1routing-trong-reactjs-1VgZvQjmKAw)
- [JSX mang gì về cho React?](https://viblo.asia/p/chu-den-mang-tien-ve-cho-me-con-jsx-mang-gi-ve-cho-react-924lJBQalPM)
- [Fullstack React với Blitzjs](https://viblo.asia/p/fullstack-react-voi-blitzjs-p1-gioi-thieu-V3m5WWo75O7)
- [Tự tạo một Single Page Application với React JS và kiến trúc Flux](https://viblo.asia/p/tu-tao-mot-single-page-application-voi-react-js-va-kien-truc-flux-1l0rvmnDRyqA)
- [Spring Kết Hợp React](https://viblo.asia/p/spring-ket-hop-react-V3m5WbvQlO7)
- [Làm game đoán từ cơ bản để luyện ReactJS](https://viblo.asia/p/lam-game-doan-tu-co-ban-de-luyen-reactjs-Az45b0DwZxY)
- [Tổng quan và so sánh ReactJS với VueJS](https://viblo.asia/p/tong-quan-va-so-sanh-reactjs-voi-vuejs-LzD5deXEKjY)
- [Tại sao bạn nên chọn VueJS hơn là ReactJS dành cho các dự án startup](https://viblo.asia/p/tai-sao-ban-nen-chon-vuejs-hon-la-reactjs-danh-cho-cac-du-an-startup-63vKj6xbK2R)
- ["Một chút" về kiến trúc mới của React Native](https://viblo.asia/p/mot-chut-ve-kien-truc-moi-cua-react-native-Az45bRXO5xY)

Debug trong ứng dụng ReactJS
- [Redux DevTools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd/related)
- [Sử dụng React Developer Tools để debug React Component](https://viblo.asia/p/su-dung-react-developer-tools-de-debug-react-component-V3m5WLQWKO7)
- [Giới thiệu về Debug trong ứng dụng ReactJS](https://medium.com/velacorpblog/gi%E1%BB%9Bi-thi%E1%BB%87u-v%E1%BB%81-debug-trong-%E1%BB%A9ng-d%E1%BB%A5ng-reactjs-6c353ce1ce96)
- [Hướng dẫn Debug ứng dụng ReactJS ngay trong VS Code](https://vntalking.com/debug-react-trong-vscode.html)
- [ReactJS: Cách gỡ lỗi (debug) các component bằng React Developer Tools](https://v1study.com/reactjs-how-to-cach-go-loi-debug-cac-component-bang-react-developer-tools.html)