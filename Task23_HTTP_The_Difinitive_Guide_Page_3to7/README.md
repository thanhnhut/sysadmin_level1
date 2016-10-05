## Đọc và dịch sách "HTTP The Difinitive Guide 2002"


> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **4/10/2016**

---

##Mục lục

[1. Tổng quan về HTTP](#1)

- [1.1 Đa phương tiện chuyển phát nhanh của Internet](#11)

- [1.2 Web Clients and Servers](#12)

- [1.3 Tài nguyên web](#13)

 - [1.3.1 Các phương tiện truyền thông](#131)

 - [1.3.2 URIs](#132)

 - [1.3.3 URLs](#133)

 - [1.3.4 URNs](#134)



<a name="1"></a>
#1. Tổng quan về HTTP

Thế giới trình duyệt web, máy chủ và các ứng dụng web có liên quan tất cả các cuộc nói chuyện với nhau lại thông qua HTTP, Hypertext Transfer Protocol. HTTP là ngôn ngữ phổ biến của Internet toàn cầu hiện đại.

Chương này là một tổng quan ngắn gọn của HTTP. Bạn sẽ thấy cách ứng dụng web sử dụng HTTP để giao tiếp, và bạn sẽ có được một ý tưởng thô về cách thức HTTP làm công việc của mình. Đặc biệt, chúng tôi nói chuyện về:

- Làm thế nào khách hàng web và máy chủ giao tiếp

- Nơi các nguồn lực (nội dung web) đến từ đâu

- Làm thế nào các giao dịch web làm việc

- Các định dạng của thông điệp được sử dụng để giao tiếp HTTP

- Việc vận chuyển mạng TCP cơ bản

- Các biến thể khác nhau của giao thức HTTP

- Một số trong rất nhiều thành phần kiến trúc HTTP được cài đặt trên Internet

Chúng tôi đã có rất nhiều đất để trang trải, do đó, hãy bắt đầu chuyến tham quan của chúng ta về HTTP.

<a name="11"></a>
###1.1 Đa phương tiện chuyển phát nhanh của Internet

Hàng tỷ hình ảnh JPEG, các trang HTML, các file văn bản, phim MPEG, file âm thanh WAV, Java applet, và nhiều hành trình qua Internet mỗi ngày. HTTP di chuyển số lượng lớn các thông tin này một cách nhanh chóng, thuận tiện, và đáng tin cậy từ các máy chủ web trên toàn thế giới với các trình duyệt web trên máy tính của mọi người.

Bởi vì HTTP sử dụng giao thức truyền dữ liệu đáng tin cậy, nó đảm bảo rằng dữ liệu của bạn sẽ không được hư hỏng hoặc bị xáo trộn trong quá trình chuyển, ngay cả khi nó đến từ phía bên kia của địa cầu. Điều này tốt cho bạn như là một người sử dụng, bởi vì bạn có thể truy cập thông tin mà không cần lo lắng về tính toàn vẹn của nó. Đường truyền đáng tin cậy  cũng tốt cho bạn  như là một nhà phát triển ứng dụng Internet, bởi vì bạn không cần phải lo lắng về thông tin liên lạc HTTP bị phá hủy, sao chép, hoặc bị bóp méo quá trình. Bạn có thể tập trung về lập trình các chi tiết khác biệt của ứng dụng của bạn, mà không lo lắng về những sai sót và
nhược điểm của Internet.

Hãy xem xét kỹ hơn cách thức HTTP chuyển tải lưu lượng của Web

<a nae="12"></a>
###1.2 Web Clients and Servers

Nội dung web trên các máy chủ web. Máy chủ Web nói giao thức HTTP, do đó chúng thường được gọi các máy chủ HTTP. Các máy chủ lưu trữ dữ liệu HTTP của Internet và cung cấp các dữ liệu khi nó được yêu cầu bởi khách hàng của HTTP. Các khách hàng gửi yêu cầu HTTP tới máy chủ, và máy chủ trả lại dữ liệu yêu cầu trong phản ứng HTTP, như phác họa trong Hình 1-1. Cùng nhau, HTTP client và HTTP server, tạo nên thành phần cơ bản của World Wide Web.

<center><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task23_HTTP_The_Difinitive_Guide_Page_3to7/Images/1.jpg" ></center> <center>*Hình 1-1 Web clients and servers*</center>

Bạn có thể sử dụng HTTP clients mỗi ngày. Các client phổ biến nhất là một trình duyệt web, chẳng hạn như Microsoft Internet Explorer hoặc Netscape Navigator. Trình duyệt Web yêu cầu đối tượng HTTP từ máy chủ
và hiển thị các đối tượng trên màn hình của bạn. 

<a name="13"></a>
###1.3 Tài nguyên

Các web server lưu trữ tài nguyên web. Một nguồn tài nguyên web là nguồn gốc của nội dung web. Các loại nguồn tài nguyên web đơn giản nhất là một tập tin tĩnh về hệ thống tập tin máy chủ web. Những tập tin này có thể chứa bất cứ điều gì: họ có thể là các file văn bản, file HTML,       các file Microsoft Word, Adobe Acrobat, tập tin hình ảnh JPEG, AVI file phim, hoặc bất kỳ định dạng khác mà bạn có thể nghĩ đến.

Tuy nhiên, các nguồn tài nguyên không phải là tập tin tĩnh. Tài nguyên cũng có thể là các chương trình phần mềm mà tạo ra nội dung theo yêu cầu.  Các nguồn tài nguyên nội dung động có thể tạo ra nội dung dựa trên danh tính của bạn, trên những thông tin mà bạn yêu cầu, hoặc vào thời gian trong ngày. Họ có thể cho bạn một hình ảnh trực tiếp từ máy ảnh, hoặc cho phép bạn giao dịch cổ phiếu, tìm kiếm cơ sở dữ liệu bất động sản, hay mua quà tặng từ các cửa hàng trực tuyến (xem Hình 1-2).

<center><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task23_HTTP_The_Difinitive_Guide_Page_3to7/Images/2.png" ></center> <center>*Hình 1-2 Một nguồn tài nguyên web là bất cứ điều gì mà cung cấp nội dung web*</center>

Tóm lại, một nguồn tài nguyên là bất kỳ loại nguồn nội dung. Một tập tin có chứa dự báo bán hàng bảng tính của công ty bạn là một nguồn tài nguyên. Một cổng web để quét kệ thư viện công cộng tại địa phương của bạn là một tài nguyên. Một công cụ tìm kiếm Internet là một nguồn tài nguyên.

<a name="131"></a>
###1.3.1 Các phương tiện truyền thông

Bởi vì có nhiều Internet host với hàng ngàn các loại dữ liệu khác nhau, HTTP cẩn thận gắn thẻ mỗi đối tượng đang được vận chuyển qua các trang web với một nhãn định dạng dữ liệu được gọi là một loại MIME. MIME (Multipurpose Internet Mail Extensions) được thiết kế để giải quyết vấn đề gặp phải trong việc di chuyển tin nhắn giữa các hệ thống thư điện tử khác nhau. MIME làm việc rất tốt cho email HTTP thông qua nó để mô tả và ghi nhãn nội dung đa phương tiện riêng của mình.

Web server đính kèm một loại MIME cho tất cả các đối tượng dữ liệu HTTP (xem hình 1-3). Khi một trình duyệt web trở thành một đối tượng trở về từ một máy chủ, nó giống như một kiểu MIME liên quan để xem nếu nó biết làm thế nào để xử lý các đối tượng. Hầu hết các trình duyệt có thể xử lý hàng trăm loại đối tượng phổ biến: hiển thị các tập tin hình ảnh, phân tích và định dạng tập tin HTML, chơi các tập tin âm thanh thông qua loa của máy tính, hoặc tung ra bên ngoài plug-in phần mềm để xử lý các định dạng đặc biệt. 

<center><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task23_HTTP_The_Difinitive_Guide_Page_3to7/Images/3.png" ></center> <center>*Hình 1-3. loại MIME được gửi trở lại với nội dung dữ liệu*</center>

Một loại MIME là một nhãn văn bản, biểu diễn như là một loại đối tượng chính và một subtype cụ thể, cách nhau bằng một dấu gạch chéo. Ví dụ:

- Một tài liệu văn bản dạng HTML sẽ được gắn nhãn với loại **text /html**

- Một tài liệu văn bản ASCII sẽ được gắn nhãn với loại **text /plain**

- Một phiên bản JPEG của một hình ảnh sẽ được **image /jpeg**

- Một hình ảnh GIF định dạng sẽ là **image / gif**

- Một bộ phim QuickTime của Apple sẽ là **video / quicktime**

- Một bài thuyết trình Microsoft PowerPoint sẽ là **applications / vnd.ms powerpoint**

Có hàng trăm loại MIME phổ biến, và nhiều loại thử nghiệm nhiều hơn hoặc hạn chế sử dụng. Rất nhiều danh sách kiểu MIME được cung cấp trong Phụ lục D.

<a name="132"></a>
###1.3.2 URIs

Mỗi tài nguyên web server có một cái tên, vì vậy khách hàng có thể chỉ ra những nguồn lực mà họ đang quan tâm. Tên tài nguyên máy chủ được gọi là một Uri, hoặc URI. URI giống như các địa chỉ bưu chính của Internet, duy nhất xác định và định vị các nguồn thông tin trên toàn thế giới.

Dưới đây là một URI cho một nguồn tài nguyên hình ảnh trên phần cứng máy chủ cửa hàng web của Joe:

http://www.joes-hardware.com/specials/saw-blade.gif

Hình 1-4 cho thấy cách các URI chỉ định các giao thức HTTP để truy cập tài nguyên lưỡi cưa GIF trên máy chủ lưu trữ của Joe. Với URI, HTTP có thể lấy các đối tượng. URIs đến trong hai vị, được gọi là URL và URNs. Chúng ta hãy nhìn qua mỗi một trong các loại định danh tài nguyên bây giờ.

<center><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task23_HTTP_The_Difinitive_Guide_Page_3to7/Images/4.png" ></center> <center>*Hình 1-4. URLs chỉ định giao thức, máy chủ, và tài nguyên địa phương*</center>

<a name="133"></a>
###1.3.3 URLs 

Các bộ định vị tài nguyên thống nhất (URL) là hình thức phổ biến nhất của định danh tài nguyên. URL mô tả vị trí cụ thể của một tài nguyên trên một máy chủ cụ thể. Họ nói với bạn một cách chính xác làm thế nào để lấy tài nguyên từ một, vị trí cố định chính xác. Hình 1-4 cho thấy cách một URL nói chính xác nơi một nguồn tài nguyên nằm và làm thế nào để truy cập vào nó. Bảng 1.1 cho thấy một vài ví dụ về URL.

*Bảng 1.1 ví dụ URLs*

|URL														|Mô tả																			|
|-----------------------------------------------------------|------------------------------------------------------------------------------|
|http://www.oreilly.com/index.html							| The home URL for O'Reilly & Associates, Inc 									|
|http://www.yahoo.com/images/logo.gif						| URL cho biểu tượng trang web của Yahoo!										|	
|http://www.joes-hardware.com/inventorycheck.cgi?item=12731 | URL cho một chương trình kiểm tra nếu hàng tồn kho mục # 12.731 là trong kho																													|
|ftp://joe:tools4u@ftp.joes-hardware.com/lockingpliers.gif 	| URL của tập tin hình ảnh khóa-pliers.gif, sử dụng mật khẩu bảo vệ FTP như truy cập giao thức																																 |																					|																									

Hầu hết các URL theo một định dạng chuẩn của ba phần chính:

- Phần đầu tiên của URL được gọi là kế hoạch, và nó mô tả các giao thức dùng để truy cập các tài nguyên. Điều này thường là các giao thức HTTP (http: //).

- Phần thứ hai cung cấp cho các máy chủ địa chỉ Internet (ví dụ, www.joe's-hardware.com).

- Những cái tên còn lại một nguồn tài nguyên trên máy chủ web (ví dụ, /specials/saw-blade.gif).

Ngày nay, hầu hết các URI là một URL.

<a name="134"></a>
###1.3.4 URNs

Các hương thứ hai của URI là tên tài nguyên thống nhất, hoặc URN. Một URN phục vụ như là một tên duy nhất cho một phần của nội dung, độc lập với các nơi có tài nguyên hiện đang cư trú. Những vị trí URNs độc lập  cho phép các nguồn lực để di chuyển từ nơi này đến nơi khác. URNs cũng cho phép các nguồn lực để được truy cập bởi nhiều giao thức truy cập mạng trong khi duy trì cùng tên. Ví dụ, URN sau đây có thể được sử dụng để đặt tên cho tài liệu tiêu chuẩn Internet "RFC 2141" không phân biệt nơi nó cư trú (thậm chí nó có thể được sao chép ở một vài nơi):

**urn:ietf:rfc:2141**

URNs vẫn còn thử nghiệm và chưa được áp dụng rộng rãi. Để làm việc hiệu quả, URNs cần có một cơ sở hạ tầng hỗ trợ giải quyết vị trí tài nguyên; việc thiếu một cơ sở hạ tầng như vậy cũng đã chậm lại của họ
nhận con nuôi. Nhưng URNs giữ một số hứa hẹn thú vj cho tương lai. Chúng tôi sẽ thảo luận về URNs trong một vài chi tiết trong Chương 2, nhưng hầu hết các phần còn lại của cuốn sách này tập trung chủ yếu vào các URLs. 

Trừ khi có quy định, chúng tôi áp dụng các thuật ngữ thông thường và sử dụng URI và URL thay thế cho nhau trong phần còn lại của cuốn sách này.


																			
