# Creating test suites

Các trường hợp kiểm thử trong Robot Framework được tạo ra trong các tệp kiểm thử, có thể được tổ chức thành các thư mục. Những tệp và thư mục này tạo ra một cấu trúc bộ kiểm thử phân cấp. Các khái niệm tương tự cũng được áp dụng khi tạo các tác vụ, nhưng thuật ngữ sẽ khác.

## Suite files

Các trường hợp kiểm thử trong Robot Framework được tạo ra bằng cách sử dụng các phần kiểm thử trong các tệp bộ kiểm thử, còn được gọi là tệp kiểm thử. Một tệp như vậy tự động tạo ra một bộ kiểm thử từ tất cả các trường hợp kiểm thử mà nó chứa. Không có giới hạn tối đa cho số lượng trường hợp kiểm thử có thể có, nhưng nên có ít hơn mười trường hợp, trừ khi phương pháp dữ liệu động được sử dụng, trong đó một trường hợp kiểm thử chỉ bao gồm một từ khóa cấp cao.

Các cài đặt sau trong phần Cài đặt có thể được sử dụng để tùy chỉnh bộ kiểm thử:

* **Name**: Sử dụng để thiết lập tên bộ kiểm thử tùy chỉnh. Tên mặc định được tạo dựa trên tên tệp hoặc thư mục.

* **Documentation**: Sử dụng để chỉ định tài liệu cho bộ kiểm thử.

* **Metadata**: Sử dụng để thiết lập siêu dữ liệu tự do cho bộ kiểm thử dưới dạng cặp tên-giá trị.

* **Suite Setup** and **Suite Teardown**: Xác định cài đặt và dọn dẹp cho bộ kiểm thử.

!!! Note 
    Các tên cài đặt không phân biệt chữ hoa chữ thường, nhưng định dạng được sử dụng ở trên là được khuyến nghị.

## Suite directories

Các tệp kiểm tra có thể được tổ chức thành các thư mục, và các thư mục này tạo ra các bộ kiểm tra cấp cao hơn. Một bộ kiểm tra được tạo từ một thư mục không thể có bất kỳ trường hợp kiểm tra nào trực tiếp, nhưng nó chứa các bộ kiểm tra khác với các trường hợp kiểm tra bên trong. Các thư mục này có thể được đặt vào các thư mục khác, tạo ra một bộ kiểm tra cấp cao hơn nữa. Không có giới hạn nào cho cấu trúc, vì vậy các trường hợp kiểm tra có thể được tổ chức theo cách cần thiết.

Khi một thư mục kiểm tra được thực thi, các tệp và thư mục bên trong nó được xử lý một cách đệ quy như sau:

* Các tệp và thư mục có tên bắt đầu bằng dấu chấm (.) hoặc dấu gạch dưới (_) sẽ bị bỏ qua.

* Các thư mục có tên CVS sẽ bị bỏ qua (phân biệt chữ hoa chữ thường).

* Các tệp ở định dạng tệp được hỗ trợ sẽ được xử lý.

* Các tệp khác sẽ bị bỏ qua.

Nếu một tệp hoặc thư mục được xử lý không chứa bất kỳ trường hợp kiểm tra nào, nó sẽ bị bỏ qua một cách lặng lẽ (một thông điệp sẽ được ghi vào syslog) và việc xử lý sẽ tiếp tục.

#### Suite initialization files

Một bộ kiểm tra được tạo từ một thư mục có thể có các thiết lập tương tự như một bộ được tạo từ tệp kiểm tra. Bởi vì một thư mục đơn lẻ không thể có loại thông tin đó, nó phải được đặt vào một tệp khởi tạo bộ kiểm tra đặc biệt. Tên tệp khởi tạo phải luôn có định dạng init.ext, trong đó phần mở rộng phải là một trong các định dạng tệp được hỗ trợ (thông thường là init.robot). Định dạng tên này được vay mượn từ Python, nơi các tệp có tên như vậy cho biết rằng một thư mục là một mô-đun.

Bắt đầu từ Robot Framework 6.1, cũng có thể định nghĩa một tệp khởi tạo bộ kiểm tra cho các bộ kiểm tra được tạo tự động khi bắt đầu thực thi kiểm tra bằng cách cung cấp nhiều đường dẫn.

