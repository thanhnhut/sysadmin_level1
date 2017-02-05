<p align="center"><img src="https://hostingviet.vn/data/tinymce/tin-tuc/ftp-la-gi.png" /></p>

> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật: **27/01/2017**

###Mục lục

[1.Khái niệm](#1)

[2.Hoạt động](#2)

[3.Ưu và nhược điểm](#3)

[4.Một số FTP Client](#4)

[5.Tài liệu tham khảo](#5)

---

<a name="1"></a>
#1.Khái Niệm 

FTP (viết tắt của File Transfer Protocol dịch ra là "Giao thức truyền tập tin") thường được dùng để trao đổi tập tin qua mạng lưới truyền thông dùng giao thức TCP/IP. Hoạt động của FTP cần có hai máy tính, một máy chủ và một máy khách). Máy chủ FTP, dùng chạy phần mềm cung cấp dịch vụ FTP, gọi là trình chủ, lắng nghe yêu cầu về dịch vụ của các máy tính khác trên mạng lưới. Máy khách chạy phần mềm FTP dành cho người sử dụng dịch vụ, gọi là trình khách, thì khởi đầu một liên kết với máy chủ.  Một khi hai máy đã liên kết với nhau, máy khách có thể xử lý một số thao tác về tập tin, như tải tập tin lên máy chủ, tải tập tin từ máy chủ xuống máy của mình, đổi tên của tập tin, hoặc xóa tập tin ở máy chủ v.v. 

FTP sử dụng 2 cổng gồm:

- Cổng 20 để truyền dữ liệu (data port)

- Cổng 21 dùng để truyền câu lệnh (command port)

<a name="2"></a>
#2.Hoạt Động

Giao thức FTP hoạt động theo mô hình Client-Server. Tùy thuộc vào chế độ truyền tải được sử dụng, trình khách (ở chế độ chủ động - active mode) hoặc trình chủ (ở chế độ bị động - passive mode) đều có thể lắng nghe yêu cầu kết nối đến từ đầu kia. 

- Actice FTP: máy Client khởi tạo connection tới cổng của máy chủ (21) để trao đổi lệnh sau đó máy chủ mới mở cộng thứ 2 cổng dữ liệu và kết nối với cổng dữ liệu của máy Client.

- Passive FTP: máy Client làm cả 2 việc này (thiết lập đường dẫn cho commands và đườn dẫn dữ liệu.

<p align="center"><img src="https://camo.githubusercontent.com/94fff970495e9644243775c343137d3385375ae9/687474703a2f2f75736572732e736b796e65742e62652f73706f757365656c652f4654502f4654502d6f766572766965772e676966" /></p>

Thành phần Protocol Interpreter (PI) là thành phần quản lý kênh điều khiển, với chức năng phát và nhận lệnh.

Thành phần Data Transfer Process (DTP) có chức năng gửi và nhận dữ liệu giữa phía client với server. 

###Các tiến trình

Tiến trình phía server bao gồm hai giao thức:

- Server Protocol Interpreter (Server-PI): chịu trách nhiệm quản lý kênh điều khiển trên server. Nó lắng nghe yêu cầu kết nối hướng tới từ users trên cổng dành riêng. Khi kết nối đã được thiết lập, nó sẽ nhận lệnh từ phía User-PI, trả lời lại, và quản lý tiến trình truyền dữ liệu trên server.

- Server DataTransfer Process (Server-DTP): làm nhiệm vụ gửi hoặc nhận file từ bộ phận User-DTP. Server-DTP vừa làm nhiệm thiết lập kết nối kênh dữ liệu và lắng nghe một kết nối kênh dữ liệu từ user. Nó tương tác với server file trên hệ thống cục bộ để đọc và chép file.

Tiến trình phía Client:

- User Protocol Interpreter (User-PI): chịu trách nhiệm quản lý kênh điều khiển phía client. Nó khởi tạo phiên kết nối FTP bằng việc phát ra yêu cầu tới phía Server-PI. Khi kết nối đã được thiết lập, nó xử lý các lệnh nhận được trên giao diện người dùng, gửi chúng tới Server-PI, và nhận phản hồi trở lại. Nó cũng quản lý tiến trình User-DTP.

- User Data Transfer Process (User-DTP): là bộ phận DTP nằm ở phía người dùng, làm nhiệm vụ gửi hoặc nhận dữ liệu từ Server-DTP. User-DTP có thể thiết lập hoặc lắng nghe yêu cầu kết nối kênh dữ liệu trên server. Nó tương tác với thiết bị lưu trữ file phía client.

- User Interface: cung cấp giao diện xử lý cho người dùng. Nó cho phép sử dụng các lệnh đơn giản hướng người dùng, và cho phép người điều khiển phiên FTP theo dõi được các thông tin và kết quả xảy ra trong tiến trình.

###Thiết lập kênh

- Server-PI sẽ lắng nghe các kết nối TCP trên cổng 21

- User-PI sử dụng một cổng bất kỳ (> 1024) để kết nối tới server

- Sau khi thiết lập xong, Server-PI sẽ đáp trả kết quả bằng các mã thông báo

- Sau đó, là bước login của người dùng. Bước này có hai mục đích:

 -  Access Control (Điều khiển truy cập): quá trình chứng thực cho phép hạn chế truy cập tới server với những người dùng nhất định. Nó cũng cho phép server điều khiển loại truy cập như thế nào đối với từng người dùng. 

 - Resource Selection (Chọn nguồn cung cấp): Bằng việc nhận dạng người dùng tạo kết nối, FTP server có thể đưa ra quyết định sẽ cung cấp những nguồn nào cho người dùng đã được nhận dạng đó.


###Chứng thực


B1: Client gửi ID và Password từ User-PI lên Server-PI bằng lệnh USER và PASS.

B2: Server kiểm tra ID và Password, nếu hợp lệ thì server sẽ thiết lập phiên làm việc. Nếu sai quá số lần quy định, phiên sẽ được đóng và ngắt kết nối.

###Phương thức truyền dữ liệu

**Stream mode:**


- Dữ liệu được truyền đi dưới dạng các byte không cấu trúc liên tiếp

- Bên gửi chỉ đơn thuần đầy luồng dữ liệu qua kết nối TCP tới phía nhận.

- Phương thức này chủ yếu dựa vào tính tin cậy trong truyền dữ liệu của TCP.
 
- Do không có các header, vì vậy khi truyền file xong kết nối sẽ bị ngắt

- Xử lý với các file đều đơn thuần như là xử lý dòng byte, mà không để ý tới nội dung của các file

- Không tốn dung lượng để thông báo header


**Block mode:**


- Phương thức này mang tính quy chuẩn hơn, dữ liệu được chia thành nhiều khối nhỏ và được đóng gói thành các FTP block

- Mỗi block này có một trường header 3 byte báo hiệu độ dài, và chứa thông tin về các khối dữ liệu đang được gửi.

- Có một thuật toán để kiểm tra các dữ liệu đã được gửi đi và phát hiện, khởi tạo lại đối với một phiên dữ liệu đã bị ngắt trước đó.


**Compressed mode:**

Phương thức truyền sử dụng một kỹ thuật nén đơn giản, là "Run-length encoding" để phát hiện và xử lý các đoạn lặp trong dữ liệu được gửi đi để giảm chiều dài của thông điệp Thông tin đã được nén sẽ được gắn các header và được xử lý như ở Block mode.



<a name="3"></a>
#3.Ưu và nhược điểm

**Ưu điểm**

- Cho phép bạn chuyển nhiều tập tin cũng như các thư mục

- Khả năng tiếp tục chuyển nếu kết nối bị mất

- Khả năng để thêm các mục vào một hàng đợi sẽ được tải lên/tải về

- Nhiều FTP client có khả năng lên lịch chuyển

- Không có giới hạn về dung lượng truyền (các trình duyệt chỉ cho phép lên đến 2 GB)

- Nhiều client có khả năng truyền thông qua dòng lệnh

- Hầu hết client có một tiện ích đồng bộ hóa

- Chuyển nhanh hơn HTTP


- Hỗ trợ trên hầu hết các máy chủ


**Nhược điểm**

- Mật khẩu và nội dung của tập tin được truyền qua đường cáp mạng ở dạng văn bản thường (clear text), vì vậy chúng có thể bị chặn và nội dung bị lộ ra cho những kẻ nghe trộm. Hiện nay, người ta đã có những cải tiến để khắc phục nhược điểm này.

- Cần phải có nhiều kết nối TCP/IP: một dòng dành riêng cho việc điều khiển kết nối, một dòng riêng cho việc truyền tập tin lên, truyền tập tin xuống, hoặc liệt kê thư mục. Các phần mềm bức tường lửa cần phải được cài đặt thêm những lôgic mới, đế có thể lường trước được những kết nối của FTP.
- Việc thanh lọc giao thông FTP bên trình khách, khi nó hoạt động ở chế độ năng động, dùng bức tường lửa, là một việc khó làm, vì trình khách phải tùy ứng mở một cổng mới để tiếp nhận đòi hỏi kết nối khi nó xảy ra. Vấn đề này phần lớn được giải quyết bằng cách chuyển FTP sang dùng ở chế độ bị động.

- Người ta có thể lạm dụng tính năng ủy quyền, được cài đặt sẵn trong giao thức, để sai khiến máy chủ gửi dữ liệu sang một cổng tùy chọn ở một máy tính thứ ba. Xin xem thêm về FXP.

- FTP là một giao thức có tính trì trệ rất cao (high latency). Sự trì trệ gây ra do việc, nó bắt buộc phải giải quyết một số lượng lớn các dòng lệnh khởi đầu một phiên truyền tải.

- Phần nhận không có phương pháp để kiểm chứng tính toàn vẹn của dữ liệu được truyền sang. Nếu kết nối truyền tải bị ngắt giữa lưng chừng thì không có cách gì, trong giao thức, giúp cho phần nhận biết được rằng, tập tin nhận được là hoàn chỉnh hay còn vẫn còn thiếu sót. Sự hỗ trợ bên ngoài, như việc dùng kiểm tra tổng MD5, hoặc dùng kiểm độ dư tuần hoàn (cyclic redundancy checking) là một việc cần thiết.


<a name="4"></a>
#4.Một số FPT Client

###FileZilla

**Kết nối tới host**

Điền các thông tin sau đó Click **Quickconnect** để kết nối đến host.

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task38_Hosting_Usage/Images/14.png" /></p>

**Upload file lên Host**

Bạn chọn tập tin cần upload trên máy và chọn thư mục lưu trữ của tập trên host (thường là thư mục public_html). Sau đó bạn chuột phải vào file cần upload rồi chọn Tải lên (Upload).

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task38_Hosting_Usage/Images/15.png" /></p>

###WinSCP

**Kết nối tới host**

Điền thông tin rồi click **Login** để kết nối

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task39_FTP_Protocol/Images/1.png" /></p>

**Upload file**

Bạn chọn tập tin cần upload trên máy và chọn thư mục lưu trữ của tập trên host (thường là thư mục public_html). Sau đó bạn chuột phải vào file cần upload rồi chọn Upload.

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task39_FTP_Protocol/Images/2.png)

###CuteFTP

**Kết nối tới host**

Điền thông tin rồi click ![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task39_FTP_Protocol/Images/5.png) để kết nối

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task39_FTP_Protocol/Images/3.png" /></p>

**Upload file**

Bạn chọn tập tin cần upload trên máy và chọn thư mục lưu trữ của tập trên host (thường là thư mục public_html). Sau đó bạn chuột phải vào file cần upload rồi chọn Upload.

![](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task39_FTP_Protocol/Images/4.png)

<a name="5"></a>
#5.Tài liệu tham khảo

https://vi.wikipedia.org/wiki/FTP

http://aita.gov.vn/tin-tuc/1353/tieu-chuan-ftp-giao-thuc-truyen-tep-tin

https://github.com/hoangdh/ghichep-FTP

