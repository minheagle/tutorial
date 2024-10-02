# Using test libraries


Các thư viện kiểm tra chứa những từ khóa cấp thấp nhất, thường được gọi là từ khóa thư viện, thực hiện việc tương tác thực tế với hệ thống cần kiểm tra. Tất cả các trường hợp kiểm tra luôn sử dụng các từ khóa từ một thư viện nào đó, thường thông qua các từ khóa người dùng cấp cao hơn. Phần này giải thích cách sử dụng các thư viện kiểm tra và cách sử dụng các từ khóa mà chúng cung cấp. Việc tạo ra các thư viện kiểm tra được mô tả trong một phần riêng biệt.

## Importing libraries

Các thư viện kiểm tra thường được nhập vào bằng cách sử dụng thiết lập **Library**, nhưng cũng có thể sử dụng từ khóa **Import Library**.

#### Using Library setting

Các thư viện kiểm tra thường được nhập bằng cách sử dụng thiết lập Library trong phần Setting và đặt tên thư viện vào cột tiếp theo. Không giống như hầu hết các dữ liệu khác, tên thư viện phân biệt cả chữ hoa, chữ thường và khoảng cách. Nếu một thư viện nằm trong một package, tên đầy đủ bao gồm cả tên package phải được sử dụng.

Trong các trường hợp thư viện cần các đối số, chúng được liệt kê trong các cột sau tên thư viện. Có thể sử dụng các giá trị mặc định, số lượng đối số biến đổi và các đối số được đặt tên khi nhập thư viện kiểm tra, tương tự như với các đối số của từ khóa. Cả tên thư viện và các đối số đều có thể được đặt bằng cách sử dụng các biến.

```robotframework
*** Settings ***
Library    OperatingSystem
Library    my.package.TestLibrary
Library    MyLibrary    arg1    arg2
Library    ${LIBRARY}
```

Có thể nhập các thư viện kiểm tra vào các tệp suite, tệp tài nguyên (resource files) và tệp khởi tạo suite (suite initialization files). Trong tất cả các trường hợp này, tất cả các từ khóa trong thư viện đã nhập sẽ có sẵn trong tệp đó. Đối với các tệp tài nguyên, những từ khóa này cũng sẽ có sẵn trong các tệp khác sử dụng chúng.

#### Using Import Library keyword

Một cách khác để sử dụng thư viện kiểm tra là sử dụng từ khóa **Import Library** từ thư viện **BuiltIn**. Từ khóa này nhận tên thư viện và các đối số tương tự như trong thiết lập **Library**. Các từ khóa từ thư viện được nhập sẽ có sẵn trong bộ kiểm tra nơi từ khóa **Import Library** được sử dụng. Cách tiếp cận này hữu ích trong các trường hợp mà thư viện không có sẵn khi quá trình thực thi kiểm tra bắt đầu và chỉ một số từ khóa khác mới làm cho thư viện này có sẵn.

```robotframework
*** Test Cases ***
Example
    Do Something
    Import Library    MyLibrary    arg1    arg2
    KW From MyLibrary
```

## Specifying library to import

Các thư viện để nhập có thể được chỉ định bằng cách sử dụng tên thư viện hoặc đường dẫn đến thư viện. Cả hai phương pháp này đều hoạt động giống nhau, bất kể thư viện được nhập bằng cách sử dụng thiết lập **Library** hay từ khóa **Import Library**.

#### Using library name


Cách phổ biến nhất để chỉ định một thư viện kiểm thử để nhập là sử dụng tên của nó, như đã được thực hiện trong tất cả các ví dụ ở phần này. Trong các trường hợp này, Robot Framework sẽ cố gắng tìm lớp hoặc mô-đun triển khai thư viện từ đường dẫn tìm kiếm mô-đun. Các thư viện đã được cài đặt thường sẽ có trong đường dẫn tìm kiếm mô-đun một cách tự động, nhưng với các thư viện khác, đường dẫn tìm kiếm có thể cần được cấu hình riêng.

Lợi ích lớn nhất của phương pháp này là khi đường dẫn tìm kiếm mô-đun đã được cấu hình, thường bằng cách sử dụng một tập lệnh khởi động tùy chỉnh, người dùng bình thường không cần phải lo lắng về nơi các thư viện thực sự được cài đặt. Điểm hạn chế là việc đưa các thư viện của riêng bạn, dù có thể rất đơn giản, vào đường dẫn tìm kiếm có thể yêu cầu một số cấu hình bổ sung.

#### Using physical path to library

Một cơ chế khác để chỉ định thư viện cần nhập là sử dụng đường dẫn đến nó trong hệ thống tệp. Đường dẫn này được coi là tương đối so với thư mục nơi tệp dữ liệu kiểm thử hiện tại nằm, tương tự như cách xử lý các đường dẫn đến tệp tài nguyên và biến. Lợi ích chính của cách tiếp cận này là không cần cấu hình đường dẫn tìm kiếm mô-đun.

Nếu thư viện là một tệp, đường dẫn đến nó phải chứa phần mở rộng, tức là .py. Nếu thư viện được triển khai dưới dạng một thư mục, đường dẫn đến nó phải có dấu gạch chéo hướng về phía trước (/) nếu đường dẫn là tương đối. Với đường dẫn tuyệt đối, dấu gạch chéo ở cuối là tùy chọn. Các ví dụ sau đây minh họa các cách sử dụng khác nhau này.

