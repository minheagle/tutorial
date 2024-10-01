# Creating test cases

## Test case syntax

#### Basic syntax

Các test case được tạo ra trong các phần test case từ các từ khóa có sẵn. Từ khóa có thể được nhập từ các thư viện kiểm thử hoặc từ các tệp tài nguyên, hoặc được tạo trong phần từ khóa của chính tệp test case.

Cột đầu tiên trong phần test case chứa tên các test case. Một test case bắt đầu từ hàng có dữ liệu trong cột này và tiếp tục cho đến tên test case tiếp theo hoặc đến cuối phần này. Sẽ xảy ra lỗi nếu có dữ liệu nào giữa tiêu đề phần và test case đầu tiên.

Cột thứ hai thông thường chứa tên các từ khóa. Ngoại lệ cho quy tắc này là khi thiết lập biến từ các giá trị trả về của từ khóa, khi đó cột thứ hai và có thể là các cột tiếp theo chứa tên các biến, và tên từ khóa sẽ nằm sau chúng. Trong cả hai trường hợp, các cột sau tên từ khóa chứa các đối số (arguments) có thể được truyền vào từ khóa được chỉ định.

```robotframework
*** Test Cases ***
Valid Login
    Open Login Page
    Input Username    demo
    Input Password    mode
    Submit Credentials
    Welcome Page Should Be Open

Setting Variables
    Do Something    first argument    second argument
    ${value} =    Get Some Value
    Should Be Equal    ${value}    Expected value
```

!!! Note 
    Mặc dù tên test case có thể chứa bất kỳ ký tự nào, nhưng việc sử dụng ? và đặc biệt là * không được khuyến khích vì chúng được coi là ký tự đại diện (wildcards) khi chọn test case. Ví dụ, khi cố gắng chạy một test có tên Example * bằng lệnh --test 'Example *', thì thực tế sẽ chạy tất cả các test bắt đầu bằng Example.

#### Settings in the Test Case section

Các test case cũng có thể có các thiết lập riêng. Tên của thiết lập luôn nằm ở cột thứ hai, nơi thường chứa các từ khóa, và giá trị của chúng nằm ở các cột tiếp theo. Tên của thiết lập có dấu ngoặc vuông xung quanh để phân biệt với từ khóa. Các thiết lập có sẵn được liệt kê dưới đây và sẽ được giải thích chi tiết hơn trong phần này.

* **[Documentation]**: Dùng để chỉ định tài liệu cho test case.

* **[Setup]**, **[Teardown]**: Chỉ định thiết lập trước và sau khi thực hiện test.

* **[Tags]**: Dùng để gắn thẻ cho các test case.

* **[Template]**: Chỉ định từ khóa mẫu để sử dụng. Test case sẽ chỉ chứa dữ liệu làm đối số cho từ khóa đó.

* **[Timeout]**: Dùng để thiết lập thời gian chờ cho test case. Thời gian chờ sẽ được thảo luận trong phần riêng của nó.

!!! Note 
    Tên của các thiết lập không phân biệt chữ hoa chữ thường, nhưng định dạng được sử dụng ở trên là khuyến nghị. Trước đây, các thiết lập cũng không phân biệt khoảng trắng, nhưng tính năng này đã bị loại bỏ trong Robot Framework 3.1, và việc cố sử dụng một định dạng như [T a g s] sẽ gây ra lỗi trong Robot Framework 3.2. Tuy nhiên, các khoảng trắng giữa dấu ngoặc và tên (ví dụ: [ Tags ]) vẫn được phép.

Ví dụ: 

```robotframework
*** Test Cases ***
Test With Settings
    [Documentation]    Another dummy test
    [Tags]    dummy    owner-johndoe
    Log    Hello, world!
```

#### Test case related settings in the Setting section

Phần Setting có thể chứa các thiết lập liên quan đến test case sau. Các thiết lập này chủ yếu là giá trị mặc định cho các thiết lập cụ thể của test case đã được liệt kê trước đó.

* **Test Setup**, **Test Teardown**: Giá trị mặc định cho thiết lập trước và sau khi thực hiện test.

* **Test Tags**: Gắn thẻ mặc định cho tất cả các test trong bộ test, ngoài các thẻ riêng của từng test.

* **Test Template**: Từ khóa mẫu mặc định sẽ được sử dụng.

* **Test Timeout**: Giá trị mặc định cho thời gian chờ của test case. Thời gian chờ sẽ được thảo luận trong phần riêng của nó.

## Using arguments

Các ví dụ trước đã minh họa từ khóa có thể nhận các tham số khác nhau, và phần này sẽ thảo luận kỹ hơn về chức năng quan trọng này. Cách thực hiện các từ khóa do người dùng tạo và từ khóa của thư viện với các tham số khác nhau sẽ được thảo luận trong các phần riêng biệt.

Từ khóa có thể chấp nhận từ không đến nhiều tham số, và một số tham số có thể có giá trị mặc định. Các tham số mà một từ khóa chấp nhận phụ thuộc vào cách nó được thực hiện, và thông tin này thường được tìm thấy tốt nhất trong tài liệu của từ khóa đó. Trong các ví dụ ở phần này, tài liệu được giả định là được tạo bằng công cụ Libdoc, nhưng thông tin tương tự cũng có sẵn trong tài liệu được tạo bằng các công cụ tài liệu chung như pydoc.

#### Positional arguments

Hầu hết các từ khóa yêu cầu một số lượng tham số nhất định phải được cung cấp. Trong tài liệu của từ khóa, điều này được biểu thị bằng cách chỉ định tên các tham số, ngăn cách bằng dấu phẩy như first, second, third. Tên của các tham số thực sự không quan trọng trong trường hợp này, ngoại trừ việc chúng nên giải thích rõ chức năng của tham số, nhưng điều quan trọng là phải có đúng số lượng tham số như được chỉ định trong tài liệu. Việc sử dụng quá ít hoặc quá nhiều tham số sẽ dẫn đến lỗi.

Ví dụ dưới đây sử dụng các từ khóa Create Directory và Copy File từ thư viện OperatingSystem. Các tham số của chúng được chỉ định là path và source, destination, nghĩa là chúng lần lượt yêu cầu một và hai tham số. Từ khóa cuối cùng, No Operation từ BuiltIn, không yêu cầu tham số nào.

