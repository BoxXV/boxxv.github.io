---
layout: post
title: Tạo thư viện JavaScript cho người mới
subtitle: How to publish a package with TypeScript, testing, GitHub Actions, and auto-publish to NPM
image: "img/js.jpg"
tags:
- Rollup
- AMD
- CommonJS
- UMD
- npm
- JavaScript
- library
- module
---

![Module Javascript](https://boxxv.github.io/img/posts/module-loading.png "Module Javascript")

## Xuất bản thư viện

Hồi đó, khi tôi muốn viết và xuất bản một thư viện JavaScript, tất cả những gì tôi phải làm là tạo một dự án GitHub mới, viết package.json với một số chi tiết cơ bản, thêm index.js và xuất bản lên NPM thông qua CLI. Nhưng thiết lập đơn giản này bỏ sót rất nhiều thứ mới được coi là thiết yếu: không có loại, không CI/CD, không kiểm tra, v.v.

Vì vậy, lần cuối cùng tôi cần bắt đầu một thư viện JavaScript mới, tôi đã dành chút thời gian để thiết lập những điều cơ bản và sau đó nhận ra rằng các bước này hầu hết đều chung chung và có thể được sử dụng lại trong các dự án khác nhau. Bài viết này là tài liệu về các khía cạnh khác nhau cần thiết để phát triển và xuất bản một thư viện hiện đại.

Cụ thể hơn, tôi muốn các tính năng này:

- Thư viện được viết bằng TypeScript với các loại được xuất bản trong gói
- Có những bài kiểm tra, cũng được viết bằng TypeScript
- Một đường dẫn CI chạy để xây dựng các cam kết và chạy thử nghiệm
- Một đường dẫn CD được chạy cho mọi phiên bản mới xuất bản lên sổ đăng ký NPM

## Bắt đầu viết mã

Các tệp quan trọng là một số cấu hình, package source và các bài kiểm tra:

```javascript
src/index.ts
src/index.test.ts
package.json
tsconfig.json
```

Vì có bước biên dịch nên nguồn và tệp được biên dịch nằm trong các thư mục khác nhau. Trong khi các tệp `.ts` nằm trong `src/`, thì mục tiêu biên dịch lại nằm ở `dist/`.

Gói.json:

```javascript
{
	// name, version, description, other data
	"main": "dist/index.js",
	"type": "module",
	"files": [
		"dist"
	],
	"devDependencies": {
		"ts-node": "^10.9.2",
		"typescript": "^5.3.3"
	}
}
```

Các tệp xác định `dist` vì chỉ các tệp đã biên dịch mới được đóng gói và đẩy vào sổ đăng ký NPM. Sau đó, `main: "dist/index.js"` xác định điểm vào.

`tsconfig.json` định cấu hình trình biên dịch TypeScript:

```javascript
{
	"compilerOptions": {
		"noEmitOnError": true,
		"strict": true,
		"sourceMap": true,
		"target": "es6",
		"module": "nodenext",
		"moduleResolution": "nodenext",
		"declaration": true,
		"outDir": "dist"
	},
	"include": [
		"src/**/*.*"
	],
	"exclude": [
		"**/*.test.ts"
	]
}
```

Tùy thuộc vào dự án, có thể có nhiều cấu hình khác nhau, nhưng phần quan trọng là các tệp trong thư mục `src/` được bao gồm chứ không phải các thử nghiệm và `outDir` là `dist`.

Sau đó, các tệp `index.ts` và `index.test.ts` rất đơn giản, chỉ để chứng minh rằng thư viện hoạt động:

```javascript
// src/index.ts

export const test = (value: string) => {
	return "Hello " + value;
}
```

```javascript
// src/index.test.ts

import test from "node:test";
import { strict as assert } from "node:assert";
import {test as lib} from "./index.js";

test('synchronous passing test', (t) => {
	const result = lib("World");
  assert.strictEqual(result, "Hello World");
});
```

Lưu ý dòng `import ... from "./index.js"`. Mặc dù tệp có phần mở rộng `.ts`, việc nhập được thực hiện bằng `.js`.

## NPM scripts

Tiếp theo, định cấu hình các tập lệnh trong `package.json`.

Đầu tiên là việc `build` và `clean`:

```javascript
{
	"scripts": {
		"build": "tsc --build",
		"clean": "tsc --build --clean"
	}
}
```

Chúng chỉ đơn giản gọi `tsc` để biên dịch TypeScript thành JavaScript:

```javascript
$ npm run build

> website-validator@0.0.8 build
> tsc --build

$ ls dist
index.d.ts  index.js  index.js.map
```

Tiếp theo, tập lệnh `prepare` chạy bản dựng khi gói được xuất bản. Đây là một cái tên đặc biệt mà `npm` gọi nó ở các [phần khác nhau của vòng đời](https://docs.npmjs.com/cli/v10/using-npm/scripts#prepare-and-prepublish):

```javascript
{
	"scripts": {
		"prepare": "npm run clean && npm run build"
	}
}
```

## Tests

Tiếp theo, cấu hình các bài kiểm tra tự động. Đối với điều này, tôi thấy rằng sẽ dễ dàng hơn nếu không biên dịch mã kiểm tra mà sử dụng thư viện tự động tuân thủ các tệp TS khi cần. Đây là nơi sự phụ thuộc của `ts-node` phát huy tác dụng.

Do đó, tập lệnh `test` không cần chạy bản `build`:

```javascript
{
	"scripts": {
		"test": "node --test --loader ts-node/esm src/**/*.test.ts"
	}
}
```

`--loader ts-node/esm` gắn `ts-node` vào quy trình phân giải mô-đun nút và biên dịch các tệp `.ts` bất cứ khi nào chúng được nhập. Điều này làm cho việc thiết lập thử nghiệm trở nên cực kỳ dễ dàng: không cần biên dịch, chỉ chạy.

```javascript
$ npm test

> website-validator@0.0.8 test
> node --test --loader ts-node/esm src/**/*.test.ts

(node:245543) ExperimentalWarning: `--experimental-loader` may be removed in the future; instead use `register()`:
--import 'data:text/javascript,import { register } from "node:module"; import { pathToFileURL } from "node:url"; register("ts-node/esm", pathToFileURL("./"));'
(Use `node --trace-warnings ...` to show where the warning was created)
✔ synchronous passing test (1.01411ms)
ℹ tests 1
ℹ suites 0
ℹ pass 1
ℹ fail 0
ℹ cancelled 0
ℹ skipped 0
ℹ todo 0
ℹ duration_ms 2650.590767
```

## Tích hợp liên tục

Bây giờ chúng ta đã có sẵn tất cả các tập lệnh cho thư viện, đã đến lúc thiết lập `GitHub Actions` để chạy bản dựng và kiểm thử cho mỗi lần đẩy.

Các hành động được định cấu hình trong thư mục `.github/workflows`, trong đó mỗi tệp YAML mô tả một quy trình làm việc.

```javascript
# .github/workflows/node.js.yml
name: Node.js CI

on:
  push:
  pull_request:

jobs:
  build:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [21.x]

    steps:
    - uses: actions/checkout@v4
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    - run: npm ci
    - run: npm run build --if-present
    - run: npm test
```

Hãy chia nhỏ những phần thú vị trong quy trình làm việc này!

`on: push, pull_requests` xác định rằng công việc sẽ chạy theo mọi yêu cầu Đẩy và kéo. Bạn có thể xác định một số bộ lọc ở đây, chẳng hạn như chỉ chạy thử nghiệm cho một số nhánh nhất định, nhưng hiện tại nó không cần thiết.

Công việc `build` sử dụng `ubuntu-latest`, đây là cơ sở toàn diện tốt để chạy các tập lệnh vì nó có rất nhiều phần mềm được cài đặt sẵn.

`strategy/matrix` xác định `node-version` nào sẽ chạy bản dựng. Điều này hoạt động giống như tạo khuôn mẫu: phần giữ chỗ `${matrix.node-version}` sẽ được điền từng giá trị trong mảng này và mỗi cấu hình sẽ chạy trong quá trình xây dựng.

Các `steps` rất đơn giản: `checkout` lấy mã hiện tại, `setup-node` cài đặt phiên bản NodeJS cụ thể, sau đó chạy `npm ci`, `npm run build` và `npm test`.

### In action

Trang Hành động GitHub cho thấy quy trình làm việc chạy cho mỗi lần đẩy:

### Auto-deploy to NPM

```javascript
# .github/workflows/npm-publish.yml
name: Node.js Package

on:
  push:
    tags:
      - "*"

permissions:
  id-token: write

jobs:
  build:
    # same as the other build

  publish-npm:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v3
        with:
          node-version: 20
          registry-url: https://registry.npmjs.org/
      - run: npm ci
      - run: npm publish --provenance
        env:
          NODE_AUTH_TOKEN: ${{secrets.npm_token}}
```

### Provenance

### Secrets

```javascript
# .github/workflows/npm-publish.yml

jobs:
  publish-npm:
    steps:
      # ...
      - run: npm publish --provenance
        env:
          NODE_AUTH_TOKEN: ${{secrets.npm_token}}
```

### Publishing a new version

```javascript
$ npm version patch
v0.0.9
```

```javascript
$ git push
$ git push --tags
```

-----
Tham khảo:
- [Modern JavaScript library starter](https://advancedweb.hu/modern-javascript-library-starter/)
- [Building A JavaScript App VS Building A JavaScript Library](https://speckle.systems/blog/building-a-javascript-app-vs-building-a-javascript-library/)
- [6 Steps to Create and Publish a Modern JavaScript and TypeScript Library in 2024](https://medium.com/@jfmelo/master-the-art-of-writing-and-launching-your-own-modern-javascript-and-typescript-library-in-2024-a9f26f62acba)
- [6 Tips for Writing a JavaScript Library](https://javascript.plainenglish.io/6-tips-to-write-a-library-bb19dc83841c)
- [How To Create And Publish Your JavaScript Library With SvelteKit](https://joyofcode.xyz/how-to-publish-a-javascript-library)
- [Modern JavaScript Essentials for Developers](https://daily.dev/blog/modern-javascript-essentials-for-developers)
- [How to Write a TypeScript Library](https://www.tsmean.com/articles/how-to-write-a-typescript-library/)
- [Exploring Modern JavaScript Tools: npm, Parcel, Babel, and ES6 Modules](https://www.linkedin.com/pulse/exploring-modern-javascript-tools-npm-parcel-babel-es6-ketan-raval-trnnf)
- [The Pragmatic Guide to Your First JavaScript Library](https://betterprogramming.pub/the-pragmatic-guide-to-your-first-javascript-library-516a7b08c677)
- [An Overview of Modern JavaScript Development](https://medium.com/@firatatalay/an-overview-of-modern-javascript-development-7fde33693b3c)
- [AssetMapper: Modern JS with Zero Build System](https://symfonycasts.com/screencast/asset-mapper)
- [Building modules with Deno](https://deno.com/learn/modules)
- [Design and Build Your Own JavaScript Library: Tips & Tricks](https://www.sitepoint.com/design-and-build-your-own-javascript-library/)
- [Creating a Reliable JavaScript Library: A Step-by-Step Guide](https://betterprogramming.pub/creating-a-reliable-javascript-library-a-step-by-step-guide-6907c778341c)
- [Best Practices for Writing Efficient JavaScript Code](https://medium.com/@ishahmeer/best-practices-for-writing-efficient-javascript-code-90689033c6f6)
- [Creating Custom JavaScript Libraries: A Guide to Reusable and Efficient Code](https://blog.bitsrc.io/creating-custom-javascript-libraries-a-guide-to-reusable-and-efficient-code-2bcaff45339d)
- [Best practices for building a JS library (tooling and architecture)](https://www.reddit.com/r/javascript/comments/mjeiys/askjs_best_practices_for_building_a_js_library/)
- [How to Write and Publish Your First JavaScript Library](https://dev.to/oluwaferanmi/how-to-write-and-publish-your-first-javascript-library-cei)
- [Exploring Modern JavaScript Tooling: Babel, Webpack, and Rollup](https://www.linkedin.com/pulse/exploring-modern-javascript-tooling-babel-webpack-rollup-singh-d6a0c)
- [Tips on Writing Good JavaScript Libraries](https://medium.com/@PepsRyuu/tips-on-writing-good-javascript-libraries-e3c3068ec705)
