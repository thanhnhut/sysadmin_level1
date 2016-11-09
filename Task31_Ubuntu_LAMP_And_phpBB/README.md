## Ubuntu LAMP and phpBB


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **10/11/2016**

### Mục lục

[1. Cài đặt Ubuntu Server 16.04](#1)

[2. Set IP tĩnh](#2)

[3. SSH bằng puclic-key](#3)

[4. Cài đặt phpBB](#4)


---



<a name="1"></a>
# 1.Phần cài mới Ubuntu Server 16.04


 Màn hình đầu tiên của Ubuntu cài đặt. Chọn ngôn ngữ của bạn để thực hiện cài đặt và nhấn phím Enter để chuyển sang màn hình tiếp theo.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a.png"/></p>

 Tiếp theo, chọn tùy chọn đầu tiên, cài đặt Ubuntu Server và nhấn phím Enter để tiếp tục.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/b.png"/></p>

 Chọn ngôn ngữ bạn có cài đặt hệ thống và nhấn Enter lần nữa để tiếp tục thêm

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/c.png"/></p>

 Trên series tiếp theo của màn hình chọn vị trí  của bạn từ danh sách trình bày. Nếu vị trí của bạn là khác nhau hơn so với những người được cung cấp trên màn hình đầu tiên, chọn khác, rồi bấm phím Enter, sau đó chọn vị trí dựa trên lục địa và đất nước của bạn. Vị trí này cũng sẽ được sử dụng bởi các biến hệ thống múi giờ. 

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/d.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/e.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/f.png"/></p>

 Gán các miền địa phương và bàn phím thiết lập cho hệ thống của bạn như hình minh họa dưới đây và nhấn Enter để tiếp tục cài đặt.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/g.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/h.png"/></p>

 Ở bước này trình cài đặt sẽ nhắc bạn để thiết lập một tên người dùng  mật khẩu và các thông tin cho hệ thống của bạn

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/i.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/k.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/l.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/m.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/n.png"/></p>

 Chọn không để mã hóa thư mục nhà của bạn và nhấn Enter để tiếp tục thêm.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a1.png"/></p>

 Tiếp theo, trình cài đặt sẽ tự động thiết lập đồng hồ của bạn dựa trên vị trí địa lý được cấu hình trước đó. Trong trường hợp địa điểm được lựa chọn một cách chính xác nhấn Yes để tiếp tục bố trí phân vùng đĩa.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a2.png"/></p>

 Trên bước tiếp theo bạn có thể chọn các phương pháp sẽ được sử dụng để lát lên đĩa cứng của bạn. Ví dụ, nếu bạn cần phải tạo một kế hoạch phân vùng tùy chỉnh (như / home, / var, / boot vv) chọn phương pháp thủ côn, chọn như hình để có thể tự động tạo ra các phân vùng thay cho bạn.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a3.png"/></p>

 Tiếp theo, chọn ổ đĩa mà sẽ được sử dụng bởi trình cài đặt để tạo ra các phân vùng và nhấn phím Enter.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a4.png"/></p>

 Trả lời với Yes tại màn hình tiếp theo để cam kết thay đổi vào đĩa với chương trình LVM và nhấn vào Continue để sử dụng toàn bộ không gian đĩa cho các phân vùng đã hướng dẫn

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a5.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a6.png"/></p>

 Cuối cùng, phê duyệt lần cuối cùng những thay đổi phải được ghi vào đĩa bằng cách nhấn vào Yes và cài đặt sẽ bắt đầu. Từ bước này trên tất cả các thay đổi sẽ được cam kết vào đĩa.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a7.png"/></p>

 Trong trường hợp hệ thống của bạn là sau một proxy hoặc tường lửa sử dụng màn hình tiếp theo để vượt qua những hạn chế mạng, nếu không chỉ cần để nó trống và nhấn Continue.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a8.png"/></p>

 Tiếp theo, trình cài đặt sẽ cấu hình apt và sẽ cài đặt các phần mềm được chọn. Sau khi nó kết thúc nhiệm vụ lắp đặt một màn hình mới sẽ xuất hiện mà sẽ yêu cầu bạn làm thế nào để quản lý quá trình nâng cấp.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a9.png"/></p>

 Trên bước tiếp theo bạn sẽ được yêu cầu chọn phần mềm nào để cài đặt. Chọn các tiện ích hệ thống chỉ tiêu chuẩn tùy bạn và nhấn Countinue

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a10.png"/></p>

 Một khi trình cài đặt kết thúc cài đặt các phần mềm, một màn hình mới sẽ nhắc bạn xem có cài đặt bộ nạp khởi động Grub do đó nhấn Yes để tiếp tục cài đặt.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a11.png"/></p>

 Cuối cùng, sau khi các bộ nạp khởi động được ghi vào đĩa cứng MBR, quá trình cài đặt hoàn tất. Nhấn Continue để khởi động lại máy và loại bỏ các phương tiện cài đặt.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a12.png"/></p>

 Sau khi khởi động lại, đăng nhập vào giao diện điều khiển hệ thống của bạn bằng cách sử dụng các thông tin cấu hình trong quá trình cài đặt 

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a13.png"/></p>


<a name="2"></a>
#2. Set IP tĩnh

Vào terminal gõ ```sudo /etc/network/interfaces``` rồi nhập các lệnh giống ví dụ bên dưới

```
auto eth0
iface eth0 inet static
   address 10.253.0.50
   netmask 255.255.255.0
   network 10.253.0.0
   gateway 10.253.0.1
   dns-nameservers 8.8.8.8
```

<a name="3"></a>
#3. SSH bằng public-key

####Vào *terminal* nhập lệnh sau để cài SSH

```
$ sudo apt-get install openssh-server
```

Đầu tiên mình cần tạo thư mục chứa Public Key trên Server từ Client, ví dụ:
```
ssh nhut@192.168.15.183 mkdir -p .ssh
```

Bước tiếp theo sẽ tạo authorized_keys cho server bằng chuỗi lệnh:

```
cat .ssh/id_rsa.pub | ssh nhut@192.168.15.183 'cat >> .ssh/authorized_keys'
```

Tiếp sau sẽ dùng chmod phân quyền 700 cho folder .ssh & 640 cho file authorized_keys

```
chmod 700 .ssh
chmod 640 .ssh/authorized_keys
```

Đến đây kể như hoàn tất Client đã có Private Key, trên Server đã có Public Key nhưng kết nối vẫn xác  thực theo Password Authentication.  Tìm đến file /etc/ssh/sshd_config hiệu chỉnh thông số như sau.

```
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no 
```



<a name="4"></a>
#4. Cài đặt phpBB

Để cài đặt phpBB trước tiên hãy chắc chắn rằng tất cả các gói hệ thống của bạn là up-to-date bằng cách chạy các apt-get lệnh sau trong terminal

```
sudo  apt - get  update 
sudo  apt - get  upgrade 
```

<a name="41"></a>
###Bước 1: Cài đặt LAMP


#### Cài đặt WEBSERVER APACHE 2.4.18

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

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/1.png" /></p>

hoặc chạy lệnh ```sudo service apache2 status```

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/2.png" /></p>


###Cài đặt MYSQL 

Cài MYSQL

```
sudo apt-get install mysql-server
```
Khi cài MYSQL sẽ hiện lên giao diện để thiết lập mật khẩu root cho MYSQL

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/3.png" /></p>

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

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/4.png" /></p>


### Cài đặt PHP 7.0

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

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task21_Ubuntu_LAMP/images/5.png" /></p>


###Bước 2: Tạo DATABASE

Gõ lệnh sau vào terminal để tạo database 

```
sudo mysql -u root -p
```

Sau khi vào mysql nhập các lệnh dưới để tạo DATABASE

```
CREATE DATABASE phpBB;
CREATE USER 'nhut'@'localhost' identified by 'badpassword';
GRANT ALL PEIVILEGES ON phpBB.* TO 'nhut'@'localhost';
FLUSH PRIVILEGES;
exit
```

###Bước 3: Cài đặt phpBB

Đầu tiên, download phiên bản mới nhất của hệ thống phpBB

```
wget https://www.phpbb.com/files/release/phpBB-3.1.2.zip
```

Giải nén gói bạn đã tải về.

```
unzip phpBB-3.1.2.zip
```

Tạo một thư mục sao lưu cho bất kỳ tập tin trang web hiện có.

```
mkdir ~/website-backup
```

Di chuyển tất cả file web vào thư mục vừa tạo

```sudo mv /var/www/html/* ~/website-backup/```

Sao chép các tập tin hệ thống phpBB trên vào thư mục mặc định của Apache

```sudo cp -R phpBB3/* /var/www/html/```

Tiếp theo, chúng ta muốn cập nhật các điều khoản trên các tập tin hệ thống phpBB, thêm mình vào nhóm www-data 

```sudo usermod -aG www-data nhut```

Tiếp theo, thay đổi chủ sở hữu và nhóm của các tập tin trong thư mục / var / www / html tới www-data

```sudo chown -R www-data:www-data /var/www/html/```

Di chuyển đến thư mục / var / www / html /

```cd /var/www/html/```

Thêm quyền cho các nhóm tới các thư mục và các tập tin sau đây.

```sudo chmod 660 images/avatars/upload/ config.php
sudo chmod 770 store/ cache/ files/```

###Bước 4: Hoàn thành cài đặt

Trong bước này, chúng ta sẽ hoàn tất cài đặt bằng cách thêm vào cơ sở dữ liệu, quản trị, và các thông tin chi tiết thông qua các trang web cài đặt phpBB.

Tử trình duyệt truy cập vào địa chỉ web server

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP__And_phpBB/Images/1.png)

Click vào tab INSTALL

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP__And_phpBB/Images/2.png)

Bạn nên có tất cả các gói cần thiết đã được cài đặt. Nhấp vào **Proceed to next step**, sau đó bắt đầu cài đặt.

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP__And_phpBB/Images/3.png)

Sau đó nhấp vào **Proceed to next step**. Đối với hầu hết các bước sau thời điểm này, bạn sẽ phải bấm vào nút **Proceed to next step** để di chuyển

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP__And_phpBB/Images/4.png)

