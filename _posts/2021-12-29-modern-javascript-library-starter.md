---
layout: post
title: Module Javascript
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
