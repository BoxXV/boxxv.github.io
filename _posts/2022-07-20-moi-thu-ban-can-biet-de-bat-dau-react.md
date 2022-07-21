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

React là thư viện Front End phổ biến nhất hiện nay. Nhưng bắt đầu học React có thể đôi lúc gặp khó khăn. Gồm những Component, states, props and functional programming. Bài viết này cố gắng giải quyết vấn đề này, bằng cách chỉ ra cho bạn cách bắt đầu tốt và dễ dàng trong React. Vì vậy, không lãng phí thêm thời gian nữa, hãy tới luôn nào.

### Môi Trường

Chúng ta sẽ sử dụng một tệp HTML đơn giản trong bài viết này. Chỉ cần include các thẻ scritpt sau trong phần head file HTML của bạn.

```html
<script src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/6.26.0/babel.js"></script>
```

### Components

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


### JavaScript Syntax Extension (JSX)







-----
Tham khảo:
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


- [15 thư viện UI Components tốt nhất cho ReactJS](https://viblo.asia/p/15-thu-vien-ui-components-tot-nhat-cho-reactjs-maGK7pDMZj2)
- [15 câu hỏi phỏng vấn React phổ biến](https://viblo.asia/p/15-cau-hoi-phong-van-react-pho-bien-V3m5W0PwKO7)
- [7 lần code React của bạn bốc mùi ???](https://viblo.asia/p/7-lan-code-react-cua-ban-boc-mui-bWrZnm2QKxw)
- [5 thu viện PDF cho react](https://viblo.asia/p/top-5-thu-vien-pdf-cho-react-gGJ597bPZX2)
- [3 lời khuyên nhỏ giúp tăng preformance trong ReactJS](https://viblo.asia/p/3-loi-khuyen-nho-giup-tang-preformance-trong-reactjs-V3m5WxY8KO7)
- [Tìm hiểu Props và State trong React](https://viblo.asia/p/tim-hieu-props-va-state-trong-react-GrLZD8RBZk0)
- [Sự khác nhau giữa Props và State trong ReactJS](https://viblo.asia/p/su-khac-nhau-giua-props-va-state-trong-reactjs-OeVKBvrJKkW)
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