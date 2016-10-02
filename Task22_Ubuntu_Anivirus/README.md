


## Tìm hiểu Anti Virus


> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **2/10/2016**

---

##Mục lục

[1. ClamAV](#1)

- [1.1 Giới thiệu](#11)

- [1.2 Tính năng và đặc điểm](#12)

- [1.3 Cài đặt ClamAV trên Ubuntu](#13)

- [1.4 Cài đặt ClamAV trên CentOS](#14)

[2. Linux Malware Detect](#2)

- [2.1 Gi ớithiệu](#21)

- [2.2 Tính năng](#22)

- [2.3 Cài đặt](#23)


<a name="1"></a>
#1. ClamAV 


<a name="11"></a>
###1.1 Giới thiệu

Clam AntiVirus (ClamAV) là miễn phí và mã nguồn mở , nền tảng phần mềm chống virus công cụ có thể phát hiện nhiều loại phần mềm độc hại, bao gồm cả virus . Một trong những mục đích chính của nó là trên các máy chủ mail như một server-side quets email-virus . Các ứng dụng được phát triển cho Unix và có các phiên bản của bên thứ ba có sẵn cho AIX , BSD , HP-UX , Linux , OS X , OpenVMS , OSF (Tru64) và Solaris . Với phiên bản 0.97.5, ClamAV xây dựng và chạy trên Microsoft Windows .  Cả hai ClamAV và cập nhật của nó được cấp miễn phí.

![1](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task22_Ubuntu_Antivirus/images/1.png)

ClamAV bao gồm một số tiện ích: một máy quét dòng lệnh, cập nhật cơ sở dữ liệu tự động và đa luồng khả năng mở rộng daemon ., Chạy trên một công cụ chống virus từ một thư viện chia sẻ 



Các sở dữ liệu virus ClamAV được cập nhật ít nhất bốn giờ và đến ngày 25 tháng 12 năm 2014 chứa trên 3.700.000 chữ ký virus với số DB cập nhật Virus hàng ngày tại 19837.


<a name="12"></a>
###1.2 Tính năng

- Hổ trợ quét theo dòng lệnh

- Quét theo lịch đặt sẵn 

- Quét nhanh, daemon đa luồng với sự hổ trợ cho việc quét truy cập 

- Sử dụng giao diện milner cho send mail

- Năng cao cơ sở dữ liệu cập nhật với sự hổ trợ các bản cập nhật và chữ ký số

- Truy cập quets Linux vá BSD free

- Cở sở dữ liệu virus được cập nhật nhiều lần trong ngày

- Tích hợp hổ trọ cho các định dạng lưu trữ khác nhau

- Tích hợp hổ trợ cho thực thi ELF và các tập tin thực thi portable nén với UpX, FSG. Nspack, wwpack32, MEW, Upack obfuscated với SUE. Y0da Crytor và các định dạng khác.

- Tich hợp hổ trợ cho các định dạng tài liệu phổ biến bao gồm MS Office và MAC Office hình ảnh HTML, RDF và PDF ....

**Hạn chế**

ClamAV không hổ trợ cơ chế bảo vệ thời gian thực nên khi chúng ta có nghi ngờ về virus, malware, toolkit,...  thì có thể khởi động ClamAV lên quét. Hoặc có thể dựa vào cơ chế đặt lịch quét mà ClamAV đã hổ trợ trên.


<a name="13"></a>
###1.3 Cài đặt ClamAV trên Ubuntu

ClamAV có thể được tìm thấy cho Ubuntu trong kho apt. Chạy lệnh này để cài đặt ClamAV:
```
apt-get install clamav (Terminal version)
apt-get install clamtk (GUI version) 
```

Nếu bạn cần clamd, bạn cũng có thể muốn chạy:
```
apt-get install clamav-daemon
```
Nếu bạn cần hỗ trợ cho các chức năng quét các tập tin nén RAR lần đầu tiên bạn cần phải kích hoạt các kho lưu trữ không tự do, và sau đó bạn có thể cài đặt RAR-plugin sử dụng:
```
apt-get install libclamunrar6

```

<a name="14"></a>
###1.4 Cài đặt ClamAV trên CentOS 7/6

Cài đặt ClamAV sẽ giúp cho Linux Malware Detect scan nhanh và hiệu quả hơn.

Đầu tiên cần tạo cài đặt repo Epel
```
yum install epel-release
```
Sau đó tiến hành cài đặt:
```
yum update && yum install clamd
```

Sau khi cài đặt xong các  có thể sử dụng lệnh sau để quét trên hệ thống
```
#clamscan -r <đường dẫn các bạn muốn quyét>
```
Ví dụ: #clamscan -r /home

Mình cũng xin hướng dẫn thêm cho các bạn một số tùy chọn kèm theo để tiện cho cách bạn tham khảo

- --log=<đường dẫn đến file> : option giúp bạn lưu lại phần report vào một file các bạn phải tạo file trước khi chạy để tránh phát sinh lỗi

- --remove=[yes/no] : option này giúp bị xóa hoặc không xóa file clamav scan được

- --move=<đường dẫn lưu trữ>: di chuyển tất cả các file có nội dung malware sang một đường dẫn khác để cách ly

- --copy=<đường dẫn lưu trữ>: tạo ra một nhân bản để lưu trữ lại

- --help: hướng dẫn


<a name="2"></a>
#2. Linux Malware Detect (LMD)

<a name="21"></a>
###2.1 Giới thiệu 

Linux phần mềm độc hại phát hiện (LMD) là một máy quét phần mềm độc hại cho Linux phát hành theo giấy phép GNU GPLv2, được thiết kế xung quanh các mối đe dọa đối mặt trong môi trường lưu trữ chia sẻ. Nó sử dụng dữ liệu mối đe dọa từ các hệ thống phát hiện xâm nhập cạnh mạng để trích xuất phần mềm độc hại đang tích cực được sử dụng trong các cuộc tấn công và tạo ra chữ ký để phát hiện. Ngoài ra, dữ liệu mối đe dọa cũng có nguồn gốc từ đệ trình sử dụng với các tính năng thanh toán LMD và từ các nguồn lực của cộng đồng phần mềm độc hại. Các chữ ký mà sử dụng LMD là băm tập tin MD5 và mô hình HEX phù hợp, họ cũng dễ dàng xuất khẩu sang bất kỳ số lượng các công cụ phát hiện như ClamAV.

<a name="22"></a>
###2.2 Tính năng và đặc điểm

- Phát hiện tập tin MD5 băm để xác định mối đe dọa nhanh chóng 

- HEX dựa mô hình phù hợp để xác định các mối đe dọa biến thể 

- Thành phần phân tích thống kê để phát hiện các mối đe dọa làm rắc rối (ví dụ: base64) 

- Phát hiện tích hợp của ClamAV để sử dụng làm công cụ quét để tăng hiệu suất 

- Chữ ký tích hợp cập nhật tính năng với -u | -Update 

- Tích hợp tính năng cập nhật phiên bản với -d | -Update-ver 

- Quét-gần đây chọn lựa chỉ để quét các tập tin đã được thêm vào / thay đổi trong ngày X 

- Quét-tất cả các tùy chọn để quét đường dẫn đầy đủ dựa 

- Tùy chọn thanh toán để tải lên nghi ngờ phần mềm độc hại để rfxn.com để xem xét / băm 

- Hệ thống báo cáo đầy đủ để xem kết quả quét hiện tại và trước 

- Hàng đợi kiểm dịch mà các cửa hàng các mối đe dọa một cách an toàn không có quyền 

- Tùy chọn trộn kiểm dịch để kiểm dịch các kết quả của một quét hiện tại hay quá khứ 

- Kiểm dịch khôi phục tùy chọn để khôi phục các file con đường ban đầu, chủ sở hữu và perms 

- Kiểm dịch tạm đình chỉ lựa chọn tài khoản để Cpanel đình chỉ hoặc thu hồi vỏ người dùng 

- Quy tắc sạch hơn để cố gắng loại bỏ các phần mềm độc hại tiêm dây 

- Tùy chọn trạm trộn sạch hơn để cố gắng làm sạch báo cáo quét trước 

- Quy tắc sạch để loại bỏ phần mềm độc hại base64 và gzinflate (base64 tiêm 

- Hàng ngày cron dựa quét của tất cả các thay đổi trong 24 giờ qua ở homedirs người dùng 

- Cron script hàng ngày tương thích với các hệ thống theo phong cách cổ RH, Cpanel & Ensim 

- Hạt nhân dựa inotify thời gian thực quét tập tin của tạo / chỉnh sửa / chuyển file 

- Kernel màn inotify rằng có thể mất dữ liệu đường dẫn từ STDIN hoặc FILE 

- Hạt nhân inotify tính năng màn hình thuận tiện cho người sử dụng hệ thống giám sát 

- Hạt nhân inotify màn hình có thể được hạn chế một gốc html sử dụng cấu hình 

- Hạt nhân inotify giám sát với giới hạn sysctl động cho hiệu suất tối ưu 

- Hạt nhân inotify cảnh báo thông qua các báo cáo hàng tuần hàng ngày và / hoặc tùy chọn 
báo cáo cảnh báo e-mail sau mỗi lần thực hiện quét (bằng tay & hàng ngày) - 

- Con đường, mở rộng và dựa trên chữ ký bỏ qua tùy chọn 

- Tùy chọn quét nền cho các hoạt động quét tự động 

- Tiết đăng nhập và đầu ra của tất cả các hành động


<a name="23"></a>
###2.3 Cài đặt LMD 

**Tải về và giải nén**

```
wget http://www.rfxn.com/downloads/maldetect-current.tar.gz
tar -xvf maldetect-current.tar.gz
```
**Vào thư mục và cài đặt**

```
cd maldetect-1.5
./install.sh
```
**Cấu hình LMD**
```
sudo vi /usr/local/maldetect/conf.maldet
```

điều chỉnh một vài tham số như sau:
```
email_alert="1" 
email_addr="youremail@localhost" 
quarantine_hits="1" 
quarantine_clean="1" 
quarantine_suspend_user="1" 
scan_clamscan="1"
```





**Lệnh sử dụng Linux Malware Detect**

- Để scan một thư mục cụ thể trên VPS, bạn có thể sử dụng lệnh sau:
```
maldet -a /home/domain.com
```
Bạn tùy thay /home/domain.com bằng đường dẫn folder của bạn.
- Update LMD bằng lệnh:
```
maldet -u
```
- Lệnh View report:

```
maldet --report 14715-1421.3219
```

**Quét virus bằng giao diện**

![3](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task22_Ubuntu_Antivirus/images/3.png)

**Quét virus bằng terminal**

![2](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task22_Ubuntu_Antivirus/images/2.png)
