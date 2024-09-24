# Test data syntax

## Files and directories

Cấu trúc phân cấp để sắp xếp các trường hợp kiểm thử được xây dựng như sau:

* Các trường hợp kiểm thử được tạo trong các tệp suite.

* Một tệp trường hợp kiểm thử tự động tạo ra một bộ kiểm thử chứa các trường hợp kiểm thử trong tệp đó.

* Một thư mục chứa các tệp trường hợp kiểm thử hình thành một bộ kiểm thử cấp cao hơn. Thư mục bộ kiểm thử này có các bộ kiểm thử được tạo từ các tệp trường hợp kiểm thử là các bộ kiểm thử con của nó.

* Một thư mục bộ kiểm thử cũng có thể chứa các thư mục bộ kiểm thử khác, và cấu trúc phân cấp này có thể được lồng sâu tùy ý.

* Thư mục bộ kiểm thử có thể có một tệp khởi tạo đặc biệt cấu hình bộ kiểm thử được tạo ra.

Ngoài ra, còn có:

* Các thư viện kiểm thử chứa các từ khóa cấp thấp nhất.

* Các tệp tài nguyên với các biến và từ khóa người dùng cấp cao hơn.

* Các tệp biến cung cấp cách linh hoạt hơn để tạo biến so với các tệp tài nguyên.

Các tệp trường hợp kiểm thử, tệp khởi tạo bộ kiểm thử và tệp tài nguyên đều được tạo bằng cú pháp dữ liệu kiểm thử của Robot Framework. Các thư viện kiểm thử và tệp biến được tạo bằng các ngôn ngữ lập trình "thực", thường là Python.

## Test data sections

Dữ liệu của Robot Framework được định nghĩa trong các phần khác nhau, thường được gọi là bảng, như sau:

| **Section**     | **Sử dụng cho**                                                                                      |
|------------------|-----------------------------------------------------------------------------------------------------|
| **Settings**     | 1) Nhập các thư viện kiểm thử, tệp tài nguyên và tệp biến. <br> 2) Định nghĩa siêu dữ liệu cho bộ kiểm thử và trường hợp kiểm thử. |
| **Variables**    | Định nghĩa các biến có thể được sử dụng ở những nơi khác trong dữ liệu kiểm thử.                |
| **Test Cases**   | Tạo các trường hợp kiểm thử từ các từ khóa có sẵn.                                                 |
| **Tasks**        | Tạo các tác vụ bằng cách sử dụng các từ khóa có sẵn. Một tệp đơn chỉ có thể chứa hoặc là các kiểm thử hoặc là các tác vụ. |
| **Keywords**     | Tạo các từ khóa người dùng từ các từ khóa cấp thấp hơn.                                          |
| **Comments**     | Các chú thích hoặc dữ liệu bổ sung. Bị Robot Framework bỏ qua.                                   |

Các phần khác nhau được nhận diện bởi hàng tiêu đề của chúng. Định dạng tiêu đề được khuyến nghị là <code>*** Settings ***</code>, nhưng tiêu đề là không phân biệt chữ hoa chữ thường, khoảng trắng bao quanh là tùy chọn, và số lượng ký tự asterisk có thể thay đổi miễn là có ít nhất một ký tự asterisk ở đầu. Ví dụ, <code>*settings</code> cũng sẽ được công nhận là tiêu đề phần.

Robot Framework cũng hỗ trợ các tiêu đề số ít như <code>*** Setting ***</code>, nhưng hỗ trợ đó đã bị ngưng hỗ trợ trong Robot Framework 6.0. Có một cảnh báo ngừng hỗ trợ rõ ràng bắt đầu từ Robot Framework 7.0 và các tiêu đề số ít sẽ cuối cùng không được hỗ trợ nữa.

Hàng tiêu đề có thể chứa dữ liệu khác ngoài tiêu đề phần thực tế. Dữ liệu bổ sung phải được phân tách khỏi tiêu đề phần bằng cách sử dụng ký tự phân tách phụ thuộc vào định dạng dữ liệu, thường là hai hoặc nhiều khoảng trắng. Các tiêu đề bổ sung này sẽ bị bỏ qua trong thời gian phân tích cú pháp, nhưng chúng có thể được sử dụng cho mục đích tài liệu. Điều này đặc biệt hữu ích khi tạo các trường hợp kiểm thử bằng cách sử dụng kiểu dữ liệu điều khiển.