```robotframework
*** Test Cases ***
Example
    Create Directory    ${TEMPDIR}/stuff
    Copy File    ${CURDIR}/file.txt    ${TEMPDIR}/stuff
    No Operation
```

#### Default values

Các tham số thường có giá trị mặc định, có thể được cung cấp hoặc không. Trong tài liệu, giá trị mặc định thường được tách khỏi tên tham số bằng dấu bằng, ví dụ: name=default value. Có thể tất cả các tham số đều có giá trị mặc định, nhưng không thể có bất kỳ tham số vị trí nào sau các tham số có giá trị mặc định.

Việc sử dụng giá trị mặc định được minh họa bằng ví dụ dưới đây, trong đó sử dụng từ khóa Create File với các tham số path, content=, encoding=UTF-8. Cố gắng sử dụng từ khóa này mà không có tham số nào hoặc với hơn ba tham số sẽ không hoạt động.

```robotframework
*** Test Cases ***
Example
    Create File    ${TEMPDIR}/empty.txt
    Create File    ${TEMPDIR}/utf-8.txt         Hyvä esimerkki
    Create File    ${TEMPDIR}/iso-8859-1.txt    Hyvä esimerkki    ISO-8859-1
```

#### Variable number of arguments

Cũng có thể một từ khóa chấp nhận số lượng tham số bất kỳ. Các tham số kiểu này, được gọi là varargs, có thể được kết hợp với các tham số bắt buộc và tham số có giá trị mặc định, nhưng chúng luôn được đặt sau các tham số này. Trong tài liệu, varargs có dấu hoa thị trước tên tham số, ví dụ: *varargs.

Chẳng hạn, các từ khóa Remove Files và Join Paths từ thư viện OperatingSystem có các tham số lần lượt là *paths và base, *parts. Từ khóa đầu tiên có thể được sử dụng với bất kỳ số lượng tham số nào, nhưng từ khóa thứ hai yêu cầu ít nhất một tham số.

```robotframework
*** Test Cases ***
Example
    Remove Files    ${TEMPDIR}/f1.txt    ${TEMPDIR}/f2.txt    ${TEMPDIR}/f3.txt
    @{paths} =    Join Paths    ${TEMPDIR}    f1.txt    f2.txt    f3.txt    f4.txt
```

#### Named arguments

Cú pháp tham số có tên (named argument) giúp việc sử dụng các tham số có giá trị mặc định linh hoạt hơn và cho phép gắn nhãn rõ ràng cho giá trị của một tham số cụ thể. Về mặt kỹ thuật, các tham số có tên hoạt động giống hệt như các keyword arguments trong Python.

###### Basic syntax

Có thể đặt tên cho một tham số được truyền cho một từ khóa bằng cách thêm tên của tham số trước giá trị như arg=value. Điều này đặc biệt hữu ích khi nhiều tham số có giá trị mặc định, vì bạn có thể chỉ định tên cho một số tham số và để các tham số khác sử dụng giá trị mặc định của chúng. Ví dụ, nếu một từ khóa chấp nhận các tham số arg1=a, arg2=b, arg3=c, và được gọi với một tham số arg3=override, thì các tham số arg1 và arg2 sẽ nhận giá trị mặc định, nhưng arg3 sẽ nhận giá trị override. Nếu điều này có vẻ phức tạp, ví dụ về các tham số có tên dưới đây sẽ giúp làm rõ hơn.

Cú pháp tham số có tên nhạy cảm với cả chữ hoa và khoảng trắng. Điều này có nghĩa là nếu bạn có một tham số arg, bạn phải sử dụng nó như arg=value, và không có Arg=value hay ARG=value nào hoạt động. Điều này cũng có nghĩa là không cho phép có khoảng trắng trước dấu "=" và các khoảng trắng có thể có sau nó sẽ được coi là một phần của giá trị được cung cấp.

Khi cú pháp tham số có tên được sử dụng với các từ khóa do người dùng định nghĩa, các tên tham số phải được ghi mà không có ký hiệu ${}. Ví dụ, từ khóa của người dùng với các tham số ${arg1}=first, ${arg2}=second phải được sử dụng như arg2=override.

Việc sử dụng các tham số vị trí thông thường sau các tham số có tên như, chẳng hạn, | Keyword | arg=value | positional |, sẽ không hoạt động. Thứ tự tương đối của các tham số có tên không quan trọng.

###### Named arguments with variables

Có thể sử dụng biến trong cả tên và giá trị của các tham số có tên. Nếu giá trị là một biến đơn, nó sẽ được truyền cho từ khóa mà không thay đổi gì. Điều này cho phép sử dụng bất kỳ đối tượng nào, không chỉ chuỗi, làm giá trị khi sử dụng cú pháp tham số có tên. Ví dụ, gọi một từ khóa như arg=${object} sẽ truyền biến ${object} đến từ khóa mà không chuyển đổi nó thành chuỗi.

Nếu biến được sử dụng trong tên tham số có tên, các biến này sẽ được giải quyết trước khi khớp với các tên tham số.

Cú pháp tham số có tên yêu cầu dấu "=" phải được viết chính xác trong cuộc gọi từ khóa. Điều này có nghĩa là biến một mình sẽ không bao giờ kích hoạt cú pháp tham số có tên, ngay cả khi nó có giá trị như foo=bar. Đây là điều quan trọng cần nhớ, đặc biệt là khi bọc các từ khóa vào các từ khóa khác. Nếu, ví dụ, một từ khóa chấp nhận một số lượng biến tham số như @{args} và truyền tất cả chúng đến một từ khóa khác bằng cách sử dụng cùng cú pháp @{args}, thì cú pháp named=arg có thể được sử dụng ở phía gọi sẽ không được nhận diện. Điều này được minh họa bởi ví dụ dưới đây.

```robotframework
*** Test Cases ***
Example
    Run Program    shell=True    # This will not come as a named argument to Run Process

*** Keywords ***
Run Program
    [Arguments]    @{args}
    Run Process    program.py    @{args}    # Named arguments are not recognized from inside @{args}
```


Nếu một từ khóa cần chấp nhận và chuyển tiếp bất kỳ tham số có tên nào, nó phải được thay đổi để chấp nhận các tham số có tên tự do. Hãy xem các ví dụ về tham số có tên tự do để biết một phiên bản từ khóa bọc có thể chuyển tiếp cả tham số vị trí và tham số có tên.

