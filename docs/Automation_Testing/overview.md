# Automation Testing

**Automation Testing** là quá trình sử dụng các công cụ phần mềm để thực hiện kiểm thử tự động cho các ứng dụng phần mềm. Mục tiêu chính của automation testing là giảm thiểu sự can thiệp của con người trong quá trình kiểm thử, tăng tốc độ và độ chính xác của việc phát hiện lỗi, giúp đảm bảo chất lượng của ứng dụng phần mềm. Dưới đây là tổng quan về các khía cạnh chính của automation testing:

## Tổng quan

#### 1. Lợi ích của Automation Testing

* Tiết kiệm thời gian và công sức: Khi các trường hợp kiểm thử (test cases) được tự động hóa, chúng có thể chạy nhiều lần mà không cần can thiệp thủ công.
* Tăng tính chính xác: Kiểm thử thủ công dễ gặp sai sót do con người gây ra, trong khi các công cụ tự động sẽ thực hiện đúng theo lập trình.
* Khả năng tái sử dụng: Các tập lệnh (scripts) kiểm thử tự động có thể được tái sử dụng trên các phiên bản khác nhau của phần mềm mà không cần viết lại từ đầu.
* Cải thiện phạm vi kiểm thử: Các kịch bản kiểm thử có thể được thực thi trên nhiều môi trường, nền tảng và cấu hình khác nhau.

#### 2. Các loại Automation Testing

* Functional Testing: Kiểm thử các chức năng cụ thể của phần mềm theo yêu cầu đã được mô tả.
* Regression Testing: Đảm bảo các thay đổi mới không gây ra lỗi ở các phần đã hoạt động ổn định trước đó.
* Load Testing: Đo lường hiệu suất của hệ thống khi bị tải nặng.
* Integration Testing: Đảm bảo các module khác nhau của phần mềm làm việc tốt với nhau.
* Unit Testing: Kiểm thử từng phần nhỏ nhất của mã nguồn (thường do các lập trình viên thực hiện).

#### 3. Các công cụ Automation Testing phổ biến

* Selenium: Một công cụ mã nguồn mở hỗ trợ kiểm thử trên nhiều trình duyệt và hệ điều hành.
* JUnit, TestNG: Dùng cho kiểm thử unit trong các ứng dụng Java.
* Cypress: Công cụ kiểm thử front-end hiện đại với khả năng tích hợp tốt vào các dự án web.
* Postman, RestAssured: Dùng cho kiểm thử API.
* Appium: Dành cho kiểm thử ứng dụng di động.
* JMeter: Sử dụng để kiểm thử hiệu suất (performance testing).

#### 4. Quy trình Automation Testing

* Lựa chọn các trường hợp kiểm thử để tự động hóa: Chọn các test cases có tính lặp lại nhiều lần, dễ gây lỗi hoặc quan trọng cho hệ thống.
* Chọn công cụ phù hợp: Phụ thuộc vào yêu cầu của dự án và ngôn ngữ lập trình đang sử dụng.
* Viết script kiểm thử tự động: Sử dụng ngôn ngữ lập trình hoặc các ngôn ngữ script mà công cụ hỗ trợ.
* Thực thi và phân tích kết quả: Chạy các script và theo dõi kết quả để phát hiện lỗi.
* Bảo trì test cases: Cập nhật các kịch bản kiểm thử khi có thay đổi trong phần mềm.

#### 5. Thách thức trong Automation Testing

* Chi phí ban đầu cao: Việc tạo lập và duy trì kịch bản tự động có thể đòi hỏi nhiều thời gian và công sức ban đầu.
* Bảo trì test scripts: Khi phần mềm thay đổi, các test scripts cũng cần được cập nhật liên tục.
* Không thay thế hoàn toàn kiểm thử thủ công: Automation testing không phù hợp cho tất cả các trường hợp, đặc biệt là kiểm thử trải nghiệm người dùng hoặc các tình huống phức tạp.

#### 6. Khi nào nên sử dụng Automation Testing?