Các dữ liệu có thể có trước phần đầu tiên sẽ bị bỏ qua.

## Supported file formats

Cách tiếp cận phổ biến nhất để tạo dữ liệu Robot Framework là sử dụng định dạng phân tách bằng khoảng trắng, trong đó các phần của dữ liệu, chẳng hạn như từ khóa và các tham số của chúng, được tách nhau bằng hai hoặc nhiều khoảng trắng. Một lựa chọn thay thế là sử dụng định dạng phân tách bằng ký tự ống (pipe), trong đó ký tự phân tách là ký tự ống được bao quanh bởi khoảng trắng (|).

Các tệp suite thường sử dụng phần mở rộng <code>.robot</code>, nhưng các tệp nào được phân tích cú pháp có thể được cấu hình. Các tệp tài nguyên cũng có thể sử dụng phần mở rộng <code>.robot</code>, nhưng khuyến nghị sử dụng phần mở rộng riêng biệt <code>.resource</code> và điều này có thể được yêu cầu trong tương lai. Các tệp chứa ký tự không phải ASCII phải được lưu bằng mã hóa UTF-8.

Robot Framework cũng hỗ trợ các tệp reStructuredText để dữ liệu Robot Framework bình thường được nhúng vào trong các khối mã. Chỉ các tệp có phần mở rộng <code>.robot.rst</code> được phân tích cú pháp theo mặc định. Nếu bạn muốn sử dụng chỉ phần mở rộng <code>.rst</code> hoặc <code>.rest</code>, điều đó cần được cấu hình riêng.

Dữ liệu Robot Framework cũng có thể được tạo ở định dạng JSON, điều này nhắm đến nhiều hơn cho các nhà phát triển công cụ hơn là cho người dùng bình thường của Robot Framework. Chỉ các tệp JSON với phần mở rộng tùy chỉnh <code>.rbt</code> được phân tích cú pháp theo mặc định.

Các phiên bản Robot Framework trước đây cũng hỗ trợ dữ liệu ở định dạng HTML và TSV. Định dạng TSV vẫn hoạt động nếu dữ liệu tương thích với định dạng phân tách bằng khoảng trắng, nhưng hỗ trợ cho định dạng HTML đã bị loại bỏ hoàn toàn. Nếu bạn gặp phải các tệp dữ liệu như vậy, bạn cần chuyển đổi chúng sang định dạng văn bản thuần túy để có thể sử dụng chúng với Robot Framework 3.2 hoặc mới hơn. Cách dễ nhất để làm điều đó là sử dụng công cụ Tidy, nhưng bạn phải sử dụng phiên bản đi kèm với Robot Framework 3.1 vì các phiên bản mới hơn hoàn toàn không hiểu định dạng HTML.

#### Space separated format

Khi Robot Framework phân tích dữ liệu, nó trước tiên chia dữ liệu thành các dòng và sau đó chia các dòng thành các mã thông báo, chẳng hạn như từ khóa và tham số. Khi sử dụng định dạng phân tách bằng khoảng trắng, ký tự phân tách giữa các mã thông báo là hai hoặc nhiều khoảng trắng hoặc, thay vào đó, là một hoặc nhiều ký tự tab. Ngoài khoảng trắng ASCII thông thường, bất kỳ ký tự Unicode nào được coi là khoảng trắng (ví dụ: khoảng trắng không ngắt) đều hoạt động như một ký tự phân tách. Số lượng khoảng trắng được sử dụng làm ký tự phân tách có thể thay đổi, miễn là có ít nhất hai, điều này cho phép sắp xếp dữ liệu một cách gọn gàng trong phần cài đặt và những nơi khác khi làm cho dữ liệu dễ hiểu hơn.

```robotframework
*** Settings ***
Documentation     Example using the space separated format.
Library           OperatingSystem

*** Variables ***
${MESSAGE}        Hello, world!

*** Test Cases ***
My Test
    [Documentation]    Example test.
    Log    ${MESSAGE}
    My Keyword    ${CURDIR}

Another Test
    Should Be Equal    ${MESSAGE}    Hello, world!

*** Keywords ***
My Keyword
    [Arguments]    ${path}
    Directory Should Exist    ${path}
```