###### Escaping named arguments syntax

Cú pháp tham số có tên chỉ được sử dụng khi phần của tham số trước dấu "=" khớp với một trong các tham số của từ khóa. Có thể có một tham số vị trí với giá trị văn bản như foo=quux, và cũng có một tham số không liên quan có tên là foo. Trong trường hợp này, tham số foo sẽ nhận giá trị quux một cách không chính xác, hoặc có thể sẽ xảy ra lỗi cú pháp.

Trong những trường hợp hiếm hoi mà có sự khớp nhầm lẫn, có thể sử dụng ký tự backslash để thoát cú pháp như foo=quux. Bây giờ, tham số sẽ nhận giá trị văn bản foo=quux. Lưu ý rằng việc thoát không cần thiết nếu không có tham số nào có tên foo, nhưng vì nó làm cho tình huống rõ ràng hơn, vẫn có thể là một ý tưởng tốt.

###### Where named arguments are supported

Như đã giải thích trước đó, cú pháp tham số có tên hoạt động với các từ khóa. Ngoài ra, nó cũng hoạt động khi nhập các thư viện.

Việc đặt tên tham số được hỗ trợ bởi các từ khóa người dùng và hầu hết các thư viện kiểm tra. Những ngoại lệ duy nhất là các từ khóa Python sử dụng rõ ràng các tham số chỉ vị trí.

###### Named arguments example

Ví dụ sau đây minh họa cách sử dụng cú pháp tham số có tên với các từ khóa thư viện, từ khóa người dùng và khi nhập thư viện kiểm tra Telnet.

```robotframework
*** Settings ***
Library    Telnet    prompt=$    default_log_level=DEBUG

*** Test Cases ***
Example
    Open connection    10.0.0.42    port=${PORT}    alias=example
    List files    options=-lh
    List files    path=/tmp    options=-l

*** Keywords ***
List files
    [Arguments]    ${path}=.    ${options}=
    Execute command    ls ${options} ${path}
```

#### Free named arguments


Robot Framework hỗ trợ các tham số có tên tự do, thường được gọi là tham số từ khóa tự do hoặc kwargs, tương tự như Python hỗ trợ **kwargs. Điều này có nghĩa là một từ khóa có thể nhận tất cả các tham số sử dụng cú pháp tham số có tên (name=value) và không khớp với bất kỳ tham số nào được chỉ định trong chữ ký của từ khóa.

Các tham số có tên tự do được hỗ trợ bởi cùng một loại từ khóa như các tham số có tên thông thường. Cách mà các từ khóa chỉ định rằng chúng chấp nhận các tham số có tên tự do phụ thuộc vào loại từ khóa. Ví dụ, các từ khóa dựa trên Python đơn giản sử dụng **kwargs và các từ khóa người dùng sử dụng &{kwargs}.

Các tham số có tên tự do hỗ trợ biến tương tự như các tham số có tên. Trên thực tế, điều đó có nghĩa là các biến có thể được sử dụng cả trong tên và giá trị, nhưng dấu escape phải luôn hiển thị một cách rõ ràng. Ví dụ, cả foo=${bar} và ${foo}=${bar} đều hợp lệ, miễn là các biến được sử dụng tồn tại. Một hạn chế bổ sung là tên tham số tự do phải luôn là chuỗi.

#### Examples

Như một ví dụ đầu tiên về việc sử dụng các tham số có tên tự do, hãy xem từ khóa Run Process trong thư viện Process. Nó có chữ ký như sau: **command, *arguments, configuration, điều này có nghĩa là nó nhận lệnh để thực thi (command), các tham số của nó dưới dạng số lượng tham số biến (*arguments) và cuối cùng là các tham số cấu hình tùy chọn dưới dạng tham số có tên tự do (configuration). Ví dụ dưới đây cũng cho thấy rằng các biến hoạt động với các tham số từ khóa tự do giống như khi sử dụng cú pháp tham số có tên.

```robotframework
*** Test Cases ***
Free Named Arguments
    Run Process    program.py    arg1    arg2    cwd=/home/user
    Run Process    program.py    argument    shell=True    env=${ENVIRON}
```

Xem phần **Free keyword arguments (kwargs) trong mục Tạo thư viện kiểm tra để biết thêm thông tin về cách sử dụng cú pháp tham số có tên tự do trong các thư viện kiểm tra tùy chỉnh của bạn.

Như một ví dụ thứ hai, hãy tạo một từ khóa người dùng bao bọc cho việc chạy program.py trong ví dụ trên. Từ khóa bao bọc Run Program chấp nhận tất cả các tham số vị trí và tham số có tên và truyền chúng tới từ khóa Run Process cùng với tên của lệnh để thực thi.

```robotframework
*** Test Cases ***
Free Named Arguments
    Run Program    arg1    arg2    cwd=/home/user
    Run Program    argument    shell=True    env=${ENVIRON}

*** Keywords ***
Run Program
    [Arguments]    @{args}    &{config}
    Run Process    program.py    @{args}    &{config}
```

#### Named-only arguments

Bắt đầu từ Robot Framework 3.1, các từ khóa có thể chấp nhận tham số mà phải luôn được đặt tên bằng cách sử dụng cú pháp tham số có tên. Nếu, chẳng hạn, một từ khóa chấp nhận một tham số duy nhất chỉ có tên là example, thì nó luôn cần được sử dụng như example=value và việc chỉ sử dụng value sẽ không hoạt động. Cú pháp này được lấy cảm hứng từ cú pháp tham số chỉ tên được hỗ trợ bởi Python 3.

Đối với hầu hết các phần, các tham số chỉ tên hoạt động tương tự như các tham số có tên. Sự khác biệt chính là các thư viện được thực hiện bằng Python 2 sử dụng API thư viện tĩnh không hỗ trợ cú pháp này.

Là một ví dụ về việc sử dụng các tham số chỉ tên với các từ khóa người dùng, dưới đây là một biến thể của Run Program trong các ví dụ về tham số có tên tự do ở trên, chỉ hỗ trợ cấu hình shell:

```robotframework
*** Test Cases ***
Named-only Arguments
    Run Program    arg1    arg2              # 'shell' is False (default)
    Run Program    argument    shell=True    # 'shell' is True

*** Keywords ***
Run Program
    [Arguments]    @{args}    ${shell}=False
    Run Process    program.py    @{args}    shell=${shell}
```

