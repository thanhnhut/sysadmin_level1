## HTTP The Difinitive Guide Page 17 to 22 


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **/11/2016**

### Mục lục
- [1.8.1 Proxies](#181)

- [1.8.2 Caches](#182)

- [1.8.3 Gateways](#183)

- [1.8.4 Tunnels](#184)

- [1.8.5 Agents](#185)

[1.9 The End of the Beginning](#19)

[1.10 For more Information](#110)

- [1.10.1 HTTP Protocol Information](#1101)

- [1.10.2 Historical Perspective](#1101)

- [1.10.3 Other World Wide Web Information](#1103)


---


<a name="181"></a>
###1.8.1 Proxies

Hãy bắt đầu bằng cách nhìn vào các HTTP proxy server, khối kiến trúc quan trọng đối với an ninh web, tích hợp ứng dụng và tối ưu hóa hiệu suất. 

Như thể hiện trong hình 1-11, một proxy nằm giữa một client và một server, nhận được tất cả các yêu cầu HTTP của client và chuyển tiếp các yêu cầu đến server (có lẽ sau khi thay đổi yêu cầu). Các ứng dụng này hoạt động như một đại diện cho người sử dụng, truy cập vào server 

<p align="center"><em>Hình 1-11. Proxy chuyển tiếp giao thông giữa server và client thay mặt của người dùng.</em></p>


<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task32_HTTP_The_Difinitive_Guide_Page_17to20/Images/1.png" /></p>


Proxy thường được sử dụng cho an ninh, làm trung gian đáng tin cậy thông qua các luồng lưu lượng web. Proxy cũng có thể lọc các yêu cầu và trả lời; Ví dụ, để phát hiện virus ứng dụng trong download của công ty hoặc để lọc nội dung người lớn đi từ học sinh tiểu học. Chúng ta sẽ nói về proxy chi tiết trong Chương 6


<a name="182"></a>
###1.8.2 Caches

Một bộ nhớ web cache hoặc bộ nhớ đệm proxy là một loại đặc biệt của HTTP proxy server mà vẫn giữ các bản sao của các tài liệu phổ biến đi qua proxy. Các client tiếp theo yêu cầu cùng một tài liệu có thể được phục vụ từ cá nhân bộ nhớ cache (xem hình 1-12).


<p align="center"><em>Hình 1-12. proxy caching giữ bản sao địa phương của các tài liệu phổ biến để cải thiện hiệu suất.</em></p>


<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task32_HTTP_The_Difinitive_Guide_Page_17to20/Images/2.png" /></p>


Một khách hàng có thể tải tài liệu nhanh hơn từ một bộ nhớ cache lân cận hơn là từ một web server từ xa. HTTP định nghĩa nhiều phương tiện để làm cho bộ nhớ đệm hiệu quả hơn và để điều chỉnh sự tươi mát và sự riêng tư của nội dung được lưu trữ. Chúng ta sẽ cover công nghệ bộ nhớ đệm trong Chương 7.


<a name="183"></a>
###1.8.3 Gateways

Gateway là server đặc biệt làm trung gian cho các server khác. Chúng thường được sử dụng để chuyển đổi giao thức HTTP để giao thức khác. Một gateway luôn luôn nhận được yêu cầu như thể nó là server gốc cho các nguồn tài nguyên. Các client có thể không biết nó đang giao tiếp với một gateway.

Ví dụ, một gateway HTTP / FTP nhận các yêu cầu cho FTP URIs người dùng qua các  HTTP request nhưng lấy về các tài liệu bằng cách sử dụng giao thức FTP (xem hình 1-13). Các kết quả tài liệu được đóng gói vào một thông điệp HTTP và gửi client. Chúng ta thảo luận về các cổng trong Chương 8.


<p align="center"><em>Hình 1-13. HTTP / FTP gateway.</em></p>


<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task32_HTTP_The_Difinitive_Guide_Page_17to20/Images/3.png" /></p>


<a name="184"></a>
###1.8.4 Tunnels (đường hầm)

Tunnels là ứng dụng HTTP, sau khi thiết lập, sẽ không thấy chuyển tiếp dữ liệu thô giữa hai kết nối. HTTP tunnels thường được sử dụng để vận chuyển  non-HTTP dữ liệu qua một hoặc nhiều kết nối HTTP, mà không nhìn vào các dữ liệu. Một sử dụng phổ biến của HTTP tunnels là để thực hiện mã hóa Secure Sockets Layer (SSL) chuyển giao thông qua một kết nối HTTP, cho phép lưu lượng SSL thông qua tường lửa nó chỉ cho phép lưu lượng web.

Như đã phác thảo trong hình 1-14, một HTTP / SSL tunnels nhận được một yêu cầu HTTP request để thiết lập một kết nối gửi đi đến một địa chỉ đích và cổng, rồi tiến tới tunnels, lưu lượng SSL được mã hóa trên kênh HTTP để nó có thể được chuyển tiếp đến các server đích.



<p align="center"><em>Hình 1-14. Tunnels chuyển dữ liệu qua mạng non-HTTP (HTTP / SSL tunnels show.</em></p>


<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task32_HTTP_The_Difinitive_Guide_Page_17to20/Images/4.png" /></p>


<a name="185"></a>
###1.8.5 Agents

Người dùng agent (hoặc chỉ agent) là những chương trình khách hàng có những yêu cầu HTTP request thay mặt của người sử dụng. Bất kỳ ứng dụng có vấn đề yêu cầu web request là một HTTP agent. Cho đến nay, chúng ta đã mới chỉ nói đến một loại HTTP agent: trình duyệt web. Nhưng có rất nhiều loại khác của các người dùng agent. 

Ví dụ, ta có các người dùng agent tự động đi lang thang trên web, phát hành các giao dịch HTTP và lấy nội dung, không có sự giám sát của con người. Các agent tự động thường có những cái tên màu mè, chẳng hạn như "Spiders" hoặc "webrobots" (xem hình 1-15). Spiders lang thang trên web để xây dựng kho lưu trữ hữu dụng của nội dung trang web, chẳng hạn như cơ sở dữ liệu công cụ tìm kiếm hoặc một danh mục sản phẩm cho một robot mua sắm. Xem Chương 9 để biết thêm thông tin.


<p align="center"><em>Hình 1-15. Công cụ tìm kiếm tự động "spiders" là agent, lấy các trang web
vòng quanh thế giới</em></p>


<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task32_HTTP_The_Difinitive_Guide_Page_17to20/Images/5.png" /></p>



<a name="19"></a>
#1.9 The End of the Beginning

Tất cả phần phía trên được cho là sự giới thiệu nhanh chóng của chúng ta về HTML. trong chương này, chúng ta nhấn mạnh vai trò của HTTP như một giao thức truyền tải đa phương tiện. Chúng ta đã vạch ra cách thức HTTP sử dụng URI để tên nguồn tài nguyên đa phương tiện trên các server từ xa, chúng ta đã phác thảo cách thức HTTP yêu cầu và đáp ứng các thông điệp được sử dụng để thao tác các nguồn tài nguyên đa phương tiện trên các server từ xa, và chúng ta đã hoàn thành việc khảo sát một vài trong số các ứng dụng web sử dụng HTTP.

Các chương còn lại giải thích các cơ cấu kỹ thuật của giao thức HTTP, các ứng dụng, và các nguồn lực cụ thể nhiều hơn.


<a name="110"></a>
#1.10 For more Information

Chương sau của cuốn sách này sẽ khám phá HTTP chi tiết hơn, nhưng bạn có thể thấy rằng một số các nguồn sau đây chứa nền tản hữu ích về chủ đề cụ thể, chúng ta đề cập trong chương này. 

<a name="1101"></a>
###1.10.1 HTTP Protocol Information

http://www.w3.org/Protocols/


Trang web W3C này có chứa nhiều liên kết tuyệt vời về các giao thức HTTP.


http://www.ietf.org/rfc/rfc2616.txt

RFC 2616, "Hypertext Transfer Protocol-HTTP / 1.1", là các đặc điểm kỹ thuật chính thức cho HTTP / 1.1, phiên bản hiện tại của giao thức HTTP. 



http://www.ietf.org/rfc/rfc1945.txt

RFC 1945, "Hypertext Transfer Protocol-HTTP / 1.0", là một RFC thông tin mô tả các nền tảng hiện đại cho HTTP.


http://www.w3.org/Protocols/HTTP/AsImplemented.html

Trang web này có chứa một mô tả của năm 1991 HTTP / 0.9 giao thức, mà chỉ thực hiện yêu cầu GET và không có người gõ nội dung.

<a name="1102"></a>
###1.10.2 Historical Perspective


http://www.w3.org/Protocols/WhyHTTP.html

Đây trang web ngắn từ năm 1991, từ các tác giả của HTTP, nhấn mạnh một số, mục tiêu tối giản ban đầu của HTTP.

http://www.w3.org/History.html

Một lịch sử nhỏ của World Wide Web "đưa ra một viễn cảnh ngắn nhưng thú vị về một số mục tiêu đầu và nền tảng của World Wide Web và HTTP.

http://www.w3.org/DesignIssues/Architecture.html

"Kiến trúc Web từ 50.000 Feet" vẽ nên một cái nhìn rộng, đầy tham vọng của World Wide Web và các nguyên tắc thiết kế có ảnh hưởng đến HTTP và các công nghệ web có liên quan.


<a name="1103"></a>
###1.10.3 Other World Wide Web Information

http://www.w3.org/

World Wide Web Consortium (W3C) là đội dẫn công nghệ cho Web. W3C phát triển công nghệ tương thích (thông số kỹ thuật, hướng dẫn, phần mềm và công cụ) cho phát triển Web. Trang web W3C là một kho tàng tài liệu giới thiệu và chi tiết về công nghệ web.

http://www.ietf.org/rfc/rfc2396.txt

RFC 2396, "Uniform Resource Identifiers (URI): Generic Syntax," là tài liệu tham khảo chi tiết cho các URI và URL.

http://www.ietf.org/rfc/rfc2141.txt

RFC 2141, "URN Syntax,"  là một đặc điểm kỹ thuật năm 1997 mô tả cú pháp URN.

http://www.ietf.org/rfc/rfc2046.txt

RFC 2046, "MIME Phần 2: Media Týpes," là lần thứ hai trong một bộ năm số kỹ thuật Internet xác định các tiêu chuẩn Multipurpose Internet Mail Extensions cho quản lý nội dung đa phương tiện.

http://www.wrec.org/Drafts/draft-ietf-wrec-taxonomy-06.txt

Dự thảo Internet này, "Internet Web Replication và Caching Toxonmy," xác định thuật ngữ chuẩn cho các thành phần kiến trúc web.

