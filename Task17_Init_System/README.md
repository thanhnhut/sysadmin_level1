## Tìm hiểu Init System

> 
> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **4/9/2016**

##1.SystemD

SystemD là một hệ thống và quản lý dịch vụ cho Linux, tương thích với SysV và LSB init script. Systemd cung cấp khả năng song song mạnh mẽ, sử dụng ổ cắm và D-Bus kích hoạt cho các dịch vụ bắt đầu, cung cấp xuất theo yêu cầu của daemon, theo dõi các quá trình sử dụng cgroups Linux, hỗ trợ snapshotting và phục hồi tình trạng hệ thống, duy trì gắn kết  automount điểm và thực hiện một xây dựng giao dịch logic phụ thuộc dựa trên điều khiển dịch vụ. Nó có thể làm việc như một sự thay thế cho sysvinit.

###Cách thức hoạt động

Các Systemd mới bắt đầu daemon tại cùng một thời gian và chạy song song này của daemon có nghĩa là một khởi động rất nhanh, systemd sử dụng ổ cắm cho tất cả các dịch vụ. Nó thiết lập ổ cắm cho daemon và phối giữa chúng khi chúng bắt đầu lên. Vì vậy, khi một daemon yêu cầu hỗ trợ từ daemon khác, systemd phối hợp các dữ liệu từ ổ cắm của chúng. Ví dụ, daemon A bắt đầu và nó cần một sự hỗ trợ từ daemon B, tuy nhiên, daemon B đã chưa bắt đầu. Do đó, systemd viết yêu cầu daemon A tới daemon ổ cắm B (đệm) và nó tiếp tục. Vì vậy daemon A không cần phải chờ đợi cho daemon B. Ngay khi daemon B bắt đầu, nó sẽ đọc socket của nó. Điều này có nghĩa là xử lý song song và hệ thống khởi động rất nhanh. Việc kích hoạt ổ cắm được thiết kế bởi hệ điều hành OS X của Apple. 

###Các câu lệnh của systemd

**Làm thế nào để bắt đầu / dừng hoặc kích hoạt / vô hiệu hóa các dịch vụ?**

Kích hoạt một dịch vụ ngay lập tức:

```
  systemctl start foo 
```

Hủy kích hoạt một dịch vụ ngay lập tức:
```
  systemctl stop foo

```   

Khởi động lại một dịch vụ:
```
  systemctl restart foo 
```
Hiển thị trạng thái của một dịch vụ bao gồm cả cho dù nó đang chạy hay không:
```
   systemctl  status foo
```
Cho phép một dịch vụ sẽ được bắt đầu vào lúc khởi động:
```
  systemctl enable foo 
```
Vô hiệu hóa một dịch vụ để không bắt đầu trong quá trình khởi:
```
  systemctl disable foo 
```
Ngăn chặn một dịch vụ này khởi động hoặc thậm chí tay, trừ khi lột mặt nạ:
```
  systemctl mask foo 
```
Kiểm tra xem một dịch vụ đã được kích hoạt hay không:
```
  systemctl is-enable foo 
```

**Làm thế nào để thay đổi target (runlevel)?**

systemd có khái niệm về các mục tiêu đó là một sự thay thế linh hoạt hơn cho runlevel trong sysvinit.

Runlevel3 được mô phỏng bởi multi-user.target. Runlevel5 được mô phỏng bởi graphical.target. runlevel3.target là một liên kết tượng trưng đến multi-user.target và runlevel5.target là một liên kết tượng trưng đến graphical.target.

Bạn có thể chuyển sang 'runlevel 3' bằng cách chạy
```
  systemctl isolate multi-user.target 
```
Bạn có thể chuyển sang 'runlevel 5' bằng cách chạy
```
  systemctl isolate graphical.target 
```
**Làm thế nào để thay đổi mục tiêu mặc định?**
```
  systemctl set-default <tên của target> .target
```

**Làm thế nào để tôi biết các mục tiêu hiện tại?**
```
  systemctl set-default 
```

** Có hoạt động lệnh dịch vụ với systemd**

Có. Nó đã được sửa đổi để gọi systemctl tự động khi đối phó với các tập tin dịch vụ systemd. Vì vậy, một trong các lệnh sau đây không cùng một kiểu

```
systemctl stop NetworkManager
```

hoặc là 

```
service NetworkManager stop
```

Có, bật dịch vụ / tắt, tính tương thích đã được cung cấp cả hai cách. chkconfig đã được sửa đổi để gọi systemctl khi giao dịch với các tập tin dịch vụ systemd. Cũng systemctl tự động gọi chkconfig khi giao dịch với một tập tin sysv init truyền thống.

Vì vậy, một trong các lệnh sau đây không cùng một kiểu
```
  systemctl disable NetworkManager 
```
hoặc là
```
  chkconfig NetworkManager off
```   

**Làm thế nào để thay đổi số lượng Gettys chạy theo mặc định?**

