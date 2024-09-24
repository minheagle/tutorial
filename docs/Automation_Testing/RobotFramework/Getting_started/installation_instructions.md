# Cài đặt 

## Cài đặt Python 

Robot Framework được triển khai bằng Python, và điều kiện tiên quyết để cài đặt nó là cần có Python hoặc phiên bản thay thế PyPy được cài đặt. Một điều kiện tiên quyết được khuyến nghị khác là có sẵn trình quản lý gói pip.

Robot Framework yêu cầu Python 3.8 trở lên. Phiên bản mới nhất hỗ trợ Python 3.6 và 3.7 là Robot Framework 6.1.1. Nếu bạn cần sử dụng Python 2, Jython hoặc IronPython, bạn có thể sử dụng Robot Framework 4.1.3.

#### Cài đặt Python trên Linux

Trên Linux, bạn nên có sẵn bản cài đặt Python phù hợp với pip. Nếu không, bạn cần tham khảo tài liệu phân phối của mình để biết cách cài đặt. Điều này cũng đúng nếu bạn muốn sử dụng phiên bản Python khác ngoài phiên bản mặc định được cung cấp bởi hệ thống.

Để kiểm tra phiên bản Python bạn đã cài đặt, bạn có thể chạy lệnh python --version trong terminal:

```
$ python --version
Python 3.10.13
```

Lưu ý rằng nếu hệ thống của bạn cũng cung cấp Python 2 cũ hơn, chạy lệnh python có thể sử dụng Python 2. Để sử dụng Python 3, bạn có thể dùng lệnh python3 hoặc thậm chí lệnh cụ thể hơn như python3.8. Bạn cần sử dụng các biến thể chỉ định phiên bản cụ thể này nếu bạn có nhiều phiên bản Python 3 được cài đặt và cần xác định chính xác phiên bản nào sẽ sử dụng:

```
$ python3.11 --version
Python 3.11.7
$ python3.12 --version
Python 3.12.1
```

Cài đặt Robot Framework trực tiếp dưới Python hệ thống cung cấp có nguy cơ gây ra các sự cố có thể ảnh hưởng đến toàn bộ cài đặt Python mà hệ điều hành cũng sử dụng. Ngày nay, các bản phân phối Linux thường sử dụng phương pháp cài đặt theo người dùng mặc định để tránh các vấn đề như vậy, nhưng người dùng cũng có thể quyết định sử dụng môi trường ảo (virtual environments) để kiểm soát tốt hơn.

#### Cài đặt Python trên Windows

Trên Windows, Python không có sẵn theo mặc định, nhưng việc cài đặt rất dễ dàng. Cách được khuyến nghị để cài đặt Python là sử dụng trình cài đặt chính thức từ trang web python.org. Đối với các phương pháp thay thế khác, như cài đặt từ Microsoft Store, bạn có thể tham khảo tài liệu chính thức của Python.

Khi cài đặt Python trên Windows, bạn nên thêm Python vào PATH để dễ dàng chạy Python cũng như các công cụ như pip và Robot Framework từ dòng lệnh. Khi sử dụng trình cài đặt chính thức, chỉ cần chọn hộp kiểm **Add Python 3.x to PATH** trong hộp thoại đầu tiên.

Để đảm bảo cài đặt Python thành công và Python đã được thêm vào PATH, bạn có thể mở Command Prompt và chạy lệnh python --version:

```
C:\>python --version
Python 3.10.9
```

Nếu bạn cài đặt nhiều phiên bản Python trên Windows, phiên bản được sử dụng khi chạy lệnh python là phiên bản được đặt đầu tiên trong PATH. Nếu bạn cần sử dụng phiên bản khác, cách dễ nhất là dùng trình khởi chạy py:

```
C:\>py --version
Python 3.10.9
C:\>py -3.12 --version
Python 3.12.1
```

#### Cài đặt Python trên macOS

macOS không cung cấp phiên bản Python 3 tương thích theo mặc định, vì vậy cần cài đặt riêng. Phương pháp khuyến nghị là sử dụng trình cài đặt chính thức cho macOS từ trang web python.org. Nếu bạn sử dụng trình quản lý gói như Homebrew, bạn cũng có thể cài đặt Python thông qua nó.

Bạn có thể kiểm tra cài đặt Python trên macOS bằng cách chạy lệnh <code>python --version</code> giống như trên các hệ điều hành khác.

#### Cài đặt PyPy

