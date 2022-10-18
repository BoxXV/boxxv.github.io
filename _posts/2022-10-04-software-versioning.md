---
layout: post
title: Tìm hiểu về cách đánh version phiên bản phần mềm
subtitle: Software Versioning And Release Numbers
tags:
- Versioning
- version
- Release
- Software
---

Bài viết này giúp chúng ta hiểu thêm về quy tắc đánh số hiệu các phiên bản (version) của phần mềm máy tính do các hãng, các lập trình viên sử dụng phát hành.

![Software Versioning](https://boxxv.github.io/img/2022/builds-releases-1.webp "Software Versioning")


### Đặt vấn đề

Người “ngoại đạo” hoặc thậm chí những người sử dụng máy tính chuyên nghiệp cũng chưa chắc hiểu rõ ý nghĩa đằng sau những dãy số “bí ẩn” đi kèm với phần mềm mình vừa cài đặt. Ví dụ: **Mozilla Firefox 68.0.1**, **Google Chrome 76.0.3809.132**, **TeamViewer 14.0.13880** …v.v. Câu hỏi lớn nhất với chúng ta là:

- Tại sao phiên bản của phần mềm lại được đánh số?
- Phiên bản phần mềm 1.0 và 2.0 khác nhau như thế nào?
- Nếu bây giờ tôi bắt tay viết một phần mềm mà đặt mã hiệu phiên bản của tôi như thế nào thì phù hợp?


### Định nghĩa

Hệ thống đánh số hiệu phiên bản phần mềm là quy tắc để xác định tên duy nhất của một phần mềm ở mỗi giai đoạn phát triển của nó

Thông thường, một phần mềm trong quá trình phát triển nó được chỉnh sửa, nâng cấp hoặc vá lỗi nhiều lần. Có những lần chỉnh sửa chỉ đơn thuần là những hiệu chỉnh nhỏ không đáng kể, những cũng có những lần “nâng cấp” toàn diện khiến cho nó không còn là thứ giống như nguyên thủy (bản thân hệ điều hành Windows là 1 ví dụ), hay nói cách khác lần “nâng cấp” này đã đưa phần mềm lên “level” mới.

Hiện có một số phương pháp gán số hiệu phiên bản phần mềm được dùng phổ biến là:

- **Sequence-based identifiers**: Đánh số phiên bản bằng các con số
		+ Semantic Versioning
		+ major.minor[.build[.revision]]
- **Stage-based identifiers**: Đánh số hiệu phiên bản dựa theo mức độ ổn định của sản phẩm ()


### Sematic Versioning

Theo Semantic Versioning thì version number về cơ bản sẽ có format như sau →

![Software Versioning](https://boxxv.github.io/img/2022/semver.png "Software Versioning")

> x.y.z

Trong đó:
- **x – MAJOR version:** tăng khi bạn thực hiện các thay đổi dẫn đến KHÔNG tương thích ngược.
- **y – MINOR version:** tăng khi bạn thêm tính năng và vẫn đảm bảo tương thích ngược (backwards-compatible).
- **z – PATCH version:** tăng khi bạn thực hiện fix lỗi xử lý bên trong và vẫn đảm bảo tương thích ngược (backwards-compatible)

Ngoài ta cũng có thể có thêm các nhãn bổ sung đằng sau đối với các bản pre-release, cái này sẽ giải thích ngay ở phần bên dưới.


### major.minor[.build[.revision]]

Phương pháp này sử dụng các con số (đôi khi kết hợp thêm các chữ cái) để gán số hiệu cho các phiên bản. Công thức đánh số hiệu phiên bản như sau:

`major`.`minor`.[`build `[.`revision`]]
hoặc
`major`.`minor` [`maintenance`[.`build`]]

![Software Versioning](https://boxxv.github.io/img/2022/version_control.jpg "Software Versioning")

Ý nghĩa các số major, minor, build, revision như sau

- **major**: Chuỗi phiên bản chính. Đánh số khi có những thay đổi không tương thích với phiên bản cũ
- **minor**: Chuỗi phiên bản phụ. Đánh số khi thêm tính năng mới nhưng vẫn đảm bảo tương thích với các phiên bản cũ.
- **build**: Chuỗi phiên bản build. Đánh dấu các lần fix bugs, 2 chữ số.
- **revision**: Lần sửa đổi. đánh dấu số lần sửa đổi của mã nguồn của phiên bản build.
Chỉ số `major` sẽ tăng mỗi khi:  Có sự **thay đổi lớn trong “nhân hệ thống”** mà theo đó hệ thống mới có thể khác 1 phần hay hoàn toàn hệ thống cũ.

Chỉ số `minor` sẽ tăng mỗi khi: Có sự thay đổi phần “core” của hệ thống mà **không làm mất đi hoàn toàn tính tương thích** trong cùng phiên bản chính.

Còn chỉ số `build` sẽ tăng mỗi khi: Có đóng gói gửi đi ra ngoài đội code (đội phát triển) nhằm các mục đích phát hành hay thử nghiệm…

Chỉ số `revision` có thể được sử dụng mỗi khi: Cần thay thế code phát hành trước đó mà chưa cần thiết phải thay tên phiên bản. Chỉ số này là lần sửa đổi (revisions) của mã nguồn, nó đánh dấu số lần sửa đổi của mã nguồn và được thường được hệ thống kiểm quản lý mã nguồn của hãng kiểm soát:

#### Quy tắc quan trọng đối với phương pháp đánh số phiên bản bằng cách này như sau:
1. Khi phát hành một phiên bản mới các chỉ số `major`, `minor`, `build` phải được tăng ổn định và có thứ tự. Ví dụ 1.9.0 → 1.10.0 → 1.10.1
2. Mỗi khi phiên bản mới đã được phát hành, tất cả nội dung (bao gồm mã nguồn, API) của phiên bản đó phải giữ nguyên không được thay đổi. Bất kỳ thay đổi phát sinh nào đều phải được công bố như phát hành một phiên bản mới.
3. Các phiên bản phát triển ban đầu thường được đánh số major = 0 (dạng 0.y.z). Bạn có thể thực hiện bất kỳ thay đổi nào trong các phiên bản ở giai đoạn này.
4. Chỉ số `build` tăng nếu phiên bản này chỉ sửa các lỗi phát sinh, và đảm bảo tương thích với các bản cũ trước đó.
5. Chỉ số phiên bản phụ `minor` tăng nếu phiên bản này:
- Tương thích ngược với các bản cũ có cùng phiên bản chính
- Cung cấp thêm mới hoặc loại bỏ ít nhất 1 chức năng của phần mềm

Thông thường người ta thường tăng chỉ số minor nếu:
- Thêm mới một chức năng quan trọng
- Có sự cải thiện trong mã nguồn (giúp chương trình xử lý tốt hơn, nhanh hơn…). Sau khi tăng chỉ số phiên bản phụ minor thì số hiệu phiên bản vá build thường được thiết lập về 0


### Stage-based identifers

![Software Versioning](https://boxxv.github.io/img/2022/image-33.png "Software Versioning")

Tên gọi cho các phiên bản phần mềm khi phát hành gồm : `Closebeta`, `Openbeta`, `ReleaseCandidate`, `Official version`. Ý nghĩa của từng phiên bản như sau:

#### Tiền alpha
Đây là giai đoạn sơ khai nhất, bao gồm những hoạt động được thực hiện trước khi vào giai đoạn kiểm thử phần mềm. Những hoạt động trong giai đoạn này gồm có phân tích yêu cầu, thiết kế phần mềm, phát triển phần mềm, kiểm thử đơn vị (unit testing).

#### Alpha
Giai đoạn này là pha đầu tiên bắt đầu kiểm thử phần mềm trong vòng đời phát hành (alpha là kí tự đầu tiên trong bảng chữ cái Hy Lạp, được sử dụng như số 1).

Giai đoạn alpha luôn luôn được kết thúc bằng việc không bổ sung thêm chức năng nào nữa (feature freeze), như vậy có thể nói phần mềm sau giai đoạn này là “đã hoàn chỉnh về chức năng” (feature complete).

Các phần mềm trong giai đoạn này đều chưa hoàn chỉnh và có thể gây ra mất dữ liệu hoặc crash, nên những phiên bản phần mềm như vậy thường không được công bố rộng rãi mà chỉ **khuyến khích bộ phận kiểm thử hay những người tình nguyện kiểm thử sử dụng nhằm tìm kiếm lỗi.**

Tuy nhiên, đối với những phần mềm mã nguồn mở thì có thể có một chút khác biệt. Những phiên bản alpha của chúng thường được phân phối công khai và thường kèm theo mã nguồn của phần mềm đó.

#### Beta
Là các phiên bản dùng thử, nhằm tung ra để người dùng public rộng rãi sử dụng và… test lỗi, phản hồi. Bản này có thể có lỗi được phát hành để nhằm mục tiêu hoàn thiện trước hi phát hành chính thức.

#### Closebeta: Phiên bản thử nghiệm hạn chế.
- **Đặc điểm**: Bản closebeta là bản thử nghiệm các tính năng mới phát triển, nó thường không mang đầy đủ các đặc điểm của hệ thống và dễ dàng thay đổi hoặc bị loại bỏ nếu nhận được các phản ứng không tốt sau khi thử nghiệm.
- **Ý nghĩa**: Phiên bản này được sử dụng để khảo sát một hoặc một vài tính năng mới xây dựng nào đó của hệ thống (khi chỉ số majorthay đổi).
- **Mục đích**: Bản closebeta là bản phát hành sớm của một phần mềm nhằm mục đích tập hợp và sử dụng sức mạnh cộng đồng trong việc đóng góp ý kiến, cải tiến tính năng; phát hiện các lỗi trước khi phân phối rộng rãi tới người sử dụng thông thường.
- **Đối tượng được mời thử nghiệm**: các lập trình viên và nhóm người dùng có kinh nghiệm.
Bản closebeta không phải bản phát hành rộng rãi đến tay người sử dụng, do đó chỉ gửi hạn chế đến những người có trình độ và thực sự quan tâm đến việc phát triển hệ thống.
- **Nâng cấp**: Không.

#### Openbeta: Phiên bản thử nghiệm diện rộng.
- Đặc điểm: Bản openbeta là bản thử nghiệm các tính năng đã phát triển, nó thường mang đầy đủ các đặc điểm của hệ thống và hiếm khi thay đổi hoặc bị loại bỏ khỏi hệ thống trừ khi có phản hồi không tốt từ cộng đồng.
- Ý nghĩa: Phiên bản này được sử dụng để thử nghiệm một cách đầy đủ và toàn diện hệ thống mới phát triển.
- Mục đích: Bản openbeta là bản thử nghiệm đầy đủ nhằm mục đích tập hợp và sử dụng sức mạnh cộng đồng trong việc dò tìm để vá các lỗi có thể xảy ra mà quá trình thử nghiệm hạn chế (closebeta) không phát hiện ra.
- Đối tượng được mời thử nghiệm: tất cả mọi người là thành viên diễn đàn
- Hỗ trợ thử nghiệm: Có đầy đủ.
- Hỗ trợ sử dụng: 1 phần. Người thử nghiệm được cung cấp các tài liệu hướng dẫn sử dụng, được trợ giúp trực tiếp trên diễn đàn.
- Nâng cấp: Không.

#### Release Candidate: Phiên bản ứng viên.
Là phiên bản cho dùng thử trước khi sản phẩm chính thức ra đời.

- Đặc điểm: Bản Release Candidate là bản ổn định, là ứng cử viên cho phiên bản chính thức. Các lỗi được phát hiện trong giai đoạn này sẽ tiếp tục được sửa chữa.
- Mục đích & Ý nghĩa: Phiên bản này được sử dụng như một bản đệm trong thời gian chờ phiên bản chính thức ra mắt nhằm tránh trường hợp một bản chính thức có thể bị lỗi ngay sau khi ra mắt.
- Đối tượng người dùng: tất cả mọi người
- Hỗ trợ sử dụng: đầy đủ
- Nâng cấp: Có thể. Cả việc nâng cấp từ phiên bản cũ lên và nâng cấp lên phiên bản chính thức đều có thể được hỗ trợ.

#### Official version: Phiên bản chính thức.
- Đặc điểm: Bản Official version là bản chính thức đầu tiên của giai đoạn phát triển của dòng phiên bản mới. Official version là tên gọi của lần phát hành phiên bản duy nhất, các phiên bản tiếp theo sau đó sẽ chỉ được gọi tên bằng số phiên bản.
- Mục đích & Ý nghĩa: Phiên bản này đánh dấu việc ra mắt dòng phiên bản mới và khuyến khích người sử dụng chuyển tiếp lên phiên bản mới.

![Software Versioning](https://boxxv.github.io/img/2022/image-36.png "Software Versioning")

**Các căn cứ để đưa ra tên gọi cho các phiên bản mới phát hành**:Tên gọi xếp theo mức độ ổn định sẽ được gán cho một phiên bản đặt theo số nhất định, việc đặt tên do đội code chọn dựa trên đánh giá về tính ổn định của code sau phát hành. Các căn cứ để đưa ra tên gọi như sau:

**1. Closebeta:**
Có thể có nhiều phiên bản đánh số theo thứ tự phát hành: Closebeta 1, Closebeta 2, Closebeta 3… để phân biệt. Mỗi phiên bản tương ứng với một phiên bản số khác nhau & duy nhất. Phiên bản sau không nhất thiết phải bao gồm các tính năng của phiên bản trước và cũng không có quy định về mặt thời gian giữa mỗi phiên bản. Giai đoạn Closebeta sẽ kết thúc khi không còn những thay đổi lớn trong nhân hệ thống.

**2. Openbeta:**
Nếu không có sự cố nào nghiêm trọng trong bản Closebeta cuối cùng, bản thử nghiệm diện rộng (Openbeta) đầu tiên sẽ được phát hành tới tất cả các thành viên. Trong giai đoạn này, đều đặn mỗi tuần sẽ có một phiên bản Openbeta ra mắt để fix lỗi phiên bản Openbeta trước.
Có thể có nhiều phiên bản đánh số theo thứ tự phát hành: Openbeta 1, Openbeta 2, Openbeta 3… để phân biệt. Mỗi phiên bản tương ứng với một phiên bản số khác nhau & duy nhất. Phiên bản sau bắt buộc bao gồm các tính năng của phiên bản trước.
Giai đoạn Openbeta sẽ kết thúc khi số lượng lỗi được phát hiện giảm xuống, không còn các lỗi nghiêm trọng sau 2 phiên bản Openbeta.

**3. Release Candidate (RC)**
Khi số lượng lỗi được phát hiện giảm xuống, không còn các lỗi nghiêm trọng sau 2 phiên bản Openbeta, thì một bản Release Candidate sẽ được phát hành. Có thể có nhiều phiên bản đánh số theo thứ tự phát hành: RC1, RC2, RC3… để phân biệt. Mỗi phiên bản tương ứng với một phiên bản số khác nhau & duy nhất. Phiên bản sau bắt buộc bao gồm các tính năng của phiên bản trước. Một bản Release Candidate mới sẽ được ra mắt sớm hơn thông lệ thời gian (như quy định ở bản Openbeta) nếu nó bị phát hiện các lỗi nghiêm trọng

**4. Official version**
Phiên bản chính thức chỉ được phát hành sau một khoảng thời gian 2 tuần, khi bản RC gần nhất không phát hiện các lỗi tính năng.


-----
Tham khảo:

- [Tìm hiểu về cách đánh version phiên bản phần mềm](https://cloudgeeks.net/tim-hieu-ve-cach-danh-version-phien-ban-phan-mem/)
- [Software versioning](https://en.wikipedia.org/wiki/Software_versioning)
- [Software Versioning And Release Numbers](https://www.zapbuild.com/bitsntricks/software-versioning-and-release-numbers/)
- [How to Create Version Numbers that are Actually Semantic](https://blog.inedo.com/blog/release-numbering-scheme)
- [Introduction to Semantic Versioning](https://www.geeksforgeeks.org/introduction-semantic-versioning/)