Bởi vì các ký tự tab và các khoảng trắng liên tiếp được coi là ký tự phân tách, chúng phải được thoát nếu cần thiết trong các tham số của từ khóa hoặc ở những nơi khác trong dữ liệu thực tế. Có thể sử dụng cú pháp thoát đặc biệt như <code>\t</code> cho tab và <code>\xA0</code> cho khoảng trắng không ngắt cũng như các biến tích hợp <code>${SPACE}</code> và <code>${EMPTY}</code>. Xem phần Thoát ký tự để biết thêm chi tiết.

> Mẹo
> 
> Mặc dù việc sử dụng hai khoảng trắng làm ký tự phân tách là đủ, nhưng nên sử dụng bốn khoảng trắng để làm cho ký tự phân tách dễ nhận diện hơn.


> Lưu ý
>
> Trước phiên bản Robot Framework 3.2, các khoảng trắng không phải ASCII được sử dụng trong dữ liệu đã được chuyển đổi thành khoảng trắng ASCII trong quá trình phân tích. Ngày nay, tất cả dữ liệu đều được bảo tồn nguyên trạng.

#### Pipe separated format

Vấn đề lớn nhất của định dạng phân tách bằng khoảng trắng là việc phân tách trực quan giữa các từ khóa và tham số có thể khó khăn. Đây là một vấn đề đặc biệt nếu các từ khóa nhận nhiều tham số và/hoặc các tham số chứa khoảng trắng. Trong những trường hợp như vậy, biến thể phân tách bằng dấu ống có thể hoạt động tốt hơn vì nó làm cho ký tự phân tách dễ thấy hơn.

Một tệp có thể chứa cả dòng phân tách bằng khoảng trắng và dòng phân tách bằng dấu ống. Các dòng phân tách bằng dấu ống được nhận diện bởi ký tự dấu ống bắt buộc ở đầu dòng, nhưng dấu ống ở cuối dòng là tùy chọn. Luôn phải có ít nhất một khoảng trắng hoặc tab ở cả hai bên của dấu ống, ngoại trừ ở đầu và cuối dòng. Không cần thiết phải căn chỉnh các dấu ống, nhưng việc đó thường làm cho dữ liệu dễ đọc hơn.

```robotframework
| *** Settings ***   |
| Documentation      | Example using the pipe separated format.
| Library            | OperatingSystem

| *** Variables ***  |
| ${MESSAGE}         | Hello, world!

| *** Test Cases *** |                 |               |
| My Test            | [Documentation] | Example test. |
|                    | Log             | ${MESSAGE}    |
|                    | My Keyword      | ${CURDIR}     |
| Another Test       | Should Be Equal | ${MESSAGE}    | Hello, world!

| *** Keywords ***   |                        |         |
| My Keyword         | [Arguments]            | ${path} |
|                    | Directory Should Exist | ${path} |
```

Khi sử dụng định dạng phân tách bằng dấu ống, các khoảng trắng hoặc tab liên tiếp bên trong các tham số không cần phải được thoát. Tương tự, các cột trống không cần phải được thoát, ngoại trừ khi chúng nằm ở cuối. Tuy nhiên, các dấu ống có thể xuất hiện bên trong dữ liệu thử nghiệm thực tế cần phải được thoát bằng một dấu gạch chéo ngược:

```robotframework
| *** Test Cases *** |                 |                 |                      |
| Escaping Pipe      | ${file count} = | Execute Command | ls -1 *.txt \| wc -l |
|                    | Should Be Equal | ${file count}   | 42                   |
```

> Lưu ý
>
> Việc bảo tồn các khoảng trắng và tab liên tiếp trong các tham số là điều mới trong Robot Framework 3.2. Trước đó, các khoảng trắng không phải ASCII được sử dụng trong dữ liệu cũng đã được chuyển đổi thành khoảng trắng ASCII.

#### reStructuredText format

reStructuredText (reST) là một cú pháp đánh dấu văn bản thuần túy dễ đọc, thường được sử dụng để tài liệu hóa các dự án Python, bao gồm cả Python và Hướng dẫn Người dùng này. Các tài liệu reST thường được biên dịch thành HTML, nhưng cũng hỗ trợ các định dạng đầu ra khác. Việc sử dụng reST với Robot Framework cho phép bạn kết hợp các tài liệu định dạng phong phú và dữ liệu thử nghiệm trong một định dạng văn bản ngắn gọn, dễ làm việc với bằng các trình soạn thảo văn bản đơn giản, công cụ so sánh và hệ thống kiểm soát phiên bản.

