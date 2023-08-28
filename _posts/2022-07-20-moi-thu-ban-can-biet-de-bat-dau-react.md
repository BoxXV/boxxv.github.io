---
layout: post
title: Mọi thứ bạn cần biết để bắt đầu với React
subtitle: Everything you need to know to get started in React

tags:
- Front-End
- Back-End
- React
---

![React Roadmap](https://boxxv.github.io/img/2023/react.jpg "React Roadmap")

![React Developer Roadmap in 2019](https://raw.githubusercontent.com/adam-golab/react-developer-roadmap/master/roadmap.png "React Developer Roadmap in 2019")

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

Sau đây là một số ưu điểm mà đi kèm với nó:
- **Nhanh hơn** vì nó thực hiện tối ưu hóa trong khi biên dịch mã thành JavaScript.
- **An toàn** và hầu hết các lỗi có thể bị bắt trong quá trình biên dịch.
- Giúp bạn viết mẫu **dễ dàng hơn** và **nhanh hơn**, nếu bạn quen thuộc với HTML.

Mặc dù nó tương tự như HTML, nhưng có một vài điều chúng ta cần lưu ý khi làm việc với JSX.

#### Phần tử lồng nhau:
Nếu bạn muốn trả về nhiều phần tử hơn, chúng ta cần bọc nó với một phần tử, phần tử gì cũng được miễn sao nó bao bọc những thẻ còn lại, mình thường sử dụng thẻ `<div>`.

#### Thuộc tính
Nếu muốn sử dụng các thuộc tính tùy chỉnh của riêng các bạn ngoài các thuộc tính và thuộc tính HTML thông thường. Ví dụ ta muốn thêm thuộc tính tùy chỉnh, chúng ta cần sử dụng tiền tố data-. Ví dụ: data-myattribute.

#### Biểu thức Javascript
Các biểu thức JavaScript có thể được sử dụng bên trong JSX. Chúng ta chỉ cần bọc nó với dấu ngoặc nhọn {}. Ví dụ sau sẽ hiển thị số 2: <h1>{ 1+1 }</h1>

#### Style
Style trong JSX sử dụng inline. Khi chúng ta muốn thiết lập style, chúng ta cần sử dụng cú pháp camelCase. React cũng sẽ tự động thêm px sau giá trị số trên các phần tử cụ thể. Ví dụ sau đây cho thấy cách thêm style inline vào phần tử h1.

```javascript
render() {
	var myStyle = {
		fontSize: 100,
		color: '#FF0000'
	}
	return (
		<div>
			<h1 style = { myStyle }>Header</h1>
			<h2>Content</h2>
			<p data-myattribute = "somevalue">This is the content!!!</p>
		</div>
	);
}
```

#### Comment
Khi cần comment, chúng ta cần đặt nó trong dấu ngoặc nhọn {}.

```javascript
{//End of the line Comment...}
{/*Multi line comment...*/}
```

#### Quy ước đặt tên

Thẻ HTML luôn sử dụng tên thẻ thường, trong khi các thành phần React bắt đầu bằng chữ hoa.

Lưu ý - Bạn nên sử dụng **className** và **htmlFor** làm tên thuộc tính XML thay vì `class` và `for`.

Vì JSX là JavaScript, nên các mã định danh như class và for không được khuyến khích là các tên thuộc tính XML. Thay vào đó, các thành phần React DOM mong đợi các tên thuộc tính DOM như className và htmlFor tương ứng.

```javascript
<div className="container">
	<h1 style = { myStyle }>Header</h1>
	<h2>Content</h2>
	<p data-myattribute = "somevalue">This is the content!!!</p>
	<label htmlFor="ex">Name: </label>
	<input type="text" id="ex" placeholder="Something" />
</div>
```

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


## Redux

Là một thư viện javascript giúp tạo ra một lớp quản lý trạng thái (state) của ứng dụng. Được dựa trên nền tảng tư tưởng của kiến trúc Flux do Facebook giới thiệu, do vậy Redux thường là bộ đôi kết hợp hoàn hảo với Reactjs.

![Redux](https://boxxv.github.io/img/posts/redux-basic-concepts-and-data-flow-0-1635261038.gif "Redux")

Nguồn dữ liệu tin cậy duy nhất: State của toàn bộ ứng được chứa trong một object tree nằm trong Store duy nhất Trạng thái chỉ được phép đọc: Cách duy nhất để thay đổi State của ứng dụng là phát một Action (là 1 object mô tả những gì xảy ra) Thay đổi chỉ bằng hàm thuần túy: Để chỉ ra cách mà State được biến đổi bởi Action chúng ta dùng các pure function gọi là Reducer

Về cơ bản Redux có các thành phần như sau:

#### 1. Action
Trong Redux, cách duy nhất để thay đổi nội dung state là phải submit lên 1 cái mẫu tin. mà theo lí thuyết Redux là action. Đó là một đối tượng mô tả những gì đã diễn ra, và bạn send nó tới store bằng cách store.dispatch()

```javascript
function addTodo(text) {
	return {
		type: ADD_TODO,
		text
	}
}
```

#### 2. Reducer
Reducer là những pure function, tức là nó sẽ không thay đổi giá trị của những tham số truyền vào. Ngoài ra, nó sẽ trả về 1 đối tượng khác không có những tham chiếu gì đến tham số truyền vào. Là nơi xác định State thay đổi như thế nào.

```javascript
function todoApp(state = initialState, action) {
  switch (action.type) {
    case ADD_TODO:
      return Object.assign({}, state, {
        todos: [
          ...state.todos,
          {
            text: action.text,
            completed: false
          }
        ]
      })
    default:
      return state
  }
}
```

#### 3. Store
Trong Redux, trạng thái của toàn bộ ứng dụng được lưu trữ bằng một cây đôi tượng thể hiện trạng thái hiện hành của dữ liệu trong ứng dụng và cây này được lưu trong 1 store.

Điều này giúp cho ta có thể phát triển những ứng dụng lớn vì trạng thái dữ liệu có thể đồng bộ từ tầng server đến tầng client mà không phải tốn nhiều công sức. Là nơi quản lý State, cho phép truy cập State qua getState(), update State qua dispatch(action), đăng kí listener qua subscribe(listener).


```javascript
import { createStore } from 'redux'
import todoApp from './reducers'

let store = createStore(todoApp)
```

#### 4. View
Hiển thị dữ liệu được cung cấp bởi Store

![Redux](https://boxxv.github.io/img/posts/Redux Flow.jpg "Redux")

#### Middleware
Về cơ bản nó nhận các action đầu vào rồi và trả ra cũng là các action trước khi dispatch đến reducer để xử lý

#### Redux-sagas
Cho phép bạn thực hiện các request API và các tác vụ bất đồng bộ nhờ vào function generator


### Middleware library

Trên thực tế thì việc thao tác với các state ở redux store có nhiều vấn đề khác, ví dụ mình muốn gọi api, hoặc sử dụng các hàm setTimeout để thao tác các state thì sao, tất cả những việc đó được gọi chung là side effects, vậy làm thế nào để mình handle được những side effect đó. Thì lúc này middleware library sẽ giúp xử lý những vấn đề này. Các bạn có thể hiều đơn gian middleware library là thành phần đứng giữa các action và reducer. Khi một action được dispatch vào reducer, thì nó sẽ kiểm tra xem action đó có thực thiện bất đồng bộ hay không, nếu có nó sẽ chờ cho action bất đồng bộ thực hiện xong rồi mới đưa action vào trong reducer. 

Một số library middleware thường sử dụng:
- Redux-thunk
- Redux-saga
- Redux-promise

### Redux-thunk
Ở trong phạm vi của bài viết này mình sẽ chỉ nói về redux thunk và redux saga. Redux thunk: Chắc các bạn cũng biết là action thường trả về dạng object, người ta hay gọi là plain Javascript object. Trong trường hợp mình muốn gọi một api để trả về một list trending thì action của mình không thể trả về một plain Javascript object thông thường được, mà mình sẽ phải trả về một function, action như vậy được gọi là async action. Đây là code cho ví dụ của mình:

```javascript
export const fetchTrendingRequest = () => {
  return (dispatch) => {
    callAPI().then(({data})=>{
      dispatch(fetchTrending(data.data));
    })
  }
}

export const fetchTrending = (trendings) => {
  return {
    type: Types.FETCH_TRENDING,
    trendings
  }
}
```

Các bạn hãy quan sát action đầu tiên của mình, ở đây mình trả về một function và function này sẽ tiến hành call api để lấy về listTrending, lúc này redux thunk nó sẽ cho phép chương trình dừng lại cho đến khi api gọi xong và trả về kết quả. Tiếp đến mình gọi đến một action bên dưới truyền data vừa mới get được vào và lúc này redux thunk nó sẽ kiểm tra action này không thực hiện async nên nó sẽ đưa đến cho reducer để xử lý. Đây cũng là một quy trình cơ bản mà redux thunk thực hiện. Khá là đơn giản, còn về làm thế nào để set up redux thunk thì các bạn có thể xem ở đây: https://github.com/reduxjs/redux-thunk

### Redux saga

Về mặt cơ chế hoạt động thì nó cũng tương tự như thunk, dùng để handle các side effect. Redux saga cung cấp các hàm helper effect, các hàm này sẽ trả về một effect object chứa đựng thông tin đặc biệt chỉ dẫn middeware của Redux có thể thực hiện tiếp các hành động khác. Các hàm helper effect sẽ được thực thi trong các generator function. Generator function là một tính năng mới trong ES6, nó cũng là một function. Tuy nhiên điểm đặc biệt của function này là có thể tạm dừng để thực thi một việc khác, hoặc có thể gọi đến một Generator function khác. Chi tiết về Generator function: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*

Một số helper của generator function được redux saga sử dụng:
- `takeEvery()` : thực thi và trả lại kết quả của mọi actions được gọi.
- `takeLastest()` : có nghĩa là nếu chúng ta thực hiện một loạt các actions, nó sẽ chỉ thực thi và trả lại kết quả của của actions cuối cùng.
- `take()` : tạm dừng cho đến khi nhận được action
- `put()` : dispatch một action.
- `call()`: gọi function. Nếu nó return về một promise, tạm dừng saga cho đến khi promise được giải quyết.
- `race()` : chạy nhiều effect đồng thời, sau đó hủy tất cả nếu một trong số đó kết thúc

Đối với redux thunk nó có những ưu nhược điểm như sau:

| So sánh | Redux Thunk | Rudux-saga |
| -- | -- | -- |
| Ưu điểm | Đơn giản, mạnh mẽ, dễ sử dụng , dễ tiếp cận đối với các bạn là mới học React | Đối với những dự án phức tạp sử dụng redux-saga code sẽ clean và dễ test hơn so với redux-thunk, giải quyết được những vấn đề về chains of promises |
| Nhược điểm | Chỉ phù hợp với các dự án nhỏ, xử lý logic đơn giản. Còn đối với những dự án phức tạp sử dụng redux-thunk sẽ phải tốn nhiều dòng code và gây khó khăn cho việc test các action | Phức tạp, tốn thời gian cho member mới vào team, nặng về xử lý logic, không dành cho những ứng dụng đơn giản |

Trên đây là mình đã chia sẻ về redux-thunk và resux-saga. Đây là 2 middleware library được dùng nhiều trong Reactjs, việc lựa chọn redux-thunk hay redux-saga còn tùy thuộc vào project.

Tài liệu tham khảo
https://medium.com/@shoshanarosenfield/redux-thunk-vs-redux-saga-93fe82878b2d


## Hook
Chúng ta có 10 hooks được xây dựng trong phiên bản React từ 16.8 trở đi. Chúng cho phép sử dụng state và những tính năng khác của React mà không cần phải dùng tới class.

React Hooks cho phép chúng ta có thể sử dụng state và life cycle bên trong một functional components. Hooks đem lại một vài lợi ích khi làm việc như :
- Cải thiện hiệu suất làm việc bằng cách có thể tái sử dụng code.
- Các thành phần được trình bày khoa học hơn.
- Sử dụng một cách linh hoạt trong component tree.

### useState()
Việc sử dụng useState() cho phép chúng ta có thể làm việc với state bên trong functional component mà không cần chuyển nó về class component. Ở ví dụ bên trên mình cũng đã sử dụng useState() để cập nhật state. Chúng ta có thể sử dụng nó bằng cú pháp:

```javascript
const [state, setState] = useState(initialStateValue);
```

Đây làm một hooks được sử dụng hầu như trong tất cả các funcitonal component.

### useEffect()
useEffect() là function nắm bắt tất cả các sự thay đổi của code. Trong một function component, việc sử dụng life cycle không React hỗ trợ, bởi vậy rất khó để debug, cũng như nắm bắt được quá trình khởi chạy của component.

useEffect() sinh ra để làm điều này, nó được khởi chạy khi giá trị của một biến nào đó thay đổi, hay component đã được render ra,...useEffect() có thể thay thế hòan toàn các life cycle trong class component. Chúng ta có thể sử dụng nó bằng cú pháp :

```javascript
useEffect(effectFunction, arrayDependencies);
```

### useContext()
useContext() cho phép nhận về giá trị của context mỗi khi nó thay đổi. Cú pháp cơ bản như sau:

```javascript

```

### useReducer()
Hook useReducer được sử dụng để xử lý các state phức tạp và việc chia sẻ state giữa các component. Ở đây chúng ta có cú pháp.

```javascript
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

Updating...


## Tạo ứng dụng React mới bằng cách sử dụng Create React App (CRA)

Mở terminal của bạn và chạy lệnh sau:

```bat
npx create-react-app hello-world
npx create-react-app hello-world-typescript --template typescript
npx create-react-app hello-world-empty --template cra-template-empty
npx create-react-app hello-world-minimal --template cra-template-minimal

npm init react-app hello-world

yarn create react-app hello-world
```

Chạy ứng dụng React

```bat
cd hello-world
cd hello-world-typescript
cd hello-world-empty
cd hello-world-minimal

npm start
```

## Cấu trúc thư mục

Việc chạy bất kỳ lệnh nào trong số này sẽ tạo một thư mục có tên `hello-world` bên trong thư mục hiện tại. Bên trong thư mục đó, nó sẽ tạo cấu trúc dự án ban đầu và cài đặt các phụ thuộc bắc cầu:

```
hello-world
├── README.md
├── node_modules
├── package.json
├── .gitignore
├── public
│   ├── favicon.ico
│   ├── index.html
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    ├── serviceWorker.js
    └── setupTests.js
```




-----
Tham khảo:
- [React homepage](https://reactjs.org)
- React [Roadmap](https://roadmap.sh/react)
- [Awesome React](https://github.com/enaqx/awesome-react)
- [Redux homepage](https://redux.js.org)
- [ReactJS là gì? Những điều bạn cần biết về ReactJS](https://200lab.io/blog/reactjs-la-gi/)
- [Generate a new React app using Create React App (CRA)](https://create-react-app.dev/)

-----
- [Next.js vs. Remix vs. Gatsby: Which One to Choose for Your Next Project?](https://medium.com/codex/next-js-vs-remix-vs-gatsby-which-one-to-choose-for-your-next-project-ab89fb8e48c4)
- [Getting Started: Gatsby vs. Next.js vs. Remix](https://satellytes.com/blog/post/getting-started-gatsby-next-remix/)
- [Popular React Framework Choices to Develop React Apps in 2023](https://hackernoon.com/popular-react-framework-choices-to-develop-react-apps-in-2023)
- [Next.js vs. Gatsby in 2023](https://prismic.io/blog/compare-nextjs-vs-gatsby)
- [Next.js, Gatsby, Remix](https://reactbricks.com/features/nextjs-gatsby-remix-cms)
- [Next.js vs Astro vs Remix: Choosing the Right Front-end Framework](https://strapi.io/blog/nextjs-vs-astro-vs-remix-choosing-the-right-frontend-framework)
- [Remix vs. Next.js vs. SvelteKit](https://blog.logrocket.com/react-remix-vs-next-js-vs-sveltekit/)
- [gatsby vs next vs remix](https://npmtrends.com/gatsby-vs-next-vs-remix)
- [The Tectonic Shift in React Ecosystem: Unearthing the Future with Next.js, Remix, Gatsby, Vite, QGP, and Astro](https://dev.to/jlarky/the-tectonic-shift-in-react-ecosystem-unearthing-the-future-with-nextjs-remix-gatsby-vite-qgp-and-astro-okl)

-----
- [Đi tìm chiếc structure hoàn hảo cho ứng dụng React](https://viblo.asia/p/di-tim-chiec-structure-hoan-hao-cho-ung-dung-react-Az45b41NZxY)
  * [Thinking in React](https://react.dev/learn/thinking-in-react)
  * [File Structure](https://legacy.reactjs.org/docs/faq-structure.html)
- [Tạo ứng dụng ReactJS bằng Create React App](https://viblo.asia/p/tao-ung-dung-reactjs-bang-create-react-app-Eb85oXr0K2G)
- [Reactjs part1: Tạo project và tìm hiểu những kiến thức cơ bản](https://viblo.asia/p/reactjs-part1-tao-project-va-tim-hieu-nhung-kien-thuc-co-ban-4P856z1a5Y3)
- [Learn ReactJS By Create React App (Part 1)](https://viblo.asia/p/learn-reactjs-by-create-react-app-part-1-924lJpLaKPM)
- [Learn ReactJS By Create React App (Part 2)](https://viblo.asia/p/learn-reactjs-by-create-react-app-part-2-RnB5pxGw5PG)
- [Các khái niệm ban đầu với Reactjs](https://viblo.asia/p/cac-khai-niem-ban-dau-voi-reactjs-gDVK2p9elLj)
- [Các khái niệm ban đầu với Reactjs (II)](https://viblo.asia/p/cac-khai-niem-ban-dau-voi-reactjs-ii-E375zkqjKGW)
- [Xây dựng một project React Js cơ bản với Webpack và Babel - Part 1](https://viblo.asia/p/xay-dung-mot-project-react-js-co-ban-voi-webpack-va-babel-part-1-4P856pJaZY3)
- []()
- []()
- [Cài đặt HTTPS ở localhost với create-react-app](https://viblo.asia/p/cai-dat-https-o-localhost-voi-create-react-app-gDVK2nXrKLj)

-----
- [Viblo React.js Essentitals](https://learn.viblo.asia/courses/reactjs-essentitals-VolejRRejN)
- [Junior vs Senior React Folder Structure - How To Organize React Projects](https://youtu.be/UUga4-z7b6s)
- [Tất cả mọi thứ bạn cần biết để bắt đầu học React](https://viblo.asia/p/tat-ca-moi-thu-ban-can-biet-de-bat-dau-hoc-react-Qbq5QAPR5D8)
- [Everything you need to know to get started in React](https://www.freecodecamp.org/news/everything-you-need-to-know-to-get-started-in-react-11311ae997cb)
- [161 Videos Khóa Học Lập Trình React.js - Redux](https://www.youtube.com/playlist?list=PLJ5qtRQovuEOoKffoCBzTfvzMTTORnoyp)
- [83 Videos học ReactJS 2022](https://www.youtube.com/playlist?list=PL_-VfJajZj0UXjlKfBwFX73usByw3Ph9Q)
- [51 Videos Tự Học React Cơ Bản Từ A đến Z Cho Người Mới Bắt Đầu](https://www.youtube.com/playlist?list=PLncHg6Kn2JT4C0enPGQPK7ZIlEoZ1ZvRy)
- [51 Videos React Season 2 với Hook - Tự Học React.JS Cơ Bản Từ Z đến A Cho Người Mới Bắt Đầu](https://www.youtube.com/playlist?list=PLncHg6Kn2JT4xzJyhXfmJ53dzwVbq-S_E)
- [31 Videos Khóa học ReactJS căn bản](https://www.youtube.com/playlist?list=PLRhlTlpDUWswrSLW_wYQCotCI3vGa8Ljz)
- [21 Videos học ReactJS](https://www.youtube.com/playlist?list=PLfKpBi4l8XymowXn9gDbqrlkenBBEf8Ps)
- [Tìm hiểu về ReactJs](https://viblo.asia/p/tim-hieu-ve-reactjs-ogBG2lo5RxnL)
- [ReactJS cho người mới bắt đầu](https://viblo.asia/p/reactjs-cho-nguoi-moi-bat-dau-LzD5dP9e5jY)
- [Thiết lập môi trường ReactJS](https://viblo.asia/p/thiet-lap-moi-truong-reactjs-E375z0R1ZGW)
- [Một số thứ cần biết trước khi tìm hiểu về ReactJS ( Phần 1 )](https://viblo.asia/p/mot-so-thu-can-biet-truoc-khi-tim-hieu-ve-reactjs-phan-1-YWOZrg0YlQ0)
- [Một số thứ cần biết trước khi tìm hiểu về ReactJS ( Phần 2 )](https://viblo.asia/p/mot-so-thu-can-biet-truoc-khi-tim-hieu-ve-reactjs-phan-2-GrLZDXXwZk0)
- [Bắt đầu với ReactJs (Phần 1)](https://viblo.asia/p/bat-dau-voi-reactjs-phan-1-3P0lPOE8Zox)
- [Bắt đầu với ReactJs (Phần 2)](https://viblo.asia/p/bat-dau-voi-reactjs-phan-2-1Je5EMGA5nL)
- [Học React.js trong 5 phút!](https://viblo.asia/p/hoc-reactjs-trong-5-phut-E375zRwq5GW)
- [Tập tọe những bước chân đầu tiên ReactJS](https://viblo.asia/p/tap-toe-nhung-buoc-chan-dau-tien-reactjs-gAm5yqpV5db)
- [Basic ReactJs (P1)](https://viblo.asia/p/basic-reactjs-p1-4dbZNDdq5YM)
- [Basic ReactJs (P2)](https://viblo.asia/p/basic-reactjs-p2-ORNZqoRG50n)
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

-----
Redux
- [Tìm hiểu về Redux trong ReactJS](https://viblo.asia/p/tim-hieu-ve-redux-trong-reactjs-GrLZDe7Olk0)
- [Redux là gì? Hiểu rõ cách hoạt động của Redux](https://200lab.io/blog/redux-la-gi/)
- [React js: Phân biệt Redux-thunk và Redux saga](https://viblo.asia/p/react-js-phan-biet-redux-thunk-va-redux-saga-eW65Gb1jlDO)
- [Tổng quan Immutability trong React và Redux!](https://viblo.asia/p/tong-quan-immutability-trong-react-va-redux-maGK77MaKj2)
- [Một số cách cập nhật state trong Redux!](https://viblo.asia/p/mot-so-cach-cap-nhat-state-trong-redux-07LKXJq2lV4)
- [Tìm hiểu Redux qua ví dụ thực tế](https://viblo.asia/p/tim-hieu-redux-qua-vi-du-thuc-te-gAm5yaNO5db)
- [Từng bước để xây dựng một ứng dụng React Redux](https://viblo.asia/p/tung-buoc-de-xay-dung-mot-ung-dung-react-redux-gGJ59jgPKX2)
- [Làm sao để áp dụng typescript vào dự án React Redux](https://viblo.asia/p/lam-sao-de-ap-dung-typescript-vao-du-an-react-redux-924lJpxXKPM)
- [Thiết lập ứng dụng React - TypeScript từ A-Z](https://viblo.asia/p/thiet-lap-ung-dung-react-typescript-tu-a-z-4dbZN1NkKYM)
- [Redux cho người mới bắt đầu - Part 1 Introduction](https://viblo.asia/p/redux-cho-nguoi-moi-bat-dau-part-1-introduction-ZjleaBBZkqJ)
- [Redux cho người mới bắt đầu - Part 2 First Project](https://viblo.asia/p/redux-cho-nguoi-moi-bat-dau-part-2-first-project-aRBvXWQZkWE)
- [Redux cho người mới bắt đầu - Part 3 Middleware](https://viblo.asia/p/redux-cho-nguoi-moi-bat-dau-part-3-middleware-3Q75wDXMKWb)
- [[Redux] Middleware Redux-saga](https://viblo.asia/p/redux-middleware-redux-saga-gGJ59X7jlX2)
- [Ứng dụng Redux của bạn mở rộng như thế nào ?](https://viblo.asia/p/ung-dung-redux-cua-ban-mo-rong-nhu-the-nao-924lJMQXZPM)
- [Tìm hiểu về Redux saga](https://viblo.asia/p/tim-hieu-ve-redux-saga-bWrZnODmlxw)
- [Tìm hiểu redux-toolkit phần 1](https://viblo.asia/p/tim-hieu-redux-toolkit-phan-1-YWOZrN3vZQ0)
- [Tìm hiểu redux-toolkit phần 2](https://viblo.asia/p/tim-hieu-redux-toolkit-phan-2-QpmlejPD5rd)
- [Redux toolkit - Refactor lại redux structure](https://viblo.asia/p/redux-toolkit-refactor-lai-redux-structure-RQqKL0pmK7z)
- [Reflux vs. Redux](https://viblo.asia/p/reflux-vs-redux-7prv31XOMKod)
- [React bỏ Redux](https://viblo.asia/p/messi-con-roi-barca-thi-code-react-ma-bo-redux-co-gi-dau-ma-bat-ngo-1VgZvrW7ZAw)
- [Quản lý state trong React bằng Mobx - Part 1](https://viblo.asia/p/quan-ly-state-trong-react-bang-mobx-part-1-OeVKB9aM5kW)
- [Quản lý state trong React bằng Mobx - Part 2](https://viblo.asia/p/mobx-quan-ly-state-trong-react-part-2-07LKXkE25V4)
- [Giới thiệu về MobX và React trong mười phút](https://viblo.asia/p/gioi-thieu-ve-mobx-va-react-trong-muoi-phut-bJzKmyrEK9N)
- [Sử dụng Reselect với React, Redux](https://viblo.asia/p/su-dung-reselect-voi-react-redux-QpmleBED5rd)
- [Using Redux Toolkit’s `createAsyncThunk`](https://blog.logrocket.com/using-redux-toolkits-createasyncthunk/)

-----
Hooks
- [Giới thiệu về Hook](https://vi.reactjs.org/docs/hooks-intro.html)
- [Giới thiệu React Hooks](https://viblo.asia/p/gioi-thieu-react-hooks-924lJRQWlPM)
- [Tản mạn về Redux và React Hooks](https://viblo.asia/p/tan-man-ve-redux-va-react-hooks-Az45br9o5xY)
- [Đôi chút về useState trong React Hooks](https://viblo.asia/p/doi-chut-ve-usestate-trong-react-hooks-07LKXpVeKV4)
- [Đôi chút về useEffect trong React Hook](https://viblo.asia/p/doi-chut-hieu-ve-useeffect-trong-reactjs-hook-RQqKLkA057z)
- [React: useMemo là gì ? khi nào nên sử dụng?](https://viblo.asia/p/react-usememo-la-gi-khi-nao-nen-su-dung-1VgZvDm95Aw)
- [Tìm hiểu về useMomo và cách sử dụng hợp lý?](https://codestus.com/posts/tim-hieu-ve-usemomo-va-cach-su-dung-hop-ly)
- [Custom Hook là gì?](https://viblo.asia/p/custom-hook-la-gi-gAm5yDo8ldb)
- [React Hooks Course - All React Hooks Explained](https://youtu.be/LlvBzyy-558)
- [React - Introducing Hooks](https://viblo.asia/p/react-introducing-hooks-QpmleERNlrd)
- [Cảm nhận về React Hooks](https://viblo.asia/p/cam-nhan-ve-react-hooks-OeVKBnPMKkW)
- [[React JS] Xử lý form đơn giản hơn với React-hook-form](https://viblo.asia/p/react-js-xu-ly-form-don-gian-hon-voi-react-hook-form-yMnKMRXNZ7P)
- [Làm thế nào để Build React Forms đơn giản với react-hook-form?](https://viblo.asia/p/lam-the-nao-de-build-react-forms-don-gian-voi-react-hook-form-Az45bLywZxY)
- [Tự build một thư viện validate form bất đồng bộ chỉ ~100 dòng code với React Hooks](https://viblo.asia/p/tu-build-mot-thu-vien-validate-form-bat-dong-bo-chi-100-dong-code-voi-react-hooks-gDVK2RDXKLj)
- [React Hook Form](https://react-hook-form.com)
- [`Series:` React up and running](https://viblo.asia/s/react-up-and-running-68Z00JJjZkG)
- [Validation với Yup trong React](https://viblo.asia/p/validation-voi-yup-trong-react-XL6lAVbJ5ek)
- [Quản lý form trong React với Formik và Yup (P1)](https://viblo.asia/p/quan-ly-form-trong-react-voi-formik-va-yup-p1-RQqKLvw4l7z)
- [Quản lý form trong React với Formik và Yup (P2)](https://viblo.asia/p/quan-ly-form-trong-react-voi-formik-va-yup-p2-m68Z002QZkG)

-----
- [The React Cheatsheet for 2020 (Phần 1)](https://viblo.asia/p/the-react-cheatsheet-for-2020-phan-1-WAyK8PY6KxX)
- [The React Cheatsheet for 2020 (Phần 2)](https://viblo.asia/p/the-react-cheatsheet-for-2020-phan-2-4P856oBAKY3)
- [The React Cheatsheet for 2020 (Phần cuối)](https://viblo.asia/p/the-react-cheatsheet-for-2020-phan-cuoi-oOVlYMxBl8W)
- [Các cách truyền data giữa các components trong ReactJS](https://viblo.asia/p/cac-cach-truyen-data-giua-cac-components-trong-reactjs-924lJjV0lPM)
- [Server-side Rendering trong React](https://viblo.asia/p/server-side-rendering-trong-react-yMnKMYozK7P)

-----
- [React.js - Những Câu Hỏi Phỏng Vấn Thường Gặp - Phần 1](https://viblo.asia/p/reactjs-nhung-cau-hoi-phong-van-thuong-gap-phan-1-Ljy5VDkbZra)
- [React.js - Những Câu Hỏi Phỏng Vấn Thường Gặp - Phần 2](https://viblo.asia/p/reactjs-nhung-cau-hoi-phong-van-thuong-gap-phan-2-bWrZno8plxw)
- [React.js - Những Câu Hỏi Phỏng Vấn Thường Gặp - Phần 3](https://viblo.asia/p/reactjs-nhung-cau-hoi-phong-van-thuong-gap-phan-3-924lJBV8lPM)
- [15 câu hỏi phỏng vấn React phổ biến](https://viblo.asia/p/15-cau-hoi-phong-van-react-pho-bien-V3m5W0PwKO7)
- [15 thư viện UI Components tốt nhất cho ReactJS](https://viblo.asia/p/15-thu-vien-ui-components-tot-nhat-cho-reactjs-maGK7pDMZj2)
- [7 lần code React của bạn bốc mùi ???](https://viblo.asia/p/7-lan-code-react-cua-ban-boc-mui-bWrZnm2QKxw)
- [5 thu viện PDF cho react](https://viblo.asia/p/top-5-thu-vien-pdf-cho-react-gGJ597bPZX2)
- [3 lời khuyên nhỏ giúp tăng preformance trong ReactJS](https://viblo.asia/p/3-loi-khuyen-nho-giup-tang-preformance-trong-reactjs-V3m5WxY8KO7)
- [Material UI in ReactJs - Xây dựng giao diện dễ dàng hơn](https://viblo.asia/p/material-ui-in-reactjs-xay-dung-giao-dien-de-dang-hon-yMnKMz8mZ7P)
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

-----
Tips & Tricks
- [`'overflow-wrap'` in React.js](https://stackoverflow.com/questions/62723863/css-overflow-wrap-does-not-work-in-react-js)
- [Validate if a start date is after an end date with Yup](https://stackoverflow.com/a/60277510)
- [Validate two input dates and max/min ranges](https://github.com/jquense/yup/issues/287#issuecomment-501481042)

-----
Debug trong ứng dụng ReactJS
- [Redux DevTools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd)
- [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
- [Logging Solutions for Node.js](https://blog.bitsrc.io/logging-solutions-for-node-js-964487f169ea)
- [Sử dụng React Developer Tools để debug React Component](https://viblo.asia/p/su-dung-react-developer-tools-de-debug-react-component-V3m5WLQWKO7)
- [Giới thiệu về Debug trong ứng dụng ReactJS](https://medium.com/velacorpblog/gi%E1%BB%9Bi-thi%E1%BB%87u-v%E1%BB%81-debug-trong-%E1%BB%A9ng-d%E1%BB%A5ng-reactjs-6c353ce1ce96)
- [Hướng dẫn Debug ứng dụng ReactJS ngay trong VS Code](https://vntalking.com/debug-react-trong-vscode.html)
- [ReactJS: Cách gỡ lỗi (debug) các component bằng React Developer Tools](https://v1study.com/reactjs-how-to-cach-go-loi-debug-cac-component-bang-react-developer-tools.html)