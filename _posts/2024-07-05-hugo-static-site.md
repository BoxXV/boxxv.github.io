---
layout: post
categories: ["Web & Frontend"]
title: Xây dựng một trang web tĩnh cực nhanh với Hugo
subtitle: How To Build a Blazing Fast Static Site With Hugo
image: "img/home-bg.jpg"
tags:
- Hugo
- Framework
- Static Site
---

# Mục lục

- [Mục lục](#mục-lục)
- [Giới thiệu](#giới-thiệu)
- [Xây dựng trang web với hugo](#xây-dựng-trang-web-với-hugo)
  - [Cài đặt Hugo](#cài-đặt-hugo)
  - [Kiểm tra cài đặt](#kiểm-tra-cài-đặt)
  - [Tạo khung sườn cho Hugo](#tạo-khung-sườn-cho-hugo)
  - [Themes](#themes)
  - [Cấu hình hugo](#cấu-hình-hugo)
    - [Phương pháp 1 - Git Clone](#phương-pháp-1---git-clone)
    - [Phương pháp 2 - Git Submodule (`Recomended`)](#phương-pháp-2---git-submodule-recomended)
    - [Phương pháp 3 - Download an unzip](#phương-pháp-3---download-an-unzip)
    - [Phương pháp 4 - Hugo module](#phương-pháp-4---hugo-module)
    - [Cuối cùng đặt chủ đề là PaperMod trong cấu hình trang web của bạn](#cuối-cùng-đặt-chủ-đề-là-papermod-trong-cấu-hình-trang-web-của-bạn)
  - [Bài viết đầu tiên](#bài-viết-đầu-tiên)
- [Triển khai website lên github và cấu hình Github Action](#triển-khai-website-lên-github-và-cấu-hình-github-action)
- [Kết luận](#kết-luận)

# Giới thiệu

Một ngày đẹp trời, mình bắt đầu nổi hứng muốn tạo một trang blog cho riêng mình để lưu lại những cái mình đã trải nghiệm và đang tìm hiểu. Tập trung chính vào công nghệ và tiếng anh. Mình lượn lờ trên mạng và xem cách tạo trang web cá nhân cũng như dùng cái gì để giải quyết vấn đề đó, nào là Wordpress, Hexo, Jekyll, Hugo,… Và sau một vài chục phút tìm hiểu thì mình quyết định chọn Hugo để đồng hành cùng mình. Tại sao chỉ từ A đến X, vì mình muốn để Z cho bạn tự trải nghiệm

# Xây dựng trang web với hugo

Để xây dựng trang web với Hugo, bước đầu tiên vẫn là nắm vững tổng quan về nó

## Cài đặt Hugo

Mình sử dụng ubuntu để host nên sử dụng apt package manager và câu lệnh như sau:

```
sudo apt install hugo
```

- [Install Hugo in Windows 11](https://www.jeremymorgan.com/tutorials/golang/how-to-hugo-windows-11/)
- [Install Hugo on Windows 10](https://www.techielass.com/how-to-install-hugo-on-windows-10/)
- [Install Hugo on Windows](https://gohugo.io/installation/windows/)

## Kiểm tra cài đặt

Để kiểm tra cài đặt, hãy mở một shell lệnh PowerShell hoặc một Command Prompt và nhập `hugo version`

## Tạo khung sườn cho Hugo

Sau khi cài đặt thì đi đến tạo website đầu tiên với hugo

```
hugo new site MyFreshWebsite
hoặc
hugo new site MyFreshWebsite --format yaml
cd MyFreshWebsite
```

Hugo sẽ tạo 1 folder tên là mysite và đây là cấu trúc của folder mà hugo vừa tạo

```
.
├── archetypes
│   └── default.md
├── assets
├── content
├── data
├── i18n
├── layouts
├── static
├── themes
└── hugo.yaml
```

Trong đó chúng ta chỉ cần chú ý đến mấy thư mục và file chính:

- `content`: Nơi viết nội dung cho website, là các file markdown, mỗi file tương ứng 1 trang trong website.
- `theme`: Chứa các theme có sẵn tải trên mạng về để làm giao diện cho website.
- `config.toml`: File cấu hình cho website như tên website, sử dụng theme gì, ... Có thể đổi sang định dạng yml hoặc yaml nếu không quen với toml.

## Themes

Thế là đã có khung sườn cho hugo. Công việc tiếp theo là tìm themes cho hắn. Vậy thì tìm themes ở đâu? ở trang [Hugo themes](https://themes.gohugo.io) này nè

Sau khi lục lọi 1 hồi thì mình đã tìm đến[ hugo-profile theme](https://hugo-profile.netlify.app)

![hugo-profile theme](https://images.viblo.asia/878fd387-2097-4124-90e5-1443ffb61326.png "hugo-profile theme")

Chủ đề nằm trong thư mục `MyFreshWebsite/themes`.

Ví dụ: `PaperMod` will be installed in `MyFreshWebsite/themes/PaperMod`

## Cấu hình hugo

Chọn được theme rồi thì thêm nó vào trong hugo project thôi. Về lệnh thì do có chút khác biệt về phần themes nên mình sử câu lệnh hơi khác so với trang [Hugo quickstart](https://gohugo.io/getting-started/quick-start/) nên ai gặp lỗi thì có thể tham khảo document của Hugo

### Phương pháp 1 - Git Clone

CÀI ĐẶT: Trong thư mục MyFreshWebsite của trang Hugo, hãy chạy:

```
git clone https://github.com/adityatelange/hugo-PaperMod themes/PaperMod --depth=1
cd themes/PaperMod
git pull
```

Bạn có thể sử dụng `--branch v7.0` ở cuối lệnh trên nếu bạn muốn giữ nguyên bản phát hành cụ thể.

### Phương pháp 2 - Git Submodule (`Recomended`)

CÀI ĐẶT: Trong thư mục MyFreshWebsite của trang Hugo, hãy chạy:

```
cd MyFreshWebsite
git init
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
hugo server
```

Bạn có thể sử dụng `--branch v7.0` để kết thúc lệnh trên nếu bạn muốn giữ nguyên bản phát hành cụ thể. Đọc thêm về git submodules [tại đây](https://www.atlassian.com/git/tutorials/git-submodule).

CẬP NHẬT: Bên trong thư mục MyFreshWebsite của trang Hugo của bạn, hãy chạy:

```
git submodule update --remote --merge
```

### Phương pháp 3 - Download an unzip

Tải xuống mã nguồn PaperMod dưới dạng Zip từ Github Releases và giải nén trong thư mục chủ đề của bạn tại MyFreshWebsite/themes/PaperMod

https://github.com/adityatelange/hugo-PaperMod/archive/master.zip

https://github.com/adityatelange/hugo-PaperMod/archive/v7.0.zip

https://github.com/adityatelange/hugo-PaperMod/archive/refs/tags/v7.0.zip

### Phương pháp 4 - Hugo module

Cài đặt [ngôn ngữ lập trình Go](https://go.dev/doc/install) vào hệ điều hành của bạn.

Khởi tạo bản mod hugo của riêng bạn

```
hugo mod init YOUR_OWN_GIT_REPOSITORY
```

Thêm PaperMod vào file config.yml của bạn

```
module:
  imports:
  - path: github.com/adityatelange/hugo-PaperMod
```

CẬP NHẬT:

```
hugo mod get -u
```

Đọc thêm: [Hugo Docs - HUGO MODULES](https://gohugo.io/hugo-modules/use-modules/)

### Cuối cùng đặt chủ đề là PaperMod trong cấu hình trang web của bạn

Trong `config.yml` thêm:

```
theme: ["PaperMod"]
```

## Bài viết đầu tiên

Cấu hình xong theme thì chúng ta có thể bắt đầu viết blog bằng cách gõ lệnh sau để tạo ra một file markdown trong thư mục `content` (my-first-post.md):

```
hugo new posts/my-first-post.md
```

File mới tạo sẽ trông dạng như sau:

```md
---
title: "My First Post"
date: 2019-03-26T08:47:11+01:00
draft: true
---
```

Trong đó có cấu hình tên bài viết (title), ngày xuất bản (date), bản nháp hay đã sẵn sàng xuất bản (draft). Nội dung bài viết thì viết bằng cú pháp markdown, viết sau phần dấu gạch ngang ---. Bài viết nào có đánh dấu draft: true thì sẽ không được build.

Chạy thử website trên local bằng lệnh `hugo server`, truy cập [http://localhost:1313](http://localhost:1313) để xem kết quả. Đường dẫn của trang sẽ tương ứng với đường dẫn file [http://localhost:1313/posts/my-first-post](http://localhost:1313/posts/my-first-post). Khi đã thấy ưng ý thì build ra static files (HTML CSS JS) bằng lệnh hugo. Website sẽ được build vào trong thư mục public và chỉ cần đẩy lên 1 hosting hỗ trợ static web là xong.

# Triển khai website lên github và cấu hình Github Action

Tóm tắt thì việc cần làm ở đây là tạo 1 [github pages](https://pages.github.com/) repository dạng `<username>.github.io`

Thay vì **Deploy from a branch**, bạn có thể Deploy từ **Github Action**. Cách này dùng trong trường hợp bạn không có project web tĩnh trực tiếp, mà phải build qua công cụ như React, Webpack, Hugo,... thì Github Action sẽ build cho bạn và lưu vào nhánh riêng trên repo đấy.

# Kết luận

Chân thành cảm ơn đã đọc hế bài viết. BYE👋👋👋

-----
- [Xây dựng website cá nhân với Hugo và GitHub](https://viblo.asia/p/xay-dung-website-ca-nhan-voi-hugo-va-github-x7Z4DjBnLnX)
- [Cách tạo một trang blog cá nhân miễn phí dành cho dev](https://viblo.asia/p/cach-tao-mot-trang-blog-ca-nhan-mien-phi-danh-cho-dev-1VgZv2jOZAw)
- []()
- [Cách để custom domain cho github pages](https://viblo.asia/p/cach-de-custom-domain-cho-github-pages-PwlVmODlJ5Z)
- [Xây dựng blog cá nhân đảm bảo RẺ-ĐẸP-NHANH-BỀN.👍](https://viblo.asia/p/xay-dung-blog-ca-nhan-dam-bao-re-dep-nhanh-ben-RQqKLqObZ7z)
- []()