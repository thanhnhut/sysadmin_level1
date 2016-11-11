## Ubuntu LAMP with Virtualhost


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **11/11/2016**

### Mục lục

[1.Cài đặt LAMP trên Ubuntu 16.04](#1)

 - [1.1 Cài đặt Webserver Apache](#11)

 - [1.2 Cài đặt MySQL](#12)

 - [1.3 Cài đặt PHP7](#13)

 - [1.4 Cài đặt phpmyAmin](#14)

[2. Tạo Virtualhost](#2)

---


<a name="1"></a>
#1. Cài đặt LAMP trên Ubuntu 16.04

Trước khi cài đặt nên cập nhật các gói phần mềm lên phiên bản mới nhất với lệnh
```
sudo apt-get update
sudo apt-get upgrade
```

<a name="11"></a>
###1.1 Cài đặt WEBSERVER APACHE 2.4.18

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

<a name="12"></a>
###1.2 Cài đặt MYSQL 

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

<a name="13"></a>
###1.3 Cài đặt PHP 7.0

PHP7 là phiên bản mặc định trên Ubuntu 16.04 thay thế cho php 5.3, 5.4, 5.5, 5.6. Bạn có thể cài PHP7 để chạy các các mã nguồn phổ biến WordPress 4.5, joomla 3.5 riêng vơi drupal 7 không vượt qua những thử nghiệm của nhóm phát triển hiện vẫn chưa được hỗ trợ trên Ubuntu 16.04.

Cài những gói cần thiết nhất của PHP7.0 để chạy script php,  bạn có thể bổ sung thêm tuỳ mục đích sử dụng.

```
sudo apt-get install php7.0-cli php7.0-json php7.0-common libapache2-mod-php7.0 php7.0-mcrypt php7.0-mysql php-mbstring php-gettext php7.0-curl php7.0-zipip
```

Cài đặt hoàn tất, bạn hãy kiểm tra bằng cách tạo một file info.php có nội dung như sau để kiểm tra php script đã chạy hay chưa.

```
<?php phpinfo(); ?>
```

Mở trình duyệt nhập vào url http://your_domain/info.php hoặc http://server-ip/info.php. Như hình là OK

![5](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/5.png)

<a name="14"></a>
###1.4 Cài đặt PHPMYADMIN

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


<a name="2"></a>
#2.Tạo Virtual Host trên Apache

###Bước 1: Tạo thư mục cho trang web

Cần tạo ra ba thư mục để chứa tập tin và dữ liệu của ba trang web trên bằng câu lệnh sau:

>sudo mkdir -p /var/www/oc/public_html
>sudo mkdir -p /var/www/wp/public_html
>sudo mkdir -p /var/www/phpbb/public_html



###Bước 2: Cấp quyền 

```
sudo chown -R $USER:$USER /var/www/op/public_html
sudo chown -R $USER:$USER /var/www/wp/public_html
sudo chown -R $USER:$USER /var/www/phpbb/public_html
sudo chmod 755 /var/www/
```

###Bước 3: Tạo trang demo cho mỗi Virtual Host

>sudo nano /var/www/oc/public_html/index.html
>sudo nano /var/www/wp/public_html/index.html
>sudo nano /var/www/phpbb/public_html/index.html

Với nội dung của file index.html tùy bạn

```
<html>
	<head>
	<title>Hello</title>
	</head>
	<body>
		<h1>Welcome To website</h1>
	</body>
</html>
```

###Bước 4: Tạo Virtual Host mới 

Bắt đầu bằng cách sao chép các tập tin cho các tên miền đầu tiên:

```
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/op.conf

sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/wp.conf

sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/phpbb.conf

```
Mở tập tin mới trong trình soạn thảo của bạn với quyền root, tập tin VirtualHost của ta sẽ chỉnh sữa trông như thế này:

```
<VirtualHost *:80>
    ServerAdmin admin@thanhnhut-oc.local
    ServerName thanhnhut-oc.local
    ServerAlias www.thanhnhut-oc.local
    DocumentRoot /var/www/oc/public_html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

###Bước 5:  Kích hoạt tập tin Virtual Host

```
sudo a2ensite oc.conf
sudo a2ensite wp.conf
sudo a2ensite phpbb.conf
```

Sau đó bạn cần phải khởi động lại Apache để thực hiện những thay đổi này có hiệu lực:

```
sudo service apache2 restart
```

###Bước 6: Thiết lập file /etc/hosts

Mở tập tin mới trong trình soạn thảo của bạn

```
sudo nano /etc/hosts
```

Các chi tiết mà bạn cần phải thêm là địa chỉ IP webserver của bạn và sau đó là tên miền của Virtua Host vd

```
192.168.15.146 thanhnhut-oc.conf
192.168.15.146 thanhnhut-wp.conf
192.168.15.146 thanhnhut-phpbb.conf
```

Cuối cùng test thử xem các Virtual Host có hoạt động hay không bằng cách truy cập tên miền vào trình duyệt của bạn, vd 

>httpt://thanhnhut-oc.local

Bạn sẽ thấy một trang đó trông như thế này:

##Welcome To website



