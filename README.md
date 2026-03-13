# Campus Bookstore Lab -- Báo cáo sửa lỗi

## Tổng quan

Project **Campus Bookstore** là một bài lab PHP mô phỏng hệ thống quản
trị nhà sách trong trường học. Trong source code ban đầu có nhiều lỗi
**syntax** và **logic** được cài sẵn để sinh viên thực hành debug.

Sau khi sửa các lỗi, tất cả các trang quản trị hoạt động đúng và các
phép tính trong hệ thống cho kết quả hợp lý.

------------------------------------------------------------------------

# Danh sách lỗi và cách sửa

## 1. Lỗi Logic -- Tính sai Discount

**File:** `pages/checkout.php`

### Lỗi

``` php
$discountValue = $subtotal * $discountPercent;
```

Giảm giá được tính sai vì `discountPercent` là phần trăm.

### Sửa

``` php
$discountValue = $subtotal * ($discountPercent / 100);
```

------------------------------------------------------------------------

## 2. Lỗi Syntax -- Thiếu dấu chấm phẩy

**File:** `pages/customers.php`

### Lỗi

``` php
$activeCustomers = []
```

### Sửa

``` php
$activeCustomers = [];
```

------------------------------------------------------------------------

## 3. Lỗi Syntax -- Thiếu dấu ngoặc trong foreach

**File:** `pages/reports.php`

### Lỗi

``` php
foreach ($totalsByCategory as $category => $total {
```

### Sửa

``` php
foreach ($totalsByCategory as $category => $total) {
```

------------------------------------------------------------------------

## 4. Lỗi Syntax -- Thiếu dấu phẩy trong mảng

**File:** `pages/settings.php`

### Lỗi

``` php
'timezone' => 'Asia/Ho_Chi_Minh'
'language' => 'en',
```

### Sửa

``` php
'timezone' => 'Asia/Ho_Chi_Minh',
'language' => 'en',
```

------------------------------------------------------------------------

## 5. Lỗi Logic -- Tính sai doanh thu

**File:** `pages/dashboard.php`

### Lỗi

``` php
foreach ($order['items'] as $item) {
    $totalRevenue += $item['qty'];
}
```

Chỉ cộng số lượng sản phẩm mà không tính giá.

### Sửa

``` php
foreach ($order['items'] as $item) {
    $price = $products[$item['sku']]['price'];
    $totalRevenue += $price * $item['qty'];
}
```

------------------------------------------------------------------------

## 6. Lỗi Logic -- Sắp xếp đơn hàng sai thứ tự

**File:** `pages/orders.php`

### Lỗi

``` php
return $left['id'] <=> $right['id'];
```

Danh sách được sắp xếp tăng dần.

### Sửa

``` php
return $right['id'] <=> $left['id'];
```

------------------------------------------------------------------------

## 7. Lỗi Logic -- Biến chưa được khởi tạo

**File:** `pages/reports.php`

### Lỗi

``` php
$reportRows[] = strtoupper($category) . ': $' . number_format($total, 2);
```

Biến `$reportRows` chưa được khai báo.

### Sửa

``` php
$reportRows = [];
```

------------------------------------------------------------------------

# Kết quả sau khi sửa

Sau khi sửa tất cả các lỗi:

-   Tất cả các route đều truy cập được:
    -   `/`
    -   `/?page=dashboard`
    -   `/?page=orders`
    -   `/?page=checkout`
    -   `/?page=customers`
    -   `/?page=reports`
    -   `/?page=settings`
-   Dashboard hiển thị số liệu hợp lý.
-   Danh sách đơn hàng hiển thị đúng và sắp xếp đơn mới trước.
-   Checkout tính toán chính xác.
-   Trang Reports và Settings không còn lỗi cú pháp.

------------------------------------------------------------------------

## Kết luận

Bài lab giúp rèn luyện kỹ năng phát hiện và sửa lỗi trong PHP, bao gồm:

-   Lỗi cú pháp (syntax errors)
-   Lỗi logic trong tính toán
-   Lỗi sắp xếp dữ liệu
-   Lỗi sử dụng biến chưa khởi tạo
