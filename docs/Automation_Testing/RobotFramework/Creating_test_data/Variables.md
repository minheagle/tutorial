# Variables

## Introduction

Biến là một tính năng thiết yếu của Robot Framework và chúng có thể được sử dụng ở hầu hết mọi nơi trong dữ liệu kiểm tra. Thông thường, chúng được sử dụng trong các đối số cho các từ khóa trong phần Test Case và Keyword, nhưng tất cả các cài đặt cũng cho phép biến trong giá trị của chúng. Một tên từ khóa thông thường không thể được chỉ định bằng biến, nhưng từ khóa BuiltIn Run Keyword có thể được sử dụng để đạt được hiệu ứng tương tự.

Robot Framework có các biến riêng của nó có thể được sử dụng dưới dạng số vô hướng, danh sách hoặc từ điển bằng cách sử dụng cú pháp ${SCALAR}, @{LIST} và &{DICT}, tương ứng. Ngoài ra, các biến môi trường có thể được sử dụng trực tiếp với cú pháp %{ENV_VAR}.

Các biến rất hữu ích, ví dụ như trong các trường hợp sau:

* Khi các chuỗi thường xuyên thay đổi trong dữ liệu kiểm tra. Với các biến, bạn chỉ cần thực hiện những thay đổi này ở một nơi.

* Khi tạo dữ liệu kiểm tra không phụ thuộc vào hệ thống và hệ điều hành. Sử dụng biến thay vì chuỗi mã cứng giúp điều này dễ dàng hơn rất nhiều (ví dụ: ${RESOURCES} thay vì c:\resources, hoặc ${HOST} thay vì 10.0.0.1:8080). Bởi vì các biến có thể được thiết lập từ dòng lệnh khi bắt đầu các bài kiểm tra, việc thay đổi các biến phụ thuộc vào hệ thống rất dễ dàng (ví dụ: --variable HOST:10.0.0.2:1234 --variable RESOURCES:/opt/resources). Điều này cũng giúp kiểm thử định vị, thường liên quan đến việc chạy cùng một bài kiểm tra với các chuỗi khác nhau.

* Khi có nhu cầu có các đối tượng khác ngoài chuỗi làm đối số cho các từ khóa. Điều này là không thể nếu không có các biến.

* Khi các từ khóa khác nhau, thậm chí trong các thư viện kiểm tra khác nhau, cần giao tiếp. Bạn có thể gán giá trị trả về từ một từ khóa vào một biến và truyền nó như một đối số cho một từ khóa khác.

* Khi các giá trị trong dữ liệu kiểm tra dài hoặc phức tạp theo cách khác. Ví dụ, ${URL} ngắn hơn http://long.domain.name:8080/path/to/service?foo=1&bar=2&zap=42.

Nếu một biến không tồn tại được sử dụng trong dữ liệu kiểm tra, từ khóa sử dụng nó sẽ thất bại. Nếu cú pháp giống như được sử dụng cho các biến cần thiết như một chuỗi nguyên văn, nó phải được thoát bằng một dấu gạch chéo ngược như trong ${NAME}.

## Using variables

Phần này giải thích cách sử dụng các biến, bao gồm cú pháp biến số vô hướng thông thường ${var}, cách sử dụng biến trong các ngữ cảnh danh sách và từ điển như @{var} và &{var}, tương ứng, và cách sử dụng các biến môi trường như %{var}. Các cách khác nhau để tạo biến sẽ được thảo luận trong các phần tiếp theo.

Các biến trong Robot Framework, giống như các từ khóa, không phân biệt chữ hoa chữ thường, và cả khoảng trắng và dấu gạch dưới đều bị bỏ qua. Tuy nhiên, được khuyến nghị sử dụng chữ in hoa cho các biến toàn cục (ví dụ: ${PATH} hoặc ${TWO WORDS}) và chữ thường cho các biến cục bộ chỉ có sẵn trong một số trường hợp kiểm tra hoặc từ khóa người dùng (ví dụ: ${my var}). Quan trọng hơn nhiều, tuy nhiên, cần sử dụng kiểu chữ một cách nhất quán.

Tên biến bao gồm định danh kiểu biến ($, @, &, %), dấu ngoặc nhọn ({, }) và tên biến thực tế nằm giữa các dấu ngoặc nhọn. Không giống như một số ngôn ngữ lập trình mà cú pháp biến tương tự được sử dụng, dấu ngoặc nhọn luôn là bắt buộc. Tên biến cơ bản có thể chứa bất kỳ ký tự nào giữa các dấu ngoặc nhọn. Tuy nhiên, được khuyến nghị sử dụng chỉ các ký tự chữ cái từ a đến z, số, dấu gạch dưới và khoảng trắng, và thậm chí là yêu cầu để sử dụng cú pháp biến mở rộng.

#### Scalar variable syntax

Cách sử dụng phổ biến nhất các biến trong dữ liệu kiểm tra Robot Framework là sử dụng cú pháp biến số vô hướng như ${var}. Khi cú pháp này được sử dụng, tên biến sẽ được thay thế bằng giá trị của nó như là. Hầu hết thời gian, giá trị biến là chuỗi, nhưng các biến có thể chứa bất kỳ đối tượng nào, bao gồm số, danh sách, từ điển hoặc thậm chí các đối tượng tùy chỉnh.

Ví dụ dưới đây minh họa việc sử dụng các biến số vô hướng. Giả sử rằng các biến ${GREET} và ${NAME} có sẵn và được gán lần lượt cho các chuỗi Hello và world, thì cả hai trường hợp kiểm tra trong ví dụ đều tương đương.

```robotframework
*** Test Cases ***
Constants
    Log    Hello
    Log    Hello, world!!

Variables
    Log    ${GREET}
    Log    ${GREET}, ${NAME}!!
```

Khi một biến số vô hướng được sử dụng một mình mà không có bất kỳ văn bản hoặc biến nào khác xung quanh, như trong ${GREET} ở trên, biến này sẽ được thay thế bằng giá trị của nó nguyên trạng và giá trị có thể là bất kỳ đối tượng nào. Nếu biến không được sử dụng một mình, như trong ${GREER}, ${NAME}!! ở trên, giá trị của nó sẽ được chuyển đổi thành một chuỗi trước, sau đó được nối với các dữ liệu khác.

!!! Note 
    Giá trị biến được sử dụng nguyên trạng mà không cần chuyển đổi khi truyền tham số cho các từ khóa bằng cách sử dụng cú pháp tham số tên như argname=${var}.

Ví dụ dưới đây minh họa sự khác biệt giữa việc có một biến đứng riêng lẻ hoặc với nội dung khác. Đầu tiên, giả sử rằng chúng ta có một biến ${STR} được đặt thành chuỗi "Hello, world!" và ${OBJ} được đặt thành một thể hiện của đối tượng Python như sau:

```robotframework
class MyObj:

    def __str__():
        return "Hi, terra!"
```

Với hai biến này đã được thiết lập, chúng ta có dữ liệu kiểm tra sau:

```robotframework
*** Test Cases ***
Objects
    KW 1    ${STR}
    KW 2    ${OBJ}
    KW 3    I said "${STR}"
    KW 4    You said "${OBJ}"
```

Cuối cùng, khi dữ liệu kiểm tra này được thực thi, các từ khóa khác nhau sẽ nhận các đối số như sau:

* KW 1 nhận được một chuỗi: Hello, world!

* KW 2 nhận được một đối tượng được lưu trong biến ${OBJ}

* KW 3 nhận được một chuỗi: I said "Hello, world!"

* KW 4 nhận được một chuỗi: You said "Hi, terra!"

!!! Note 
    Việc chuyển đổi các biến sang Unicode rõ ràng sẽ thất bại nếu biến đó không thể được biểu diễn dưới dạng Unicode. Điều này có thể xảy ra, ví dụ, nếu bạn cố gắng sử dụng các chuỗi byte làm đối số cho các từ khóa bằng cách nối các giá trị lại với nhau như ${byte1}${byte2}. Một cách khắc phục là tạo một biến chứa toàn bộ giá trị và sử dụng nó một mình trong ô (ví dụ, ${bytes}) vì khi đó giá trị sẽ được sử dụng nguyên trạng.

#### List variable syntax

Khi một biến được sử dụng như một biến vô hướng như ${EXAMPLE}, giá trị của nó sẽ được sử dụng nguyên trạng. Nếu giá trị của biến là một danh sách hoặc giống như danh sách, cũng có thể sử dụng nó như một biến danh sách như @{EXAMPLE}. Trong trường hợp này, danh sách sẽ được mở rộng và các mục riêng lẻ sẽ được truyền vào dưới dạng các đối số riêng biệt. Điều này dễ dàng được giải thích bằng một ví dụ. Giả sử rằng một biến @{USER} có giá trị ['robot', 'secret'], hai trường hợp kiểm tra sau sẽ tương đương:

```robotframework
*** Test Cases ***
Constants
    Login    robot    secret

List Variable
    Login    @{USER}
```


Robot Framework lưu trữ các biến của mình trong một bộ nhớ nội bộ và cho phép sử dụng chúng dưới dạng vô hướng, danh sách hoặc từ điển. Việc sử dụng một biến như một danh sách yêu cầu giá trị của nó phải là một danh sách Python hoặc một đối tượng tương tự như danh sách. Robot Framework không cho phép sử dụng chuỗi như danh sách, nhưng các đối tượng có thể lặp lại khác như tuple hoặc từ điển thì được chấp nhận.

