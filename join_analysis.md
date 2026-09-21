# Giải trình kỹ thuật: COUNT(o.order_id) vs COUNT(*) trong LEFT JOIN

Khi sử dụng `LEFT JOIN`, với những bản ghi ở bảng bên trái không có dữ liệu tương ứng ở bảng bên phải (ví dụ: khách hàng Charlie chưa mua hàng), các cột từ bảng `Orders` sẽ mang giá trị `NULL`.

- **COUNT(*)**: Đếm tất cả các dòng được trả về trong tập kết quả, bất kể giá trị là NULL hay không. Do đó, dòng của Charlie vẫn được đếm là 1.
- **COUNT(o.order_id)**: Chỉ đếm các ô chứa giá trị **không phải NULL** (NON-NULL) trên cột `order_id`. Khi Charlie chưa có đơn hàng, `o.order_id` mang giá trị NULL, hàm sẽ trả về kết quả chính xác là `0`.

Vì vậy, việc dùng `COUNT(o.order_id)` là bắt buộc để phản ánh đúng số lượng đơn hàng thực tế của khách hàng.