**PyPy** là một triển khai thay thế của Python. Ưu điểm chính của PyPy so với Python chuẩn là nó có thể nhanh hơn và sử dụng ít bộ nhớ hơn, nhưng điều này phụ thuộc vào ngữ cảnh và cách sử dụng. Nếu tốc độ thực thi là quan trọng, thì thử nghiệm với PyPy là một ý tưởng tốt.

Việc cài đặt PyPy rất đơn giản và bạn có thể tìm thấy trình cài đặt cùng hướng dẫn cài đặt tại pypy.org. Để kiểm tra cài đặt PyPy thành công, hãy chạy lệnh pypy --version hoặc pypy3 --version.

> Lưu ý
> 
> Việc sử dụng Robot Framework với PyPy chỉ được hỗ trợ chính thức trên Linux.

#### Cấu hình PATH

Biến môi trường PATH liệt kê các thư mục mà hệ thống tìm kiếm các lệnh được thực thi. Để dễ dàng sử dụng Python, pip và Robot Framework từ dòng lệnh, bạn nên thêm thư mục cài đặt Python cũng như thư mục chứa các lệnh như pip và robot vào PATH.

Khi sử dụng Python trên Linux hoặc macOS, Python và các công cụ được cài đặt cùng nó thường tự động nằm trong PATH. Nếu bạn cần cập nhật PATH, bạn thường phải chỉnh sửa một tệp cấu hình toàn hệ thống hoặc tệp cấu hình riêng cho người dùng. Tệp nào cần chỉnh sửa và cách làm phụ thuộc vào hệ điều hành, và bạn cần tham khảo tài liệu của nó để biết thêm chi tiết.

Cách sửa đổi PATH trên Windows
Cách dễ nhất để đảm bảo PATH được cấu hình chính xác trên Windows là chọn hộp kiểm **Add Python 3.x to PATH** khi chạy trình cài đặt. Nếu bạn muốn chỉnh sửa PATH thủ công trên Windows, làm theo các bước sau:

1. Tìm Environment Variables trong Settings. Có các biến ảnh hưởng đến toàn hệ thống và các biến ảnh hưởng chỉ đến người dùng hiện tại. Việc sửa đổi các biến hệ thống sẽ yêu cầu quyền quản trị viên, nhưng việc sửa đổi biến của người dùng là đủ trong hầu hết các trường hợp.

2. Chọn PATH (thường được viết là Path) và nhấp Edit. Nếu bạn đang chỉnh sửa biến người dùng và PATH không tồn tại, nhấp New.

3. Thêm cả thư mục cài đặt Python và thư mục Scripts nằm dưới thư mục cài đặt vào PATH.

4. Thoát hộp thoại với Ok để lưu thay đổi.

5. Khởi động lại Command Prompt để thay đổi có hiệu lực.

## Cài đặt bằng pip

Hướng dẫn này bao gồm việc cài đặt Robot Framework bằng **pip**, trình quản lý gói chuẩn của Python. Nếu bạn đang sử dụng trình quản lý gói khác như **Conda**, bạn có thể sử dụng nó, nhưng cần tham khảo tài liệu hướng dẫn của nó.

Khi cài đặt Python, bạn thường sẽ có **pip** tự động được cài đặt. Nếu không, bạn cần kiểm tra tài liệu hướng dẫn của phiên bản Python đó để biết cách cài đặt **pip** riêng.

#### Sử dụng lệnh pip

Thông thường bạn sử dụng pip bằng cách chạy lệnh **pip**, nhưng trên Linux bạn có thể cần sử dụng **pip3** hoặc phiên bản cụ thể hơn như **pip3.8**. Khi chạy pip hoặc các biến thể của nó, phiên bản pip đầu tiên được tìm thấy trong **PATH** sẽ được sử dụng. Nếu bạn có nhiều phiên bản Python cài đặt, bạn có thể chỉ định phiên bản cụ thể bạn muốn sử dụng. Cách dễ nhất là chạy lệnh <code>python -m pip</code>, thay thế <code>python</code> bằng phiên bản Python mà bạn muốn sử dụng.

Để đảm bảo pip có sẵn, bạn có thể chạy lệnh <code>pip --version</code> hoặc tương đương.

#### Ví dụ trên Linux:

```
$ pip --version
pip 23.2.1 from ... (python 3.10)
$ python3.12 -m pip --version
pip 23.3.1 from ... (python 3.12)
```

#### Ví dụ trên Windows:

```
C:\> pip --version
pip 23.2.1 from ... (python 3.10)
C:\> py -m 3.12 -m pip --version
pip 23.3.2 from ... (python 3.12)
```

