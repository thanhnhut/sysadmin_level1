## Tìm hiểu về SSH 

> 
> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **31/07/2016**

###Mục lục

[1.Giới thiệu](#1)

[2.Đặc điểm và cách thức hoạt động của SSH](#2)

 - [2.1 Đặc điểm](#21)
 
 - [2.2 Hoạt động](#22)

[3.Public key và Private key trong SSH](#3)

[4.File cấu hình SSH server và một số phương thức xác thực](#4)
 
 - [4.1 Cấu hình /etc/ssh/sshd-config](#41)
 
 - [4.2 Xác thực dùng Password](#42)

 
 - [4.3 Xác thực dùng Public key](#43)
 
 - [4.4 Restric Root (hạn chế truy cập root)](#44)


---
<a name="1"></a>
###**1.Giới thiệu**

SSH ( Secure Shell) là một giao thức mạng dùng để thiết lập kết nối mạng một cách bảo mật. SSH hoạt động ở lớp trên trong mô hình phân lớp TCP/IP. Các công cụ SSH (như là OpenSSH, PuTTy,…) cung cấp cho người dùng cách thức để thiết lập kết nối mạng được mã hoá để tạo một kênh kết nối riêng tư. Hơn nữa tính năng tunneling (hoặc còn gọi là port forwarding) của các công cụ này cho phép chuyển tải các giao vận theo các giao thức khác. Do vậy có thể thấy khi xây dựng một hệ thống mạng dựa trên SSH, chúng ta sẽ có một hệ thống mạng riêng ảo VPN đơn giản.

SSH cũng là một chương trình tương tác giữa máy chủ và máy khách có sử dụng cơ chế mã hoá đủ mạnh nhằm ngăn chặn các hiện tượng nghe trộm, đánh cắp thông tin trên đường truyền. Các chương trình trước đây: telnet, rlogin không sử dụng phương pháp mã hoá. Vì thế bất cứ ai cũng có thể nghe trộm thậm chí đọc được toàn bộ nội dung của phiên làm việc bằng cách sử dụng một số công cụ đơn giản. Sử dụng SSH là biện pháp hữu hiệu bảo mật dữ liệu trên đường truyền từ hệ thống này đến hệ thống khác.
<a name="2"></a>
###**2.Đặc điểm và cách thức hoạt động của SSH**

<a name="21"></a>
####2.1 Đặc điểm

Các đặc điểm chính của giao thức SSH là:

- Tính bí mật (Privacy) của dữ liệu thông qua việc mã hoá mạnh mẽ

- Tính toàn vẹn (integrity) của thông tin truyền, đảm bảo chúng không bị biến đổi.

- Chứng minh xác thực (authentication) nghĩa là bằng chứng để nhận dạng bên gửi và bên nhận

- Giấy phép (authorization) :dùng để điều khiển truy cập đến tài khoản.

- Chuyển tiếp (forwarding) hoặc tạo đường hầm (tunneling) để mã hoá những phiên khác dựa trên giao thức TCP/IP

<a name="22"></a>
####2.2 Hoạt động

SSH làm việc thông qua 3 bước đơn giản:


#####1 . Định danh host - xác định định danh của hệ thống tham gia phiên làm việc SSH.

Việc định danh host được thực hiện qua việc trao đổi khoá. Mỗi máy tính có hỗ trợ kiểu truyền thông SSH có một khoá định danh duy nhất. Khoá này gồm hai thành phần: khoá riêng và khoá công cộng. Khoá công cộng được sử dụng khi cần trao đổi giữa các máy chủ với nhau trong phiên làm việc SSH, dữ liệu sẽ được mã hoá bằng khoá công khai và chỉ có thể giải mã bằng khoá riêng. Khi có sự thay đổi về cấu hình trên máy chủ: thay đổi chương trình SSH, thay đổi cơ bản trong hệ điều hành, khoá định danh cũng sẽ thay đổi. Khi đó mọi người sử dụng SSH để đăng nhập vào máy chủ này đều được cảnh báo về sự thay đổi này. Khi hai hệ thống bắt đầu một phiên làm việc SSH, máy chủ sẽ gửi khoá công cộng của nó cho máy khách. Máy khách sinh ra một khoá phiên ngẫu nhiên và mã hoá khoá này bằng khoá công cộng của máy chủ, sau đó gửi lại cho máy chủ. Máy chủ sẽ giải mã khoá phiên này bằng khoá riêng của mình và nhận được khoá phiên. Khoá phiên này sẽ là khoá sử dụng để trao đổi dữ liệu giữa hai máy. Quá trình này được xem như các bước nhận diện máy chủ và máy khách.

#####2 . Mã hoá - thiết lập kênh làm việc mã hoá.

Sau khi hoàn tất việc thiết lập phiên làm việc bảo mật (trao đổi khoá, định danh), quá trình trao đổi dữ liệu diễn ra thông qua một bước trung gian đó là mã hoá/giải mã. Điều đó có nghĩa là dữ liệu gửi/nhận trên đường truyền đều được mã hoá và giải mã theo cơ chế đã thoả thuận trước giữa máy chủ và máy khách. Việc lựa chọn cơ chế mã hoá thường do máy khách quyết định. Các cơ chế mã hoá thường được chọn bao gồm: 3DES, IDEA, và Blowfish. Khi cơ chế mã hoá được lựa chọn, máy chủ và máy khách trao đổi khoá mã hoá cho nhau. Việc trao đổi này cũng được bảo mật dựa trên đinh danh bí mật của các máy. Kẻ tấn công khó có thể nghe trộm thông tin trao đổi trên đường truyền vì không biết được khoá mã hoá. Các thuật toán mã hoá khác nhau và các ưu, nhược điểm của từng loại:

   <ul>

   <li>3DES (cũng được biết như Triple-DES) -- phương pháp mã hoá mặc định cho SSH.</li>

 <li>IDEA—Nhanh hơn 3DES, nhưng chậm hơn Arcfour và Blowfish.</li>

  <li>Arcfour—Nhanh, nhưng các vấn đề bảo mật đã được phát hiện.</li>

  <li>Blowfish—Nhanh và bảo mật, nhưng các phương pháp mã hoá đang được cải tiến.</li>
 </ul>

<a name="3"></a>
#####3 . Chứng thực - xác thực người sử dụng có quyền đăng nhập hệ thống.

Việc chứng thực là bước cuối cùng trong ba bước, và là bước đa dạng nhất. Tại thời điểm này, kênh trao đổi bản thân nó đã được bảo mật. Mỗi định danh và truy nhập của người sử dụng có thể được cung cấp theo rất nhiều cách khác nhau. Chẳng hạn, kiểu chứng thực rhosts có thể được sử dụng, nhưng không phải là mặc định; nó đơn giản chỉ kiểm tra định danh của máy khách được liệt kê trong file rhost (theo DNS và địa chỉ IP). Việc chứng thực mật khẩu là một cách rất thông dụng để định danh người sử dụng, nhưng ngoài ra cũng có các cách khác: chứng thực RSA, sử dụng ssh-keygen và ssh-agent để chứng thực các cặp khoá.

###**3. Public key và Private key trong SSH**

Private key và Public key luôn có liên hệ chặt chẽ với nhau để nó có thể nhận diện lẫn nhau. Khi tạo một SSH Key thì  sẽ có cả 2 loại key này. Sau đó mang  public key bỏ lên máy chủ , còn  private key  sẽ lưu ở máy trạm và khi đăng nhập vào server,  gửi yêu cầu đăng nhập kèm theo  Private Key này để gửi tín hiệu đến server, server sẽ kiểm tra xem  Private key  có khớp với Public key có trên server hay không, nếu có thì  sẽ đăng nhập được.Nội dung giữa Private Key và Public Key hoàn toàn khác nhau, nhưng nó vẫn sẽ nhận diện được với nhau thông qua một thuật toán riêng của nó.




<a name="4"></a>
###**4. File cấu hình SSH server và một số phương thức xác thực**

<a name="41"></a>
####4.1 Cấu hình /etc/ssh/sshd-config 

Các tập tin / etc / ssh / sshd_config là tập tin cấu hình hệ thống cho OpenSSH cho phép bạn thiết lập các tùy chọn  thay đổi hoạt động của các daemon. Tập tin này có chứa cặp khóa-giá trị, mỗi một dòng, với từ khóa là các trường hợp . Dưới đây là những từ khóa quan trọng nhất để cấu hình sshd  , một danh sách đầy đủ and / or yêu cầu đặc biệt có sẵn trong các trang  cho sshd. 

Chỉnh sửa file sshd_config, vi / etc / ssh / sshd_config và thay đổi and/or , nếu cần thiết, các thông số sau:

```
 Đây là ssh server  tập tin cấu hình toàn hệ thống.

Port 22
          
          ListenAddress 192.168.1.1
          HostKey /etc/ssh/ssh_host_key
          ServerKeyBits 1024
          LoginGraceTime 600
          KeyRegenerationInterval 3600
          PermitRootLogin no
          IgnoreRhosts yes
          IgnoreUserKnownHosts yes
          StrictModes yes
          X11Forwarding no
          PrintMotd yes
          SyslogFacility AUTH
          LogLevel INFO
          RhostsAuthentication no
          RhostsRSAAuthentication no
          RSAAuthentication yes
          PasswordAuthentication yes
          PermitEmptyPasswords no
          AllowUsers admin

```

Điều này cho file sshd_config  tự thiết lập cho các thiết lập cấu hình này đặc biệt với:

**Port 22**

Các tùy chọn cổng quy định cụ thể mà trên đó số cổng ssh daemon lắng nghe kết nối đến. Cổng mặc định là 22.

**ListenAddress 192.168.1.1**

Các tùy chọn ListenAddress xác định địa chỉ IP của  giao diện mạng trên đó ssh server socket daemon được ràng buộc. Mặc định là 0.0.0.0 để cải thiện an ninh, bạn có thể xác định chỉ những người cần thiết để hạn chế các địa chỉ có thể.

**HostKey / etc / ssh / ssh_host_key**

Các tùy chọn HostKey xác định vị trí chứa private host key.

**ServerKeyBits 1024**

Các ServerKeyBits tùy chọn xác định bao nhiêu bit để sử dụng trong server key. Những bit này được sử dụng khi các daemon bắt đầu để tạo ra chìa khóa RSA của nó.

**LoginGraceTime 600**

Các tùy chọn LoginGraceTime chỉ định độ dài trong vài giây sau khi một yêu cầu kết nối máy chủ sẽ chờ đợi trước khi ngắt kết nối nếu người dùng không đăng nhập thành công

**KeyRegenerationInterval 3600**

Các tùy chọn KeyRegenerationInterval chỉ định độ dài trong vài giây máy chủ nên chờ đợi trước khi tự động tái tạo key của nó. Đây là một tính năng bảo mật để ngăn giải mã phiên .

**PermitRootLogin no**

Các tùy chọn PermitRootLogin định liệu gốc có thể đăng nhập bằng ssh. Không bao giờ nói yes với tùy chọn này.

**IgnoreRhosts yes**

Các IgnoreRhosts tùy chọn xác định xem rhosts hoặc các tập tin shosts không nên được sử dụng trong xác thực. Vì lý do an ninh nó được khuyến khích để không rhosts sử dụng hoặc các tập tin shosts để xác thực.

**IgnoreUserKnownHosts yes**

Các IgnoreUserKnownHosts tùy chọn xác định xem daemon ssh nên bỏ qua của người dùng $ HOME / .ssh / known_hosts trong RhostsRSAAuthentication.

**StrictModes yes**

Các StrictModes tùy chọn chỉ định cho dù ssh có kiểm tra quyền của người sử dụng trong thư mục chủ và tập tin rhosts của họ trước khi chấp nhận đăng nhập. Tùy chọn này luôn luôn phải được thiết lập  yes bởi vì đôi khi người dùng có thể vô tình để lại thư mục hoặc tập tin.

**X11Forwarding no**
Các tùy chọn X11Forwarding chỉ định cho dù X11 chuyển tiếp phải được kích hoạt hay không trên máy chủ này. Kể từ khi ta thiết lập  một máy chủ mà không cần cài đặt GUI trên nó,  ta có thể an toàn tắt tùy chọn này.

**PrintMotd yes**

Các tùy chọn PrintMotd xác định xem daemon ssh nên in các nội dung của / etc / motd tập tin khi người dùng đăng nhập tương tác. Các file / etc / motd còn được gọi là thông điệp của ngày.

**SyslogFacility AUTH**

Các tùy chọn SyslogFacility định mã cơ sở sử dụng khi đăng nhập tin nhắn từ sshd. Các cơ sở xác định các hệ thống phụ sinh ra thông báo - trong trường hợp của chúng tôi, AUTH.

**LogLevel INFO**

Các tùy chọn LogLevel định mức được sử dụng khi đăng nhập tin nhắn từ sshd. INFO là một lựa chọn tốt.

**RhostsAuthentication no**

Các tùy chọn RhostsAuthentication xác định xem sshd có thể thử sử dụng rhosts dựa vào Authentication. Bởi vì  xác thực rhosts là không an toàn, bạn không nên sử dụng tùy chọn này.

**RhostsRSAAuthentication no**

Các tùy chọn RhostsRSAAuthentication xác định liệu có nên cố gắng xác thực rhosts trong concert với RSA host anthentication.

**RSAAuthentication yes**

Các tùy chọn RSAAuthentication xác định liệu có nên cố gắng xác thực RSA. Tùy chọn này phải được thiết lập để có bảo mật tốt hơn trong các phiên của bạn. RSA sử dụng public key và private key cặp khóa tạo ra với ssh-keygen1utility cho các mục đích xác thực.

**PasswordAuthentication yes**

Các tùy chọn thực mật khẩu xác định xem chúng ta có nên sử dụng xác thực dựa trên mật khẩu. Để bảo mật mạnh mẽ, tùy chọn này luôn luôn phải được thiết lập là yes.

**PermitEmptyPasswords no**

Các PermitEmptyPasswords tùy chọn xác định xem máy chủ cho phép đăng nhập vào tài khoản với mật khẩu null. Nếu bạn có ý định sử dụng các tiện ích scp để thực hiện sao lưu tự động qua mạng, bạn phải thiết lập tùy chọn này để yes.

**AllowUsers admin**

Các tùy chọn AllowUsers định chi tiết và kiểm soát mà người dùng có thể truy cập vào dịch vụ SSH. Nhiều người sử dụng có thể được chỉ định, cách nhau bởi dấu cách.

#####Các bước thay đổi Port đăng nhập SSH

Port 22 mặc định được sử dụng để kết nối SSH đến Linux Server, do đó sẽ có nhiều người lợi dụng điều này để tìm cách tấn công tài khoản root của VPS.

Để tăng thêm tính bảo mật cho VPS, các bạn nên thay đổi port đăng nhập SSH trên VPS thay vì dùng port 22 mặc định.

- Login vào VPS sử dụng quyền root

- Chỉnh sửa file sshd_config
```
/etc/ssh/sshd_config
```
- Tìm kiếm dòng Port 22,  thay bằng port bạn muốn dùng, ví dụ 2222 (Port này được sử dụng trên Windows chứ không dùng trên Linux). Xe  thêm các port của [TCP và UDP](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)
```
Port 2222
```
Lưu ý port cần phải  free và không có service nào sử dụng để tránh xung đột.

<a name="42"></a.>
####4.2 Xác thực chỉ dùng Password

Phương thức mật khẩu thì rất đơn giản: nó tên là “password”. Phương thức này chỉ có trong một số bản bố sung của SSH2. Sau khi kiểm tra các tham số thích hợp, server sẽ gửi thông báo chấp nhận truy cập của client và nếu có giao thức này thì server sẽ gửi kết hợp password với thông báo đó để xác thực với client.

<a name="43"></a>
####4.3 Xác thực chỉ dùng Public key

Một yêu cầu chứng thực khoá công khai mang phương thức có tên là “publickey” và có thể có nhiều dạng khác nhau phụ thuộc vào một cờ được thiết lập. Một dạng của phương thức này là:

flag = FALSE

Tên thuật toán

Dữ liệu khoá

Thuật toán khoá công khai có thể dùng là những thuật toán thiết lập trong SSH-TRANS và định dạng dữ liệu khoá phụ thuộc vào kiểu khoá như ssh-dss hay ssh-rsa.

Với cờ thiết lập là FALSE, thông báo này chỉ đơn thuần là kiểm tra xác thực: nó yêu cầu server kiểm tra khoá này có được xác thực để truy cập như mong muốn của tài khoản hay không, nếu được thì gửi lại một thông báo cho biết. Nếu khoá không được xác thực, hồi đáp có giá trị FALSE đơn giản.

Sau khi xác nhận khoá và gửi thông báo thành công, server cho biết đã chấp nhận truy cập và kết thúc phiên SSH-AUTH.

<a name="44"></a>
####4.4 Restric Root (hạn chế truy cập root)

Ngày nay, SSH là một giao thức phổ biến để thực hiện remote từ xa từ máy client đến máy chủ Linux. Điều này, giúp việc quản trị hệ thống trở lên dễ dàng và thuận tiện hơn. Tuy nhiên, nó cũng đi kèm với những rủi ro nhất định nếu người quản trị không ý thức rõ ràng về việc phải bảo vệ server của mình trước các kẻ tấn công bất hợp pháp, đặc biệt là khi server được public ra internet. Các hacker có thể lợi dụng thực hiện tấn công từ điển, hay tấn công brute force để dò user và mật khẩu của server.

Trong linux, tài khoản ‘root’ là tài khoản nhạy cảm, nó có đặc quyền cao nhất. Nếu bạn để mất tài khoản này vào tay hacker thì gần như là chấm hết. Vì vậy, cách tốt hơn là bạn nên truy cập qua SSH bằng một tài khoản khác và ‘switch’ sang root bằng lệnh ‘su -’ khi cần thiết.

**Disable SSH Root login**

Để disable ssh root login, bạn mở file /etc/ssh/sshd_config, sau đó tìm đến dòng:
```
#PermitRootLogin no
```
Bỏ kí tự # trước dòng đó:

PermitRootLogin no

Restart lại SSH:
```
#/etc/init.d/sshd restart
```
Bây giờ, bạn sẽ không truy cập trực tiếp tài khoản root từ ssh được nữa.
```
login as: root

Access denied

root@172.31.41.51's password:
```
**Enable SSH Root login**

Bạn mở file /etc/ssh/sshd_config, sau đó tìm đến dòng:

PermitRootLogin no

Thêm # trước dòng đó:
```
#PermitRootLogin no
```
Restart lại SSH:
```
#PermitRootLogin no
```
**Giới hạn User SSH login**

Để giới hạn 1 số lượng tài khoản được login ssh vào hệ thống, bạn mở file /etc/ssh/sshd_config, tìm đến dòng:
```
AllowUsers
```
Sau dòng này bạn add các user bạn muốn cho login ssh vào hệ thống. Ví dụ, tôi muốn cho tài khoản nhut, securitydaily được quyền login vào hệ thống thì cấu hình như sau:
```
AllowUsers nhut securitydaily
```


 