Các tệp khởi tạo có cùng cấu trúc và cú pháp như các tệp kiểm tra, ngoại trừ việc chúng không thể có các phần trường hợp kiểm tra và không phải tất cả các thiết lập đều được hỗ trợ. Các biến và từ khóa được tạo ra hoặc nhập khẩu trong các tệp khởi tạo không có sẵn trong các bộ kiểm tra cấp thấp hơn. Nếu bạn cần chia sẻ biến hoặc từ khóa, bạn có thể đặt chúng vào các tệp tài nguyên có thể được nhập khẩu bởi cả tệp khởi tạo và tệp kiểm tra.

Mục đích chính của các tệp khởi tạo là chỉ định các thiết lập liên quan đến bộ kiểm tra tương tự như trong các tệp bộ, nhưng việc thiết lập một số thiết lập liên quan đến trường hợp kiểm tra cũng có thể được thực hiện. Dưới đây là cách sử dụng các thiết lập khác nhau trong các tệp khởi tạo.

* **Name, Documentation, Metadata, Suite Setup, Suite Teardown**: Các thiết lập cụ thể cho bộ này hoạt động giống như trong các tệp khởi tạo bộ.

* **Test Tags**: Các thẻ được chỉ định sẽ được đặt không điều kiện cho tất cả các kiểm tra trong tất cả các tệp bộ mà thư mục này chứa, một cách đệ quy. Mới trong Robot Framework 6.1. Thẻ Force đã bị loại bỏ cần được sử dụng với các phiên bản cũ hơn.

* **Test Setup, Test Teardown, Test Timeout**: Đặt giá trị mặc định cho thiết lập/dọn dẹp kiểm tra hoặc thời gian chờ kiểm tra cho tất cả các trường hợp kiểm tra mà thư mục này chứa. Có thể ghi đè ở cấp thấp hơn. Lưu ý rằng các từ khóa được sử dụng làm thiết lập và dọn dẹp phải có sẵn trong các tệp kiểm tra nơi các kiểm tra sử dụng chúng. Việc định nghĩa các từ khóa trong tệp khởi tạo tự nó là không đủ.

* **Task Setup, Task Teardown, Task Tags, Task Timeout**: Các bí danh cho Thiết lập kiểm tra, Dọn dẹp kiểm tra, Thẻ kiểm tra và Thời gian chờ kiểm tra, tương ứng, có thể được sử dụng khi tạo tác vụ, không phải kiểm tra.

* **Default Tags, Test Template**: Không được hỗ trợ trong các tệp khởi tạo.

```robotframework
*** Settings ***
Documentation    Example suite
Suite Setup      Do Something    ${MESSAGE}
Test Tags        example
Library          SomeLibrary

*** Variables ***
${MESSAGE}       Hello, world!

*** Keywords ***
Do Something
    [Arguments]    ${args}
    Some Keyword    ${arg}
    Another Keyword
```

## Suite name


Tên bộ kiểm tra được tạo từ tên tệp hoặc thư mục theo mặc định. Tên này được tạo ra sao cho phần mở rộng bị bỏ qua, các dấu gạch dưới có thể được thay thế bằng khoảng trắng, và các tên hoàn toàn bằng chữ thường sẽ được viết hoa theo quy tắc tiêu đề. Ví dụ, some_tests.robot trở thành Some Tests và My_test_directory trở thành My test directory.

Tên tệp hoặc thư mục có thể chứa một tiền tố để kiểm soát thứ tự thực thi của các bộ kiểm tra. Tiền tố được tách biệt với tên cơ sở bằng hai dấu gạch dưới, và khi tạo tên bộ kiểm tra thực tế, cả tiền tố và dấu gạch dưới đều bị loại bỏ. Ví dụ, các tệp 01__some_tests.robot và 02__more_tests.robot tạo ra các bộ kiểm tra Some Tests và More Tests, tương ứng, và bộ trước được thực thi trước bộ sau.

Bắt đầu từ Robot Framework 6.1, cũng có thể đặt một tên tùy chỉnh cho một bộ kiểm tra bằng cách sử dụng thiết lập Name trong phần Setting.

```robotframework
*** Settings ***
Name            Custom suite name
```

Tên của bộ kiểm tra cấp cao nhất có thể được ghi đè từ dòng lệnh bằng tùy chọn --name.

## Suite documentation

