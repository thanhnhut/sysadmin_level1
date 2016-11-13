## Ubuntu LAMP with Virtualhost


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **12/11/2016**

### Mục lục

[1.Cài đặt LAMP trên Ubuntu 16.04](#1)

 - [1.1 Cài đặt Webserver Apache](#11)

 - [1.2 Cài đặt MySQL](#12)

 - [1.3 Cài đặt PHP7](#13)

 - [1.4 Cài đặt phpmyAmin](#14)

[2. Tạo Virtualhost](#2)

[3. Cài đặt Opencart trên Virtualhost](#3)

[4. Cài đặt Wordpress trên Virtualhos](#4)

[5. Cài đặt phpBB trên Virtualhos](#5)

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
sudo apt-get install php7.0-cli php7.0-json php7.0-common libapache2-mod-php7.0 php7.0-mcrypt php7.0-mysql php-mbstring php-gettext php7.0-curl php7.0-zip
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

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task33_Ubuntu_LAMP_with_Virtualhost/Images/1.png)




<a name="3"></a>
#3. Caì đặt Opencart


Tải về giải nén như các dòng lệnh sau hoặc có thể tải tử source [ OpenCart’s download page](https://github.com/opencart/opencart)

```
wget https://github.com/opencart/opencart/archive/2.3.0.2.zip
unzip 2.3.0.2.zip
mv opencart-2.3.0.2/upload/* /var/www/oc/public_html

```

Đổi tên file ‘config-dist.php’ thành ‘config.php’

```mv config-dist.php config.php```

Cần phải thay đổi một số thư mục cho phép

```


chown -R www-data.www-data /var/www/html
chmod -R 755 /var/www/html
```

###Cấu hình MariaDB hoặc MySQL cho Opencart

Đầu tiên cần đi vào cơ sở dữ liệu

```sudo mysql -u root -p```

Điều này sẽ nhắc bạn nhập mật khẩu, hãy nhập vào mật khẩu root MariaDB của bạn và nhấn Enter. Một khi bạn đã đăng nhập vào máy chủ cơ sở dữ liệu của bạn, bạn cần phải tạo ra một cơ sở dữ liệu để cài đặt OpenCart

```


MariaDB [(none)]> CREATE DATABASE opencart;
MariaDB [(none)]> GRANT ALL PRIVILEGES ON opencart.* TO 'opencartuser'@'localhost' IDENTIFIED BY 'opencartuser_passwd';
MariaDB [(none)]> FLUSH PRIVILEGES;
MariaDB [(none)]> exit
```

Cuối cùng sau khi tất cả mọi thứ được thiết lập cần trỏ đến trình duyệt web của bạn đến máy chủ  tên miền ```thanhnhut-oc.local```

Bắt đầu quá trình cài đặt như hình dưới đây.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task33_Ubuntu_LAMP_with_Virtualhost/Images/2.png"/></p>

Click vào Continue điều này sẽ tải một trang cài đặt nơi mỗi cấu hình cài đặt sẵn được kiểm tra. 

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task33_Ubuntu_LAMP_with_Virtualhost/Images/3.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a16.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a17.png"/></p>

Tiếp theo click vào Continue để di chuyển đến trang Configuration. Ở đây, ta sẽ cần phải nhập thông tin đăng nhập cơ sở dữ liệu chúng ta đã thiết lập ở trên trong khi tạo ra cơ sở dữ liệu của chúng ta khi cài đặt OpenCart. Sau đó sẽ thiết lập tên người dùng, mật khẩu và email.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task33_Ubuntu_LAMP_with_Virtualhost/Images/6.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task33_Ubuntu_LAMP_with_Virtualhost/Images/7.png"/></p>

Cài đặt hoàn tất 

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task33_Ubuntu_LAMP_with_Virtualhost/Images/8.png"/></p>

Để đăng nhập vào trang quản trị làm như ví dụ sau 

```
https://thanhnhut-oc.local/admin
```

Màn hình đăng nhập sẽ xuất hiện sau khi đăng nhập thành công sẽ thấy trang quản trị

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task33_Ubuntu_LAMP_with_Virtualhost/Images/19.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task33_Ubuntu_LAMP_with_Virtualhost/Images/11.png"/></p>


<a name="4"></a>
#4. Cài đặt Worpress trên Virtualhost

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





3.Download source code

Ở đây tôi tải về thư mục tmp, còn tải vào đâu thì tùy 

```
curl -O https://wordpress.org/latest.tar.gz
```

4.Giải nén

```
tar xzvf latest.tar.gz
```

đổi tên mặc định file config và xoá file config mặc định


```
mv wp-config-sample.php wp=config.php
```


 copy vào thư mực /var/www/wp/public_html


```
sudo cp -a wordpress/*. /var/www/wp/public_html/

```

###Cấu hình thư mục chứa source wordpress 

Để hạn chế sự dòm ngó của hacker cũng như tăng sự bảo mật cho website chúng ta cần cấu hình báo mật thự mục chứa source code wordpress

Cấu hình bảo mật thư mục /var/www/wp/public_html/

```
sudo chown -R www-data:www-data /var/www/wp/public_html/ sudo chmod -R 755 /var/www/wp/public_html/
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

Đăng nhập vào trình duyệt với ```http://thanhnhut-wp.local```

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task33_Ubuntu_LAMP_with_Virtualhost/Images/12.png"/></p>

Điền đầy đủ các thông tin

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task33_Ubuntu_LAMP_with_Virtualhost/Images/13.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task33_Ubuntu_LAMP_with_Virtualhost/Images/14.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task33_Ubuntu_LAMP_with_Virtualhost/Images/15.png"/></p>


#5. Cài đặt phpBB trên Virtualhost 

###Bước 1: Tạo DATABASE

Gõ lệnh sau vào terminal để tạo database 

```
sudo mysql -u root -p
```

Sau khi vào mysql nhập các lệnh dưới để tạo DATABASE

```
CREATE DATABASE phpBB;
CREATE USER 'nhut'@'localhost' identified by 'badpassword';
GRANT ALL PRIVILEGES ON phpBB.* TO 'nhut'@'localhost';
FLUSH PRIVILEGES;
exit
```

###Bước 2: Cài đặt phpBB

Đầu tiên, download phiên bản mới nhất của hệ thống phpBB

```
wget https://www.phpbb.com/files/release/phpBB-3.1.2.zip
```

Giải nén gói bạn đã tải về.

```
unzip phpBB-3.1.2.zip
```





Sao chép các tập tin hệ thống phpBB trên vào thư mục mặc định của Apache

```sudo cp -R phpBB3/* /var/www/phpbb/public_html```

Tiếp theo, chúng ta muốn cập nhật các điều khoản trên các tập tin hệ thống phpBB, thêm mình vào nhóm www-data 

```sudo usermod -aG www-data nhut(hostname)```

Tiếp theo, thay đổi chủ sở hữu và nhóm của các tập tin trong thư mục / var / www / html tới www-data

```sudo chown -R www-data:www-data /var/www/phpbb/public_html```

Di chuyển đến thư mục / var / www /phpbb/public_html/

```cd /var/www/phpbb/public_html```

Thêm quyền cho các nhóm tới các thư mục và các tập tin sau đây.

```
sudo chmod 660 images/avatars/upload/ config.php
sudo chmod 770 store/ cache/ files/

```

###Bước 3: Hoàn thành cài đặt

Trong bước này, chúng ta sẽ hoàn tất cài đặt bằng cách thêm vào cơ sở dữ liệu, quản trị, và các thông tin chi tiết thông qua các trang web cài đặt phpBB.

Từ trình duyệt truy cập vào địa chỉ web server


![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP_And_phpBB/Images/1.png)


Click vào tab INSTALL


![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP_And_phpBB/Images/2.png)


Bạn nên có tất cả các gói cần thiết đã được cài đặt. Nhấp vào **Proceed to next step**, sau đó bắt đầu cài đặt.


![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP_And_phpBB/Images/3.png)


Sau đó nhấp vào **Proceed to next step**. Đối với hầu hết các bước sau thời điểm này, bạn sẽ phải bấm vào nút **Proceed to next step** để di chuyển


![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP_And_phpBB/Images/4.png)


Bây giờ bạn sẽ thấy một kết nối cơ sở dữ liệu thành công.


![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP_And_phpBB/Images/5.png)


Ở bước tiếp theo này, bạn thiết lập username administrator và mật khẩu của bạn.


![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP_And_phpBB/Images/6.png)


Thiết lập cài đặt email nếu bạn có một máy chủ SMTP tùy chỉnh, nếu không, gắn nó với các giá trị mặc định.


![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP_And_phpBB/Images/9.png)


###Bước 4: Dọn dẹp

Bước này, chúng ta sẽ làm sạch sau khi cài đặt của bạn bằng cách loại bỏ các tập tin không cần thiết và điều chỉnh một số điều khoản.

Hủy bỏ một số quyền truy cập vào các tập tin config.php

```sudo chmod 640 /var/www/phpbb/public_html/config.php```

Bây giờ cài đặt xong, bạn nên xóa các thư mục / var / www / install . phpBB sẽ không hoạt động trừ khi thư mục này sẽ bị xóa, và một thông điệp cảnh báo sẽ được hiển thị.

```sudo rm -rf /var/www/phpbb/public_html/install```

Bây giờ bạn sẽ có thể truy cập vào diễn đàn phpBB của bạn tại địa chỉ IP  của bạn!


![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task33_Ubuntu_LAMP_with_Virtualhost/Images/16.png)