Cách đơn giản nhất là để chỉnh sửa /etc/systemd/logind.conf:
```
 [Login]
 ...
 NAutoVTs = 8
```
Thiết lập này sẽ có hiệu lực sau khi khởi động lại.

Ngoài ra, getty @ .services mà mở cửa sổ đăng nhập có thể được kích hoạt và bắt đầu cá nhân.

Để thêm getty khác:
```
 systemctl enable getty @ tty8
 systemctl start getty @ tty8
```
Để loại bỏ một getty:
```
 systemctl disable getty @ tty8
 systemctl stop getty @ tty8
```
systemd không sử dụng / etc / inittab.

**Làm thế nào để thiết lập tự động đăng nhập vào một giao diện điều khiển terminal ảo?**

Đầu tiên tạo ra một dịch vụ mới tương tự như getty @ .service:
```
 # Cp /lib/systemd/system/getty@.service \
      /etc/systemd/system/autologin@.service
 # Ln -s /etc/systemd/system/autologin@.service \
         /etc/systemd/system/getty.target.wants/getty@tty8.service
```
sau đó chỉnh sửa ExecStart, Restart và Alias ​​giá trị, như thế này:
```
 ...
 ExecStart = - / sbin / mingetty --autologin USERNAME% I
 Khởi động lại = không
 ...
 Alias=getty.target.wants/getty@tty8.service
```
và cuối cùng  daemon lại và bắt đầu các dịch vụ:
```
 systemctl daemon-reload
 systemctl start getty@tty8.service
```
Lưu ý rằng nếu bạn thoát khỏi phiên tty8, bạn sẽ không thể sử dụng nó cho đến khi khởi động lại hoặc khởi động bằng tay của systemctl, trừ khi bạn để  Khởi động lại như 'always', nhưng  nên tránh điều này theo lý do an ninh.

**Làm thế nào để tùy chỉnh một tập tin đơn vị / thêm một tập tin đơn vị tùy chỉnh?*

Cách tốt nhất để tùy chỉnh các file đơn vị là thêm /etc/systemd/system/foobar.service.d/*.conf nơi foobar.service là tên của dịch vụ mà bạn muốn tùy chỉnh. Nếu một thư mục không tồn tại, tạo ra một và thả một file conf với các thiết lập mà bạn muốn ghi đè lên. Ví dụ,

/etc/systemd/system/httpd.service.d/restart.conf
```
 [Service]
 Restart = always
 RestartSec = 30
```

**Đừng quên để tải lại daemon systemd sử dụng systemctl daemon-reload và systemctl restart foobar sau khi chỉnh sửa một tập tin đơn vị nơi foobar là tên của đơn vị. Cũng lưu ý rằng bạn có thể systemd-delta để liệt kê các tập tin đơn vị đã được tùy biến và cũng có những khác biệt chính xác**

Chăm sóc đặc biệt phải được thực hiện khi trọng tùy chọn có thể được thiết lập lần muliple ( ExecStart , ExecStartPre , ExecStartPost là một ví dụ phổ biến). Gán một số giá trị cho các tùy chọn gắn thêm vào danh sách hiện có, trong khi assiging giá trị rỗng reset danh sách.

Ví dụ, giả sử chúng ta có một tập tin dịch vụ như thế này:
```
 [Service]
 ExecStart = /bin/echo execstart1 
 ExecStart =
 ExecStart = /bin/echo execstart2 
 ExecStartPost = /bin/echo post1 
 ExecStartPost = /bin/echo post2
``` 
Khi bắt đầu, dịch vụ này sẽ in
```
 execstart2
 post1
 post2
```
Các quy tắc tương tự áp dụng cho các đoạn trích trong thư mục ".d". Điều này có nghĩa rằng các đoạn đó ghi đè ExecStart và các thiết lập tương tự, thường nên bắt đầu với việc chuyển nhượng trống ExecStart= , tiếp theo là thiết lập mới. 

###Vị trí lưu file cấu hình

- /usr/lib/systemd/system/  đơn vị cung cấp bới các gói cài đặt

- /etc/systemd/system/ đơn vị cung cấp bởi người quản trị hệ thống

###Những dòng hệ điều hành sử dụng systemd

- Fedora

- Mageia

- OpenSuSe

- Arch Linux

- Debian 

- Ubuntu

- Core OS

- CentOS

- Red Hat Enterprise Linux

- SUSE Linux Enterprise Server

###Ưu điểm

- Thiết kế sạch sẽ, đơn giản và hiệu quả

- Xử lý đồng thời và song song khi khởi động

- APIv tốt hơn

- Cho phép loại bỏ các quy trình bắt buộc

- Hỗ trợ sự kiện khai thác gỗ sử dụng journald

- Hỗ trợ lập lịch công việc sử dụng tính giờ lịch systemd

- Lưu trữ các bản ghi trong các tập tin nhị phân

- Bảo quản của nhà nước systemd để tham khảo trong tương lai

- Tích hợp tốt hơn với GNOME cộng thêm nhiều hơn


