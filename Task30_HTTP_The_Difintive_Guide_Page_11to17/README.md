## <font color="#0000FF">HTTP The Definitive Guide Page 11 to 17</font>


> 
> <font color="red">Thực hiện: **Nguyễn Thanh Nhựt**
> 
> <font color="red">Cập nhật lần cuối: **9/11/2016**</font>

### Mục lục

[1.6 Connections](#16)

 - [1.6.1 TCP/IP](#161)

 - [1.6.2 Connections, IP Address and Port Number](#162)

 - [1.6.3 A Real Example Using Telnet](#163)

[1.7 Protocol Versions](#17)

[1.8  Architectural Components of the Web ](#18)

---

<a name="16"></a>
#<font color="#0000FF">1.6 Connections</font>

Bây giờ chúng ta đã có một sự tóm tắt về một thông điệp HTTP trông như thế nào, chúng ta hãy nói một chút về cách các thông điệp di chuyển từ nơi này đến nơi khác, thông qua giao thức kết nối TCP (Tranmisstion Control Protocol).

<a name="161"></a>
###<font color="#0000FF">1.6.1 TCP/IP</font>

HTTP là một giao thức lớp ứng dụng. HTTP không lo lắng về các chi tiết thực dụng của mạng giao tiếp; thay vào đó, nó để lại các chi tiết của mạng TCP / IP, giao thức vận chuyển phổ biến tin cậy IP(Internet transport protocol).

TCP cung cấp:

- Vận chuyển dữ liệu không bị lỗi.
- Trong khi chuyển (dữ liệu sẽ luôn đến theo thứ tự mà trong đó nó đã được gửi) .
- Dòng dữ liệu Unsegmented (có thể truyền dữ liệu ở bất kỳ kích thước bất cứ lúc nào)

Internet được dựa trên giao thức TCP / IP, một giao thức mạng phổ biến dùng  chuyển mạch gói được biết bởi các máy tính và các thiết bị mạng trên khắp thế giới. TCP / IP ẩn các yếu tố đặc trưng điểm yếu của các mạng cá nhân và phần cứng, cho phép máy tính và mạng của bất kỳ kiểu nói chuyện với nhau cách đáng tin cậy. 

Khi một kết nối TCP được thiết lập, thông điệp trao đổi giữa client và máy tính server sẽ không bao giờ bị mất, bị hư hỏng, hoặc nhận sai yêu cầu.

Trong một giới hạn mạng, các giao thức HTTP được xếp trên lớp TCP. HTTP sử dụng TCP để truyền tải dữ liệu thông điệp của mình. Tương tự như vậy, TCP là lớp over IP (xem hình 1-9).


<p align="center"><em>Hình 1-9. HTTP giao thức mạng stack</em></p>


<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/1.png" /></p>


<a name=162"></a>
###<font color="#0000FF">1.6.2 Connections, IP Address and Port Number</font>

Trước khi một HTTP client có thể gửi một tin nhắn đến một server, nó cần phải thiết lập một kết nối TCP / IP giữa client và địa chỉ server sử dụng giao thức Internet (IP) và số cổng.

Thiết lập một kết nối TCP giống như gọi một người nào đó tại một văn phòng công ty. Đầu tiên, bạn gọi số điện thoại của công ty. Điều này giúp bạn để việc tổ chức đúng. Sau đó, bạn gọi các phần mở rộng cụ thể của người mà bạn đang cố gắng để liên lạc được.

Trong TCP, bạn cần có địa chỉ IP của máy tính server và số cổng TCP kết hợp với các chương trình phần mềm cụ thể chạy trên server.

Tất cả điều này là tốt, nhưng làm thế nào để bạn có được địa chỉ IP và số cổng của máy chủ HTTP ở nơi đầu tiên? Tại sao, URL, tất nhiên! Chúng ta đã đề cập trước đó URL là địa chỉ cho nguồn lực, vì thế một cách tự nhiên họ có thể cung cấp đủ cho chúng ta với địa chỉ IP cho themachine có tài nguyên. Chúng ta hãy xem xét một vài URL:

http://207.200.83.29:80/index.html 
http://www.netscape.com:80/index.html 
http://www.netscape.com/index.html 

URL đầu tiên có địa chỉ IP của máy, "207.200.83.29", và số cổng, "80". URL thứ hai không có một địa chỉ IP dạng số; nó có một tên tên miền, hoặc tên máy ("www.netscape.com"). Tên máy chỉ là một bí danh thân thiện cho một địa chỉ IP. Hostname có thể dễ dàng được chuyển đổi thành địa chỉ IP thông qua một cơ sở gọi là dịch vụ tên miền (DNS), vì vậy chúng ta cũng có tất cả các thiết lập ở đây. Chúng ta sẽ nói nhiều hơn về DNS và URL trong Chương 2.

URL cuối cùng không có số cổng. Khi số cổng bị mất từ một HTTP URL, bạn có thể giả định các giá trị mặc định của cổng 80.

Với địa chỉ IP và số cổng, một client có thể dễ dàng giao tiếp thông qua giao thức TCP / IP. Hình 1-10 cho thấy làm thế nào một trình duyệt sử dụng HTTP để hiển thị một nguồn HTML đơn giản mà nằm trên một server ở xa.

Đây là các bước:


![2](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/2.png)


<p align="center">Trình duyệt lấy ra tên máy của server từ URL.</p>


![2](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/3.png)


<p align="center">Trình duyệt chuyển đổi tên máy của server vào địa chỉ IP của server.</p>


![2](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/4.png)


<p align="center">Trình duyệt sẽ lấy ra từ các số cổng (nếu có) từ URL.</p>


![2](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/5.png)


<p align="center">Các trình duyệt thiết lập một kết nối TCP với web server.</p>


![2](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/6.png)


<p align="center">Trình duyệt sẽ gửi một thông điệp HTTP request  đến server.</p>


![2](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/7.png)


<p align="center">Các server sẽ gửi một HTTP response lại cho trình duyệt.</p>


![2](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/8.png)


<p align="center">Các kết nối được đóng lại, và trình duyệt sẽ hiển thị các tài liệu</p>


<p align="center"><em>Hình 1-10. Quá trình kết nối trình duyệt cơ bản</em></p>


<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/9.png" /></p>

<a name="163"></a>
###<font color="#0000FF">1.6.3 A Real Example Using Telnet</font>

Bởi vì HTTP sử dụng giao thức TCP / IP, và dựa trên văn bản, như trái ngược với sử dụng một số định dạng nhị phân tối nghĩa, nó thì đơn giản để nói chuyện trực tiếp với một web server.

Các tiện ích Telnet kết nối bàn phím của bạn đến một điểm đến cổng TCP và kết nối đầu ra cổng TCP trở lại màn hình hiển thị của bạn. Telnet thường được sử dụng cho các phiên điều khiển terminal từ xa, nhưng nó thường có thể kết nối với bất kỳ TCP server, bao gồm các HTTP server.

Bạn có thể sử dụng tiện ích Telnet để nói chuyện trực tiếp với các web server. Telnet cho phép bạn mở một kết nối TCP tới một cổng trên máy tính và kiểu ký tự trực tiếp vào cổng. Các web server xem bạn như một web client, và bất kỳ dữ liệu được gửi trở lại trên các kết nối TCP được hiển thị trên màn hình. 

Hãy sử dụng Telnet để tương tác với một web server thực sự. Chúng ta sẽ sử dụng Telnet để lấy các tài liệu được trỏ đến bởi URL http://www.joes-hardware.com:80/tools.html (bạn có thể thử ví dụ một này mình).

Hãy xem những gì sẽ xảy ra:

- Đầu tiên, chúng ta cần phải tìm địa chỉ IP của www.joes-hardware.com và mở một TCP kết nối đến cổng 80 trên máy đó. 

- Telnet làm legwork này cho chúng ta. Khi kết nối TCP được mở ra, chúng ta cần phải nhập vào các yêu cầu HTTP request. 

- Khi công việc hoàn tất (chỉ ra bởi một dòng trống), server sẽ gửi lại các nội dung trong một phản ứng HTTP và đóng kết nối. 

Ví dụ của chúng ta HTTP request cho http://www.joes-hardware.com:80/tools.html được hiển thị trong ví dụ 1-1. Những gì chúng ta đã gõ được thể hiện dưới dạng in đậm.

####Ví dụ 1-1. Một giao dịch HTTP sử dụng telnet


![](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/10.png)


![](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/11.png)


Telnet nhìn lên tên máy và mở một kết nối đến máy chủ www.joes-hardware.com web, được lắng nghe trên cổng 80. ba dòng sau khi lệnh được xuất ra từ Telnet, nói với chúng ta nó đã thiết lập một kết nối. Sau đó chúng ta gõ vào lệnh yêu cầu cơ bản , "GET /tools.html HTTP / 1.1", và gửi một tiêu đề chủ cung cấp tên máy ban đầu, theo sau là một dòng trống, yêu cầu server để GET những tài nguyên "/tools.html" từ máy chủ www.joes-hardware.com. Sau đó, server đáp ứng với một dòng phản ứng, một số tiêu đề phản ứng, một dòng trống, và cuối cùng là phần thân của tài liệu HTML. 

Hãy coi chừng Telnet bắt chước HTTP client tốt nhưng không làm việc tốt như một server. Và tự động Telnet là không có vui. Đối với một công cụ linh hoạt hơn, bạn có thể muốn kiểm tra **nc** (netcat). Các công cụ **nc** cho phép bạn dễ dàng thao tác và bản UDP- và lưu lượng dựa trên TCP, bao gồm cả HTTP. Xem http://www.bgw.org/tutorials/utilities/nc.php để biết chi tiết.

<a name="17"></a>
#<font color="#0000FF">1.7 Protocol Versions</font>

Có một số phiên bản của giao thức HTTP chúng ta sử dụng ngày nay. ứng dụng HTTP cần phải làm việc chăm chỉ để xử lý mạnh mẽ biến thể khác nhau của giao thức HTTP. Các phiên bản được sử dụng là:


![](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/12.png)


Phiên bản 1991 nguyên mẫu của HTTP được gọi là HTTP / 0.9. Giao thức này có chứa nhiều lỗ hổng thiết kế nghiêm trọng và cần được sử dụng chỉ để tương thích với các khách hàng di sản. HTTP / 0.9 chỉ hỗ trợ các phương thức GET, và nó không hỗ trợ MIME gõ nội dung đa phương tiện, tiêu đề HTTP, hoặc số phiên bản. HTTP / 0.9 ban đầu được xác định để lấy đối tượng HTML đơn giản. Nó nhanh chóng được thay thế bằng HTTP / 1.0.

![](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/13.png)

1.0 là phiên bản đầu tiên của HTTP đã được triển khai rộng rãi. HTTP / 1.0 thêm số phiên bản, tiêu đề HTTP, phương pháp bổ sung, đa phương tiện và đối tượng xử lý. HTTP / 1.0 đã làm cho nó thực tế để hỗ trợ các trang web đồ họa hấp dẫn và các hình thức tương tác, giúp thúc đẩy việc áp dụng rộng quy mô của World Wide Web. đặc điểm kỹ thuật này chưa bao giờ xác định tốt. Nó đại diện cho một tập hợp các thực hành tốt nhất trong một thời gian tiến hóa thương mại và học thuật nhanh chóng của các giao thức.


![](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/14.png)


Nhiều khách hàng web phổ biến và máy chủ nhanh chóng bổ sung các tính năng HTTP vào giữa năm 1990 để đáp ứng nhu cầu của một mở rộng nhanh chóng, thương mại thành công World Wide Web. Nhiều người trong số các tính năng này, bao gồm cả các kết nối lâu dài "keep-alive", hỗ trợ lưu trữ ảo, và hỗ trợ kết nối proxy, đã được thêm vào HTTP và trở thành chính thức, trên thực tế tiêu chuẩn. Điều này không chính thức, phiên bản mở rộng của HTTP thường được gọi là HTTP / 1.0 +.


![](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/15.png)


HTTP / 1.1 tập trung vào việc sửa chữa sai sót về kiến trúc trong thiết kế của HTTP, xác định ngữ nghĩa, giới thiệu tối ưu hóa hiệu suất đáng kể, và loại bỏ tính năng sai. HTTP / 1.1 cũng bao gồm hỗ trợ cho các ứng dụng web phức tạp hơn và triển khai ở dưới đường vào cuối năm 1990. HTTP / 1.1 là phiên bản hiện tại của HTTP.


![](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/16.png)


HTTP-NG là một đề nghị nguyên mẫu cho người kế nhiệm một archit ectural HTTP / 1.1 tập trung vào tối ưu hóa hiệu suất đáng kể và một khuôn khổ mạnh mẽ hơn cho thực hiện từ xa của logic server. Các nỗ lực nghiên cứu HTTP-NG kết luận vào năm 1998, và tại thời điểm viết bài này, không có kế hoạch để thúc đẩy đề xuất này như một sự thay thế cho HTTP / 1.1. Xem Chương 10 để biết thêm thông tin.


<a name="18"></a>
#<font color="#0000FF">1.8  Architectural Components of the Web (các thành phần kiến trúc của web)</font>

Trong chương tổng quan này, chúng tôi đã tập trung vào việc làm thế nào hai ứng dụng web (trình duyệt web và web server) gửi tin nhắn qua lại để thực hiện các giao dịch cơ bản. Có rất nhiều các ứng dụng web khác mà bạn tương tác với trên Internet. Trong phần này, chúng tôi sẽ nêu một số ứng dụng quan trọng khác, bao gồm:


![2](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/17.png)


<p align="center">HTTP trung gian mà ngồi giữa client và server.</p>


![2](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/18.png)


<p align="center">kho HTTP giữ bản sao của các trang web phổ biến gần client.</p>


![2](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/19.png)


<p align="center">Các web server đặc biệt để kết nối với các ứng dụng khác.</p>


![2](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/20.png)


<p align="center">Proxy đặc biệt không nhìn thấy HTTP giao tiếp phía trước.</p>


![2](https://github.com/thanhnhut/sysadmin_level1/tree/master/Task30_HTTP_The_Difintive_Guide_Page_11to17/Images/21.png)


<p align="center">Web client thông minh làm HTTP request tự động.</p>








