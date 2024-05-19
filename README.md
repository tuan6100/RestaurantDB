<div align="center">
  <h1>THIẾT KẾ MÔ HÌNH CƠ SỞ DỮ LIỆU QUẢN LÝ NHÀ HÀNG
  </h1>
  <p>
    <strong>Bộ môn Cơ sở dữ liệu - Mã lớp 147773</strong>
  </p>
</div>

<!-- Chen anh vao day -->

<details>
  <summary><b>Mục lục</b></summary> 
  
   <ol>
      <li><a href="#gioi-thieu-de-tai">Giới thiệu để tài</a></li>
      <li><a href="#danh-sach-thanh-vien">Danh sách thành viên</a></li>
      <li><a href="#xay-dung-mo-hinh-du-lieu">Xây dựng mô hình dữ liệu</a></li>
      <li><a href="#danh-sach-cau-truy-van-sql-va-bieu-thuc-dsqh">Danh sách các câu truy vấn SQL và biểu thức ĐSQH</a></li>
      <li><a href="#danh-sach-phu-thuoc-ham">Danh sách các phụ thuộc hàm</a></li>
   </ol>

</details>

<h1 id="gioi-thieu-de-tai">1. Giới thiệu để tài</h1>

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

Chi tiết xem tại: [link](https://github.com/tuan6100/RestaurantDB)

<h1 id="danh-sach-thanh-vien">2. Danh sách thành viên</h1>

| STT | Họ tên | MSSV | 
| :-------- | :------- | :----------|
| 1 | Hồ Tuấn Anh | 20226100 |
| 2 | Phạm Trường Dương | 20226105 |
| 3 | Nguyễn Trung Hiếu | 20226082 |
| 4 | Nguễn Huy Hoàng | 20226107 |
| 5 | Đỗ Gia Huy | 20226085 |

<h1 id="xay-dung-mo-hinh-du-lieu">3. Xây dựng mô hình dữ liệu</h1>

## 3.1. Mô hình thực thể - liên kết

![erd](https://raw.githubusercontent.com/tuan6100/RestaurantDB/main/img/438299734_319544691031935_7138416519740917392_n.png)

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
![Sơ đồ quan hệ](https://raw.githubusercontent.com/tuan6100/RestaurantDB/main/img/drawSQL-image-export-2024-05-14.png)

<!-- Chèn ảnh vào đây -->

<h1 id="danh-sach-cau-truy-van-sql-va-bieu-thuc-dsqh">4. Danh sách các câu truy vấn SQL và biểu thức ĐSQH</h1>

 1. Truy xuất dữ liệu từ bảng công thức
```sql
SELECT * FROM "Recipe";
```
Biểu thức đại số quan hệ:  $$\pi_{fb-id, Ingredient-id, Quantity}(Recipe)$$

 2. Lấy tổng số lượng của mỗi nguyên liệu được sử dụng trong các công thức:
```sql
SELECT "Ingredient_id", SUM("Quantity") AS "Total_Quantity"
FROM "Recipe"
GROUP BY "Ingredient_id";
```
3. Lấy hóa đơn cùng với các đặt bàn tương ứng:
```sql
   SELECT *
   FROM "Bill"
   INNER JOIN "Reservation" ON "Bill"."Reservation_id" = "Reservation"."Reservation_id"
WHERE Customer_id = 20011001;
```
Biểu thức đại số quan hệ:  $$\sigma_{customer_id = 20011001}(bill ⋈ _{bill.reservation-id = reservation.reservation-id}reservation)$$

4. Lấy các đặt bàn được thực hiện bởi một khách hàng cụ thể:
```sql
   SELECT *
   FROM "Reservation"
   WHERE "Customer_id" = 1000;
```
Biểu thức đại số quan hệ:  $$\sigma_{customer_id=1000}(reservation)$$

5. Lấy các mặt hàng trong kho sắp hết hạn:
```sql
   SELECT *
   FROM "Inventory"
   WHERE "Expiration_date" <= CURRENT_TIMESTAMP;
```
Biểu thức đại số quan hệ:  $$\sigma_{Expiration_date<=CURRENT_TIMESTAMP}(Inventory)$$

6. Lấy tổng giá của mỗi hóa đơn:
```sql
   SELECT "Bill_id", SUM("Total_price") AS "Total_Price"
   FROM "Bill"
   GROUP BY "Bill_id";
```

7. Lấy các đặt bàn có số lượng khách hàng cao nhất:
```sql
   SELECT *
   FROM "Reservation"
   WHERE "Num_of_customer" = (
       SELECT MAX("Num_of_customer")
       FROM "Reservation"
   );
```
Biểu thức đại số quan hệ:  $$\sigma_{x = y}(mytable)$$

 8. Lấy tên của các khách hàng đã đặt bàn:
```sql
   SELECT "Name"
   FROM "Customer"
   WHERE "Customer_id" IN (
       SELECT DISTINCT "Customer_id"
       FROM "Reservation"
   );
```
Biểu thức đại số quan hệ:  $$\sigma_{x = y}(mytable)$$

9. Lấy giá trung bình của thức ăn và đồ uống: 
```sql
   SELECT AVG("Price") AS "Average_Price"
   FROM "Food_and_Beverage";
   
```

10. Lấy các đặt bàn có tổng giá cao nhất:
```sql
    SELECT *
    FROM "Reservation"
    WHERE "Reservation_id" = (
        SELECT "Reservation_id"
        FROM "Bill"
        GROUP BY "Reservation_id"
        ORDER BY SUM("Total_price") DESC
        LIMIT 1
    );
```
Biểu thức đại số quan hệ:  $$\sigma_{x = y}(mytable)$$

11. Lấy tên và số lượng của các nguyên liệu được sử dụng trong một công thức cụ thể:
```sql
    SELECT "Inventory"."Name", "Recipe"."Quantity"
    FROM "Recipe"
    INNER JOIN "Inventory" ON "Recipe"."Ingredient_id" = "Inventory"."Ingredient_id"
    WHERE "Recipe"."f&b_id" = <f&b_id>;
```
Biểu thức đại số quan hệ:  $$\pi_{Inventory.Name, Recipe.Quantity}(σ_{"Recipe.f&b_id" = <f&b_id>}(Recipe ⨝ Inventory))$$

12. Lấy các đặt bàn có trạng thái "Confirmed":
```sql
    SELECT *
    FROM "Reservation"
    WHERE "Status" = 'Confirmed';
```
Biểu thức đại số quan hệ: $$\sigma_{"Status" = 'Confirmed'}(Reservation)$$

13. Lấy tổng số khách hàng cho mỗi đặt bàn:
```sql
    SELECT "Reservation_id", COUNT("Customer_id") AS "Total_Customers"
    FROM "Reservation"
    GROUP BY "Reservation_id";
```

14. Lấy các đặt bàn được thực hiện bởi khách hàng có tên miền email cụ thể:
```sql
    SELECT *
    FROM "Reservation"
    WHERE "Customer_id" IN (
        SELECT "Customer_id"
        FROM "Customer"
        WHERE "Email" LIKE '%@example.com'
    );
```

15. Lấy các mặt hàng thức ăn và đồ uống có giá lớn hơn giá trung bình:
```sql
    SELECT *
    FROM "Food_and_Beverage"
    WHERE "Price" > (
        SELECT AVG("Price")
        FROM "Food_and_Beverage"
    );
```

16. Lấy các đặt bàn có trạng thái "Confirmed" và có hơn 4 khách hàng:
```sql
    SELECT *
    FROM "Reservation"
    WHERE "Status" = 'Confirmed'
    AND "Num_of_customer" > 4;
```
Biểu thức đại số quan hệ:  $$\sigma_{status = "Confirmed" AND num_of_customer > 4}(reservation)$$

17. Lấy tên của các nguyên liệu thuộc danh mục "Dairy": 
```sql
SELECT * FROM mytable WHERE x = y;
```
Biểu thức đại số quan hệ:  $$\sigma_{x = y}(mytable)$$

18. Lấy các đặt bàn được thực hiện bởi khách hàng có số điện thoại bắt đầu bằng mã vùng cụ thể:
```sql
    SELECT "Name"
    FROM "Inventory"
    WHERE "Category" = 'Dairy';
```
Biểu thức đại số quan hệ:  $$\pi_{"Name"}(σ_{Category = 'Dairy'}(Inventory))$$

19. Lấy giá trung bình của số lượng nguyên liệu được sử dụng trong các công thức:

```sql
   SELECT AVG("Quantity") AS "Average_Quantity"
    FROM "Recipe"
```

20. Lấy các đặt bàn có ngày đặt sau ngày cụ thể:
```sql
    SELECT "Bill"."Bill_id", "Bill"."Total_price", "Reservation"."Status"
    FROM "Bill"
    INNER JOIN "Reservation" ON "Bill"."Reservation_id" = "Reservation"."Reservation_id";
    
    Relational Algebra: π("Bill.Bill_id", "Bill.Total_price", "Reservation.Status")(Bill ⨝ Reservation)
```
Biểu thức đại số quan hệ:  $$\pi_{Bill.Bill_id, Bill.Total_price, Reservation.Status}(Bill ⨝ Reservation)$$

 21. Truy xuất các mặt hàng thực phẩm, đồ uống có giá lớn hơn giá trung bình, được nhóm theo danh mục:
```sql
    SELECT "Category", COUNT(*) AS "Count"
    FROM "Food_and_Beverage"
    WHERE "Price" > (
        SELECT AVG("Price")
        FROM "Food_and_Beverage"
    )
    GROUP BY "Category";
```

 22. Truy xuất các đặt chỗ được thực hiện bởi khách hàng có cùng tên miền email với khách hàng khác:
```sql
    SELECT *
    FROM "Reservation"
    WHERE "Customer_id" IN (
        SELECT DISTINCT "Customer_id"
        FROM "Customer"
        WHERE SUBSTRING("Email", POSITION('@' IN "Email") + 1) IN (
            SELECT SUBSTRING("Email", POSITION('@' IN "Email") + 1)
            FROM "Customer"
            GROUP BY SUBSTRING("Email", POSITION('@' IN "Email") + 1)
            HAVING COUNT(DISTINCT "Customer_id") > 1
        )
    );
```

 23. Câu lệnh 23: 
```sql
    SELECT "Name"
    FROM "Inventory"
    WHERE "Category" <> 'Vegetables';
```
Biểu thức đại số quan hệ:  $$\pi_{Name}(σ_{"Category" <> 'Vegetables'}(Inventory))$$

 24. Câu lệnh 24: 
```sql
    SELECT *
    FROM "Reservation"
    WHERE "Customer_id" IN (
        SELECT DISTINCT "Customer_id"
        FROM "Bill"
        WHERE "Total_price" > 1000
    );
```

 25. Tìm top 10 khách có lượt đặt bàn nhiều nhất năm 2023:
```sql
SELECT "Customer_id", COUNT("Reservation_id") AS "Total_Reservations"
FROM "Reservation"
WHERE EXTRACT(YEAR FROM "Reservation_date") = 2023
GROUP BY "Customer_id"
ORDER BY "Total_Reservations" DESC
LIMIT 10;
```

> [!Note]  
> Danh sách các câu truy vấn có mệnh đề <span style="color:#4da6ff">GROUP BY</span>: 2, 6, 10, 13, 21, 22
> Danh sách các câu truy vấn có ánh xạ lồng: 4, 5


<h1 id="danh-sach-phu-thuoc-ham">5. Danh sách các phụ thuộc hàm</h1>

- Xét lược đồ quan hệ <span style="color:#ff00ff">Customer</span>(Customer_id, Name, Email, Phone_number) \
  Ký hiệu A = Customer_id, B = Name, C = Email, D = Phone_number \
  Lược đồ này có tập phụ thuộc hàm F = {f1, f2} trong đó:
  - f1 = A -> BCD
  - f2 = B -> CD
   
- Xét lược đồ quan hệ <span style="color:#800080">Reservation</span>(Reservation_id, Customer_id, Table_number, Time, Num_of_customer, Status) \
  Ký hiệu A = Reservation_id, B = Customer_id, C = table_number, D = Time, E = Num_of_customer, F = Status \
  Lược đồ này có tập phụ thuộc hàm F = {f3, f4} trong đó:
  - f3 = A -> C
  - f4 = B -> DEF
 
- Xét lược đồ quan hệ <span style="color:#0000ff">Inventory</span>(Ingredient_ID, Name, Description, Catelogy, Current_quantity, Expiration) \
  Ký hiệu A = Ingredient_ID, B = Name, C = Description, D = Catelogy, E = Current_quantity, F = Expiration\
  Lược đồ này có tập phụ thuộc hàm F = {f5, f6} trong đó:
  - f5 = A -> BCDEF
  - f6 = B -> CDEF

- Xét lược đồ quan hệ <span style="color:#00ffff">Foof_and_Beverage</span>(f&b_id, name, catelogy, price) \
  Ký hiệu A = f&b_id, B = name, C = catelogy, D = price
  Lược đồ này có tập phụ thuộc hàm F = {f7, f8} trong đó:
  - f7 = A -> BCD
  - f8 = B -> CD
 
- Xét lược đồ quan hệ <span style="color:#33ff99">Bill</span>(Bill_id, Reservation_id, Date_and_time, Total_price) \
  Ký hiệu A = Bill_id, B = Reservation_id, C = Date_and_time, D = Total_price\
  Lược đồ này có tập phụ thuộc hàm F = {f9, f10} trong đó:
  - f9 = A -> BCD
  - f10 = B -> D