Lưu ý

Việc sử dụng tệp reStructuredText với Robot Framework yêu cầu cài đặt mô-đun Python docutils.

Khi sử dụng Robot Framework với các tệp reStructuredText, dữ liệu Robot Framework bình thường được nhúng vào các khối mã gọi là code blocks. Trong reST tiêu chuẩn, các khối mã được đánh dấu bằng chỉ thị code, nhưng Robot Framework cũng hỗ trợ các chỉ thị code-block hoặc sourcecode được sử dụng bởi công cụ Sphinx.

```robotframework
reStructuredText example
------------------------

This text is outside code blocks and thus ignored.

.. code:: robotframework

   *** Settings ***
   Documentation    Example using the reStructuredText format.
   Library          OperatingSystem

   *** Variables ***
   ${MESSAGE}       Hello, world!

   *** Test Cases ***
   My Test
       [Documentation]    Example test.
       Log    ${MESSAGE}
       My Keyword    ${CURDIR}

   Another Test
       Should Be Equal    ${MESSAGE}    Hello, world!

Also this text is outside code blocks and ignored. Code blocks not
containing Robot Framework data are ignored as well.

.. code:: robotframework

   # Both space and pipe separated formats are supported.

   | *** Keywords ***  |                        |         |
   | My Keyword        | [Arguments]            | ${path} |
   |                   | Directory Should Exist | ${path} |

.. code:: python

   # This code block is ignored.
   def example():
       print('Hello, world!')
```

Robot Framework hỗ trợ các tệp reStructuredText với các phần mở rộng <code>.robot.rst</code>, <code>.rst</code> và <code>.rest</code>. Để tránh phân tích các tệp reStructuredText không liên quan, chỉ các tệp có phần mở rộng <code>.robot.rst</code> được phân tích theo mặc định khi thực thi một thư mục. Việc phân tích các tệp với các phần mở rộng khác có thể được kích hoạt bằng cách sử dụng tùy chọn <code>--parseinclude</code> hoặc <code>--extension</code>.

Khi Robot Framework phân tích các tệp reStructuredText, các lỗi dưới cấp <code>SEVERE</code> sẽ bị bỏ qua để tránh tiếng ồn về các chỉ thị không tiêu chuẩn và các cú pháp tương tự khác. Điều này có thể che giấu cả những lỗi thực tế, nhưng chúng có thể được nhìn thấy khi xử lý các tệp bằng công cụ reStructuredText bình thường.

> Lưu ý
> 
> Việc tự động phân tích các tệp .robot.rst là điều mới trong Robot Framework 6.1.

#### JSON format

Robot Framework cũng hỗ trợ dữ liệu ở định dạng JSON. Định dạng này được thiết kế chủ yếu cho các nhà phát triển công cụ hơn là cho người dùng Robot Framework thông thường và không được thiết kế để chỉnh sửa thủ công. Các trường hợp sử dụng quan trọng nhất của nó là:

* Chuyển dữ liệu giữa các quy trình và máy móc. Một bộ thử nghiệm có thể được chuyển đổi sang định dạng JSON trên một máy và được tái tạo ở nơi khác.
* Lưu một bộ thử nghiệm, có thể là một bộ lồng nhau, được xây dựng từ dữ liệu Robot Framework thông thường vào một tệp JSON duy nhất để phân tích nhanh hơn.
* Định dạng dữ liệu thay thế cho các công cụ bên ngoài tạo ra các bài kiểm tra hoặc nhiệm vụ.

> Lưu ý
>
> Hỗ trợ dữ liệu JSON là tính năng mới trong Robot Framework 6.1 và có thể được cải thiện trong các phiên bản Robot Framework trong tương lai. Nếu bạn có ý tưởng cải tiến hoặc tin rằng bạn đã gặp lỗi, vui lòng gửi một vấn đề hoặc bắt đầu một thảo luận trên kênh #devel trên Slack của chúng tôi.

Chuyển đổi bộ thử nghiệm sang JSON

