<p align="center"><img src="http://thuatngu.org/wp-content/uploads/2016/08/vps-la-gi.jpg" /></p>

> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật: **08/02/2017**

###Mục lục

[1.VPS](#1)

[2.Cloud VPS](#2)

[3.Giao diện quản lý VPS](#3)

[4.Cài đặt SSH và SSH bằng public key](#4)

[5.Một số thao tác qua SSH](#5)

[6.Tham Khảo](#6)


---

<a name="1"></a>
#1.VPS

VPS (Virtual Private Server) là dạng máy chủ được tạo ra bằng phương pháp phân chia một máy chủ vật lý thành nhiều máy chủ khác nhau có tính năng tương tự như máy chủ riêng (dedicated server), chạy dưới dạng chia sẻ tài nguyên từ máy chủ vật lý ban đầu. Khác với hosting sử dụng phần mềm quản lý (hosting control panel) để khởi tạo và quản lý các gói hosting, VPS được tạo ra nhờ công nghệ ảo hóa. Số lượng VPS luôn thấp hơn nhiều lần so với số lượng hosting nếu cài đặt trên cùng một hệ thống server, do đó tính ổn định và hiệu suất sử dụng tài nguyên của VPS luôn vượt trội so với hosting. Một VPS có thể chứa hàng trăm hosting khác nhau.

Máy chủ ảo phù hợp để xây dựng các hệ thống Mail Server, Web Server, Backup/Storage Server... dùng riêng hoặc truyền tải file dữ liệu giữa các chi nhánh với nhau một cách nhanh chóng, thuận tiện và bảo mật; dễ dàng nâng cấp tài nguyên và tái tạo lại hệ điều hành khi gặp sự cố hệ thống với thời gian thực hiện rất nhanh mà không cần cài đặt lại từ đầu.

Máy chủ ảo như một giải pháp dung hòa giữa hosting và máy chủ riêng (dedicated server) theo cả khía cạnh chi phí và cách thức vận hành. Vì vậy đây là giải pháp phù hợp cho các cá nhân hoặc doanh nghiệp muốn có một hệ thống máy chủ riêng biệt, toàn quyền quản lý với chi phí thấp.

 VPS thường được sử dụng cho các nhu cầu sau:

- Máy chủ game (game server).

- Lưu trữ website đa dịch vụ (website bán hàng, website thương mại điện tử, các diễn đàn, các trang web có lượng truy cập lớn...)

- Phát triển platform.

- Máy chủ cho hệ thống email doanh nghiệp.

- Chạy các chương trình truyền thông trực tiếp.

- Tạo các môi trường ảo để lập trình, phân tích virus, nghiên cứu...

- Lưu trữ các dữ liệu: tài liệu, hình ảnh, video...

###Các thông số cần lưu ý

**1.RAM**

 VPS bạn càng nhiều RAM thì khả năng truy xuất dữ liệu càng tốt bởi vì khi dùng VPS, bạn sẽ cần RAM để nó xử lý các vấn đề như xử lý các đoạn mã PHP với phần mềm PHP, xử lý truy vấn nhập xuất của database với MySQL, các ứng dụng nhỏ đi kèm, hỗ trợ đọc ghi dữ liệu,…

Hiện nay đa phần các dịch vụ VPS sẽ cho phép bạn chọn mức RAM từ 512MB đến 16GB (nếu bạn thấy VPS nào nhiều hơn 16GB RAM thì đó chính là Cloud VPS) và tùy theo lượng truy cập vào website của bạn cũng như cách tối ưu VPS thì bạn sẽ cần nhiều RAM hay ít.

**2.SWAP**

Swap (hoán đổi) là một vùng trên ổ đĩa mà nó có thể được sử dụng để lưu trữ các dữ liệu mà không được sử dụng trên bộ nhớ vật lý (RAM). Đây là nơi tạm thời chứa các tài nguyên đang không hoạt động trong bộ nhớ.

Khuyến cáo nên tạo swap để máy chủ đạt hiệu suất tốt hơn.

**3.DISK**

Ổ đĩa hiện nay được chia làm 2 loại:

- HDD (Hard Disk Drive): Là loại ổ đĩa thông dụng nhất mà bấy lâu nay bạn sử dụng trên máy tính đó.

- SSD (Solid State Drive): SSD hoặc bạn cũng có thể nghe dịch ra tiếng Việt là ổ cứng bán dẫn, là một loại ổ cứng để lưu trữ dữ liệu nhưng nó sẽ có tốc độ truy xuất dữ liệu nhanh hơn loại HDD lên tới 300 lần, cái này mình không phải lấy từ các lý thuyết mà mình đã tiến hành test thử, ổ HDD có tốc độ truy xuất chỉ khoảng 80MB/s nhưng SSD thì có tốc độ lên tới hơn 400MB/s và vài trường hợp nó sẽ tính bằng GB (ví dụ VPS tại AZDIGI dùng RAID-10 nên tốc độ sẽ lên tới gần 2GB/s).

**4.CPU Core**

CPU Core nghĩa là lõi xử lý của CPU. Một Dedicated Server có số lượng core nhất định và nó sẽ được chia cho các VPS. Thường thì số core càng cao thì khả năng xử lý dữ liệu càng tốt.

Ở các gói VPS, trung bình sẽ được chọn từ loại 1 core đến 6 cores.

**5.Bandwidth**

Băng thông cũng như 1 con đường, nếu băng thông lớn, tương tự như một con đường rộng, nhiều người có thể đi qua, tình trạng tắc nghẽn khó xảy ra và ngược lại.

Các nhà cung cấp băng thông thường cung cấp lượng băng thông tối thiểu 10 – 20 Mbps

**6.Up-time**

Thời gian up-time của VPS thường được ước lượng từ thời gian hoạt động của nó. Thời gian hoạt động của VPS từ 99,95 đến 99,9% thì bạn đều có thể chấp nhận mua được.

**7.Hệ điều hành**

Hầu hết các dịch vụ cung cấp VPS sẽ hỗ trợ các loại điều hành sau đây:

- CentOS (Linux)

- Ubuntu (Linux)

- Debian (Linux)
- Fedora (Linux)

- Windows Server (Windows)

###Ưu điểm


- Toàn quyền quản lý với tính năng như một máy chủ độc lập.

- Độ ổn định và bảo mật cao.

- Dễ dàng nâng cấp tài nguyên mà không làm gián đoạn dịch vụ.

- Quản trị từ xa, cài đặt các phần mềm và ứng dụng theo nhu cầu

- Cài đặt lại hệ điều hành nhanh, chỉ từ 5-10 phút

- Tiết kiệm được chi phí đầu tư máy chủ.

###Nhược điểm

- Hoạt động của VPS bị ảnh hưởng bởi hoạt động và độ ổn định của máy chủ vật lý tạo ra VPS.

-  Việc sử dụng chung máy chủ vật lý khiến VPS của bạn bị phụ thuộc.

-  Tốn thời gian và chi phí để nâng cấp tài nguyên và cũng không thể mở rộng nhiều.

-  Cách thức vận hành và năng suất hoạt động của VPS không đạt được hiệu quả như mong muốn.

<a name="2"></a>
#2.Cloud VPS

<p align="center"><img src="http://hostuserver.com/image/cloudvps.jpg" /></p>

Cloud VPS là một hệ thống được xây dựng trên nền tảng điên toán đám mây cloud sử dụng công nghệ vmware. Cloud Vps là một giải pháp lưu trữ web, bạn hãy thử tưởng tượng nếu một máy chủ web có thể uptime 99,99% thời gian hoạt động với hệ thống dự phòng đầy đủ và khả năng mở rộng cao.Cloud server có tính năng khôi phục và thay thế ngay khi một vps xảy ra sự cố. Đặc biệt với hệ thống lưu trữ dữ liệu tập trung SAN “Storage Area Network” giúp giảm thiểu thời gian bảo trì và khả năng nâng cấp mở rộng dung lượng lưu trữ lên đến hơn 1000 TB.


#### Những tính năng vượt trội của Cloud VPS

###Tính sẵn sàng cao.​

- Các VPS thông thường được host trên 1 máy chủ vật lý, nên nếu có sự cố xảy ra với máy chủ này thì các VPS đều bị ảnh hưởng.

- Còn đối với các VPS cloud, thì các VPS được host trên 1 hệ thống gồm nhiều máy chủ vật lý, nên giả sử 1 VPS  host ở 1 trong các máy chủ đó, mà máy chủ đó gặp sự cố, thì VPS đó tự động được chuyển qua host trên 1 máy khác trong hệ thống. Điều này đảm bảo được tính sẵn sàng cho VPS.

###Thuận tiện trong việc quản lý.​

- Các dịch vụ VPS thông thường hiện nay đa số chỉ cung cấp cho khách hàng tài khoản admin hay root để khách hàng truy cập từ xa. Các công việc như khởi động , backup, cài lại OS thì khách hàng phải gửi yêu cầu lên nhà cung cấp dịch vụ. Có chỗ làm miễn phí nhưng cũng có chỗ tính phí. Nói chung là khách hàng không được chủ động.

- Còn trên VPS cloud, khách hàng được cung cấp tài khoản portal, khách hàng có thể chủ động khởi động, tắt, backup, cài lại OS từ image ở local hoặc có sẵn trên hệ thống. Khách hàng sẽ được chủ động trong mọi tình huống.

###Khả năng mở rộng linh hoạt.​

- Các VPS thông thường được host trên 1 máy chủ riêng lẻ, khi khách hàng muốn nâng cấp VPS , nếu máy chủ đó vẫn còn tài nguyên thì không sao, nhưng nếu máy chủ đang hết tài nguyên dự trữ thì việc nâng cấp lên sẽ gián đoạn VPS 1 khoảng thời gian , tuy là không nhiều.

- Còn đối với các VPS cloud thì tài nguyên dự trữ là rât nhiều và lúc nào cũng sẵn sàng để nâng cấp VPS, việc cấp phát cũng rất nhanh chóng.

<a name="3"></a>
#3.Giao diện quản trị VPS

Đây là trang quản trị VPS tại hostvn.net. Cho biết các thông số của VPS

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/1.png)


![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/2.png)

###Một số thao tác với VPS

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/2.png) Khởi động VPS

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/3.png) Dừng VPS

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/4.png) Tắt VPS

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/5.png) Khởi động lại VPS

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/2.png) Cài lại hệ điêu hành cho VPS

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/2.png) Mở giao diện điều khiển. Click vào và bắt đầu Login với tài khoản của hostvn đã cung cấp.

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/9.png)