Trong các phần sau, pip sẽ luôn được chạy bằng lệnh pip. Bạn có thể cần sử dụng một số cách khác như đã giải thích ở trên tùy thuộc vào môi trường của bạn.

#### Cài đặt và gỡ cài đặt Robot Framework

Cách dễ nhất để sử dụng pip là để nó tự động tìm và tải xuống các gói từ Python Package Index (PyPI), nhưng nó cũng có thể cài đặt các gói đã tải xuống riêng từ PyPI. Các trường hợp sử dụng phổ biến nhất được liệt kê dưới đây, và tài liệu của pip có thêm nhiều thông tin và ví dụ.

* Cài đặt phiên bản mới nhất (không nâng cấp):

```commandline
pip install robotframework
```

* Nâng cấp lên phiên bản ổn định mới nhất:

```commandline
pip install --upgrade robotframework
```

* Nâng cấp lên phiên bản mới nhất ngay cả khi là bản phát hành trước:

```commandline
pip install --upgrade --pre robotframework
```

* Cài đặt một phiên bản cụ thể:

```
pip install robotframework==7.0
```

Cài đặt gói đã tải về riêng (không cần kết nối mạng):

```commandline
pip install robotframework-7.0-py3-none-any.whl
```

Cài đặt mã mới nhất (có thể chưa phát hành) trực tiếp từ GitHub:

```commandline
pip install https://github.com/robotframework/robotframework/archive/master.zip
```

Gỡ cài đặt:

```commandline
pip uninstall robotframework
```

## Cài đặt từ mã nguồn

Một phương án cài đặt khác là tải mã nguồn của **Robot Framework** và cài đặt nó bằng tập lệnh <code>setup.py</code>. Cách tiếp cận này chỉ được khuyến nghị nếu bạn không thể sử dụng pip vì một lý do nào đó.

Bạn có thể tải mã nguồn bằng cách tải xuống gói phân phối nguồn (source distribution) dưới dạng tệp zip từ PyPI và giải nén nó. Một lựa chọn khác là cloning (nhân bản) kho lưu trữ từ GitHub và kiểm tra nhãn phát hành cần thiết.

Sau khi bạn đã có mã nguồn, bạn có thể cài đặt nó bằng lệnh sau:

```commandline
python setup.py install
```

Tập lệnh setup.py chấp nhận nhiều tham số cho phép, chẳng hạn như cài đặt vào một vị trí không mặc định, không yêu cầu quyền quản trị viên. Tập lệnh này cũng được sử dụng để tạo các gói phân phối khác nhau. Để biết thêm chi tiết, bạn có thể chạy:

```commandline
python setup.py --help
```

## Xác minh cài đặt

Để đảm bảo rằng Robot Framework đã được cài đặt đúng phiên bản, bạn có thể chạy lệnh sau:

```
$ robot --version
Robot Framework 7.0 (Python 3.10.3 on linux)
```

Nếu lệnh này không chạy và hiển thị thông báo lỗi như **command not found** hoặc **not recognized**, bước đầu tiên là kiểm tra lại cấu hình **PATH**.

Nếu bạn đã cài đặt **Robot Framework** trên nhiều phiên bản Python, lệnh robot sẽ chạy phiên bản xuất hiện đầu tiên trong **PATH**. Để chọn rõ ràng phiên bản Python nào sẽ sử dụng, bạn có thể chạy:

```
$ python3.12 -m robot --version
Robot Framework 7.0 (Python 3.12.1 on linux)
```

Trên Windows, bạn có thể sử dụng py launcher:

```
C:\>py -3.11 -m robot --version
Robot Framework 7.0 (Python 3.11.7 on win32)
```

## Môi trường ảo

**Môi trường ảo của Python** cho phép cài đặt các gói Python trong một vị trí cô lập cho từng hệ thống hoặc ứng dụng, thay vì cài đặt tất cả các gói vào cùng một vị trí toàn cục. Có hai trường hợp sử dụng chính:

1. **Cài đặt các gói cần thiết cho từng dự án vào các môi trường riêng biệt**. Điều này giúp tránh xung đột nếu các dự án cần các phiên bản khác nhau của cùng một gói.

2. **Tránh cài đặt tất cả vào cài đặt Python toàn cục**. Điều này đặc biệt quan trọng trên Linux, nơi cài đặt Python toàn cục có thể được hệ điều hành sử dụng. Việc làm rối cài đặt Python toàn cục có thể gây ra các vấn đề nghiêm trọng.