Bắt đầu từ Robot Framework 4.0, việc mở rộng danh sách có thể được sử dụng kết hợp với truy cập vào các mục trong danh sách, điều này cho phép những cách sử dụng sau:

```robotframework
*** Test Cases ***
Nested container
    ${nested} =    Evaluate    [['a', 'b', 'c'], {'key': ['x', 'y']}]
    Log Many    @{nested}[0]         # Logs 'a', 'b' and 'c'.
    Log Many    @{nested}[1][key]    # Logs 'x' and 'y'.

Slice
    ${items} =    Create List    first    second    third
    Log Many    @{items}[1:]         # Logs 'second' and  'third'.
```

###### Using list variables with other data

Có thể sử dụng biến danh sách với các đối số khác, bao gồm cả các biến danh sách khác.

```robotframework
*** Test Cases ***
Example
    Keyword    @{LIST}    more    args
    Keyword    ${SCALAR}    @{LIST}    constant
    Keyword    @{LIST}    @{ANOTHER}    @{ONE MORE}
```

###### Using list variables with settings

Các biến danh sách chỉ có thể được sử dụng với một số cài đặt nhất định. Chúng có thể được sử dụng làm đối số cho các thư viện đã nhập và tệp biến, nhưng tên của thư viện và tệp biến không thể là biến danh sách. Ngoài ra, trong các thiết lập và dọn dẹp, biến danh sách không thể được sử dụng làm tên của từ khóa, nhưng có thể được sử dụng trong các đối số. Đối với các cài đặt liên quan đến thẻ, chúng có thể được sử dụng tự do. Việc sử dụng các biến scala là có thể ở những nơi mà biến danh sách không được hỗ trợ.

```robotframework
*** Settings ***
Library         ExampleLibrary      @{LIB ARGS}    # This works
Library         ${LIBRARY}          @{LIB ARGS}    # This works
Library         @{LIBRARY AND ARGS}                # This does not work
Suite Setup     Some Keyword        @{KW ARGS}     # This works
Suite Setup     ${KEYWORD}          @{KW ARGS}     # This works
Suite Setup     @{KEYWORD AND ARGS}                # This does not work
Default Tags    @{TAGS}                            # This works
```

#### Dictionary variable syntax

Như đã đề cập ở trên, một biến chứa danh sách có thể được sử dụng như một biến danh sách để truyền các mục trong danh sách đến một từ khóa dưới dạng các đối số riêng biệt. Tương tự, một biến chứa từ điển Python hoặc một đối tượng giống như từ điển có thể được sử dụng như một biến từ điển như &{EXAMPLE}. Thực tế, điều này có nghĩa là từ điển sẽ được mở rộng và các mục riêng lẻ sẽ được truyền dưới dạng các đối số có tên đến từ khóa. Giả sử rằng một biến &{USER} có giá trị {'name': 'robot', 'password': 'secret'}, hai trường hợp thử nghiệm sau đây là tương đương.

```robotframework
*** Test Cases ***
Constants
    Login    name=robot    password=secret

Dict Variable
    Login    &{USER}
```

Bắt đầu từ Robot Framework 4.0, việc mở rộng từ điển có thể được sử dụng kết hợp với truy cập mục từ điển, cho phép các cách sử dụng như &{nested}[key] trở nên khả thi.

###### Using dictionary variables with other data

Có thể sử dụng các biến từ điển với các đối số khác, bao gồm cả các biến từ điển khác. Vì cú pháp đối số có tên yêu cầu các đối số vị trí phải đứng trước các đối số có tên, nên các từ điển chỉ có thể đứng trước các đối số có tên hoặc các từ điển khác.

```robotframework
*** Test Cases ***
Example
    Keyword    &{DICT}    named=arg
    Keyword    positional    @{LIST}    &{DICT}
    Keyword    &{DICT}    &{ANOTHER}    &{ONE MORE}
```

###### Using dictionary variables with settings

Các biến từ điển nói chung không thể được sử dụng với các cài đặt. Ngoại lệ duy nhất là các phần nhập khẩu, thiết lập và dọn dẹp, nơi mà các từ điển có thể được sử dụng làm đối số.

```robotframework
*** Settings ***
Library        ExampleLibrary    &{LIB ARGS}
Suite Setup    Some Keyword      &{KW ARGS}     named=arg
```

#### Accessing list and dictionary items

Có thể truy cập các mục của các biến có thể chỉ mục, chẳng hạn như danh sách và từ điển, bằng cách sử dụng cú pháp đặc biệt như ${var}[item] hoặc ${var}[nested][item]. Bắt đầu từ Robot Framework 4.0, cũng có thể sử dụng truy cập mục cùng với việc mở rộng danh sách và mở rộng từ điển bằng cách sử dụng cú pháp @{var}[item] và &{var}[item], tương ứng.

!!! Note 
    Trước Robot Framework 3.1, cú pháp truy cập mục thông thường là @{var}[item] với danh sách và &{var}[item] với từ điển. Robot Framework 3.1 đã giới thiệu cú pháp tổng quát ${var}[item] cùng với một số cải tiến khác, và cú pháp truy cập mục cũ đã bị gỡ bỏ trong Robot Framework 3.2.

###### Accessing sequence items

Có thể truy cập một mục nhất định của một biến chứa chuỗi (ví dụ: danh sách, chuỗi hoặc byte) bằng cú pháp ${var}[index], trong đó index là chỉ số của giá trị được chọn. Chỉ số bắt đầu từ 0, chỉ số âm có thể được sử dụng để truy cập các mục từ cuối, và việc cố gắng truy cập một mục với chỉ số quá lớn sẽ gây ra lỗi. Các chỉ số được tự động chuyển đổi thành số nguyên, và cũng có thể sử dụng các biến làm chỉ số.

```robotframework
*** Test Cases ***
Positive index
    Login    ${USER}[0]    ${USER}[1]
    Title Should Be    Welcome ${USER}[0]!

Negative index
    Keyword    ${SEQUENCE}[-1]

Index defined as variable
    Keyword    ${SEQUENCE}[${INDEX}]
```


Truy cập mục chuỗi cũng hỗ trợ chức năng "cắt" tương tự như Python với cú pháp ${var}[1:]. Với cú pháp này, bạn không nhận được một mục đơn lẻ mà nhận được một đoạn của chuỗi gốc. Tương tự như với Python, bạn có thể chỉ định chỉ số bắt đầu, chỉ số kết thúc và bước nhảy:

```robotframework
*** Test Cases ***
Start index
    Keyword    ${SEQUENCE}[1:]

End index
    Keyword    ${SEQUENCE}[:4]

Start and end
    Keyword    ${SEQUENCE}[2:-1]

Step
    Keyword    ${SEQUENCE}[::2]
    Keyword    ${SEQUENCE}[1:-1:10]
```

!!! Note 
    Cú pháp cắt được giới thiệu trong Robot Framework 3.1. Nó đã được mở rộng để hoạt động với việc mở rộng danh sách như @{var}[1:] trong Robot Framework 4.0.

!!! Note 
    Trước Robot Framework 3.2, việc truy cập mục và cắt chỉ được hỗ trợ với các biến chứa danh sách, tuple hoặc các đối tượng được coi là giống danh sách. Hiện nay, tất cả các chuỗi, bao gồm cả chuỗi ký tự (strings) và byte, đều được hỗ trợ.

###### Accessing individual dictionary items

Bạn có thể truy cập một giá trị cụ thể của biến từ điển bằng cú pháp ${NAME}[key], trong đó key là tên của giá trị được chọn. Các khóa (keys) được coi là chuỗi, nhưng có thể sử dụng các khóa không phải chuỗi dưới dạng biến. Các giá trị từ điển được truy cập theo cách này có thể được sử dụng tương tự như các biến kiểu scalar.

Nếu một khóa là chuỗi, bạn cũng có thể truy cập giá trị của nó bằng cú pháp truy cập thuộc tính ${NAME.key}. Xem thêm chi tiết về cú pháp này trong phần Tạo biến từ điển.

```robotframework
*** Test Cases ***
Dictionary variable item
    Login    ${USER}[name]    ${USER}[password]
    Title Should Be    Welcome ${USER}[name]!

Key defined as variable
    Log Many    ${DICT}[${KEY}]    ${DICT}[${42}]

Attribute access
    Login    ${USER.name}    ${USER.password}
    Title Should Be    Welcome ${USER.name}!
```

###### Nested item access

Các biến có thể lồng nhau cũng có thể được truy cập bằng cách sử dụng cùng một cú pháp truy cập phần tử như ${var}[item1][item2]. Điều này đặc biệt hữu ích khi làm việc với dữ liệu JSON thường được trả về bởi các dịch vụ REST. Ví dụ, nếu một biến ${DATA} chứa danh sách [{'id': 1, 'name': 'Robot'}, {'id': 2, 'name': 'Mr. X'}], các kiểm tra sau đây sẽ thành công:

```robotframework
*** Test Cases ***
Nested item access
    Should Be Equal    ${DATA}[0][name]    Robot
    Should Be Equal    ${DATA}[1][id]      ${2}
```

#### Environment variables

Robot Framework cho phép sử dụng các biến môi trường trong dữ liệu kiểm tra bằng cú pháp %{ENV_VAR_NAME}. Chúng chỉ giới hạn ở các giá trị chuỗi. Có thể chỉ định một giá trị mặc định, sẽ được sử dụng nếu biến môi trường không tồn tại, bằng cách tách tên biến và giá trị mặc định bằng dấu "=" như %{ENV_VAR_NAME=default value}.

Các biến môi trường được thiết lập trong hệ điều hành trước khi thực hiện kiểm tra có sẵn trong suốt quá trình thực hiện, và có thể tạo mới chúng bằng từ khóa Set Environment Variable hoặc xóa các biến hiện có bằng từ khóa Delete Environment Variable, cả hai đều có trong thư viện OperatingSystem. Vì các biến môi trường là toàn cục, các biến môi trường được thiết lập trong một trường hợp kiểm tra có thể được sử dụng trong các trường hợp kiểm tra khác thực hiện sau đó. Tuy nhiên, các thay đổi đối với các biến môi trường sẽ không có hiệu lực sau khi thực hiện kiểm tra.

```robotframework
*** Test Cases ***
Environment variables
    Log    Current user: %{USER}
    Run    %{JAVA_HOME}${/}javac

Environment variables with defaults
    Set port    %{APPLICATION_PORT=8080}
```

!!! Note 
    Hỗ trợ việc chỉ định giá trị mặc định là tính năng mới được giới thiệu trong Robot Framework 3.2.

## Creating variables

Các biến có thể được tạo ra từ nhiều nguồn khác nhau.

#### Variable section

Nguồn phổ biến nhất cho các biến là các phần biến trong các tệp suite và tệp tài nguyên. Các phần biến rất tiện lợi vì chúng cho phép tạo ra các biến ở cùng một nơi với phần còn lại của dữ liệu kiểm tra, và cú pháp cần thiết rất đơn giản. Tuy nhiên, nhược điểm chính của chúng là giá trị luôn là chuỗi và không thể được tạo ra một cách động. Nếu bất kỳ điều nào trong số này là một vấn đề, thì có thể sử dụng các tệp biến thay thế.

###### Creating scalar variables

Cách gán biến đơn giản nhất có thể là gán một chuỗi vào một biến vô hướng. Điều này được thực hiện bằng cách đặt tên biến (bao gồm cả ${}) ở cột đầu tiên của phần Biến và giá trị ở cột thứ hai. Nếu cột thứ hai để trống, một chuỗi rỗng sẽ được đặt làm giá trị. Ngoài ra, một biến đã được định nghĩa trước đó cũng có thể được sử dụng trong giá trị.

```robotframework
*** Variables ***
${NAME}         Robot Framework
${VERSION}      2.0
${ROBOT}        ${NAME} ${VERSION}
```

Cũng có thể sử dụng dấu "=" sau tên biến, nhưng điều này không bắt buộc, để việc gán biến trở nên rõ ràng hơn một chút.

```robotframework
*** Variables ***
${NAME} =       Robot Framework
${VERSION} =    2.0
```

Nếu một biến scalar có giá trị dài, nó có thể được chia thành nhiều hàng bằng cách sử dụng cú pháp .... Theo mặc định, các hàng sẽ được nối với nhau bằng một khoảng trắng, nhưng điều này có thể được thay đổi bằng cách sử dụng tùy chọn cấu hình having separator sau giá trị cuối cùng.

```robotframework
*** Variables ***
${EXAMPLE}      This value is joined
...             together with a space.
${MULTILINE}    First line.
...             Second line.
...             Third line.
...             separator=\n
```

Tùy chọn separator là mới trong Robot Framework 7.0, nhưng các phiên bản cũ hơn cũng hỗ trợ việc cấu hình dấu phân cách. Với chúng, giá trị đầu tiên có thể chứa một dấu hiệu đặc biệt SEPARATOR.

```robotframework
*** Variables ***
${MULTILINE}    SEPARATOR=\n
...             First line.
...             Second line.
...             Third line.
```

Cả tùy chọn separator và dấu hiệu SEPARATOR đều phân biệt chữ hoa chữ thường. Việc sử dụng tùy chọn separator được khuyến nghị, trừ khi cần hỗ trợ các phiên bản cũ hơn.

###### Creating list variables

Việc tạo các biến danh sách cũng dễ dàng như việc tạo các biến vô hướng. Một lần nữa, tên biến nằm ở cột đầu tiên của phần Biến và các giá trị nằm ở các cột tiếp theo. Một biến danh sách có thể có bất kỳ số lượng giá trị nào, bắt đầu từ số không, và nếu cần nhiều giá trị, chúng có thể được chia thành nhiều hàng.

```robotframework
*** Variables ***
@{NAMES}        Matti       Teppo
@{NAMES2}       @{NAMES}    Seppo
@{NOTHING}
@{MANY}         one         two      three      four
...             five        six      seven
```

###### Creating dictionary variables

Các biến từ điển có thể được tạo trong phần Biến tương tự như các biến danh sách. Sự khác biệt là các mục cần được tạo bằng cú pháp name=value hoặc các biến từ điển hiện có. Nếu có nhiều mục có cùng tên, giá trị cuối cùng sẽ có ưu tiên. Nếu một tên chứa dấu "=" (dấu bằng) nguyên văn, nó có thể được thoát bằng cách sử dụng dấu gạch chéo ngược như =.

```robotframework
*** Variables ***
&{USER 1}       name=Matti    address=xxx         phone=123
&{USER 2}       name=Teppo    address=yyy         phone=456
&{MANY}         first=1       second=${2}         ${3}=third
&{EVEN MORE}    &{MANY}       first=override      empty=
...             =empty        key\=here=value
```

Các biến từ điển có hai thuộc tính bổ sung so với các từ điển Python bình thường. Đầu tiên, các giá trị của những từ điển này có thể được truy cập như các thuộc tính, nghĩa là có thể sử dụng cú pháp biến mở rộng như ${VAR.key}. Điều này chỉ hoạt động nếu khóa là một tên thuộc tính hợp lệ và không trùng với bất kỳ thuộc tính bình thường nào mà các từ điển Python có. Ví dụ, giá trị cá nhân &{USER}[name] cũng có thể được truy cập như ${USER.name} (chú ý rằng $ là cần thiết trong ngữ cảnh này), nhưng việc sử dụng ${MANY.3} là không khả thi.

!!! Tip 
    Với các biến từ điển lồng nhau, các khóa có thể được truy cập như ${VAR.nested.key}. Điều này giúp việc làm việc với các cấu trúc dữ liệu lồng nhau trở nên dễ dàng hơn.

Một đặc điểm đặc biệt khác của các biến từ điển là chúng có thứ tự. Điều này có nghĩa là nếu các từ điển này được lặp qua, các mục của chúng luôn xuất hiện theo thứ tự mà chúng được định nghĩa. Điều này có thể hữu ích nếu các từ điển được sử dụng như các biến danh sách với các vòng lặp FOR hoặc trong các tình huống khác. Khi một từ điển được sử dụng như một biến danh sách, giá trị thực tế chứa các khóa của từ điển. Ví dụ, biến @{MANY} sẽ có giá trị là ['first', 'second', 3].

###### Creating variable name based on another variable

Bắt đầu từ Robot Framework 7.0, có thể tạo tên biến một cách động dựa trên một biến khác.

```robotframework
*** Variables ***
${X}        Y
${${X}}     Z    # Name is created based on '${X}'.

*** Test Cases ***
Dynamically created name
    Should Be Equal    ${Y}    Z
```

#### Variable file

Các tệp biến là cơ chế mạnh mẽ nhất để tạo ra các loại biến khác nhau. Có thể gán biến cho bất kỳ đối tượng nào bằng cách sử dụng chúng, và chúng cũng cho phép tạo biến một cách động. Cú pháp tệp biến và cách sử dụng các tệp biến được giải thích trong phần Tệp tài nguyên và biến.

#### Setting variables in command line

Các biến có thể được thiết lập từ dòng lệnh, hoặc là từng cái một với tùy chọn --variable (-v) hoặc bằng cách sử dụng một tệp biến với tùy chọn --variablefile (-V). Các biến được thiết lập từ dòng lệnh có sẵn toàn cầu cho tất cả các tệp dữ liệu thử nghiệm đã được thực thi, và chúng cũng ghi đè lên các biến có cùng tên trong phần Biến và trong các tệp biến được nhập trong dữ liệu thử nghiệm.

Cú pháp để thiết lập các biến cá nhân là --variable name:value, trong đó name là tên của biến không có ${} và value là giá trị của nó. Nhiều biến có thể được thiết lập bằng cách sử dụng tùy chọn này nhiều lần. Chỉ có thể thiết lập các biến vô hướng bằng cú pháp này và chúng chỉ có thể nhận giá trị chuỗi.

```
--variable EXAMPLE:value
--variable HOST:localhost:7272 --variable USER:robot
```

Trong các ví dụ trên, các biến được thiết lập như sau:

* ${EXAMPLE} nhận giá trị value

* ${HOST} và ${USER} nhận các giá trị localhost:7272 và robot

Cú pháp cơ bản để sử dụng các tệp biến từ dòng lệnh là --variablefile path/to/variables.py, và phần "Sử dụng tệp biến" có nhiều chi tiết hơn. Các biến thực sự được tạo ra phụ thuộc vào các biến có trong tệp biến được tham chiếu.

Nếu cả tệp biến và các biến cá nhân được chỉ định từ dòng lệnh, các biến cá nhân sẽ có độ ưu tiên cao hơn.

#### Return values from keywords

Giá trị trả về từ các từ khóa cũng có thể được gán vào các biến. Điều này cho phép giao tiếp giữa các từ khóa khác nhau ngay cả trong các thư viện kiểm thử khác nhau.

Các biến được thiết lập theo cách này về cơ bản giống như bất kỳ biến nào khác, nhưng chúng chỉ có sẵn trong phạm vi cục bộ nơi chúng được tạo ra. Do đó, không thể, ví dụ, gán một biến như vậy trong một trường hợp kiểm thử và sử dụng nó trong một trường hợp khác. Điều này là do, nhìn chung, các trường hợp kiểm thử tự động không nên phụ thuộc vào nhau, và việc vô tình thiết lập một biến được sử dụng ở nơi khác có thể gây ra những lỗi khó gỡ lỗi. Nếu có nhu cầu thực sự để thiết lập một biến trong một trường hợp kiểm thử và sử dụng nó trong một trường hợp khác, có thể sử dụng các từ khóa BuiltIn như được giải thích trong phần tiếp theo.

###### Assigning scalar variables

Bất kỳ giá trị nào được trả về bởi một từ khóa đều có thể được gán cho một biến kiểu scalar. Như được minh họa trong ví dụ dưới đây, cú pháp cần thiết rất đơn giản:

```robotframework
*** Test Cases ***
Returning
    ${x} =    Get X    an argument
    Log    We got ${x}!
```


Trong ví dụ trên, giá trị được trả về bởi từ khóa Get X trước tiên được gán vào biến ${x} và sau đó được sử dụng bởi từ khóa Log. Việc có dấu "=" sau tên biến là không bắt buộc, nhưng nó giúp việc gán biến trở nên rõ ràng hơn. Việc tạo ra các biến cục bộ như thế này hoạt động cả ở cấp độ test case và cấp độ user keyword.

Lưu ý rằng mặc dù một giá trị được gán cho một biến kiểu scalar, nó vẫn có thể được sử dụng như một biến kiểu list nếu nó có giá trị giống như danh sách và như một biến kiểu dictionary nếu nó có giá trị giống như từ điển.

```robotframework
*** Test Cases ***
Example
    ${list} =    Create List    first    second    third
    Length Should Be    ${list}    3
    Log Many    @{list}
```

###### Assigning variables with item values

Bắt đầu từ Robot Framework 6.1, khi làm việc với các biến hỗ trợ gán mục như danh sách hoặc từ điển, có thể thiết lập giá trị của chúng bằng cách chỉ định chỉ số hoặc khóa của mục bằng cách sử dụng cú pháp ${var}[item], trong đó phần item có thể chứa một biến:

```robotframework
*** Test Cases ***
Item assignment to list
    ${list} =          Create List      one    two    three    four
    ${list}[0] =       Set Variable     first
    ${list}[${1}] =    Set Variable     second
    ${list}[2:3] =     Evaluate         ['third']
    ${list}[-1] =      Set Variable     last
    Log Many           @{list}          # Logs 'first', 'second', 'third' and 'last'

Item assignment to dictionary
    ${dict} =                Create Dictionary    first_name=unknown
    ${dict}[first_name] =    Set Variable         John
    ${dict}[last_name] =     Set Variable         Doe
    Log                      ${dictionary}        # Logs {'first_name': 'John', 'last_name': 'Doe'}
```

###### Creating variable name based on another variable

Bắt đầu từ Robot Framework 7.0, có thể tạo tên của biến được gán một cách động dựa trên một biến khác:

```robotframework
*** Test Cases ***
Dynamically created name
    ${x} =    Set Variable    y
    ${${x}} =    Set Variable    z    # Name is created based on '${x}'.
    Should Be Equal    ${y}    z
```

###### Assigning list variables

Nếu một từ khóa trả về một danh sách hoặc bất kỳ đối tượng nào giống danh sách, có thể gán nó cho một biến danh sách:

```robotframework
*** Test Cases ***
Example
    @{list} =    Create List    first    second    third
    Length Should Be    ${list}    3
    Log Many    @{list}
```

Bởi vì tất cả các biến trong Robot Framework đều được lưu trữ trong cùng một không gian tên, không có nhiều sự khác biệt giữa việc gán giá trị cho một biến vô hướng (scalar) và một biến danh sách. Điều này có thể thấy rõ khi so sánh hai ví dụ cuối cùng ở trên. Sự khác biệt chính là khi tạo một biến danh sách, Robot Framework tự động xác minh rằng giá trị đó là một danh sách hoặc giống danh sách, và giá trị biến được lưu trữ sẽ là một danh sách mới được tạo từ giá trị trả về. Trong khi đó, khi gán cho một biến vô hướng, giá trị trả về sẽ không được xác minh và giá trị được lưu trữ sẽ là chính đối tượng mà được trả về.

###### Assigning dictionary variables

Nếu một từ khóa (keyword) trả về một từ điển (dictionary) hoặc bất kỳ đối tượng nào giống như từ điển, bạn có thể gán nó vào một biến từ điển.

```robotframework
*** Test Cases ***
Example
    &{dict} =    Create Dictionary    first=1    second=${2}    ${3}=third
    Length Should Be    ${dict}    3
    Do Something    &{dict}
    Log    ${dict.first}
```

Vì tất cả các biến trong Robot Framework đều được lưu trữ trong cùng một không gian tên (namespace), nên cũng có thể gán một từ điển vào một biến scalar và sử dụng nó sau này như một từ điển khi cần. Tuy nhiên, có một số lợi ích thực sự trong việc tạo một biến từ điển một cách rõ ràng.

Trước tiên, Robot Framework xác minh rằng giá trị trả về là một từ điển hoặc giống như từ điển, tương tự như cách nó xác minh rằng các biến danh sách chỉ có thể nhận giá trị giống như danh sách.

Lợi ích lớn hơn là giá trị được chuyển đổi thành một từ điển đặc biệt mà nó cũng sử dụng khi tạo các biến từ điển trong phần Biến (Variable section). Các giá trị trong các từ điển này có thể được truy cập bằng cách sử dụng cú pháp truy cập thuộc tính như ${dict.first} trong ví dụ trên. Những từ điển này cũng được sắp xếp, nhưng nếu từ điển gốc không được sắp xếp, thứ tự kết quả sẽ là ngẫu nhiên.

###### Assigning multiple variables

Nếu một keyword trả về một danh sách hoặc một đối tượng giống như danh sách, bạn có thể gán các giá trị cá nhân vào nhiều biến scalar hoặc vào các biến scalar và một biến danh sách.

```robotframework
*** Test Cases ***
Assign multiple
    ${a}    ${b}    ${c} =    Get Three
    ${first}    @{rest} =    Get Three
    @{before}    ${last} =    Get Three
    ${begin}    @{middle}    ${end} =    Get Three
```


Giả sử rằng keyword Get Three trả về một danh sách [1, 2, 3], các biến sau sẽ được tạo ra:

* ${a}, ${b} và ${c} có giá trị lần lượt là 1, 2 và 3.

* ${first} có giá trị là 1, và @{rest} có giá trị là [2, 3].

* @{before} có giá trị là [1, 2] và ${last} có giá trị là 3.

* ${begin} có giá trị là 1, @{middle} có giá trị là [2] và ${end} có giá trị là 3.

Sẽ xảy ra lỗi nếu danh sách trả về có nhiều hoặc ít giá trị hơn số biến scalar để gán. Thêm vào đó, chỉ cho phép một biến danh sách và các biến dictionary chỉ có thể được gán riêng lẻ.

###### Automatically logging assigned variable value

Để dễ hiểu hơn về những gì xảy ra trong quá trình thực thi, giá trị bắt đầu được gán sẽ tự động được ghi lại. Mặc định là hiển thị 200 ký tự đầu tiên, nhưng điều này có thể được thay đổi bằng cách sử dụng tùy chọn dòng lệnh --maxassignlength khi chạy các bài kiểm tra. Nếu giá trị là 0 hoặc âm, toàn bộ giá trị được gán sẽ bị ẩn.

```
--maxassignlength 1000
--maxassignlength 0
```

Lý do giá trị không được ghi lại hoàn toàn là vì nó có thể rất lớn. Nếu bạn luôn muốn thấy một giá trị nhất định một cách đầy đủ, bạn có thể sử dụng từ khóa Log của thư viện BuiltIn để ghi lại nó sau khi thực hiện gán.

!!! Note 
    Tùy chọn --maxassignlength là một tính năng mới trong Robot Framework 5.0.

#### VAR syntax

Bắt đầu từ Robot Framework 7.0, có thể tạo biến bên trong các bài kiểm tra và các từ khóa người dùng bằng cách sử dụng cú pháp VAR. Đánh dấu VAR phân biệt chữ hoa chữ thường và phải được theo sau bởi một tên biến và giá trị. Ngoài VAR bắt buộc, cú pháp tổng thể chủ yếu giống như khi tạo biến trong phần Biến.

Cú pháp mới này nhằm mục đích làm cho việc tạo biến trở nên đơn giản và đồng nhất hơn. Nó đặc biệt được thiết kế để thay thế các từ khóa BuiltIn như Set Variable, Set Test Variable, Set Suite Variable và Set Global Variable, nhưng cũng có thể được sử dụng thay thế cho Catenate, Create List và Create Dictionary.

###### Creating scalar variables

Trong các trường hợp đơn giản, các biến số được tạo ra chỉ bằng cách đưa ra tên biến và giá trị của nó. Giá trị có thể là một chuỗi cố định hoặc có thể chứa một biến khác. Nếu giá trị dài, có thể chia nó thành nhiều cột và hàng. Trong trường hợp đó, các phần sẽ được kết nối với nhau bằng một khoảng trắng theo mặc định, nhưng có thể chỉ định dấu phân cách cần sử dụng bằng tùy chọn cấu hình separator. Có thể có một dấu "=" tùy chọn sau tên biến theo cách tương tự như khi tạo các biến dựa trên giá trị trả về từ các từ khóa và trong phần Biến.

```robotframework
*** Test Cases ***
Scalar examples
     VAR    ${simple}       variable
     VAR    ${equals} =     this works too
     VAR    ${variable}     value contains ${simple}
     VAR    ${sentence}     This is a bit longer variable value
     ...                    that is split into multiple rows.
     ...                    These parts are joined with a space.
     VAR    ${multiline}    This is another longer value.
     ...                    This time there is a custom separator.
     ...                    As the result this becomes a multiline string.
     ...                    separator=\n
```

###### Creating list and dictionary variables

Các biến danh sách và từ điển được tạo ra tương tự như các biến số. Khi tạo từ điển, các mục phải được chỉ định bằng cú pháp name=value.

```robotframework
*** Test Cases ***
List examples
     VAR    @{two items}     Robot    Framework
     VAR    @{empty list}
     VAR    @{lot of stuff}
     ...    first item
     ...    second item
     ...    third item
     ...    fourth item
     ...    last item

Dictionary examples
     VAR    &{two items}     name=Robot Framework    url=http://robotframework.org
     VAR    &{empty dict}
     VAR    &{lot of stuff}
     ...    first=1
     ...    second=2
     ...    third=3
     ...    fourth=4
     ...    last=5
```

###### Scope

Các biến được tạo bằng cú pháp VAR chỉ khả dụng trong test hoặc user keyword nơi chúng được tạo ra. Tuy nhiên, điều này có thể được thay đổi bằng cách sử dụng tùy chọn cấu hình phạm vi. Các giá trị được hỗ trợ bao gồm:

* **LOCAL**: Giúp biến khả dụng trong phạm vi cục bộ hiện tại. Đây là giá trị mặc định.

* **TEST**: Giúp biến khả dụng trong test hiện tại. Điều này bao gồm tất cả các keywords được gọi bởi test.

* **TASK**: Bí danh cho TEST có thể được sử dụng khi tạo các task.

* **SUITE**: Giúp biến khả dụng trong suite hiện tại. Điều này bao gồm tất cả các test tiếp theo trong suite đó, nhưng không bao gồm các test trong các child suite có thể có.

* **SUITES**: Giúp biến khả dụng trong suite hiện tại và trong các child suite của nó. (Mới trong Robot Framework 7.1).

* **GLOBAL**: Giúp biến khả dụng toàn cầu. Điều này bao gồm tất cả các keywords và tests tiếp theo.

```robotframework
*** Variables ***
${SUITE}         this value is overridden

*** Test Cases ***
Scope example
    VAR    ${local}     local value
    VAR    ${TEST}      test value            scope=TEST
    VAR    ${SUITE}     suite value           scope=SUITE
    VAR    ${SUITES}    nested suite value    scope=SUITES
    VAR    ${GLOBAL}    global value          scope=GLOBAL
    Should Be Equal    ${local}     local value
    Should Be Equal    ${TEST}      test value
    Should Be Equal    ${SUITE}     suite value
    Should Be Equal    ${SUITES}    nested suite value
    Should Be Equal    ${GLOBAL}    global value
    Keyword
    Should Be Equal    ${TEST}      new test value
    Should Be Equal    ${SUITE}     new suite value
    Should Be Equal    ${SUITES}    new nested suite value
    Should Be Equal    ${GLOBAL}    new global value

Scope example, part 2
    Should Be Equal    ${SUITE}     new suite value
    Should Be Equal    ${SUITES}    new nested suite value
    Should Be Equal    ${GLOBAL}    new global value

*** Keywords ***
Keyword
    Should Be Equal    ${TEST}      test value
    Should Be Equal    ${SUITE}     suite value
    Should Be Equal    ${SUITES}    nested suite value
    Should Be Equal    ${GLOBAL}    global value
    VAR    ${TEST}      new ${TEST}      scope=TEST
    VAR    ${SUITE}     new ${SUITE}     scope=SUITE
    VAR    ${SUITES}    new ${SUITES}    scope=SUITES
    VAR    ${GLOBAL}    new ${GLOBAL}    scope=GLOBAL
    Should Be Equal    ${TEST}      new test value
    Should Be Equal    ${SUITE}     new suite value
    Should Be Equal    ${SUITES}    new nested suite value
    Should Be Equal    ${GLOBAL}    new global value
```

Mặc dù các biến Robot Framework không phân biệt chữ hoa chữ thường, nhưng được khuyến nghị sử dụng chữ hoa cho các tên biến không phải cục bộ.

###### Creating variables conditionally

Cú pháp VAR hoạt động với các cấu trúc IF/ELSE, giúp việc tạo biến theo điều kiện trở nên dễ dàng. Trong những trường hợp đơn giản, việc sử dụng IF inline có thể thuận tiện.

```robotframework
*** Test Cases ***
IF/ELSE example
    IF    "${ENV}" == "devel"
        VAR    ${address}    127.0.0.1
        VAR    ${name}       demo
    ELSE
        VAR    ${address}    192.168.1.42
        VAR    ${name}       robot
    END

Inline IF
    IF    "${ENV}" == "devel"    VAR    ${name}    demo    ELSE    VAR    ${name}    robot
```

###### Creating variable name based on another variable

Nếu cần, tên biến cũng có thể được tạo ra một cách động dựa trên một biến khác.

```robotframework
*** Test Cases ***
Dynamic name
    VAR    ${x}       y    # Normal assignment.
    VAR    ${${x}}    z    # Name created dynamically.
    Should Be Equal    ${y}    z
```

#### Using Set Test/Suite/Global Variable keywords

!!! Note 
    Cú pháp VAR được khuyến nghị hơn các từ khóa này khi sử dụng Robot Framework phiên bản 7.0 hoặc mới hơn.

Thư viện BuiltIn có các từ khóa Set Test Variable, Set Suite Variable và Set Global Variable, có thể được sử dụng để thiết lập biến một cách động trong quá trình thực thi bài kiểm tra. Nếu một biến đã tồn tại trong phạm vi mới, giá trị của nó sẽ bị ghi đè, và nếu không, một biến mới sẽ được tạo ra.

Biến được thiết lập bằng từ khóa Set Test Variable có sẵn ở mọi nơi trong phạm vi của trường hợp kiểm tra hiện tại. Ví dụ, nếu bạn thiết lập một biến trong một từ khóa người dùng, nó sẽ có sẵn cả ở cấp độ trường hợp kiểm tra và cũng trong tất cả các từ khóa người dùng khác được sử dụng trong bài kiểm tra hiện tại. Các trường hợp kiểm tra khác sẽ không thấy các biến được thiết lập bằng từ khóa này. Gọi Set Test Variable bên ngoài phạm vi của một bài kiểm tra (ví dụ: trong Suite Setup hoặc Teardown) sẽ gây ra lỗi.

Biến được thiết lập bằng từ khóa Set Suite Variable có sẵn ở mọi nơi trong phạm vi của bộ kiểm tra hiện tại. Thiết lập biến bằng từ khóa này sẽ có tác dụng tương tự như việc tạo ra chúng trong phần Variable trong tệp dữ liệu kiểm tra hoặc nhập từ các tệp biến. Các bộ kiểm tra khác, bao gồm các bộ kiểm tra con, sẽ không thấy các biến được thiết lập bằng từ khóa này.

Biến được thiết lập bằng từ khóa Set Global Variable có sẵn toàn cầu trong tất cả các trường hợp kiểm tra và bộ kiểm tra được thực thi sau khi thiết lập chúng. Thiết lập biến bằng từ khóa này sẽ có tác dụng tương tự như việc tạo từ dòng lệnh bằng cách sử dụng các tùy chọn --variable hoặc --variablefile. Bởi vì từ khóa này có thể thay đổi biến ở mọi nơi, nó nên được sử dụng một cách cẩn thận.

!!! Note 
    Các từ khóa Set Test Variable, Set Suite Variable, và Set Global Variable thiết lập các biến có tên trực tiếp vào phạm vi biến của kiểm tra, bộ hoặc toàn cầu và không trả về giá trị gì. Mặt khác, từ khóa BuiltIn khác là Set Variable thiết lập các biến cục bộ bằng cách sử dụng các giá trị trả về.

## Built-in variables

Robot Framework cung cấp một số biến tích hợp sẵn có sẵn tự động.

#### Operating-system variables

Các biến tích hợp sẵn liên quan đến hệ điều hành giúp làm cho dữ liệu kiểm tra không phụ thuộc vào hệ điều hành.

| Variable   | Explanation                                                                                                          |
|------------|----------------------------------------------------------------------------------------------------------------------|
| ${CURDIR}  | An absolute path to the directory where the test data file is located. This variable is case-sensitive.             |
| ${TEMPDIR} | An absolute path to the system temporary directory. In UNIX-like systems, this is typically /tmp, and in Windows, c:\Documents and Settings\<user>\Local Settings\Temp. |
| ${EXECDIR} | An absolute path to the directory where test execution was started from.                                           |
| ${/}       | The system directory path separator. / in UNIX-like systems and \ in Windows.                                     |
| ${:}       | The system path element separator. : in UNIX-like systems and ; in Windows.                                       |
| ${\n}      | The system line separator. \n in UNIX-like systems and \r\n in Windows.                                           |

```robotframework
*** Test Cases ***
Example
    Create Binary File    ${CURDIR}${/}input.data    Some text here${\n}on two lines
    Set Environment Variable    CLASSPATH    ${TEMPDIR}${:}${CURDIR}${/}foo.jar
```

#### Number variables

Cú pháp biến có thể được sử dụng để tạo cả số nguyên và số thực, như được minh họa trong ví dụ dưới đây. Điều này rất hữu ích khi một từ khóa mong đợi nhận một số thực tế, chứ không phải một chuỗi chỉ trông giống như một số, dưới dạng đối số.

```robotframework
*** Test Cases ***
Example 1A
    Connect    example.com    80       # Connect gets two strings as arguments

Example 1B
    Connect    example.com    ${80}    # Connect gets a string and an integer

Example 2
    Do X    ${3.14}    ${-1e-4}        # Do X gets floating point numbers 3.14 and -0.0001
```

Có thể tạo ra số nguyên từ các giá trị nhị phân, bát phân và thập lục phân bằng cách sử dụng các tiền tố lần lượt là 0b, 0o và 0x. Cú pháp này không phân biệt chữ hoa chữ thường.

```robotframework
*** Test Cases ***
Example
    Should Be Equal    ${0b1011}    ${11}
    Should Be Equal    ${0o10}      ${8}
    Should Be Equal    ${0xff}      ${255}
    Should Be Equal    ${0B1010}    ${0XA}
```

#### Boolean and None/null variables

Ngoài ra, các giá trị Boolean và Python None cũng có thể được tạo ra bằng cách sử dụng cú pháp biến tương tự như các số.

```robotframework
*** Test Cases ***
Boolean
    Set Status    ${true}               # Set Status gets Boolean true as an argument
    Create Y    something   ${false}    # Create Y gets a string and Boolean false

None
    Do XYZ    ${None}                   # Do XYZ gets Python None as an argument
```

Các biến này không phân biệt chữ hoa chữ thường, vì vậy, chẳng hạn, ${True} và ${true} là tương đương nhau.

#### Space and empty variables

Có thể tạo ra khoảng trắng và chuỗi rỗng bằng cách sử dụng các biến ${SPACE} và ${EMPTY}, tương ứng. Các biến này rất hữu ích, chẳng hạn, khi sẽ cần phải thoát các khoảng trắng hoặc các ô rỗng bằng một dấu gạch chéo. Nếu cần nhiều hơn một khoảng trắng, có thể sử dụng cú pháp biến mở rộng như ${SPACE * 5}. Trong ví dụ sau, từ khóa Should Be Equal nhận các tham số giống hệt nhau, nhưng những tham số sử dụng biến thì dễ hiểu hơn so với những tham số sử dụng dấu gạch chéo.

```robotframework
*** Test Cases ***
One space
    Should Be Equal    ${SPACE}          \ \

Four spaces
    Should Be Equal    ${SPACE * 4}      \ \ \ \ \

Ten spaces
    Should Be Equal    ${SPACE * 10}     \ \ \ \ \ \ \ \ \ \ \

Quoted space
    Should Be Equal    "${SPACE}"        " "

Quoted spaces
    Should Be Equal    "${SPACE * 2}"    " \ "

Empty
    Should Be Equal    ${EMPTY}          \
```

Cũng có một biến danh sách rỗng @{EMPTY} và một biến từ điển rỗng &{EMPTY}. Vì chúng không có nội dung, nên chúng gần như biến mất khi được sử dụng ở đâu đó trong dữ liệu kiểm tra. Chúng hữu ích, chẳng hạn, trong các mẫu kiểm tra khi từ khóa mẫu được sử dụng mà không có đối số hoặc khi ghi đè các biến danh sách hoặc từ điển trong các phạm vi khác nhau. Việc sửa đổi giá trị của @{EMPTY} hoặc &{EMPTY} là không thể.

```robotframework
*** Test Cases ***
Template
    [Template]    Some keyword
    @{EMPTY}

Override
    Set Global Variable    @{LIST}    @{EMPTY}
    Set Suite Variable     &{DICT}    &{EMPTY}
```

!!! Note 
    ${SPACE} đại diện cho khoảng trắng ASCII (\x20) và các khoảng trắng khác nên được chỉ định bằng cách sử dụng các chuỗi thoát như \xA0 (NO-BREAK SPACE) và \u3000 (IDEOGRAPHIC SPACE).

#### Automatic variables

Một số biến tự động cũng có thể được sử dụng trong dữ liệu kiểm tra. Những biến này có thể có các giá trị khác nhau trong quá trình thực thi bài kiểm tra và một số biến trong số đó thậm chí không có sẵn mọi lúc. Việc thay đổi giá trị của những biến này không ảnh hưởng đến các giá trị gốc, nhưng một số giá trị có thể được thay đổi động bằng cách sử dụng các từ khóa từ thư viện BuiltIn.

| Variable                          | Explanation                                                                                                                                                   | Available           |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|
| ${TEST NAME}                      | The name of the current test case.                                                                                                                          | Test case           |
| @{TEST TAGS}                      | Contains the tags of the current test case in alphabetical order. Can be modified dynamically using Set Tags and Remove Tags keywords.                      | Test case           |
| ${TEST DOCUMENTATION}             | The documentation of the current test case. Can be set dynamically using Set Test Documentation keyword.                                                    | Test case           |
| ${TEST STATUS}                    | The status of the current test case, either PASS or FAIL.                                                                                                   | Test teardown        |
| ${TEST MESSAGE}                   | The message of the current test case.                                                                                                                       | Test teardown        |
| ${PREV TEST NAME}                 | The name of the previous test case, or an empty string if no tests have been executed yet.                                                                   | Everywhere           |
| ${PREV TEST STATUS}               | The status of the previous test case: either PASS, FAIL, or an empty string when no tests have been executed.                                               | Everywhere           |
| ${PREV TEST MESSAGE}              | The possible error message of the previous test case.                                                                                                       | Everywhere           |
| ${SUITE NAME}                     | The full name of the current test suite.                                                                                                                    | Everywhere           |
| ${SUITE SOURCE}                   | An absolute path to the suite file or directory.                                                                                                            | Everywhere           |
| ${SUITE DOCUMENTATION}            | The documentation of the current test suite. Can be set dynamically using Set Suite Documentation keyword.                                                  | Everywhere           |
| &{SUITE METADATA}                 | The free metadata of the current test suite. Can be set using Set Suite Metadata keyword.                                                                   | Everywhere           |
| ${SUITE STATUS}                   | The status of the current test suite, either PASS or FAIL.                                                                                                  | Suite teardown       |
| ${SUITE MESSAGE}                  | The full message of the current test suite, including statistics.                                                                                            | Suite teardown       |
| ${KEYWORD STATUS}                 | The status of the current keyword, either PASS or FAIL.                                                                                                     | User keyword teardown |
| ${KEYWORD MESSAGE}                | The possible error message of the current keyword.                                                                                                          | User keyword teardown |
| ${LOG LEVEL}                      | Current log level.                                                                                                                                          | Everywhere           |
| ${OUTPUT DIR}                     | An absolute path to the output directory as a string.                                                                                                       | Everywhere           |
| ${OUTPUT FILE}                    | An absolute path to the output file as a string or a string NONE if the output file is not created.                                                        | Everywhere           |
| ${LOG FILE}                       | An absolute path to the log file as a string or a string NONE if the log file is not created.                                                              | Everywhere           |
| ${REPORT FILE}                    | An absolute path to the report file as a string or a string NONE if the report file is not created.                                                        | Everywhere           |
| ${DEBUG FILE}                     | An absolute path to the debug file as a string or a string NONE if the debug file is not created.                                                          | Everywhere           |
| &{OPTIONS}                        | A dictionary exposing command line options. The dictionary keys match the command line options and can be accessed both like ${OPTIONS}[key] and ${OPTIONS.key}. Available options: <br> ${OPTIONS.exclude} (--exclude) <br> ${OPTIONS.include} (--include) <br> ${OPTIONS.skip} (--skip) <br> ${OPTIONS.skip_on_failure} (--skip-on-failure) <br> ${OPTIONS.console_width} (--console-width) <br> ${OPTIONS} itself was added in RF 5.0 and ${OPTIONS.console_width} in RF 7.1. More options can be exposed later. | Everywhere           |

Các biến liên quan đến suite như ${SUITE SOURCE}, ${SUITE NAME}, ${SUITE DOCUMENTATION} và &{SUITE METADATA}, cũng như các tùy chọn liên quan đến các tùy chọn dòng lệnh như ${LOG FILE} và &{OPTIONS}, đã có sẵn ngay khi các thư viện và tệp biến được nhập khẩu. Tuy nhiên, các biến có thể trong những biến tự động này vẫn chưa được giải quyết vào thời điểm nhập khẩu.

## Variable priorities and scopes

Các biến đến từ các nguồn khác nhau có ưu tiên khác nhau và có sẵn trong các phạm vi khác nhau.

#### Variable priorities

* **Các biến từ dòng lệnh**:

    * Các biến được thiết lập trong dòng lệnh có ưu tiên cao nhất trong số tất cả các biến có thể được thiết lập trước khi thực hiện thử nghiệm thực tế. Chúng ghi đè lên các biến có thể được tạo trong các phần Biến trong các tệp trường hợp thử nghiệm, cũng như trong các tệp tài nguyên và biến được nhập trong dữ liệu thử nghiệm.

    * Các biến được thiết lập riêng lẻ (tùy chọn --variable) ghi đè lên các biến được thiết lập bằng cách sử dụng các tệp biến (--variablefile). Nếu bạn chỉ định cùng một biến cá nhân nhiều lần, biến được chỉ định sau cùng sẽ ghi đè lên các biến trước đó. Điều này cho phép thiết lập các giá trị mặc định cho các biến trong một kịch bản khởi động và ghi đè chúng từ dòng lệnh. Tuy nhiên, hãy lưu ý rằng nếu nhiều tệp biến có cùng một biến, thì các biến trong tệp được chỉ định đầu tiên có ưu tiên cao nhất.

* **Phần Biến trong tệp trường hợp thử nghiệm**:

    * Các biến được tạo bằng cách sử dụng phần Biến trong một tệp trường hợp thử nghiệm có sẵn cho tất cả các trường hợp thử nghiệm trong tệp đó. Những biến này ghi đè lên các biến có cùng tên trong các tệp tài nguyên và biến đã nhập.

    * Các biến được tạo trong phần Biến có sẵn trong tất cả các phần khác trong tệp mà chúng được tạo ra. Điều này có nghĩa là chúng cũng có thể được sử dụng trong phần Cài đặt, chẳng hạn, để nhập thêm biến từ các tệp tài nguyên và biến.

* **Các tệp tài nguyên và biến được nhập**:

    * Các biến được nhập từ các tệp tài nguyên và biến có ưu tiên thấp nhất trong số tất cả các biến được tạo trong dữ liệu thử nghiệm. Các biến từ các tệp tài nguyên và tệp biến có cùng ưu tiên. Nếu một số tệp tài nguyên và/hoặc tệp biến có cùng các biến, thì những biến trong tệp được nhập đầu tiên sẽ được sử dụng.

    * Nếu một tệp tài nguyên nhập các tệp tài nguyên hoặc tệp biến, các biến trong phần Biến của nó có ưu tiên cao hơn các biến mà nó nhập. Tất cả các biến này có sẵn cho các tệp nhập tệp tài nguyên này.

    * Lưu ý rằng các biến được nhập từ các tệp tài nguyên và tệp biến không có sẵn trong phần Biến của tệp nhập chúng. Điều này là do phần Biến được xử lý trước phần Cài đặt, nơi các tệp tài nguyên và biến được nhập.

* **Các biến được thiết lập trong quá trình thử nghiệm**:

    * Các biến được thiết lập trong quá trình thử nghiệm, cho dù bằng cách sử dụng các giá trị trả về từ các từ khóa hoặc bằng cách sử dụng các từ khóa Set Test/Suite/Global Variable, luôn ghi đè lên các biến hiện có trong phạm vi mà chúng được thiết lập. Về một khía cạnh, chúng có ưu tiên cao nhất, nhưng mặt khác, chúng không ảnh hưởng đến các biến bên ngoài phạm vi mà chúng được định nghĩa.

* **Các biến tích hợp**:

    * Các biến tích hợp như ${TEMPDIR} và ${TEST_NAME} có ưu tiên cao nhất trong số tất cả các biến. Chúng không thể bị ghi đè bằng cách sử dụng phần Biến hoặc từ dòng lệnh, nhưng thậm chí chúng có thể được đặt lại trong quá trình thử nghiệm. Một ngoại lệ cho quy tắc này là các biến số, được giải quyết một cách động nếu không tìm thấy biến nào khác. Do đó, chúng có thể bị ghi đè, nhưng điều đó thường không phải là ý tưởng hay. Ngoài ra, ${CURDIR} là đặc biệt vì nó đã được thay thế ngay trong thời gian xử lý dữ liệu thử nghiệm.

#### Variable scopes

Tùy thuộc vào nơi và cách chúng được tạo ra, các biến có thể có phạm vi toàn cục, phạm vi bộ kiểm tra, phạm vi trường hợp kiểm tra hoặc phạm vi cục bộ.

* **Phạm vi toàn cục**:

    * Các biến toàn cục có sẵn ở mọi nơi trong dữ liệu thử nghiệm. Những biến này thường được thiết lập từ dòng lệnh với các tùy chọn --variable và --variablefile, nhưng cũng có thể tạo ra các biến toàn cục mới hoặc thay đổi các biến hiện có bằng cách sử dụng cú pháp VAR hoặc từ khóa Set Global Variable ở bất kỳ đâu trong dữ liệu thử nghiệm. Ngoài ra, các biến tích hợp cũng là toàn cục.

    * Khuyến cáo nên sử dụng chữ hoa với tất cả các biến toàn cục.

* **Phạm vi bộ kiểm tra**:

    * Các biến có phạm vi bộ kiểm tra có sẵn ở bất kỳ đâu trong bộ kiểm tra nơi chúng được định nghĩa hoặc nhập khẩu. Chúng có thể được tạo ra trong các phần Biến, được nhập từ các tệp tài nguyên và tệp biến, hoặc được thiết lập trong quá trình kiểm tra bằng cách sử dụng cú pháp VAR hoặc từ khóa Set Suite Variable.

    * Phạm vi bộ kiểm tra không mang tính đệ quy, điều này có nghĩa là các biến có sẵn trong bộ kiểm tra cấp cao hơn sẽ không có sẵn trong các bộ cấp thấp hơn. Nếu cần thiết, các tệp tài nguyên và tệp biến có thể được sử dụng để chia sẻ các biến.

    * Vì những biến này có thể được coi là toàn cục trong bộ kiểm tra mà chúng được sử dụng, nên cũng khuyến cáo nên sử dụng chữ hoa với chúng.

* **Phạm vi trường hợp kiểm tra**:

    * Các biến có phạm vi trường hợp kiểm tra có thể được nhìn thấy trong một trường hợp kiểm tra và trong tất cả các từ khóa người dùng mà trường hợp kiểm tra sử dụng. Ban đầu, không có biến nào trong phạm vi này, nhưng có thể tạo ra chúng bằng cách sử dụng cú pháp VAR hoặc từ khóa Set Test Variable ở bất kỳ đâu trong một trường hợp kiểm tra. Cố gắng tạo biến kiểm tra trong thiết lập bộ hoặc hủy thiết lập bộ sẽ gây ra lỗi.

    * Ngoài ra, các biến trong phạm vi trường hợp kiểm tra cũng có phần nào đó mang tính toàn cục. Do đó, thường khuyến cáo nên sử dụng chữ hoa với chúng.

* **Phạm vi cục bộ**:

    * Các trường hợp kiểm tra và từ khóa người dùng có một phạm vi biến cục bộ mà không được thấy bởi các kiểm tra hoặc từ khóa khác. Các biến cục bộ có thể được tạo ra bằng cách sử dụng các giá trị trả về từ các từ khóa đã thực thi và với cú pháp VAR, và các từ khóa người dùng cũng nhận chúng dưới dạng tham số.

    * Khuyến cáo nên sử dụng chữ thường với các biến cục bộ.

## Advanced variable features

#### Extended variable syntax

Cú pháp biến mở rộng cho phép truy cập các thuộc tính của một đối tượng được gán cho một biến (ví dụ, ${object.attribute}) và thậm chí gọi các phương thức của nó (ví dụ, ${obj.getName()}). Nó hoạt động với cả biến số nguyên và biến danh sách, nhưng chủ yếu hữu ích với các biến số.

Cú pháp biến mở rộng là một tính năng mạnh mẽ, nhưng cần được sử dụng một cách cẩn thận. Việc truy cập các thuộc tính thường không phải là vấn đề, ngược lại, vì một biến chứa một đối tượng với nhiều thuộc tính thường tốt hơn việc có nhiều biến. Mặt khác, việc gọi các phương thức, đặc biệt khi chúng được sử dụng với các tham số, có thể làm cho dữ liệu kiểm tra trở nên phức tạp hơn để hiểu. Nếu điều đó xảy ra, nên di chuyển mã vào một thư viện kiểm tra.

Các trường hợp sử dụng phổ biến nhất của cú pháp biến mở rộng được minh họa trong ví dụ dưới đây. Trước tiên, giả sử rằng chúng ta có tệp biến và trường hợp kiểm tra sau:

```robotframework
class MyObject:

    def __init__(self, name):
        self.name = name

    def eat(self, what):
        return '%s eats %s' % (self.name, what)

    def __str__(self):
        return self.name

OBJECT = MyObject('Robot')
DICTIONARY = {1: 'one', 2: 'two', 3: 'three'}
```

```robotframework
*** Test Cases ***
Example
    KW 1    ${OBJECT.name}
    KW 2    ${OBJECT.eat('Cucumber')}
    KW 3    ${DICTIONARY[2]}
```

Khi dữ liệu kiểm tra này được thực hiện, các từ khóa nhận các đối số như đã giải thích dưới đây:

* KW 1 nhận chuỗi "Robot".

* KW 2 nhận chuỗi "Robot eats Cucumber".

* KW 3 nhận chuỗi "two".

Cú pháp biến mở rộng được đánh giá theo thứ tự sau:

1. Biến được tìm kiếm bằng tên biến đầy đủ. Cú pháp biến mở rộng chỉ được đánh giá nếu không tìm thấy biến nào khớp.