```robotframework
*** Settings ***
Library    PythonLibrary.py
Library    relative/path/PythonDirLib/    possible    arguments
Library    ${RESOURCES}/Example.class
```

Một hạn chế của cách tiếp cận này là các thư viện được triển khai dưới dạng các lớp Python phải nằm trong một mô-đun có cùng tên với lớp đó.

## Setting custom name to library

Tên thư viện được hiển thị trong nhật ký kiểm thử trước tên từ khóa, và nếu có nhiều từ khóa có cùng tên, chúng phải được sử dụng sao cho tên từ khóa được thêm tiền tố với tên thư viện. Tên thư viện thường lấy từ tên mô-đun hoặc tên lớp triển khai nó, nhưng có một số trường hợp việc thay đổi tên là cần thiết:

* Cần phải nhập cùng một thư viện nhiều lần với các đối số khác nhau. Điều này không thể thực hiện được theo cách thông thường.

* Tên thư viện quá dài hoặc không tiện lợi.

* Bạn muốn sử dụng các biến để nhập các thư viện khác nhau trong các môi trường khác nhau, nhưng muốn tham chiếu đến chúng bằng cùng một tên.

* Tên thư viện gây hiểu lầm hoặc không phù hợp. Trong trường hợp này, thay đổi tên thật của thư viện là giải pháp tốt hơn.

Cú pháp cơ bản để chỉ định tên mới là thêm văn bản "AS" (phân biệt chữ hoa chữ thường) sau tên thư viện và tiếp theo là tên mới. Tên đã chỉ định này sẽ hiển thị trong nhật ký và phải được sử dụng trong dữ liệu kiểm thử khi sử dụng tên đầy đủ của từ khóa (LibraryName.Keyword Name).

```robotframework
*** Settings ***
Library    packagename.TestLib    AS    TestLib
Library    ${LIBRARY}    AS    MyName
```

Các đối số có thể cho thư viện được đặt giữa tên thư viện gốc và ký hiệu AS. Ví dụ dưới đây minh họa cách cùng một thư viện có thể được nhập nhiều lần với các đối số khác nhau:

```robotframework
*** Settings ***
Library    SomeLibrary    localhost        1234    AS    LocalLib
Library    SomeLibrary    server.domain    8080    AS    RemoteLib

*** Test Cases ***
Example
    LocalLib.Some Keyword     some arg       second arg
    RemoteLib.Some Keyword    another arg    whatever
    LocalLib.Another Keyword
```

Việc đặt tên tùy chỉnh cho một thư viện kiểm thử hoạt động cả khi nhập một thư viện trong phần Cài đặt và khi sử dụng từ khóa **Import Library**.

!!! Note 
    Trước phiên bản Robot Framework 6.0, dấu hiệu được sử dụng khi đặt tên tùy chỉnh cho một thư viện là WITH NAME thay vì AS. Cú pháp cũ vẫn hoạt động, nhưng được coi là đã lỗi thời và sẽ bị loại bỏ trong tương lai.

## Standard libraries

Một số thư viện kiểm thử được phân phối cùng với Robot Framework và những thư viện này được gọi là thư viện chuẩn. Thư viện BuiltIn là đặc biệt, vì nó được sử dụng tự động và do đó các từ khóa của nó luôn có sẵn. Các thư viện chuẩn khác cần được nhập vào theo cách tương tự như bất kỳ thư viện nào khác, nhưng không cần phải cài đặt chúng.

#### Normal standard libraries


Các thư viện chuẩn thông thường có sẵn được liệt kê dưới đây kèm theo liên kết đến tài liệu của chúng:

* BuiltIn

* Collections

* DateTime

* Dialogs

* OperatingSystem

* Process

* Screenshot

* String

* Telnet

* XML

#### Remote library

Ngoài các thư viện chuẩn thông thường được liệt kê ở trên, còn có Remote library, hoàn toàn khác biệt so với các thư viện chuẩn khác. Thư viện này không có bất kỳ từ khóa nào riêng, nhưng hoạt động như một proxy giữa Robot Framework và các triển khai thư viện kiểm tra thực tế. Những thư viện này có thể chạy trên các máy khác với khung chính và thậm chí có thể được triển khai bằng các ngôn ngữ không được Robot Framework hỗ trợ một cách tự nhiên.

Xem phần giao diện thư viện từ xa để biết thêm thông tin về khái niệm này.

## External libraries

Bất kỳ thư viện kiểm tra nào không thuộc về các thư viện chuẩn đều được định nghĩa là thư viện bên ngoài. Cộng đồng mã nguồn mở Robot Framework đã triển khai một số thư viện tổng quát, chẳng hạn như SeleniumLibrary và SwingLibrary, những thư viện này không được đóng gói cùng với khung chính. Một danh sách các thư viện có sẵn công khai có thể được tìm thấy tại robotframework.org.

Các thư viện tổng quát và tùy chỉnh cũng có thể được các nhóm sử dụng Robot Framework triển khai. Xem phần Tạo thư viện kiểm tra để biết thêm thông tin về chủ đề này.

Các thư viện bên ngoài khác nhau có thể có cơ chế cài đặt và sử dụng hoàn toàn khác nhau. Đôi khi, chúng cũng có thể yêu cầu một số phụ thuộc khác phải được cài đặt riêng. Tất cả các thư viện nên có tài liệu cài đặt và sử dụng rõ ràng, và tốt nhất là nên tự động hóa quá trình cài đặt.