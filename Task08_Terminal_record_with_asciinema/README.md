


## Tìm hiểu Asciinema

> 
> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **3/8/2016**

###Mục lục

[I. Làm thế nào nó hoạt động](#ls)

[II.Getting started](#g)

 - [1.Cài đặt recorder](#1)

 - [2.Recorder](#2)

 - [3.Quản lý các bản ghi âm](#3)

[III.Cài đặt](#cd)

[IV.Sử dụng Asciinema](#sd)

---
<a name="ls"></a>
##**I.Làm thế nào nó hoạt động**

Dự án asciinema được xây dựng dựa trên một vài miếng bổ sung:

- Dòng lệnh dựa trên terminal phiên ghi , asciinema.

- Trang web với API tại asciinema.org 

- Javacript player

Khi bạn chạy **asciinema rec** trong terminal của bạn ghi bắt đầu, tất cả các đầu ra  đang được in vào terminal của bạn trong khi bạn đang thực hiện các lệnh shell. Khi kết thúc ghi  (bằng cách nhấn Ctrl-D hoặc gõ exit ) thì đầu ra bắt được tải lên trang web asciinema.org và chuẩn bị sẵn sàng để phát lại trên web.

Dưới đây là một tổng quan ngắn gọn về cách các bộ phận làm việc.

###Ghi  (Recording)

Bạn có thể biết các lệnh **ssh** , **screen** hoặc **script** lệnh.Trên thực tế, asciinema được lấy cảm hứng từ lệnh script (và **scriptreplay** ).  Bạn có thể không biết là tất cả họ đều sử dụng cùng một hệ thống UNIX : một pseudo-terminal.


>Một pseudo-terminal là một cặp pseudo-devices, một trong số đó, những phụ thuộc, giả lập một văn bản terminal  thực sự, những thứ khác trong đó, chủ, cung cấp các phương tiện mà một quá trình mô phỏng thiết bị điều khiển các phụ thuộc.

Dưới đây là giao diện giả lập  terminal với người sử dụng và shell:

>Vai trò của quá trình mô phỏng thiết bị là tương tác với người sử dụng để xuất  văn bản đầu vào để làm chủ pseudo-devices để sử dụng bởi các shell (được kết nối với các phụ thuộc pseudo-devices) và đọc văn bản đầu ra từ tổng thể pseudo-devices và hiển thị nó cho người dùng.

Nói cách khác, pseudo- terminal cho các chương trình có khả năng hoạt động như một trung gian giữa người sử dụng, màn hình và shell. Nó cho phép chụp trong suốt qúa trình của người sử dụng đầu vào (bàn phím) và đầu ra (màn hình). **screen** lệnh sử dụng nó để chụp hình các phím tắt bàn phím đặc biệt như Ctrl-A và thay đổi đầu ra để hiển thị window numbers  / name và các thông báo khác.

asciinema recorder làm công việc của mình bằng cách sử dụng pseudo-terminal để chụp tất cả các đầu ra mà đi đến  terminal và lưu nó trong bộ nhớ (cùng với thông tin thời gian). Sản lượng bị bắt bao gồm tất cả các văn bản và trình tự escape / control vô hình trong một hình thức nguyên, không thay đổi gì. Khi buổi ghi âm kết thúc nó tải lên các đầu ra (trong định dạng asciicast ) tới asciinema.org. Đó là tất cả về phần "ghi âm".



###playback


Khi ghi  là một dòng chuỗi văn bản và kiểm soát trình tự, nó không thể  chỉ hoạt động bằng cách từng bước in văn bản trong khoảng thời gian thích hợp. Nó đòi hỏi sự giải thích của **các trình tự mã thoát ANSI** để hiển thị một cách chính xác những thay đổi màu sắc, di chuyển con trỏ và in văn bản ở những nơi thích hợp trên màn hình.

Người sử dụng đi kèm với mô phỏng terminal của mình dựa trên **phân tích Paul Williams 'cho terminal Video ANSI tương thích** . Nó chỉ bao gồm phần hiển thị của sự mô phỏng vì đây là những gì thuộc về người dùng (đầu vào được xử lý bởi terminal + shell của bạn tại thời điểm ghi anyway) và xử lý của trình tự thoát ra là hoàn toàn tương thích với hầu hết các giả lập thiết bị đầu cuối hiện đại như xterm, Gnome Terminal, iTerm, Mosh,...

Kết quả cuối cùng là một hình ảnh động trơn tru với tất cả các thuộc tính văn bản (in đậm, gạch chân, nghịch đảo, ...) và 256 màu sắc hoàn trả lại.

<a name="g"></a>
##II. Getting started 

<a name="1"></a>
###1. Cài đặt recorder

cài đăt asciinema với:

```
brew update && brew install asciinema
```

[Xem các tùy chọn cài đặt khác](#cd)

<a name="2"></a>
###2. Rcorder 

Để bắt đầu quay chạy lệnh sau:
```
 asciinema rec 
```
Spawns này một ví dụ Shell mới và ghi lại tất cả các đầu ra terminal. Khi bạn đã sẵn sàng để kết thúc đơn giản là thoát khỏi shell bằng cách đánh exit hoặc nhấn Ctrl-D .

Xem [hướng dẫn sử dụng](#sd) để tìm hiểu về tất cả các lệnh và các tùy chọn.

<a name="3"></a>
###3. Quản lý các bản ghi âm (Optional)

Nếu bạn muốn quản lý các bản ghi âm của bạn trên asciinema.org (set title /description, delete etc ...), bạn cần phải xác thực. Chạy lệnh sau đây và mở URL được hiển thị trong trình duyệt web của bạn:
```
 asciinema auth 
```
<a name="cd"></a>
##III. Cài đặt

####**Python packet**

asciinema có sẵn trên [PyPI](https://translate.googleusercontent.com/translate_c?depth=1&hl=vi&prev=search&rurl=translate.google.com.vn&sl=en&u=https://pypi.python.org/pypi/asciinema&usg=ALkJrhiGYYscoDNGVvD7yySYeH9T4tEkLA) và có thể được cài đặt với pip (Python 3 bắt buộc):

```
sudo pip3 install asciinema 
```
####**Native pacet**
Arch Linux
```
 yaourt -S asciinema 
```
####**Debian**
```
 sudo apt-get install asciinema 
```
####**Fedora**

Dành cho Fedora <22:
```
 sudo yum install asciinema 
```
Dành cho Fedora> = 22:
```
 sudo dnf install asciinema 
```
####**FreeBSD**

Ports:
```
 cd /usr/ports/textproc/asciinema && make install 
```
gói:

```
 pkg install asciinema 
```
####**Gentoo Linux**
```
 layman -a go-overlay && emerge -av asciinema 
```
####**NixOS / Nix**
```

 nix-env -i go1.4-asciinema 
```
####**OS X**

homebrew:
```
 brew update && brew install asciinema 
```
MacPorts:
```
 sudo port selfupdate && sudo port install asciinema 
```
nix:
```
 nix-env -i go1.4-asciinema 
```
####**Ubuntu**
```
sudo apt-add-repository ppa:zanchey/asciinema 
sudo apt-get install asciinema 
```

<a name="sd"></a>
##IV. Sử dụng Asciinema

asciinema được bao gồm nhiều lệnh, tương tự như **git** , **apt-get** hoặc **brew** .

Khi bạn chạy **asciinema** không có thông báo đối số giúp đỡ được hiển thị, liệt kê tất cả các lệnh có sẵn với các tùy chọn của họ.

###rec [filename]
**Recorder terminal session**

Đây là các lệnh quan trọng nhất trong asciinema, vì nó là cách bạn sử dụng công việc chính của công cụ này.

Bằng cách chạy **asciinema rec [filename]** bạn bắt đầu một buổi ghi âm mới. Lệnh (process) được ghi lại có thể được chỉ định với các **-c** tùy chọn (xem dưới đây), và mặc định là **$SHELL** đó là những gì bạn muốn trong hầu hết các trường hợp.

Recorder kết thúc khi bạn thoát khỏi shell (nhấn Ctrl + D hoặc loại **exit** ). Nếu quá trình recorder lại không phải là một shell sau đó recorder kết thúc khi quá trình thoát.

Nếu **filename** tóm tắt được đưa ra sau đó kết quả ghi âm (gọi là **asciicast** ) được lưu vào một tập tin địa phương. Nó sau đó có thể được thực hiện lại với **asciinema play [filename] and / or** tải lên asciinema.org với asciinema upload [filename] . Nếu **filename** tóm tắt là bỏ qua thì sau đó (sau khi yêu cầu xác nhận) các kết qủa asciicast  được tải lên asciinema.org để phát lại xa hơn trong một trình duyệt web.

**ASCIINEMA_REC=1** được thêm vào biến môi trường quá trình ghi. Điều này có thể được sử dụng bởi các tập tin cấu hình của bao của bạn ( **.bashrc , .zshrc** ) để thay đổi dấu nhắc hoặc chơi một âm thanh khi shell đã được ghi lại.

Tùy chọn có sẵn:

- **c, --command=ơơcommand]** - Chỉ định lệnh để ghi âm, mặc định là $ SHELL

- **t, --title=[title] -** Xác định tiêu đề của asciicast

- **w, --max-wait=[sec] -** Giảm ghi không hoạt động thiết bị đầu cuối để tối đa giây

- **y, --yes -** trả lời "có" cho tất cả lời nhắc (ví dụ như xác nhận tải lên)

- **q, --quiet -** Hãy yên tĩnh, ngăn chặn tất cả các thông báo / cảnh báo (ngụ ý -y)

###play [filename]

**Replay recordered asciicast trong một terminal.**

Lệnh này replay cho asciicast ( được ghi lại như lệnh **rec**) trực tiếp vào terminal của bạn.

Sử dụng từ một tập tin địa phương:
```
 asciinema play /path/to/asciicast.json 
```

Sử dụng từ HTTP (S) URL:
```
 asciinema play https://asciinema.org/a/22124.json asciinema play http://example.com/demo.json 
```
Sử dụng từ URL trang asciicast (yêu cầu **link rel="alternate" type="application/asciicast+json" href="....json"** trong HTML của trang):
```
 asciinema play https://asciinema.org/a/22124 
 asciinema play http://example.com/blog/post.html 
```
Sử dụngh từ stdin:
```
 cat /path/to/asciicast.json | asciinema play - ssh user@host cat asciicast.json | asciinema play - 
```
Sử dụngh từ IPFS:
```
 asciinema play ipfs:/ipfs/QmcdXYJp6e4zNuimuGeWPwNMHQdxuqWmKx7NhZofQ1nw2V 
 asciinema play fs:/ipfs/QmcdXYJp6e4zNuimuGeWPwNMHQdxuqWmKx7NhZofQ1nw2V 
```
tùy chọn có sẵn:

- **-w, --max-wait=[sec] -**  Tái giảm terminal không hoạt động đến tối đa

Chú ý: bạn nên chạy asciinema play trong một terminal của kích thước không nhỏ hơn so với sử dụng để ghi như không có "chuyển mã" của trình tự kiểm soát đối với kích thước terminal mới.

###upload [filename]

**Tải recorded asciicast vào trang web asciinema.org.**

Đây asciicast lệnh cập nhất định (như được ghi lại bởi **rec** lệnh) để asciinema.org phát lại xa hơn trong một trình duyệt web.

**asciinema rec demo.json + asciinema play demo.json + asciinema upload demo.json** là một kết hợp tốt đẹp cho bạn khi muốn xem lại một asciicast trước khi xuất bản nó trên asciinema.org.

##auth

**Quản lý ghi trên tài khoản asciinema.org.**

Nếu bạn muốn quản lý các bản ghi âm của bạn trên asciinema.org (đặt tên / mô tả, xóa vv), bạn cần phải xác thực. Lệnh này hiển thị các URL bạn nên mở trong trình duyệt web của bạn để làm điều đó.

Trên mỗi máy bạn chạy ghi asciinema, bạn sẽ có được một cái mới, token API duy nhất. Nếu bạn đã đăng nhập vào trang web asciinema.org và bạn chạy **asciinema auth** từ một máy tính mới sau đó thiết bị mới này sẽ được liên kết với tài khoản của bạn.

Bạn có thể đồng bộ hóa tập tin cấu hình của bạn (mà giữ token API) trên máy vì vậy tất cả trong số họ sử dụng các dấu hiệu như vậy, nhưng đó là không cần thiết. Bạn có thể gán thẻ mới vào tài khoản của bạn từ nhiều máy như bạn muốn.


