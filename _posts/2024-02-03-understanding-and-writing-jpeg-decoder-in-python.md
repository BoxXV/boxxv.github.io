---
layout: post
title: Hiểu và giải mã hình ảnh JPEG bằng Python
subtitle: Understanding and Decoding a JPEG Image using Python
image: "img/2024/reverse_engineering_intro_featured.jpg"
tags:
- Reverse Engineering
- JPEG
- Python
---
# Mục lục

- [Mục lục](#mục-lục)
- [Giới thiệu](#giới-thiệu)
- [Different parts of a JPEG](#different-parts-of-a-jpeg)
- [Bắt đầu tập tin và kết thúc tập tin](#bắt-đầu-tập-tin-và-kết-thúc-tập-tin)
- [Mã hóa JPEG](#mã-hóa-jpeg)
- [Không gian màu JPEG](#không-gian-màu-jpeg)
- [Biến đổi và lượng tử hóa cosine rời rạc](#biến-đổi-và-lượng-tử-hóa-cosine-rời-rạc)
- [Zig-zag](#zig-zag)
- [Mã hóa độ dài chạy và Delta](#mã-hóa-độ-dài-chạy-và-delta)
- [Huffman Encoding](#huffman-encoding)
- [Giải mã JPEG](#giải-mã-jpeg)
- [Trích xuất bảng Huffman](#trích-xuất-bảng-huffman)
- [Tổng kết](#tổng-kết)

Chào mọi người! 👋 Hôm nay chúng ta sẽ tìm hiểu thuật toán nén JPEG. Một điều mà nhiều người không biết là JPEG không phải là một định dạng mà là một thuật toán. Hình ảnh JPEG bạn nhìn thấy hầu hết ở định dạng JFIF (Định dạng trao đổi tệp JPEG) sử dụng nội bộ thuật toán nén JPEG. Đến cuối bài viết này, bạn sẽ hiểu rõ hơn nhiều về cách thuật toán JPEG nén dữ liệu và cách bạn có thể viết một số mã Python tùy chỉnh để giải nén nó. Chúng tôi sẽ không đề cập đến tất cả các sắc thái của định dạng JPEG (như quét lũy tiến) mà chỉ đề cập đến định dạng đường cơ sở cơ bản khi viết bộ giải mã của chúng tôi.

# Giới thiệu

Tại sao phải viết một bài khác trên JPEG khi đã có hàng trăm bài viết trên internet? Chà, thông thường khi bạn đọc các bài viết về JPEG, tác giả chỉ cung cấp cho bạn thông tin chi tiết về định dạng trông như thế nào. Bạn không triển khai bất kỳ mã nào để thực hiện việc giải nén và giải mã thực tế. Ngay cả khi bạn viết mã, nó vẫn ở dạng C/C++ và không thể truy cập được đối với nhiều người. Tôi dự định thay đổi điều đó bằng cách chỉ cho bạn cách bộ giải mã JPEG cơ bản hoạt động bằng Python 3. Tôi sẽ dựa trên mã được cấp phép MIT này nhưng sẽ sửa đổi nhiều để tăng khả năng đọc và dễ hiểu. Bạn có thể tìm thấy mã đã sửa đổi cho bài viết này trên repo GitHub của tôi.

# Different parts of a JPEG

Hãy bắt đầu với bức ảnh đẹp này của Ange Albertini. Nó liệt kê tất cả các phần khác nhau của một tệp JPEG đơn giản. Hãy nhìn vào nó. Chúng ta sẽ khám phá từng phân khúc. Bạn có thể phải tham khảo hình ảnh này khá nhiều lần khi đọc hướng dẫn này.

![Reverse Engineering](https://boxxv.github.io/img/2024/JPEGRGB_dissected.png "Reverse Engineering")

Ở mức rất cơ bản, hầu hết mọi tệp nhị phân đều chứa một vài điểm đánh dấu (hoặc tiêu đề). Bạn có thể coi những điểm đánh dấu này giống như dấu trang. Chúng rất quan trọng trong việc hiểu tệp và được các chương trình như tệp (trên Mac/Linux) sử dụng để cho chúng tôi biết chi tiết về tệp. Các điểm đánh dấu này xác định nơi lưu trữ một số thông tin cụ thể trong một tệp. Hầu hết các điểm đánh dấu được theo sau bởi thông tin độ dài cho đoạn đánh dấu cụ thể. Điều này cho chúng ta biết đoạn cụ thể đó dài bao nhiêu.

# Bắt đầu tập tin và kết thúc tập tin

Điểm đánh dấu đầu tiên chúng tôi quan tâm là `FF D8`. Nó cho chúng ta biết đây là điểm bắt đầu của hình ảnh. Nếu không thấy nó, chúng ta có thể cho rằng đây là một tập tin khác. Một điểm đánh dấu quan trọng không kém khác là `FF D9`. Nó cho chúng ta biết rằng chúng ta đã đến cuối tệp hình ảnh. Mỗi điểm đánh dấu, ngoại trừ `FFD0` đến `FFD9` và `FF01`, ngay sau đó là bộ xác định độ dài sẽ cung cấp cho bạn độ dài của đoạn đánh dấu đó. Đối với các điểm đánh dấu bắt đầu và kết thúc tệp hình ảnh, mỗi điểm sẽ luôn dài hai byte.

Trong suốt hướng dẫn này, chúng ta sẽ làm việc với hình ảnh này:

![Reverse Engineering](https://boxxv.github.io/img/2024/profile.jpg "Reverse Engineering")

Hãy viết một số mã để xác định các điểm đánh dấu này.

```python
from struct import unpack

marker_mapping = {
    0xffd8: "Start of Image",
    0xffe0: "Application Default Header",
    0xffdb: "Quantization Table",
    0xffc0: "Start of Frame",
    0xffc4: "Define Huffman Table",
    0xffda: "Start of Scan",
    0xffd9: "End of Image"
}

class JPEG:
    def __init__(self, image_file):
        with open(image_file, 'rb') as f:
            self.img_data = f.read()
    
    def decode(self):
        data = self.img_data
        while(True):
            marker, = unpack(">H", data[0:2])
            print(marker_mapping.get(marker))
            if marker == 0xffd8:
                data = data[2:]
            elif marker == 0xffd9:
                return
            elif marker == 0xffda:
                data = data[-2:]
            else:
                lenchunk, = unpack(">H", data[2:4])
                data = data[2+lenchunk:]            
            if len(data)==0:
                break        

if __name__ == "__main__":
    img = JPEG('profile.jpg')
    img.decode()    

# OUTPUT:
# Start of Image
# Application Default Header
# Quantization Table
# Quantization Table
# Start of Frame
# Huffman Table
# Huffman Table
# Huffman Table
# Huffman Table
# Start of Scan
# End of Image
```

Chúng tôi đang sử dụng [struct](https://docs.python.org/3/library/struct.html) để giải nén các byte dữ liệu hình ảnh. `>H` yêu cầu `struct` xử lý dữ liệu ở dạng big endian và thuộc loại `unsigned short`. Dữ liệu trong JPEG được lưu trữ ở định dạng big-endian. Chỉ dữ liệu EXIF ​​có thể ở dạng endian nhỏ (mặc dù nó không phổ biến). Và một đoạn ngắn có kích thước 2 nên chúng tôi cung cấp giải nén hai byte từ img_data của chúng tôi. Bạn có thể tự hỏi làm sao chúng tôi biết đó là một đoạn ngắn. Chà, chúng ta biết rằng các điểm đánh dấu trong JPEG có 4 chữ số hex: `ffd8`. Một chữ số hex bằng 4 bit (1/2 byte) nên 4 chữ số hex sẽ bằng 2 byte và một chữ số ngắn bằng 2 byte.

Ngay sau phần Bắt đầu quét là dữ liệu quét hình ảnh và dữ liệu quét hình ảnh đó không có độ dài được chỉ định. Quá trình này tiếp tục cho đến khi tìm thấy điểm đánh dấu “cuối tập tin”, vì vậy hiện tại chúng tôi đang “tìm kiếm” thủ công điểm đánh dấu EOF bất cứ khi nào chúng tôi nhìn thấy điểm đánh dấu SOC.

Bây giờ chúng ta đã có khung cơ bản, hãy tiếp tục và tìm hiểu phần còn lại của dữ liệu hình ảnh chứa gì. Trước tiên chúng ta sẽ xem xét một số lý thuyết cần thiết và sau đó chuyển sang viết mã.

# Mã hóa JPEG

Đầu tiên tôi sẽ giải thích một số khái niệm cơ bản và kỹ thuật mã hóa được JPEG sử dụng, sau đó việc giải mã sẽ tự nhiên diễn ra theo hướng ngược lại. Theo kinh nghiệm của tôi, việc trực tiếp cố gắng hiểu ý nghĩa của việc giải mã là hơi khó.

Mặc dù hình ảnh bên dưới hiện không có nhiều ý nghĩa đối với bạn nhưng nó sẽ cung cấp cho bạn một số điểm neo để bạn giữ vững trong khi chúng ta thực hiện toàn bộ quá trình mã hóa/giải mã. Nó hiển thị các bước liên quan đến quá trình mã hóa JPEG: ([src](https://users.cs.cf.ac.uk/Dave.Marshall/Multimedia/node234.html))

![Reverse Engineering](https://boxxv.github.io/img/2024/encoding.png "Reverse Engineering")

# Không gian màu JPEG

Theo thông số JPEG ([ISO/IEC 10918-6:2013 (E)](www.itu.int/rec/T-REC-T.872-201206-I/en), mục 6.1):

> - Hình ảnh được mã hóa chỉ có một thành phần được coi là dữ liệu thang độ xám trong đó 0 là màu đen và 255 là màu trắng.
> - Hình ảnh được mã hóa bằng ba thành phần được coi là dữ liệu RGB được mã hóa dưới dạng YCbCr trừ khi hình ảnh chứa đoạn đánh dấu APP14 như được chỉ định trong 6.5.3, trong trường hợp đó, mã hóa màu được coi là RGB hoặc YCbCr theo dữ liệu ứng dụng của điểm đánh dấu APP14 bộ phận. Mối quan hệ giữa RGB và YCbCr được xác định như được chỉ định trong Rec. ITU-T T.871 | ISO/IEC 10918-5.
> - Hình ảnh được mã hóa với bốn thành phần được giả sử là CMYK, với (0,0,0,0) biểu thị màu trắng trừ khi hình ảnh chứa đoạn đánh dấu APP14 như được chỉ định trong 6.5.3, trong trường hợp đó mã hóa màu được coi là CMYK hoặc YCCK theo dữ liệu ứng dụng của đoạn đánh dấu APP14. Mối quan hệ giữa CMYK và YCCK được xác định như quy định tại Điều 7.

Hầu hết việc triển khai thuật toán JPEG đều sử dụng độ chói và sắc độ (mã hóa YUV) thay vì RGB. Điều này cực kỳ hữu ích trong JPEG vì mắt người khá kém trong việc nhìn thấy sự thay đổi độ sáng tần số cao trên một khu vực nhỏ nên về cơ bản chúng ta có thể giảm lượng tần số và mắt người sẽ không thể nhận ra sự khác biệt. Kết quả? Một hình ảnh được nén ở mức độ cao mà hầu như không bị giảm chất lượng.

Giống như mỗi pixel trong không gian màu RGB được tạo thành từ 3 byte dữ liệu màu (Đỏ, Xanh lục, Xanh lam), mỗi pixel trong YUV cũng sử dụng 3 byte nhưng nội dung mà mỗi byte biểu thị hơi khác nhau. Thành phần Y xác định độ sáng của màu (còn được gọi là độ chói hoặc độ sáng), trong khi thành phần U và V xác định màu (còn được gọi là sắc độ). Thành phần U đề cập đến lượng màu xanh lam và thành phần V đề cập đến lượng màu đỏ.

Định dạng màu này được phát minh khi TV màu chưa phổ biến và các kỹ sư muốn sử dụng một định dạng mã hóa hình ảnh cho cả TV màu và TV đen trắng. YUV có thể được hiển thị an toàn trên TV đen trắng nếu không có màu. Bạn có thể đọc thêm về lịch sử của nó trên [Wikipedia](https://www.wikiwand.com/en/YUV).

# Biến đổi và lượng tử hóa cosine rời rạc

JPEG chuyển đổi một hình ảnh thành các khối pixel 8x8 (được gọi là MCU hoặc Đơn vị mã hóa tối thiểu), thay đổi phạm vi giá trị của các pixel để chúng tập trung vào 0 và sau đó áp dụng Chuyển đổi Cosine rời rạc cho từng khối và sau đó sử dụng lượng tử hóa để nén khối kết quả. Chúng ta hãy hiểu ở mức độ cao hơn về ý nghĩa của tất cả các thuật ngữ này.

Biến đổi Cosine rời rạc là một phương pháp chuyển đổi các điểm dữ liệu rời rạc thành sự kết hợp của các sóng cosine. Có vẻ khá vô ích khi dành thời gian chuyển đổi một hình ảnh thành một loạt cos nhưng sẽ có ý nghĩa khi chúng ta hiểu DCT kết hợp với cách hoạt động của bước tiếp theo. Trong JPEG, DCT sẽ lấy một khối hình ảnh 8x8 và cho chúng ta biết cách tái tạo nó bằng ma trận 8x8 gồm các hàm cosine. Đọc thêm [tại đây](https://www.impulseadventure.com/photo/jpeg-minimum-coded-unit.html))

Ma trận 8x8 của hàm cosine trông như thế này:

![Reverse Engineering](https://boxxv.github.io/img/2024/cosine-funcs.png "Reverse Engineering")

Chúng tôi áp dụng DCT cho từng thành phần của pixel một cách riêng biệt. Đầu ra của việc áp dụng DCT là một ma trận hệ số 8x8 cho chúng ta biết mỗi hàm cosine (trong tổng số 64 hàm) đóng góp bao nhiêu vào ma trận đầu vào 8x8. Ma trận hệ số của DCT thường chứa các giá trị lớn hơn ở góc trên bên trái của ma trận hệ số và các giá trị nhỏ hơn ở góc dưới bên phải. Góc trên bên trái biểu thị hàm cosin tần số thấp nhất và góc dưới bên phải biểu thị hàm cosin tần số cao nhất.

Điều này cho chúng ta biết rằng hầu hết các hình ảnh đều chứa một lượng lớn thông tin tần số thấp và một lượng nhỏ thông tin tần số cao. Nếu chúng ta chuyển các thành phần dưới cùng bên phải của mỗi ma trận DCT về 0, hình ảnh thu được vẫn xuất hiện giống nhau vì như tôi đã đề cập, con người rất kém trong việc quan sát những thay đổi tần số cao. Đây chính xác là những gì chúng ta làm trong bước tiếp theo.

[https://youtu.be/Q2aEzeMDHMA](https://youtu.be/Q2aEzeMDHMA)

Tất cả chúng ta đều đã nghe nói rằng JPEG là một thuật toán nén có tổn hao nhưng cho đến nay chúng ta vẫn chưa thực hiện bất kỳ thuật toán nào có tổn hao. Chúng tôi chỉ chuyển đổi các khối thành phần YUV 8x8 thành các khối hàm cosin 8x8 mà không làm mất thông tin. Phần mất mát xuất hiện trong bước lượng tử hóa.

Lượng tử hóa là một quá trình trong đó chúng ta lấy một vài giá trị trong một phạm vi cụ thể và biến chúng thành một giá trị riêng biệt. Đối với trường hợp của chúng tôi, đây chỉ là một cái tên ưa thích để chuyển đổi các hệ số tần số cao hơn trong ma trận đầu ra DCT thành 0. Khi bạn lưu hình ảnh bằng JPEG, hầu hết các chương trình chỉnh sửa hình ảnh đều hỏi bạn cần nén bao nhiêu. Tỷ lệ phần trăm bạn cung cấp ở đó ảnh hưởng đến mức độ lượng tử hóa được áp dụng và lượng thông tin tần số cao hơn bị mất. Đây là nơi áp dụng nén mất mát. Khi bạn mất thông tin tần số cao, bạn không thể tạo lại hình ảnh gốc chính xác từ hình ảnh JPEG thu được.

Tùy thuộc vào mức độ nén được yêu cầu, một số ma trận lượng tử hóa phổ biến sẽ được sử dụng (sự thật thú vị: Hầu hết các nhà cung cấp đều có bằng sáng chế về xây dựng bảng lượng tử hóa). Chúng tôi chia phần tử ma trận hệ số DCT với ma trận lượng tử hóa, làm tròn kết quả thành một số nguyên và lấy ma trận lượng tử hóa. Hãy xem qua một ví dụ.

Nếu bạn có ma trận DCT này:

![Reverse Engineering](https://boxxv.github.io/img/2024/dct_matrix.png "Reverse Engineering")

Ma trận lượng tử hóa (phổ biến) này:

![Reverse Engineering](https://boxxv.github.io/img/2024/quant-matrix.png "Reverse Engineering")

Sau đó, ma trận lượng tử hóa kết quả sẽ là:

![Reverse Engineering](https://boxxv.github.io/img/2024/result_quant_matrix.png "Reverse Engineering")

Mặc dù con người không thể nhìn thấy thông tin tần số cao nhưng nếu bạn loại bỏ quá nhiều thông tin khỏi các khối hình ảnh 8x8 thì hình ảnh tổng thể sẽ trông có vẻ khối. Trong ma trận lượng tử hóa này, giá trị đầu tiên được gọi là giá trị DC và các giá trị còn lại là giá trị AC. Nếu chúng ta lấy các giá trị DC từ tất cả các ma trận lượng tử hóa và tạo ra một hình ảnh mới, về cơ bản chúng ta sẽ có một hình thu nhỏ có độ phân giải bằng 1/8 của hình ảnh gốc.

Cũng cần lưu ý rằng vì chúng tôi áp dụng lượng tử hóa trong khi giải mã nên chúng tôi sẽ phải đảm bảo màu sắc nằm trong phạm vi [0,255]. Nếu chúng nằm ngoài phạm vi này, chúng ta sẽ phải kẹp chúng vào phạm vi này theo cách thủ công.

# Zig-zag

Sau khi lượng tử hóa, JPEG sử dụng mã hóa zig-zag để chuyển đổi ma trận thành 1D ([img src](https://people.ece.cornell.edu/land/courses/ece5760/FinalProjects/f2009/jl589_jbw48/jl589_jbw48/index.html)):

![Reverse Engineering](https://boxxv.github.io/img/2024/zigzag.jpg "Reverse Engineering")

Hãy tưởng tượng chúng ta có ma trận lượng tử hóa này:

![Reverse Engineering](https://boxxv.github.io/img/2024/sample-quant.png "Reverse Engineering")

Đầu ra của mã hóa zig-zag sẽ là:

> [15 14 13 12 11 10 9 8 0  ...  0]

Mã hóa này được ưu tiên vì hầu hết thông tin tần số thấp (quan trọng nhất) được lưu trữ ở đầu ma trận sau khi lượng tử hóa và mã hóa zig-zag lưu trữ tất cả thông tin đó ở đầu ma trận 1D. Điều này rất hữu ích cho việc nén xảy ra ở bước tiếp theo.

# Mã hóa độ dài chạy và Delta

Mã hóa độ dài chạy được sử dụng để nén dữ liệu lặp lại. Khi kết thúc quá trình mã hóa zig-zag, chúng ta thấy hầu hết các mảng 1D được mã hóa zig-zag đều có rất nhiều số 0 ở cuối. Mã hóa độ dài thời gian chạy cho phép chúng tôi lấy lại tất cả không gian bị lãng phí đó và sử dụng ít byte hơn để biểu thị tất cả các số 0 đó. Hãy tưởng tượng bạn có một số dữ liệu như thế này:

> 10 10 10 10 10 10 10

Mã hóa độ dài chạy sẽ chuyển đổi nó thành:

> 7 10

Chúng tôi đã có thể nén thành công 7 byte dữ liệu thành 2 byte.

Mã hóa Delta là một kỹ thuật được sử dụng để biểu diễn một byte so với byte trước nó. Điều này dễ hiểu hơn bằng một ví dụ. Giả sử bạn có dữ liệu sau:

> 10 11 12 13 10 9

Bạn có thể sử dụng mã hóa delta để lưu trữ nó như thế này:

> 10 1  2  3  0 -1

Trong JPEG, mọi giá trị DC trong ma trận hệ số DCT được mã hóa delta so với giá trị DC trước nó. Điều này có nghĩa là nếu bạn thay đổi hệ số DCT đầu tiên của hình ảnh, toàn bộ hình ảnh sẽ bị sai lệch nhưng nếu bạn sửa đổi giá trị đầu tiên của ma trận DCT cuối cùng thì chỉ một phần rất nhỏ trong hình ảnh của bạn sẽ bị ảnh hưởng. Điều này rất hữu ích vì giá trị DC đầu tiên trong hình ảnh của bạn thường đa dạng nhất và bằng cách áp dụng mã hóa Delta, chúng tôi đưa các giá trị DC còn lại về gần 0 và điều đó dẫn đến khả năng nén tốt hơn trong bước tiếp theo của Mã hóa Huffman.

# Huffman Encoding

Mã hóa Huffman là một phương pháp nén thông tin không mất dữ liệu. Huffman từng tự hỏi: “Tôi có thể sử dụng bao nhiêu bit nhỏ nhất để lưu trữ một đoạn văn bản tùy ý?”. Định dạng mã hóa này là câu trả lời của anh ấy. Hãy tưởng tượng bạn phải lưu trữ văn bản này:

> a b c d e

Trong trường hợp bình thường, mỗi ký tự sẽ chiếm 1 byte dung lượng:

```
a: 01100001
b: 01100010
c: 01100011
d: 01100100
e: 01100101
```

Điều này dựa trên ASCII để ánh xạ nhị phân. Nhưng điều gì sẽ xảy ra nếu chúng ta có thể tạo ra một bản đồ tùy chỉnh?

```
# Mapping

000: 01100001
001: 01100010
010: 01100011
100: 01100100
011: 01100101
```

Bây giờ chúng ta có thể lưu trữ cùng một văn bản bằng cách sử dụng ít bit hơn:

```
a: 000
b: 001
c: 010
d: 100
e: 011
```

Điều này hoàn toàn tốt nhưng nếu chúng ta muốn chiếm ít không gian hơn thì sao? Điều gì sẽ xảy ra nếu chúng ta có thể làm được điều gì đó như thế này:

```
# Mapping
0:  01100001
1:  01100010
00: 01100011
01: 01100100
10: 01100101

a: 0
b: 1
c: 00
d: 01
e: 10
```

Mã hóa Huffman cho phép chúng ta sử dụng loại ánh xạ có độ dài thay đổi này. Nó lấy một số dữ liệu đầu vào, ánh xạ các ký tự thường xuyên nhất sang các mẫu bit nhỏ hơn và các ký tự ít thường xuyên nhất thành các mẫu bit lớn hơn và cuối cùng tổ chức ánh xạ thành cây nhị phân. Trong JPEG, chúng tôi lưu trữ thông tin DCT (Biến đổi Cosine rời rạc) bằng cách sử dụng mã hóa Huffman. Hãy nhớ rằng tôi đã nói với bạn rằng việc sử dụng mã hóa delta cho các giá trị DC sẽ giúp ích cho Mã hóa Huffman? Tôi hy vọng bây giờ bạn có thể hiểu tại sao. Sau khi mã hóa delta, chúng tôi thu được ít “ký tự” hơn để ánh xạ và tổng kích thước của cây Huffman của chúng tôi giảm xuống.

Tom Scott có một video tuyệt vời kèm theo hình ảnh động về cách hoạt động của mã hóa Huffman nói chung. Hãy xem nó trước khi tiếp tục.

[https://youtu.be/JsTptu56GM8](https://youtu.be/JsTptu56GM8)

Một JPEG chứa tối đa 4 bảng Huffman và những bảng này được lưu trữ trong phần “Xác định bảng Huffman” (bắt đầu bằng 0xffc4). Các hệ số DCT được lưu trữ trong 2 bảng Huffman khác nhau. Một cái chỉ chứa các giá trị DC từ các bảng zig-zag và cái kia chứa các giá trị AC từ các bảng zig-zag. Điều này có nghĩa là trong quá trình giải mã, chúng ta sẽ phải hợp nhất các giá trị DC và AC từ hai ma trận riêng biệt. Thông tin DCT cho kênh độ chói và sắc độ được lưu trữ riêng biệt nên chúng ta có 2 bộ thông tin DC và 2 bộ thông tin AC, cung cấp cho chúng ta tổng cộng 4 bảng Huffman.

Trong ảnh thang độ xám, chúng ta sẽ chỉ có 2 bảng Huffman (1 cho DC và 1 cho AC) vì chúng ta không quan tâm đến màu sắc. Như bạn có thể tưởng tượng, 2 hình ảnh có thể có các bảng Huffman rất khác nhau nên điều quan trọng là phải lưu trữ các bảng này bên trong mỗi JPEG.

Vì vậy, chúng tôi biết các chi tiết cơ bản về nội dung của hình ảnh JPEG. Hãy bắt đầu với việc giải mã!

# Giải mã JPEG

Chúng ta có thể chia quá trình giải mã thành nhiều bước:

- Trích xuất bảng Huffman và giải mã các bit
- Trích xuất các hệ số DCT bằng cách hoàn tác mã hóa độ dài chạy và delta
- Sử dụng hệ số DCT để kết hợp sóng cosine và tái tạo giá trị pixel cho mỗi khối 8x8
- Chuyển đổi YCbCr sang RGB cho mỗi pixel
- Hiển thị hình ảnh RGB thu được

Chuẩn JPEG hỗ trợ 4 định dạng nén:

- Đường cơ sở
- Trình tự mở rộng
- Cấp tiến
- Không mất mát

Chúng ta sẽ làm việc với tính năng nén Đường cơ sở và theo tiêu chuẩn, đường cơ sở sẽ chứa một chuỗi các khối 8x8 ngay cạnh nhau. Các định dạng nén khác bố trí dữ liệu hơi khác một chút. Chỉ để tham khảo, tôi đã tô màu các phân đoạn khác nhau trong nội dung hex của hình ảnh mà chúng tôi đang sử dụng. Cái này nó thì trông như thế nào:

![Reverse Engineering](https://boxxv.github.io/img/2024/profile-img-hex.png "Reverse Engineering")

# Trích xuất bảng Huffman






# Tổng kết

Chúc bạn thành công!

-----
Tham khảo:
- [Decoding binary data structure](https://reverseengineering.stackexchange.com/questions/15969/decoding-binary-data-structure)
- [Understanding and Decoding a JPEG Image using Python](https://yasoob.me/posts/understanding-and-writing-jpeg-decoder-in-python/)
- [DCode™ – Timestamp Decoder](https://www.digital-detective.net/dcode/)
- [图片的 Metadata 与网站性能优化](https://github.com/shfshanyue/blog/blob/master/web-performance/image-metadata.md)
