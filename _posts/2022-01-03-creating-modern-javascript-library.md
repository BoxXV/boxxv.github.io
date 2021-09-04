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

# Introduction

Sử dụng hệ sinh thái JavaScript hiện đại, về phần lớn, là một trải nghiệm khá tốt. Chắc chắn, có thể có quá nhiều frameworks để đếm, nhưng nếu bạn đã sử dụng JS đủ lâu, bạn đã biết chính xác gói nào mình sẽ sử dụng trong mỗi dự án mới và tệ nhất là bạn sẽ sử dụng một cái gì đó như Tạo Ứng dụng React để đi tắt đón đầu.

{% highlight js %}
// Magic! React now works
import React from 'react';
{% endhighlight %}

Mặc dù việc sử dụng các thư viện rất đơn giản, nhưng việc tạo và duy trì một thư viện có thể là một cơn ác mộng tuyệt đối. 


### The problem

Bạn cần hỗ trợ càng nhiều phiên bản của nhiều nền tảng khác nhau càng tốt để làm hài lòng người dùng của mình. Ngay cả khi bạn đang tạo một gói chỉ cho Node.js hoặc chỉ các trình duyệt, việc xuất hoạt động bình thường có thể rất khó khăn.

{% highlight js %}
// ES Modules
import myPackage from 'my-package';

// CommonJS
const myPackage = require('my-package');

// UMD
document.write('<script src="//unpkg.com/my-package"></script>');
{% endhighlight %}

Bạn muốn giảm thiểu kích thước gói cho người dùng trình duyệt, nhưng có rất ít tài nguyên mô tả cách tốt nhất để làm như vậy. Nếu thư viện của bạn nhiều hơn một trăm kilobyte, người dùng của bạn sẽ phàn nàn rằng bây giờ phải mất thêm một hoặc hai giây để tải trang web của họ trên một thiết bị di động rẻ tiền.

Bạn có thể muốn hỗ trợ người dùng TypeScript và Flow bằng cách thêm các kiểu đánh máy cho gói của mình, nhưng vẫn chưa rõ liệu bạn có nên thêm chúng vào DefiniedlyTyped / flow-typed hay không hay đưa chúng vào gói của mình. Nếu bạn không quen thuộc với TypeScript hoặc Flow, việc quản lý các loại khi thư viện của bạn phát triển có thể trở nên cực kỳ khó khăn.

Có rất nhiều mối quan tâm khác. Làm thế nào để bạn viết tài liệu tốt? Làm cách nào để bạn sửa lỗi nhanh chóng và quản lý các vấn đề khi chúng bắt đầu chồng chất? Làm thế nào để bạn khuyến khích sự đóng góp của cộng đồng? Làm thế nào để bạn làm cho thư viện của bạn dễ hiểu cho người mới? 


### Tại sao phải nghe những lời đề nghị của tôi?

