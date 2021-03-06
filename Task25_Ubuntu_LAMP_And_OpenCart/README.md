## Ubuntu LAMP and OpenCart


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **29/10/2016**

### Mục lục

[1. Cài đặt Ubuntu Server 16.04](#1)

[2. Set IP tĩnh](#2)

[3. SSH bằng puclic-key](#3)

[4. Cài đặt Opencart](#4)

 - [4.1 Cài đặt LAMP](#41)

  - [4.1.1 Cài đặt WEBSERVER APACHE 2.4.18](#411)

  - [4.1.2 Cài đặt MYSQL](#412)

  - [4.1.3 Cài đặt PHP 7.0](#413)

 - [4.2 Bắt đầu caì đặt Opencart](#42)

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
#4. Cài đặt Opencart

Để cài đặt Opencart trước tiên hãy chắc chắn rằng tất cả các gói hệ thống của bạn là up-to-date bằng cách chạy các apt-get lệnh sau trong terminal

```
sudo  apt - get  update 
sudo  apt - get  upgrade 
```

<a name="41"></a>
###4.1 Cài đặt LAMP

<a name="411"></a>
####4.1.1 Cài đặt WEBSERVER APACHE 2.4.18

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

<a name="412"></a>
###4.1.2 Cài đặt MYSQL 

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

<a name="413"></a>
###4.1.3 Cài đặt PHP 7.0

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

<a name="42"></a>
###4.2 Bắt đầu cài đặt Opencart

Tải về giải nén như các dòng lệnh sau hoặc có thể tải tử source [ OpenCart’s download page](https://github.com/opencart/opencart)

```
wget https://github.com/opencart/opencart/archive/2.3.0.2.zip
unzip 2.3.0.2.zip
mv opencart-2.3.0.2/upload/* /var/www/html/

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

Cuối cùng sau khi tất cả mọi thứ được thiết lập cần trỏ đến trình duyệt web của bạn đến máy chủ bằng  IP hoặc tên miền như ```http://địa chỉ IP / ```hoặc ```http://domain.com/-Tây Bắc``` , theo cách hướng dẫn trên thì sẽ trỏ trình duyệt tới như vd sau 

```
https://192.168.15.183/install/
```

Bắt đầu quá trình cài đặt như hình dưới đây.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a14.png"/></p>

Click vào Continue điều này sẽ tải một trang cài đặt nơi mỗi cấu hình cài đặt sẵn được kiểm tra. 

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a15.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a16.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a17.png"/></p>

Tiếp theo click vào Continue để di chuyển đến trang Configuration. Ở đây, ta sẽ cần phải nhập thông tin đăng nhập cơ sở dữ liệu chúng ta đã thiết lập ở trên trong khi tạo ra cơ sở dữ liệu của chúng ta khi cài đặt OpenCart. Sau đó sẽ thiết lập tên người dùng, mật khẩu và email.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a18.png"/></p>

Cài đặt hoàn tất 

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a19.png"/></p>

Để đăng nhập vào trang quản trị làm như ví dụ sau 

```
https://192.168.15.183/admin
```

Màn hình đăng nhập sẽ xuất hiện sau khi đăng nhập thành công sẽ thấy trang quản trị

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a20.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a21.png"/></p>
