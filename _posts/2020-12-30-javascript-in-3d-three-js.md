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



### Materials
_Vật liệu, Chất liệu_

Hình học xác định hình dạng của các đối tượng 3D của chúng ta, nhưng không xác định hình dạng của chúng. Để làm được điều đó, chúng ta cần thêm một `material`

Three.js đi kèm với 10 `mesh materials`, mỗi material có những ưu điểm và đặc tính có thể tùy chỉnh riêng. Chúng tôi sẽ xem xét một số ít những điều hữu ích nhất.

![Materials](http://boxxv.com/img/posts/material.png "Materials")_Materials_

#### MeshNormalMaterial
**MeshNormalMaterial**  
[https://threejs.org/docs/index.html#api/en/materials/MeshNormalMaterial](https://threejs.org/docs/index.html#api/en/materials/MeshNormalMaterial)

Hữu ích cho: thiết lập và chạy nhanh chóng

Chúng tôi sẽ bắt đầu với `MeshNormalMaterial`, vật liệu nhiều màu mà chúng tôi đã sử dụng trong các ví dụ cho đến nay. Nó ánh xạ các vectơ thông thường sang màu RGB: nói cách khác, nó sử dụng màu sắc để phân biệt vị trí của vectơ trong không gian 3D.

```javascript
const material = new THREE.MeshNormalMaterial();
```










-----
Tham khảo:
- [JavaScript in 3D: an Introduction to Three.js](https://medium.com/javascript-in-plain-english/javascript-in-3d-an-introduction-to-three-js-780f1e4a2e6d)