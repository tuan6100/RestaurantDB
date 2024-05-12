<div align="center">
  <h1>THIẾT KẾ MÔ HÌNH CƠ SỞ DỮ LIỆU QUẢN LÝ NHÀ HÀNG
  </h1>
  <p>
    <strong>Bộ môn Cơ sở dữ liệu - Mã lớp 147773</strong>
  </p>
</div>

<!-- Chen anh vao day -->
<details>
  <summary><b>Mục lục </b></summary>
  
  - [1. Giới thiệu để tài](#heading)
  - [2. Danh sách thành viên](#heading-1)

</details>

## 1. Giới thiệu để tài

Xuất phát từ nhu cầu chuyển đổi số, hệ thống mô hình dữ liệu quản lý nhà hàng
được xây dựng nhằm mục đích ứng dụng công nghệ vào trong hoạt động lưu
trữ và xử lý thông tin một cách hiệu quả, hợp lý và nhanh chóng theo những
nhu cầu cụ thể :
<ol type = 'i'>
  <li> Về phía người quản lý nhà hàng: tăng cường khả năng quản lý và thống
kê, giup người chủ có thể giám sát nguồn nhân sự, cơ sở vật chất tài chính,
chất lượng dịch vụ qua đó nhằm tối ưu hóa hiệu suất kinh doanh </li>
  <li> Về phía nhân sự trong nhà hàng: giúp nhân viên quản lý lịch làm việc,
quản lý thực phẩm, thực đơn và thông tin cũng như yêu cầu từ phía khách
hàng,... </li>
  <li>Về phía khách hàng: Tạo ra trải nghiệm tương tác với khách hàng thông
qua việc lưu trữ thông tin mua hang, hóa đơn điện tử và nhiều dịch vụ
trực tuyến khác. </li>
</ol>


## 2. Danh sách thành viên 

| STT | Họ tên | MSSV | 
| :-------- | :------- | :----------|
| 1 | Hồ Tuấn Anh | 20226100 |
| 2 | Phạm Trường Dương | 20226105 |
| 3 | Nguyễn Trung Hiếu | 20226082 |
| 4 | Nguễn Huy Hoàng | 20226107 |
| 5 | Đỗ Gia Huy | 20226085 |

# 3. Xây dựng mô hình dữ liệu

## 3.1. Mô hình thực thể - liên kết

<!-- Chèn ảnh vào đây-->
Danh sách thực thể:
<ul>
  <li> Customer: Thông tin của khách hàng </li>
  <li> Employee: Thông tin của nhân viên nhà hàng </li>
  <li> Inventory: Thông tin của tất cả các nguyên liệu trong kho </li>
  <li> F&B: Thông tin của tất cả các món ăn </li>
  <li> Reservation: Thông tin của mỗi đơn đặt hàng từ khách hàng </li>
  <li> Bill: Thông tin hóa đơn khách hàng </li>
</ul>


## 3.2. Sơ đồ quan hệ 

<!-- Chèn ảnh vào đây -->

# 4. Danh sách các câu truy vấn SQL và biểu thức ĐSQH 

 1. Câu lệnh 1: 
```sql
SELECT * FROM table WHERE x = y;
```
Biểu thức đại số quan hệ:  $$\sigma_{x = y}(mytable)$$

3. Câu lệnh 2:




