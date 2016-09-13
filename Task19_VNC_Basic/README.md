## Tìm hiểu VNC (Virtial Network Computing)


> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **13/9/2016**

### Mục lục

[1. Giới thiệu](#1)

[2. Hoạt động](#2)

[3. Cấu hình VNC server](#3)

 - [3.1 Trên Ubuntu](#31)
 
 - [3.2 Trên CentOS 6](#32)  


---
<a name="1"></a>
#1.Giới thiệu

Trong máy tính, Virtual Network Computing (VNC) là một đồ họa chia sẻ desktop  hệ thống sử dụng các Remote Frame Buffer protocol  (RFB) để điều khiển từ xa máy tính khác. Nó truyền bàn phím chuột và các sự kiện từ một máy tính khác, chuyển tiếp các đồ họa màn hình cập nhật lại theo hướng khác, trên một mạng . 

VNC là nền tảng độc lập - có client và server cho nhiều hệ điều hành dựa trên GUI và cho Java . Nhiều client có thể kết nối đến một VNC server cùng một lúc. Sử dụng phổ biến cho công nghệ này bao gồm hỗ trợ kỹ thuật từ xa và truy cập các tập tin trên một máy tính làm việc từ một máy tính tại nhà, hoặc ngược lại.

![1](1.png)

*Logo VNC*

![2](2.png)

*VNC trong KDE 3.1*

VNC ban đầu được phát triển tại Olivetti & Oracle Lab nghiên cứu ở Cambridge, Vương quốc Anh. Các VNC gốc mã nguồn và nhiều dẫn xuất hiện đại là mã nguồn mở dưới GNU General Public License .


Có một số biến thể của VNC  trong đó cung cấp các chức năng đặc biệt của riêng mình; ví dụ, một số tối ưu hóa cho Microsoft Windows , hoặc chuyển cung cấp tập tin (không một phần của VNC thích hợp), vv Nhiều tương thích (không có tính năng gia tăng của họ) với VNC đúng theo nghĩa là một người xem một hương vị có thể kết nối với một máy chủ của người khác ; những người khác được dựa trên mã VNC nhưng không tương thích với các VNC.

VNC và RFB được đăng ký thương hiệu của RealVNC Ltd ở Mỹ và ở các nước khác.

###Một số khuyết điểm trong sử dụng VNC

Có thể có một loạt các thách thức phải đối mặt với cách sử dụng một chương trình VNC. Họ thường liên quan đến một loạt các vấn đề bảo mật tiềm năng và các vấn đề hiệu suất. Có hay không những thế mạnh lớn hơn những thách thức này phụ thuộc vào lý do của bạn để sử dụng một chương trình như vậy. Nó cũng phụ thuộc vào loại an ninh và phần mềm đã có sẵn trên mạng máy tính.

Vấn đề an ninh có thể nhanh chóng trở thành một vấn đề lớn. Không có tính năng bảo mật trên hầu hết các chương trình mạng máy tính ảo có sẵn. Ví dụ, nếu khách hàng mỏng hiện tại của bạn có chứa virus, điều này có thể làm tổn hại toàn bộ mạng của bạn. Tuy nhiên, bạn có thể tải về các chương trình bảo mật khác mà có thể giúp bảo vệ mạng của bạn. điều quan trọng là để giữ an ninh hiện tại để tránh hack mới hơn và rủi ro thấp hơn.

Một vấn đề khác là hiệu suất. Chương trình của bạn chỉ là nhanh như các kết nối Internet chậm nhất có sẵn. Nếu kết nối Internet của bạn chậm, bạn có thể có một vấn đề với chạy các chương trình trên máy khách lớn của bạn. vấn đề hiệu suất cũng sẽ có xu hướng tăng lên khi bạn sử dụng các chương trình thời gian thực và các ứng dụng tương tác.

Phức tạp có thể gây ra một số người để cho lên trên bằng cách sử dụng hệ thống mạng máy tính ảo. Nếu bạn đang sử dụng nhiều hơn một mạng, giao thức, cung cấp dịch vụ, hoặc tập hợp các thiết bị phần cứng mạng để thiết lập các đường hầm VNC , sau đó bạn có thể có một thời gian khó khăn cố gắng để làm cho chương trình làm việc cùng nhau. Bạn có thể cần phải thuê một chuyên gia để làm cho mọi công việc. Điều này đặc biệt đúng nếu các chương trình không được thiết kế để làm việc cùng nhau.

###Lợi ích của việc sử dụng một hệ thống VNC

Nếu bạn có thể tìm cách để vượt qua những thách thức bằng cách sử dụng một hệ thống mạng máy tính, sau đó không có nghi ngờ rằng bạn sẽ tận hưởng những lợi ích của hệ thống này. Ngoài việc tiết kiệm dữ liệu, các lợi ích bao gồm tiết kiệm thời gian và tiền bạc.

Bạn có thể tiết kiệm tiền trên tổng số yêu cầu phần cứng. VNC có thể cho phép bạn sử dụng một máy tính cũ để chạy một chương trình gần đây. Điều này đôi khi cho phép các doanh nghiệp để mua máy tính ít hơn. Doanh nghiệp không còn cần cùng một loại bộ nhớ ổ đĩa hoặc khả năng xử lý, cho VNC làm cho mọi thứ dễ dàng hơn.

Trong trường hợp có thảm họa, bạn có khả năng có thể khôi phục bất kỳ dữ liệu bị mất đó là trên máy tính của khách hàng lớn. Điều này là bởi vì tất cả các dữ liệu mà một máy tính để bàn ảo có được lưu trữ trong một trung tâm dữ liệu thứ cấp. Điều này cho phép bạn truy cập tất cả dữ liệu của bạn không có công việc bình thường bị gián đoạn.



<a name="2"></a>
#2.Hoạt động

- VNC server là các chương trình trên máy tính mà chia sẻ màn hình của nó. Các server thụ động cho phép các client để kiểm soát nó.

- VNC client (hoặc người xem) là chương trình đồng hồ, điều khiển và tương tác với server. Các client điều khiển server.

- VNC protocol ( RFB protocol ) là rất đơn giản, dựa trên một đồ họa nguyên thủy từ server cho client 

Các VNC server đang chạy trên không cần phải có một màn hình vật lý. Trong phương pháp vận hành bình thường một người xem kết nối tới một cổng trên máy chủ (cổng mặc định 5900). Ngoài ra một trình duyệt có thể kết nối đến server (tùy thuộc vào việc thực hiện) (cổng mặc định 5800). Và một server có thể kết nối với người xem ở chế độ "lắng nghe" trên cổng 5500. Một lợi thế của chế độ nghe là các server trang web không phải cấu hình tường lửa để cho phép truy cập trên cổng 5900 (hoặc 5800); các trách nhiệm này thuộc về người xem, đó là hữu ích nếu các máy chủ trang web không có chuyên môn máy tính, trong khi người dùng xem sẽ được dự kiến ​​sẽ được hiểu biết nhiều hơn.

VNC theo mặc định sử dụng cổng TCP 5900+ N, [6] [7] trong đó N là số hiển thị (thường là: 0 cho một màn hình vật lý). Một số hiện thực cũng bắt đầu một cơ bản HTTP máy chủ trên cổng 5800+ N để cung cấp một trình xem VNC như một applet Java , cho phép kết nối dễ dàng thông qua bất kỳ trình duyệt web Java. cổng khác nhau có thể được sử dụng miễn là cả hai client và server được cấu hình cho phù hợp. Một HTML5 VNC thực hiện khách hàng cho các trình duyệt hiện đại (không bổ sung cần thiết) tồn tại quá. 

Sử dụng VNC qua Internet hoạt động tốt nếu người dùng có một băng thông rộng kết nối ở cả hai đầu. Tuy nhiên, nó có thể yêu cầu tiên tiến NAT , tường lửa và bộ định tuyến cấu hình như cổng chuyển tiếp để các kết nối để đi qua. Một số người dùng có thể chọn để sử dụng ngay lập tức Mạng riêng ảo (VPN) các ứng dụng như Hamachi để làm cho việc sử dụng trên Internet dễ dàng hơn nhiều. Ngoài ra, một kết nối VNC có thể được thành lập như là một kết nối mạng LAN nếu VPN được sử dụng như là một proxy.

Xvnc là server Unix VNC, mà là dựa trên một tiêu chuẩn X server . Để ứng dụng Xvnc là một X "server" (tức là cửa sổ hiển thị client), và cho người sử dụng VNC từ xa nó là một VNC server. Ứng dụng có thể hiển thị bản thân trên Xvnc như thể nó là một màn hình X bình thường, nhưng họ sẽ xuất hiện trên bất kỳ người xem VNC kết nối hơn là trên một màn hình vật lý. Ngoài ra một máy (có thể là một máy trạm hoặc một máy chủ mạng) với màn hình , bàn phím và chuột có thể được thiết lập để khởi động và chạy các máy chủ VNC như một dịch vụ hoặc daemon, sau đó màn hình, bàn phím và chuột có thể được loại bỏ và máy lưu trữ trong một vị trí ngoài đường.

Ngoài ra, màn hình hiển thị được phục vụ bởi VNC không nhất thiết phải là màn hình hiển thị cùng nhìn thấy bởi một người dùng trên máy chủ. Trên các máy tính Unix / Linux có hỗ trợ nhiều phiên X11 đồng thời, VNC có thể được thiết lập để phục vụ cho một phiên X11 hiện cụ thể, hoặc để bắt đầu một trong những của riêng mình. Nó cũng có thể chạy nhiều phiên VNC từ cùng một máy tính. Trên Microsoft Windows phiên VNC phục vụ luôn luôn là phiên người dùng hiện tại.

<a name="3"></a>
#3.Cấu hình VNC server trên Ubuntu và CentOS6

<a name="31"></a>
###3.1 Trên Ubuntu

####Cài đặt VNC server

```
# apt-get -y install vnc4server  
```

####Đăng nhập với user mà bạn muốn nhưng để bảo mật nên tạo riêng 1 tài khoản để remote. 
```
adduser vncuser
```

Chọn password đăng nhập. Những thông tin tiếp theo bạn có thể nhấn Enter để mặc định.
```
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
Changing the user information for vncuser
Enter the new value, or press ENTER for the default
 Full Name []:
 Room Number []:
 Work Phone []:
 Home Phone []:
 Other []:
Is the information correct? [Y/n] y
```

Để thay đổi pass user bạn chọn
```
passwd vncuser
```

Giờ hãy chuyển qua tài khoản vnc để cài đặt file xstartup để khởi động xfce4 mỗi khi kết nối VNC.
```
su - vncuser
```



####Khởi động VNC server với tài khoản đã chọn để tiến hành cài đặt
```
vncserver
```

####Tiếp theo VNC sẽ hỏi password để kết nối remote cho tài khoản này, hãy nhập vào password mong muốn.
```
vncuser@chiasecoupon:~$ vncserver
You will require a password to access your desktops.
Password:
Verify:
xauth: file /home/vncuser/.Xauthority does not exist

New 'chiasecoupon:1 (vncuser)' desktop is chiasecoupon:1

Creating default startup script /home/vncuser/.vnc/xstartup
Starting applications specified in /home/vncuser/.vnc/xstartup
Log file is /home/vncuser/.vnc/chiasecoupon:1.log
```

####Sau khi VNC Server đã khởi động, chúng ta cần tắt nó đi để chỉnh sửa xstartup file để đảm bảo luôn khởi động xfce4 thay vì gnome.

####Kill VNC Server session
```
vncserver -kill :1
```
####Chỉnh sửa xstartup file
```
cd ~
> .vnc/xstartup
nano .vnc/xstartup
```

####Điền nội dung bên dưới:
```
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
startxfce4 &
[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
vncconfig -iconic &
```

####Lưu lại và tiến hành tạo VNC Server statup script

```
su -
nano /etc/init.d/vncserver
```

####Với nội dung

```
#!/bin/bash
unset VNCSERVERARGS
VNCSERVERS=""
[ -f /etc/vncserver/vncservers.conf ] && . /etc/vncserver/vncservers.conf
prog=$"VNC server"
start() {
 . /lib/lsb/init-functions
 REQ_USER=$2
 echo -n $"Starting $prog: "
 ulimit -S -c 0 >/dev/null 2>&1
 RETVAL=0
 for display in ${VNCSERVERS}
 do
 export USER="${display##*:}"
 if test -z "${REQ_USER}" -o "${REQ_USER}" == ${USER} ; then
 echo -n "${display} "
 unset BASH_ENV ENV
 DISP="${display%%:*}"
 export VNCUSERARGS="${VNCSERVERARGS[${DISP}]}"
 su ${USER} -c "cd ~${USER} && [ -f .vnc/passwd ] && vncserver :${DISP} ${VNCUSERARGS}"
 fi
 done
}
stop() {
 . /lib/lsb/init-functions
 REQ_USER=$2
 echo -n $"Shutting down VNCServer: "
 for display in ${VNCSERVERS}
 do
 export USER="${display##*:}"
 if test -z "${REQ_USER}" -o "${REQ_USER}" == ${USER} ; then
 echo -n "${display} "
 unset BASH_ENV ENV
 export USER="${display##*:}"
 su ${USER} -c "vncserver -kill :${display%%:*}" >/dev/null 2>&1
 fi
 done
 echo -e "\n"
 echo "VNCServer Stopped"
}
case "$1" in
start)
start $@
;;
stop)
stop $@
;;
restart|reload)
stop $@
sleep 3
start $@
;;
condrestart)
if [ -f /var/lock/subsys/vncserver ]; then
stop $@
sleep 3
start $@
fi
;;
status)
status Xvnc
;;
*)
echo $"Usage: $0 {start|stop|restart|condrestart|status}"
exit 1
esac
```

####Chmod vncserver script
```
chmod +x /etc/init.d/vncserver
```

Giờ tạo file cấu hình VNC Server trong thư mục /etc/
```
mkdir -p /etc/vncserver
nano /etc/vncserver/vncservers.conf
```

Copy đoạn sau vào, dòng đầu tiên là VNC port và VNC user, nếu muốn add thêm user thì điền thêm ở dòng này. Dòng tiếp theo là kích thước màn hình khi connect VNC.
```
VNCSERVERS="1:vncuser"
VNCSERVERARGS[1]="-geometry 1024x768"
```

####Cuối cùng đảm bảo VNC Server luôn khởi động cùng Ubuntu
```
update-rc.d vncserver defaults 99
```

####Khởi động lại Ubuntu Server
```
reboot
```

<a name="32"></a>
###3.2 Trên CentOS 6

####Cài đặt VNC server
```
yum install tigervnc-server -y
```

Để đảm bảo bảo mật cho VPS, mình sẽ sử dụng một tài khoản vncuser chuyên để remote.
```
adduser vncuser
```

Chuyển sang tài khoản này và cài đặt VNC password
```
su vncuser
vncpasswd
```

Quay trở lại tài khoản root
```
exit
```

Tiếp theo cài đặt local password cho vncuser, có thể giống với VNC password cũng được
```
passwd vncuser
```

File cấu hình TightVNC có đường dẫn /etc/sysconfig/vncservers trên CentOS. Bạn hãy mở file này lên
```
nano /etc/sysconfig/vncservers
```

Và thêm đoạn sau vào cuối file
```
VNCSERVERS="2:vncuser"
VNCSERVERARGS[2]="-geometry 1024x768"
```

Trong đó dòng đầu tiên là port (2 hoặc 5902) và account kết nối VNC. Dòng thứ 2 là screen resolution.

Giờ khởi động VNC Server
```
service vncserver start
```

Nếu bạn VNC Server luôn được khởi động cùng server thì dùng lệnh:
```
chkconfig vncserver on
```
