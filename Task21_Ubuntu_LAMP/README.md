
## Tìm hiểu LAMP


> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **22/9/2016**

---
##Mục lục

[1.Giới thiệu](#1)

[2. Cài đặt LAMP trên Ubuntu 16.04](#2)

 - [2.1 Cài đặt Webserver Apache](#21)

 - [2.2 Cài đặt MySQL](#22)

 - [2.3 Cài đặt PHP7](#23)

 - [2.4 Cài đặt phpmyAmin](#24)

[3. Cài đặt Wordpress trên Ubuntu 16.04](#3)




<a name="1"></a>
#1. Giới thiệu

LAMP là chữ viết tắt thường được dùng để chỉ sự sử dụng các phần mềm Linux, Apache, MySQL và ngôn ngữ văn lệnh PHP hay Perl hay Python để tạo nên một môi trường máy chủ Web có khả năng chứa và phân phối các trang Web động.

![11](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/11.png)

Linux: Linux là một hệ điều hành. Về mặt nguyên tắc hệ điều hành cũng là một software; nhưng đây là một software đặc biệt được dùng để quản lý, điều phối các tài nguyên (resource) của hệ thống (bao gồm cả hardware và các software khác). Linux còn được gọi là Open Source Unix (OSU)

Apache: Đây là phần mềm webserver phổ biến hiện nay. Apache được cài đặt trên server để giúp xử lý các request với giao thức HTTP gửi tới máy chủ. Do đó, Apache còn được gọi là HTTP webserver. Lưu ý: HTTPS cũng là một giao thức mà Apache có thể sử lý.

Mysql: Là phần mềm database server giúp lưu trữ và truy xuất dữ liệu một cách hiệu quả trên server.

PHP: Viêt tắt của chữ Personal Home Page, là một trong các ngôn ngữ lập trình server phổ biến nhất hiện nay.

Các phần mềm nói trên tạo thành một gói phần mềm LAMP. Ngoài ra, MySQL có thể được thay thế bằng PostgreSQL để lập thành gói phần mềm LAPP với các khả năng kỹ thuật tương tự.

Tại sao chọn LAMP

- Miễn phí bản quyền phần mềm

- Được phép chỉnh sửa phần mềm phù hợp nhu cầu

- An toàn cao

- Tính cộng đồng

- Được miễn phí các phiên bản nâng cấp trong toàn bộ vòng đời sử dụng sản phẩm

- Tiết kiệm chi phí phát triển; các doanh nghiệp sử dụng lại những mã nguồn sẵn có để phát triển, cải tiến nâng cấp

- Không đòi hỏi cấu hình phần cứng quá cao cho việc triển khai ứng dụng

- Đa dạng trong việc lựa chọn nhà cung cấp sản phẩm

- Nâng cao uy tín, thương hiệu của doanh nghiệp đặc biệt khi đối tác kinh doanh là khách nước ngoài

- Tránh vi phạm bản quyền phần mềm

<a name="2"></a>
#2. Cài đặt LAMP trên Ubuntu 16.04

Trước khi cài đặt nên cập nhật các gói phần mềm lên phiên bản mới nhất với lệnh
```
sudo apt-get update
sudo apt-get upgrade
```

<a name="21"></a>
###2.1 Cài đặt WEBSERVER APACHE 2.4.18

Để cài đặt chạy lệnh
```
sudo apt-get install apache2 
```

Nó sẽ hởi y/n chọn **y** rồi nhấn enter, nếu không muốn nhập **y** mỗi khi cài đặt thêm **-y** vào câu lệnh ```sudo apt-get -y install apache 2```

Mặc đinh Apache được cấu hình khởi động cùng hệ thống, nếu chưa thì chạy lệnh dưới
```
sudo systemctl enable apache2
sudo systemctl start apache2
```

Kiểm tra apache chạy hay chưa, mở trình duyệt Chrome nhập vào url http://your_domain/ hoặc http://server-ip/ thông tin như hình bên dưới là OK 

![1](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/1.png)

hoặc chạy lệnh ```sudo service apache2 status```

![2](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/2.png)

<a name="22"></a>
###2.2 Cài đặt MYSQL 

Cài MYSQL

```
sudo apt-get install mysql-server
```
Khi cài MYSQL sẽ hiện lên giao diện để thiết lập mật khẩu root cho MYSQL

![3](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/3.png)

Cài xong, hãy kích hoạt nó bằng lệnh sau:

```
mysql_install_db
```

Sau đó chạy thêm lệnh này để cài đặt bảo mật cho MySQL Server và có thể đổi lại mật khẩu root.
```
/usr/bin/mysql_secure_installation
```

kiểm tra MYSQL chạy hay chưa 

```
sudo service mysql-server status
```

![4](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/4.png)

<a name="23"></a>
###2.3 Cài đặt PHP 7.0

PHP7 là phiên bản mặc định trên Ubuntu 16.04 thay thế cho php 5.3, 5.4, 5.5, 5.6. Bạn có thể cài PHP7 để chạy các các mã nguồn phổ biến WordPress 4.5, joomla 3.5 riêng vơi drupal 7 không vượt qua những thử nghiệm của nhóm phát triển hiện vẫn chưa được hỗ trợ trên Ubuntu 16.04.

Cài những gói cần thiết nhất của PHP7.0 để chạy script php,  bạn có thể bổ sung thêm tuỳ mục đích sử dụng.

```
sudo apt-get install php7.0-cli php7.0-json php7.0-common libapache2-mod-php7.0 php7.0-mcrypt php7.0-mysql php-mbstring php-gettext
```

Cài đặt hoàn tất, bạn hãy kiểm tra bằng cách tạo một file info.php có nội dung như sau để kiểm tra php script đã chạy hay chưa.

```
<?php phpinfo(); ?>
```

Mở trình duyệt nhập vào url http://your_domain/info.php hoặc http://server-ip/info.php. Như hình là OK

![5](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/5.png)

<a name="24"></a>
###2.4 Cài đặt PHPMYADMIN

Cài đặt thêm phpadmin để dễ quản lý MYSQL chạy lệnh
```
sudo apt-get install phpadmin
```
Cửa sổ cấu hinhf phpadmin hiện ra chọn *apache* và Enter

![6](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/6.png)

Và hãy chọn Yes để thiết lập các cấu hình ban đầu cho phpMyAdmin.

![7](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/7.png)

Tạo mật khẩu cho tài khoản phpmyadmin.

![8](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/8.png)

Xác nhận lại mật khẩu lần nữa.

![9](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/9.png)

<a name="3"></a.>
#3. Cài đặt Wordpress trên Ubuntu 16.04

###Tạo database và user cho wordpress

1.Command:

```
mysql -u root -p
```
2.Tạo database và user nhập các lệnh dưới

```
CREATE DATABASE wordpress character set utf8 collate utf8_bin; 
GRANT ALL PRIVILEGES on wordpress.* to 'wpuser'@'localhost' identified by 'nhut96'; 
FLUSH PRIVILEGES; exit
```

![12](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/12.png)

###Cài đặt extention cho PHP

Nhập lệnh sau

```
sudo apt-get install php7.0-mysql php7.0-curl php7.0-json php7.0-cgi php7.0 libapache2-mod-php7.0 php7.0-mcrypt php7.0-xmlrpc php7.0-gd -y
```

###Download wordpress

1.Download source code

Ở đây tôi tải về thư mục tmp, còn tải vào đâu thì tùy 

```
cd /tmp
curl -O https://wordpress.org/latest.tar.gz
```

2.Giải nén

```
tar xzvf latest.tar.gz
```

đổi tên mặc định file config và xoá file config mặc định


```
cp /tmp/wordpress/wp-config-sample.php /tmp/wordpress/wp-config.php && rm wp-config-sample.php
```


 copy vào thư mực /var/www/html/wordpress


```
sudo cp -a /tmp/wordpress/. /var/www/html/wordpress/

```

###Cấu hình thư mục chứa source wordpress 

Để hạn chế sự dòm ngó của hacker cũng như tăng sự bảo mật cho website chúng ta cần cấu hình báo mật thự mục chứa source code wordpress

Cấu hình bảo mật thư mục /var/www/html/wordpress/

```
sudo chown -R www-data:www-data /var/www/html/wordpress/ sudo chmod -R 755 /var/www/html/wordpress/
```

###Cấu hình file config wp-config.php trong /html/wordpress/

Nhập lệnh

```
sudo vi wp-config.php
```

Chỉnh sữa các phần **DB_NAME, DB_USER, DB_PASSWORD**

![13](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/13.png)

lưu lại và restart lại các dịch vụ

```
sudo systemctl restart mysql && systemctl restart apache2
```

###Hoàn thành việc cài đặt wordpress

1.cấu hình các thông số cần thiết cho website

Đăng nhập vào trình duyệt với ```http://localhost/wordpress```

![15](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/14.png)

Điền đầy đủ các thông tin

![16](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/16.png)

![17](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/17.png)

![18](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/18.png)









