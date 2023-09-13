---
layout: post
title: Lộ trình học Machine Learning Cơ Bản đến Nâng Cao
subtitle: Artificial Intelligence - A Comprehensive Guide
author: "TAn"
image: "img/lonely.jpg"
tags:
- Python
- Scripting
- Data Science
- Machine Learning
- Big Data
- Hadoop
- MapReduce
- TensorFlow
- Scikit-Learn
- NumPy
- Keras
- PyTorch
- SciPy
- Pandas
- Matplotlib
- Seaborn
- Bokeh
- Pillow
- Data Analyst
- Chuyên viên Phân tích Dữ liệu
- Data Scientist
- Nhà Khoa học Dữ liệu
- Machine Learning Engineer
- Kĩ sư Học máy
- Artificial Intelligence Engineer
- Kĩ sư Trí tuệ Nhân tạo
---

# Mục lục

- [Mục lục](#mục-lục)
- [Sự khác nhau giữa AI, ML, DL](#sự-khác-nhau-giữa-ai-ml-dl)
	- [Aritifical Intelligient](#aritifical-intelligient)
	- [Machine learning](#machine-learning)
	- [Học sâu (Deep learning)](#học-sâu-deep-learning)
- [Ứng dụng của học máy](#ứng-dụng-của-học-máy)
	- [Ứng dụng cụ thể](#ứng-dụng-cụ-thể)
	- [Các dạng học máy](#các-dạng-học-máy)
		- [Học có giám sát (supervised learning)](#học-có-giám-sát-supervised-learning)
		- [Học không giám sát (un-supervised learning)](#học-không-giám-sát-un-supervised-learning)
		- [Học bán giám sát (semi-supervised learning)](#học-bán-giám-sát-semi-supervised-learning)
		- [Học tăng cường (reinforcement learning)](#học-tăng-cường-reinforcement-learning)
- [Lộ trình học machine learning](#lộ-trình-học-machine-learning)
- [Tổng kết](#tổng-kết)


Trí tuệ nhân tạo (Aritifical Intelligient), Máy học (Machine learning), Học sâu (Deep Learning) là 3 thuật ngữ rất hot trong những năm gần đây.

# Sự khác nhau giữa AI, ML, DL

## Aritifical Intelligient

AI đã tồn tại trong một thời gian dài - thần thoại Hy lạp có những câu chuyện về những người máy được thiết kế để bắt chước các hành động của chúng ta. Rất sớm ở châu âu các máy tính được hình thành được gọi là "máy logic" và bằng cách tái tạo các khả năng như số học cơ bản và bộ nhớ, về cơ bản là cố gắng tạo ra một bộ não cơ học.

Được định nghĩa vào năm 1956 bởi John MacCarthy, AI bao gồm các máy có thể thực hiện các tác vụ mà có các đặc trưng của trí thông minh của con người.

AI thường được phân loại thành 1 trong 2 nhóm cơ bản - **Applied** hoặc **General**
- `Applied AI` rất phổ biến, là các hệ thống được thiết kế để giao dịch chứng khoán và cổ phiếu một cách thông minh, hoặc tự điều khiển một chiếc xe, ...
- `Generalized AI` ít phổ biến hơn, là các hệ thống hoặc các thiết bị về lý thuyết có thể xử lý mọi tác vụ, nhưng đây là nơi mà những sự tiến bộ thú vị nhất đang diễn ra hiện nay. Nó cũng là nơi dẫn đến sự phát triển của ML

## Machine learning

Về cơ bản, máy học đơn giản là cách để đạt được AI.

Được định nghĩa bởi Arthur Samuel vào năm 1959, không lâu sau khi AI được định nghĩa. Nó được định nghĩa "là khả năng để máy tự học mà không cần phải lập trình". 

Bạn có thể có AI mà không cần dùng ML, nhưng sẽ cần hàng triệu dòng code để xây dựng với các quy tắc phức tạp và các cây quyết định.

Do vậy thay cho việc code các chương trình phần mềm với các chỉ dẫn cụ thể để hoàn thành một nhiệm vụ cụ thể, thì ML là một cách đào tạo một thuật toán để nó biết cách học. 

Đào tạo bao gồm việc cho thuật toán truy xuất vào một khối lượng lớn dữ liệu và cho phép thuật toán tự phân tích, điều chỉnh và cải thiện.

Ví dụ: ML được dùng để cải tiến mạnh mẽ tầm nhìn của máy tính (khả năng của máy có thể nhận ra một đối tượng trong ảnh hoặc video). 

Bạn thu thập hàng trăm, hàng nghìn thậm chí là hàng triệu bức ảnh và sau đó cho con người phân loại chúng. Ở đây, con người có thể phân loại các bức ảnh thành 2 nhóm là nhóm có mèo và nhóm ko có mèo, xuất hiện trong ảnh.

Sau đó thuật toán sẽ xây dựng một model có thể phân loại chính xác bức ảnh nào có mèo hay ko có mèo, giống như con người. 

Một khi mà độ chính xác đủ cao thì lúc đó ML đã học được đâu là con mèo.

## Học sâu (Deep learning)

DL là một trong nhiều cách để tiếp cận đến ML. 

Các cách tiếp cận khác bao gồm cây học tập quyết đinh (decision tree learning), lập trình logic quy nạp (inductive logic programming), phân cụm (clustering), học tăng cường (reinforcement learning), và mạng Bayesian, ...

DL được lấy cảm hứng từ cấu trúc và chức năng của bộ não, ở đây là sự kết nối của các tế bào thần kinh.

Mạng thần kinh nhân tạo (Artifical Neural Networks - ANNs) là thuật toán mô phỏng cấu trúc sinh học của bộ não. Trong ANNs, có các neuron thần kinh có các lớp riêng rẽ và được kết nối với các neuron khác. 

Sự phát triển của neural network là chìa khóa để dạy máy tính nghĩ và hiểu thế giới như cách của chúng ta làm, trong khi vẫn giữ được những lợi thế như tốc độ, độ chính xác và thiếu thiên hướng.

Về cơ bản nó làm việc trên một hệ thống xác suất - dựa trên dữ liệu được cung cấp, nó có thể đưa ra các tuyên bố, quyết định hoặc tiên đoán với một mức độ chắc chắn. Việc bổ sung một vòng lặp phản hồi cho phép học - bằng cách tự nhận biết hoặc được cho biết là quyết định đúng hay sai, nó sẽ thay đổi cách tiếp cận trong tương lai.



# Ứng dụng của học máy

Có rất nhiều ứng dụng thực tế khác nhau của học máy. Hai lĩnh vực ứng dụng lớn nhất của học máy là khai phá dữ liệu (`Data Mining`) và nhận dạng mẫu (`Pattern Recognition`).

**Khai phá dữ liệu** là ứng dụng kỹ thuật học máy vào các cơ sở dữ liệu hoặc các tập dữ liệu lớn để phát hiện quy luật hay tri thức trong dữ liệu đó hoặc để dự đoán các thông tin quan tâm trong tương lai. Ví dụ, từ tập hợp hóa đơn bán hàng có thể phát hiện ra quy luật “những người mua bánh mì thường mua bơ”.

**Nhận dạng mẫu** là ứng dụng các kỹ thuật học máy để phát hiện các mẫu có tính quy luật trong dữ liệu, thường là dữ liệu hình ảnh, âm thanh. Bài toán nhận dạng mẫu cụ thể thường là xác định nhãn cho đầu vào cụ thể, ví dụ cho ảnh chụp mặt người, cần xác định đó là ai.

Cần lưu ý, khai phá dữ liệu và nhận dạng mẫu có nhiều điểm trùng nhau cả trong phạm vi nghiên cứu và ứng dụng. Điểm khác nhau chủ yếu liên quan tới lĩnh vực ứng dụng và kỹ thuật sử dụng, theo đó khai phá dữ liệu liên quan tới dữ liệu thương mại trong khi nhận dạng mẫu liên quan nhiều tới dữ liệu âm thanh, hình ảnh và được dùng nhiều trong kỹ thuật.

## Ứng dụng cụ thể

- Nhận dạng ký tự: phân loại hình chụp ký tự thành các loại, mỗi loại ứng với một ký tự tương ứng.
- Phát hiện và nhận dạng mặt người: phát hiện vùng có chứa mặt người trong ảnh, xác định đó là mặt người nào trong số những người đã có ảnh trước đó, tức là phân chia ảnh thành những loại tương ứng với những người khác nhau.
- Lọc thư rác, phân loại văn bản: dựa trên nội dung thư điện tử, chia thư thành loại “thư rác” hay “thư bình thường”; hoặc phân chia tin tức thành các thể loại khác nhau như “xã hội”, “kinh tế”, “thể thao”.v.v.
- Dịch tự động: dựa trên dữ liệu huấn luyện dưới dạng các văn bản song ngữ, hệ thống dịch tự động học cách dịch từ ngôn ngữ này sang ngôn ngữ khác. Hệ thống dịch tự động tiêu biểu dạng này là Google Translate.
- Chẩn đoán y tế: học cách dự đoán người bệnh có mắc hay không mắc một số bệnh nào đó dựa trên triệu chứng quan sát được.
- Phân loại khách hàng và dự đoán sở thích: sắp xếp khách hàng vào một số loại, từ đây dự đoán sở thích tiêu dùng của khách hàng.
- Dự đoán chỉ số thí trường: căn cứ giá trị một số tham số hiện thời và trong lịch sử, đưa ra dự đoán, chẳng hạn dự đoán giá chứng khoán, giá vàng.v.v.
- Các hệ khuyến nghị, hay hệ tư vấn lựa chọn: cung cấp một danh sách ngắn các loại hàng hóa, phim, video, tin tức v.v. mà người dùng nhiều khả năng quan tâm. Ví dụ ứng dụng loại này là phần khuyến nghị trên Youtube hay trên trang mua bán trực tuyến Amazon.
- Ứng dụng lái xe tự động: dựa trên các mẫu học chứa thông tin về các tình huống trên đường, hệ thống học máy cho phép tự ra quyết định điều khiển xe, và do vậy không cần người lái. Hiện Google đã có kế hoạch thương mại hóa xe ôtô tự động lái như vậy.

![AI](https://boxxv.github.io/img/ai/machine-learning.png "AI")

## Các dạng học máy

Khi thiết kế và xây dựng hệ thống học máy cần quan tâm tới những yếu tố sau.
– Thứ nhất, kinh nghiệm hoặc dữ liệu cho học máy được cho dưới dạng nào?
– Thứ hai, lựa chọn biểu diễn cho hàm đích ra sao? Hàm đích có thể biểu diễn dưới dạng hàm đại số thông thường nhưng cũng có thể biểu diễn dưới những dạng khác như dạng cây, dạng mạng nơ ron, công thức xác suất .v.v.

Việc sử dụng những dạng kinh nghiệm và dạng biểu diễn khác nhau dẫn tới những dạng học máy khác nhau. Có ba dạng học máy chính như sau:

### Học có giám sát (supervised learning)

Là dạng học máy trong đó cho trước tập dữ liệu huấn luyện dưới dạng các ví dụ cùng với giá trị đầu ra hay giá trị đích. Dựa trên dữ liệu huấn luyện, thuật toán học cần xây dựng mô hình hay hàm đích để dự đoán giá trị đầu ra (giá trị đích) cho các trường hợp mới.

- Nếu giá trị đầu ra là rời rạc thì học có giám sát được gọi là phân loại hay phân lớp (classification).
- Nếu đầu ra nhận giá trị liên tục, tức đầu ra là số thực, thì học có giám sát được gọi là hồi quy (regression). Trong phần tiếp theo, ta sẽ xem xét chi tiết hơn về học có giám sát.

### Học không giám sát (un-supervised learning)

Là dạng học máy trong đó các ví dụ được cung cấp nhưng không có giá trị đầu ra hay giá trị đích.

- Thay vì xác định giá trị đích, thuật toán học máy dựa trên độ tương tự giữa các ví dụ để xếp chúng thành những nhóm, mỗi nhóm gồm các ví dụ tương tự nhau. Hình thức học không giám sát như vậy gọi là phân cụm (clustering). Ví dụ, chỉ bằng cách quan sát hoặc đo chiều cao của mọi người, dần dần ta học được khái niệm “người cao” và “người thấp”, và có thể xếp mọi người vào hai cụm tương ứng.
- Ngoài phân cụm, một dạng học không giám sát phổ biến khác là phát hiện luật kết hợp (association rule). Luật kết hợp có dạng P(A | B), cho thấy xác suất hai tính chất A và B xuất hiện cùng với Ví dụ, qua phân tích dữ liệu mua hàng ở siêu thị, ta có luật P(Bơ | Bánh mỳ) =80%, có nghĩa là 80% những người mua bánh mỳ cũng mua bơ.

### Học bán giám sát (semi-supervised learning)

Học bán giám sát là việc chúng ta có một khối lượng dữ liệu đầu vào (input) mà chỉ một phần trong đó là các dữ liệu được gắn nhãn. Học bán giám sát nằm ở giữa hai loại học có giám sát và học không giám sát. Bài toán này thường phát sinh trong thực tế bởi các dữ liệu hầu như hiếm khi được gắn nhãn toàn bộ, các dữ liệu gắn nhãn thường tốn nhiều thời gian và chi phí hơn so với các dữ liệu không gắn nhãn.

### Học tăng cường (reinforcement learning)

Đối với dạng học này, kinh nghiệm không được cho trực tiếp dưới dạng đầu vào/đầu ra cho mỗi trạng thái hoặc mỗi hành động. Thay vào đó, hệ thống nhận được một giá trị khuyến khích (reward) là kết quả cho một chuỗi hành động nào đó. Thuật toán cần học cách hành động để cực đại hóa giá trị khuyển khích. Ví dụ của học khuyến khích là học đánh cờ, trong đó hệ thống không được chỉ dẫn nước đi nào là hợp lý cho từng tình huống mà chỉ biết kết quả toàn ván cờ. Như vậy, các chỉ dẫn về nước đi được cho một cách gián tiến và có độ trễ dưới dạng giá trị thưởng. Nước đi tốt là nước đi nằm trong một chuỗi các nước đi dẫn tới kết quả thắng toàn bộ ván cờ.

Trong các dạng học máy, học có giám sát là dạng phổ biến, có nhiều thuật toán liên quan và nhiều ứng dụng nhất.

# Lộ trình học machine learning

![AI](https://boxxv.github.io/img/2023/ai-data-scientist.jpg "AI")

- Các kiến thức về toán học căn bản
   + Xác xuất thống kê
   + Giải tích
   + Đại số tuyến tính
   + vector, ma trận, đạo hàm (chain rule và production rule)
   + xác suất sử dụng không gian mẫu, xác suất có điều kiện, biến ngẫu nhiên, phân phối xác xuất...
- Kỹ năng về ngôn ngữ lập trình
   + Python
   + R
   + Lisp
   + Prolog
   + Java
- Xây dựng được các model cơ bản
   + NumPy
   + Keras
   + Tensoflow
   + Scikit Learn
- Tìm hiểu về Machine Learning thông qua các khoá học online và offline
- Trao đổi và luyện tập trên các diễn đàn
   + Github
   + Stack Overflow
   + Dev.to
   + Quora

# Tổng kết


-----
Tham khảo
- [Sự khác nhau giữa AI, ML, DL](https://www.linkedin.com/pulse/s%E1%BB%B1-kh%C3%A1c-nhau-gi%E1%BB%AFa-ai-ml-dl-hu%C3%A2n-b%C3%B9i-%C4%91%C3%ACnh)
- [Học máy (machine learning) là gì? Ứng dụng và phân loại](https://lytuong.net/hoc-may-machine-learning-la-gi/)
- [Lộ Trình Học Machine Learning Python Cho Newbies](https://www.mcivietnam.com/blog-detail/lo-trinh-hoc-python-machine-learning-cho-newbies/)
- []()
- [Hướng dẫn toàn diện về Trí tuệ nhân tạo với Python (Dịch.p1)](https://viblo.asia/p/huong-dan-toan-dien-ve-tri-tue-nhan-tao-voi-python-dichp1-eW65G8nxKDO)
    1. Why Is Python Best For AI?
    2. Demand for AI
    3. What Is Artificial Intelligence?
    4. Types Of Artificial Intelligence
- [Hướng dẫn toàn diện về Trí tuệ nhân tạo với Python (Dịch.p2)](https://viblo.asia/p/huong-dan-toan-dien-ve-tri-tue-nhan-tao-voi-python-dichp2-eW65G89LKDO)
    1. Machine Learning Basics
    2. Types Of Machine Learning
    3. What Problems Can Machine Learning Solve?
    4. Machine Learning Process Steps
- [Hướng dẫn toàn diện về Trí tuệ nhân tạo với Python (Dịch.p3)](https://viblo.asia/p/huong-dan-toan-dien-ve-tri-tue-nhan-tao-voi-python-dichp3-gDVK2mbA5Lj)
    1. Machine Learning With Python
    2.  Limitations Of Machine Learning
    3.  Why Deep Learning?
    4.  How Deep Learning Works?
    5.  What Is Deep Learning?
    6.  Deep Learning Use Case
    7.  What Is A Perceptron?
    8.  Multilayer Perceptrons
- [Hướng dẫn toàn diện về Trí tuệ nhân tạo với Python (Dịch.p4)](https://viblo.asia/p/huong-dan-toan-dien-ve-tri-tue-nhan-tao-voi-python-dichp4-Ljy5VyqVlra)
    1.  Deep Learning With Python
    2.  Introduction To Natural Language Processing (NLP)
    3.  Natural Language Processing Applications
    4.  Thuật ngữ trong xử lý ngôn ngữ tự nhiên
- [Artificial Intelligence With Python: A Comprehensive Guide](https://www.edureka.co/blog/artificial-intelligence-with-python/)
- [Machine Learning hoạt động như thế nào? Thần thoại và sự thật](https://viblo.asia/p/machine-learning-hoat-dong-nhu-the-nao-than-thoai-va-su-that-bJzKm76rl9N)
- [Fact vs. Fiction: How Does Machine Learning Actually Work?](https://www.expert.ai/blog/how-does-machine-learning-work/)
- [Soon We Won't Program Computers. We'll Train Them Like Dogs](https://www.wired.com/2016/05/the-end-of-code/)
- [IBM Watson | Full Q&A | Oxford Union](https://youtu.be/rXVoRyIGGhU)
- [Lộ Trình Tự Học Lập Trình PYTHON Cho Người Mới Bắt Đầu](https://youtu.be/O5AsvA9OGhM)
- [Lập Trình Cơ Bản PYTHON Tự Học Cho Người Mới Bắt Đầu](https://youtu.be/oFgg7K2tpfk)
- [Khóa học lập trình Python miễn phí. Đăng ký, Download Free](https://chiasepremium.com/khoa-hoc-lap-trinh-python-mien-phi/)

Video
- [AI For Everyone - Andrew Ng](https://www.coursera.org/learn/ai-for-everyone)
- [Machine learning Vietsub - Andrew Ng](https://www.youtube.com/playlist?list=PLDpRz2wA0qZzTcDLeXP5PSCfmQ96l9-Qr)
- [Tự Học Data Science Cho Người Mới Bắt Đầu](https://www.youtube.com/playlist?list=PLJcWUrckOCKKwjjHALg6fnyQCHv8z92rs)
- []()

Thực hành
- [Chihuahua or muffin? My search for the best computer vision API](https://www.freecodecamp.org/news/chihuahua-or-muffin-my-search-for-the-best-computer-vision-api-cbda4d6b425d/)