#### Arguments embedded to keyword names

Một cách hoàn toàn khác để chỉ định các tham số là nhúng chúng vào trong tên từ khóa. Cú pháp này được hỗ trợ bởi cả từ khóa thư viện kiểm tra và từ khóa người dùng.

## Failures

#### When test case fails


Một trường hợp kiểm tra sẽ thất bại nếu bất kỳ từ khóa nào mà nó sử dụng thất bại. Thông thường, điều này có nghĩa là việc thực thi của trường hợp kiểm tra đó sẽ bị dừng lại, các thao tác dọn dẹp kiểm tra có thể được thực hiện, và sau đó việc thực thi sẽ tiếp tục từ trường hợp kiểm tra tiếp theo. Cũng có thể sử dụng các lỗi có thể tiếp tục đặc biệt nếu không muốn dừng việc thực thi kiểm tra.

#### Error messages

Thông điệp lỗi được gán cho một trường hợp kiểm tra thất bại được lấy trực tiếp từ từ khóa đã thất bại. Thông thường, thông điệp lỗi được tạo ra bởi chính từ khóa, nhưng một số từ khóa cho phép cấu hình chúng.

Trong một số trường hợp, chẳng hạn như khi sử dụng các lỗi có thể tiếp tục, một trường hợp kiểm tra có thể thất bại nhiều lần. Trong trường hợp đó, thông điệp lỗi cuối cùng được tạo ra bằng cách kết hợp các lỗi riêng lẻ. Những thông điệp lỗi rất dài sẽ tự động bị cắt từ giữa để giữ cho báo cáo dễ đọc hơn, nhưng toàn bộ thông điệp lỗi luôn được hiển thị trong các tệp nhật ký dưới dạng thông điệp của các từ khóa bị thất bại.

Theo mặc định, thông điệp lỗi là văn bản bình thường, nhưng chúng có thể chứa định dạng HTML. Điều này được kích hoạt bằng cách bắt đầu thông điệp lỗi với chuỗi dấu hiệu HTML. Dấu hiệu này sẽ bị loại bỏ khỏi thông điệp lỗi cuối cùng được hiển thị trong báo cáo và nhật ký. Việc sử dụng HTML trong một thông điệp tùy chỉnh được hiển thị trong ví dụ thứ hai dưới đây.

```robotframework
*** Test Cases ***
Normal Error
    Fail    This is a rather boring example...

HTML Error
    ${number} =    Get Number
    Should Be Equal    ${number}    42    *HTML* Number is not my <b>MAGIC</b> number.
```

## Test case name and documentation

Tên của trường hợp kiểm tra đến từ phần Test Case: nó hoàn toàn giống với những gì được nhập vào cột trường hợp kiểm tra. Các trường hợp kiểm tra trong một bộ kiểm tra nên có tên duy nhất. Liên quan đến điều này, bạn cũng có thể sử dụng biến tự động ${TEST_NAME} bên trong chính bài kiểm tra để tham chiếu đến tên kiểm tra. Nó có sẵn mỗi khi một bài kiểm tra đang được thực hiện, bao gồm tất cả các từ khóa người dùng, cũng như thiết lập kiểm tra và dọn dẹp kiểm tra.

Bắt đầu từ Robot Framework 3.2, các biến có thể trong tên trường hợp kiểm tra sẽ được giải quyết để tên cuối cùng sẽ chứa giá trị biến. Nếu biến không tồn tại, tên của nó sẽ được giữ nguyên.

```robotframework
*** Variables ***
${MAX AMOUNT}      ${5000000}

*** Test Cases ***
Amount cannot be larger than ${MAX AMOUNT}
    # ...
```

Cài đặt [Documentation] cho phép thiết lập tài liệu dạng tự do cho một trường hợp kiểm tra. Văn bản đó được hiển thị trong đầu ra dòng lệnh cũng như trong các nhật ký và báo cáo kết quả. Nếu tài liệu quá dài, nó có thể được chia thành nhiều hàng. Có thể sử dụng định dạng HTML đơn giản và các biến có thể được sử dụng để làm cho tài liệu trở nên động. Các biến không tồn tại có thể được để nguyên.

```robotframework
*** Test Cases ***
Simple
    [Documentation]    Simple and short documentation.
    No Operation

Multiple lines
    [Documentation]    First row of the documentation.
    ...
    ...                Documentation continues here. These rows form
    ...                a paragraph when shown in HTML outputs.
    No Operation

Formatting
    [Documentation]
    ...    This list has:
    ...    - *bold*
    ...    - _italics_
    ...    - link: http://robotframework.org
    No Operation

Variables
    [Documentation]    Executed at ${HOST} by ${USER}
    No Operation
```

Việc đặt tên rõ ràng và mô tả cho các trường hợp kiểm tra là rất quan trọng, và trong trường hợp này, chúng thường không cần tài liệu bổ sung. Nếu logic của trường hợp kiểm tra cần được ghi chú, thì đó thường là dấu hiệu cho thấy các từ khóa trong trường hợp kiểm tra cần được đặt tên tốt hơn và cần được cải thiện, thay vì thêm tài liệu bổ sung. Cuối cùng, thông tin siêu dữ liệu, chẳng hạn như thông tin môi trường và người dùng trong ví dụ cuối cùng ở trên, thường được chỉ định tốt hơn bằng cách sử dụng thẻ (tags).

## Tagging test cases

Việc sử dụng thẻ (tags) trong Robot Framework là một cơ chế đơn giản nhưng mạnh mẽ để phân loại các trường hợp kiểm tra và các từ khóa người dùng. Các thẻ là văn bản tự do và Robot Framework không có ý nghĩa đặc biệt nào đối với chúng, ngoại trừ các thẻ được dự trữ được thảo luận dưới đây. Các thẻ có thể được sử dụng ít nhất cho các mục đích sau:

* **Cung cấp siêu dữ liệu**: Chúng được hiển thị trong báo cáo kiểm tra, nhật ký và tất nhiên là trong dữ liệu kiểm tra, do đó cung cấp thông tin siêu dữ liệu cho các trường hợp kiểm tra.