* Dự án có thời gian dài hạn và yêu cầu kiểm thử lặp lại nhiều lần.
* Khi có các tác vụ kiểm thử phức tạp, khó thực hiện thủ công.
* Khi cần kiểm thử trên nhiều môi trường hoặc nền tảng khác nhau.
* Kiểm thử hiệu năng hoặc khả năng chịu tải của hệ thống.

#### 7. Sự khác biệt giữa Automation Testing và Manual Testing

* Automation Testing: Các kịch bản kiểm thử được thực hiện bởi máy móc, có thể tái sử dụng và ít rủi ro lỗi do con người.
* Manual Testing: Các kiểm thử viên thực hiện bằng tay, phù hợp với những trường hợp yêu cầu phân tích, sáng tạo và tương tác nhiều.

## Một số loại chính của Automation Testing

#### 1. Functional Testing (Kiểm thử chức năng)

* **Mục đích:** Đảm bảo các chức năng của phần mềm hoạt động theo yêu cầu đã được mô tả. Tự động hóa các kiểm thử chức năng giúp đảm bảo rằng mọi thay đổi trong mã nguồn không làm ảnh hưởng đến chức năng chính.
* **Công cụ:** Selenium, QTP (Quick Test Professional), Cypress, Katalon Studio.

#### 2. Regression Testing (Kiểm thử hồi quy)

* **Mục đích:** Đảm bảo rằng các tính năng mới được thêm vào hoặc các thay đổi mã nguồn không ảnh hưởng đến các tính năng hiện có. Đây là một trong những loại kiểm thử tự động phổ biến nhất vì nó yêu cầu thực hiện lặp lại nhiều lần khi có sự thay đổi trong phần mềm.
* **Công cụ:** Selenium, JUnit, TestNG.

#### 3. Smoke Testing (Kiểm thử khói)

* **Mục đích:** Kiểm tra nhanh các chức năng cơ bản của ứng dụng sau mỗi lần build để đảm bảo phần mềm không có lỗi nghiêm trọng. Đây là quá trình kiểm thử cấp cao để xác nhận rằng phần mềm chạy ổn định trước khi tiến hành các kiểm thử chi tiết hơn.
* **Công cụ:** Selenium, Katalon Studio.\

#### 4. Load Testing (Kiểm thử tải)

* **Mục đích:** Đánh giá hiệu suất của hệ thống dưới tải nặng, xác định khả năng chịu tải của ứng dụng trong điều kiện thực tế khi có nhiều người dùng hoặc thao tác đồng thời.
* **Công cụ:** Apache JMeter, LoadRunner, Gatling.

#### 5. Performance Testing (Kiểm thử hiệu năng)

* **Mục đích:** Đo lường và đánh giá hiệu năng của hệ thống như tốc độ phản hồi, thời gian xử lý, sử dụng tài nguyên khi thực hiện khối lượng công việc nhất định. Nó giúp phát hiện các điểm yếu về hiệu suất trong ứng dụng.
* **Công cụ:** Apache JMeter, BlazeMeter.

#### 6. Integration Testing (Kiểm thử tích hợp)

* **Mục đích:** Kiểm thử sự tương tác giữa các module hoặc thành phần khác nhau của hệ thống để đảm bảo chúng hoạt động trơn tru cùng nhau. Tự động hóa giúp đảm bảo việc kiểm tra tích hợp diễn ra liên tục sau mỗi thay đổi.
* **Công cụ:** Selenium, Postman, RestAssured (API Testing).

#### 7. Unit Testing (Kiểm thử đơn vị)

* **Mục đích:** Kiểm thử các đơn vị nhỏ nhất của mã nguồn (thường là hàm hoặc phương thức) để đảm bảo chúng hoạt động đúng. Đây là loại kiểm thử thường do các lập trình viên thực hiện.
* **Công cụ:** JUnit, TestNG, PyTest, NUnit.

#### 8. Acceptance Testing (Kiểm thử chấp nhận)

* **Mục đích:** Xác nhận rằng hệ thống đáp ứng các yêu cầu kinh doanh và hoạt động đúng theo mong đợi của người dùng. Kiểm thử này giúp xác định liệu hệ thống đã sẵn sàng để triển khai hay chưa.
* **Công cụ:** Selenium, Cucumber (BDD).

#### 9. Security Testing (Kiểm thử bảo mật)

