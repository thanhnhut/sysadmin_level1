## Ubuntu LAMP and OpenCart


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **15/10/2016**

### Mục lục

[1. Cài đặt Ubuntu Server 16.04](#1)

[2. Cài đặt Opencart](#2)

---



<a name="1"></a>
# 1.Phần cài mới Ubuntu Server 16.04


- Mở __VMware Workstation__ và click vào __Create a New Virtual Machine__

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a1.png/></p>

- Chọn  __custom (advanced)__ vì nó mang đến nhiều lựa chọn

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a2.png/></p>

- Click next và chọn phiên bản  __VMware Workstation__ tương ứng 

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a3.png/></p>

- Chọn I will install operating system later

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a4.png/></p>


- Đặt tên và thiết lập vị trí cho máy ảo Ubuntu

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a6.png/></p>

- Đặt CPU ảo và lõi mà bạn muốn, nên chọn 1 bộ xử lý và 2 lõi để  __Ubuntu__ mạnh hơn

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a7.png/></p>

- Điều chỉnh bộ nhớ cho __Ubuntu__ , nếu máy 32bits thì nên chọn 1024MB còn đối với máy 64 bits chọn 2048MB

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a8.png/></p>

- Chọn kiểu mạng mà bạn muốn

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a9.png/></p>

- Click Next chọn __LSI Logic (recommended)__

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a10.png/></p>

- Tiếp tục click next chọn __SCSI (recommended)__

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a11.png/></p>

- Click Next chọn __Creata a new virtual disk__ để tạo ổ đĩa mới cho __Ubuntu__

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a12.png/></p>

- Chỉ định bao nhiêu không gian đĩa  muốn sử dụng cho  __Ubuntu__  rồi chọn  __store virtual disk as a single file__  tùy chọn này cho phép thực hiện nhiều hơn

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a13.png/></p>

- Click Next ở cửa sổ tiếp theo

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a14.png/></p>

- Hiện những thông số đã cài đặt click finish

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a15.png/></p>

- Đến đây  hãy nhấp chuột vào biểu tượng *CD/DVD (SATA)* để đi đến đường đẫn của iso linux

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a16.png/></p>

- Chọn *Use ISO image file* để tìm file ISO ubuntu để cài đặt sau đó bấm ok

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a17.png/></p>

- Khi thiết lập xong thì hãy nhấn vào biểu tượng hình tam giác để khởi động máy ảo Ubuntu.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task13_Initialize_Ubuntu_Lab/a18.png/></p>

- Màn hình đầu tiên của Ubuntu cài đặt. Chọn ngôn ngữ của bạn để thực hiện cài đặt và nhấn phím Enter để chuyển sang màn hình tiếp theo.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a.png/></p>

- Tiếp theo, chọn tùy chọn đầu tiên, cài đặt Ubuntu Server và nhấn phím Enter để tiếp tục.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/b.png/></p>

- Chọn ngôn ngữ bạn có cài đặt hệ thống và nhấn Enter lần nữa để tiếp tục thêm

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/c.png/></p>

- Trên series tiếp theo của màn hình chọn vị trí  của bạn từ danh sách trình bày. Nếu vị trí của bạn là khác nhau hơn so với những người được cung cấp trên màn hình đầu tiên, chọn khác, rồi bấm phím Enter, sau đó chọn vị trí dựa trên lục địa và đất nước của bạn. Vị trí này cũng sẽ được sử dụng bởi các biến hệ thống múi giờ. 

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/d.png/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/e.png/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/f.png/></p>

- Gán các miền địa phương và bàn phím thiết lập cho hệ thống của bạn như hình minh họa dưới đây và nhấn Enter để tiếp tục cài đặt.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/g.png/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/h.png/></p>

- Ở bước này trình cài đặt sẽ nhắc bạn để thiết lập một tên người dùng  mật khẩu và các thông tin cho hệ thống của bạn

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/i.png/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/k.png/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/l.png/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/m.png/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/n.png/></p>

- Chọn không để mã hóa thư mục nhà của bạn và nhấn Enter để tiếp tục thêm.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a1.png/></p>

- Tiếp theo, trình cài đặt sẽ tự động thiết lập đồng hồ của bạn dựa trên vị trí địa lý được cấu hình trước đó. Trong trường hợp địa điểm được lựa chọn một cách chính xác nhấn Yes để tiếp tục bố trí phân vùng đĩa.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a2.png/></p>

- Trên bước tiếp theo bạn có thể chọn các phương pháp sẽ được sử dụng để lát lên đĩa cứng của bạn. Ví dụ, nếu bạn cần phải tạo một kế hoạch phân vùng tùy chỉnh (như / home, / var, / boot vv) chọn phương pháp thủ côn, chọn như hình để có thể tự động tạo ra các phân vùng thay cho bạn.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a3.png/></p>

- Tiếp theo, chọn ổ đĩa mà sẽ được sử dụng bởi trình cài đặt để tạo ra các phân vùng và nhấn phím Enter.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a4.png/></p>

- Trả lời với Yes tại màn hình tiếp theo để cam kết thay đổi vào đĩa với chương trình LVM và nhấn vào Continue để sử dụng toàn bộ không gian đĩa cho các phân vùng đã hướng dẫn

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a5.png/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a6.png/></p>

- Cuối cùng, phê duyệt lần cuối cùng những thay đổi phải được ghi vào đĩa bằng cách nhấn vào Yes và cài đặt sẽ bắt đầu. Từ bước này trên tất cả các thay đổi sẽ được cam kết vào đĩa.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a7.png/></p>

- Trong trường hợp hệ thống của bạn là sau một proxy hoặc tường lửa sử dụng màn hình tiếp theo để vượt qua những hạn chế mạng, nếu không chỉ cần để nó trống và nhấn Continue.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a8.png/></p>

- Tiếp theo, trình cài đặt sẽ cấu hình apt và sẽ cài đặt các phần mềm được chọn. Sau khi nó kết thúc nhiệm vụ lắp đặt một màn hình mới sẽ xuất hiện mà sẽ yêu cầu bạn làm thế nào để quản lý quá trình nâng cấp.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a9.png/></p>

- Trên bước tiếp theo bạn sẽ được yêu cầu chọn phần mềm nào để cài đặt. Chọn các tiện ích hệ thống chỉ tiêu chuẩn tùy bạn và nhấn Countinue

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a10.png/></p>

- Một khi trình cài đặt kết thúc cài đặt các phần mềm, một màn hình mới sẽ nhắc bạn xem có cài đặt bộ nạp khởi động Grub do đó nhấn Yes để tiếp tục cài đặt.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a11.png/></p>

- Cuối cùng, sau khi các bộ nạp khởi động được ghi vào đĩa cứng MBR, quá trình cài đặt hoàn tất. Nhấn Continue để khởi động lại máy và loại bỏ các phương tiện cài đặt.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a12.png/></p>

- Sau khi khởi động lại, đăng nhập vào giao diện điều khiển hệ thống của bạn bằng cách sử dụng các thông tin cấu hình trong quá trình cài đặt 

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task25_Ubuntu_LAMP_And_OpenCart/Images/a13.png/></p>


<a name="2"></a>
#2. Cài đặt Opencart

Để cài đặt Opencart trước tiên hãy chắc chắn rằng tất cả các gói hệ thống của bạn là up-to-date bằng cách chạy các apt-get lệnh sau trong terminal và đã cài đặt **LAMP**.

```
sudo  apt - get  update 
sudo  apt - get  upgrade 
```

###Bắt đầu cài đặt

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
