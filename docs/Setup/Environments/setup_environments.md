# Cài đặt môi trường

## 1. Python

#### Kiểm tra

###### Windows 

* Mở terminal 

* Nhập vào lệnh sau:

```commandline
python --version 
```

###### Linux 

* Mở terminal 

* Nhập vào lệnh sau:

```commandline
python3 --version 
```

#### Cài đặt 

###### Windows

* Có thể tải Python từ Microsoft Store và nhập vào phiên bản mình mong muốn (Python 3.10, Python 3.11, Python 3.12, ...) 

* Nếu trên Microsoft Store không có phiên bản mong muốn thì có thể cài đặt thông qua [link](https://www.python.org/downloads/#:~:text=As%20of%20Python%203.11.4%20and%203.12.0b1%20(2023-05-23),%20release%20installer%20packages#:~:text=As%20of%20Python%203.11.4%20and%203.12.0b1%20(2023-05-23),%20release%20installer%20packages)

###### Linux

* Mở terminal và chạy lệnh sau: 

```commandline
sudo apt install python3
```

#### Tạo môi trường ảo trong python 

Môi trường ảo giúp cho chúng ta có thể cách ly các dự án với nhau để không bị xung đột giữa các thư viện 

* Mở terminal và di chuyển đến thư mục của dự án.

###### Windows

* Nhập vào các lệnh sau: 

```commandline
python -m venv venv 
```

```commandline
venv/Sources/activate 
```

###### Linux

* Nhập vào các lệnh sau:

```commandline
python3 -m venv venv 
```

```commandline
source venv/bin/activate 
```

## 2. NodeJS

#### Kiểm tra

```commandline
node --version 
```

#### Cài đặt 

* Truy cập vào [link](https://nodejs.org/en/download/prebuilt-installer/current) để tải xuống phiên bản mong muốn và theo hệ điều hành đang sử dụng

## 3. Java

#### Install

