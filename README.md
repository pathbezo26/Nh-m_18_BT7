# Báo cáo sửa lỗi

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