* **Mục đích:** Xác định các lỗ hổng bảo mật trong hệ thống. Automation testing giúp thực hiện các kiểm thử xâm nhập (penetration testing) và các kịch bản kiểm thử bảo mật tự động.
* **Công cụ:** OWASP ZAP, Burp Suite.

#### 10. API Testing (Kiểm thử API)

* **Mục đích:** Kiểm thử tính đúng đắn của các API mà ứng dụng giao tiếp với nhau. Tự động hóa kiểm thử API giúp đảm bảo API hoạt động ổn định và hiệu quả.
* **Công cụ:** Postman, RestAssured, SoapUI.

#### 11. UI Testing (Kiểm thử giao diện người dùng)

* **Mục đích:** Đảm bảo rằng giao diện người dùng của ứng dụng hoạt động đúng và hiển thị chính xác. Đây là loại kiểm thử giúp xác nhận trải nghiệm người dùng khi tương tác với hệ thống.
* **Công cụ:** Selenium, Cypress, Appium (cho ứng dụng di động).

#### 12. End-to-End Testing (Kiểm thử đầu-cuối)

* **Mục đích:** Kiểm thử toàn bộ quy trình hoạt động của ứng dụng từ đầu đến cuối để đảm bảo rằng tất cả các thành phần trong hệ thống hoạt động liền mạch.
* **Công cụ:** Selenium, Cypress, TestComplete.

#### 13. Cross-browser Testing (Kiểm thử trên nhiều trình duyệt)

* **Mục đích:** Đảm bảo ứng dụng hoạt động nhất quán trên nhiều trình duyệt khác nhau (Chrome, Firefox, Safari, etc.).
* **Công cụ:** Selenium, BrowserStack, Sauce Labs.

#### 14. Mobile Testing (Kiểm thử di động)

* **Mục đích:** Kiểm thử các ứng dụng di động trên nhiều thiết bị và hệ điều hành khác nhau (Android, iOS) để đảm bảo trải nghiệm người dùng tốt nhất.
* **Công cụ:** Appium, TestComplete Mobile.

## Một số công cụ, thư viện phổ biến trong Python hỗ trợ cho các loại kiểm thử khác nhau

#### 1. Selenium

* **Mục đích:** Kiểm thử tự động cho các ứng dụng web bằng cách tương tác với trình duyệt.
* **Ưu điểm:**

      - Hỗ trợ nhiều trình duyệt (Chrome, Firefox, Safari, etc.).
      - Có thể tích hợp với các framework kiểm thử khác như PyTest, unittest.
      - Hỗ trợ nhiều ngôn ngữ lập trình, bao gồm Python.

* **Cách sử dụng:** Dùng để tự động hóa các tác vụ như nhấp chuột, nhập văn bản, lấy dữ liệu từ trang web, v.v.
* **Cài đặt:**

```pip  
pip install selenium
```

#### 2. PyTest

* **Mục đích:** Framework kiểm thử Python, thường được sử dụng cho Unit Testing và Integration Testing.
* **Ưu điểm:**

      - Dễ sử dụng và mở rộng.
      - Hỗ trợ kiểm thử đơn vị (unit testing) và hồi quy (regression testing).
      - Có thể tích hợp với Selenium để kiểm thử giao diện người dùng (UI testing).
  
* **Cài đặt**

```pip  
pip install pytest
```

#### 3. Unittest

* **Mục đích:** Thư viện kiểm thử đơn vị (unit testing) tích hợp sẵn trong Python.
* **Ưu điểm:**

      - Đơn giản và phổ biến.
      - Hỗ trợ nhiều loại kiểm thử như unit testing, integration testing.
      - Cách sử dụng: Được sử dụng để viết và thực thi các test cases tự động.

* **Cài đặt:** Đã có sẵn trong Python (không cần cài đặt riêng).

#### 4. Robot Framework

* **Mục đích:** Framework kiểm thử tự động dựa trên từ khóa (keyword-driven testing), có thể mở rộng với các thư viện như Selenium để kiểm thử ứng dụng web.
* **Ưu điểm:**

      - Dễ sử dụng với cú pháp rõ ràng, phù hợp cho cả những người không phải lập trình viên.
      - Tích hợp dễ dàng với Selenium và API Testing.
      - Hỗ trợ kiểm thử nhiều loại như functional, acceptance, và UI testing.

