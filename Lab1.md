Lab1

1. Phân tích lớp kiến trúc
1.1Kiến trúc lớp (Layered Architecture)
1.2. Lý do lựa chọn
  Tính tổ chức: Các thành phần được chia thành các lớp rõ ràng giúp việc quản lý và bảo trì hệ thống dễ dàng hơn.
  Tính mô-đun: Các lớp như UI, Business Logic, và Data Access có thể phát triển và thử nghiệm độc lập.
  Bảo mật: Giúp kiểm soát truy cập vào dữ liệu thông qua các lớp, hạn chế quyền truy cập trực tiếp vào lớp Data Access.
1.3:Ý nghĩa các thành phần trong kiến trúc:
   Presentation Layer: Lớp giao diện người dùng (UI) chịu trách nhiệm hiển thị thông tin và thu thập dữ liệu từ người dùng. Các hoạt động như nhập giờ làm, lựa chọn phương thức thanh toán sẽ được thực hiện tại đây.
  Business Logic Layer: Lớp logic nghiệp vụ xử lý các quy tắc nghiệp vụ, như tính toán bảng lương, kiểm tra giờ làm việc hợp lệ, và quản lý phương thức thanh toán.
  Data Access Layer: Lớp truy cập dữ liệu chịu trách nhiệm kết nối với cơ sở dữ liệu và truy vấn dữ liệu từ hệ thống cũ (Project Management Database).
  Integration Layer: Lớp tích hợp để đảm bảo giao tiếp với hệ thống DB2 trên IBM mainframe.

1.4.Pakage
https://www.planttext.com/api/plantuml/png/T5AzJGCn5EuznUkeia0A550eJX0fWcI05z_Zpk2pBTidT48CmGo8yXQ8YnHCuWbO0PkVo93GVl_FydlOpPn7w_jECeFy7Xk2TGMF381BT0ukEYFrGBIkzj1ATCJHrWMqnA4ZvHVaMvtn9xPFE--TKEJSbMu4BuAJnMefbrRpn6fxF6k1AeNOW-uVl2YQeySpdiEEpBycevtmsWu7KGLLf5NAKsFH2wtAqLRV4VTVxNbbBjsWesmzWJdTfbl1almqkbOO1nlo3qGAlfCTI-yxcPp-UPWftCGmGXt3gshORowhY-kciBBz03nkHyCAFClAsKdtDl8MsXXU32kPhFptbEIxZDkT1nN3is1iHghEt-C3003__mC0
