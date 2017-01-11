#DNS Protocol


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật: **11/1/2017**

### Mục lục
[1.Kiến trúc DNS](#1)

- [1.1 DNS Domain Names](#11)

- [1.2 DNS and Internet Domains](#12)

- [1.3 Resource Records](#13)

- [1.4 Phân phối các cơ sở dữ liệu DNS:  tập tin zone và ủy quyền](#14)

- [1.5 Truy vấn cơ sở dữ liệu](#15)

- [1.6 DNS Architecture Diagrams](#16)

[2.Giao thức DNS](#2)

- [2.1 DNS Query Message Format(Định dạng thông điệp DNS Query)](#21)

- [2.2 DNS Query Message Header (Tiêu đề thông điệp DNS Query)](#22)

- [2.3 DNS Query Question Entries (Mục câu hỏi DNS Query)](#23)

- [2.4 DNS Resource Records](#24)

- [2.5 Name Query Message (Thông điệp tên truy vấn)](#25)

- [2.6 Reverse Name Query Message (Thông điệp tên truy vấn đảo ngược)](#26)

- [2.7 DNS Update Message Flags (Thông điệp các cờ DNS update)](#27)

[3. Cấu trúc vật lý DNS](#3)

- [3.1 Dịch vụ DNS Client](#31)

- [3.2 Dịch vụ DNS Server](#32)


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


<p align="center">Hệ thông Domain Name</p>

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




<p align="center">Hình dưới đây cho thấy một ví dụ về cả hai loại truy vấn</p>

<p align="center"></p>

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

<p align="center">DNS Client Service Architecture</p>

<p align="center"><img src="https://i-technet.sec.s-msft.com/dynimg/IC195467.gif" /></p>

Sơ đồ dưới đây minh họa kiến trúc dịch vụ DNS Server với công cụ quản trị của nó và giao diện Windows Management Instrumentation (WMI).

<p align="center">DNS Server Service Architecture</p>

<p align="center"><img src="https://i-technet.sec.s-msft.com/dynimg/IC195468.gif" /></p>


<a name="2"></a>
#2.Giao thức DNS

Giao thức DNS bao gồm loại DNS khác nhau của thông điệp DNS được xử lý theo các thông tin trong các lĩnh vực thông báo.

Các loại thông điệp:

Có ba loại thông điệp DNS:

- Queries

- Responses

- Updates

Queries and responses được định nghĩa trong tiêu chuẩn DNS gốc, và updates được định nghĩa trong RFC 2136. Tất cả ba loại theo một định dạng thông điệp chung.


<a name="21"></a>
###2.1 DNS Query Message Format(Định dạng thông điệp DNS Query)

Định dạng thông điệp DNS phổ biến có chiều dài cố định, header 12 byte và một vị trí biến dành riêng cho các câu hỏi, câu trả lời, quyền hạn, và thêm bản ghi tài nguyên DNS. Định dạng thông điệp thường có thể được minh họa như sau:

Chuẩn định dạng thông điệp DNS Query

|Định dạng thông điệp DNS|
|------------------------------------|
|DNS Header (chiều dai cố định)|
|Question Entries (mục câu hỏi, độ dài thay đổi)|
|Answer Resource records (đội dài thay đổi)|
|Authority Resource records (Bản ghi tài nguyên có thẩm quyền, độ dài thay đổi)|
|Additional Resource Records (Bản ghi tài nguyên bổ sung, độ dài thay đổi)|


<a name="22"></a>
###2.2 DNS Query Message Header (Tiêu đề thông điệp DNS Query)

Các tiêu đề thông điệp DNS chứa các trường sau đây, theo thứ tự sau đây:

**Trường tiêu đề thông điệp DNS Query**

|Tên trường|Mô tả|
|--------------|--------|
|**Transaction ID(ID giao dịch)**|Một trường 16-bit, xác định một giao dịch DNS cụ thể. ID giao dịch được tạo ra bởi những người khởi đầu của thông điệp và được sao chép bởi người trả lời vào thông điệp phản ứng của nó. Sử dụng các ID giao dịch, DNS client có thể phù hợp với phản hồi yêu cầu của mình.|
|**Flags**|Một trường 16-bit có chứa các cờ dịch vụ khác nhau được trao đổi giữa các máy DNS client và DNS server, bao gồm:|
|Request/response(Yêu cầu/Phản ứng)|Trường 1-bit thiết lập là 0 để đại diện cho một yêu cầu tên dịch vụ hoặc thiết lập để 1 để đại diện cho một phản ứng tên dịch vụ.|
|Operation code(mã hoạt động)|Trường 4-bit đại diện cho các tên dịch vụ hoạt động của gói: 0x0 là một truy vấn.|
|Authoritative answer(thẩm quyền trả lời)|Trường 1-bit đại diện cho rằng người trả lời là có thẩm quyền đối với tên miền trong thông điệp truy vấn.|
|Truncation(rút gọn)|Trường 1-bit được thiết lập 1, nếu tổng số câu trả lời vượt gói dữ liệu User Datagram Protocol (UDP). Trừ khi các gói dữ liệu UDP lớn hơn 512 byte hoặc EDNS0 được kích hoạt, chỉ có 512 byte đầu tiên của UDP phản hồi được trả về.
|
|Recursion desired(mong muốn)|Trường 1-bit thiết lập 1 để chỉ ra một truy vấn đệ quy(recursion) và 0 cho các truy vấn lặp đi lặp lại(Iterative). Nếu một DNS server nhận được một thông điệp truy vấn với trường thiết lập này để 0 nó trả về một danh sách các DNS server khác mà khách hàng có thể lựa chọn để liên lạc. Danh mục này được nhập từ dữ liệu bộ nhớ cache của địa phương.|
|Recursion available(đệ quy có sẵn)|Trường 1 bit được thiết lập bởi một DNS serverthành 1 để đại diện cho các DNS server có thể xử lý truy vấn đệ quy(recursion). Nếu đệ quy vô hiệu, các máy chủ DNS thiết lập trường một cách thích hợp.|
|Reserved(dự trữ)|Trường 3-bit được dự trữ và thiết lập là 0.|
|Return code(trả mã)|Trường 4 bit giữ mã trả lại:
||- 0 là một phản ứng thành công (trả lời truy vấn là trong truy vấn phản hồi).|
||- 0x3 là một lỗi tên, chỉ ra rằng một DNS server có thẩm quyền trả lời rằng tên miền trong thông điệp truy vấn không tồn tại|
|**Question Resource Record count**|Trường 16-bit đại diện cho số lượng các mục trong phần câu hỏi của thông điệp DNS.|
|**Answer Resource Record count**|Trường 16-bit đại diện cho số lượng các mục trong phần câu hỏi của thông điệp DNS.|
|**Authority Resource Record count**| Trường 16 bit đại diện cho số lượng thẩm quyền bản ghi tài nguyên(resource records) trong thông điệp DNS|
|**Additional Resource Record count**|Trường 16 bit đại diện cho số lượng bản ghi tài nguyên(resource records) thêm vào trong thông điệp DNS|



<a name="23"></a>
###2.3 DNS Query Question Entries (Mục câu hỏi DNS Query)

Thông điệp DNS Question Entries phần chứa các tên miền mà bị truy vấn và có ba lĩnh vực sau đây:

**DNS Query Question Entry Fields**

|Tên trường|Mô tả|
|--------------|--------|
|**Question Name**|Tên miền đang được truy vấn. tên miền DNS được thể hiện như một loạt các nhãn, như microsoft.com, nhưng trong trường Question Name tên miền được mã hóa như là một loạt các cặp chiều dài có giá trị bao gồm một tập tin 1-byte cho biết chiều dài của giá trị , tiếp theo là các giá trị (nhãn). Ví dụ, microsoft.com miền được thể hiện như 0x09microsoft0x03com0x00, nơi mà các chữ số thập lục phân đại diện cho chiều dài của mỗi nhãn, các ký tự ASCII cho các nhãn cá nhân, và cuối cùng 0 cho biết kết thúc của tên.|
|**Question Type**|Sử dụng một số nguyên 16-bit để đại diện cho các loại bản ghi tài nguyên(resource record) cần được trả lại, như thể hiện dưới đây:|
|Type value(kiểu gía trị)|Record(s) Returned|
|0x01|Ghi Host (A)|
|0x02|Ghi Name server (NS)(tên server)|
|0x05|Ghi Alias (CNAME)(tên phụ)|
|0x0C (12)|Ghi Reverse-lookup (PTR)(dịch ngược) |
|0x0F (15)|Ghi Mail exchange (MX)(trao đổi mail)|
|0x21 (33)|Ghi Service (SRV)(dịch vụ)|
|0xFB (251)|Ghi Incremental zone transfer (IXFR)|
|0xFC (252)|Ghi Standard zone transfer (AXFR)|
|0xFF (255)|All records (ghi tất cả)|
|**Question Class**|Đại diện cho IN (Internet) question class và thường được thiết lập để 0x0001.|


<a name="24"></a>
###2.4 DNS Resource Records

Câu trả lời, quyền hạn, và bổ sung thông tin các phần của một thông điệp phản ứng DNS có thể chứa các bản ghi tài nguyên điều này trả lời các câu hỏi thông điệp truy vấn. Bản ghi tài nguyên(Resource records) được định dạng như sau:

**DNS Resource Record Message Fields **

|Tên trường|Mô tả|
|--------------|--------|
|**Resource record name**|Tên miền DNS ghi như một trường có độ dài thây đổi theo cùng định dạng như trường Question Name. |
|**Resource record type**|Các kiểu gía trị bản ghi tài nguyên.|
|**Resource record class**|Mã lớp bản ghi tài nguyên, Internet 0x0001|
|**Time-to-live**|TTL bằng giây như một trường không dấu 32-bit.|
|**Resource data length**|Trường 2-byte chỉ ra chiều dài của dữ liệu tài nguyên.|
|**Resource data**|Dữ liệu có độ dài thay tương ứng với loại bản ghi tài nguyên.|

Trường Resource Record Name được mã hóa trong cùng một cách như các trường Question Name trừ khi tên đã có mặt ở những nơi khác trong thông điệp DNS, trong đó có trường hợp một trường 2-byte được sử dụng ở vị trí của một  tên length-value mã hóa và đóng vai trò như một con trỏ đến tên mà đã hiện diện.


<a name="25"></a>
###2.5 Name Query Message (Thông điệp tên truy vấn)

Name Query Message giống như các định dạng thông điệp DNS mô tả ở trên. Trong một thông điệp Tên truy vấn điển hình, các lĩnh vực tin DNS sẽ được thiết lập như sau:

**DNS Name Query Message Fields **

|Tên trường|Mô tả|
|----------|-----|
|**Query identifier (Transaction ID)**|Đặt một số duy nhất để cho phép các DNS client phù hợp với việc ứng phó với các truy vấn.|
|**Flags**|Thiết lập để chỉ ra một truy vấn chuẩn cho phép đệ quy.|
|**Question count**|Thiết lập 1|
|**Question entry**|Đặt tên miền truy vấn và các loại bản ghi tài nguyên trở về.|


<a name="26"></a>
###2.6 Reverse Name Query Message (Thông điệp tên truy vấn đảo ngược)

Thông điệp tên truy vấn đảo ngược sử dụng các định dạng thông điệp chung với những khác biệt sau:

- Các DNS client xây dựng tên miền trong miền in-addr.arpa dựa trên địa chỉ IP mà được truy vấn.

- Một bản ghi tài nguyên Pointer (PTR) được truy vấn hơn là một bản ghi tài nguyên máy chủ (A).



<a name="27"></a>
###2.7 DNS Update Message Flags (Thông điệp các cờ DNS update)

Thông điệp các cờ DNS update sừ dụng các cờ sau:

- **Request/response**: trường 1-bit thiết lập là 0 để đại diện cho một yêu cầu update và 1 đại diện cho một phản ứng update.

- **Operation code**:  trường 4 bit thiết lập là 0 cho DNS update

- **7-bit reserved field set to 0**: trường đảo 7 bit thiết lập là 0

- **Return code**: trường 4-bit  có chứa mã đại diện cho các kết quả của các truy vấn update. Các mã như sau:

**DNS Update Message Flag Field Return Code Values**

|Result Code Value (gía trị mã kết qủa)|Mô tả|
|--------------|--------|
|0 (NOERROR)|Không có lỗi; cập nhật thành công.|
|1 (FORMERR)|Lỗi định dạng; Máy chủ DNS không hiểu yêu cầu cập nhật.|
|0x2 (SERVFAIL)|DNS server gặp phải lỗi nội bộ, chẳng hạn như một thời gian chờ chuyển tiếp|
|0x3 (NXDOMAIN|Một tên mà nên tồn tại không tồn tại.|
|0x4 (NOTIMP)|DNS server không hỗ trợ mã hoạt động quy định.|
|0x5 (REFUSED)|DNS server từ chối thực hiện cập nhật vì|
|0x6 (YXDOMAIN)|Một tên đó không nên tồn tại không tồn tại.|
|0x7 (YXRRSET)|Một bản ghi tài nguyên mà không nên tồn tại không tồn tại.|
|0x8 (NXRRSET)|Một bộ hồ bẻn ghi tài nguyên mà nên tồn tại không tồn tại.|
|0x9 (NOTAUTH)|DNS server là không có thẩm quyền đối với zone named trong phần Zone.|
|0xA (NOTZONE)|Một tên được sử dụng trong các phần Prerequisite hoặc Update không nằm trong zone quy định bởi phần Zone.|

<a name="3"></a>
#3.Cấu trúc vật lý DNS

<a name="31"></a>
###3.1 Dịch vụ DNS Client

**Domain Names**

Tên miền được sử dụng với tên máy tính của khách hàng để tạo thành tên đầy đủ tên miền (FQDN), còn được gọi là tên máy tính đầy đủ. Nói chung, các tên miền DNS là phần còn lại của các FQDN mà không được sử dụng như tên máy chủ duy nhất cho máy tính.

Ví dụ, nếu các FQDN hoặc tên máy tính đầy đủ, là wkstn1.example.microsoft.com; tên miền là phần example.microsoft.com của tên này. 

Tên miền DNS có hai biến thể - một tên DNS và một tên NetBIOS. Tên máy tính đầy đủ (một tên DNS đầy đủ điều kiện) được sử dụng trong truy vấn và vị trí của các nguồn tài nguyên được đặt tên trên mạng của bạn. Đối với phiên bản khách hàng trước đó, tên NetBIOS được sử dụng để xác định vị trí các loại hình dịch vụ NetBIOS được chia sẻ trên mạng của bạn.

Khi một máy tính khách hàng được bắt đầu trên mạng, nó sử dụng phân giải DNS để truy vấn một máy chủ DNS cho các bản ghi SRV cho tên miền cấu hình của nó. Truy vấn này được sử dụng để xác định vị trí các bộ điều khiển tên miền và cung cấp chứng thực đăng nhập để truy cập vào tài nguyên mạng. Một khách hàng hoặc một bộ điều khiển tên miền trên mạng tùy chọn sử dụng các dịch vụ giải quyết NetBIOS để truy vấn các máy chủ WINS, cố gắng xác định vị trí DomainName [1C] bài viết để hoàn tất quá trình đăng nhập.

DNS tên miền của bạn nên thực hiện theo các tiêu chuẩn giống nhau và khuyến nghị thực hành áp dụng cho đặt tên máy tính của DNS. Nhìn chung, quy ước đặt tên chấp nhận được cho các tên miền bao gồm việc sử dụng các chữ cái từ A đến Z, chữ số từ 0 đến 9, và các dấu gạch ngang (-). Việc sử dụng dấu chấm (.) Trong một tên miền luôn được sử dụng để tách các phần rời rạc của một tên miền, thường được gọi là nhãn. Mỗi nhãn tương ứng với một mức bổ sung quy định tại các cây không gian tên DNS.

**Host Names**

Máy tính sử dụng giao thức TCP / IP cơ bản của một mạng dựa trên Windows sử dụng một địa chỉ IP, một giá trị 32-bit số (trong trường hợp của IPv4) hoặc một giá trị số 128-bit (trong trường hợp của IPv6), để xác định kết nối mạng máy tính của máy chủ mạng. Tuy nhiên, người sử dụng mạng thích sử dụng dễ nhớ, tên chữ và số. Để hỗ trợ cho nhu cầu này, các nguồn tài nguyên mạng trong một mạng dựa trên Windows được xác định bởi cả hai tên chữ số và địa chỉ IP. DNS và WINS hai cơ chế phân giải tên cho phép sử dụng tên chữ và số, và chuyển đổi các tên này thành địa chỉ IP tương ứng của họ. Ví dụ, trong wkstn1.example.microsoft.com FQDN., Tên máy tính DNS là wkstn1 nhãn.

**NetBIOS vs. DNS Computer Names**

Trong các mạng chạy Windows NT 4.0 và trước đó, người dùng thường xác định vị trí và truy cập vào một máy tính trên mạng bằng cách sử dụng tên NetBIOS (Network Basic Input Output System). Trong các phiên bản sau này của hệ điều hành Windows, bao gồm Windows Server 2008, người dùng xác định vị trí và truy cập vào một máy tính sử dụng DNS. Thực hiện điều này trong DNS, một máy tính được xác định bởi tên máy tính đầy đủ của nó, mà là một FQDN DNS.

**Primary DNS Suffixes**

Tên máy tính đầy đủ là một nối của tên máy chủ duy nhất nhãn, như hostcomputer, và một tên DNS hậu tố chính multilabel, như corp.example.com, đó là tên DNS của miền Active Directory mà máy tính là tham gia. Sử dụng các máy chủ và DNS hậu tố chính.

Ngoài ra, hậu tố DNS kết nối cụ thể có thể được áp dụng cho các kết nối adapter mạng riêng biệt được sử dụng bởi một máy tính multihomed. hậu tố DNS kết nối cụ thể xác định vật chủ khi nó được kết nối với các mạng riêng biệt mà sử dụng các tên miền khác nhau. Khi sử dụng hậu tố DNS kết nối cụ thể, tên máy tính đầy đủ cũng là một nối của tên máy chủ và kết nối cụ thể DNS hậu tố.

Sử dụng tên máy chủ DNS của các hậu tố, một máy tính duy nhất có thể có tên máy tính đầy đủ của nó được cấu hình sử dụng có thể hai phương pháp:

- Một tên máy tính đầy đủ chính, áp dụng như mặc định tên máy tính đầy đủ cho máy tính và tất cả các kết nối mạng được cấu hình của nó.

- Một tên đầy đủ máy tính kết nối cụ thể, có thể được cấu hình như một tên miền DNS thay thế mà chỉ áp dụng cho một adapter mạng đã được cài đặt và cấu hình trên máy tính.

Khi sử dụng Active Directory, theo mặc định, phần DNS hậu tố chính của tên máy tính đầy đủ của máy tính phải được giống như tên của miền Active Directory, nơi các máy tính nằm. Để cho phép các hậu tố DNS chính khác nhau, một người quản trị miền có thể tạo ra một danh sách hạn chế các hậu tố cho phép bằng cách tạo ra các thuộc tính msDS-AllowedDNSSuffixes trong container đối tượng miền. Thuộc tính này được tạo ra và quản trị viên miền sử dụng Active Directory dịch vụ giao diện (ADSI) hoặc Lightweight Directory Access Protocol (LDAP) quản lý.

**Connection-specific Names**

Như trong hình sau, một máy tính máy chủ multihomed tên là "host-a" có thể được đặt tên theo cả hai tên miền DNS chính và kết nối cụ thể của nó.

<p align="center"><img src="https://s-media-cache-ak0.pinimg.com/736x/8a/86/cc/8a86cc87dbaab31abf53f50fcb869b24.jpg" /></p>

Trong ví dụ này, máy tính máy chủ lưu trữ, một gắn vào hai mạng riêng biệt - Subnet 1 và Subnet 2 - cũng được liên kết tại các điểm dự phòng sử dụng hai router cho đường dẫn bổ sung giữa mỗi subnet. Với cấu hình này, máy chủ một cung cấp quyền truy cập như sau thông qua mạng lưới khu vực địa phương có tên riêng của nó (LAN) kết nối:

- Cái tên "host-a.public.example.microsoft.com" cung cấp quyền truy cập sử dụng kết nối mạng LAN 1 trên Subnet 1, một tốc độ thấp hơn (10 megabit) Ethernet LAN, truy cập bình thường để người dùng có nhu cầu dịch vụ in và tập tin thông thường.

Ngoài các tên DNS kết nối cụ thể, các máy tính cũng có thể được truy cập bằng cách sử dụng một trong hai kết nối mạng LAN bằng cách xác định tên miền DNS chính của nó, "host-a.example.microsoft.com".

Khi được cấu hình, một máy tính có thể đăng ký bản ghi tài nguyên trong DNS theo ba cái tên riêng biệt và bộ địa chỉ IP của nó, như thể hiện trong bảng sau:

|Tên miên|Địa chỉ IP|Mô tả|
|--------|----------|-----|
|host-a.example.microsoft.com|10.1.1.11, 10.2.2.22|Tên DNS chính cho máy tính. Các máy tính đăng ký bản ghi tài nguyên A và PTR cho tất cả các địa chỉ IP được cấu hình dưới tên này trong zone "example.microsoft.com".|
|host-a.public.example.microsoft.com|10.1.1.11|Kết nối cụ thể tên DNS cho kết nối mạng LAN 1, cái mà đăng ký tài nguyên bản ghi A và PTR cho địa chỉ IP 10.1.1.11 trong zone "public.example.microsoft.com".|
|host-a.backup.example.microsoft.com|10.2.2.22|Kết nối cụ thể tên DNS cho kết nối mạng LAN 2, cái mà đăng ký tài nguyên bản ghi A và PTR cho địa chỉ IP 10.2.2.22 trong zone "backup.example.microsoft.com".|

Khi một máy tính thay đổi giữa các kết nối tới các mạng máy chủ khác khác miền DNS, tên máy chủ không cần phải được thay đổi trừ khi có một máy chủ trong miền DNS mới với tên cùng một máy chủ. Các hậu tố DNS chính cho máy tính có thể được thay đổi từ tên miền cũ sang tên miền mới và máy tính sẽ đăng ký tên máy tính đầy đủ mới trong DNS.


**NetBIOS Names**

Tên NetBIOS được tạo ra bằng cách sử dụng 16 byte đầu tiên của tên máy chủ, mà là số ký tự tối đa cho các tên NetBIOS. Tên NetBIOS là một chuỗi 16-byte xác định duy nhất một máy tính hoặc dịch vụ cho giao tiếp mạng. Nếu tên máy chủ DNS là 15 byte hoặc ít hơn, thì tên NetBIOS là tên máy cộng với không gian đủ để tạo thành một tên 15-byte, theo sau là một định danh duy nhất 1 byte. 16 byte xác định dịch vụ mạng liên kết với máy tính. Khi tên máy tính vượt quá độ dài tối đa cho NetBIOS, tên máy tính NetBIOS được tạo ra bằng cách cắt bỏ các tên máy chủ để tạo thành một tên 15-byte, theo sau là một định danh duy nhất 1 byte.

Nếu bạn đang sử dụng tên NetBIOS để hỗ trợ từ công nghệ mạng Microsoft, nó được khuyến khích để bạn sửa đổi tên NetBIOS máy tính sử dụng trên mạng của bạn để chuẩn bị cho việc di chuyển đến một môi trường DNS tiêu chuẩn. Điều này chuẩn bị mạng lưới của bạn tốt cho sự phát triển lâu dài và khả năng tương thích với các yêu cầu đặt tên tương lai.

Bảng dưới đây tóm tắt sự khác giữa DNS và tên NetBIOS sử dụng ví dụ FQDN client1.example.com.

<p align="center">DNS and NetBIOS Names</p>

|Tên loại|Mô tả|
|-----------|--------|
|NetBIOS name|Tên NetBIOS được sử dụng để nhận diện các dịch vụ NetBIOS của máy tính. Tên NetBIOS độc đáo này được giải quyết đến địa chỉ IP của máy tính thông qua phát sóng, WINS, hoặc các tập tin LMHosts. Theo mặc định, tên NetBIOS của máy tính cũng giống như tên máy chủ lên đến 15 byte, cộng với bất kỳ không gian cần thiết để làm cho tên dài 15 byte, cộng với nhận dạng dịch vụ. Ví dụ, một tên NetBIOS có thể là trạm Client1. |
|Host Name|Tên máy chủ là nhãn đầu tiên của một FQDN. Ví dụ, nhãn đầu tiên của client1.example.com FQDN là client1. |
|Primary DNS suffix|Mỗi máy tính chạy hệ điều hành Windows có thể được chỉ định một DNS hậu tố chính được sử dụng trong phân giải tên và đăng ký tên. Bạn có thể xem các DNS hậu tố chính cho máy tính của bạn từ các tab Computer Name của System Properties. Các hậu tố DNS chính còn được gọi là tên miền chính. Ví dụ, các client1.example.com FQDN có chính example.com DNS suffix. |
|Connection-specific DNS suffix|FQDN là một tên DNS mà xác nhận máy tính trong không gian tên DNS. Theo mặc định, nó là một móc nối của tên máy chủ, các DNS hậu chính, và một khoảng thời gian. Ví dụ, một FQDN có thể client1.example.com.|
|Full computer name|Tên máy tính đầy đủ là FQDN. Đó là phép nối của tên máy chủ và DNS hậu tố chính (hoặc tên máy chủ và kết nối cụ thể  DNS hậu tố).|

**Hạn chế về tên cho máy chủ và các miền**

Triển khai DNS khác nhau cho phép các kí tự và độ dài khác nhau, và khác với tên NetBIOS hạn chế. Bảng sau đây cho thấy những hạn chế đối với tên chuẩn DNS, tên DNS trong Windows Server 2008, và tên NetBIOS.

|Sự hạn chế|Chuẩn DNS (Bao gồm Windows NT 4.0)|DNS trong Windows Server 2008|NetBIOS|
|---------------|----------------------------------------------------|--------------------------------------------|------------|
||Hỗ trợ RFC 1123, trong đó cho phép "A" đến "Z", "a" đến "z", "0" đến "9", và các dấu gạch ngang (-)|Một số cấu hình khác nhau là có thể|Cho phép các ký tự Unicode, số, khoảng trắng, ký hiệu: @ $% ^ &) (-. _ {} ~|
|Đầy đủ chiều dài tên miền|Cho phép 63 byte cho mỗi nhãn và 255 byte cho một FQDN|Cho phép 63 byte cho mỗi nhãn và 255 byte cho một FQDN; FQDN cho một tên miền Active Directory được giới hạn đến 64 byte.|Cho phép 16 byte cho một tên máy chủ|

**Subnet ưu tiên**

DNS subnet ưu tiên trả về địa chỉ IP cục bộ của dịch vụ DNS Client trong ưu tiên cho các địa chỉ IP trên mạng con khác nhau. Tính năng này làm giảm lưu lượng mạng bằng cách khuyến khích máy khách  kết nối với các tài nguyên mạng gần với họ hơn.

Ví dụ, giả sử trong ba máy chủ web host www.example.com đang nằm trên các mạng con khác nhau. Trên máy chủ DNS, bạn có thể tạo các bản ghi tài nguyên sau:

```
www.example.com.  IN A  172.16.64.11
www.example.com.  IN A  172.17.64.22
www.example.com.  IN A  172.18.64.33

```

Khi người dùng truy vấn cho www.example.com, cả ba bản ghi tài nguyên được trả về. Với subnet ưu tiên, các dịch vụ DNS Client sắp xếp lại danh sách các hồ sơ trả lại để nó bắt đầu với các địa chỉ IP từ mạng mà máy tính được kết nối trực tiếp. Ví dụ, nếu một người sử dụng với địa chỉ IP 172.17.64.93 truy vấn cho www.example.com, các dịch vụ DNS Client trả về bản ghi tài nguyên theo thứ tự sau:

```
 www.example.com.  IN A 172.17.64.22
 www.example.com.  IN A 172.16.64.11
 www.example.com.  IN A 172.18.64.33
 
```

<a name="32"></a>
###3.2 Dịch vụ DNS Server

**Vô hiệu hóa đệ quy**

Theo mặc định, đệ quy được kích hoạt cho các dịch vụ DNS Server, và khách hàng thường yêu cầu rằng các máy chủ sử dụng đệ quy để giải quyết một tên khi gửi một truy vấn. Nếu đệ quy là vô hiệu, dịch vụ DNS Server luôn luôn sử dụng các giới thiệu, không phụ thuộc vào yêu cầu của khách hàng.

Nói chung, các máy chủ DNS có thể trả lời các truy vấn cho tên bên ngoài các khu có thẩm quyền của họ theo hai cách:

- Máy chủ có thể gửi câu trả lời giới thiệu, đó là một phản ứng ngay lập tức cho khách hàng yêu cầu với một danh sách các bản ghi tài nguyên cho các máy chủ DNS khác điều này nó biết về sự xuất hiện để được gần hơn hoặc nhiều khả năng để được giúp đỡ trong việc giải quyết các tên được truy vấn.

- Máy chủ có thể sử dụng đệ quy để truy vấn các máy chủ khác thay mặt cho các khách hàng yêu cầu, cố gắng để giải quyết đầy đủ tên. tra cứu đệ quy tiếp tục cho đến khi máy chủ nhận được một câu trả lời chính thức cho tên truy vấn. Các máy chủ sau đó chuyển tiếp câu trả lời này để đáp ứng với truy vấn ban đầu từ các khách hàng yêu cầu.

**Round Robin**

Round robin DNS là một phương thức quản lý tắc nghẽn máy chủ bằng cách phân phối tải trọng kết nối trên nhiều máy chủ (có chứa nội dung giống hệt nhau). Round robin hoạt động trên cơ sở luân phiên trong đó một máy chủ địa chỉ IP được phát ra, sau đó di chuyển đến phía sau của danh sách; địa chỉ IP của máy chủ tiếp theo được đưa ra, sau đó nó di chuyển đến cuối danh sách; và như vậy, tùy thuộc vào số lượng các máy chủ đang được sử dụng. Điều này hoạt động trong một kiểu lặp lại.

Cơ chế cân bằng của địa phương này được sử dụng bởi các máy chủ DNS để chia sẻ và phân phối tải tài nguyên mạng. Bạn có thể sử dụng luân chuyển vòng xoay tất cả các loại hồ sơ tài nguyên chứa trong một câu trả lời truy vấn nếu nhiều RR được tìm thấy.

Nếu round robin bị vô hiệu hóa cho một máy chủ DNS, thứ tự của các phản ứng đối với các truy vấn này được dựa trên một trật tự tĩnh của RR trong danh sách câu trả lời khi chúng được lưu trữ trong zone (hoặc khu tập tin hoặc AD DS).

**Hạn chế luân phiên round robin với các loại RR**

Theo mặc định, DNS sẽ thực hiện luân chuyển round robin cho tất cả các loại RR. Bây giờ bạn có thể chỉ định rằng các loại RR nhất định không phải là round robin trong đăng kí. Những thay đổi này có thể được thực hiện trong đăng ký.

**Hạn chế luân phiên round robin với tất cả các loại RR**

Theo mặc định, tất cả các loại RR được luân chuyển, ngoại trừ những người đã được xác định là bị loại từ round robin trong đăng ký

**Subnet ưu tiên**