Cấu trúc bộ thử nghiệm có thể được tuần tự hóa thành JSON bằng cách sử dụng phương thức TestSuite.to_json. Khi sử dụng mà không có tham số, nó trả về dữ liệu JSON dưới dạng chuỗi, nhưng nó cũng chấp nhận một đường dẫn hoặc một tệp đang mở để ghi dữ liệu JSON cùng với các tùy chọn cấu hình liên quan đến định dạng JSON:

```robotframework
from robot.running import TestSuite


# Create suite based on data on the file system.
suite = TestSuite.from_file_system('/path/to/data')

# Get JSON data as a string.
data = suite.to_json()

# Save JSON data to a file with custom indentation.
suite.to_json('data.rbt', indent=2)
```

Nếu bạn muốn làm việc với dữ liệu Python và sau đó chuyển đổi nó sang định dạng JSON hoặc định dạng khác, bạn có thể sử dụng TestSuite.to_dict thay thế.

###### Creating suite from JSON

Một bộ thử nghiệm có thể được xây dựng từ dữ liệu JSON bằng cách sử dụng phương thức TestSuite.from_json. Nó hoạt động với cả chuỗi JSON và đường dẫn đến các tệp JSON:

```python
from robot.running import TestSuite

# Tạo bộ từ dữ liệu JSON trong một tệp.
suite = TestSuite.from_json('data.rbt')

# Tạo bộ từ một chuỗi JSON.
suite = TestSuite.from_json('{"name": "Suite", "tests": [{"name": "Test"}]}')

# Thực hiện bộ thử nghiệm. Lưu ý rằng nhật ký và báo cáo cần được tạo riêng.
suite.run(output='example.xml')
```

Nếu bạn có dữ liệu dưới dạng từ điển Python, bạn có thể sử dụng TestSuite.from_dict thay thế. Bất kể bộ thử nghiệm được tái tạo như thế nào, nó chỉ tồn tại trong bộ nhớ và các tệp dữ liệu gốc trên hệ thống tệp sẽ không được tái tạo.

Như ví dụ trên đã minh họa, bộ thử nghiệm được tạo ra có thể được thực hiện bằng phương thức TestSuite.run. Tuy nhiên, có thể dễ dàng hơn khi thực hiện một tệp JSON trực tiếp như được giải thích trong phần sau.

###### Executing JSON files

Khi thực hiện các bài kiểm tra hoặc nhiệm vụ bằng cách sử dụng lệnh robot, các tệp JSON với phần mở rộng tùy chỉnh .rbt sẽ được phân tích tự động. Điều này bao gồm việc chạy các tệp JSON riêng lẻ như robot tests.rbt và chạy các thư mục chứa các tệp .rbt. Nếu bạn muốn sử dụng phần mở rộng tiêu chuẩn .json, bạn cần cấu hình các tệp nào sẽ được phân tích.

###### Adjusting suite source

Nguồn bộ trong dữ liệu nhận được từ TestSuite.to_json và TestSuite.to_dict ở định dạng tuyệt đối. Nếu bộ thử nghiệm được tái tạo sau đó trên một máy khác, nguồn có thể không khớp với cấu trúc thư mục trên máy đó. Để tránh điều đó, có thể sử dụng phương thức TestSuite.adjust_source để làm cho nguồn bộ trở nên tương đối trước khi lấy dữ liệu và thêm một thư mục gốc chính xác sau khi bộ thử nghiệm được tái tạo:

```python
from robot.running import TestSuite

# Tạo một bộ, điều chỉnh nguồn và chuyển đổi sang JSON.
suite = TestSuite.from_file_system('/path/to/data')
suite.adjust_source(relative_to='/path/to')
suite.to_json('data.rbt')

# Tái tạo bộ ở nơi khác và điều chỉnh nguồn cho phù hợp.
suite = TestSuite.from_json('data.rbt')
suite.adjust_source(root='/new/path/to')
```

###### JSON structure

Các nhập khẩu, biến và từ khóa được tạo trong các tệp bộ thử nghiệm được bao gồm trong JSON được tạo ra cùng với các bài kiểm tra và nhiệm vụ. Cấu trúc JSON chính xác được tài liệu hóa trong tệp running.json schema.

## Rules for parsing the data

#### Ignored data

Khi Robot Framework phân tích các tệp dữ liệu thử nghiệm, nó sẽ bỏ qua:

* Tất cả dữ liệu trước phần dữ liệu thử nghiệm đầu tiên.

* Dữ liệu trong phần Nhận xét.

* Tất cả các hàng trống.

