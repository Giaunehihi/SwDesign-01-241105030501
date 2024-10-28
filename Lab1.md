# LAB 1

# PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG CHO PAYROLL SYSTEM

# 1. Phân tích kiến trúc

 ***1.1 Kiến trúc được đề xuất cho hệ thống Payroll System là Layered Architecture (Kiến trúc phân lớp).:***

> - UI Layer
> - Business Logic Layer
> - Data Access Layer
> - Integration Layer

***1.2 Lý do lựa chọn:***  
  Kiến trúc lớp (Layered Architecture) là một mẫu thiết kế phần mềm được chia thành các tầng hoặc lớp, mỗi lớp sẽ đảm nhận một nhiệm vụ cụ thể và độc lập. Nó giúp tổ chức mã nguồn theo cách dễ quản lý, dễ bảo trì, và dễ mở rộng.
***1.3 Ý nghĩa các thành phần trong kiến trúc:***

>> **UI Layer:**

* Giúp người dùng thao tác dễ dàng và đảm bảo bảo mật, chỉ cho phép nhân viên truy cập dữ liệu của riêng họ.*.</p>
 

>> *Business Logic Layer:* </p>
- Thực hiện các quy tắc nghiệp vụ và xử lý logic tính lương phức tạp, giúp hệ thống có thể bảo trì và kiểm tra độc lập.</p>
 
>> *Data Access Layer:*

* Tách biệt truy xuất dữ liệu, giảm phụ thuộc và cho phép dễ dàng thay đổi nguồn dữ liệu.</p>

***1.4 Pakage***