* **Thu thập thống kê**: Thống kê về các trường hợp kiểm tra (tổng số, đã thông qua, thất bại và bị bỏ qua) được tự động thu thập dựa trên các thẻ này.

* **Quản lý trường hợp kiểm tra**: Chúng có thể được sử dụng để bao gồm và loại trừ cũng như bỏ qua các trường hợp kiểm tra.

Có nhiều cách để chỉ định thẻ cho các trường hợp kiểm tra, được giải thích dưới đây:

* **Cài đặt Thẻ Kiểm Tra (Test Tags) trong phần Cài đặt**: Tất cả các kiểm tra trong một tệp kiểm tra luôn nhận được các thẻ đã chỉ định. Nếu cài đặt này được sử dụng trong một tệp khởi tạo suite, tất cả các kiểm tra trong các suite con sẽ nhận được các thẻ này.

* **Cài đặt [Tags] với mỗi trường hợp kiểm tra**: Các kiểm tra sẽ nhận được các thẻ này bổ sung cho các thẻ được chỉ định bằng cách sử dụng cài đặt Thẻ Kiểm Tra. Cài đặt [Tags] cũng cho phép xóa các thẻ đã thiết lập với Thẻ Kiểm Tra bằng cách sử dụng cú pháp -tag.

* **Tùy chọn dòng lệnh --settag**: Tất cả các kiểm tra sẽ nhận được các thẻ được thiết lập với tùy chọn này bổ sung cho các thẻ mà chúng đã nhận được ở nơi khác.

* **Các từ khóa BuiltIn như Set Tags, Remove Tags, Fail và Pass Execution**: Các từ khóa này có thể được sử dụng để thao tác các thẻ một cách động trong suốt quá trình kiểm tra.

```robotframework
*** Settings ***
Test Tags       requirement: 42    smoke

*** Variables ***
${HOST}         10.0.1.42

*** Test Cases ***
No own tags
    [Documentation]    Test has tags 'requirement: 42' and 'smoke'.
    No Operation

Own tags
    [Documentation]    Test has tags 'requirement: 42', 'smoke' and 'not ready'.
    [Tags]    not ready
    No Operation

Own tags with variable
    [Documentation]    Test has tags 'requirement: 42', 'smoke' and 'host: 10.0.1.42'.
    [Tags]    host: ${HOST}
    No Operation

Remove common tag
    [Documentation]    Test has only tag 'requirement: 42'.
    [Tags]    -smoke
    No Operation

Remove common tag using a pattern
    [Documentation]    Test has only tag 'smoke'.
    [Tags]    -requirement: *
    No Operation

Set Tags and Remove Tags keywords
    [Documentation]    This test has tags 'smoke', 'example' and 'another'.
    Set Tags    example    another
    Remove Tags    requirement: *
```

Như ví dụ đã chỉ ra, các thẻ có thể được tạo bằng cách sử dụng biến, nhưng ngược lại, chúng giữ nguyên tên chính xác được sử dụng trong dữ liệu. Khi so sánh các thẻ, ví dụ như để thu thập thống kê, chọn các bài kiểm tra được thực thi hoặc loại bỏ các mục trùng lặp, thì việc so sánh không phân biệt chữ hoa, khoảng trắng và dấu gạch dưới.

Như đã trình bày trong các ví dụ trên, việc xóa thẻ bằng cú pháp -tag hỗ trợ các mẫu đơn giản như -requirement: *. Các thẻ bắt đầu bằng dấu gạch ngang không có ý nghĩa đặc biệt nào khác ngoài việc sử dụng với cài đặt [Tags]. Nếu cần thiết lập một thẻ bắt đầu bằng dấu gạch ngang với [Tags], có thể sử dụng định dạng thoát như \-tag.

!!! Note 
    Cài đặt Test Tags là một tính năng mới trong Robot Framework 6.0. Các phiên bản trước chỉ hỗ trợ các cài đặt Force Tags và Default Tags, được thảo luận trong phần tiếp theo.

!!! Note 
    Cú pháp -tag để xóa các thẻ chung là một tính năng mới trong Robot Framework 7.0. 

#### Deprecation of Force Tags and Default Tags

Trước phiên bản Robot Framework 6.0, các thẻ (tags) có thể được chỉ định cho các bài kiểm tra trong phần Cài đặt (Setting) bằng hai cài đặt khác nhau:

* **Force Tags (Thẻ Bắt Buộc)**: Tất cả các bài kiểm tra đều nhận những thẻ này mà không điều kiện nào. Điều này hoàn toàn giống với Thẻ Kiểm Tra (Test Tags) trong phiên bản hiện tại.

* **Default Tags (Thẻ Mặc Định)**: Tất cả các bài kiểm tra đều nhận những thẻ này theo mặc định. Nếu một bài kiểm tra có [Tags], nó sẽ không nhận các thẻ này.

Cả hai cài đặt này vẫn hoạt động, nhưng được coi là đã lỗi thời (deprecated). Một cảnh báo rõ ràng về việc lỗi thời sẽ được thêm vào trong tương lai, rất có thể trong phiên bản Robot Framework 8.0, và cuối cùng những cài đặt này sẽ bị xóa bỏ. Các công cụ như Tidy có thể được sử dụng để hỗ trợ quá trình chuyển đổi.

Việc cập nhật Force Tags chỉ cần đổi tên nó thành Test Tags. Cài đặt Default Tags sẽ bị xóa hoàn toàn, nhưng chức năng -tag được giới thiệu trong Robot Framework 7.0 cung cấp cùng một chức năng cơ bản. Các ví dụ sau đây minh họa những thay đổi cần thiết.

Old syntax:

```robotframework
*** Settings ***
Force Tags      all
Default Tags    default

*** Test Cases ***
Common only
    [Documentation]    Test has tags 'all' and 'default'.
    No Operation

No default
    [Documentation]    Test has only tag 'all'.
    [Tags]
    No Operation

Own and no default
    [Documentation]    Test has tags 'all' and 'own'.
    [Tags]    own
    No Operation
```

New syntax:

```robotframework
*** Settings ***
Test Tags      all    default

*** Test Cases ***
Common only
    [Documentation]    Test has tags 'all' and 'default'.
    No Operation

No default
    [Documentation]    Test has only tag 'all'.
    [Tags]    -default
    No Operation

Own and no default
    [Documentation]    Test has tags 'all' and 'own'.
    [Tags]    own    -default
    No Operation
```

