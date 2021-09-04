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


### That's it!

Vào cuối ngày, thư viện hữu ích như thế nào phụ thuộc nhiều nhất vào mức độ khó khăn khi giải quyết vấn đề mà nó giải quyết. Không ai muốn viết một thuật toán SHA-256 từ đầu, vì vậy ngay cả những [thư viện mật mã không rõ ràng cũng rất phổ biến](https://www.npmjs.com/package/sha.js). Mặt khác, các thư viện thao tác DOM rất tốn kém, vì vậy ngay cả một số [khung giao diện người dùng tuyệt vời cũng nhận được rất ít lượt tải xuống](https://www.npmjs.com/package/solid-js). Tuy nhiên, mã tốt được đánh giá rất cao cho dù có bao nhiêu người đang sử dụng nó. Tôi hy vọng những lời khuyên này hữu ích. Cảm ơn vì đã đọc!


# TypeScript và Flow

Trước khi tìm hiểu những gì bạn cần để hỗ trợ TypeScript và Flow, chúng ta hãy nghĩ về lý do tại sao mọi người sử dụng chúng ngay từ đầu. Vấn đề chính là JavaScript là một ngôn ngữ được gõ động, yếu, nhưng nhiều lập trình viên muốn gõ tĩnh (và đôi khi là mạnh).

Nhập động có nghĩa là không có kiểu nào tại thời điểm biên dịch. Điều này có nghĩa là bạn có thể vô tình thêm một hàm và một số, nhưng bạn sẽ không biết cho đến khi chạy. Rất ít ngôn ngữ được thông dịch và biên dịch JIT hỗ trợ nhập tĩnh. 

{% highlight js %}
// There is no way to declare a type for a and b, even
// though a clearly needs to be a function
const myFunction = (a, b) => {
  return a(b);
}

// This function call does not throw a type error
// until it is executed, but a statically typed
// language would not compile.

// Think of a compile-time type error like a syntax
// error. Your code doesn't need to run for a type
// error to occur in statically typed languages.
const myResult = myFunction(
  { you: 'should not' },
 'be able to do this'
);
{% endhighlight %}

Ngược lại, một ngôn ngữ như C sẽ không bao giờ cho phép những thứ như thế này:

{% highlight js %}
#include <stdio.h>

// This throws a compile time warning (or error,
// depending on your configuration)
const char* example() {
  // Not a string literal, so the program does
  // not compile and you cannot run it
  return 20;
}

int main() {
  printf("%s", example());
  return 0;
}
{% endhighlight %}

Đánh máy yếu có nghĩa là JavaScript sẽ không gặp crash/throw khi thực hiện một thao tác bất hợp pháp và thay vào đó sẽ cố gắng làm cho thao tác đó hoạt động. Loại hành vi này là nguồn gốc của [nhiều WTF](https://github.com/denysdovhan/wtfjs) của các nhà phát triển JS.

{% highlight js %}
// This is perfectly valid JavaScript
const weirdAddition = [] + [];
console.log(weirdAddition); // ""

// That worked because the engine implicitly called
// [].toString() when it saw the addition operator.

// An empty array gives an empty string, hence the
// result is "" + "" = "".
{% endhighlight %}

Hành vi này hoàn toàn trái ngược với Python: bất kỳ hoạt động không hợp lệ nào sẽ ngay lập tức gây ra ngoại lệ. Ngay cả khi thêm một chuỗi và một số cũng sẽ không thành công và yêu cầu bạn chuyển đổi số thành chuỗi trước.

{% highlight js %}
a = '9 + 10 = '
b = 9 + 10

# This fails: you must explicitly cast b to string
print(a + b)

# Only this works
print(a + str(b))
{% endhighlight %}

Mặc dù hệ thống kiểu hầu như không tồn tại của JavaScript giúp các lập trình viên linh hoạt hơn, nhưng nó cũng là nguồn gốc của nhiều lỗi. Đang gõ động và gõ yếu, bạn sẽ không gặp lỗi nếu bạn mắc lỗi với các kiểu. Do đó, các lập trình viên muốn có một giải pháp để thêm các loại vào JavaScript.

Nhập TypeScript: một phần mở rộng cho JavaScript bổ sung hỗ trợ cú pháp cho các kiểu đánh máy, trình biên dịch và hỗ trợ tự động hoàn thành đáng kinh ngạc mà trước đây chưa từng có trong JavaScript.

{% highlight js %}
// TypeScript accepts reasonable implicit conversions
const myFunction = (x: number) => 'hello ' + x;

// This will not compile, even with an explicit return type
// Adding arrays is not a reasonable use of dynamic typing
const myOtherFunction = (
  x: string[],
  y: string[]
): string => x + y;

// This will fail at compile time as well, since the first
// parameter of myFunction must be a number
myFunction('hello');
{% endhighlight %}

Tôi thực sự khuyên bạn nên sử dụng TypeScript trong thư viện của mình vì nó biên dịch sang bất kỳ phiên bản JavaScript nào, thậm chí sớm nhất là ES3. Bạn có thể hỗ trợ các môi trường JS cũ và hiện đại, hỗ trợ cả người dùng JavaScript và TypeScript, đồng thời ngăn chặn các lỗi trong mã của bạn bằng cách sử dụng TypeScript. Cho dù bạn quyết định sử dụng TS hay không, việc hỗ trợ người dùng TS có thể gây nhầm lẫn, vì vậy hãy đọc tiếp.


### Hỗ trợ TypeScript từ một dự án TypeScript

Nếu thư viện của bạn được viết bằng TypeScript, bạn có thể tự động tạo cả mã JavaScript (để hỗ trợ tất cả người dùng) và tệp khai báo TypeScript (thêm các loại TypeScript vào mã JavaScript). Bạn sẽ hầu như không bao giờ cần xuất các tệp TypeScript trong gói của mình, trừ khi tất cả người dùng của bạn sẽ sử dụng TypeScript (tức là cho một cái gì đó như [typegoose](https://github.com/typegoose/typegoose)).

Điều chính bạn cần làm là bật [`declaration`](https://www.typescriptlang.org/tsconfig#declaration) tùy chọn biên dịch trong [tsconfig.json](https://www.typescriptlang.org/tsconfig#declaration).

{% highlight js %}
{
  "compilerOptions": {
    "outDir": "lib/",
    // This is the relevant option
    // The types you need will be exported to lib/
    "declaration": true
  }
}
{% endhighlight %}

Nếu bạn không sử dụng trình biên dịch TypeScript để xây dựng mã của mình (bằng cách sử dụng tùy chọn `noEmit`), bạn cũng sẽ muốn sử dụng `emitDeclarationOnly`.

{% highlight js %}
{
  "compilerOptions": {
    "outDir": "lib/",
    "declaration": true,
    // Remove noEmit and replace it with this
    "emitDeclarationOnly": true
  }
}
{% endhighlight %}

Sau đó, trong `package.json`, hãy sử dụng trường `"types"` để bao gồm các loại của bạn.

{% highlight js %}
{
  "main": "lib/index.js",
  "types": "lib/index.d.ts"
}
{% endhighlight %}


### Hỗ trợ TypeScript từ một dự án JavaScript

Cũng giống như với một dự án TypeScript, bạn cần xuất cả tệp JavaScript và tệp khai báo TypeScript để làm cho mã của bạn có thể sử dụng được cho cả người dùng TypeScript và JavaScript.

Việc tạo và duy trì tệp khai báo bằng tay có thể khó khăn, vì vậy bạn sẽ muốn đảm bảo [đọc tài liệu](https://www.typescriptlang.org/docs/handbook/declaration-files/introduction.html) trên tệp khai báo. Nếu bạn gặp khó khăn với cú pháp, hãy thử xem các cách đánh máy cho các gói phổ biến như [Express](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/express/index.d.ts).

Trước tiên, bạn sẽ cần tìm hiểu xem các tệp bạn xuất từ gói của mình có sử dụng Mô-đun CommonJS hay ES hay không. CommonJS trông như thế này: 

{% highlight js %}
// module.exports or exports indicate CommonJS
module.exports = {
  a: 1,
  b(c, op) {
    if (op == 'sq') return c ** 2;
    if (op == 'sqrt') return Math.sqrt(c);
    throw new TypeError('invalid operation')
  }
}

// For exporting one thing:
module.exports = 'hello';
{% endhighlight %}

Ngược lại, các Mô-đun ES trông như thế này:

{% highlight js %}
// The export keyword indicates ESM
export const a = 1;
export function b(c, op) {
  if (op == 'sq') return c ** 2;
  if (op == 'sqrt') return Math.sqrt(c);
  throw new TypeError('invalid operation')
}

// export default for one thing
export default 'hello';
{% endhighlight %}

Nếu bạn xuất cả hai (chúng ta sẽ tìm hiểu cách thực hiện việc này trong một bài viết trong tương lai), hãy chỉ tạo tệp khai báo bằng ESM vì các khai báo CommonJS hầu như luôn có thể được trình biên dịch TypeScript suy ra từ phiên bản ESM.

Nếu bạn đang sử dụng CommonJS, hãy sử dụng không gian tên để đóng gói gói của bạn. Tối ưu, bạn cũng sẽ xuất các kiểu và giao diện giúp việc sử dụng TypeScript thuận tiện hơn. 

{% highlight js %}
// index.d.ts

// Everything in the namespace is exported

// If you want to use a type within the declaration
// file but not export it, declare it outside
declare namespace MyPackage {
  const a: number;
  // This type prevents TypeScript users from
  // using an invalid operation
  type MyOp = 'sq' | 'sqrt';
  function b(c: number, op: MyOp): number;
}

export = MyPackageName;

// For a single export:
declare const myPackage: string;
export = myPackage;
{% endhighlight %}

Ngoài ra, nếu bạn đang sử dụng ESM, bạn không cần (và không nên sử dụng) một không gian tên; xuất như bạn làm trong JavaScript.

{% highlight js %}
export const a: number;
export type MyOp = 'sq' | 'sqrt';
export function b(c: number, op: MyOp): number;

// For a single export:
declare const myPackage: string;
export default myPackage;
{% endhighlight %}

Bây giờ bạn đã có một index.d.ts hoàn chỉnh, bạn có thể thực hiện một trong hai việc. Bạn có thể:
- Thêm nó vào gói NPM của riêng bạn, như với phiên bản TypeScript
- Thêm nó vào kho lưu trữ [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped) để tự động nhận gói `@types/your-package-name`

Tôi khuyên bạn nên thêm khai báo vào gói NPM vì điều đó làm giảm lượng thời gian và công sức cần thiết để cập nhật gói của bạn, cũng như mang lại cho bạn sự linh hoạt hơn liên quan đến các tính năng TypeScript mà bạn có thể sử dụng và loại bỏ nhu cầu thêm các bài kiểm tra.

Tuy nhiên, nếu bạn có nhiều phụ thuộc có các kiểu bạn cần bao gồm (ví dụ: nếu bạn xuất một thành phần React, bạn phụ thuộc vào các kiểu gõ React), bạn cần thêm `@types/dependency-name` vào các `dependencies` của mình, không phải `devDependencies`, và điều đó bổ sung phình to cho người dùng cuối của bạn không sử dụng TypeScript. Trong những trường hợp đó, tốt hơn hết là bạn nên xuất bản lên DefiniedlyTyped.


### What about Flow?

Quá trình hỗ trợ người dùng Flow cực kỳ giống với quá trình của TypeScript. Thay vì thêm tệp định nghĩa vào `"types"` trong `package.json`, hãy tạo tệp `.js.flow` cùng với mọi tệp `.js` đang được xuất (ví dụ: nếu bạn xuất `lib/index.js`, hãy đảm bảo tạo `lib/index.js.flow` với các định nghĩa). Xem [tài liệu](https://flow.org/en/docs/libdefs/creation/) về cách tạo định nghĩa như vậy. Nếu bạn muốn tự mình hỗ trợ Flow, đừng xuất bản lên [flow-type](https://github.com/flow-typed/flow-typed); nó chủ yếu dành cho các thành viên cộng đồng tạo ra các loại của riêng họ cho các gói của bên thứ ba và xuất bản chúng ở đó.

{% highlight js %}
// @flow

// If this is an ES Module:
declare export function sayHello(to: string): void;

// Alternatively, if this is CommonJS:
declare module.exports: {
  sayHello(to: string): void;
}
{% endhighlight %}

Nếu bạn đang viết thư viện của mình bằng Flow, bạn có thể sử dụng [công cụ xây dựng](https://www.npmjs.com/package/flow-copy-source) để tự động hóa quy trình. Ngoài ra, sử dụng [flowgen](https://github.com/joarwilk/flowgen) để chỉ cần duy trì tệp định nghĩa TypeScript và tự động hóa quy trình hỗ trợ Flow. Trong mọi trường hợp, Flow là khá hiếm ngày nay; chỉ hỗ trợ TypeScript có lẽ sẽ không bao giờ là một vấn đề. 


# package.json và dependencies

`Package.json` của bạn là một trong những tệp quan trọng nhất trong dự án của bạn. Nó xử lý các phụ thuộc, xuất, lập phiên bản, đặt tên, v.v. `package.json` bao gồm tất cả siêu dữ liệu mà người dùng cần để sử dụng thư viện của bạn một cách hiệu quả. Do đó, điều quan trọng là bạn phải tạo `package.json` đúng cách; nếu bạn không làm vậy, khoảng một nửa số báo cáo lỗi của bạn sẽ là các vấn đề liên quan đến nhập, phụ thuộc không khớp, v.v.

Hãy xem qua các trường mà một `package.json` điển hình sẽ chứa. Chúng tôi sẽ tạo một gói mẫu để mã hóa lại dữ liệu hoặc chuỗi UTF-8 thành định dạng "Catlang" hư cấu.

#### `name` (required)

Tên thư viện của bạn. Ngay cả khi bạn có kiểu ưa thích, quy ước là sử dụng tất cả các chữ cái thường và dấu gạch ngang để phân tách các từ.

Nếu bạn đang tạo một nhánh của một gói hiện có, đừng thêm số vào cuối: mô tả những gì bạn đã thay đổi hoặc nếu điều đó quá khó, hãy diễn đạt cùng một ý tưởng bằng các từ khác nhau.

Lựa chọn tên kém:

{% highlight js %}
{
  "name": "EncodeInCatlang2",
}
{% endhighlight %}

Lựa chọn tốt về tên:

{% highlight js %}
{
  "name": "encode-in-catlang"
}
{% endhighlight %}

Nếu những điều trên đã được thực hiện:

{% highlight js %}
{
  "name": "catlang-encoder"
}
{% endhighlight %}

#### `version` (required)

Phiên bản hiện tại của gói. Bạn sẽ thay đổi điều này mỗi khi bạn muốn xuất bản một phiên bản mới của gói của mình. Cố gắng làm theo cách lập phiên bản ngữ nghĩa (thêm chi tiết về điều này sau). Đề xuất của tôi như sau:

- Khi bạn lần đầu tiên tạo một gói, hãy sử dụng `0.0.1`.
- Bất cứ khi nào bạn sửa một lỗi, bạn đều muốn có một bản sửa đổi "patch". Tăng chữ số cuối cùng.
    + `1.0.1` → `1.0.2`
    + `3,4,9` → `3,4,10`
- Bất cứ khi nào bạn thêm một tính năng mới, không chấp nhận nữa (tức là không khuyến khích) một tính năng hiện có hoặc làm bất kỳ điều gì khác không phá vỡ mã mà trước đây đã hoạt động tốt, bạn muốn có một bản sửa đổi "minor". Tăng chữ số thứ hai đến chữ số cuối cùng và đặt chữ số cuối cùng thành 0.
    + `1.0.1` → `1.1.0`
    + `3.9.0` → `3.10.0`
    + `0,3,5` → `0,3,6` *
- Bất cứ khi nào bạn không chấp nhận (tức là xóa) một tính năng hiện có, thay đổi hành vi của một thứ gì đó hoặc làm bất cứ điều gì có thể phá vỡ mã hoạt động tốt trên phiên bản trước, bạn phải sử dụng bản sửa đổi "major". Tăng chữ số đầu tiên và đặt hai chữ số còn lại bằng 0.
    + `1.1.3` → `2.0.0`
    + `10.1.3` → `11.0.0`
    + `0,3,5` → `0,4,0` *
    + `0.0.3` → `0.0.4` *

Lưu ý các ví dụ bằng dấu hoa thị. Đối với các phiên bản dưới `1.0.0`, không thể sửa đổi bản vá và hai loại còn lại chuyển xuống; tăng dần chữ số thứ hai đến chữ số cuối cùng là chữ số chính và chữ số cuối cùng là chữ số phụ. Đối với các phiên bản dưới `0.1.0`, điều này thậm chí còn nghiêm trọng hơn, vì mỗi phiên bản lỗi đều là một phiên bản chính mới.

Đây là lý do tại sao cập nhật từ `0.0.X` lên `0.1.0` và từ `0.X.X` lên `1.0.0` là những gì tôi muốn gọi là các bản sửa đổi "trưởng thành"; chúng thay đổi hoàn toàn ý nghĩa của từng chữ số. Phương pháp hay, hãy cố gắng giảm số lượng phiên bản chính bạn tạo sau `1.0.0`, nhưng hãy sử dụng nhiều phiên bản nhỏ và bản vá tùy thích.

Theo hướng dẫn ký hiệu, các phiên bản ngữ nghĩa thường được thêm tiền tố "v" bên ngoài `package.json`. Ví dụ: khi đề cập đến phiên bản `1.2.3` trong vấn đề GitHub, hãy nói "v1.2.3".

Bạn cũng có thể muốn lưu ý rằng các phiên bản ứng viên alpha, beta và phát hành được hỗ trợ bằng cách lập phiên bản ngữ nghĩa. Ví dụ: `1.0.0-alpha.1`, `2.2.0-beta.4`, `0.3.0-rc.0`. Thông thường, phiên bản vá lỗi không được đặt cho các phiên bản phát hành trước này và chúng không được người quản lý gói tải xuống trừ khi người dùng yêu cầu phiên bản phát hành trước.

Điều cuối cùng: NPM coi các gói dưới v1.0.0 là không ổn định và xếp hạng chúng thấp hơn trong tìm kiếm. Nếu bạn muốn tăng nhanh điểm số tìm kiếm, hãy làm cho thư viện của bạn ổn định!

Hãy cập nhật `package.json` của chúng tôi:

{% highlight js %}
{
  "name": "catlang-encoder",
  "version": "0.0.1"
}
{% endhighlight %}

#### `description` (strongly recommended)

Mô tả ngắn gọn về những gì gói của bạn làm. Ngay cả khi tên là tự giải thích, nó không có hại để lặp lại chính mình. Mô tả được sử dụng cho các kết quả tìm kiếm trong NPM, vì vậy hãy đảm bảo làm nổi bật các tính năng chính nhất của thư viện. 

{% highlight js %}
{
  "name": "catlang-encoder",
  "version": "0.0.1",
  "description": "Fast Unicode to Catlang converter"
}
{% endhighlight %}


#### `author` (strongly recommended)

Tên (và tùy chọn email và trang web) của tác giả của gói. Tối ưu, bạn sẽ sử dụng tên đầy đủ của mình ở đây, nhưng nếu bạn không thoải mái khi làm như vậy, bí danh trực tuyến của bạn sẽ đủ dùng. Trường có thể có một trong hai định dạng: 

{% highlight js %}
"Your Name <youremail@yourdomain.com> (https://yoursite.com)"
{% endhighlight %}

hoặc

{% highlight js %}
{
  "name": "Your Name",
  "email": "youremail@yourdomain.com",
  "url": "https://yoursite.com"
}
{% endhighlight %}

Email và trang web là tùy chọn, nhưng bạn phải thêm tên hoặc bí danh của mình.

`package.json` mới:

{% highlight js %}
{
  "name": "catlang-encoder",
  "version": "0.0.1",
  "description": "Fast Unicode to Catlang converter",
  "author": "Cat <cat@gmail.com>"
}
{% endhighlight %}

#### `license` (strongly recommended)

Giấy phép mà mã thư viện của bạn có thể được sử dụng. Chúng tôi sẽ đề cập đến việc cấp phép nhiều hơn trong một bài viết khác, nhưng hiện tại, ít nhất bạn nên biết cú pháp.

Nếu bạn đang sử dụng một giấy phép phổ biến (chẳng hạn như MIT, ICS, BSD, GPL, Apache, v.v.), bạn có thể sử dụng số nhận dạng của nó, bạn có thể tìm thấy trong [danh sách này](https://spdx.org/licenses/). Cố gắng chọn một giấy phép từ danh sách đó, nhưng nếu bạn không thể, hãy đề cập đến tệp chứa giấy phép của bạn để thay thế: 

{% highlight js %}
"SEE LICENSE IN LICENSE.md"
{% endhighlight %}

Nếu bạn muốn phân phối thư viện của mình theo nhiều giấy phép, bạn có thể sử dụng các biểu thức `OR` và `AND` với dấu ngoặc đơn. Nếu bạn muốn chỉ định một ngoại lệ trong một số giấy phép, hãy sử dụng từ khóa `WITH`.

{% highlight js %}
"(Apache-2.0 OR MIT)"
"(GPL-3.0-only WITH Bison-exception-2.2)"
{% endhighlight %}

Nếu bạn không biết gì về cấp phép và chỉ muốn tự do phân phối mã của mình, "MIT" là một lựa chọn an toàn.

`package.json` mới:

{% highlight js %}
{
  "name": "catlang-encoder",
  "version": "0.0.1",
  "description": "Fast Unicode to Catlang converter",
  "author": "Cat <cat@gmail.com>",
  "license": "MIT"
}
{% endhighlight %}


#### `keywords` (khuyến khích)

Các từ khóa để liên kết với thư viện của bạn trong tìm kiếm NPM. Đây là một cách để đưa gói của bạn vào các tìm kiếm không bao gồm bất kỳ từ nào trong trường `name` hoặc `description`. Mục đích của trường `keywords` là ngăn chặn spam từ khóa trong mô tả hoặc tiêu đề, nhưng bạn vẫn không nên sử dụng các thuật ngữ không liên quan trong các từ khóa.

Thêm từ khóa vào `package.json`:

{% highlight js %}
{
  "name": "catlang-encoder",
  "version": "0.0.1",
  "description": "Fast Unicode to Catlang converter",
  "author": "Cat <cat@gmail.com>",
  "keywords": [
    "catlang",
    "cat language",
    "catlang converter",
    "high performance"
  ],
  "license": "MIT"
}
{% endhighlight %}


#### `homepage` (khuyến khích)

Trang web cho dự án của bạn. Đây có thể là một trang tài liệu, trang ví dụ, v.v. Nếu bạn có một trang web bao gồm thông tin về thư viện của mình, thậm chí là một bài đăng trên blog, hãy sử dụng nó tại đây. Tránh sử dụng liên kết đến mã nguồn của bạn (tức là kho lưu trữ GitHub của bạn) trừ khi bạn hoàn toàn không có trang web nào khác để liên kết đến. 

{% highlight js %}
{
  "name": "catlang-encoder",
  "version": "0.0.1",
  "description": "Fast Unicode to Catlang converter",
  "author": "Cat <cat@gmail.com>",
  "keywords": [
    "catlang",
    "cat language",
    "catlang converter",
    "high performance"
  ],
  "homepage": "https://catlangencoder.js.org",
  "license": "MIT"
}
{% endhighlight %}


#### `repository` (khuyến khích)

Thông tin về kho lưu trữ. Giả sử bạn đang lưu trữ mã nguồn của mình trên hệ thống kiểm soát phiên bản (nếu không, bạn chắc chắn nên làm như vậy), hãy sử dụng một đối tượng có `type` loại và `url`:

{% highlight js %}
{
  "type": "git",
  "url": "https://domain.com/your-name/your-library.git"
}
{% endhighlight %}

Có một số cách viết tắt, chẳng hạn như chỉ sử dụng URL và để NPM đoán loại kho lưu trữ là gì, nhưng tôi khuyên bạn không nên làm điều này vì mục đích rõ ràng.

Nếu thư viện của bạn là một phần của monorepo, bạn có thể chỉ định trường con `directory` để biểu thị thư mục con chứa gói. Nếu bạn không sử dụng monorepo hoặc không biết monorepo là gì, đừng sử dụng `directory`.

{% highlight js %}
{
  "name": "catlang-encoder",
  "version": "0.0.1",
  "author": "Cat <cat@gmail.com>",
  "description": "Fast Unicode to Catlang converter",
  "keywords": [
    "catlang",
    "cat language",
    "catlang converter",
    "high performance"
  ],
  "homepage": "https://catlangencoder.js.org",
  "repository": {
    "type": "git",
    "url": "https://github.com/cat/catlang",
    "directory": "js/packages/catlang-encoder"
  },
  "license": "MIT"
}
{% endhighlight %}

#### `bugs` (khuyến khích)

Nơi người dùng nên báo cáo các vấn đề với thư viện. GitHub có một trình theo dõi vấn đề được tích hợp sẵn, vì vậy, bạn sẽ thường sử dụng miền phụ `/issue` của kho lưu trữ GitHub của mình cho việc này. Bạn có thể chỉ định một chuỗi nếu bạn chỉ muốn URL này: 

{% highlight js %}
"https://github.com/your-name/your-library/issues"
{% endhighlight %}

Tuy nhiên, nếu bạn cũng muốn thêm một email mà người dùng có thể báo cáo lỗi, bạn có thể sử dụng biểu mẫu đối tượng: 

{% highlight js %}
{
  "email": "youremail@yourdomain.com",
  "url": "https://github.com/your-name/your-library/issues"
}
{% endhighlight %}

`package.json` đã cập nhật:

{% highlight js %}
{
  "name": "catlang-encoder",
  "version": "0.0.1",
  "description": "Fast Unicode to Catlang converter",
  "author": "Cat <cat@gmail.com>",
  "keywords": [
    "catlang",
    "cat language",
    "catlang converter",
    "high performance"
  ],
  "homepage": "https://catlangencoder.js.org",
  "repository": {
    "type": "git",
    "url": "https://github.com/cat/catlang",
    "directory": "js/packages/catlang-encoder"
  },
  "bugs": {
    "email": "cat@gmail.com",
    "url": "https://github.com/cat/catlang/issues"
  },
  "license": "MIT"
}
{% endhighlight %}

#### `engines` (tùy chọn)

Môi trường mà thư viện của bạn sẽ hoạt động. Điều này chỉ áp dụng cho các thư viện hỗ trợ Node.js (ví dụ: thư viện CSS không nên sử dụng trường này). Nếu thư viện của bạn không sử dụng các tính năng hiện đại của JavaScript (chẳng hạn như trình vòng lặp không đồng bộ), bạn cũng không cần chỉ định trường này. Định dạng như sau:

{% highlight js %}
{
  "node": ">=0.10.3 <15"
}
{% endhighlight %}

Hiện tại, `node` là chìa khóa duy nhất của trường `engines` mà bạn sẽ cần sử dụng.

Giả sử `catlang-encoder` cần hỗ trợ cho các tính năng của ES6 như `Promise` + `async`/`await`, `for..of`, v.v. Vì `async`/`await` chỉ được thêm vào v7.6.0, chúng tôi sử dụng đó làm phiên bản tối thiểu.

{% highlight js %}
{
  "name": "catlang-encoder",
  "version": "0.0.1",
  "description": "Fast Unicode to Catlang converter",
  "author": "Cat <cat@gmail.com>",
  "keywords": [
    "catlang",
    "cat language",
    "catlang converter",
    "high performance"
  ],
  "homepage": "https://catlangencoder.js.org",
  "repository": {
    "type": "git",
    "url": "https://github.com/cat/catlang",
    "directory": "js/packages/catlang-encoder"
  },
  "bugs": {
    "email": "cat@gmail.com",
    "url": "https://github.com/cat/catlang/issues"
  },
  "engines": {
    "node": ">=7.6.0"
  },
  "license": "MIT"
}
{% endhighlight %}

#### `contributors` (tùy chọn)

Những người không phải là tác giả đã đóng góp một cách quan trọng vào dự án. Định dạng là một mảng đối tượng hoặc chuỗi có cùng định dạng với trường `author`. Ví dụ: 

{% highlight js %}
[
  "John Doe <me@johndoe.net> (johndoe.net)",
  {
    "name": "Place Holder",
    "email": "placeholder@gmail.com"
  }
]
{% endhighlight %}

Nếu bạn chủ yếu làm việc trên dự án này một mình (có thể với một vài yêu cầu kéo ở đây và ở đó), bạn không cần chỉ định trường này. Tuy nhiên, nếu ai đó đã giúp bạn nhiều lần, bạn nên thêm họ vào.

{% highlight js %}
{
  "name": "catlang-encoder",
  "version": "0.0.1",
  "description": "Fast Unicode to Catlang converter",
  "author": "Cat <cat@gmail.com>",
  "contributors": [
    "Cat 2"
  ],
  "keywords": [
    "catlang",
    "cat language",
    "catlang converter",
    "high performance"
  ],
  "homepage": "https://catlangencoder.js.org",
  "repository": {
    "type": "git",
    "url": "https://github.com/cat/catlang",
    "directory": "js/packages/catlang-encoder"
  },
  "bugs": {
    "email": "cat@gmail.com",
    "url": "https://github.com/cat/catlang/issues"
  },
  "engines": {
    "node": ">=7.6.0"
  },
  "license": "MIT"
}
{% endhighlight %}


#### `bin` (tùy chọn)

Vị trí của tệp nhị phân của gói. Nếu bạn đang phát triển một công cụ CLI, hãy đặt công cụ này thành điểm đầu vào của cơ sở mã của bạn. Tệp bạn đặt sẽ được thực thi bất cứ khi nào ai đó chạy `npm run your-package` hoặc `yarn run your-package`. Tất nhiên, bạn không cần trường này nếu bạn không muốn cung cấp công cụ CLI với gói của mình.

Đối với một tệp thực thi duy nhất, trường có thể chỉ là một chuỗi: 

{% highlight js %}
"path/to/bin.js"
{% endhighlight %}

Nếu bạn có nhiều tệp thực thi, bạn có thể chỉ định một ánh xạ như vậy: 

{% highlight js %}
{
  "command-1": "./bin1.js",
  "command-2": "./bin2.js"
}
{% endhighlight %}

Nếu chúng ta có tệp thực thi CLI để mã hóa Catlang nhanh chóng và bẩn thỉu từ dòng lệnh tại `lib/cli.js`:

{% highlight js %}
{
  "name": "catlang-encoder",
  "version": "0.0.1",
  "description": "Fast Unicode to Catlang converter",
  "author": "Cat <cat@gmail.com>",
  "bin": "lib/cli.js",
  "contributors": [
    "Cat 2"
  ],
  "keywords": [
    "catlang",
    "cat language",
    "catlang converter",
    "high performance"
  ],
  "homepage": "https://catlangencoder.js.org",
  "repository": {
    "type": "git",
    "url": "https://github.com/cat/catlang",
    "directory": "js/packages/catlang-encoder"
  },
  "bugs": {
    "email": "cat@gmail.com",
    "url": "https://github.com/cat/catlang/issues"
  },
  "engines": {
    "node": ">=7.6.0"
  },
  "license": "MIT"
}
{% endhighlight %}


#### `private`

Ngăn không cho gói của bạn được xuất bản nếu được đặt thành `true`. Rõ ràng, bạn không nên có trường này trong `package.json` của mình nhưng một số `projects/templates` dành cho người mới bắt đầu bao gồm `"private": true` trong `package.json` để ngăn bạn vô tình xuất bản mã không phải là một gói. Bạn sẽ muốn xóa trường `private` nếu nó tồn tại; nếu không, NPM sẽ từ chối xuất bản gói của bạn.

Có một số trường hiếm hơn mà đôi khi bạn có thể cần, chẳng hạn như `os` và `man`, trong trường hợp đó, bạn nên xem [tài liệu gốc](https://docs.npmjs.com/cli/v7/configuring-npm/package-json) cho [package.json](https://docs.npmjs.com/cli/v7/configuring-npm/package-json). Ngoài ra, sau này chúng ta sẽ sử dụng trường `script` và nếu bạn chưa quen với nó, bạn nên đọc [phần này](https://docs.npmjs.com/cli/v7/using-npm/scripts).

{% highlight js %}

{% endhighlight %}


## Dependencies và exports

Bạn có thể nhận thấy rằng `package.json` cho `catlang-encoder` của chúng tôi không có phụ thuộc và không có xuất. Chúng tôi sẽ tìm hiểu cách bạn nên xử lý xuất trong bài viết tiếp theo, vì đây là một chủ đề khá phức tạp, nhưng ngay bây giờ chúng ta sẽ thảo luận về các phụ thuộc trong `package.json`.

Theo nguyên tắc chung, bạn nên cố gắng giảm thiểu số lượng phụ thuộc mà bạn sử dụng. Nếu một phần phụ thuộc có dưới 20 dòng mã nguồn, thì logic có lẽ đủ đơn giản để bạn có thể tự viết lại nó vì điều đó sẽ giúp bạn dễ dàng duy trì cơ sở mã của mình hơn.

Nếu bạn thực sự cần các phụ thuộc, có bốn trường bạn có thể sử dụng để chỉ định chúng: `dependencies`, `peerDependencies`, `optionalDependencies`, và `devDependencies`.


#### `dependencies`

Ánh xạ tên gói tới các phiên bản được hỗ trợ cho các phụ thuộc thời gian chạy của thư viện của bạn. Nếu bạn sử dụng mã từ thư viện khác trong thời gian chạy (tức là khi ai đó sử dụng gói của bạn), hãy thêm thư viện đó vào trường này. Cú pháp như sau:

{% highlight js %}
{
  "some-package": "^2.3.1",
  "other-package": ">=7.0.0",
  "last-package": ">=2 <3"
}
{% endhighlight %}

Các khóa của đối tượng là tên của các phụ thuộc, trong khi các giá trị là các phiên bản để chấp nhận. Cú pháp để chỉ định phiên bản được gọi là lập phiên bản ngữ nghĩa hoặc "semver". Chi tiết đầy đủ được nêu chi tiết trên [trang web lập phiên bản semantic](https://semver.org), nhưng nhìn chung bạn chỉ cần biết hai điều:

- Phiên bản thực tế của một gói luôn là ba số được phân tách bằng dấu chấm, như trong trường `version` của `package.json`
- Sự phụ thuộc trong `package.json` có thể sử dụng số nhận dạng phiên bản, tham chiếu đến một hoặc nhiều phiên bản của gói

Khi người dùng cài đặt gói của bạn, trình quản lý gói của họ sẽ thấy tất cả các phần phụ thuộc trong `package.json` và tải xuống các phần có liên quan
Có nhiều loại số nhận dạng phiên bản, nhưng những loại phù hợp nhất là sau:

- Số nhận dạng chính xác, chỉ là số phiên bản. Họ có thể loại trừ bản vá và các phiên bản nhỏ.
    + `1.0.1` chỉ khớp với v1.0.1
    + `1.0.0-rc.0` chỉ khớp với v1.0.0-rc.0 (đây là cách duy nhất để tải phiên bản phát hành trước của một gói)
    + `0.10` khớp với bất kỳ phiên bản nào trong phạm vi v0.10 (ít nhất là v0.10.0, trước v0.11.0)
    + `1` khớp với bất kỳ phiên bản nào trong phạm vi v1 (ít nhất là v1.0.0, trước v2.0.0)
- Giá trị nhận dạng so sánh, khớp với các phiên bản trên hoặc dưới một phiên bản cụ thể
    + `>1.1.3` khớp với các phiên bản gần đây hơn v1.1.3 (v1.1.4, v2.0.4, v.v. tất cả đều hoạt động)
    + `<=2.8.7` khớp với các phiên bản cũ hơn hoặc bằng v2.8.7 (v2.8.7, v1.0.1, v0.0.1 đều hoạt động)
- Đối sánh tất cả các số nhận dạng, sử dụng `x` hoặc `*` để đánh dấu một phần của chuỗi semver có thể là bất kỳ phiên bản nào
    + `1.x` khớp với bất kỳ phiên bản nào trong phạm vi v1 (giống như `1`)
    + `*` phù hợp với tất cả các phiên bản của gói
    + `2.3.*` Khớp với bất kỳ phiên bản nào trong phạm vi v2.3 (như `2.3`)
    + **Cẩn thận: `2.*.0` khớp với bất kỳ phiên bản nào trong phạm vi v2, không chỉ phiên bản vá 0**
- Số nhận dạng chữ số thứ hai, sử dụng dấu ngã để khớp với chữ số thứ hai của phiên bản với điều kiện là chữ số thứ ba lớn hơn hoặc bằng chữ số được chỉ định trong số nhận dạng
    + `~1.2.3` phù hợp với tất cả các phiên bản `>=1.2.3` và `<1.3.0`
    + `~0.4.0` phù hợp với tất cả các phiên bản `>=0.4.0` và `<0.5.0`
- Trình so khớp phiên bản chính, sử dụng `^` để khớp với chữ số khác không đầu tiên
    + Về mặt kỹ thuật, chữ số đầu tiên, không hoặc khác, luôn là phiên bản chính. Tuy nhiên, khi chữ số đầu tiên là số 0, một sự thay đổi lớn đối với chữ số thứ hai là một thay đổi đáng kể và `^` ngăn thư viện của bạn vô tình chấp nhận thay đổi quan trọng, có thể phá vỡ đó.
    + **Đây là trình kết hợp phổ biến nhất**
    + `^3.2.1` khớp với bất kỳ phiên bản nào trong phạm vi v3
    + `^0.4.0` khớp với bất kỳ phiên bản nào trong phạm vi v0.4
    + `^0.0.5` chỉ khớp với v0.0.5

Điều cuối cùng: bạn có thể kết hợp các số nhận dạng phiên bản bằng cách sử dụng dấu cách giữa hai trong số chúng. Mã định danh mới khớp nếu cả hai mã số phụ khớp nhau. Nói cách khác:

- `>=1.5 <3` khớp với các phiên bản ít nhất là v1.5 nhưng thấp hơn v3 (tức là nhiều nhất là v2)
- `1.x <= 1.8` khớp với các phiên bản bắt đầu bằng v1 nhưng nhiều nhất là v1.8

Nếu bạn không chắc rằng chuỗi semver của mình là chính xác, bạn luôn có thể thử [công cụ này](https://semver.npmjs.com) để kiểm tra xem nó có khớp với các phiên bản phụ thuộc của bạn theo cách bạn muốn hay không.

Giả sử chúng ta cần `catlang-dictionary` để cho chúng tôi biết những từ nào có bản dịch trực tiếp sang các glyph ngắn hơn trong Catlang và chúng tôi nhận thấy rằng phiên bản 1.2.3 hoạt động tốt. Giả sử rằng `catlang-dictionary` tuân theo cách lập phiên bản ngữ nghĩa, bạn nên sử dụng `^1.2.3` làm mã định danh phiên bản.

{% highlight js %}
{
  "name": "catlang-encoder",
  "version": "0.0.1",
  "description": "Fast Unicode to Catlang converter",
  "author": "Cat <cat@gmail.com>",
  "bin": "lib/cli.js",
  "contributors": [
    "Cat 2"
  ],
  "keywords": [
    "catlang",
    "cat language",
    "catlang converter",
    "high performance"
  ],
  "homepage": "https://catlangencoder.js.org",
  "repository": {
    "type": "git",
    "url": "https://github.com/cat/catlang",
    "directory": "js/packages/catlang-encoder"
  },
  "bugs": {
    "email": "cat@gmail.com",
    "url": "https://github.com/cat/catlang/issues"
  },
  "engines": {
    "node": ">=7.6.0"
  },
  "dependencies": {
    "catlang-dictionary": "^1.2.3"
  },
  "license": "MIT"
}
{% endhighlight %}


#### `peerDependencies`

Các phần phụ thuộc mà gói của bạn đã được cài đặt dưới dạng tiện ích bổ sung, tiện ích mở rộng hoặc tích hợp. Sự khác biệt giữa các `dependencies` và `peerDependencies` là `peerDependencies` không được cài đặt tự động và thường được sử dụng để biểu thị những gì mà thư viện của bạn tích hợp hoặc mở rộng.

Thật khó để xác định chính xác khi nào bạn nên sử dụng phụ thuộc ngang hàng thay vì phụ thuộc, nhưng nếu người dùng cài đặt thư viện của bạn chỉ vì họ đang trực tiếp sử dụng một gói nhất định, hãy thêm gói đó vào `peerDependencies`.

Ví dụ: một thư viện thành phần React sẽ có `"react"` trong `peerDependencies` và một plugin Babel sẽ có `"@babel/core"` trong `peerDependencies`. Mặt khác, một trình bao bọc JavaScript cho API REST có thể để lại tính năng tìm `node-fetch` trong các `dependencies` thay vì `peerDependencies`. `node-fetch` không được người dùng sử dụng trực tiếp và không phải là lý do gói được cài đặt; điều quan trọng là để các yêu cầu HTTP diễn ra suôn sẻ.

Điều rất quan trọng là bạn phải **sử dụng số nhận dạng phiên bản lỏng lẻo cho các peer dependencies**. Ví dụ: nếu bạn sử dụng `~16.3` làm phiên bản React trong thư viện thành phần React của mình, khi người dùng của bạn cập nhật lên React v16.8, họ sẽ nhận được cảnh báo về các phiên bản không tương thích mặc dù thư viện của bạn có thể vẫn hoạt động trong v16.8. Tốt hơn hết bạn nên sử dụng `^16.3` hoặc nếu bạn nghĩ rằng phiên bản chính tiếp theo sẽ không phá vỡ gói của bạn, `>=16.3`.

Vì `catlang-encoder` hoạt động phổ biến, bất kể khuôn khổ, chúng tôi không cần bất kỳ phụ thuộc ngang hàng nào và sẽ không cần sửa đổi `package.json` của chúng tôi.


#### `optionalDependencies`

Bất kỳ phụ thuộc nào bạn muốn có nhưng có thể làm mà không có. Về mặt hiệu quả, không có gì đảm bảo rằng những phần phụ thuộc này sẽ được cài đặt: chúng thường được cài đặt nếu gói tương thích với hệ điều hành và nếu người dùng đồng ý cài đặt phần phụ thuộc đó. Trường hợp sử dụng chính cho trường này ngăn không cho gói của bạn cài đặt khi một trong các phần phụ thuộc của bạn không tương thích với kiến ​​trúc bộ xử lý, hệ điều hành, v.v.

Điều quan trọng cần lưu ý là **một phụ thuộc có thể được cài đặt cho các chức năng bổ sung là một phụ thuộc ngang hàng tùy chọn**. Nếu bạn có thể cải thiện hoặc thêm chức năng vào một phần mã của mình nếu một phần phụ thuộc được cài đặt, thì đó là phần phụ thuộc ngang hàng tùy chọn chứ không phải phần phụ thuộc tùy chọn vì bạn không muốn phần phụ thuộc được cài đặt theo mặc định.

Ví dụ: phần mở rộng `@discordjs/opus` cho `discord.js` cho phép hỗ trợ một số tính năng gọi thoại nhất định trong Discord API. Vì nhiều người dùng Discord API sẽ không cần hỗ trợ bằng giọng nói nên việc sử dụng `@discordjs/opus` trong `optionalDependencies` sẽ cài đặt nó theo mặc định, làm tăng thêm khối lượng. Do đó, đó là một phụ thuộc ngang hàng tùy chọn, tức là `@discordjs/opus` nằm trong `peerDependencies` và nó được chỉ định là tùy chọn bằng cách sử dụng trường `peerDependenciesMeta`:

{% highlight js %}
{
  "@discordjs/opus": {
    "optional": true
  }
}
{% endhighlight %}

(Lưu ý thêm, `discord.js` thực tế không làm điều này nữa; họ đã loại bỏ hoàn toàn phần phụ thuộc khỏi `package.json` và chỉ yêu cầu người dùng trong README cài đặt các phần phụ thuộc tùy chọn nếu họ muốn.)

Đối với `catlang-encoder`, chúng tôi có thể tùy chọn sử dụng gói `utf-8-validate` nguyên bản để xác minh rằng các đầu vào cho bộ mã hóa là hợp lệ, nhưng không cần thiết vì quá trình xác thực không cần thiết. Vì nói chung, hầu hết người dùng không cần nó, chúng tôi biến nó thành một phụ thuộc ngang hàng tùy chọn. (Hãy nhớ sử dụng trình so khớp phiên bản lỏng lẻo với các phụ thuộc ngang hàng! Chúng tôi sẽ sử dụng `*` để hỗ trợ bất kỳ phiên bản nào của `utf-8-validate`.)

Mặt khác, chúng tôi muốn sử dụng `catlang-concat` bất cứ khi nào có thể để nối các bộ đệm Catlang hiệu quả hơn, nhưng chúng tôi vẫn có thể thực hiện nối bộ đệm bình thường mà không có nó, vì vậy chúng tôi chỉ định nó như một phụ thuộc tùy chọn để nói với người quản lý gói một cách hiệu quả: "Tôi thực sự muốn catlang-concat nếu bạn có thể cài đặt nó, nhưng nếu không, tôi sẽ vẫn hoạt động nếu không có nó."

{% highlight js %}
{
  "name": "catlang-encoder",
  "version": "0.0.1",
  "description": "Fast Unicode to Catlang converter",
  "author": "Cat <cat@gmail.com>",
  "bin": "lib/cli.js",
  "contributors": [
    "Cat 2"
  ],
  "keywords": [
    "catlang",
    "cat language",
    "catlang converter",
    "high performance"
  ],
  "homepage": "https://catlangencoder.js.org",
  "repository": {
    "type": "git",
    "url": "https://github.com/cat/catlang",
    "directory": "js/packages/catlang-encoder"
  },
  "bugs": {
    "email": "cat@gmail.com",
    "url": "https://github.com/cat/catlang/issues"
  },
  "engines": {
    "node": ">=7.6.0"
  },
  "dependencies": {
    "catlang-dictionary": "^1.2.3"
  },
  "peerDependencies": {
    "utf-8-validate": "*"
  },
  "peerDependenciesMeta": {
    "utf-8-validate": {
      "optional": true
    }
  },
  "optionalDependencies": {
    "catlang-concat": "^4.5.6"
  },
  "license": "MIT"
}
{% endhighlight %}


#### `devDependencies`




-----
Tham khảo:
- [Creating a modern JS library: Introduction](https://dev.to/101arrowz/creating-a-modern-js-library-introduction-1a0c)
- [Creating a modern JS library: Writing good code](https://dev.to/101arrowz/creating-a-modern-js-library-writing-good-code-170a)
- [Creating a modern JS library: TypeScript and Flow](https://dev.to/101arrowz/creating-a-modern-js-library-typescript-and-flow-3ge)
- [Creating a modern JS library: package.json and dependencies](https://dev.to/101arrowz/creating-a-modern-js-library-package-json-and-dependencies-5ek9)