###Một số Tools

**Quản lý Firewall**

Click vào ![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/10.png) sẽ di chuyển đến trang quản lý Firewall ở đây có thêm các rules.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/15.png" /></p>

**Quản lý IP**

Click vào ![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/11.png)  để di chuyển đến trang quản lý IP để xem thông tin IP của VPS

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/16.png" /></p>

<a name="4"></a>
#4.Cài đặt SSH và SSH bằng public key

Nhập lệnh sau để cài đặt ssh ``apt-get ínstall openssh-server``

Tạo thư mục chứa Public Key trên Server từ Client, ví dụ:

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

Đến đây kể như hoàn tất Client đã có Private Key, trên Server đã có Public Key nhưng kết nối vẫn xác thực theo Password Authentication. Tìm đến file /etc/ssh/sshd_config hiệu chỉnh thông số như sau.

```
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no 
```
<a name="5"></a>
#5.Một số thao tác thực hành qua SSH

###Kiểm tra cấu hình

**Kiểm tra IP**

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/16.png" /></p>

**Hostname và Version**

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/18.png" /></p>

**Kiểm tra phần cứng**

Xem CPU gì và tốc độ ra sao, có bao nhiêu nhân hay bao nhiêu CPU vật lý.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/19.png" /></p>

 Dung lượng các ổ cứng


<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/20.png" /></p>

###Upgrade to Ubuntu 16.04

Nhập lệnh sau ```do-release-upgrade --devel-release``` để nâng cấp. Hoàn thành nâng cấp

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task40_VPS_Usage/Images/21.png" /></p>

###Cài đặt Opencart

tham khảo https://github.com/thanhnhut/sysadmin_level1/tree/master/Task25_Ubuntu_LAMP_And_OpenCart






<a name="6"></a>
#6.Tham Khảo

https://vi.wikipedia.org/wiki/M%C3%A1y_ch%E1%BB%A7_%E1%BA%A3o

https://longvan.net/vps-la-gi-vps-duoc-dung-de-lam-gi.html

http://vdo.vn/hoi-dap/sanh-giua-cloud-server-va-may-chu-ao-vps.html

https://thachpham.com/hosting-domain/cam-nang-thue-vps.html

