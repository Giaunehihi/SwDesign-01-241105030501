# Class Design - Payroll System

## **1. Authentication Subsystem**

### Operations & Methods
- `login()`: Thực hiện xác thực thông tin đăng nhập.  
- `logout()`: Đăng xuất khỏi hệ thống.  
- `validateUser()`: Kiểm tra thông tin đăng nhập.  
- `grantAccess()`: Cấp quyền truy cập dựa trên vai trò.

### State
- **LoggedOut**: Trạng thái mặc định, chưa đăng nhập.  
- **LoggedIn**: Đã xác thực và đăng nhập thành công.

### Attributes
- `userId`: int  
- `password`: string  
- `role`: string  
- `session`: string  

### Dependencies & Associations
- **LoginForm** phụ thuộc vào **SecurityManager**.  
- **SecurityManager** phụ thuộc vào **UserDatabase**.

 ![diagram](https://www.planttext.com/api/plantuml/png/N8z12W8n34NtFKMNkfWBk90HH11q9HuWjg4KEgqagIBYoLnu9AzWYpCwJ7R_ytxoytw-MXOWoLrG9W2ptYNduoPHf-zArmdLcCr_8cKfwg5w_e0cavVR7Y8uf25rWU0j21uPQGWxWYWhOv1vlA4YQn0u0MCVRtBnjdQXVPIlSIxaDL6nMCX7L-F_gaspd1PHqsAL6PzIBKPR_lu0003__mC0) 

 
## **2. Timecard Management Subsystem**

### Operations & Methods
- `createTimecard()`: Tạo bảng chấm công cho nhân viên.  
- `editTimecard()`: Chỉnh sửa bảng chấm công.  
- `deleteTimecard()`: Xóa bảng chấm công.  
- `getTimecard()`: Lấy thông tin bảng chấm công cụ thể.  

### State
- **Pending**: Chưa được phê duyệt.  
- **Approved**: Đã được xác nhận và phê duyệt.  

### Attributes
- `employeeId`: int  
- `timeIn`: datetime  
- `timeOut`: datetime  
- `status`: string  

### Dependencies & Associations
- **TimecardForm** liên kết với **Employee**.  
- **TimecardManager** truy cập dữ liệu từ **TimecardDatabase**.

 ![diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niK98PcvgSc9HYbj-KQv2DPS222GNfIQMfC9aD3GXegafcINeOYcfEQaeAckveEQwvXRav5UcfaBDr4s5yZrJh1GoyqeWWdc9kQbM2iKbHPbvwGYjCEDS4aiIanABOKOefAUMeDg4udPTNJkufPWow6PoEQJcfO120G000F__0m00) 

## **3. Payroll Processing Subsystem**

### Operations & Methods
- `calculatePayroll()`: Tính lương dựa trên bảng chấm công.  
- `generatePayslip()`: Tạo phiếu lương.  
- `processPayroll()`: Xử lý thanh toán cho nhân viên.  

### State
- **PendingPayment**: Đã tính toán nhưng chưa thanh toán.  
- **Paid**: Đã thanh toán đầy đủ.  

### Attributes
- `payrollId`: int  
- `employeeId`: int  
- `totalHours`: double  
- `grossSalary`: double  
- `netSalary`: double  
- `taxes`: double  

### Dependencies & Associations
- **PayrollManager** truy cập vào **TimecardDatabase** và **SalaryDatabase**.  
- **PayslipForm** phụ thuộc vào **PayrollManager**.

 ![diagram](https://www.planttext.com/api/plantuml/png/Z90z2W8n48Nxd2Ab5dk1BMGB6mj1KB2UJOPrSJPPPf8YY2Upy4XUGPQiFmGBf_pUuxtXFMxtHW9mY0CfGo2YTv3O4st1GOUiBqfFPu1C90WuoujbvXqwv8o5-l65H_O6HJxcgvhZzq30QGq1MX2SuoiSHl89SMDhtRkGOSTU9FjhRNri2RFWC1Ju7N_e1pJ0zg-2auyiHyzdjDz9nG9LjIg-_kKeYrM3pawhFW400F__0m00) 

## **4. Reporting Subsystem**

### Operations & Methods
- `generateReport()`: Tạo báo cáo bảng lương.  
- `generateProjectReport()`: Tạo báo cáo dựa trên thời gian làm việc cho dự án.  
- `exportReport()`: Xuất báo cáo sang các định dạng (PDF, Excel).  

### State
- **ReportGenerated**: Báo cáo đã được tạo thành công.  
- **ReportExported**: Báo cáo đã được xuất.  

### Attributes
- `reportId`: int  
- `reportType`: string  
- `format`: string  
- `generatedOn`: datetime  

### Dependencies & Associations
- **ReportGenerator** sử dụng **PayrollDatabase** và **ProjectDatabase** để lấy dữ liệu.

 ![diagram](https://www.planttext.com/api/plantuml/png/R9112i9034NtSufPwc8kq8LqKL1tnHkaRP1gsfHCIYtYoLnu9AyWmnHnYjdb_V1_alVpbNi5qR4ZKnDuRqyuiEWUUnHG5ditDjGv0epoPflIKlY2jQOYtaBtPG-p99Gm2nCLe521noN1OJSGpuZ79hDjhn5w892vG8MMV6OR7Yl27wkOkxOQ8awS9fRhWKT9NDR7EhTRh_T_9iqrEVPDUE47003__mC0) 


## **5. Project Management Subsystem**

### Operations & Methods
- `assignProject()`: Phân công dự án cho nhân viên.  
- `trackProjectHours()`: Theo dõi số giờ làm việc cho từng dự án.  
- `generateProjectReport()`: Tạo báo cáo cho từng dự án.  

### State
- **Assigned**: Dự án đã được phân công.  
- **Completed**: Dự án đã hoàn thành.  

### Attributes
- `projectId`: int  
- `employeeId`: int  
- `hoursWorked`: double  
- `projectStatus`: string  

### Dependencies & Associations
- **ProjectManager** truy cập **EmployeeDatabase** và **ProjectDatabase**.

 ![diagram](https://www.planttext.com/api/plantuml/png/R90n3i8m34Ntd28Z3Bb01zG191X024vWMYiAj4bbkmD2d8o18t45g6e4BNXyt_xVzkDsprc0fAqhKrJ0RBUKZbZ86Y9u97injgkN4dnKRJBjeH0K9sNBr1A_1OyH2GHLss6Jg9kw6WrPr4sLpeXp43W0eyOuLBugCnkY3E46Qimi2uNeFrQQCNPgUZmmKhONa9Q_dKOtEpVxsV1VpoZQv1ZBxf5F0000__y30000) 


## **6. BankSystem Subsystem**

### Operations & Methods
- `initiateTransfer()`: Khởi tạo giao dịch chuyển tiền cho nhân viên.  
- `verifyTransaction()`: Xác minh giao dịch trước khi thực hiện.  
- `completeTransaction()`: Hoàn thành giao dịch.  

### State
- **TransactionInitiated**: Giao dịch đã được khởi tạo.  
- **TransactionVerified**: Giao dịch đã được xác minh và sẵn sàng thực hiện.  
- **TransactionCompleted**: Giao dịch đã hoàn tất.  

### Attributes
- `transactionId`: int  
- `amount`: double  
- `status`: string  
- `employeeId`: int  

### Dependencies & Associations
- **BankTransactionManager** liên kết với **BankDatabase**.

 ![diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niO9JObvsI55YNd5YSabcVfvlObvYUcgHGZMN0WXavcMMP2QMf89LfAKMQMX2nCjIYpBJAf7qmIIIytCBSbAX6k1IjLn8jhaabYGc9HQdGktGBK4ezKon0bfP0X5F1PgKNvcQ2XC46eB3iRgwTYWcSpcavgM0l0W0003__mC0) 