#### Reserved tags

Người dùng thường được tự do sử dụng bất kỳ thẻ nào phù hợp với ngữ cảnh của họ. Tuy nhiên, có một số thẻ có ý nghĩa định sẵn cho chính Robot Framework, và việc sử dụng chúng cho các mục đích khác có thể gây ra những kết quả không mong muốn. Tất cả các thẻ đặc biệt mà Robot Framework hiện có và sẽ có trong tương lai đều có tiền tố robot:. Để tránh các vấn đề, người dùng không nên sử dụng bất kỳ thẻ nào có tiền tố này trừ khi thực sự kích hoạt chức năng đặc biệt. Các thẻ được giữ lại hiện tại được liệt kê dưới đây, nhưng có khả năng nhiều thẻ như vậy sẽ được thêm vào trong tương lai.

* **robot:continue-on-failure** and **robot:recursive-continue-on-failure**: Sử dụng để kích hoạt chế độ tiếp tục khi gặp lỗi.

* **robot:stop-on-failure** and **robot:recursive-stop-on-failure**: Sử dụng để vô hiệu hóa chế độ tiếp tục khi gặp lỗi.

* **robot:skip-on-failure**: Đánh dấu bài kiểm tra để bị bỏ qua nếu nó thất bại.

* **robot:skip**: Đánh dấu bài kiểm tra để bị bỏ qua một cách không điều kiện.

* **robot:exclude**: Đánh dấu bài kiểm tra để bị loại trừ một cách không điều kiện.

* **robot:private**: Đánh dấu từ khóa là riêng tư.

* **robot:no-dry-run**: Đánh dấu từ khóa không được thực thi trong chế độ chạy thử.

* **robot:exit**: Tự động được thêm vào các bài kiểm tra khi việc thực thi dừng một cách suôn sẻ.

* **robot:flatten**: Kích hoạt việc làm phẳng từ khóa trong thời gian thực thi.

Với Robot Framework 4.1, các thẻ đã giữ chỗ được ẩn theo mặc định trong thống kê thẻ. Chúng sẽ được hiển thị khi chúng được bao gồm một cách rõ ràng qua tùy chọn dòng lệnh --tagstatinclude robot:*.

## Test setup and teardown

Robot Framework có chức năng thiết lập và dọn dẹp (teardown) kiểm thử tương tự như nhiều framework tự động hóa kiểm thử khác. Nói ngắn gọn, thiết lập kiểm thử là những gì được thực thi trước khi một trường hợp kiểm thử diễn ra, và dọn dẹp kiểm thử được thực hiện sau khi một trường hợp kiểm thử kết thúc. Trong Robot Framework, các thiết lập và dọn dẹp chỉ là các từ khóa bình thường với các tham số có thể.

Một thiết lập và một dọn dẹp luôn là một từ khóa duy nhất. Nếu chúng cần thực hiện nhiều nhiệm vụ riêng biệt, có thể tạo ra các từ khóa người dùng cấp cao hơn cho mục đích đó. Một giải pháp thay thế là thực thi nhiều từ khóa bằng cách sử dụng từ khóa BuiltIn Run Keywords.

Dọn dẹp kiểm thử có đặc điểm đặc biệt ở hai điểm. Trước tiên, nó được thực thi ngay cả khi một trường hợp kiểm thử thất bại, vì vậy nó có thể được sử dụng cho các hoạt động dọn dẹp cần phải thực hiện bất kể trạng thái của trường hợp kiểm thử. Ngoài ra, tất cả các từ khóa trong dọn dẹp cũng sẽ được thực thi ngay cả khi một trong số chúng thất bại. Chức năng tiếp tục khi gặp lỗi này cũng có thể được sử dụng với các từ khóa bình thường, nhưng bên trong dọn dẹp thì mặc định là bật.

Cách dễ nhất để chỉ định một thiết lập hoặc dọn dẹp cho các trường hợp kiểm thử trong một tệp kiểm thử là sử dụng các cài đặt Test Setup và Test Teardown trong phần Setting. Các trường hợp kiểm thử riêng lẻ cũng có thể có thiết lập hoặc dọn dẹp riêng. Chúng được định nghĩa bằng các cài đặt [Setup] hoặc [Teardown] trong phần trường hợp kiểm thử và sẽ ghi đè lên các cài đặt Test Setup và Test Teardown có thể có. Không có từ khóa nào sau cài đặt [Setup] hoặc [Teardown] có nghĩa là không có thiết lập hoặc dọn dẹp nào. Cũng có thể sử dụng giá trị NONE để chỉ ra rằng một bài kiểm tra không có thiết lập/dọn dẹp.

```robotframework
*** Settings ***
Test Setup       Open Application    App A
Test Teardown    Close Application

*** Test Cases ***
Default values
    [Documentation]    Setup and teardown from setting section
    Do Something

Overridden setup
    [Documentation]    Own setup, teardown from setting section
    [Setup]    Open Application    App B
    Do Something

No teardown
    [Documentation]    Default setup, no teardown at all
    Do Something
    [Teardown]

No teardown 2
    [Documentation]    Setup and teardown can be disabled also with special value NONE
    Do Something
    [Teardown]    NONE

Using variables
    [Documentation]    Setup and teardown specified using variables
    [Setup]    ${SETUP}
    Do Something
    [Teardown]    ${TEARDOWN}
```

Tên của từ khóa được thực thi như một thiết lập hoặc dọn dẹp có thể là một biến. Điều này tạo điều kiện cho việc có các thiết lập hoặc dọn dẹp khác nhau trong các môi trường khác nhau bằng cách cung cấp tên từ khóa dưới dạng một biến từ dòng lệnh.

!!! Note 
    Các bộ kiểm tra (test suites) có thể có một thiết lập và dọn dẹp riêng của chúng. Một thiết lập cho bộ kiểm tra (suite setup) được thực thi trước bất kỳ trường hợp kiểm tra (test cases) hoặc bộ kiểm tra con (sub test suites) nào trong bộ kiểm tra đó, và tương tự, một dọn dẹp cho bộ kiểm tra (suite teardown) được thực thi sau chúng.

## Test templates

