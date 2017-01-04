## DNS Protocol


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật: **4/1/2017**

### Mục lục
[1.Kiến trúc DNS](#1)

- [1.1 DNS Domain Names](#11)

- [1.2 DNS and Internet Domains](#12)

- [1.3 Resource Records](#13)

- [1.4 Phân phối các cơ sở dữ liệu DNS:  tập tin zone và ủy quyền](#14)

- [1.5 Truy vấn cơ sở dữ liệu](#15)

- [1.6 DNS Architecture Diagrams](#16)

---


<a name="1"></a>
#1.Kiến trúc DNS

Kiến trúc DNS là một cơ sở dữ liệu phân tán theo cấp bậc và thiết lập một liên kết của các giao thức xác định:

- Một cơ chế để truy vấn và cập nhật cơ sở dữ liệu.

- Một cơ chế sao chép các thông tin trong cơ sở dữ liệu giữa các máy chủ.

- Một lược đồ cơ sở dữ liệu

DNS có nguồn gốc từ những ngày đầu của Internet khi Internet là một mạng lưới nhỏ được thành lập bởi Bộ Quốc phòng Hoa Kỳ cho mục đích nghiên cứu. Tên máy chủ của các máy tính trong mạng này được quản lý thông qua việc sử dụng một tập tin HOSTS đơn nằm trên một máy chủ quản lý tập trung. Mỗi trang web cần để chuyển các tên máy chủ trên mạng tải về tập tin này. Khi số lượng máy trên mạng Internet lớn, lưu lượng được tạo ra bởi quá trình cập nhật tăng lên, cũng như kích thước của file HOSTS. Cần một hệ thống mới, thứ mà sẽ cung cấp các tính năng như khả năng mở rộng, phân cấp quản lý, hỗ trợ cho các kiểu dữ liệu khác nhau, ngày càng trở nên rõ ràng hơn mà.

Hệ thống tên miền được giới thiệu vào năm 1984 đã trở thành hệ thống mới này. 

Với DNS, tên máy chủ nằm trong một cơ sở dữ liệu có thể được phân phối giữa nhiều máy chủ, giảm tải trên bất cứ một máy chủ và cung cấp khả năng quản lý hệ thống đặt tên này trên một cơ sở cho mỗi phân vùng. DNS hỗ trợ tên thứ bậc và cho phép đăng ký các kiểu dữ liệu khác nhau ngoài ra lưu trữ tên để ánh xạ địa chỉ IP được sử dụng trong file HOSTS. Bởi vì cơ sở dữ liệu DNS được phân phối, quy mô tiềm năng của nó là không giới hạn và hiệu suất là không bị suy giảm khi nhiều máy chủ được thêm vào.


<a name="11"></a>
###1.1 DNS Domain Names

Các hệ thống tên miền được thực hiện như một cơ sở dữ liệu phân cấp và phân phối có chứa các loại dữ liệu khác nhau, bao gồm cả tên host và tên miền. Các tên trong một cơ sở dữ liệu DNS thành một cấu trúc cây phân cấp được gọi là không gian tên miền. Tên miền bao gồm nhãn cá nhân phân cách bằng dấu (.) , ví dụ: mydomain.microsoft.com.

Fully Qualified Domain Name (FQDN) xác định duy nhất các vị trí host trong cây phân cấp DNS bằng cách xác định một danh sách các tên cách nhau bởi dấu chấm trong các đường đi từ các máy chủ tham chiếu đến thư mục gốc. Các hình tiếp theo cho thấy một ví dụ về một cây DNS với một máy chủ được gọi là mydomain trong miền microsoft.com. FQDN cho máy chủ sẽ là mydomain.microsoft.com.

 **DNS Domain Namespace**

DNS Donain Namespace, như thể hiện trong hình sau đây, dựa trên khái niệm của một cây các tên miền. Mỗi cấp độ của cây có thể đại diện cho cả một nhánh hoặc một chiếc lá của cây. Một nhánh là một mức độ mà nhiều tên được sử dụng để xác định một tập hợp các nguồn tài nguyên được đặt tên. Một lá đại diện cho một cái tên duy nhất sử dụng một lần ở cấp đó để chỉ ra một tài nguyên cụ thể.

**Hệ thống Domain Name**

<p align="center"><img src="https://i-technet.sec.s-msft.com/dynimg/IC195464.gif" /></p>

Hình trên cho thấy cách Microsoft được gán quyền bởi các máy chủ gốc Internet cho phần riêng của mình của cây  DNS Domain Namespace  trên Internet. DNS client và DNS server sử dụng các truy vấn như các phương pháp cơ bản của phaab giải tên trong cây với các loại cụ thể của tài nguyên thông tin. Thông tin này được cung cấp bởi các DNS server trong câu trả lời truy vấn cho các DNS client, sau đó trích xuất các thông tin và vượt qua nó để một chương trình yêu cầu để giải quyết các truy vấn tên. 
Trong quá trình phân giải một tên, hãy nhớ rằng DNS server thường hoạt động như DNS client, truy vấn các máy chủ khác để giải quyết đầy đủ tên truy vấn.

**DNS Domain Namespace tổ chức như thế nào?**

Bất kỳ tên miền DNS được sử dụng trong cây là một kỹ thuật miền. Tuy nhiên, các tên được xác định  một trong năm cách khác nhau, dựa trên mức độ và cách một tên thường được sử dụng. Ví dụ, tên miền DNS đã đăng ký với Microsoft (microsoft.com.) Được biết đến như một tên miền cấp hai. Điều này là bởi vì tên này có hai phần (biết như nhãn) mà chỉ ra nó nằm ở hai cấp độ dưới gốc hoặc trên cùng của cây. Hầu hết các tên miền DNS có hai hoặc nhiều nhãn, mỗi trong số đó cho thấy một mức độ mới trong cây.

Năm loại dùng để mô tả tên miền DNS bằng chức năng của chúng trong không gian tên được mô tả trong bảng dưới đây, cùng với một ví dụ về mỗi loại tên.

**Các kiểu DNS Domain Names**

|Tên|Mô tả|Ví dụ|
|---|-----|-----|
|Root domain (miền gốc)|Đây là phần trên cùng của cây, đại diện cho một mức độ vô danh; đôi khi nó được hiển thị như là hai dấu trống ngoặc kép (""), cho thấy một giá trị null. Khi được sử dụng trong một tên miền DNS, nó được quy định bởi một thời gian theo sau (.) Để chỉ rằng tên nằm ở gốc hoặc mức cao nhất của hệ thống phân cấp tên miền. Trong trường hợp này, các tên miền DNS được coi là đầy đủ và trỏ đến một vị trí chính xác trong cây tên. Tên ghi theo cách này được gọi là tên miền đầy đủ (FQDN).|Một khoảng thời gian duy nhất (.) hoặc một thời gian sử dụng ở phần cuối của một tên, chẳng hạn như "example.microsoft.com."|
|Top level domain (miền cao nhất)|Một tên dùng để chỉ một quốc gia / khu vực hoặc các loại hình tổ chức sử dụng một cái tên.|"" .com ", chỉ ra một tên đăng ký kinh doanh để sử dụng thương mại trên Internet.|
|Second level domain (miền cấp độ 2)|Tên có độ dài thay đổi đăng ký cho một cá nhân hoặc tổ chức để sử dụng trên Internet. Những tên này luôn luôn dựa trên một tên miền cấp cao thích hợp, tùy thuộc vào loại tổ chức, vị trí địa lý, nơi một tên được sử dụng.|"" Microsoft.com. ", Đó là tên miền cấp 2 đăng ký với Microsoft bằng tên miền đăng ký Internet DNS .|
|Subdomain (miền phụ)|Tên phụ tên mà một tổ chức có thể tạo ra được hình thành từ tên miền đăng ký cấp 2. Chúng bao gồm các tên phụ để phát triển cây DNS của tên trong một tổ chức và phân chia nó thành các cơ quan hay vị trí địa lý.|"" Example.microsoft.com. ", là một tên miền phụ gỉa của Microsoft được giao sử dụng tên example.|
|Host or resource name|Tên đại diện cho một lá trong cây DNS của tên và xác định một tài nguyên cụ thể. Thông thường, các nhãn tận cùng bên trái của một tên miền DNS xác định một máy tính cụ thể trên mạng. Ví dụ, nếu một tên ở cấp độ này được sử dụng trong một host (A) RR, nó được sử dụng để tìm địa chỉ IP của máy tính dựa trên tên máy chủ của nó.|"" Host-a.example.microsoft.com. ", Nơi mà các nhãn đầu tiên (" host-a ") là tên máy chủ DNS cho một máy tính cụ thể trên mạng.|


<a name="12"></a>
###1.2 DNS and Internet Domains

Internet Domain Name System được quản lý bởi một Cơ quan đăng ký tên trên Internet, trách nhiệm duy trì tên miền cấp cao được phân công của tổ chức và của quốc gia / khu vực. Những tên miền theo các tiêu chuẩn quốc tế 3166. Một số trong rất nhiều chữ viết tắt hiện có, dành cho sử dụng bởi các tổ chức, cũng như hai chữ và ba chữ viết tắt được sử dụng cho các quốc gia / vùng lãnh thổ được thể hiện trong bảng sau:

**Vài DNS Top-level Domain Names (TLDs)**

|DNS Domain Name|Kiểu cuả tổ chức|
|-------------------------|----------------------|
|com|Tổ chức thường mại|
|edu|Cơ sở giáo dục|
|org|Các tổ chức phi lợi nhuận|
|net|Networks (trụ cột của Internet)|
|gov|Các tổ chức chính phủ phi quân sự|
|mil|Các tổ chức chính phủ quân sự|
|arpa|DNS nghịch|
|"xx"|Hai từ là mã một quốc gia(us,au,fr,ca,...)|



<a name="13"></a>
###1.3 Resource Records 

Một cơ sở dữ liệu DNS bao gồm bản ghi tài nguyên (RR). Mỗi RR xác định tài nguyên cụ thể trong cơ sở dữ liệu. Có nhiều loại khác nhau của RR trong DNS. Phần này cung cấp thông tin về cấu trúc chung của bản ghi tài nguyên. 

Bảng dưới đây cung cấp thông tin chi tiết về cấu trúc chung của RR.

**Một số DNS Resource Record thông thường**

|Mô tả|Lớp|Time To Live (TTL)|Kiểu|Dữ liệu|
|--------|-----|-----------------------|-------|---------|
|Start of Authority|Internet (IN)|Mặc định là 60 phút|SOA|Tên chủ sở hữu|
|||||Primary Name Server DNS Name
|||||Serial Number
|||||Refresh Interval
|||||Thử lại Interval
|||||Thời gian hết hạn
|||||TTL tối thiểu
|Host|Internet (IN)|Ghi cụ thể TTL nếu có, hoặc khu vực khác (SOA) TTL|A|Tên chủ sở hữu (Máy chủ DNS Name)
|||||Chủ Địa chỉ IP
|Name Server|Internet (IN)|Ghi cụ thể TTL nếu có, hoặc khu vực khác (SOA) TTL|NS|Tên chủ sở hữu
|||||Đặt tên Name Server DNS
|Mail Exchanger|Internet (IN)|Ghi cụ thể TTL nếu có, hoặc khu vực khác (SOA) TTL|MX|Tên chủ sở hữu
|||||Mail Exchange DNS Server Name, Số ưu tiên
|Canonical Name (an alias) |Internet (IN)|Ghi cụ thể TTL nếu có, hoặc khu vực khác (SOA) TTL|CNAME|Tên chủ sở hữu (tên bí danh)
|||||Tên Máy chủ DNS


<a name="14"></a>
###1.4 Phân phối các cơ sở dữ liệu DNS:  tập tin zone và ủy quyền

Một cơ sở dữ liệu DNS có thể được phân chia thành nhiều zone. Một zone là một phần của cơ sở dữ liệu DNS có chứa các bản ghi tài nguyên với tên chủ sở hữu thuộc về những phần tiếp giáp của  DNS Domain Namespace. File Zone được duy trì trên các máy chủ DNS. Một DNS server duy nhất có thể được cấu hình để host không, một hoặc nhiều khu vực.

Mỗi zone được đặt ở một tên miền cụ thể được gọi là tên miền gốc của zone. Một zone có chứa thông tin về tất cả các tên kết thúc bằng tên miền gốc của zone. Một DNS server được coi là độc quyền cho một tên nếu nó tải zone chứa tên đó. Các bản ghi đầu tiên trong bất kỳ tập tin zone là một khởi đầu của Authority (SOA) RR. SOA RR xác định DNS server chính cho zone như là nguồn thông tin tốt nhất cho dữ liệu trong zone đó và như một thực thể tạo các bản cập nhật cho zone.

<p align="center"><img src="https://i-technet.sec.s-msft.com/dynimg/IC195465.gif" /></p>


<a name="15"></a>
###1.5 Truy vấn cơ sở dữ liệu

Truy vấn DNS có thể được gửi từ một DNS client (resolver) đến DNS server, hoặc giữa hai DNS server.

Một truy vấn DNS chỉ đơn thuần là một yêu cầu bản ghi tài nguyên DNS của một loại bản ghi tài nguyên xác định với một tên DNS xác định. Ví dụ, một truy vấn DNS có thể yêu cầu tất cả các bản ghi tài nguyên của loại A (host) với một tên DNS xác định.

Có hai loại truy vấn DNS có thể được gửi đến một DNS server:

- Recursive

- Iterative

Một truy vấn recursive buộc một DNS server để đáp ứng một yêu cầu với mỗi một thất bại hay một phản ứng thành công. DNS client resolve (phân giải) thường truy vấn đệ quy. Với một truy vấn recursive các DNS server phải liên hệ với bất kỳ DNS server khác nó cần phải giải quyết các yêu cầu. Khi nhận được một phản ứng thành công từ các  DNS server khác, sau đó nó sẽ gửi một phản hồi cho khách hàng DNS. 

Nếu Recursion bị disable thì nó sẽ sử dụng Iterative (tương tác), tức là nó sẽ gởi yêu cầu phân giải lại tên của host name. Khi có một truy vấn từ Client, trước hết nó sẽ tìm trong cơ sở dữ liệu của chính nó, nếu không có, nó sẽ cho biết một máy chủ khác mà từ đó có thể tìm thấy kết quả truy vấn.

**Hình dưới đây cho thấy một ví dụ về cả hai loại truy vấn.**

<p align="center"><img src="https://i-technet.sec.s-msft.com/dynimg/IC195466.gif" /></p>

Như thể hiện trong hình trên, một số truy vấn được sử dụng để xác định địa chỉ IP cho www.whitehouse.gov. Các chuỗi truy vấn được mô tả dưới đây:

1. Truy vấn Recursive cho www.whitehouse.gov (A resource record)

2. Truy vấn Iterative cho www.whitehouse.gov (A resource record)

3. Giới thiệu .gov đến các name server (NS resource records, for .gov); 

4. Truy vấn Iterative cho www.whitehouse.gov (A resource record)

5. Giới thiệu whitehouse.gov đến name server (NS resource record, for whitehouse.gov)

6. Truy vấn Iterative cho www.whitehouse.gov (A resource record)

7. Trả lời cho truy vấn interative từ máy chủ whitehouse.gov (địa chỉ IP của www.whitehouse.gov)

8. Trả lời cho các truy vấn đệ quy gốc từ DNS server local để phân giải  (địa chỉ IP của www.whitehouse.gov)

**Time to Live for Resource Records**


<a name="16"></a>
###1.6 DNS Architecture Diagrams

Các biểu đồ sau đây minh họa cách các dịch vụ DNS Client và Server làm việc và cung cấp thêm thông tin về độ phân giải tên, cập nhật và hoạt động quản lý.

Sơ đồ đầu tiên minh họa kiến trúc dịch vụ DNS Client ở độ phân giải tên và cập nhật các hoạt động của nó. Trong sơ đồ này, kiến trúc phân giải tên được chứng minh sử dụng một trình duyệt Web và Microsoft Outlook và cập nhật được đại diện bởi các DHCP client.

**DNS Client Service Architecture**

<p align="center"><img src="https://i-technet.sec.s-msft.com/dynimg/IC195467.gif" /></p>

Sơ đồ dưới đây minh họa kiến trúc dịch vụ DNS Server với công cụ quản trị của nó và giao diện Windows Management Instrumentation (WMI).

**DNS Server Service Architecture**

<p align="center"><img src="https://i-technet.sec.s-msft.com/dynimg/IC195468.gif" /></p>


