---
layout: post
title: Điều hướng dễ dàng với Jetpack Compose
subtitle: Full Guide to Navigation in Jetpack Compose
description: Hướng dẫn từng bước để có trải nghiệm người dùng mượt mà
author: "Google Developers Training team"
image: "img/2023/android-tips-for-working-with-preview-in-jetpack-compose.png"
tags:
- Android
- Kotlin
- Jetpack
- Compose
- Material Design
- Navigation
---

# Mục lục

- [Mục lục](#mục-lục)
- [Giới thiệu](#giới-thiệu)
  - [Techical Stack](#techical-stack)
- [Hướng dẫn từng bước](#hướng-dẫn-từng-bước)
  - [Xác định tuyến (routes) cho các đích đến (destinations) trong ứng dụng](#xác-định-tuyến-routes-cho-các-đích-đến-destinations-trong-ứng-dụng)
  - [Thêm NavHost vào ứng dụng](#thêm-navhost-vào-ứng-dụng)
  - [Xử lý các tuyến (route) trong NavHost](#xử-lý-các-tuyến-route-trong-navhost)
- [Tổng kết](#tổng-kết)

![Navigation](https://boxxv.github.io/img/2023/1_7v6mG_QL5vriYBdwkTLRww.webp "Navigation")

# Giới thiệu

Trong quá trình phát triển Android hiện đại, các ứng dụng nhiều màn hình được tạo bằng thành phần Điều hướng `Jetpack`. Thành phần Điều hướng (`Navigation`) trong `Compose` cho phép bạn dễ dàng xây dựng ứng dụng nhiều màn hình trong Compose bằng phương pháp khai báo, tương tự như việc tạo giao diện người dùng. Lớp học lập trình này giới thiệu thông tin cơ bản của thành phần Điều hướng trong Compose, cách giúp AppBar (Thanh ứng dụng) phản hồi nhanh với thao tác điều hướng và cách gửi dữ liệu từ ứng dụng của bạn đến một ứng dụng khác bằng ý định (thể hiện các phương pháp hay nhất trong một ứng dụng ngày càng phức tạp).

## Techical Stack

- Android Jetpack Compose
- Android Navigation Component

Android Navigation Component có 3 phần chính:

- `NavController`: Chịu trách nhiệm điều hướng giữa các destination — tức là các màn hình trong ứng dụng của bạn.
- `NavGraph`: Maps composable destinations để điều hướng đến.
- `NavHost`: Hiển thị destination hiện tại của NavGraph.

Trong lớp học lập trình này, bạn sẽ tập trung vào NavController và NavHost. Trong NavHost, bạn sẽ xác định các đích đến cho NavGraph của ứng dụng.

Kiến thức bạn sẽ học được
- Tạo một thành phần kết hợp `NavHost` để xác định các tuyến và màn hình trong ứng dụng.
- Di chuyển giữa các màn hình bằng `NavHostController`.
- Thao tác với ngăn xếp lui để chuyển về các màn hình trước.
- Dùng ý định để chia sẻ dữ liệu với một ứng dụng khác.
- Tuỳ chỉnh AppBar, bao gồm tiêu đề và nút quay lại.

# Hướng dẫn từng bước

![Navigation](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-navigation/img/fde052dfa0a1f56a.png "Navigation")

## Xác định tuyến (routes) cho các đích đến (destinations) trong ứng dụng

Một trong những khái niệm cơ bản về tính năng điều hướng trong Compose là tuyến (`route`). Tuyến là một chuỗi tương ứng với một đích đến. Ý tưởng này tương tự như khái niệm về `URL`. Giống như một URL ánh xạ đến một trang khác trên trang web, tuyến là một chuỗi ánh xạ tới một đích đến và đóng vai trò là mã nhận dạng duy nhất (unique identifier). Thông thường, đích đến là một thành phần kết hợp hoặc nhóm các thành phần kết hợp tương ứng với những gì người dùng nhìn thấy. Ứng dụng Cupcake cần các đích đến cho màn hình bắt đầu đặt hàng (order screen), màn hình hương vị (flavor screen), màn hình ngày lấy hàng (pickup date screen) và màn hình tóm tắt đơn đặt hàng (order summary screen).

Ứng dụng có số lượng màn hình giới hạn, theo đó cũng giới hạn về số lượng các tuyến. Bạn có thể xác định các tuyến của một ứng dụng bằng lớp `enum`. Các lớp enum trong Kotlin có thuộc tính tên trả về một chuỗi có tên thuộc tính.

Bạn sẽ bắt đầu bằng cách xác định 4 tuyến cho ứng dụng Cupcake.

- `Start`: Dùng một trong ba nút để chọn số lượng bánh nướng.
- `Flavor`: Chọn hương vị trong danh sách các lựa chọn.
- `Pickup`: Chọn ngày lấy hàng trong danh sách các lựa chọn.
- `Summary`: Xem lại các lựa chọn rồi gửi hoặc huỷ đơn đặt hàng.

Thêm một lớp enum để xác định các tuyến.

1. Trong `CupcakeScreen.kt`, phía trên thành phần kết hợp `CupcakeAppBar`, hãy thêm một lớp `enum` có tên `CupcakeScreen`.
2. Thêm 4 trường hợp vào lớp enum: `Start`, `Flavor`, `Pickup` và `Summary`.

```kotlin
enum class CupcakeScreen() {
    Start,
    Flavor,
    Pickup,
    Summary
}
```

## Thêm NavHost vào ứng dụng

`NavHost` là một thành phần kết hợp (Composable) cho thấy các đích đến có thể kết hợp khác (composable destinations), dựa trên một tuyến (`route`) được cung cấp. Ví dụ: nếu tuyến là `Flavor`, thì `NavHost` sẽ hiển thị màn hình để bạn chọn hương vị bánh nướng. Nếu tuyến là `Summary` thì ứng dụng sẽ cho thấy màn hình tóm tắt (summary screen).

Cú pháp cho `NavHost` cũng giống như mọi Thành phần kết hợp khác.

![Navigation](https://boxxv.github.io/img/2023/fae7688d6dd53de9.png "Navigation")

Trong đó, Có hai tham số đáng chú ý:

- `navController`: Một bản sao (instance) của lớp `NavHostController`. Bạn có thể sử dụng đối tượng này để điều hướng giữa các màn hình, chẳng hạn như bằng cách gọi phương thức `navigate()` để điều hướng đến một đích đến (destinations) khác. Bạn có thể lấy `NavHostController` bằng cách gọi `rememberNavController()` từ một hàm composable.
- `startDestination`: Một tuyến (route) của chuỗi xác định đích đến sẽ xuất hiện theo mặc định khi ứng dụng hiện `NavHost` lần đầu tiên được khởi tạo. Trong trường hợp ứng dụng Cupcake, đây phải là tuyến `Start`.

Giống như các thành phần kết hợp khác, `NavHost` cũng lấy tham số `modifier`.

> Lưu ý: `NavHostController` là một lớp con của lớp `NavController`, cung cấp chức năng bổ sung để sử dụng với thành phần kết hợp (composable) `NavHost`.

Bạn sẽ thêm NavHost vào thành phần kết hợp CupcakeApp trong CupcakeScreen.kt. Trước tiên, bạn cần tham chiếu đến trình điều khiển điều hướng. Bạn có thể sử dụng trình điều khiển điều hướng trong cả NavHost bạn đang thêm và AppBar mà bạn sẽ thêm ở bước sau. Do đó, bạn nên khai báo biến trong thành phần kết hợp CupcakeApp().

1. Mở `CupcakeScreen.kt`.
2. Phía trên biến `viewModel` trong thành phần kết hợp `CupcakeApp`, hãy tạo một biến mới bằng cách sử dụng val có tên `navController` và đặt biến bằng với kết quả của lệnh gọi `rememberNavController()`.

```kotlin
@Composable
fun CupcakeApp(modifier: Modifier = Modifier){
    val navController = rememberNavController()

    ...
}
```

3. Trong `Scaffold`, bên dưới biến `uiState`, hãy thêm một thành phần kết hợp `NavHost`.

```kotlin
Scaffold(
    ...
) { innerPadding ->
    val uiState by viewModel.uiState.collectAsState()

    NavHost()
}
```

4. Truyền biến `navController` cho tham số `navController` và `CupcakeScreen.Start.name` cho tham số `startDestination`. Truyền đối tượng sửa đổi đã truyền vào `CupcakeApp()` cho tham số của đối tượng sửa đổi. Truyền trailing lambda (lambda theo sau) trống cho thông số cuối cùng.

```kotlin
NavHost(
   navController = navController,
   startDestination = CupcakeScreen.Start.name,
   modifier = modifier.padding(innerPadding)
) {
}
```

## Xử lý các tuyến (route) trong NavHost

Giống như những thành phần kết hợp (composable) khác, NavHost có một hàm để khai báo content cho nó.

![Navigation](https://boxxv.github.io/img/2023/f67974b7fb3f0377.png "Navigation")

Trong hàm nội dung của `NavHost`, bạn hãy gọi hàm `composable()`. Hàm `composable()` có hai tham số bắt buộc.

- `route`: Một chuỗi tương ứng với tên của một tuyến. Đây có thể là một chuỗi duy nhất. Bạn sẽ sử dụng thuộc tính tên của các hằng số enum `CupcakeScreen`. Ví dụ: `CupcakeScreen.Start.name`
- `content`: Tại đây, bạn có thể gọi thành phần kết hợp mà bạn muốn trình bày cho tuyến vừa nêu khi route được chọn.

Bạn sẽ gọi hàm `composable()` một lần cho mỗi tuyến.

> Lưu ý: Hàm `composable()` là một hàm mở rộng của `NavGraphBuilder`.

1. Gọi hàm `composable()`, truyền `CupcakeScreen.Start.name` cho `route`.

```kotlin
NavHost(
   navController = navController,
   startDestination = CupcakeScreen.Start.name,
   modifier = modifier.padding(innerPadding)
) {
    composable(route = CupcakeScreen.Start.name) {

    }
}
```

2. Trong trailing lambda (lambda theo sau), gọi thành phần kết hợp `StartOrderScreen` để truyền `quantityOptions` cho thuộc tính `quantityOptions`.

```kotlin
NavHost(
   navController = navController,
   startDestination = CupcakeScreen.Start.name,
   modifier = modifier.padding(innerPadding)
) {
    composable(route = CupcakeScreen.Start.name) {
        StartOrderScreen(
            quantityOptions = quantityOptions
        )
    }
}
```

> Lưu ý: Thuộc tính `quantityOptions` bắt nguồn từ việc gọi `collectAsState()` ở dòng trước `NavHost`. Các thuộc tính khác trong mô hình chế độ xem sẽ được truy cập theo cách tương tự.

3. Bên dưới lệnh gọi đầu tiên tới `composable()`, hãy gọi lại `composable()`, truyền `CupcakeScreen.Flavor.name` cho `route`.

```kotlin
composable(route = CupcakeScreen.Flavor.name) {

}
```
4. Trong trailing lambda, hãy tham chiếu đến `LocalContext.current` và lưu trữ nó trong một biến có tên là `context`. Bạn có thể sử dụng biến này để lấy chuỗi từ danh sách mã nhận dạng tài nguyên trong mô hình chế độ xem để hiện danh sách các hương vị.

```kotlin
composable(route = CupcakeScreen.Flavor.name) {
    val context = LocalContext.current

}
```

5. Gọi thành phần kết hợp `SelectOptionScreen`.

```kotlin
composable(route = CupcakeScreen.Flavor.name) {
    val context = LocalContext.current
    SelectOptionScreen(

    )
}
```

6. Màn hình hương vị cần hiển thị và cập nhật tổng giá tiền khi người dùng chọn hương vị. Truyền vào `uiState.price` cho tham số `subtotal`.

```kotlin
composable(route = CupcakeScreen.Flavor.name) {
    val context = LocalContext.current
    SelectOptionScreen(
        subtotal = uiState.price
    )
}
```

7. Màn hình hương vị lấy danh sách các hương vị từ tài nguyên chuỗi của ứng dụng. Tạo một danh sách các chuỗi từ danh sách hương vị trong mô hình chế độ xem. Bạn có thể chuyển đổi danh sách mã nhận dạng tài nguyên thành danh sách các chuỗi bằng cách sử dụng hàm `map()` và gọi `stringResource()`.

```kotlin
composable(route = CupcakeScreen.Flavor.name) {
    val context = LocalContext.current
    SelectOptionScreen(
        subtotal = uiState.price,
        options = flavors.map { id -> stringResource(id) }
    )
}
```

8. Đối với tham số `onSelectionChanged`, hãy truyền biểu thức lambda gọi `setFlavor()` trên mô hình chế độ xem, truyền vào `it` (đối số đã truyền vào `onSelectionChanged()`).

```kotlin
composable(route = CupcakeScreen.Flavor.name) {
    val context = LocalContext.current
    SelectOptionScreen(
        subtotal = uiState.price,
        options = flavors.map { id -> context.resources.getString(id) },
        onSelectionChanged = { viewModel.setFlavor(it) }
    )
}
```

Màn hình ngày lấy hàng cũng tương tự như màn hình hương vị. Điểm khác biệt duy nhất là dữ liệu được truyền vào thành phần kết hợp `SelectOptionScreen`.

9. Gọi lại hàm `composable()`, truyền `CupcakeScreen.Pickup.name` cho tham số `route`.

```kotlin
composable(route = CupcakeScreen.Pickup.name) {

}
```

10. Trong trailing lambda, hãy gọi thành phần kết hợp `SelectOptionScreen` và truyền `uiState.price` vào `subtotal` như trước. Truyền `uiState.pickupOptions` cho tham số `options` và biểu thức lambda gọi `setDate()` trên `viewModel` cho tham số `onSelectionChanged`.

```kotlin
SelectOptionScreen(
    subtotal = uiState.price,
    options = uiState.pickupOptions,
    onSelectionChanged = { viewModel.setDate(it) }
)
```

11. Gọi `composable()` lại một lần nữa, truyền `CupcakeScreen.Summary.name` cho `route`.

```kotlin
composable(route = CupcakeScreen.Summary.name) {

}
```

12. Trong trailing lambda, hãy gọi thành phần kết hợp `OrderSummaryScreen()`, truyền vào biến `uiState` cho tham số `orderUiState`.

```kotlin
composable(route = CupcakeScreen.Summary.name) {
    OrderSummaryScreen(
        orderUiState = uiState
    )
}
```

Đó là các bước để thiết lập `NavHost`. Ở phần tiếp theo, bạn sẽ làm cho ứng dụng thay đổi các tuyến và di chuyển giữa các màn hình khi người dùng nhấn vào từng nút.

# Tổng kết

Đến đây là xong rồi đó bạn có thể thấy rằng nó thực sự đơn giản. Hãy thử và để lại bình luận nhé.

Chúc bạn thành công!

-----
Tham khảo
- [Android Jetpack Compose - Navigation Component part 1](https://viblo.asia/p/android-jetpack-compose-navigation-component-part-1-3RlL53m24bB)
- [Navigation in Jetpack Compose](https://developer.android.com/courses/pathways/android-basics-compose-unit-4-pathway-2)
- [Codelabs - Navigate between screens with Compose](https://developer.android.com/codelabs/basic-android-kotlin-compose-navigation)
- [https://github.com/google-developer-training/basic-android-kotlin-compose-training-cupcake](https://github.com/google-developer-training/basic-android-kotlin-compose-training-cupcake)

- [Effortless Navigation with Compose](https://blog.stackademic.com/effortless-navigation-with-compose-30d37ddf5625)
- [Navigation Basics in Jetpack Compose](https://youtu.be/glyqjzkc4fk)
- [Full Guide to Nested Navigation Graphs in Jetpack Compose](https://youtu.be/FIEnIBq7Ups)
- [Migrate Jetpack Navigation to Navigation Compose](https://developer.android.com/jetpack/compose/migrate/migration-scenarios/navigation)
