## HTTP The Definitive Guide Page 8 to 11


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **1/11/2016**

### Mục lục
[1.4 Transactions](#14)
 
- [1.4.1 Methods](#141)
 
- [1.4.2 Status Codes](#142)
 
- [1.4.3 Web Pages Can Consist of Multiple Object](#143)
 
[1.5 Messages](#15)
 
- [1.5.1 Simple Message Example](#151)

---

<a name="14"></a>
#1.4 Transactions (giao dịch)

Hãy xem chi tiết hơn cách client sử dụng HTTP để giao dịch với các máy chủ web và các nguồn lực của họ. Một giao dịch HTTP bao gồm một lệnh yêu cầu (được gửi từ client đến server), và một kết quả phản ứng (được gửi từ server lại cho client). thông tin liên lạc này sẽ xảy ra với các khối định dạng dữ liệu được gọi là thông điệp HTTP, như minh họa trong hình 1-5.

<p align="center"><em>1-5. giao dịch HTTP bao gồm các thông điệp yêu cầu và phản ứng</em></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task27_HTTP_The_Difinitive_Guide_Page_8to11/Images/1.png" /></p>

<a name="141"></a>
###1.4.1 Methods (phương thức)

HTTP hỗ trợ các lệnh yêu cầu khác nhau, được gọi là phương thức HTTP. Mỗi tin yêu cầu HTTP có một phương thức. Phương thức này cho máy chủ những hành động để thực hiện (lấy một trang web, chạy một chương trình gateway, xóa một tập tin, vv).

<p align="center"><em>Bảng 1-2 liệt kê năm phương pháp HTTP thông thường.</em></p>

|HTTP method|Mô tả|
|-----------|------|
|GET|Gửi tài nguyên được đặt tên từ các server cho client.|
|PUT|Lưu trữ dữ liệu từ client vào một nguồn tài nguyên tên server|
|DELETE|Xóa các tài nguyên được đặt tên từ một server.|
|POST|Gửi dữ liệu client vào một ứng dụng server gateway|
|HEAD|Chỉ gửi các tiêu đề HTTP từ các phản ứng đối với các nguồn tài nguyên được đặt tên.|

<a name="142"></a>
###1.4.2 Status Codes (mã trạng thái)

Mọi thông điệp HTTP phản ứng trở lại với một mã trạng thái. Các mã trạng thái là một mã số có ba chữ số cho khách hàng nếu yêu cầu thành công, hoặc nếu các hành động khác được yêu cầu. Một vài mã trạng thái thông thường được thể hiện trong Bảng 1-3.

<p align="center"><em>Bảng 1-3. Một số mã trạng thái HTTP thông thường</em></p>

|HTTP status code|Mô tả|
|-|-|
|300|OK. Document returned correctly. (ĐƯỢC. Tài liệu quay trở lại một cách chính xác.)|
|302|Redirect. Go someplace else to get the resource. (Chuyển. Tới nơi nào khác để có được những tài nguyên.)|
|404|Not Found. Can't find this resource(Không tìm thấy. Không thể tìm thấy tài nguyên này)|

HTTP cũng sẽ gửi một văn bản "cụm từ lý do" giải thích với từng mã trạng thái số (xem các tin nhắn phản ứng trong Hình 1-5). Các cụm từ văn bản được bao gồm chỉ cho mục đích mô tả; mã số được sử dụng cho tất cả các tiến trình xử lý.

Các mã trạng thái sau và cụm từ được điều cho là giống nhau của phần mềm HTTP:

![3](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task27_HTTP_The_Difinitive_Guide_Page_8to11/Images/3.png)

<a name="143"></a>
###1.4.3 Web Pages Can Consist of Multiple Objects (Các trang web có thể bao gồm nhiều đối tượng)

Một ứng dụng thường chia thành nhiều giao dịch HTTP để hoàn thành một nhiệm vụ. Ví dụ, một trình duyệt web đưa ra một chuỗi các giao dịch HTTP để lấy và hiển thị một trang web đồ họa. Các trình duyệt để thực hiện một giao dịch để lấy "khung" HTML mô tả cách bố trí trang, sau đó ban hành các giao dịch HTTP bổ sung cho mỗi hình ảnh nhúng, bảng điều khiển đồ họa, Java applet, vv. Những nguồn lực nhúng thậm chí có thể cư trú trên các server khác nhau, như trong hình 1-6. Do đó, một "trang web" thường là một tập hợp các nguồn lực, không phải là một nguồn duy nhất.

<p align="center"><em>Hình 1-6. các trang web tổng hợp yêu cầu giao dịch HTTP riêng biệt cho mỗi
nguồn tài nguyên nhúng</em></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task27_HTTP_The_Difinitive_Guide_Page_8to11/Images/4.png" /></p>

<a name="15"></a>
#1.5 Messages (tin nhắn)

Bây giờ chúng ta hãy có một cái nhìn nhanh cấu trúc của yêu cầu HTTP và thông điệp trả lời. Chúng ta sẽ nghiên cứu các thông điệp HTTP chi tiết tinh tế trong Chương 3.

tThông điệp HTTP đơn giản, trình tự dòng theo định hướng của người dùng. Bởi vì chúng là văn bản đơn giản, không nhị phân, chúng dễ dàng cho người đọc và viết. Hình 1-7 cho thấy các thông điệp HTTP cho một giao dịch đơn giản.

*Một số lập trình viên phàn nàn về những khó khăn của HTTP như phân tích cú pháp, có thể gặp nhiều được khó khăn và dễ bị lỗi, đặc biệt là khi thiết kế phần mềm tốc độ cao. Một định dạng nhị phân hoặc một định dạng văn bản hạn chế hơn có thể được đơn giản để xử lý, nhưng hầu hết các lập trình viên HTTP đánh giá cao HTTPs mở rộng và debuggability.*

<p align="center"><em>Hình 1-7. thông điệp HTTP đơn giản, dòng định hướng cấu trúc văn bản đơn giản</em></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task27_HTTP_The_Difinitive_Guide_Page_8to11/Images/5.png" /></p>

Thông điệp HTTP gửi từ web client đến các web server được gọi là thông điệp yêu cầu. Tin nhắn từ server cho khách hàng được gọi là thông điệp trả lời. Không có các loại khác của thông điệp HTTP. Các định dạng của HTTP yêu cầu và đáp ứng các thông điệp là rất giống nhau. Thông điệp HTTP bao gồm ba phần:

![6](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task27_HTTP_The_Difinitive_Guide_Page_8to11/Images/6.png)

Dòng đầu tiên của tin nhắn là dòng bắt đầu, cho thấy những gì làm cho một yêu cầu hoặc những gì đã xảy ra cho một phản ứng.

![7](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task27_HTTP_The_Difinitive_Guide_Page_8to11/Images/7.png)

Zero hoặc nhiều trường tiêu đề theo dòng bắt đầu. Mỗi trường tiêu đề bao gồm một cái tên và một giá trị, cách nhau bằng dấu hai chấm (:) cho dễ phân tích cú pháp. Các tiêu đề kết thúc với một dòng trống. Thêm một trường tiêu đề là dễ dàng như việc thêm một dòng khác.

![8](https://github.com/thanhnhut/sysadmin_level1/blob/master/Task27_HTTP_The_Difinitive_Guide_Page_8to11/Images/8.png)

Sau dòng trống là một thân thư tùy chọn có chứa bất kỳ loại dữ liệu. Thân yêu cầu mang dữ liệu đến web server; thân phản ứng mang dữ liệu lại cho client. Không giống như các dòng bắt đầu và tiêu đề, đó là văn bản và cấu trúc, thân có thể chứa dữ liệu nhị phân tùy ý (ví dụ, hình ảnh, video, âm thanh, phần mềm ứng dụng). Tất nhiên, thân cũng có thể chứa văn bản.

<a name="151"></a>
###1.5.1 Simple Message Example (ví dụ thông điệp đơn giản)

Hình 1-8 cho thấy các thông điệp HTTP có thể được gửi như là một phần của một giao dịch đơn giản. Trình duyệt yêu cầu các tài nguyên http://www.joes-hardware.com/tools.html. 

<p align="center"><em>Hình 1-8. Ví dụ GET giao dịch cho http://www.joes-hardware.com/tools.html</em></p>


<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task27_HTTP_The_Difinitive_Guide_Page_8to11/Images/9.png" /></p>

Trong hình 1-8, trình duyệt sẽ gửi một thông điệp yêu cầu HTTP. Các yêu cầu có một phương thức GET trong dòng bắt đầu, và các nguồn lực địa phương là /tools.html. Các yêu cầu cho biết nó đang nói Phiên bản 1.0 của giao thức HTTP. Thông điệp yêu cầu không có thân, bởi vì không có dữ liệu yêu cầu là cần thiết để GET một tài liệu đơn giản từ một server.Các server sẽ gửi lại một tin nhắn phản ứng HTTP. Các phản ứng có chứa các số phiên bản HTTP (HTTP / 1.0), một mã trạng thái thành công (200), một cụm từ lý do mô tả (OK), và một khối của các trường đáp ứng tiêu đề, tất cả tiếp theo phản ứng thân có chứa các tài liệu yêu cầu.Chiều dài thân phản ứng được ghi rõ trong tiêu đề Content-Length, và kiểu MIME của tài liệu được ghi rõ trong tiêu đề Content-Type
