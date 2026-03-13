# Nhom11_NT208
## Lỗi syntax
### 1. File `pages\customers.php` (Dòng 6)
- Parse error: Unclosed '[' does not match ')'
- Code hiện tại:
```php
foreach ($customers as $customer) {
    if ($customer['active') {
        $activeCustomers[] = $customer;
    }
}
```
- Sửa: thêm `]` sau `['active'`.
### 2. File ``pages\reports.php`` (Dòng 4)
- Parse error: syntax error, unexpected variable "$totalsByCategory"
- Code hiện tại:
```php
$reportRows = []
$totalsByCategory = [];
```
- Sửa: thêm `;` sau `$reportRows = []`
### 3. File ``pages\settings.php`` (Dòng 7)
- Parse error: syntax error, unexpected token ";", expecting "]" 
- Code hiện tại:
```php
$config = [
    'currency' => 'USD',
    'timezone' => 'Asia/Ho_Chi_Minh',
    'language' => 'en',
;
```
- Sửa: thêm `]` sau dòng 6 trước `;`.
## Lỗi logic
### 1. Lỗi logic trạng thái đơn hàng file `pages\dashboard.php`
- Code hiện tại:
```php
if ($order['status'] === 'pending') {
$completedOrders++;
$totalRevenue += calculate_order_total($order, $products);
}
```
- Biến được đặt tên là `$completedOrders` dùng để tính doanh thu `$totalRevenue`, nhưng code lại đang kiểm tra điều kiện là `'pending'`
- Sửa: đổi `'pending'` thành `'completed'`.
### 2. Lỗi logic cảnh báo kho thấp file `pages\dashboard.php`
- Đoạn code hiện tại:
```php
if ($product['stock'] < 1) {
    $lowStockItems[] = $sku . ' - ' . $product['name'];
}
```
- Chỉ hiện sản phẩm khi stock < 1 (tức là đã hết hàng), không đúng ý nghĩa low stock (sắp hết hàng).
- Sửa: đổi `$product['stock'] < 1` thành một ngưỡng cao hơn, ví dụ `< 5`.
### 3. Lỗi logic lọc danh sách sai file `pages/orders.php`
- Đoạn code hiện tại:
```php
foreach ($orders as $order) {
    if ($order['status'] === 'completed') {
        $pendingOnly[] = $order;
    }
}
```
- Biến là `$pendingOnly` (chỉ đơn hàng chờ) nhưng code lại lọc đơn `'completed'`.
- Sửa: đổi `if ($order['status'] === 'completed')` thành `=== 'pending'`.
### 4. Lỗi logic tính Subtotal sai file `pages/checkout.php`
- Đoạn code hiện tại:
```php
foreach ($cart as $item) {
    $subtotal = $products[$item['sku']]['price'] * $item['qty'];
}
```
- Biến `$subtotal` bị gán lại liên tục trong vòng lặp thay vì cộng dồn.
- Sửa: đổi `$subtotal = ...` thành `$subtotal += ...`.
### 5. Lỗi logic phân loại sai file `pages/reports.php`
- Đoạn code hiện tại:
```php
foreach ($products as $product) {
    $category = $product['name'];

    if (!isset($totalsByCategory[$category])) {
        $totalsByCategory[$category] = 0;
    }

    $totalsByCategory[$category] += $product['stock'] * $product['price'];
```
- Đang nhóm doanh thu theo tên sản phẩm `($product['name'])` thay vì danh mục `(category)`.
- Sửa: đổi `$category = $product['name']` thành `$category = $product['category']`.