Tài liệu cho một bộ kiểm tra được thiết lập bằng cách sử dụng tùy chọn Documentation trong phần Settings. Nó có thể được sử dụng cả trong các tệp bộ kiểm tra và trong các tệp khởi tạo bộ kiểm tra. Tài liệu của bộ kiểm tra có các đặc điểm giống hệt nhau về nơi hiển thị và cách thức tạo ra như tài liệu của các trường hợp kiểm tra. Để biết thêm chi tiết về cú pháp, hãy xem phụ lục Documentation formatting.

```robotframework
*** Settings ***
Documentation    An example suite documentation with *some* _formatting_.
...              Long documentation can be split into multiple lines.
```

Tài liệu của bộ kiểm tra cấp cao nhất có thể được ghi đè từ dòng lệnh bằng tùy chọn --doc.

## Free suite metadata

Ngoài tài liệu, các bộ kiểm tra cũng có thể có siêu dữ liệu tự do. Siêu dữ liệu này được định nghĩa dưới dạng cặp tên-giá trị trong phần Cài đặt bằng cách sử dụng cài đặt Metadata. Nó được hiển thị trong các báo cáo và nhật ký tương tự như tài liệu.

Tên của siêu dữ liệu là đối số đầu tiên được cung cấp cho cài đặt Metadata, và các đối số còn lại xác định giá trị của nó. Giá trị được xử lý tương tự như tài liệu, có nghĩa là nó hỗ trợ định dạng HTML và biến, và các giá trị dài hơn có thể được chia thành nhiều hàng.

```robotframework
*** Settings ***
Metadata        Version            2.0
Metadata        Robot Framework    http://robotframework.org
Metadata        Platform           ${PLATFORM}
Metadata        Longer Value
...             Longer metadata values can be split into multiple
...             rows. Also *simple* _formatting_ is supported.
```

Siêu dữ liệu tự do của bộ kiểm tra cấp cao nhất có thể được thiết lập từ dòng lệnh bằng cách sử dụng tùy chọn --metadata.

## Suite setup and teardown


Không chỉ các trường hợp kiểm tra mà cả các bộ kiểm tra cũng có thể có thiết lập (setup) và giải phóng (teardown). Thiết lập của bộ kiểm tra được thực hiện trước khi chạy bất kỳ trường hợp kiểm tra nào trong bộ đó hoặc các bộ kiểm tra con, và giải phóng của bộ kiểm tra được thực hiện sau khi chúng hoàn tất. Tất cả các bộ kiểm tra đều có thể có một thiết lập và một giải phóng; đối với các bộ được tạo từ một thư mục, chúng phải được chỉ định trong một tệp khởi tạo bộ kiểm tra.

Tương tự như với các trường hợp kiểm tra, thiết lập và giải phóng của bộ kiểm tra là các từ khóa có thể nhận các đối số. Chúng được định nghĩa trong phần Cài đặt bằng các cài đặt Thiết lập Bộ (Suite Setup) và Giải phóng Bộ (Suite Teardown), tương ứng. Tên từ khóa và các đối số khả thi được đặt ở các cột sau tên cài đặt.

Nếu một thiết lập bộ kiểm tra thất bại, tất cả các trường hợp kiểm tra trong bộ đó và các bộ kiểm tra con sẽ ngay lập tức được gán trạng thái thất bại và thực tế sẽ không được thực thi. Điều này làm cho thiết lập bộ kiểm tra trở nên lý tưởng để kiểm tra các điều kiện tiên quyết phải được đáp ứng trước khi có thể chạy các trường hợp kiểm tra.

Giải phóng của bộ kiểm tra thường được sử dụng để dọn dẹp sau khi tất cả các trường hợp kiểm tra đã được thực hiện. Nó được thực hiện ngay cả khi thiết lập của cùng một bộ kiểm tra thất bại. Nếu giải phóng bộ kiểm tra thất bại, tất cả các trường hợp kiểm tra trong bộ sẽ được đánh dấu là thất bại, bất kể trạng thái thực thi ban đầu của chúng. Lưu ý rằng tất cả các từ khóa trong giải phóng bộ kiểm tra sẽ được thực hiện ngay cả khi một trong số chúng thất bại.

Tên của từ khóa sẽ được thực hiện như một thiết lập hoặc một giải phóng có thể là một biến. Điều này giúp dễ dàng có các thiết lập hoặc giải phóng khác nhau trong các môi trường khác nhau bằng cách cung cấp tên từ khóa dưới dạng một biến từ dòng lệnh.