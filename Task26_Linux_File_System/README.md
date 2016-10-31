## Linux File System


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **30/10/2016**

### Mục lục
[1. Cấu trúc cây thư mục](#1)

[2.File System](#2)

[3. Các thao tác cơ bản Fdisk](#3)


---

<a name="1"></a>
#1. Cấu trúc cây thư mục

Thư mục có thể chứa các thư mục khác cũng như các tập tin thông thường, đó là những "lá" của cây. 

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task26_Linux_File_System/Images/1.png" /></p>

|Danh mục|Mô tả|
|----------|-------|
|**/bin**|là nơi phổ biến nhất sử dụng lệnh terminal, giống như ls, mount, rm, etc.|
|**/boot**|chứa các tập tin cần thiết để khởi động hệ thống, bao gồm các Linux kernel , một hình ảnh đĩa RAM và bộ nạp khởi động các file cấu hình|
|**/dev**|chứa tất cả các tập tin thiết bị, mà không phải là tập tin thông thường nhưng thay vì tham khảo các thiết bị phần cứng khác nhau trên hệ thống, bao gồm cả các ổ đĩa cứng|
|**/etc**|chứa các tập tin cấu hình hệ thống, ảnh hưởng đến hành vi của hệ thống cho tất cả người dùng|
|**/home**|đây là nơi dành cho các thư mục home của người dùng|
|**/lib**|chứa các thư viện động rất quan trọng và mô-đun hạt nhân|
|**/media**|được dự định như là một điểm gắn kết cho các thiết bị bên ngoài, chẳng hạn như ổ cứng hoặc thiết bị lưu trữ (đĩa mềm, đĩa CD, DVD)|
|**/mnt**|cũng là nơi để gắn kết điểm, nhưng dành riêng cho các thiết bị "tạm thời gắn kết", chẳng hạn như hệ thống tập tin mạng|
|**/opt**|có thể được sử dụng để lưu trữ phần mềm bổ sung cho hệ thống của bạn, mà không được xử lý bởi các package manager|
|**/proc**|là một hệ thống tập tin ảo cung cấp một cơ chế cho hạt nhân để gửi thông tin đến các quá trình|
|**/root**|là superuser thư mục của home, không phải trong / home / để cho phép khởi động hệ thống ngay cả khi / home / không có sẵn|
|**/sbin**|chứa các lệnh hành chính quan trọng mà nên thường chỉ được sử dụng bởi các superuser|
|**/srv**|có thể chứa các thư mục dữ liệu của các dịch vụ như HTTP (/ srv / www /) hoặc FTP|
|**/tmp**|là một nơi cho các tập tin tạm thời được sử dụng bởi các ứng dụng|
|**/usr**|chứa phần lớn các tiện ích người dùng và các ứng dụng, và một phần tái tạo cấu trúc thư mục gốc, chứa vài thư mục trong số những thư mục khác, / usr / bin / và / usr / lib.|
|**/var**|là dành riêng cho các biến dữ liệu, chẳng hạn như các bản ghi, cơ sở dữ liệu, các trang web, và ống chỉ tạm thời (e-mail etc) các tập tin mà vẫn tồn tại từ một khởi động tiếp theo. Một thư mục đáng chú ý nó chứa là / var / log nơi các tập tin đăng nhập hệ thống được lưu giữ.|

<a name="2"></a>
#2. File System

- Hệ thống tập tin là một trong những điều mà bất kỳ người mới dùng linux phải làm quen. Trong thế giới của Microsoft, bạn không bao giờ thực sự phải lo lắng về nó, mặc định là NTFS. Tuy nhiên Linux, được xây dựng trên một thế giới mã nguồn mở, không giới hạn theo cách này và do đó người dùng cần phải có một sự hiểu biết về những gì một hệ thống tập tin, và làm thế nào nó ảnh hưởng đến máy tính.

- Một hệ thống file (file system) là một kiểu lưu trữ và tổ chức các file và dữ liệu trong file để dễ tìm kiếm và truy cập. Hiện tại trong Linux phổ biến hai kiểu hệ thống file là ext3 và ext4.

- Một hệ thống file là một cây thư mục bao gồm một thư mục gốc (/), các thư mục con và các file chứa trong đó.

- Trên mỗi partition chỉ có thể có một kiểu hệ thống file (được tạo ra khi format: ext3, ext4, fat, ntfs, …). Nhưng một cây thư mục có thể đặt trên nhiều partition: thư mục gốc / đặt ở partition sda2, thư mục /home đặt ở sda5, v.v… tùy ý người dùng chọn khi cài đặt.

- Các kiểu hệ thống file:

 - Hệ thống file ổ cứng (Disk file systems): FAT, NTFS, ext2/3/4, HFS, …
 - Riêng file trong Compact Disk hoặc DVD lưu theo hệ thống file ISO 9660 hoặc UDF. Từ Linux 2.6 và Windows Vista, đĩa DVD có thể ghi theo format - Mount Rainier (mở rộng của UDF) như đĩa mềm.
 - Hệ thống file flash (Flash file systems): tối ưu cho ghi vào bộ nhớ flash (ổ USB).
 - Hệ thống file mạng (Network file systems): SMB, NFS.
 - Hệ thống file ổ cứng mạng (Shared disk file systems): dùng truy cập các file lưu trên các cụm ổ cứng trong mạng (SAN). Thuộc loại này có GFS của Red Hat, GPFS của IBM.
và nhiều thứ nữa …..

- Đây là một so sánh rất ngắn gọn về các hệ thống tập tin phổ biến nhất được sử dụng với thế giới Linux

|File System|Max File Size|Max Partition Size|Journaling|Notes|
|-----------|-------------|------------------|----------|-----|
|Fat16|2 GiB|2 GiB|No|Legacy|
|Fat32|4 Gib|8 Gib|No|Legacy|
|NTFS|2 TiB|256 Tib|Yes|(Đối với Windows Compatibility) NTFS-3G được cài đặt theo mặc định trong Ubuntu, cho phép đọc / ghi hỗ trợ|
|ext2|2 TiB|32 TiB|No|Legacy|
|ext3|2 TiB|32 TiB|Yes|hệ thống tập tin Linux tiêu chuẩn cho nhiều năm. sự lựa chọn tốt nhất để cài đặt siêu chuẩn.|
|ext4|16 GiB|1 EiB|Yes|là phiên bản hiện đại của ext3. sự lựa chọn tốt nhất cho việc cài đặt mới, nơi siêu chuẩn là không cần thiết.|
|reiserFS|8 TiB|16 TiB|Yes|Không còn duy trì tốt.|
|JFS|4 PiB|32 PiB|Yes(metadata)|Tạo bởi IBM - Không duy trì tốt.|
|XFS|8 EiB|8 EiB|Yes(metadata)|Tạo bởi SGI. sự lựa chọn tốt nhất cho một kết hợp của sự ổn định và ghi nhật ký tiên tiến|

<a name="3"></a>
#3. Các thao tác cơ bản với Fdisk

###Xem tất cả các phân vùng đĩa 

Sử dụng câu lệnh **sudo fdisk -l** để liệt kê danh sách phân vùng có sẵn của hệ thống

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task26_Linux_File_System/Images/2.png" /></p>

###Xem phân vùng đĩa cụ thể

Thêm tên ổ vào sau lệnh **sudo fdisk -l** vd

###Kiểm tra tất cả các lệnh fdisk có sẵn

Nếu bạn muốn xem tất cả các lệnh trong đó có sẵn cho fdisk. Đơn giản chỉ cần sử dụng lệnh sau đây bằng cách nhắc đến tên đĩa cứng như / dev / sda như hình dưới đây.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task26_Linux_File_System/Images/4.png" /></p>

Gõ 'm' để xem danh sách tất cả các lệnh có sẵn của fdisk có thể hoạt động trên đĩa cứng / dev / sda.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task26_Linux_File_System/Images/5.png" /></p>

###Xem tất cả bảng phân vùng


Từ chế độ lệnh, hãy nhập 'p' thay vì 'm' như chúng ta đã làm trước đó.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task26_Linux_File_System/Images/6.png" /></p>

###Xóa một phân vùng

Để xóa một phân vùng, sử dụng lệnh “d“. Bạn sẽ được hỏi lựa chọn phân vùng để xóa. Danh sách phân vùng có thể được xem ở lệnh “p“. Ví dụ, tôi muốn xóa phân vùng /dev/sda5, thì gõ vào số 5.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task26_Linux_File_System/Images/7.png" /></p>


###Tạo phân vùng mới

Đẻ tạo mới một phân vùng, gõ lệnh “n“. Bạn sẽ có hai tùy chọn, tạo phân vùng logic (gõ “l“) hoặc phân vùng primary (gõ “p“). Lưu ý rằng, một ổ đĩa chỉ có tối đa 4 phân vùng primary.

Tiếp theo, xác định sector mà bạn muốn bắt đầu phân vùng. Ấn Enter để chấp nhận thiết lập mặc định.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task26_Linux_File_System/Images/8.png" /></p>


Cuối cùng, xác định sector cuối của phân vùng. Ấn Enter để chấp nhận sử dụng hết phần ổ đĩa còn trống. Thay vì chỉ định sector, bạn có thể chỉ định kích thước, chữ viết tắt tương ứng: K – Kilobyte, M – Megabyte và G – Gigabyte. Ví dụ, gõ “+5G” cho phân vùng với kích thước 5 Gigabyte. Nếu bạn không gõ đơn vị sau dấu “+”, fdisk sẽ lựa chọn sector làm đơn vị. Ví dụ, nếu bạn gõ “+10000”, fdisk sẽ cộng thêm 10000 sector để làm điểm kết thúc của phân vùng.

###Đinh danh phân vùng

Bạn phải định dạng (format) phân vùng trước khi sử dụng. Bạn có thể làm điểu này với lệnh mkfs thích hợp. Ví dụ, câu lệnh sau sẽ định dạng phân vùng thứ 5 của ổ đĩa đầu tiên với hệ thống tệp tin Ext4 vd

```
sudo fdisk.ext4 /dev/sda5/
```

###Kiểm tra kích thước một phân vùng

Sau khi định dạng phân vùng mới, kiểm tra kích thước của phân vùng sử dụng lệnh

```
sudo fdisk -s /dev/sda5
```

###Thay đổi loại phân vùng

Nếu muốn thay đổi loại của phân vùng, bạn gõ “t” và chỉ định số thứ tự của phân vùng đó.

Bạn sẽ được yêu cầu nhập vào mã hexa của loại tương ứng. Nếu không rành về điều này, gõ “l” để tra danh sách mã hexa tương ứng.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task26_Linux_File_System/Images/9.png" /></p>

Ghi lại những thay đổi:

- Gõ “w” để ghi lại những thay đổi vào đĩa.

- Gõ “q” để thoát mà không lưu lại.




