# Lab 3: Xác định các phần tử thiết kế

## 1. Biểu đồ ngữ cảnh của các hệ thống con

### 1.1 BankSystem
![Diagram](https://www.planttext.com/api/plantuml/png/H8v12W8n34NtFKNeVd3lGeQA-q9F4AOHYcqp974nPtFXaRo27HNSXRpta_zwF6Sr5Bktwd0n5eYu2TUQDZLgW0en_KZ0VlklGt8k9fYcqnZX23vHpv2Bq6AGQMKj1YROTQGBT_KkVFNuqS_ShqKQxknm4HaFX7GT8datZrjxfJS0003__mC0). <br>

***Mô tả:*** 

**Chức năng:**  Xử lý giao dịch lương qua ngân hàng, đảm bảo thanh toán chính xác và kịp thời.

**Giao diện:** <br>
  **- Đầu vào:** Giao dịch chuyển khoản (thông tin tài khoản, số tiền).<br>
  **- Đầu ra:** Xác nhận hoặc thông báo lỗi.<br>
  **- Giao thức:** API giao dịch ngân hàng.<br>
### 1.2 PrintService <br>
![Diagram](https://www.planttext.com/api/plantuml/png/D8x12SCm34NldaBudWLwA84kOE89HAeMWIsxibBmR3rafAvGREZjmtiF_lTphirGxSZ9uMv58M3NabBipIW3DWZnJvJ58kcRTvfWYyw52Cjo7Hiku3Tw7TGCAlQMk48T2SlJko5CSNgt8W_MZCP5l5j9xkF03m00__y30000) <br>

***Mô tả*** <br>
**Chức năng:** In phiếu lương và các tài liệu liên quan. <br>
**Giao diện:**<br>
 **- Đầu vào:** Yêu cầu in phiếu lương (tên nhân viên, số tiền, ngày tháng).<br>
 **- Đầu ra:** Xác nhận in thành công hoặc lỗi.<br>
 **- Giao thức:** Giao diện in nội bộ hoặc API.<br>

### 1.3 ProjectManagementDatabase
![Diagram](https://www.planttext.com/api/plantuml/png/F8ux3i8m44HxdsALFXUWG2dIHhBm2HPx543-W7U3bBDHS2Ik00w2RgJtPZIlntCGvQfBYeQzbagMrrfYTAie4h6GTJzIomLU9yuy8o7hoCf75cpMD1fZ7VNzlcNQKNV0RO4eNRyzyYUkCyYN0EbCapRPDVUpVJ-7FnoGGxlq1W00__y30000
)

***Mô tả:*** <br>
**Chức năng:** Cung cấp dữ liệu dự án và mã charge cho hệ thống quản lý thẻ chấm công. <br>
**Giao diện:** <br>
  **- Đầu vào:** Yêu cầu truy vấn mã số charge từ PayrollSystem.<br>
  **- Đầu ra:** Kết quả truy vấn danh sách mã dự án.<br>
  **- Giao thức:** JDBC hoặc API RESTful.<br>

## 2. Ánh xạ lớp phân tích đến phần tử thiết kế

| Lớp phân tích         | Phần tử thiết kế                |
|----------------------|--------------------------------|
| Employee             | Employee Entity Class          |
| Timecard             | Timecard DAO Class             |
| PayrollAdministrator | Payroll Admin Control Class    |
| ProjectManagement    | Project Database Access Layer  |

## 3. Gộp nhóm phần tử thiết kế vào các gói
***Các phần tử thiết kế được tổ chức thành các gói:*** <br>

**Domain Layer:** Quản lý nghiệp vụ chính (Employee, Timecard).<br>
**Application Layer:** Xử lý logic ứng dụng (Payroll Admin Control Class).<br>
**Infrastructure Layer:** Tương tác với hệ thống phụ (Project Database Access Layer).<br>

***Biểu đồ Packages:*** <br>
![Diagram](https://www.planttext.com/api/plantuml/png/R8yx2i9G44Nxjuf7Lf9WB0GB2pTmdOpozFsOcHGXk38Bb-GMZ8qYfBm7pe7xUZnRDOYDAReAkk72lkbBGiX-ZucbyRFpdY9K_JRLM2RcBpY6n0GPtDtzxAxM60WMoahYW4bAZDsGGjwKRCluatVvB52JaMmKNl6bN9ciX-44vOw8LPT2otduV7W3003__mC0)

## 4. Kiến trúc layers và quan hệ phụ thuộc
***Biểu đồ layers:*** <br>
![Diagram](https://www.planttext.com/api/plantuml/png/R90x3i8m38RtdCBgtYkWyXegTK12JAY32QQAQ9F8JX08SJ86ZiGLQ650VQoV_y-_vVVpbKb03h6fbKTzneeWsJ09sO31E0i5teWJk2k0_Iw7fMkyi-rKIlLGVsVkVMtqM5b4CPP4e72LqNqdjoT62HnrY4mzROK13oW4SwrRk-pO-Xg8BTQm9RwO5d-t3Ow2D9sDMuVWbngLJCScUZEon-vb7m000F__0m00) <br>

***Giải thích:*** <br>
**- Presentation Layer:** Giao diện người dùng.<br>
**- Application Layer:** Xử lý logic nghiệp vụ.<br>
**- Infrastructure Layer:** Kết nối cơ sở dữ liệu và hệ thống phụ.<br>


