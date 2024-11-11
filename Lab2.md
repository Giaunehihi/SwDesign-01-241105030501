# LAB 2
# Phân tích ca sử dụng "Create Administrative Report"

## 1. Xác định các lớp phân tích
Dựa vào luồng sự kiện trong ca sử dụng, chúng ta có thể xác định các lớp phân tích sau:

- **PayrollAdministrator**: Lớp đại diện cho người dùng (tác nhân) tương tác với hệ thống, cụ thể là yêu cầu tạo và lưu báo cáo.
- **ReportCriteria**: Lớp đại diện cho các tiêu chí báo cáo bao gồm loại báo cáo, ngày bắt đầu, ngày kết thúc và tên nhân viên.
- **Report**: Lớp đại diện cho đối tượng báo cáo được tạo dựa trên các tiêu chí đã chọn.
- **ReportGenerator**: Lớp chịu trách nhiệm xử lý việc tạo báo cáo từ các tiêu chí do Payroll Administrator cung cấp.
- **ReportSaver**: Lớp chịu trách nhiệm lưu báo cáo theo tên và vị trí mà Payroll Administrator cung cấp.

## 2. Biểu đồ Sequence (Sequence Diagram)
Dưới đây là biểu đồ sequence mô tả hành vi của các lớp trong quá trình thực hiện ca sử dụng *Create Administrative Report*:

![Diagram](https://www.planttext.com/api/plantuml/png/T991Ri8m44NtFiM85KZq0bbKHAd4hegSNc3gJAabnpPZWvIpTT4ZzGfrOWS1fImYbF_cpv-l_7nzxq94ZgV125JHCRGuiZEcxWTjTOYCqqiCqDR29r0hxT56M4doZcF3EX9hN4s8R1uXUx8qksHc_uZ9qYEbmpELoKw8jeQdv-HHWMB2I9bPRuJSJq9RLy1qF568j_4IKKQR2Zoxi-xfel6ClesUjl1E1srValCMoFRbp-2D6ubUSQ2qgLaYCCKJswiL9OMiu91lNlAfmgJf9MQlWpSuNWuGQEBIFToM7r850U8dGKug8FtAELqroyN6feHRC4vXrCvkPb1sTyrCZJREVcWUPcozkJDKMPouzRM7pBl-R24Jw9_elKl9hOlpuFq9SbcOkb38_QMBrBpOfSVqKVu2003__mC0)

## 3. Nhiệm vụ của từng lớp phân tích

- **PayrollAdministrator**: Tương tác với hệ thống để yêu cầu tạo báo cáo, cung cấp các tiêu chí, xem báo cáo, và lựa chọn lưu hoặc bỏ qua báo cáo.
  
- **ReportCriteria**: Nhận các tiêu chí cho báo cáo từ Payroll Administrator, lưu trữ thông tin cần thiết như loại báo cáo, khoảng thời gian, và tên nhân viên.
  
- **ReportGenerator**: Sử dụng các tiêu chí từ lớp *ReportCriteria* để tạo ra báo cáo. Xử lý trường hợp thiếu hoặc sai định dạng thông tin và yêu cầu nhập lại nếu cần.
  
- **Report**: Đại diện cho báo cáo đã được tạo, được cung cấp cho Payroll Administrator để xem xét và đưa ra quyết định lưu trữ.
  
- **ReportSaver**: Chịu trách nhiệm lưu báo cáo vào vị trí và tên mà Payroll Administrator cung cấp hoặc bỏ qua báo cáo nếu Payroll Administrator không lưu.

## 4. Các thuộc tính và quan hệ giữa các lớp

Dưới đây là một số thuộc tính chính và quan hệ giữa các lớp:

- **PayrollAdministrator**
  - Quan hệ: *PayrollAdministrator* cung cấp thông tin cho *ReportCriteria* và đưa ra yêu cầu cho *ReportGenerator*.
  
- **ReportCriteria**
  - Thuộc tính:
    - `reportType: String` - loại báo cáo (tổng số giờ làm việc hoặc lương tích lũy trong năm).
    - `beginDate: Date` - ngày bắt đầu báo cáo.
    - `endDate: Date` - ngày kết thúc báo cáo.
    - `employeeName: List<String>` - danh sách tên nhân viên cho báo cáo.
  - Quan hệ: *ReportCriteria* cung cấp thông tin cho *ReportGenerator* để tạo báo cáo.

- **ReportGenerator**
  - Quan hệ: *ReportGenerator* sử dụng *ReportCriteria* để tạo một đối tượng *Report*.

- **Report**
  - Thuộc tính:
    - `content: String` - nội dung của báo cáo được tạo dựa trên tiêu chí.
    - `createdDate: Date` - ngày tạo báo cáo.
  - Quan hệ: *Report* được tạo bởi *ReportGenerator* và được lưu bởi *ReportSaver*.

- **ReportSaver**
  - Thuộc tính:
    - `saveLocation: String` - vị trí lưu báo cáo.
    - `saveName: String` - tên báo cáo được lưu.
  - Quan hệ: *ReportSaver* có thể lưu hoặc bỏ báo cáo dựa trên quyết định của *PayrollAdministrator*.
  
## 5. Biểu đồ lớp (Class Diagram)
Dưới đây là biểu đồ lớp mô tả các lớp phân tích và quan hệ giữa chúng:

![Diagram](https://www.planttext.com/api/plantuml/png/V9DDQiCm48NtFiKiOt0k84e8iNSrXLBJ_SGLji2LGZmg3QKdww97wXKwZkNefwPUcJVocpUVnZzVt_kHy4psTSZQ0SSH7Ytg-j8egMjhT0SV6LmVGdD0KwBPv4vfhUvAFF5HM_Rg9hzZ-z2pXxKiVMRErfsQBPpf5WQ3JXBmH6UbErVG7LuEI1LQ0HMI3EHxIKrlsqWdgQUUpvnQGAr6kflTTaluNacgVLRVjmXQ5Q5_4Pg6Wx1ltommLl3Gt4F48-S2vXVlbB3GHbLCT0L4C-6vJGl0m-ZcIZnEnSWJppV51POJKvekDnO1XkNhpT7TY4lkwaT__zmsNPFjBY4ZeerPEnxY4N-tAG7DNwmP-shIGYoO_iqGOHFnxYPCWm0ULPxjfNwP_fvV0000__y30000g)

## 6. Giải thích

Biểu đồ trên mô tả cách các lớp tương tác với nhau để tạo và xử lý một báo cáo hành chính. 

- **PayrollAdministrator** sẽ tương tác với hệ thống qua *ReportGenerator*, cung cấp các tiêu chí cho báo cáo thông qua *ReportCriteria*, và xem báo cáo qua *Report*. Cuối cùng, *ReportSaver* sẽ lưu hoặc bỏ báo cáo dựa trên lựa chọn của *PayrollAdministrator*.

- Các lớp và quy trình này giúp phân tích rõ hơn từng bước xử lý và quản lý báo cáo, đảm bảo tính logic và toàn vẹn trong hệ thống.


# Code Java mô phỏng ca sử dụng Maintain Timecard

Dưới đây là code Java để mô phỏng ca sử dụng *Maintain Timecard*, trong đó hệ thống quản lý thẻ chấm công cho phép các chức năng chính như thêm, chỉnh sửa, xóa và xem các bản ghi chấm công cho từng nhân viên.

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Scanner;

// Model lớp Timecard đại diện cho bản ghi chấm công
class Timecard {
    private String date;
    private double hoursWorked;

    public Timecard(String date, double hoursWorked) {
        this.date = date;
        this.hoursWorked = hoursWorked;
    }

    public String getDate() {
        return date;
    }

    public double getHoursWorked() {
        return hoursWorked;
    }

    public void setHoursWorked(double hoursWorked) {
        this.hoursWorked = hoursWorked;
    }

    @Override
    public String toString() {
        return "Date: " + date + ", Hours Worked: " + hoursWorked;
    }
}

// Lớp Employee đại diện cho một nhân viên và danh sách các bản ghi chấm công của họ
class Employee {
    private String employeeId;
    private String name;
    private List<Timecard> timecards;

    public Employee(String employeeId, String name) {
        this.employeeId = employeeId;
        this.name = name;
        this.timecards = new ArrayList<>();
    }

    public String getEmployeeId() {
        return employeeId;
    }

    public String getName() {
        return name;
    }

    public List<Timecard> getTimecards() {
        return timecards;
    }

    public void addTimecard(Timecard timecard) {
        timecards.add(timecard);
    }

    public void removeTimecard(String date) {
        timecards.removeIf(tc -> tc.getDate().equals(date));
    }

    public Timecard findTimecardByDate(String date) {
        for (Timecard tc : timecards) {
            if (tc.getDate().equals(date)) {
                return tc;
            }
        }
        return null;
    }
}

// Lớp TimecardSystem để quản lý các chức năng chính cho việc Maintain Timecard
class TimecardSystem {
    private Map<String, Employee> employees = new HashMap<>();
    private Scanner scanner = new Scanner(System.in);

    public void addEmployee(String employeeId, String name) {
        employees.put(employeeId, new Employee(employeeId, name));
    }

    public void addTimecard(String employeeId) {
        Employee employee = employees.get(employeeId);
        if (employee == null) {
            System.out.println("Employee not found.");
            return;
        }

        System.out.print("Enter date (YYYY-MM-DD): ");
        String date = scanner.nextLine();
        System.out.print("Enter hours worked: ");
        double hours = scanner.nextDouble();
        scanner.nextLine(); // consume newline

        employee.addTimecard(new Timecard(date, hours));
        System.out.println("Timecard added.");
    }

    public void editTimecard(String employeeId) {
        Employee employee = employees.get(employeeId);
        if (employee == null) {
            System.out.println("Employee not found.");
            return;
        }

        System.out.print("Enter date of timecard to edit (YYYY-MM-DD): ");
        String date = scanner.nextLine();
        Timecard timecard = employee.findTimecardByDate(date);
        if (timecard == null) {
            System.out.println("Timecard not found.");
            return;
        }

        System.out.print("Enter new hours worked: ");
        double newHours = scanner.nextDouble();
        scanner.nextLine(); // consume newline

        timecard.setHoursWorked(newHours);
        System.out.println("Timecard updated.");
    }

    public void deleteTimecard(String employeeId) {
        Employee employee = employees.get(employeeId);
        if (employee == null) {
            System.out.println("Employee not found.");
            return;
        }

        System.out.print("Enter date of timecard to delete (YYYY-MM-DD): ");
        String date = scanner.nextLine();
        employee.removeTimecard(date);
        System.out.println("Timecard deleted if existed.");
    }

    public void viewTimecards(String employeeId) {
        Employee employee = employees.get(employeeId);
        if (employee == null) {
            System.out.println("Employee not found.");
            return;
        }

        System.out.println("Timecards for " + employee.getName() + ":");
        for (Timecard timecard : employee.getTimecards()) {
            System.out.println(timecard);
        }
    }
}

// Lớp Main để chạy hệ thống quản lý timecard
public class Main {
    public static void main(String[] args) {
        TimecardSystem system = new TimecardSystem();
        system.addEmployee("E001", "John Doe");
        system.addEmployee("E002", "Jane Smith");

        Scanner scanner = new Scanner(System.in);
        while (true) {
            System.out.println("\n1. Add Timecard");
            System.out.println("2. Edit Timecard");
            System.out.println("3. Delete Timecard");
            System.out.println("4. View Timecards");
            System.out.println("5. Exit");
            System.out.print("Select an option: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter employee ID: ");
                    String empId = scanner.nextLine();
                    system.addTimecard(empId);
                    break;
                case 2:
                    System.out.print("Enter employee ID: ");
                    empId = scanner.nextLine();
                    system.editTimecard(empId);
                    break;
                case 3:
                    System.out.print("Enter employee ID: ");
                    empId = scanner.nextLine();
                    system.deleteTimecard(empId);
                    break;
                case 4:
                    System.out.print("Enter employee ID: ");
                    empId = scanner.nextLine();
                    system.viewTimecards(empId);
                    break;
                case 5:
                    System.out.println("Exiting...");
                    return;
                default:
                    System.out.println("Invalid option.");
            }
        }
    }
}



