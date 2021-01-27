---
layout: post
title: Hiển thị 3D trong JavaScript với Three.js
subtitle: JavaScript in 3D with Three.js
tags:
- Three.js
- Threejs
- JavaScript
- 3D
---


-----
## Materials
_Vật liệu, Chất liệu_

Hình học xác định hình dạng của các đối tượng 3D của chúng ta, nhưng không xác định hình dạng của chúng. Để làm được điều đó, chúng ta cần thêm một `material`

Three.js đi kèm với 10 `mesh materials`, mỗi material có những ưu điểm và đặc tính có thể tùy chỉnh riêng. Chúng tôi sẽ xem xét một số ít những điều hữu ích nhất.

![Materials](http://boxxv.com/img/posts/material.png "Materials")_Materials_


-----
### MeshNormalMaterial
Hữu ích cho: _thiết lập và chạy nhanh chóng_

[https://threejs.org/docs/index.html#api/en/materials/MeshNormalMaterial](https://threejs.org/docs/index.html#api/en/materials/MeshNormalMaterial)


Chúng tôi sẽ bắt đầu với `MeshNormalMaterial`, vật liệu nhiều màu mà chúng tôi đã sử dụng trong các ví dụ cho đến nay. Nó ánh xạ các vectơ thông thường sang màu RGB: nói cách khác, nó sử dụng màu sắc để phân biệt vị trí của vectơ trong không gian 3D.

```javascript
const material = new THREE.MeshNormalMaterial();
```

Lưu ý rằng, nếu bạn muốn thay đổi màu sắc của MeshNormalMaterial, bạn có thể chỉ cần sử dụng bộ lọc CSS và thay đổi màu sắc: ví dụ: `filter: hue-rotate(90deg)`.

Theo kinh nghiệm của tôi, `MeshNormalMaterial` hữu ích nhất để bắt đầu và vận hành nhanh chóng. Để kiểm soát nhiều hơn giao diện của các đối tượng, tốt nhất bạn nên sử dụng một thứ khác.


-----
### MeshBasicMaterial
Hữu ích cho: _wireframes_

[https://threejs.org/docs/index.html#api/en/materials/MeshBasicMaterial](https://threejs.org/docs/index.html#api/en/materials/MeshBasicMaterial)

Nếu bạn muốn đối tượng của mình có màu đồng nhất, bạn có thể sử dụng `MeshBasicMaterial`, vì nó không bị ảnh hưởng bởi ánh sáng. Tôi thấy điều này hữu ích cho wireframe. Để sử dụng chế độ wireframe, chỉ cần chuyển `{wireframe: true}` làm đối số. 

```javascript
const material = new THREE.MeshBasicMaterial({ 
  wireframe: true, 
  color: 0xdaa520
});
```

[Demo](https://codepen.io/BretCameron/pen/ZEzwERw?editors=0010)

Nhược điểm của `MeshBasicMaterial` là nó không cung cấp manh mối về độ sâu của vật liệu. Mọi vật liệu đều có các tùy chọn để tạo khung dây, nhưng một giải pháp hiệu quả bao gồm chiều sâu là `MeshDepthMaterial`.



-----
### MeshLambertMaterial
Hữu ích cho: **hiệu suất cao** _(nhưng độ chính xác thấp hơn)_

[https://threejs.org/docs/index.html#api/en/materials/MeshLambertMaterial](https://threejs.org/docs/index.html#api/en/materials/MeshLambertMaterial)

Đây là vật liệu đầu tiên bị ảnh hưởng bởi ánh sáng, vì vậy, để xem những gì chúng tôi đang làm, chúng tôi sẽ cần thêm một số ánh sáng vào cảnh của chúng tôi. Trong đoạn mã dưới đây, chúng tôi sẽ thêm vào đèn sân khấu, với một chút màu vàng để tạo hiệu ứng ấm hơn: 

```javascript
const scene = new THREE.Scene();

const frontSpot = new THREE.SpotLight(0xeeeece);
frontSpot.position.set(1000, 1000, 1000);
scene.add(frontSpot);

const frontSpot2 = new THREE.SpotLight(0xddddce);
frontSpot2.position.set(-500, -500, -500);
scene.add(frontSpot2);
```

Bây giờ, hãy thêm `material` cho hình dạng của chúng ta. Vì nó trông hơi giống một món đồ trang sức, tôi nghĩ tôi sẽ chọn màu vàng. Thuộc tính khác, `emissive`, là màu sắc mà vật thể phát ra từ chính nó (không có bất kỳ nguồn sáng nào). Thông thường, nó hoạt động tốt nhất khi có màu tối - chẳng hạn như bóng tối của màu xám, như bên dưới:

```javascript
const material = new THREE.MeshLambertMaterial({
  color: 0xdaa520,
  emissive: 0x111111,
});
```

[https://codepen.io/BretCameron/pen/OJLdJGz](https://codepen.io/BretCameron/pen/OJLdJGz?editors=0010)

Như bạn có thể thấy trong ví dụ bên dưới, màu sắc ít nhiều đều đúng, nhưng cách nó tương tác với ánh sáng không tạo ra vẻ ngoài chân thực nhất. Để làm được điều đó, chúng ta sẽ cần sử dụng `MeshPhongMaterial` hoặc `MeshStandardMaterial`.


-----
### MeshPhongMaterial
Hữu ích cho: _hiệu suất và độ chính xác trung bình_

[https://threejs.org/docs/index.html#api/en/materials/MeshPhongMaterial](https://threejs.org/docs/index.html#api/en/materials/MeshPhongMaterial)

Vật liệu này mang lại sự dung hòa giữa hiệu suất và hình thức, và do đó nó là điểm trung gian tốt cho các ứng dụng cần hiệu suất cao đồng thời đạt được mức chất lượng cao hơn `MeshLambertMaterial`.

Giờ đây, chúng tôi có thể thay đổi một thuộc tính mới, `specular`, xác định độ sáng và màu sắc của hệ số phản xạ của bề mặt. Trong khi đặc tính `emissive` thường có màu tối, đặc tính `specular` thường hoạt động tốt nhất khi có màu sáng. Bên dưới, chúng tôi đang sử dụng màu xám nhạt: 

```javascript
const material = new THREE.MeshPhongMaterial({
  color: 0xdaa520,
  emissive: 0x000000,
  specular: 0xbcbcbc,
});
```

[https://codepen.io/BretCameron/pen/YzKBwwQ](https://codepen.io/BretCameron/pen/YzKBwwQ?editors=0010)

Về mặt trực quan, hình ảnh trên phản chiếu ánh sáng theo cách thuyết phục hơn nhiều, nhưng nó vẫn chưa hoàn hảo. Ánh sáng trắng hơi quá sáng và vật liệu trông giống như cao su hơn là kim loại (hiệu ứng mong muốn của chúng tôi). Chúng ta có thể có được kết quả tốt hơn bằng cách sử dụng `MeshStandardMaterial`.


-----
### MeshStandardMaterial
Hữu ích cho: **độ chính xác cao** _(nhưng hiệu suất thấp hơn)_

[https://threejs.org/docs/index.html#api/en/materials/MeshStandardMaterial](https://threejs.org/docs/index.html#api/en/materials/MeshStandardMaterial)

Đây là vật liệu có độ chính xác cao nhất trong số các vật liệu của Three.js, mặc dù nó phải trả giá bằng công suất xử lý lớn hơn. `MeshStandardMaterial` đi kèm với một số đặc tính bổ sung - `metalness` (tính kim loại) và `roughness` (độ nhám), cả hai đều có giá trị từ `0` đến `1`. 

Đặc tính kim loại `metalness` làm thay đổi cách phản xạ của đối tượng để nó có bản chất gần hơn với kim loại. Điều này là do các vật liệu dẫn điện, như kim loại, có đặc tính phản xạ khác với vật liệu điện môi, như gốm sứ.

Độ nhám `roughness` thêm một lớp tùy chỉnh khác. Bạn có thể nghĩ nó ngược lại với độ bóng: giá trị `0` là cực kỳ bóng, trong khi giá trị `1` là cực kỳ thô (có nghĩa là rất ít ánh sáng bị phản chiếu).

```javascript
const material = new THREE.MeshStandardMaterial({
  color: 0xfcc742,
  emissive: 0x111111,
  specular: 0xffffff,
  metalness: 1,
  roughness: 0.55,
});
```




-----
Tham khảo:
- [JavaScript in 3D: an Introduction to Three.js](https://medium.com/javascript-in-plain-english/javascript-in-3d-an-introduction-to-three-js-780f1e4a2e6d)