* Tất cả các ô trống ở cuối hàng khi sử dụng định dạng phân cách bằng ống.

* Tất cả các dấu gạch chéo đơn (<code>\\</code>) khi không được sử dụng để thoát.

* Tất cả các ký tự theo sau ký tự hash (<code>#</code>), khi nó là ký tự đầu tiên của một ô. Điều này có nghĩa là các dấu hash có thể được sử dụng để nhập nhận xét trong dữ liệu thử nghiệm.

Khi Robot Framework bỏ qua một số dữ liệu, dữ liệu này sẽ không có trong bất kỳ báo cáo nào được tạo ra, và hơn nữa, hầu hết các công cụ được sử dụng với Robot Framework cũng bỏ qua chúng. Để thêm thông tin có thể nhìn thấy trong các đầu ra của Robot Framework, hãy đặt nó vào tài liệu hoặc các siêu dữ liệu khác của các trường hợp thử nghiệm hoặc bộ thử nghiệm, hoặc ghi lại nó bằng các từ khóa BuiltIn như Log hoặc Comment.

## Escaping

Ký tự thoát trong dữ liệu thử nghiệm Robot Framework là dấu gạch chéo ngược (<code>\\</code>) và thêm vào đó, các biến tích hợp như <code>${EMPTY}</code> và <code>${SPACE}</code> thường có thể được sử dụng để thoát. Các cơ chế thoát khác nhau sẽ được thảo luận trong các phần dưới đây.

#### Escaping special characters

Ký tự gạch chéo ngược có thể được sử dụng để thoát các ký tự đặc biệt để giá trị của chúng được sử dụng một cách nguyên bản.

| Ký tự | Ý nghĩa | Ví dụ |
|-------|---------|-------|
| `$`   | Dấu đô la, không bao giờ bắt đầu một biến vô hướng. | `${notvar}` |
| `@`   | Dấu at, không bao giờ bắt đầu một biến danh sách. | `@{notvar}` |
| `&`   | Dấu và, không bao giờ bắt đầu một biến từ điển. | `&{notvar}` |
| `%`   | Dấu phần trăm, không bao giờ bắt đầu một biến môi trường. | `%{notvar}` |
| `#`   | Dấu thăng, không bao giờ bắt đầu một chú thích. | `# not comment` |
| `=`   | Dấu bằng, không bao giờ là một phần của cú pháp đối số có tên. | `not=named` |
| `|`   | Ký tự ống, không phải là một bộ phân cách trong định dạng tách ống. | `ls -1 *.txt | wc -l` |
| `\\`  | Ký tự gạch chéo ngược, không bao giờ thoát bất kỳ điều gì. | `c:\\temp`, `\\${var}` |

#### Forming escape sequences

Ký tự backslash cũng cho phép tạo ra các chuỗi thoát đặc biệt được nhận diện như những ký tự mà nếu không có nó thì sẽ khó hoặc không thể tạo ra trong dữ liệu kiểm tra.

| Dãy ký tự    | Ý nghĩa                               | Ví dụ                           |
|--------------|---------------------------------------|---------------------------------|
| `\n`         | Ký tự xuống dòng.                     | `first line\n2nd line`         |
| `\r`         | Ký tự trở về đầu dòng.                | `text\rmore text`              |
| `\t`         | Ký tự tab.                            | `text\tmore text`              |
| `\xhh`       | Ký tự có giá trị hex hh.              | `null byte: \x00, ä: \xE4`     |
| `\uhhhh`     | Ký tự có giá trị hex hhhh.            | `snowman: \u2603`              |
| `\Uhhhhhhhh` | Ký tự có giá trị hex hhhhhhhh.        | `love hotel: \U0001f3e9`       |

> **Lưu ý**
>
> Tất cả các chuỗi được tạo trong dữ liệu kiểm tra, bao gồm các ký tự như \x02, đều là Unicode và phải được chuyển đổi thành chuỗi byte một cách rõ ràng nếu cần thiết. Việc này có thể được thực hiện, chẳng hạn, bằng cách sử dụng các từ khóa Convert To Bytes hoặc Encode String To Bytes trong các thư viện BuiltIn và String, hoặc bằng cách sử dụng value.encode('UTF-8') trong mã Python.

> **Lưu ý**
>
> Nếu các giá trị số hex không hợp lệ được sử dụng với các ký tự thoát \x, \u hoặc \U, kết quả cuối cùng sẽ là giá trị gốc mà không có ký tự backslash. Ví dụ, \xAX (không phải hex) và \U00110000 (giá trị quá lớn) sẽ cho ra kết quả lần lượt là xAX và U00110000. Hành vi này có thể thay đổi trong tương lai.

> **Lưu ý**
>
> Biến tích hợp ${\n} có thể được sử dụng nếu cần thiết kế kết thúc dòng phụ thuộc vào hệ điều hành (\r\n trên Windows và \n ở nơi khác).

#### Handling empty values

Khi sử dụng định dạng cách nhau bởi khoảng trắng, số lượng khoảng trắng được sử dụng làm dấu phân cách có thể thay đổi và do đó, các giá trị trống không thể được nhận diện trừ khi chúng được thoát. Các ô trống có thể được thoát bằng ký tự backslash hoặc biến tích hợp ${EMPTY}. Biến sau thường được khuyến nghị hơn vì dễ hiểu hơn.

```robotframework
*** Test Cases ***
Using backslash
    Do Something    first arg    \
    Do Something    \            second arg

Using ${EMPTY}
    Do Something    first arg    ${EMPTY}
    Do Something    ${EMPTY}     second arg
```

Khi sử dụng định dạng cách nhau bằng dấu pipe, các giá trị trống chỉ cần được thoát khi chúng nằm ở cuối hàng:

```robotframework
| *** Test Cases *** |              |           |            |
| Using backslash    | Do Something | first arg | \          |
|                    | Do Something |           | second arg |
|                    |              |           |            |
| Using ${EMPTY}     | Do Something | first arg | ${EMPTY}   |
|                    | Do Something |           | second arg |
```

#### Handling spaces

Khoảng trắng, đặc biệt là khoảng trắng liên tiếp, khi là một phần của đối số cho các từ khóa hoặc cần thiết cho các mục đích khác, sẽ gây ra một số vấn đề vì hai lý do sau:

* Hai hoặc nhiều khoảng trắng liên tiếp được coi là dấu phân cách khi sử dụng định dạng phân cách bằng khoảng trắng.

* Khoảng trắng ở đầu và cuối sẽ bị bỏ qua khi sử dụng định dạng phân cách bằng ống.

Trong những trường hợp này, khoảng trắng cần được thoát. Tương tự như khi thoát các giá trị trống, bạn có thể thực hiện điều đó bằng cách sử dụng ký tự backslash hoặc bằng cách sử dụng biến tích hợp ${SPACE}.

| Escaping with backslash         | Escaping with ${SPACE}          | Notes                               |
|----------------------------------|----------------------------------|-------------------------------------|
| \ leading space                  | ${SPACE}leading space            |                                     |
| trailing space \                 | trailing space${SPACE}           | Backslash must be after the space.  |
| \ \                              | ${SPACE}                        | Backslash needed on both sides.     |
| consecutive \ \ spaces           | consecutive${SPACE * 3}spaces    | Using extended variable syntax.      |

Như các ví dụ ở trên đã chỉ ra, việc sử dụng biến ${SPACE} thường làm cho dữ liệu kiểm tra dễ hiểu hơn. Nó đặc biệt hữu ích khi kết hợp với cú pháp biến mở rộng khi cần nhiều hơn một khoảng trắng.

#### Dividing data to several rows

Nếu có nhiều dữ liệu hơn những gì có thể vừa vặn trong một hàng, có thể chia nhỏ dữ liệu và bắt đầu các hàng tiếp theo bằng dấu ba chấm (...). Dấu ba chấm có thể được thụt vào để phù hợp với mức thụt đầu dòng của hàng bắt đầu và phải luôn được theo sau bởi dấu phân cách dữ liệu kiểm tra thông thường.

Trong hầu hết các trường hợp, các dòng bị chia nhỏ có ý nghĩa giống hệt như các dòng không bị chia. Các trường hợp ngoại lệ đối với quy tắc này là tài liệu của bộ, kiểm tra và từ khóa cũng như siêu dữ liệu của bộ. Đối với chúng, các giá trị bị chia sẽ được tự động nối với nhau bằng ký tự xuống dòng để dễ dàng tạo ra các giá trị nhiều dòng.

Cú pháp ... cũng cho phép chia nhỏ các biến trong phần Biến. Khi các biến vô hướng dài (ví dụ: ${STRING}) được chia thành nhiều hàng, giá trị cuối cùng được tạo ra bằng cách nối các hàng lại với nhau. Dấu phân cách mặc định là một khoảng trắng, nhưng điều đó có thể được thay đổi bằng cách bắt đầu giá trị với SEPARATOR=<sep>.

Việc chia nhỏ các dòng được minh họa trong hai ví dụ sau đây chứa cùng một dữ liệu mà không chia và có chia.

```robotframework
*** Settings ***
Documentation      Here we have documentation for this suite.\nDocumentation is often quite long.\n\nIt can also contain multiple paragraphs.
Default Tags       default tag 1    default tag 2    default tag 3    default tag 4    default tag 5

*** Variables ***
${STRING}          This is a long string. It has multiple sentences. It does not have newlines.
${MULTILINE}       This is a long multiline string.\nThis is the second line.\nThis is the third and the last line.
@{LIST}            this     list     is    quite    long     and    items in it can also be long
&{DICT}            first=This value is pretty long.    second=This value is even longer. It has two sentences.

*** Test Cases ***
Example
    [Tags]    you    probably    do    not    have    this    many    tags    in    real    life
    Do X    first argument    second argument    third argument    fourth argument    fifth argument    sixth argument
    ${var} =    Get X    first argument passed to this keyword is pretty long    second argument passed to this keyword is long too
```

```robotframework
*** Settings ***
Documentation      Here we have documentation for this suite.
...                Documentation is often quite long.
...
...                It can also contain multiple paragraphs.
Default Tags       default tag 1    default tag 2    default tag 3
...                default tag 4    default tag 5

*** Variables ***
${STRING}          This is a long string.
...                It has multiple sentences.
...                It does not have newlines.
${MULTILINE}       SEPARATOR=\n
...                This is a long multiline string.
...                This is the second line.
...                This is the third and the last line.
@{LIST}            this     list     is      quite    long     and
...                items in it can also be long
&{DICT}            first=This value is pretty long.
...                second=This value is even longer. It has two sentences.

*** Test Cases ***
Example
    [Tags]    you    probably    do    not    have    this    many
    ...       tags    in    real    life
    Do X    first argument    second argument    third argument
    ...    fourth argument    fifth argument    sixth argument
    ${var} =    Get X
    ...    first argument passed to this keyword is pretty long
    ...    second argument passed to this keyword is long too
```

## Style

Cú pháp của Robot Framework tạo ra một ngôn ngữ lập trình đơn giản, và cũng như với các ngôn ngữ khác, việc nghĩ về phong cách lập trình là rất quan trọng. Cú pháp của Robot Framework khá linh hoạt với mục đích như vậy, nhưng có một số quy ước được khuyến nghị chung:

* Thụt lề bốn khoảng trắng.

* Khoảng cách bốn khoảng trắng giữa các từ khóa và các đối số, các cài đặt và giá trị của chúng, v.v... Trong một số trường hợp, hợp lý khi sử dụng nhiều hơn bốn khoảng trắng, chẳng hạn như khi căn chỉnh các giá trị trong phần Cài đặt hoặc Biến hoặc trong phong cách dữ liệu động.

* Các biến toàn cục sử dụng chữ hoa như ${EXAMPLE} và các biến cục bộ sử dụng chữ thường như ${example}.

* Sự nhất quán trong một tệp duy nhất và tốt nhất là trong toàn bộ dự án.

Một trường hợp mà hiện tại không có quy ước mạnh mẽ là việc viết hoa từ khóa. Robot Framework thường sử dụng chữ cái đầu của mỗi từ như Example Keyword trong tài liệu và ở nơi khác, và phong cách này thường được sử dụng trong dữ liệu của Robot Framework. Tuy nhiên, nó không hoạt động tốt với các từ khóa dài, giống như câu như Log into system as an admin.

Các đội và tổ chức sử dụng Robot Framework nên có các tiêu chuẩn lập trình riêng của mình. Hướng dẫn phong cách Robot Framework do cộng đồng phát triển là một điểm khởi đầu xuất sắc mà có thể được sửa đổi khi cần thiết. Cũng có thể thực thi những quy ước này bằng cách sử dụng công cụ kiểm tra mã Robocop và định dạng mã Robotidy.