Các mẫu kiểm tra (test templates) chuyển đổi các trường hợp kiểm tra theo kiểu từ khóa thông thường thành các bài kiểm tra dựa trên dữ liệu. Trong khi phần thân của một trường hợp kiểm tra theo kiểu từ khóa được xây dựng từ các từ khóa và các đối số có thể có của chúng, thì các trường hợp kiểm tra với mẫu chỉ chứa các đối số cho từ khóa mẫu. Thay vì lặp lại cùng một từ khóa nhiều lần cho mỗi bài kiểm tra và/hoặc với tất cả các bài kiểm tra trong một tệp, có thể chỉ sử dụng nó một lần cho mỗi bài kiểm tra hoặc chỉ một lần cho mỗi tệp.

Các từ khóa mẫu có thể chấp nhận cả đối số vị trí thông thường và đối số theo tên, cũng như các đối số nhúng vào tên từ khóa. Khác với các cài đặt khác, không thể định nghĩa một mẫu bằng cách sử dụng một biến.

#### Basic usage

Cách một từ khóa chấp nhận các đối số vị trí thông thường có thể được sử dụng như một mẫu được minh họa bởi các trường hợp kiểm tra ví dụ dưới đây. Hai bài kiểm tra này hoàn toàn giống nhau về mặt chức năng.

```robotframework
*** Test Cases ***
Normal test case
    Example keyword    first argument    second argument

Templated test case
    [Template]    Example keyword
    first argument    second argument
```

Như ví dụ minh họa, có thể chỉ định mẫu cho một trường hợp kiểm tra riêng lẻ bằng cách sử dụng cài đặt [Template]. Một cách tiếp cận thay thế là sử dụng cài đặt Test Template trong phần Cài đặt, trong trường hợp này mẫu sẽ được áp dụng cho tất cả các trường hợp kiểm tra trong tệp kiểm tra đó. Cài đặt [Template] ghi đè lên mẫu có thể được thiết lập trong phần Cài đặt, và một giá trị trống cho [Template] có nghĩa là kiểm tra không có mẫu ngay cả khi Test Template được sử dụng. Cũng có thể sử dụng giá trị NONE để chỉ ra rằng một bài kiểm tra không có mẫu.

Nếu một trường hợp kiểm tra có mẫu có nhiều hàng dữ liệu trong nội dung của nó, mẫu sẽ được áp dụng cho tất cả các hàng theo từng hàng một. Điều này có nghĩa là cùng một từ khóa sẽ được thực thi nhiều lần, mỗi lần với dữ liệu trên từng hàng. Các bài kiểm tra có mẫu cũng đặc biệt ở chỗ rằng tất cả các vòng đều được thực hiện ngay cả khi một hoặc nhiều vòng đó thất bại. Cũng có thể sử dụng chế độ tiếp tục khi thất bại kiểu này với các bài kiểm tra thông thường, nhưng với các bài kiểm tra có mẫu, chế độ này sẽ tự động được bật.

```robotframework
*** Settings ***
Test Template    Example keyword

*** Test Cases ***
Templated test case
    first round 1     first round 2
    second round 1    second round 2
    third round 1     third round 2
```

Việc sử dụng các từ khóa với giá trị mặc định hoặc chấp nhận số lượng tham số biến đổi, cũng như việc sử dụng các tham số đặt tên và các tham số đặt tên tự do, hoạt động với các mẫu giống như cách chúng hoạt động ở những nơi khác. Việc sử dụng các biến trong các tham số cũng được hỗ trợ như bình thường.

#### Templates with embedded arguments

Templates hỗ trợ một biến thể của cú pháp tham số nhúng. Với các mẫu, cú pháp này hoạt động theo cách mà nếu từ khóa mẫu có biến trong tên của nó, chúng được coi là các vị trí dành cho tham số và được thay thế bằng các tham số thực tế được sử dụng với mẫu. Từ khóa kết quả sau đó được sử dụng mà không cần tham số vị trí. Điều này được minh họa tốt nhất bằng một ví dụ:

```robotframework
*** Test Cases ***
Normal test case with embedded arguments
    The result of 1 + 1 should be 2
    The result of 1 + 2 should be 3

Template with embedded arguments
    [Template]    The result of ${calculation} should be ${expected}
    1 + 1    2
    1 + 2    3

*** Keywords ***
The result of ${calculation} should be ${expected}
    ${result} =    Calculate    ${calculation}
    Should Be Equal    ${result}     ${expected}
```

Khi các tham số nhúng được sử dụng với mẫu, số lượng tham số trong tên từ khóa mẫu phải khớp với số lượng tham số mà nó được sử dụng cùng. Tuy nhiên, tên tham số không cần phải khớp với các tham số của từ khóa gốc, và cũng có thể sử dụng các tham số hoàn toàn khác nhau:

```robotframework
*** Test Cases ***
Different argument names
    [Template]    The result of ${foo} should be ${bar}
    1 + 1    2
    1 + 2    3

Only some arguments
    [Template]    The result of ${calculation} should be 3
    1 + 2
    4 - 1

New arguments
    [Template]    The ${meaning} of ${life} should be 42
    result    21 * 2
```

Lợi ích chính của việc sử dụng tham số nhúng với mẫu là tên tham số được chỉ định một cách rõ ràng. Khi sử dụng tham số thông thường, hiệu ứng tương tự có thể đạt được bằng cách đặt tên cho các cột chứa tham số. Điều này được minh họa bởi ví dụ về phong cách dựa trên dữ liệu trong phần tiếp theo.

#### Templates with FOR loops

Khi sử dụng mẫu với vòng lặp FOR, mẫu sẽ được áp dụng cho tất cả các bước bên trong vòng lặp. Chế độ "tiếp tục khi có lỗi" cũng được áp dụng trong trường hợp này, nghĩa là tất cả các bước sẽ được thực thi với tất cả các phần tử trong vòng lặp, ngay cả khi có lỗi xảy ra.

```robotframework
*** Test Cases ***
Template with FOR loop
    [Template]    Example keyword
    FOR    ${item}    IN    @{ITEMS}
        ${item}    2nd arg
    END
    FOR    ${index}    IN RANGE    42
        1st arg    ${index}
    END
```

#### Templates with IF/ELSE structures

Cấu trúc IF/ELSE cũng có thể được sử dụng cùng với các mẫu. Điều này có thể hữu ích, chẳng hạn, khi được sử dụng kết hợp với các vòng lặp FOR để lọc các tham số được thực thi.