![Diagram](https://www.planttext.com/api/plantuml/png/T5AzJGCn5EuznUkeia0A550eJX0fWcI05z_Zpk2pBTidT48CmGo8yXQ8YnHCuWbO0PkVo93GVl_FydlOpPn7w_jECeFy7Xk2TGMF381BT0ukEYFrGBIkzj1ATCJHrWMqnA4ZvHVaMvtn9xPFE--TKEJSbMu4BuAJnMefbrRpn6fxF6k1AeNOW-uVl2YQeySpdiEEpBycevtmsWu7KGLLf5NAKsFH2wtAqLRV4VTVxNbbBjsWesmzWJdTfbl1almqkbOO1nlo3qGAlfCTI-yxcPp-UPWftCGmGXt3gshORowhY-kciBBz03nkHyCAFClAsKdtDl8MsXXU32kPhFptbEIxZDkT1nN3is1iHghEt-C3003__mC0)

# 2. Cơ chế phân tích 

   Dưới đây là các cơ chế quan trọng cần giải quyết trong hệ thống "Payroll System" cùng với lý do đề xuất để đảm bảo hệ thống hoạt động hiệu quả và đáp ứng đầy đủ yêu cầu:

***1. Quản lý xác thực và phân quyền*** </p>
* **Giải thích:**  Cơ chế này đảm bảo rằng chỉ những người dùng có quyền truy cập thích hợp mới có thể xem và chỉnh sửa dữ liệu cá nhân của họ. Hệ thống cần xác thực người dùng thông qua việc yêu cầu đăng nhập và sau đó kiểm tra quyền truy cập dựa trên vai trò của người dùng (nhân viên, quản trị viên, v.v.).
* * **Lý do:** Bảo mật thông tin lương và thông tin nhân sự là nhạy cảm, cần được bảo vệ để tránh rò rỉ thông tin cá nhân, kiểm soát truy cập


***2. Tính toán lương tự động***
* **Giải thích:** Cơ chế này xử lý việc tính toán lương cho từng loại nhân viên, bao gồm nhân viên làm theo giờ, nhân viên có lương cố định, và nhân viên nhận hoa hồng. Nó cũng sẽ hỗ trợ tính toán lương làm thêm giờ nếu có

* **Lý do:** Đảm bảo tính toán lương chính xác và theo dõi hiệu suất làm việc.

***3. Giao tiếp với cơ sở dữ liệu***
* **Giải thích:** Hệ thống cần có cơ chế để truy xuất thông tin từ Project Management Database mà không sửa đổi dữ liệu trong đó. Điều này có thể được thực hiện thông qua các truy vấn SQL hoặc API để lấy thông tin mà không làm thay đổi trạng thái của dữ liệu.

* **Lý do:**Bảo vệ dữ liệu, Tính nhất quán: Giúp đảm bảo rằng thông tin từ các nguồn khác nhau có thể được sử dụng một cách chính xác mà không làm gián đoạn đến các hệ thống khác.

***4. Xử lý Tiền lương Tự động***
* **Giải thích:** Hệ thống cần tự động hóa việc tính lương vào mỗi thứ Sáu và vào ngày làm việc cuối cùng của tháng. Điều này có thể được thực hiện thông qua các tác vụ lập lịch như cron jobs hoặc các tác vụ định kỳ trong ứng dụng.

* **Lý do:** Giảm tải công việc: Tự động hóa việc tính lương giúp giảm bớt khối lượng công việc cho quản trị viên và đảm bảo rằng lương được xử lý đúng thời hạn.

# 3. Phân tích ca sử dụng Payment
*3.1 Các lớp phân tích cho ca sử dụng "Payment":*

*NhânViên (Employee):*

* Mô tả: Đại diện cho nhân viên trong hệ thống, chứa thông tin cá nhân và phương thức thanh toán của họ.

**Thuộc tính:**

      - mãNhânViên: String
      - tên: String
      - địaChỉ: String
      - phươngThứcThanhToán: String
      - tàiKhoảnNgânHàng: String

*HệThốngLương (PayrollSystem):*

* Mô tả: Chịu trách nhiệm tính toán lương cho nhân viên dựa trên số giờ làm việc hoặc doanh thu từ hoa hồng.
  
**Thuộc tính:**
      - danhSáchNhânViên: List<NhânViên>
      - Phương thức:
      - tínhToánLương()
      - gửiThôngBáo()
      
*ThanhToán (Payment):*

* Mô tả: Thông tin liên quan đến giao dịch thanh toán cho nhân viên.
  
**Thuộc tính:**

      - sốTiền: Double
      - ngàyThanhToán: Date
      - trạngThái: String (thành công, thất bại)
      
*NgânHàng (Bank):*

* Mô tả: Chịu trách nhiệm thực hiện các giao dịch thanh toán từ hệ thống.
  
**Thuộc tính:**

      - tênNgânHàng: String
      - sốTàiKhoảnNgânHàng: String
      
*XửLýThanhToán (PaymentProcessor):*

* Mô tả: Thực hiện các thao tác xử lý thanh toán và giao tiếp với ngân hàng để hoàn tất giao dịch.
  
**Thuộc tính:**

      - mãGiaoDịch: String
      - trạngTháiGiaoDịch: String
      
*3.2  Biểu Đồ Tuần Tự (Sequence Diagram)*

![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aO9Vnk55UM6PXrVbSHK09JAJCmiIyqeKF1xkRW_9UBXxObwwpx4DnnRcfQD8HppSlTRdyDwGZCIyZ93ymmjHDVkb0ytqEBm0g8aBORw2hXqMOwqKAW-lAbL8VhXhUId2E0rDBaobk0meERmMgWqgX5CtXhEj52hGXO2QCPI1z28y1RGHQFB6v92CJFVCn7oNXxkxapE0sX0gSDXLKlHmrsBlXxlsbmIM0baech7QYSstm91QM-2N0IHBWDAJWuyj92BO4B40SlpXBNdfJeSNveS0tGDK499nU64cYY4EgNafe2G20000__y30000)

*3.3 Nhiệm Vụ của Các Lớp Phân Tích*

*NhânViên (Employee):*

* Gửi yêu cầu thanh toán tới hệ thống.
* Nhận thông báo về trạng thái thanh toán.

*HệThốngLương (PayrollSystem):*

* Tính toán số tiền lương dựa trên giờ làm việc hoặc hoa hồng.
* Gửi yêu cầu xử lý thanh toán đến lớp XửLýThanhToán.
  
*ThanhToán (Payment):*

* Lưu trữ thông tin thanh toán cho mỗi nhân viên, bao gồm số tiền và trạng thái giao dịch.
  
*NgânHàng (Bank):*

* Thực hiện các giao dịch thanh toán cho nhân viên và trả kết quả về lớp xử lý thanh toán.

*XửLýThanhToán (PaymentProcessor):*

* Nhận yêu cầu thanh toán từ hệ thống lương.
* Xử lý giao dịch với ngân hàng và cập nhật trạng thái thanh toán.

*3.4. Biểu Đồ Lớp (Class Diagram)*

![Diagram](https://www.planttext.com/api/plantuml/png/V5F1IiD04BtdAuQSL6ZHQv1Ij631qak3U8rfsLriDwNPWY8UF8buwXVOs9D2GQ6dBjB3IlzZly1VSDAkoTAqvZZlpRoPzpO_Sb6DHJ0GmrxN2Rj174EJgbT-mTGxXpi7y2j1JqtogWSjCM2S64mKIzyZBP-3KwhbqmRIfykFPSA9ZzXRwDE0KpzIIN7cc9tJICydl4bGjwx6d6ISUyTiclTdcyPQZdocvGEEh4N3gsx709oeyQqjM0l47oO6UhvQIYMig5BNyZ7TTyH9OxrzfjR6SIsLXDHsfy5YSPmNAYiku4rJesscxEqRX6WvPIW-u-H49H7MC-rBX1hgQykX6CaP2w8QEXtIJVkiUtQG06usHzkwkUkPO9hpbZ0is_yDpPY0FdvYxjPQQrdhqRb7BfHA5N0Fo-K3rmxP0u67HL1njcIIjbXJa6kU6kQpkwDei0VNI7jXlf4gCbPAkK4U43m67zryqKT-jSFRwS_q2m00__y30000)

*3.5 Giải Thích Biểu Đồ Lớp*

**NhânViên:** Có thể tạo nhiều ThanhToán. Điều này phản ánh rằng mỗi nhân viên có thể nhận nhiều khoản thanh toán khác nhau trong suốt thời gian làm việc.

**HệThốngLương:** Tương tác với NhânViên để nhận thông tin và thực hiện tính toán. Nó sẽ gọi đến lớp XửLýThanhToán để xử lý thanh toán.

**XửLýThanhToán:** Là cầu nối giữa HệThốngLương và NgânHàng, đảm bảo rằng các giao dịch thanh toán được thực hiện một cách an toàn và chính xác.

**NgânHàng:** Chịu trách nhiệm thực hiện giao dịch thanh toán cho nhân viên và trả kết quả về lớp XửLýThanhToán.


# 4. Phân tích ca sử dụng Maintain Timecard
**4.1 Các lớp phân tích cho ca sử dụng "Maintain Timecard":**

*NhânViên (Employee):*

* Mô tả: Đại diện cho nhân viên trong hệ thống, chứa thông tin cá nhân và quyền truy cập vào thời gian làm việc của họ.
  
***Thuộc tính:***
  
       - mãNhânViên: String
       - tên: String
       - địaChỉ: String
       - thờiGianLàmViệc: List<ThờiGian>

*ThờiGian (Timecard):*

* Mô tả: Đại diện cho thời gian làm việc của nhân viên, chứa thông tin về giờ làm việc và các thông tin liên quan.

***Thuộc tính:***

        - ngày: Date
        - sốGiờ: Double
        - mãSốChiPhí: String
        - trạngThái: String (đã gửi, chưa gửi)

 *HệThốngLương (PayrollSystem):*

* Mô tả: Chịu trách nhiệm quản lý và cập nhật thông tin thời gian làm việc của nhân viên.

***Thuộc tính:***

      - danhSáchNhânViên: List<NhânViên>
     
***Phương thức:***

      - cậpNhậtThờiGian()
      - lưuThờiGian()
      - XácNhận (Approval):

* Mô tả: Chịu trách nhiệm quản lý trạng thái phê duyệt thời gian làm việc của nhân viên.
***Thuộc tính:***
  
     - trạngTháiPhêDuyệt: String (đã phê duyệt, chưa phê duyệt)
     - ngườiPhêDuyệt: String
     
**4.2 Biểu Đồ Tuần Tự (Sequence Diagram)**
     ![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aO9Vnk55UM6PXrVbSHK09JAJCmiIyqeKF1xkRW_9UBXxObwwpx4DnnRcfQD8WwJcPhfd9gBgYZYyCDalu-6kjNbSN0Y35NJji9XdfL1vU5MfGlB3NSjBdO5Q2i0QIn0cQsXoOUe2cOLGOgLGyd3NmdmKFGWEBdlJ7-vUcncISNXBNdf8PXuH5YAyXUpeW8p3grnAAu4wIe0w4MfmMLjIz73NuX0W0UG1RL-OYMe0TgiHeGWq0EnafyD03oEPWXHsG5CSKlDIG94B0000__y30000)

**4.3 Nhiệm Vụ của Các Lớp Phân Tích**
*NhânViên (Employee):*

* Gửi yêu cầu cập nhật thời gian làm việc.
* Nhận thông báo về trạng thái cập nhật thời gian.

*ThờiGian (Timecard):*

* Lưu trữ thông tin về thời gian làm việc của nhân viên.
* Cung cấp thông tin cho hệ thống lương khi cần thiết.

*HệThốngLương (PayrollSystem):*

* Cập nhật thông tin thời gian làm việc của nhân viên.
* Gửi yêu cầu phê duyệt đến lớp xác nhận.

*XácNhận (Approval):*

* Kiểm tra và xác nhận thời gian làm việc của nhân viên.
* Trả lại trạng thái phê duyệt cho hệ thống lương.  

**4.4 Biểu Đồ Lớp (Class Diagram)**

 ![Diagram](https://www.planttext.com/api/plantuml/png/T5AnQiCm4Dtz5OUdjf3GhgQOG0Bf448X8NHr7MC9R2NOyX1Avr8wvGC2IJiK307FyT11nV_XByWlz9GQoN5h3HhUUtVttad7_AiNSoVYIHWORk34COo9U6SpAb86JmRWwK0eFZHgmOH7bFaLn_z2t-ioVtFwfCnVcsB4DdH87JOIst16o_p5jM14OtuxLPHjF1kL5mqgBymNsvK50uTx5HAN-Ng8hJQ8BfB7mDEk9qZr2RqdOjzq4fM77VEdHEoeejJSEpGcPw-PFogo0eLg_jnXP29sBgblv9H00_P92-2MX_roJF3cEid5PSK6HPQSmMhy0_O_bUdOTRyO9nqaA_J86wcONsIoOPi2OAcPvkpQmvit9dGwDfZNtUwLMNy62pWQMO1j_BCZMLBhWjfVOefvsYlEkikbj4jhYx5W9T94hlXJ5lGyDfT_-0S00F__0m00)

**4.5 Giải Thích Biểu Đồ Lớp**
* NhânViên: Có thể tạo nhiều ThờiGian. Điều này phản ánh rằng mỗi nhân viên có thể ghi lại nhiều khoảng thời gian khác nhau trong suốt thời gian làm việc của họ.

* ThờiGian: Lưu trữ thông tin về thời gian làm việc của nhân viên, bao gồm ngày làm việc, số giờ làm việc và mã số chi phí liên quan.

* HệThốngLương: Quản lý danh sách nhân viên và cập nhật thông tin thời gian làm việc của họ.

* XácNhận: Kiểm tra và phê duyệt thời gian làm việc trước khi lưu trữ vào hệ thống lương.


# 5. Hợp nhất kết quả phân tích

**5.1. Giới Thiệu** </p>

Tài liệu này mô tả kết quả phân tích cho hai ca sử dụng "Payment" và "Maintain Timecard" trong hệ thống quản lý lương của Acme, Inc. Mục tiêu là cải thiện quy trình thanh toán và ghi nhận thời gian làm việc của nhân viên.

**5.2 Ca Sử Dụng "Payment"**</p>

*5.2.1 Mô Tả*

Ca sử dụng "Payment" xử lý và tạo hóa đơn thanh toán cho nhân viên dựa trên giờ làm việc và doanh thu.

*5.2.2 Các Lớp Phân Tích*

    - NhânViên (Employee): Gửi yêu cầu thanh toán.
    - ThờiGian (Timecard): Cung cấp thông tin thời gian làm việc.
    - HệThốngLương (PayrollSystem): Quản lý quy trình thanh toán.
    - HóaĐơn (Invoice): Tạo và xác nhận hóa đơn thanh toán.
    
*5.2.3 Biểu Đồ Tuần Tự*

![Diagram](https://www.planttext.com/api/plantuml/png/UhzxFvT3SKbYKKbfRWvNOd99Vf62NyRXHNbXcOTNvN4L02KoapCB4lDA53mUxcuFoNYuUs9Uki-n3SSMvgMZI8EavcQwPoQYwJgyEV781A1gBYw4kGgwTbYCirAeFBogL27vuQxbfI4PYNaP8Vc75-PfQ79XAWKPWB3GIY7duQwbbI4PXxVafOTavY5aW9eH75osbXGztBKOksRiDiFz1DJxSDV2V3WVf0F6ncLRnU65oGfv6GzthSr3qOVL9aIG0Qq2kz3fyC9ybC1nICrB0SOT0000__y30000)

**5.3. Ca Sử Dụng "Maintain Timecard"**</p>

*5.3.1 Mô Tả*

Ca sử dụng "Maintain Timecard" cho phép nhân viên ghi lại và duy trì thông tin thời gian làm việc.

*5.3.2 Các Lớp Phân Tích*

-   NhânViên (Employee): Gửi yêu cầu cập nhật thời gian làm việc.
-   ThờiGian (Timecard): Lưu trữ thông tin thời gian làm việc.
-   HệThốngLương (PayrollSystem): Quản lý và cập nhật thông tin thời gian.
-   XácNhận (Approval): Phê duyệt thông tin thời gian làm việc.
  
*5.3.3 Biểu Đồ Tuần Tự*

![Diagram](https://www.planttext.com/api/plantuml/png/UhzxFvT3SKbYKKbfRWvNOd99Vf62NyRXHNbXcOTNvN4L02KoapCB4lDA53mUxcuFoNYuUs9Uki-n3SSMvgMZI8EavcQwPoQYweeul33PB-FXhhLvN5m8WnLqxR2OPwLGUNXLgKBomrtBIvs1MWh06aiG9cjeSc7g0fc5K6AbKF9mry9y53q83Yvxqn_kNfiPad5uIrvwI6OU4HOYl8Niw82CmwjSIYk1Eag0EX5gS5bRKlHmr-8G807a0MrVc8bg07Qh4Q48D03iPAV3G0yZcO8KTa1J75BpKa2H2m000F__0m00)

**5.4. Hợp Nhất Kết Quả Phân Tích**

*5.4.1 Sự Kết Hợp Giữa Hai Ca Sử Dụng*

-   NhânViên: Trung tâm của cả hai ca sử dụng.
-   HệThốngLương: Lớp chính quản lý quy trình thanh toán và thông tin thời gian làm việc.
-   ThờiGian: Lưu trữ thông tin thời gian trong cả hai ca sử dụng.
-   HóaĐơn và XácNhận: Đảm bảo quy trình thanh toán và phê duyệt thông tin được thực hiện chính xác.
  
*5.4.2 Đối Tượng và Quy Trình*
    
Nhân viên tương tác với hệ thống để cập nhật thời gian làm việc và yêu cầu thanh toán. Hệ thống xử lý các yêu cầu này và thông báo trạng thái cho nhân viên.

**5. Kết Luận**

- Tài liệu này đã hợp nhất phân tích cho hai ca sử dụng "Payment" và "Maintain Timecard", giúp cải thiện quy trình quản lý lương và thời gian làm việc tại Acme, Inc.