2. Tên của biến cơ sở được tạo ra. Nội dung của tên bao gồm tất cả các ký tự sau dấu mở { cho đến lần xuất hiện đầu tiên của một ký tự không phải chữ cái hoặc không phải số. Ví dụ, các biến cơ sở của ${OBJECT.name} và ${DICTIONARY[2]} lần lượt là OBJECT và DICTIONARY.

3. Một biến khớp với nội dung được tìm kiếm. Nếu không có khớp nào, một ngoại lệ được ném ra và trường hợp kiểm tra sẽ thất bại.

4. Biểu thức bên trong dấu ngoặc nhọn được đánh giá như một biểu thức Python, do đó tên biến cơ sở được thay thế bằng giá trị của nó. Nếu việc đánh giá thất bại do cú pháp không hợp lệ hoặc thuộc tính được truy vấn không tồn tại, một ngoại lệ được ném ra và kiểm tra sẽ thất bại.

5. Toàn bộ biến mở rộng được thay thế bằng giá trị trả về từ việc đánh giá.

Nhiều đối tượng Python chuẩn, bao gồm chuỗi và số, có các phương thức có thể được sử dụng với cú pháp biến mở rộng, cả theo cách rõ ràng hoặc ngầm hiểu. Đôi khi điều này có thể rất hữu ích và giảm bớt nhu cầu thiết lập các biến tạm thời, nhưng cũng dễ dàng lạm dụng nó và tạo ra dữ liệu kiểm tra thực sự khó hiểu. Các ví dụ sau đây cho thấy một số cách sử dụng khá tốt.

```robotframework
*** Test Cases ***
String
    ${string} =    Set Variable    abc
    Log    ${string.upper()}      # Logs 'ABC'
    Log    ${string * 2}          # Logs 'abcabc'

Number
    ${number} =    Set Variable    ${-2}
    Log    ${number * 10}         # Logs -20
    Log    ${number.__abs__()}    # Logs 2
```

Lưu ý rằng mặc dù abs(number) được khuyến nghị hơn number.__abs__() trong mã Python bình thường, việc sử dụng ${abs(number)} sẽ không hoạt động. Điều này là do tên biến phải nằm ở đầu cú pháp mở rộng. Việc sử dụng các phương thức __xxx__ trong dữ liệu kiểm tra như thế này đã có chút đáng ngờ, và thường thì tốt hơn là chuyển loại logic này vào các thư viện kiểm tra.

Cú pháp biến mở rộng cũng hoạt động trong bối cảnh biến danh sách. Nếu, ví dụ, một đối tượng được gán cho biến ${EXTENDED} có thuộc tính attribute chứa một danh sách dưới dạng giá trị, nó có thể được sử dụng như một biến danh sách @{EXTENDED.attribute}.

#### Extended variable assignment

Có thể thiết lập các thuộc tính của các đối tượng được lưu trữ vào các biến vô hướng bằng cách sử dụng giá trị trả về từ từ khóa và một biến thể của cú pháp biến mở rộng. Giả sử chúng ta có biến ${OBJECT} từ các ví dụ trước, các thuộc tính có thể được thiết lập cho nó như trong ví dụ bên dưới.

```robotframework
*** Test Cases ***
Example
    ${OBJECT.name} =    Set Variable    New name
    ${OBJECT.new_attr} =    Set Variable    New attribute
```

Cú pháp gán biến mở rộng được đánh giá theo các quy tắc sau:

1. Biến được gán phải là biến vô hướng và có ít nhất một dấu chấm. Nếu không, cú pháp gán mở rộng sẽ không được sử dụng và biến sẽ được gán theo cách thông thường.

2. Nếu tồn tại một biến với tên đầy đủ (ví dụ: ${OBJECT.name} trong ví dụ trên), biến đó sẽ được gán một giá trị mới và cú pháp mở rộng sẽ không được sử dụng.

3. Tên của biến cơ sở được tạo. Phần thân của tên bao gồm tất cả các ký tự giữa dấu mở ${ và dấu chấm cuối cùng, ví dụ: OBJECT trong ${OBJECT.name} và foo.bar trong ${foo.bar.zap}. Như ví dụ thứ hai minh họa, tên cơ sở có thể chứa cú pháp biến mở rộng bình thường.

4. Tên của thuộc tính để thiết lập được tạo bằng cách lấy tất cả các ký tự giữa dấu chấm cuối cùng và dấu đóng }, ví dụ: name trong ${OBJECT.name}. Nếu tên không bắt đầu bằng một chữ cái hoặc dấu gạch dưới và chỉ chứa các ký tự này cùng với số, thuộc tính được coi là không hợp lệ và cú pháp mở rộng sẽ không được sử dụng. Thay vào đó, một biến mới với tên đầy đủ sẽ được tạo ra.

5. Tìm kiếm một biến phù hợp với tên cơ sở. Nếu không tìm thấy biến, cú pháp mở rộng sẽ không được sử dụng và thay vào đó, một biến mới sẽ được tạo ra bằng cách sử dụng tên biến đầy đủ.

6. Nếu biến tìm thấy là một chuỗi hoặc một số, cú pháp mở rộng sẽ bị bỏ qua và một biến mới sẽ được tạo ra bằng tên đầy đủ. Điều này được thực hiện vì bạn không thể thêm thuộc tính mới vào các chuỗi hoặc số Python, và theo cách này, cú pháp mới cũng ít gây ra sự không tương thích ngược.

7. Nếu tất cả các quy tắc trước đó khớp, thuộc tính sẽ được thiết lập cho biến cơ sở. Nếu việc thiết lập gặp lỗi vì bất kỳ lý do gì, một ngoại lệ sẽ được ném ra và bài kiểm tra sẽ thất bại.

!!! Note
    Khác với việc gán biến theo cách thông thường bằng cách sử dụng giá trị trả về từ các từ khóa, các thay đổi đối với biến được thực hiện bằng cú pháp gán mở rộng không bị giới hạn trong phạm vi hiện tại. Bởi vì không có biến mới nào được tạo ra mà thay vào đó trạng thái của một biến hiện có được thay đổi, tất cả các bài kiểm tra và từ khóa thấy biến đó cũng sẽ thấy các thay đổi.

#### Variables inside variables

Các biến cũng được phép nằm bên trong các biến khác, và khi cú pháp này được sử dụng, các biến sẽ được giải quyết từ trong ra ngoài. Ví dụ, nếu bạn có một biến ${var${x}} thì ${x} sẽ được giải quyết trước. Nếu ${x} có giá trị là name, thì giá trị cuối cùng sẽ là giá trị của biến ${varname}. Có thể có nhiều biến lồng nhau, nhưng việc giải quyết biến bên ngoài cùng sẽ thất bại nếu bất kỳ biến nào trong số đó không tồn tại.

Trong ví dụ dưới đây, Do X nhận giá trị ${JOHN HOME} hoặc ${JANE HOME}, tùy thuộc vào việc Get Name trả về john hay jane. Nếu nó trả về một giá trị khác, việc giải quyết ${${name} HOME} sẽ thất bại.

```robotframework
*** Variables ***
${JOHN HOME}    /home/john
${JANE HOME}    /home/jane

*** Test Cases ***
Example
    ${name} =    Get Name
    Do X    ${${name} HOME}
```

#### Inline Python evaluation

Cú pháp biến cũng có thể được sử dụng để đánh giá các biểu thức Python. Cú pháp cơ bản là ${{expression}}, tức là có hai dấu ngoặc nhọn xung quanh biểu thức. Biểu thức có thể là bất kỳ biểu thức Python hợp lệ nào, chẳng hạn như ${{1 + 2}} hoặc ${{['a', 'list']}}. Các khoảng trắng xung quanh biểu thức được phép, vì vậy cả ${{ 1 + 2 }} và ${{ ['a', 'list'] }} đều hợp lệ. Ngoài việc sử dụng các biến kiểu scalar bình thường, các biến kiểu danh sách và biến kiểu từ điển cũng hỗ trợ cú pháp @{{expression}} và &{{expression}} tương ứng.

Các mục đích chính cho chức năng khá nâng cao này là:

* Đánh giá các biểu thức Python liên quan đến các biến của Robot Framework (${{len('${var}') > 3}}, ${{$var[0] if $var is not None else None}}).

* Tạo ra các giá trị không phải kiểu cơ bản của Python (${{decimal.Decimal('0.11')}}, ${{datetime.date(2019, 11, 5)}}).

* Tạo ra các giá trị một cách động (${{random.randint(0, 100)}}, ${{datetime.date.today()}}).

* Xây dựng các tập hợp, đặc biệt là các tập hợp lồng nhau (${{[1, 2, 3, 4]}}, ${{ {'id': 1, 'name': 'Example', 'children': [7, 9]} }}).

* Truy cập các hằng số và thuộc tính hữu ích khác trong các mô-đun Python (${{math.pi}}, ${{platform.system()}}).

Chức năng này tương tự như cú pháp biến mở rộng đã được thảo luận trước đó. Như các ví dụ trên minh họa, cú pháp này còn mạnh mẽ hơn vì nó cung cấp quyền truy cập vào các hàm tích hợp của Python như len() và các mô-đun như math. Ngoài việc có thể sử dụng các biến như ${var} trong các biểu thức (chúng được thay thế trước khi đánh giá), các biến cũng có sẵn thông qua cú pháp đặc biệt $var trong quá trình đánh giá. Toàn bộ cú pháp biểu thức được giải thích trong phụ lục Đánh giá biểu thức.

!!! Note 
    Thay vì tạo ra các biểu thức phức tạp, thường thì tốt hơn là di chuyển logic vào một thư viện tùy chỉnh. Điều này giúp dễ dàng bảo trì, làm cho dữ liệu kiểm tra dễ hiểu hơn và cũng có thể cải thiện tốc độ thực thi.

!!! Note 
    Cú pháp đánh giá Python nội tuyến là mới trong Robot Framework 3.2.