* **Cài đặt:**

```pip  
pip install robotframework
pip install robotframework-seleniumlibrary
```

#### 5. Behave

* **Mục đích:** Framework kiểm thử tự động dựa trên Behavior-Driven Development (BDD), giúp viết các test cases dễ hiểu cho các bên không chuyên kỹ thuật.
* **Ưu điểm:**

     - Test cases được viết dưới dạng ngôn ngữ tự nhiên (Gherkin), dễ đọc và hiểu.
     - Phù hợp cho kiểm thử chấp nhận (acceptance testing).

* **Cài đặt:**

```pip  
pip install pytest
```

#### 6. Locust

* **Mục đích:** Công cụ kiểm thử tải và hiệu năng (Load Testing, Performance Testing).
* **Ưu điểm:**

     - Dễ dàng viết kịch bản kiểm thử hiệu năng với Python.
     - Tạo ra các tình huống tải lớn để kiểm tra khả năng chịu tải của hệ thống.
     - Giao diện web dễ sử dụng để giám sát kết quả kiểm thử.

* **Cài đặt:**

```pip  
pip install locust
```

#### 7. Postman + Newman

* **Mục đích:** Kiểm thử API, tự động hóa các yêu cầu HTTP.
* **Ưu điểm:**

    - Dễ sử dụng cho kiểm thử API RESTful.
    - Postman hỗ trợ tạo và thực thi các bộ kiểm thử API, còn Newman giúp tích hợp các kịch bản đó vào quy trình CI/CD.

* **Cài đặt:**

    - Postman: tải từ trang chính thức.
    - Newman:

```pip  
npm install -g newman
```

#### 8. Requests + PyTest (API Testing)

* **Mục đích:** Kiểm thử API bằng cách sử dụng thư viện requests để gửi yêu cầu HTTP và pytest để kiểm tra kết quả.
* **Ưu điểm:**

    - Đơn giản và mạnh mẽ cho các trường hợp kiểm thử API.
    - Dễ dàng kết hợp với các framework kiểm thử khác như PyTest để kiểm tra kết quả.

* **Cài đặt:**

```pip  
pip install requests
pip install pytest
```

#### 9. Appium (Mobile Testing)

* **Mục đích:** Kiểm thử ứng dụng di động (Android, iOS) bằng cách tương tác với giao diện người dùng.
* **Ưu điểm:**

    - Hỗ trợ nhiều nền tảng di động (Android, iOS).
    - Có thể sử dụng cùng với Selenium cho kiểm thử ứng dụng di động.

* **Cài đặt:**

```pip  
pip install Appium-Python-Client
```

#### 10. JMeter (Performance Testing)

* **Mục đích:** Công cụ kiểm thử hiệu năng, đo lường tốc độ, khả năng chịu tải của hệ thống.
* **Ưu điểm:**

    - Mạnh mẽ và tùy chỉnh cho kiểm thử hiệu năng trên các giao thức khác nhau (HTTP, FTP, WebSockets, etc.).
  
* **Cài đặt:**

    - Cài đặt JMeter qua file .zip từ trang chính thức.
  
#### 11. Allure (Test Reporting)

* **Mục đích:** Tạo báo cáo kiểm thử với giao diện đồ họa rõ ràng, trực quan.
* **Ưu điểm:**

    - Cung cấp báo cáo kiểm thử chi tiết và có giao diện thân thiện.
    - Dễ dàng tích hợp với PyTest, Robot Framework, Selenium.

* **Cài đặt:**

```pip  
pip install allure-pytest
```

#### 12. PyAutoGUI (UI Testing)

* **Mục đích:** Tự động hóa các thao tác trên màn hình máy tính, chẳng hạn như nhấp chuột, nhập văn bản, di chuyển chuột.
* **Ưu điểm:**

    - Phù hợp cho kiểm thử giao diện người dùng đơn giản.
    - Hỗ trợ tương tác trực tiếp với giao diện desktop.

* **Cài đặt:**

```pip  
pip install pyautogui
```