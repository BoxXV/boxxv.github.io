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



## Materials
_Vật liệu, Chất liệu_

Hình học xác định hình dạng của các đối tượng 3D của chúng ta, nhưng không xác định hình dạng của chúng. Để làm được điều đó, chúng ta cần thêm một `material`

Three.js đi kèm với 10 `mesh materials`, mỗi material có những ưu điểm và đặc tính có thể tùy chỉnh riêng. Chúng tôi sẽ xem xét một số ít những điều hữu ích nhất.

![Materials](http://boxxv.com/img/posts/material.png "Materials")_Materials_


### MeshNormalMaterial
Hữu ích cho: _thiết lập và chạy nhanh chóng_

[https://threejs.org/docs/index.html#api/en/materials/MeshNormalMaterial](https://threejs.org/docs/index.html#api/en/materials/MeshNormalMaterial)


Chúng tôi sẽ bắt đầu với `MeshNormalMaterial`, vật liệu nhiều màu mà chúng tôi đã sử dụng trong các ví dụ cho đến nay. Nó ánh xạ các vectơ thông thường sang màu RGB: nói cách khác, nó sử dụng màu sắc để phân biệt vị trí của vectơ trong không gian 3D.

```javascript
const material = new THREE.MeshNormalMaterial();
```

Lưu ý rằng, nếu bạn muốn thay đổi màu sắc của MeshNormalMaterial, bạn có thể chỉ cần sử dụng bộ lọc CSS và thay đổi màu sắc: ví dụ: `filter: hue-rotate(90deg)`.

Theo kinh nghiệm của tôi, `MeshNormalMaterial` hữu ích nhất để bắt đầu và vận hành nhanh chóng. Để kiểm soát nhiều hơn giao diện của các đối tượng, tốt nhất bạn nên sử dụng một thứ khác.


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


### MeshLambertMaterial
Hữu ích cho: **hiệu suất cao** _(nhưng độ chính xác thấp hơn)_

[https://threejs.org/docs/index.html#api/en/materials/MeshLambertMaterial](https://threejs.org/docs/index.html#api/en/materials/MeshLambertMaterial)




### MeshPhongMaterial
Hữu ích cho: _hiệu suất và độ chính xác trung bình_

[https://threejs.org/docs/index.html#api/en/materials/MeshPhongMaterial](https://threejs.org/docs/index.html#api/en/materials/MeshPhongMaterial)



### MeshStandardMaterial
Hữu ích cho: **độ chính xác cao** _(nhưng hiệu suất thấp hơn)_

[https://threejs.org/docs/index.html#api/en/materials/MeshStandardMaterial](https://threejs.org/docs/index.html#api/en/materials/MeshStandardMaterial)





-----
Tham khảo:
- [JavaScript in 3D: an Introduction to Three.js](https://medium.com/javascript-in-plain-english/javascript-in-3d-an-introduction-to-three-js-780f1e4a2e6d)