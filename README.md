# Nhom11_NT208
## Lỗi syntax
1. File pages\customers.php (Dòng 6)
- Lỗi: Unclosed '[' does not match ')'
- Thiếu dấu ]
2. File pages\reports.php (Dòng 4)
- Lỗi: unexpected variable "$totalsByCategory"
- Thiếu dấu ;
3. File pages\settings.php (Dòng 7)
- Lỗi: unexpected token ";", expecting "]"
- Thiếu dấu ] sau dòng 6
## Lỗi logic
1. Lỗi logic trạng thái đơn hàng File pages\dashboard.php
- Đoạn code hiện tại:
```php
if ($order['status'] === 'pending') {
$completedOrders++;
$totalRevenue += calculate_order_total($order, $products);
}
```
- Biến được đặt tên là `$completedOrders` dùng để tính doanh thu `$totalRevenue`, nhưng code lại đang kiểm tra điều kiện là `'pending'`
- Sửa: Đổi `'pending'` thành `'completed'`
   