Bây giờ bạn sẽ thấy một kết nối cơ sở dữ liệu thành công.

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP__And_phpBB/Images/5.png)

Ở bước tiếp theo này, bạn thiết lập username administrator và mật khẩu của bạn.

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP__And_phpBB/Images/6.png)

Thiết lập cài đặt email nếu bạn có một máy chủ SMTP tùy chỉnh, nếu không, gắn nó với các giá trị mặc định.

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP__And_phpBB/Images/9.png)

###Bước 5: Dọn dẹp

Bước này, chúng ta sẽ làm sạch sau khi cài đặt của bạn bằng cách loại bỏ các tập tin không cần thiết và điều chỉnh một số điều khoản.

Hủy bỏ một số quyền truy cập vào các tập tin config.php

```sudo chmod 640 /var/www/html/config.php```

Bây giờ cài đặt xong, bạn nên xóa các thư mục / var / www / install . phpBB sẽ không hoạt động trừ khi thư mục này sẽ bị xóa, và một thông điệp cảnh báo sẽ được hiển thị.

```sudo rm -rf /var/www/html/install```

Bây giờ bạn sẽ có thể truy cập vào diễn đàn phpBB của bạn tại địa chỉ IP  của bạn!

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task31_Ubuntu_LAMP__And_phpBB/Images/11.png)

