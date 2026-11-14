---
layout: post
categories: ["DevOps & Hạ tầng"]
title: "Website tài liệu kỹ thuật cho doanh nghiệp (1): Tổng quan, technical stack và các cách triển khai"
subtitle: "Bố cục ba cột, Markdown, ảnh, PDF, MP4, code block và 8 cách đưa lên mạng có mật khẩu mà vẫn giữ kín source"
date: 2026-11-15 14:00:00 +0700
tags:
- Documentation
- Docs as Code
- Docusaurus
- VitePress
- MkDocs
- aaPanel
- cPanel
- Cloudflare
- GitHub Pages
- Nginx
series: "Website tài liệu kỹ thuật cho doanh nghiệp"
series_order: 1
---

> Series 2 bài về việc dựng một website tài liệu kỹ thuật cho doanh nghiệp: danh mục bên trái, nội dung ở giữa, thông tin phụ bên phải, viết bằng Markdown, chạy được trong mạng nội bộ lẫn trên Internet có user/password. Bài này là phần tổng quan: yêu cầu, technical stack, các công cụ mã nguồn mở và tám cách triển khai xếp từ dễ đến khó, ưu tiên giữ kín source. [Bài 2](/2026/11/15/website-tai-lieu-ky-thuat-doanh-nghiep-2-docusaurus-aapanel/) chọn một cách và làm từng bước trên aaPanel. Phiên bản và giới hạn gói miễn phí được tra cứu vào tháng 11/2026, hãy kiểm tra lại trước khi quyết định.