```robotframework
*** Test Cases ***
Template with FOR and IF
    [Template]    Example keyword
    FOR    ${item}    IN    @{ITEMS}
        IF  ${item} < 5
            ${item}    2nd arg
        END
    END
```

## Different test case styles

Có nhiều cách khác nhau để viết các trường hợp kiểm tra. Các trường hợp kiểm tra mô tả một loại quy trình công việc có thể được viết theo phong cách điều khiển từ khóa (keyword-driven) hoặc phong cách điều khiển hành vi (behavior-driven). Phong cách dữ liệu điều khiển (data-driven) có thể được sử dụng để kiểm tra cùng một quy trình công việc với các dữ liệu đầu vào khác nhau.

#### Keyword-driven style

Các bài kiểm tra quy trình công việc, chẳng hạn như bài kiểm tra Đăng Nhập Hợp Lệ được mô tả trước đó, được xây dựng từ nhiều từ khóa và các tham số khả thi của chúng. Cấu trúc thông thường của chúng là đầu tiên đưa hệ thống về trạng thái ban đầu (Open Login Page in the Valid Login example), sau đó thực hiện một thao tác nào đó trên hệ thống (Input Name, Input Password, Submit Credentials), và cuối cùng xác minh rằng hệ thống hoạt động như mong đợi (Welcome Page Should Be Open).

#### Data-driven style

Một phong cách khác để viết các bài kiểm tra là phương pháp dựa trên dữ liệu, trong đó các bài kiểm tra chỉ sử dụng một từ khóa cấp cao duy nhất, thường được tạo ra dưới dạng từ khóa người dùng, nhằm ẩn đi quy trình kiểm tra thực tế. Những bài kiểm tra này rất hữu ích khi cần thử nghiệm cùng một kịch bản với dữ liệu đầu vào và/hoặc đầu ra khác nhau. Thay vì lặp lại cùng một từ khóa với mỗi bài kiểm tra, chức năng mẫu kiểm tra cho phép chỉ định từ khóa cần sử dụng chỉ một lần.

```robotframework
*** Settings ***
Test Template    Login with invalid credentials should fail

*** Test Cases ***                USERNAME         PASSWORD
Invalid User Name                 invalid          ${VALID PASSWORD}
Invalid Password                  ${VALID USER}    invalid
Invalid User Name and Password    invalid          invalid
Empty User Name                   ${EMPTY}         ${VALID PASSWORD}
Empty Password                    ${VALID USER}    ${EMPTY}
Empty User Name and Password      ${EMPTY}         ${EMPTY}
```

!!! Tip 
    Việc đặt tên các cột như trong ví dụ ở trên giúp các bài kiểm tra trở nên dễ hiểu hơn. Điều này khả thi vì trên hàng tiêu đề, các ô khác ngoại trừ ô đầu tiên sẽ bị bỏ qua.

Ví dụ trên có sáu bài kiểm tra riêng biệt, một bài cho mỗi kết hợp tên người dùng/mật khẩu không hợp lệ, trong khi ví dụ dưới đây minh họa cách có chỉ một bài kiểm tra với tất cả các kết hợp. Khi sử dụng mẫu kiểm tra, tất cả các vòng trong một bài kiểm tra đều được thực hiện ngay cả khi có lỗi, vì vậy không có sự khác biệt chức năng thực sự giữa hai phong cách này. Trong ví dụ trên, các kết hợp riêng biệt được đặt tên để dễ dàng thấy được những gì chúng kiểm tra, nhưng việc có một số lượng lớn các bài kiểm tra như vậy có thể làm rối thống kê. Phong cách nào được sử dụng phụ thuộc vào ngữ cảnh và sở thích cá nhân.

```robotframework
*** Test Cases ***
Invalid Password
    [Template]    Login with invalid credentials should fail
    invalid          ${VALID PASSWORD}
    ${VALID USER}    invalid
    invalid          whatever
    ${EMPTY}         ${VALID PASSWORD}
    ${VALID USER}    ${EMPTY}
    ${EMPTY}         ${EMPTY}
```

#### Behavior-driven style


Cũng có thể viết các bài kiểm tra dưới dạng yêu cầu mà ngay cả những người tham gia dự án không chuyên môn cũng phải hiểu. Những yêu cầu có thể thực thi này là một nền tảng của một quy trình thường được gọi là Phát triển Được Kiểm Tra Bằng Chấp Nhận (ATDD) hoặc Đặc Tả Qua Ví Dụ.

Một cách để viết những yêu cầu/kiểm tra này là theo phong cách Given-When-Then, phong cách này được phổ biến bởi Phát Triển Dựa Trên Hành Vi (BDD). Khi viết các bài kiểm tra theo phong cách này, trạng thái ban đầu thường được diễn đạt bằng một từ khóa bắt đầu bằng từ Given, các hành động được mô tả bằng từ khóa bắt đầu bằng từ When, và các kỳ vọng được diễn đạt bằng từ khóa bắt đầu bằng từ Then. Các từ khóa bắt đầu bằng And hoặc But có thể được sử dụng nếu một bước có hơn một hành động.

```robotframework
*** Test Cases ***
Valid Login
    Given login page is open
    When valid username and password are inserted
    and credentials are submitted
    Then welcome page should be open
```

###### Ignoring Given/When/Then/And/But prefixes

Các tiền tố Given, When, Then, And và But có thể được bỏ qua khi tạo từ khóa. Ví dụ, câu "Given login page is open" trong ví dụ trên thường được triển khai mà không có từ "Given", do đó tên chỉ đơn giản là "Login page is open". Việc bỏ qua các tiền tố cho phép sử dụng cùng một từ khóa với các tiền tố khác nhau. Ví dụ, "Welcome page should be open" có thể được sử dụng như "Then welcome page should be open" hoặc "And welcome page should be open".

!!! Note 
    Các tiền tố này có thể được địa phương hóa. Xem phần Phụ lục Dịch thuật để biết các bản dịch được hỗ trợ.

###### Embedding data to keywords

Khi viết các ví dụ cụ thể, việc có thể truyền dữ liệu thực tế vào các thực thi từ khóa là rất hữu ích. Điều này có thể được thực hiện bằng cách nhúng các tham số vào tên từ khóa.