Nói ngắn gọn: Tôi đã làm việc trên [Parcel](https://github.com/parcel-bundler/parcel) trong vài tháng và do đó đã tìm hiểu rất sâu về các chi tiết nhỏ của việc làm cho một gói thân thiện với người dùng gói. Tôi cũng đã xuất bản và duy trì các gói thành công khác nhau, trong đó phổ biến nhất là [thư viện nén hiệu suất cao](https://github.com/101arrowz/fflate) đạt hơn 4 triệu lượt tải xuống trong 6 tháng và hiện đang phụ thuộc vào các dự án lớn như SheetJS và Three.js. Tôi đã giải quyết nhiều vấn đề mà các tác giả thư viện mới gặp phải nhiều lần, vì vậy tôi đã quen với các cách giải quyết.


### Giải pháp

Loạt bài này sẽ mô tả những điều nên làm và không nên khi tạo một thư viện JavaScript mà người dùng của bạn sẽ thích sử dụng và bạn sẽ thích duy trì. Ngay cả khi bạn không có kế hoạch tạo thư viện sớm, những bài viết này sẽ giúp bạn tìm hiểu thêm về hệ sinh thái JavaScript và nhiều điều kỳ quặc của nó. Đừng lo lắng về việc làm theo bất kỳ thứ tự cụ thể nào; bạn sẽ không cần phải đọc bất kỳ mục nào trong loạt bài này để hiểu phần tiếp theo. Tôi hy vọng thông tin này sẽ giúp bạn thiết kế phần bổ sung tuyệt vời tiếp theo cho hệ sinh thái JS!


# Writing good code

Không thể gán một định nghĩa cố định cho "`good code`", nhưng hầu hết thời gian trong thế giới JS, chúng tôi muốn nói đến mã đó là:
- Không có lỗi
- Linh hoạt
- Có thể đọc được
- Nhanh
- Nhỏ

Theo thứ tự đó. Đối với thư viện, bạn có thể chọn chuyển khả năng đọc xuống cuối danh sách, nhưng đó có lẽ không phải là động thái tốt nhất nếu bạn muốn người khác giúp bạn duy trì dự án của mình. Bây giờ, chúng ta hãy xem từng khía cạnh của "mã tốt" bao gồm những gì.

Xin hãy nhớ rằng, đây hoàn toàn là ý kiến của riêng tôi: vui lòng bỏ qua nó hoàn toàn. Mọi người nên có định nghĩa của riêng mình về "các phương pháp hay nhất".


### Viết mã không có lỗi

![Writing bug-free code](https://boxxv.github.io/img/posts/new_bug.png "Writing bug-free code")

Sẽ không ai học cách sử dụng một thư viện mới nếu nó có quá nhiều lỗi, cho dù các khía cạnh khác của nó có tốt đến đâu. Chính nỗi sợ hãi về các lỗi ẩn và các trường hợp chưa được kiểm tra giải thích tại sao các dự án mới hơn, bất kể tốt hơn các dự án tiền nhiệm của chúng bao nhiêu, thường ít phổ biến hơn các thư viện đã thành lập.

Viết các bài kiểm tra là hoàn toàn cần thiết nếu bạn muốn giảm thiểu số lượng lỗi mà codebase của bạn mắc phải. Ngay cả những thử nghiệm thô sơ, dường như vô nghĩa cũng phục vụ hai mục đích: chúng ngăn bạn vô tình xuất bản một phiên bản bị hỏng và chúng mang lại cho người dùng cảm giác an toàn rằng ứng dụng của họ sẽ không bị hỏng khi họ cập nhật các phần phụ thuộc của mình. Bất cứ khi nào một lỗi mới được báo cáo hoặc tìm thấy, bạn sẽ muốn thêm một bài kiểm tra đã không thành công trước khi lỗi được vá để đảm bảo gói không thoái lui trong tương lai.

Có rất nhiều thư viện mà bạn có thể sử dụng để kiểm tra mã của mình. Bạn sẽ cần một trình chạy thử nghiệm và thường là một tiện ích thử nghiệm. Đối với các dự án cấp thấp hoặc nhỏ, tôi khuyên bạn nên dùng [uvu](https://github.com/lukeed/uvu) như một trình chạy thử nghiệm và `uvu/assert` là một tiện ích thử nghiệm, cả hai đều hoạt động trong Node.js hoặc trình duyệt.

{% highlight js %}
// test/index.js
import { test } from 'uvu';
import * as assert from 'uvu/assert';

// Import from the source file
import { myFunction } from '../src/index.js';

test('works on basic input', () => {
  assert.equal(
    myFunction({ a: 'b'}),
    'expected output'
  );
  assert.is(Math.sqrt(144), 12);

  // Throwing errors also works, so uvu works with
  // most third-party assertion libraries
  if (myFunction(123) != 456) {
    throw new Error('failed on 123');
  }
});

// Running node test/ runs these tests
{% endhighlight %}

Đối với các dự án lớn hơn, có lẽ bạn sẽ thích [Jest](https://jestjs.io) hơn, vì nó hỗ trợ các trường hợp sử dụng nâng cao hơn như [snapshots](https://jestjs.io/docs/snapshot-testing). Bạn không thể dễ dàng chạy thử nghiệm Jest trong trình duyệt, nhưng hầu hết các khung giao diện người dùng đều có tích hợp cho phép thử nghiệm Jest trong Node.js.

{% highlight js %}
// __tests__/index.js
import { myFunction } from '../src/index.js';

test('works on basic input', () => {
  expect(myFunction({ a: 'b'}))
    .toBe('expected output');

  expect(myFunction(123)).toMatchSnapshot();
});

// npm run jest runs the tests
{% endhighlight %}

Nếu bạn cần nhiều hơn các công cụ xác nhận cơ bản đi kèm với trình chạy thử nghiệm của mình, bạn sẽ cần chọn tiện ích thử nghiệm nào để sử dụng dựa trên những gì thư viện của bạn thực hiện. Cá nhân tôi thích bộ [Testing Library](https://testing-library.com), ví dụ: [Thư viện React Testing](https://testing-library.com/docs/react-testing-library/intro/) cho các thư viện thành phần React.

Ngoài việc kiểm tra mã của bạn, bạn nên viết thư viện của mình trong [TypeScript](https://www.typescriptlang.org). Lỗi loại là một trong những loại lỗi phổ biến nhất trong JavaScript, vì vậy việc sử dụng TypeScript hầu như luôn làm giảm thời gian phát triển và đôi khi có thể ngăn bạn xuất bản mã bị hỏng nếu bạn quên thêm một bài kiểm tra. Hơn nữa, trình biên dịch TypeScript tuyệt vời sẽ cho phép bạn tránh sử dụng một trình gói khi xuất bản gói của bạn (chúng ta sẽ đi sâu vào vấn đề này sau) và sẽ giúp hỗ trợ người dùng TypeScript và JavaScript đồng thời dễ dàng hơn nhiều. 

Dài quá; đừng đọc: Tests and (optionally) TypeScript


### Viết code linh hoạt

Người dùng tận hưởng trải nghiệm giàu tính năng. Một thư viện hoạt động rất tốt trong việc thực hiện một nhiệm vụ cụ thể có thể thu hút các tác giả thư viện khác, vì họ muốn giảm thiểu sự cồng kềnh của mã, nhưng viết mã hoạt động tốt cho các tác vụ mục đích chung sẽ mang lại nhiều phụ thuộc trực tiếp hơn.

![Writing versatile code](https://boxxv.github.io/img/posts/bnlx6qr1buiv9rp0cqcd.gif "Writing versatile code")

Không thực sự có thể đưa ra lời khuyên về những tính năng bạn nên thêm vào thư viện của mình vì tất cả phụ thuộc vào những gì bạn đang cố gắng đạt được. Tuy nhiên, tôi có thể đưa ra lời khuyên về cách viết mã theo cách cho phép dễ dàng mở rộng trong tương lai. Dưới đây là một vài gợi ý:

- Tránh tạo các hàm sử dụng một lần, ngắn trừ khi bạn có kế hoạch sử dụng lại chúng trong tương lai gần. Việc chia nhỏ một chức năng có thể làm cho mã trông đẹp hơn, nhưng nó khiến việc duy trì và theo dõi các thay đổi đối với mã đó trở nên khó khăn hơn. Bạn có thể bỏ qua điều này nếu chức năng sử dụng một lần rất dài. 

{% highlight js %}
// Don't do this:
const rand = (a, b) => {
  // If you decide to change this in the future (e.g. adding
  // a third argument for random number generation) you will
  // need to modify two functions instead of one.
  const randfloat = Math.random();
  return a + Math.floor(randfloat * (b - a));
}

const randArrayInRange = (len, a, b) => {
  const arr = new Array(len);
  for (let i = 0; i < len; ++i) {
    arr[i] = rand(a, b);
  }
  return arr;
}

// Use a single function, but make sure to add comments where
// you would otherwise have called a helper function.
const randArrayInRange = (len, a, b) => {
  const arr = new Array(len);
  for (let i = 0; i < len; ++i) {
    // Generate random number at least 0, less than 1
    const randfloat = Math.random();
    // Move randfloat into [a, b) range
    arr[i] = a + Math.floor(randfloat * (b - a));
  }
  return arr;
}
{% endhighlight %}

- Thêm nhận xét `Add TODO` bất cứ khi nào bạn nhận thấy điều gì đó có thể trở thành vấn đề trong tương lai. Làm như vậy sẽ giúp bạn tiết kiệm thời gian khi bạn quyết định thêm một tính năng mà ban đầu không thành công do các quyết định trước hoặc sơ suất.

{% highlight js %}
const numPostsOnPage = async page => {
  // TODO: "page" may not be the name of the argument in the
  // calling function - can be ambiguous
  if (typeof page != 'number') {
    throw new TypeError('page must be a number');
  }
  const resp = await fetch(`//example.com/page/${page}`);
  const posts = await resp.json();
  return posts.length;
}

const example = (x, y) => {
  if (typeof x != 'number') {
    throw new TypeError('x must be a number');
  }
  // TODO: This is an async function, so a type error for y
  // will not throw but will reject the returned Promise,
  // but a type error for x throws
  return x * numPostsOnPage(y);
}

// Because of the TODOs, in the future, you'll easily
// find why the type error for y isn't caught here
try {
  example(0, 'mistake');
} catch(e) {
  console.error(`Got error: ${e}`);
}
{% endhighlight %}

- Sử dụng tài liệu cho mã mà bạn sẽ cân nhắc sửa đổi trong tương lai. Ngay cả khi mã chỉ được sử dụng trong nội bộ, điều này sẽ giúp sửa đổi dễ dàng hơn và sẽ giúp các cộng tác viên chẩn đoán lỗi dễ dàng hơn.

{% highlight js %}
// TODO: in the future, consider changing the following
// recursive function to be more efficient by fetching
// all users simultaneously with Promise.all()

// gets the names of all users
const getUserNames = async max => {
  // Recursive base case - no user 0 exists
  if (!max) return [];
  const res = await fetch(`/users/${max}`);
  // Data for user ID # max
  const userData = await res.json();
  // Prepend data for users with lower IDs
  return (await getUserNames(max - 1)).concat(userData);
}
{% endhighlight %}

Dài quá; đừng đọc: Giữ cho codebase của bạn có thể bảo trì được và mọi thứ sẽ vào đúng vị trí


### Viết code có thể đọc được

Mã có thể đọc được rất quan trọng đối với khả năng bảo trì và nhận được sự trợ giúp từ cộng đồng. Không ai muốn dành một giờ để nghiên cứu cơ sở mã của bạn chỉ để hiểu mỗi chức năng làm gì; viết mã dễ đọc là một khởi đầu tốt.

Bước này cực kỳ đơn giản. Hai điều bạn cần làm là:
- Sử dụng tài liệu nội tuyến đủ (nhưng không quá nhiều) cho các hàm, biến, v.v.
- Ngoài ra, hãy sử dụng các tên biến / hàm tự lập tài liệu cho mã giao diện người dùng (tức là những gì được xuất). Một cách tối ưu, JSDoc sạch sẽ đi kèm với mỗi khai báo (sử dụng JSDoc/TSDoc sẽ rất hữu ích, như chúng ta sẽ thấy trong một bài viết trong tương lai).

{% highlight js %}
// The short names used here are OK because they are
// documented and because the names make sense

// zip compression worker
// send string -> Uint8Array mapping
// receive Uint8Array ZIP data
const zwk = new Worker('./zip-worker.js');

// read file to [filename, Uint8Array]
const readFile = file => new Promise((resolve, reject) => {
  // file reader: File to ArrayBuffer
  const fr = new FileReader();
  fr.onload = () => {
    // fr.result is ArrayBuffer
    resolve([file.name, new Uint8Array(fr.result)]);
  }
  fr.onerror = () => {
    reject(fr.error);
  }
  fr.readAsArrayBuffer(file);
});

/**
 * Zips the provided files
 * @param files {File[]} The files to create a ZIP from
 * @returns {Promise} A promise with a Blob of the ZIPped data
 */
export async function zipFiles(files) {
  // file entries - Array of [filename, data]
  const entries = await Promise.all(files.map(readFile));
  // transferable list - neuters data passed in but reduces
  // execution time
  const tfl = fileEntries.map(([, dat]) => dat.buffer);
  // filename -> data mapping
  const fileData = fileEntries.reduce((obj, [fn, dat]) => {
    obj[fn] = dat;
    return obj;
  }, {});

  return new Promise((resolve, reject) => {
    zwk.onmessage = ({ data }) => resolve(data);
    zwk.onerror = ({ error }) => reject(error);
    zwk.postMessage(fileData, tfl);
  });
}
{% endhighlight %}

Dài quá; đừng đọc: Make it self-documenting or document it yourself


### Viết code nhanh

Đây không phải là một bài báo về hiệu suất, vì vậy tôi sẽ không đi sâu quá nhiều ở đây.

Đối với mã cấp thấp (tức là bất kỳ thứ gì liên quan đến xoắn bit, mã hóa nhị phân, v.v.), bạn sẽ muốn sử dụng trình biên dịch trong Node.js (trình chỉnh sửa mã của bạn [có thể có hỗ trợ](https://stackoverflow.com/a/61585758/10930232)) hoặc Chrome (xem [bài viết này](https://developer.chrome.com/docs/devtools/evaluate-performance/)). Hướng dẫn này về [hiệu suất trong động cơ V8](https://github.com/thlorenz/v8-perf) có thể hữu ích.

Đối với các chương trình cấp cao hơn như thư viện và khung giao diện người dùng, việc tối ưu hóa vi mô là vô nghĩa. Tìm kiếm các vấn đề kiến trúc quy mô lớn với thiết kế của bạn (ví dụ: cần gọi `document.getElementById` nhiều lần mỗi giây do giới hạn trong DOM ảo của bạn). Trình biên dịch của Chrome cũng sẽ giúp xác định xem vấn đề có nằm ở JavaScript, kết xuất hay thứ gì khác của bạn hay không.

Dài quá; đừng đọc: Nếu phần này quá dài, nó có thể không phù hợp với bạn.


### Viết code nhỏ

Một lần nữa, bài viết này không có ý nghĩa về tối ưu hóa, vì vậy tôi sẽ không thảo luận nhiều ở đây, nhưng hãy cho tôi biết trong phần nhận xét nếu bạn muốn viết chi tiết hơn về cách loại bỏ mọi điểm giảm hiệu suất cuối cùng mã của bạn.

Mã nhỏ có thể góp phần vào cả khả năng đọc và hiệu suất (tức là thời gian tải trong trình duyệt). Tuy nhiên, nếu bạn chỉ viết một thư viện cho Node.js, thì mã nhỏ hoàn toàn không phải là vấn đề đáng lo ngại trừ khi bạn có quá nhiều mã khiến cơ sở mã của bạn khó hiểu. Nói chung, mã nhỏ là khía cạnh ít quan trọng nhất của một thư viện tốt.

Nếu bạn thực sự muốn thu nhỏ kích thước của mã gói của mình, cách tốt nhất là tránh sử dụng các phần tóm tắt được tạo sẵn cho những thứ bạn có thể triển khai theo cách thủ công. Ví dụ: nếu bạn cần lấy thời lượng của một bài hát trong tệp MP3 trong trình duyệt, không sử dụng [music-metadata](https://www.npmjs.com/package/music-metadata), hãy [tự làm điều đó](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/duration). Mã bạn cần viết có thể khoảng vài trăm byte, vì vậy bạn sẽ tiết kiệm được [63 kB](https://bundlephobia.com/package/music-metadata-browser@2.2.6).

Dài quá; đừng đọc: Tự làm mọi thứ










-----
Tham khảo:
- [Creating a modern JS library: Introduction](https://dev.to/101arrowz/creating-a-modern-js-library-introduction-1a0c)
- [Creating a modern JS library: Writing good code](https://dev.to/101arrowz/creating-a-modern-js-library-writing-good-code-170a)
- [Creating a modern JS library: TypeScript and Flow](https://dev.to/101arrowz/creating-a-modern-js-library-typescript-and-flow-3ge)
- [Creating a modern JS library: package.json and dependencies](https://dev.to/101arrowz/creating-a-modern-js-library-package-json-and-dependencies-5ek9)