- [Các bài trong series](#các-bài-trong-series)
- [Bài toán và các giả định](#bài-toán-và-các-giả-định)
- [Bố cục ba cột](#bố-cục-ba-cột)
- [Hai trường phái: web tĩnh và wiki động](#hai-trường-phái-web-tĩnh-và-wiki-động)
- [Technical stack theo từng lớp](#technical-stack-theo-từng-lớp)
- [Các bộ sinh web tĩnh cho tài liệu](#các-bộ-sinh-web-tĩnh-cho-tài-liệu)
- [Các wiki động để đối chiếu](#các-wiki-động-để-đối-chiếu)
- [Hỗ trợ các loại nội dung](#hỗ-trợ-các-loại-nội-dung)
- [Triển khai nội bộ công ty](#triển-khai-nội-bộ-công-ty)
- [Tám cách triển khai online có đăng nhập](#tám-cách-triển-khai-online-có-đăng-nhập)
- [Bảng so sánh nhanh](#bảng-so-sánh-nhanh)
- [Cách được chọn và lý do](#cách-được-chọn-và-lý-do)
- [Lưu ý quan trọng](#lưu-ý-quan-trọng)
- [Nguồn tham khảo](#nguồn-tham-khảo)

## Các bài trong series

1. **Tổng quan, technical stack và các cách triển khai** (bài này)
2. [Từng bước với Docusaurus, aaPanel và Basic Auth](/2026/11/15/website-tai-lieu-ky-thuat-doanh-nghiep-2-docusaurus-aapanel/)

## Bài toán và các giả định

Yêu cầu chức năng:

- Giao diện ba cột: danh mục bên trái, nội dung chính ở giữa, thông tin phụ bên phải.
- Nội dung viết bằng Markdown, có ảnh, PDF, video MP4, code block có tô màu cú pháp, sơ đồ.
- Chạy được trong mạng nội bộ công ty, công nghệ tùy chọn.
- Chạy được trên Internet, phải có user/password mới xem được. Server online là aaPanel hoặc cPanel (có Node và PHP), hoặc các nền tảng như GitHub Pages, Cloudflare.
- Ưu tiên giữ kín source code của bộ tài liệu.

Series này viết theo ba giả định, nếu hoàn cảnh của bạn khác thì kết luận có thể khác:

| Giả định | Lựa chọn trong series | Nếu khác đi |
|---|---|---|
| Ai viết tài liệu | Lập trình viên, viết Markdown và quản lý bằng Git | Nhân viên không rành kỹ thuật cần soạn trên trình duyệt: xem mục wiki động |
| Mức đăng nhập | Vài tài khoản dùng chung | Cần mỗi người một tài khoản hoặc SSO: xem cách 4, 5 và 8 |
| Server online chính | aaPanel trên VPS, web server Nginx | cPanel: bài 2 có mục ghi chú riêng |

## Bố cục ba cột

```text
+----------------------------------------------------------------+
| Logo   Tài liệu   API   Phiên bản v2          [Tìm kiếm] [Sáng/Tối] |
+---------------+--------------------------------+---------------+
| DANH MỤC      | NỘI DUNG CHÍNH                 | THÔNG TIN PHỤ |
|               |                                |               |
| Giới thiệu    | # Cài đặt máy chủ              | Phụ trách     |
| Hướng dẫn     |                                | Phiên bản     |
|   Cài đặt  <  | Đoạn văn, bảng, ảnh,           | Ngày rà soát  |
|   Cấu hình    | code block, PDF, video...      |               |
| API           |                                | Trong trang:  |
| Vận hành      |                                |  - Yêu cầu    |
|               | [Bài trước]      [Bài sau]     |  - Các bước   |
+---------------+--------------------------------+---------------+
```

- **Cột trái** là cây danh mục toàn bộ tài liệu, thường sinh tự động từ cấu trúc thư mục.
- **Cột giữa** là nội dung, giới hạn chiều rộng khoảng 70 đến 90 ký tự mỗi dòng để dễ đọc.
- **Cột phải** mặc định là mục lục của trang đang xem (các tiêu đề cấp 2, cấp 3). Đây cũng là chỗ hợp lý cho thông tin phụ: người phụ trách, phiên bản tài liệu, ngày cập nhật, liên kết liên quan.

Gần như mọi bộ sinh web tài liệu hiện đại đều có sẵn bố cục này, bạn không phải tự viết CSS.

## Hai trường phái: web tĩnh và wiki động

| | Web tĩnh (docs as code) | Wiki động |
|---|---|---|
| Nơi lưu nội dung | File Markdown trong Git | Cơ sở dữ liệu |
| Soạn thảo | VS Code hoặc bất kỳ trình soạn thảo nào | Trình soạn thảo trên trình duyệt |
| Lịch sử, duyệt bài | Git commit, pull request | Tính năng lịch sử của wiki |
| Server cần gì | Chỉ cần phục vụ file HTML | PHP hoặc Node, cơ sở dữ liệu, cập nhật bảo mật |
| Phân quyền | Không có sẵn, phải đặt lớp xác thực phía trước | Có sẵn user, nhóm, quyền |
| Bề mặt tấn công | Rất nhỏ | Lớn hơn vì có code chạy trên server |
| Hợp với | Đội kỹ thuật | Đội hỗn hợp, nhiều người không biết Git |

Với giả định "lập trình viên viết Markdown và Git", series này đi theo hướng web tĩnh. Điểm mạnh lớn nhất của hướng này đối với yêu cầu giữ kín source: **thứ đưa lên server chỉ là HTML đã build**, còn repo Markdown, lịch sử commit và cấu hình không cần rời khỏi công ty.

## Technical stack theo từng lớp

| Lớp | Lựa chọn phổ biến | Ghi chú |
|---|---|---|
| Soạn thảo | VS Code, Markdown, MDX | MDX cho phép nhúng component vào Markdown |
| Bộ sinh web tĩnh | Docusaurus, VitePress, Starlight, MkDocs, Hugo | Xem bảng chi tiết bên dưới |
| Runtime khi build | Node.js 20 trở lên, hoặc Python, hoặc file chạy đơn (Hugo) | Chỉ cần ở máy build, server không cần |
| Tìm kiếm | Tìm kiếm cục bộ (Pagefind, MiniSearch, Lunr), Algolia DocSearch, Typesense, Meilisearch | Tài liệu riêng tư nên dùng tìm kiếm cục bộ, không gửi nội dung ra dịch vụ ngoài |
| Sơ đồ | Mermaid, PlantUML, draw.io (xuất SVG), Excalidraw | Mermaid viết ngay trong Markdown |
| Tô màu code | Prism, Shiki | Có sẵn trong bộ sinh web |
| Tài liệu API | OpenAPI kèm Redoc, Scalar hoặc Swagger UI | Sinh từ file đặc tả |
| Quản lý source | Git với GitHub private, GitLab, Gitea hoặc Forgejo tự host | Gitea và Forgejo đặt được hoàn toàn trong mạng nội bộ |
| File lớn | Git LFS, hoặc để ngoài Git và chép riêng | Dùng cho MP4, PDF nặng |
| CI/CD | GitHub Actions, GitLab CI, Gitea Actions, hoặc script chạy tay | Build rồi đẩy thư mục kết quả lên server |
| Web server | Nginx, Apache, Caddy, IIS | aaPanel dùng Nginx hoặc Apache, cPanel thường là Apache hoặc LiteSpeed |
| Xác thực | HTTP Basic Auth, Cloudflare Access, Authelia, Authentik, oauth2-proxy, Keycloak | Basic Auth đủ cho vài tài khoản dùng chung |
| HTTPS | Let's Encrypt (có sẵn trong aaPanel), AutoSSL (cPanel), Cloudflare | Bắt buộc khi dùng Basic Auth |
| Chống dò mật khẩu | Fail2ban, giới hạn tần suất của Nginx, danh sách IP cho phép | |
| Kết nối không mở cổng | Cloudflare Tunnel, Tailscale, WireGuard | Dùng khi site đặt trong mạng nội bộ |

## Các bộ sinh web tĩnh cho tài liệu

Tất cả đều mã nguồn mở và có sẵn bố cục ba cột.

| Công cụ | Nền tảng | Điểm mạnh | Điểm cần cân nhắc |
|---|---|---|---|
| **Docusaurus** (Meta) | Node, React, MDX | Quản lý nhiều phiên bản tài liệu và đa ngôn ngữ có sẵn, hệ plugin lớn, tùy biến giao diện bằng React. Bản tra cứu được là 3.10.2 (07/2026), cần Node 20 trở lên | Build chậm hơn và nặng hơn các công cụ dùng Vite |
| **VitePress** (nhóm Vue) | Node, Vue, Vite | Rất nhanh, tìm kiếm cục bộ có sẵn, cấu hình gọn | Danh mục trái phải khai báo tay hoặc dùng plugin, không có sẵn quản lý phiên bản. Bản 2.0 vẫn ở giai đoạn thử nghiệm lúc tra cứu |
| **Starlight** (Astro) | Node, Astro | Tìm kiếm Pagefind có sẵn, trang nhẹ, đa ngôn ngữ tốt | Vẫn ở dải phiên bản 0.x, quản lý phiên bản cần plugin |
| **Material for MkDocs** | Python | Cấu hình bằng một file YAML, rất dễ bắt đầu, không cần biết JavaScript | Đã vào chế độ bảo trì, chỉ còn sửa lỗi nghiêm trọng và bảo mật. Nhóm tác giả chuyển sang **Zensical**, công cụ kế nhiệm đọc được `mkdocs.yml` cũ nhưng còn rất mới |
| **Hugo** kèm theme Docsy, Hextra hoặc Doks | Go, một file chạy | Build cực nhanh, không cần Node hay Python | Ngôn ngữ template khó tùy biến hơn |
| **mdBook** | Rust, một file chạy | Đơn giản nhất, dạng sách | Ít tính năng, cột phải cần plugin |
| **Nextra**, **Fumadocs** | Node, Next.js | Hợp với đội đã dùng Next.js | Xuất web tĩnh thuần cần cấu hình thêm |
| **Docsify** | Chỉ JavaScript phía trình duyệt | Không cần bước build, chép file Markdown lên là chạy | Server phục vụ thẳng file Markdown gốc, trang trắng nếu tắt JavaScript |
| **Jekyll** kèm theme Just the Docs | Ruby | Quen thuộc nếu đã dùng GitHub Pages | Hệ sinh thái tài liệu ít phát triển hơn |

Gợi ý chọn nhanh:

- Cần nhiều phiên bản tài liệu (v1, v2), cần tùy biến sâu: **Docusaurus**.
- Cần nhanh, gọn, đội quen Vue: **VitePress**.
- Đội không dùng JavaScript, muốn một file cấu hình: **MkDocs** hoặc **Hugo**. Với dự án mới nên theo dõi Zensical trước khi gắn bó lâu dài với Material for MkDocs.

## Các wiki động để đối chiếu

Không phải hướng chính của series, nhưng nên biết để chọn đúng khi giả định thay đổi.

| Công cụ | Nền tảng | Ghi chú |
|---|---|---|
| **BookStack** | PHP (Laravel), MySQL | Chạy được trên aaPanel và nhiều gói cPanel, có user, nhóm, phân quyền, đăng nhập LDAP hoặc SSO |
| **DokuWiki** | PHP, không cần cơ sở dữ liệu | Dễ cài nhất trên shared hosting, có phân quyền |
| **Wiki.js** | Node, PostgreSQL | Soạn Markdown trên web, đồng bộ hai chiều với Git |
| **Outline** | Node, PostgreSQL, Redis | Giao diện đẹp, bắt buộc có nhà cung cấp đăng nhập (SSO), hợp với Docker |
| **Docmost** | Node, PostgreSQL | Soạn thảo cộng tác thời gian thực |

Nếu sau này cần "mỗi nhóm chỉ xem một phần tài liệu", wiki động giải quyết gọn hơn nhiều so với web tĩnh.

## Hỗ trợ các loại nội dung

| Loại nội dung | Cách làm trên web tĩnh | Lưu ý |
|---|---|---|
| Markdown | Chuẩn CommonMark và GFM (bảng, danh sách việc, chú thích) | Hộp cảnh báo (note, warning) có cú pháp riêng theo từng công cụ |
| Ảnh | Để cạnh file Markdown, tham chiếu đường dẫn tương đối | Ưu tiên SVG cho sơ đồ, WebP hoặc PNG cho ảnh chụp, thêm plugin phóng to khi bấm |
| PDF | Nhúng bằng thẻ `<iframe>` hoặc `<object>`, kèm liên kết tải về | Trình duyệt trên điện thoại thường không hiển thị PDF nhúng, luôn kèm liên kết |
| MP4 | Thẻ `<video controls>` của HTML5 | Mã hóa H.264 và AAC để chạy mọi trình duyệt. Server phải hỗ trợ Range request để tua (Nginx và Apache hỗ trợ sẵn) |
| Code block | Rào code ba dấu huyền kèm tên ngôn ngữ | Thường có sẵn tiêu đề file, số dòng, tô sáng dòng, nút sao chép, tab theo ngôn ngữ |
| Sơ đồ | Khối `mermaid` trong Markdown | Bật plugin Mermaid |
| Công thức toán | KaTeX hoặc MathJax | Cần plugin |
| Tài liệu API | Sinh từ file OpenAPI | Redoc hoặc Scalar nhúng thành một trang |

Hai điều dễ bị bỏ sót:

- **Không đưa MP4 và PDF nặng vào lịch sử Git thông thường.** Repo sẽ phình rất nhanh. Dùng Git LFS, hoặc để media ở một thư mục riêng và chép lên server tách biệt với bước build.
- **Media cũng phải nằm sau lớp đăng nhập.** Nếu video để ở YouTube ẩn danh hay một bucket công khai thì yêu cầu user/password mất ý nghĩa.

## Triển khai nội bộ công ty

Thư mục kết quả build chỉ gồm file tĩnh nên cách nào cũng được, xếp theo độ dễ:

1. **Một máy chủ nội bộ chạy Nginx, Caddy hoặc IIS** trỏ vào thư mục build. Với công ty dùng Windows Server, IIS có sẵn và dùng được đăng nhập Windows.
2. **Docker**: một container `nginx` gắn thư mục build, tiện khi đã có hạ tầng container.
3. **Gitea hoặc Forgejo tự host kèm Actions**: đẩy code là tự build và chép sang web server, toàn bộ nằm trong mạng LAN.
4. **Chính cái aaPanel nội bộ** nếu công ty đã cài: tạo site tĩnh giống hệt bản online.

Nên có tên miền nội bộ (ví dụ `docs.congty.lan`) qua DNS nội bộ thay vì nhớ địa chỉ IP. Nếu chỉ truy cập trong LAN hoặc qua VPN thì có thể không cần mật khẩu, nhưng HTTPS vẫn nên có nếu mạng có khách hoặc Wi-Fi dùng chung.

## Tám cách triển khai online có đăng nhập

Xếp theo độ dễ triển khai, có tính đến ưu tiên giữ kín source. "Source" ở đây là repo Markdown, lịch sử Git và cấu hình. Nội dung đã build thành HTML thì cách nào cũng phải nằm ở đâu đó để phục vụ người đọc.

### Cách 1. Build tại máy, chép thư mục build lên aaPanel hoặc cPanel, bật Basic Auth

- Build trên máy lập trình viên hoặc máy build nội bộ, chỉ chép thư mục kết quả lên server qua SFTP, SCP hoặc trình quản lý file.
- Bật mật khẩu bằng tính năng có sẵn: aaPanel có giới hạn truy cập bằng mật khẩu cho site, cPanel có **Directory Privacy**.
- **Riêng tư source:** tốt nhất. Server không có repo, không có token Git, không cần Node.
- **Nhược điểm:** triển khai bằng tay (viết script là hết), tài khoản dùng chung nên không biết ai đã xem gì.

### Cách 2. CI build rồi đẩy lên aaPanel hoặc cPanel

- Giống cách 1 nhưng bước build và chép file do GitHub Actions, GitLab CI hoặc Gitea Actions thực hiện mỗi khi đẩy code.
- **Riêng tư source:** tốt nếu CI tự host (Gitea trong LAN). Nếu dùng GitHub private thì source nằm ở GitHub, chấp nhận được với đa số công ty nhưng không còn "chỉ trong công ty".
- **Nhược điểm:** phải quản lý khóa SSH triển khai trong phần secrets của CI.

### Cách 3. aaPanel Git Manager kéo repo và build ngay trên server

- aaPanel có **Git Manager** với bốn tab Repository, Deployments, Script, Webhook: server tự kéo code khi có webhook, chạy script build, có lịch sử và quay lui.
- **Riêng tư source:** kém hơn. Toàn bộ repo và một token hoặc khóa đọc repo nằm trên VPS công khai. Server cũng phải cài Node và đủ RAM để build.
- **Hợp khi:** muốn tự động hóa mà không muốn dựng CI.

### Cách 4. Cloudflare Pages kèm Cloudflare Access

- Đẩy thư mục build lên Cloudflare Pages bằng lệnh `wrangler pages deploy` (không cần kết nối repo), rồi đặt Cloudflare Access phía trước. Người xem đăng nhập bằng mã gửi qua email hoặc tài khoản Google, Microsoft.
- **Riêng tư source:** tốt nếu dùng cách đẩy trực tiếp. Nội dung đã build nằm trên hạ tầng Cloudflare.
- **Giới hạn gói miễn phí của Pages lúc tra cứu:** tối đa 20.000 file mỗi site, mỗi file không quá 25 MiB, 500 lần build mỗi tháng. Video MP4 lớn hơn 25 MiB phải để ở nơi khác (ví dụ R2). Gói miễn phí của Access thường được công bố ở mức 50 người dùng, hãy kiểm tra bảng giá hiện hành.
- **Nhược điểm:** đây là đăng nhập theo từng email, không phải "vài user/password dùng chung". Phải nhớ chặn cả địa chỉ `*.pages.dev` mặc định, không chỉ tên miền riêng.

### Cách 5. Cloudflare Tunnel từ máy chủ nội bộ

- Site đặt trên máy chủ trong công ty. Dịch vụ `cloudflared` tạo kết nối đi ra Cloudflare, không cần IP tĩnh, không mở cổng trên tường lửa. Đặt Cloudflare Access phía trước, hoặc giữ Basic Auth ở Nginx nội bộ, hoặc cả hai.
- **Riêng tư source:** rất tốt. Cả source lẫn bản build đều ở trong công ty, Cloudflare chỉ chuyển tiếp lưu lượng.
- **Nhược điểm:** cần một máy nội bộ chạy liên tục và một tên miền quản lý DNS bằng Cloudflare. Phụ thuộc đường truyền Internet của công ty.

### Cách 6. GitHub Pages

- Gói Free chỉ cho Pages trên repo công khai. Gói Pro, Team cho phép Pages từ repo riêng tư nhưng **trang web vẫn công khai với cả Internet**. Chỉ GitHub Enterprise Cloud mới có tính năng giới hạn người xem theo quyền đọc repo.
- Cách vá phổ biến là mã hóa phía trình duyệt bằng **StatiCrypt**: mỗi trang HTML được mã hóa AES, người xem nhập mật khẩu để giải mã. Cách này không bảo vệ ảnh, PDF, MP4 và file chỉ mục tìm kiếm, và ai cũng tải được file đã mã hóa về để dò mật khẩu ngoại tuyến.
- **Kết luận:** không hợp với yêu cầu user/password, trừ khi công ty đã có Enterprise Cloud.

### Cách 7. Wiki động trên aaPanel hoặc cPanel

- Cài BookStack hoặc DokuWiki (PHP) hoặc Wiki.js (Node, Docker). Có sẵn tài khoản từng người, nhóm, phân quyền.
- **Riêng tư source:** nội dung nằm trong cơ sở dữ liệu trên server công khai.
- **Nhược điểm:** phải cập nhật bảo mật, sao lưu cơ sở dữ liệu, bề mặt tấn công lớn hơn. Đổi lại không cần ai biết Git.

### Cách 8. Web tĩnh kèm cổng đăng nhập tự host

- Đặt Authelia, Authentik hoặc oauth2-proxy trước Nginx (cơ chế `auth_request`). Có trang đăng nhập đẹp, mỗi người một tài khoản, xác thực hai lớp, nối được LDAP hoặc SSO công ty.
- **Riêng tư source:** tốt như cách 1.
- **Nhược điểm:** khó nhất trong danh sách, thêm một dịch vụ phải vận hành. Chỉ đáng làm khi Basic Auth không còn đủ.

## Bảng so sánh nhanh

| # | Cách | Độ dễ | Source nằm ở đâu | Kiểu đăng nhập | Chi phí thêm |
|---|---|---|---|---|---|
| 1 | Build tại máy, chép lên aaPanel/cPanel, Basic Auth | Rất dễ | Chỉ trong công ty | Vài user/password dùng chung | Không |
| 2 | CI build rồi đẩy lên | Dễ | Git server (tự host hoặc GitHub private) | Như trên | Không |
| 3 | aaPanel Git Manager build trên server | Dễ | Cả trên VPS công khai | Như trên | VPS cần đủ RAM để build |
| 4 | Cloudflare Pages và Access | Dễ | Trong công ty (đẩy trực tiếp) | Theo email, SSO | Miễn phí trong giới hạn |
| 5 | Cloudflare Tunnel từ máy nội bộ | Trung bình | Chỉ trong công ty, cả bản build | Access hoặc Basic Auth | Máy nội bộ chạy liên tục |
| 6 | GitHub Pages | Dễ nhưng không đạt yêu cầu | GitHub | Không có, trừ Enterprise Cloud | Enterprise Cloud |
| 7 | Wiki động | Trung bình | Cơ sở dữ liệu trên server | Từng người, phân quyền | Công bảo trì |
| 8 | Web tĩnh và cổng đăng nhập tự host | Khó | Chỉ trong công ty | Từng người, 2FA, SSO | Công vận hành |

## Cách được chọn và lý do

**Cách 1, dùng Docusaurus, triển khai trên aaPanel với HTTP Basic Auth qua HTTPS.**

- Đúng cả ba giả định: Markdown và Git, vài tài khoản dùng chung, aaPanel.
- Giữ kín source ở mức cao nhất trong các cách dùng VPS: server chỉ nhận HTML đã build.
- Không cần cài gì thêm trên server ngoài Nginx mà aaPanel đã có. Site tĩnh gần như không có gì để vá lỗi.
- Cùng một thư mục build dùng được cho bản nội bộ lẫn bản online.
- Dễ nâng cấp: khi cần tự động thì chuyển sang cách 2, khi cần tài khoản từng người thì thêm cách 8 hoặc Cloudflare Access mà không phải viết lại tài liệu.

Docusaurus được chọn vì có sẵn đủ ba cột, quản lý phiên bản tài liệu, MDX để nhúng PDF và video, và cột phải tùy biến được để hiện thông tin phụ. Nếu không cần quản lý phiên bản, VitePress là lựa chọn nhẹ hơn và các bước triển khai ở bài 2 vẫn giữ nguyên, chỉ khác tên thư mục build.

## Lưu ý quan trọng

- **Basic Auth chỉ an toàn khi đi qua HTTPS.** Qua HTTP, mật khẩu gửi đi gần như ở dạng rõ. Bật chuyển hướng bắt buộc sang HTTPS.
- **Kiểm tra từng loại file sau khi bật mật khẩu.** Cấu hình sai rất dễ dẫn đến trang HTML bị chặn nhưng ảnh, PDF, MP4 hoặc file chỉ mục tìm kiếm vẫn tải được không cần đăng nhập. Bài 2 có lệnh kiểm tra.
- **Màn hình mật khẩu bằng JavaScript không phải là bảo mật.** Trình duyệt vẫn nhận đủ file, chỉ là bị che đi.
- **Tài khoản dùng chung không có dấu vết từng người.** Khi một người nghỉ việc phải đổi mật khẩu cho tất cả. Nên tạo mỗi nhóm một tài khoản để ít nhất thu hồi được theo nhóm.
- **Chống dò mật khẩu.** Basic Auth không tự khóa sau nhiều lần sai. Thêm Fail2ban hoặc giới hạn tần suất, và nếu được thì chỉ cho phép dải IP của công ty.
- **Chặn máy tìm kiếm.** Thêm thẻ `noindex` và header `X-Robots-Tag`. Mật khẩu đã chặn bot, nhưng lớp thứ hai giúp ích nếu một ngày ai đó tắt nhầm mật khẩu.
- **Không viết bí mật vào tài liệu.** Mật khẩu hệ thống, khóa API, chuỗi kết nối thật thuộc về trình quản lý bí mật, không thuộc về trang tài liệu dù có đăng nhập.
- **Tìm kiếm.** Với tài liệu riêng tư, dùng tìm kiếm cục bộ. Các dịch vụ tìm kiếm bên ngoài cần thu thập nội dung của bạn, và trình thu thập của họ cũng không qua được lớp mật khẩu.
- **Sao lưu.** Repo Git là bản gốc. Site trên server luôn dựng lại được từ repo nên không cần sao lưu riêng, nhưng media để ngoài Git thì phải có.
- **Phân loại tài liệu.** Không phải tài liệu nào cũng nên lên bản online. Docusaurus và các công cụ tương tự cho phép build hai bản từ cùng một repo: bản nội bộ đầy đủ và bản online đã lược bỏ.
- **Dữ liệu cá nhân và hợp đồng.** Tài liệu có thông tin khách hàng hoặc ràng buộc bảo mật với đối tác cần được xem xét trước khi đặt lên máy chủ bên ngoài, kể cả có mật khẩu.

Bài tiếp theo: [từng bước với Docusaurus, aaPanel và Basic Auth](/2026/11/15/website-tai-lieu-ky-thuat-doanh-nghiep-2-docusaurus-aapanel/).

## Nguồn tham khảo

- [Docusaurus: Changelog](https://docusaurus.io/changelog)
- [aaPanel: Create a site from Git và Git Manager](https://www.aapanel.com/docs/Function/Tutorial/create_for_git.html)
- [Cloudflare Pages: Limits](https://developers.cloudflare.com/pages/platform/limits)
- [GitHub Docs: Changing the visibility of your GitHub Pages site](https://docs.github.com/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/changing-the-visibility-of-your-github-pages-site)
- [GitHub Changelog: Access control for GitHub Pages](https://github.blog/changelog/2021-01-21-access-control-for-github-pages)
- [NGINX: Restricting Access with HTTP Basic Authentication](https://docs.nginx.com/nginx/admin-guide/security-controls/configuring-http-basic-authentication/)
- [Material for MkDocs: Insiders now free for everyone](https://squidfunk.github.io/mkdocs-material/blog/2025/11/11/insiders-now-free-for-everyone/)
- [Python Developer Tooling Handbook: Material for MkDocs](https://pydevtools.com/handbook/reference/mkdocs-material/)
- [Zensical: Roadmap](https://zensical.org/roadmap/)
