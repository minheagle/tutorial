# Creating tasks

Ngoài việc tự động hóa kiểm thử, Robot Framework còn có thể được sử dụng cho các mục đích tự động hóa khác, bao gồm tự động hóa quy trình bằng robot (RPA). Điều này luôn có thể thực hiện được, nhưng Robot Framework 3.1 đã thêm hỗ trợ chính thức cho việc tự động hóa các tác vụ, không chỉ là kiểm thử. Về cơ bản, việc tạo tác vụ hoạt động giống như việc tạo kiểm thử và sự khác biệt thực sự duy nhất là ở thuật ngữ. Các tác vụ cũng có thể được tổ chức thành các bộ như các trường hợp kiểm thử.

## Task syntax


Các tác vụ được tạo ra dựa trên các từ khóa có sẵn giống như các trường hợp kiểm thử, và cú pháp của tác vụ về cơ bản giống với cú pháp của trường hợp kiểm thử. Sự khác biệt chính là các tác vụ được tạo ra trong các phần Tác vụ thay vì trong các phần Kiểm thử:

```robotframework
*** Tasks ***
Process invoice
    Read information from PDF
    Validate information
    Submit information to backend system
    Validate information is visible in web UI
```

Việc có cả kiểm thử và tác vụ trong cùng một tệp là một lỗi.

## Task related settings

Các cài đặt có thể được sử dụng trong phần tác vụ hoàn toàn giống với phần kiểm thử. Trong phần cài đặt, có thể sử dụng các cài đặt Task Setup, Task Teardown, Task Template và Task Timeout thay vì các biến thể kiểm thử của chúng.