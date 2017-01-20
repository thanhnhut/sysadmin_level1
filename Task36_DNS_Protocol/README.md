#DNS Protocol


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật: **19/1/2017**

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

- [3.3 Bản ghi tài nguyên trong DNS](#33)

- [3.4 Các file liên quan đến DNS](#34)

- [3.5 Zones and Zone Transfer](#35)

- [3.6 Tích hợp Active Directory](#36)

[4.Các qúa trình và tương tác DNS](#4)

- [4.1 Truy vấn DNS hoạt động thế nào](#41)

- [4.2 Tra cứu ngược](#42)

- [4.3 Forwarding (chuyển tiếp)](#43)

- [4.4 Dynamic Update (cập nhật động)](#44)

[5.Understanding Aging and Scavenging](#5)

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

Theo mặc định, các dịch vụ DNS Server sử dụng ưu tiên subnet cục bộ như là phương pháp ưu tiên cho các địa chỉ IP trên cùng một mạng khi một truy vấn khách hàng giải quyết cho một tên máy chủ được ánh xạ tới nhiều hơn một địa chỉ IP. Tính năng này đòi hỏi các ứng dụng khách hàng cố gắng để kết nối với các máy chủ sử dụng gần nhất (và thường là nhanh nhất) địa chỉ IP của nó có sẵn để kết nối.

Các dịch vụ DNS Server sử dụng ưu tiên subnet địa phương như sau:

1 . Các dịch vụ DNS Server sẽ xác định nếu ưu tiên subnet địa phương là cần thiết để đáp ứng truy vấn.

Nếu có nhiều hơn một bản ghi tài nguyên (RR) phù hợp với tên máy chủ truy vấn, các dịch vụ DNS Server có thể sắp xếp lại các hồ sơ theo vị trí mạng con của họ. Nếu tên máy chủ truy vấn chỉ phù hợp với một bản ghi tài nguyên duy nhất, hoặc nếu địa chỉ IP của khách hàng không phù hợp với một địa chỉ mạng IP cho bất kỳ địa chỉ ánh xạ trong một danh sách câu trả lời của nhiều RR, không có ưu tiên là bắt buộc.

2 . Đối với mỗi RR trong danh sách câu trả lời phù hợp, các dịch vụ DNS Server xác định trong đó ghi lại (nếu có) phù hợp với vị trí subnet của khách hàng yêu cầu.

3 . Các dịch vụ DNS Server sắp xếp lại danh sách câu trả lời để A RR phù hợp với mạng con nội bộ của khách hàng yêu cầu được đặt đầu tiên trong danh sách câu trả lời.

4 .    Ưu tiên theo lệnh subnet, danh sách câu trả lời sẽ được trả về cho khách hàng yêu cầu.

**Tham số dịch vụ DNS Server cấp cao**

Khi khởi tạo dịch vụ, máy chủ DNS sử dụng cài đặt cấu hình máy chủ lấy từ các thông số ghi trong một tập tin thông tin khởi động, đăng ký, và có thể khoanh vùng thông tin được cung cấp thông qua Active Directory.

Trong hầu hết các trường hợp, cài đặt mặc định là chấp nhận được và không nên yêu cầu sửa đổi. Tuy nhiên, khi cần thiết, bạn có thể sử dụng DNS console để điều chỉnh các thông số. 

<p align="center">Dịch vụ DNS Server các thông số cao cấp</p>

|Gía trị|Mô tả|
|-------|--------|
|Disable recursion(Vô hiệu hóa đệ quy)|Xác định xem máy chủ DNS sử dụng đệ quy. Theo mặc định, các dịch vụ DNS Server được kích hoạt để sử dụng đệ quy.|
|BIND secondaries|Xác định xem có sử dụng định dạng nhanh chóng chuyển giao khi chuyển vùng đến các máy chủ DNS chạy triển khai Berkeley Internet Name Domain (BIND) triển khai.|
|Fail on load if bad zone data(Thất bại trên tải nếu dữ liệu zone xấu|Thiết lập máy chủ DNS để phân tích các tập tin đúng. Theo mặc định, các dịch vụ DNS Server ghi dữ liệu lỗi, bỏ qua bất kỳ sai lầm dữ liệu trong các tập tin khu vực, và tiếp tục tải một vùng. Tùy chọn này có thể được cấu hình lại bằng cách sử dụng giao diện DNS để dịch vụ DNS Server ghi lỗi và không tải một khu tập tin chứa dữ liệu hồ sơ mà là quyết tâm có lỗi. |
|Enable round robin|Xác định xem máy chủ DNS sử dụng round robin và sắp xếp lại một danh sách các bản ghi tài nguyên nếu nhiều RR cùng loại tồn tại cho một câu trả lời truy vấn.|
|Enable netmask ordering|Xác định xem máy chủ DNS sắp xếp lại một bản ghi tài nguyên trong các bản ghi tài nguyên cùng một thiết lập trong phản ứng của nó với một truy vấn dựa trên địa chỉ IP của các nguồn của các truy vấn.|
|Secure cache against pollution|Xác định xem máy chủ cố gắng để làm sạch những phản ứng để tránh ô nhiễm bộ nhớ cache. Thiết lập này được kích hoạt theo mặc định.|


<a name="33"></a>
###3.3 Bản ghi tài nguyên trong DNS

Bản ghi tài nguyên DNS là các dữ liệu được liên kết với DNS tên trong không gian tên DNS. Mỗi tên miền của cây không gian tên DNS chứa một tập hợp các bản ghi tài nguyên, và mỗi bản ghi tài nguyên trong các thiết lập bao gồm các loại khác nhau của thông tin liên quan đến tên miền. DNS truy vấn bao gồm các tên miền DNS để được giải quyết và các loại thông tin bạn muốn (các bản ghi tài nguyên được yêu cầu). Truy vấn cho các địa chỉ IP của máy chủ DNS trở về một nguồn tài nguyên bản ghi và truy vấn các máy chủ DNS uỷ quyền cho một tên miền DNS tên trở lại tên máy chủ (NS) bản ghi tài nguyên.

Bản ghi tài nguyên thường được thảo luận trong hai loại: hồ sơ cơ quan (Authority Records) và các hồ sơ khác. Hồ sơ thẩm quyền xác định máy chủ DNS được uỷ quyền cho các tên miền trong không gian tên DNS và cách zone của họ nên được quản lý, và tất cả các bản ghi DNS khác chứa thông tin về một tên miền không liên quan đến thẩm quyền.

**Authority Records (quyền ghi)**

Zone được dựa trên một khái niệm về chủ quyền. Khi một máy chủ DNS được cấu hình để tải một zone, nó sử dụng hai loại bản ghi tài nguyên để xác định các tính chất cod thẩm quyền của zone:

- Đầu tiên khi bắt đầu quyền ghi (SOA) tài nguyên cho biết tên gốc cho zone và chứa tên của máy chủ đó là nguồn chính thông tin về zone. Nó cũng cho thấy các tính chất cơ bản của zone.

- Tiếp theo, các bản ghi tài nguyên tên máy chủ (NS) được sử dụng để ghi nốt mà DNS server được chỉ định như là độc quyền cho khu vực. Bằng cách liệt kê một máy chủ trong RR NS, nó trở nên được biết đến với những người khác như một máy chủ có thẩm quyền đối với khu vực. Điều này có nghĩa rằng bất kỳ máy chủ xác định trong RR NS được coi là một nguồn thẩm quyền của người khác, và có thể trả lời chắc chắn bất kỳ truy vấn được đưa cho các tên có trong khu vực.

Các bản ghi tài nguyên SOA và NS chiếm một vai trò đặc biệt trong cấu hình khu vực. Họ được yêu cầu hồ sơ cho vùng bất kỳ và thường là các bản ghi tài nguyên đầu tiên được liệt kê trong tập tin.

**Bản ghi tài nguyên SOA**

Sự bắt đầu của chính quyền bản ghi tài nguyên (SOA) luôn luôn là đầu tiên trong bất kỳ vùng tiêu chuẩn. Nó chỉ ra các máy chủ DNS mà một trong hai ban đầu tạo ra nó hay bây giờ là máy chủ chính cho zone. Nó cũng được sử dụng để lưu trữ các tài sản khác như thông tin phiên bản và thời gian ảnh hưởng đến đổi mới zone hoặc hết hạn. Các tính chất này ảnh hưởng đến mức độ thường xuyên chuyển của zone được thực hiện giữa các máy chủ có thẩm quyền đối với zone.

Các bản ghi tài nguyên SOA có chứa các thông tin sau:

<p align="center">Trường bản ghi tài nguyên SOA</p>

|Trường|Mô tả|
|---------|--------|
|Primary server (owner) (máy chủ chính)|Tên máy chủ cho các máy chủ DNS chính cho zone.|
|Responsible person (người có trách nhiệm)|Địa chỉ e-mail của người chịu trách nhiệm quản lý zone. Một dấu chấm (.) Được dùng thay cho một ký hiệu (@) trong tên e-mail này.|
|Serial number (số serial)|Các số phiên bản của khu tập tin. Con số này tăng lên mỗi khi một bản ghi tài nguyên trong vùng thay đổi. Điều quan trọng là giá trị này tăng mỗi lần vùng được thay đổi, vì vậy mà một trong hai thay đổi một phần hoặc zone điều chỉnh hoàn toàn có thể được nhân rộng đến các máy chủ thứ cấp khác trong quá trình chuyển tiếp theo.|
|Refresh interval |Hiện, trong vài giây, mà một máy chủ DNS thứ cấp phải đợi trước khi truy vấn nguồn của nó đối với zone để cố gắng đổi mới của khu vực. Khi khoảng Refresh interval hết hạn, các máy chủ DNS thứ cấp yêu cầu một bản sao của bản ghi SOA hiện tại cho các vùng từ nguồn của nó, mà câu trả lời yêu cầu này. Các máy chủ DNS thứ cấp sau đó so sánh số serial của bản ghi SOA hiện tại của máy chủ nguồn (như được chỉ ra trong các phản ứng) với số serial trong hồ sơ SOA riêng của địa phương. Nếu chúng khác nhau, các máy chủ DNS thứ cấp yêu cầu chuyển vùng từ các máy chủ DNS chính. Mặc định cho trường này là 900 giây (15 phút).|
|Retry interval|Thời gian, trong vài giây, máy chủ phụ chờ đợi trước khi thử lại chuyển vùng không thành công. Thông thường, thời gian này là ít hơn so với khoảng thời gian Refresh interval. Giá trị mặc định là 600 giây (10 phút).|
|Expire interval|Thời gian, trong vài giây, trước khi máy chủ phụ dừng đáp ứng cho các truy vấn sau một khoảng thời gian Refresh interval mất hiệu lực nơi khu vực không phải là làm mới hoặc Cập Nhật. Hết hạn xảy ra bởi vì ở tại thời điểm này, các máy chủ trung học phải xem xét dữ liệu địa phương của nó không đáng tin cậy. Giá trị mặc định là 86.400 giây (24 giờ).|
|Minimum (default) TTL|Mặc định thời gian để sống (TTL) của zone và khoảng thời gian tối đa cho bộ nhớ đệm phủ định câu trả lời cho truy vấn tên. Giá trị mặc định là 3.600 giây (1 giờ).|

Sau đây là một ví dụ về một bản ghi tài nguyên SOA mặc định:

```
@   IN  SOA     nameserver.example.microsoft.com.  postmaster.example.microsoft.com. (
                               1            ; serial number
                               3600         ; refresh   [1h]
                               600          ; retry     [10m]
                               86400        ; expire    [1d]
                               3600 )       ; min TTL   [1h]
```

**Bản ghi tài nguyên NS**

Tên máy chủ (NS) bản ghi tài nguyên có thể được sử dụng để gán quyền cho các máy chủ được chỉ định cho một tên miền DNS trong hai cách:

- Bằng cách thiết lập một danh sách các máy chủ có thẩm quyền đối với các tên miền để các máy chủ có thể được thực hiện được biết đến với những người khác mà yêu cầu thông tin về miền này (One).

- Bằng cách cho các máy chủ DNS có thẩm quyền cho bất kỳ tên miền phụ được giao đi từ zone.

Trong trường hợp phân công các máy chủ với tên máy chủ trong cùng một khu vực, địa chỉ tương ứng (A) ghi tài nguyên thường được sử dụng trong các khu vực để giải quyết các tên máy chủ định đến các địa chỉ IP của họ. Đối với các máy chủ được chỉ định sử dụng RR này như là một phần của một zone ủy quyền đến tên miền phụ, các bản ghi tài nguyên NS thường chứa tên ngoài zone. Đối với những tên ngoài khu vực để được giải quyết, một bản ghi tài nguyên cho các máy chủ được chỉ định ngoài zone có thể là cần thiết. Khi NS ngoài zone này và  một hồ sơ cần thiết để cung cấp ủy quyền, chúng được biết như bản ghi đi kèm.

Bảng dưới đây cho thấy các cú pháp cơ bản của cách một RR NS được sử dụng.

|         |
|---------|
|**Mô tả**: Được sử dụng để ánh xạ tên miền DNS như quy định tại chủ sở hữu tên của máy chủ điều hành máy chủ DNS được quy định trong lĩnh vực name_server_domain_name.|
|**Cú pháp**: chủ ttl TRÊN NS name_server_domain_name.|
|**Thí dụ**: example.microsoft.com. IN NS nameserver1.example.microsoft.com |

**Bản ghi quan trọng khacs**

Sau khi một khu vực được tạo ra, bản ghi tài nguyên bổ sung cần phải được thêm vào nó. Bảng sau liệt kê các bản ghi tài nguyên phổ biến nhất (RRs) sẽ được thêm vào.

<p align="center">Bản ghi tài nguyên DNS thông dụng</p>

|Bản ghi tài nguyên|Mô tả|
|-------------------------|--------|
|Host (A)|Để ánh xạ tên miền DNS để địa chỉ IP được sử dụng bởi một máy tính.|
|Alias (CNAME)|Đối với việc lập bản đồ một tên miền bí danh DNS khác tên chính hay tên kinh điển.|
|Mail Exchanger (MX)|Để ánh xạ tên miền DNS cho tên của máy tính đó trao đổi hoặc chuyển tiếp thư.|
|Pointer (PTR)|Để ánh xạ tên miền DNS đảo ngược dựa trên địa chỉ IP của một máy tính mà chỉ vào tên miền DNS phía trước của máy tính đó.|
|Service location (SRV)|Lập bản đồ các tên miền DNS để xác định danh sách các DNS lưu trữ máy tính mà cung cấp một loại hình cụ thể của dịch vụ, chẳng hạn như bộ điều khiển vùng Active Directory.|

**Host (A) resource records**


<a name="34"></a>
###3.4 Các file liên quan đến DNS

Các tập tin sau đây liên quan đến việc sử dụng và cấu hình máy chủ DNS và khách hàng.

|Tập tin|Mô tả|
|----------|--------|
|Boot|BIND tập tin cấu hình khởi động. Tệp này không được tạo ra bởi giao diện điều khiển DNS.  Tuy nhiên, như là một cấu hình tùy chọn cho dịch vụ DNS Server, nó có thể được sao chép từ một máy chủ DNS chạy Internet Berkeley Tên miền (BIND) thực hiện máy chủ DNS. Để sử dụng tập tin này với các dịch vụ DNS Server, bạn cần phải bấm Từ tập tin trong tính Server. Trên máy chủ BIND, tập tin này thường được gọi là "named.boot" tập tin.|
|Cache.dns|Được sử dụng để tải trước bản ghi tài nguyên vào bộ nhớ cache tên máy chủ DNS. các máy chủ DNS sử dụng tập tin này để giúp xác định vị trí máy chủ root trên hoặc mạng của bạn hoặc mạng Internet.|
||Theo mặc định, file này chứa các bản ghi tài nguyên DNS rằng thủ cache nội bộ của máy chủ với địa chỉ của máy chủ gốc có thẩm quyền cho Internet. Nếu bạn đang thiết lập một máy chủ DNS để phân giải tên DNS Internet, những thông tin trong tập tin này là cần thiết trừ khi bạn cho phép sử dụng một máy chủ DNS như một giao nhận để giải quyết các tên này.|
||Lưu lượng truy cập đến các máy chủ gốc Internet là nặng, nhưng bởi vì máy chủ lưu trữ tên không được giải quyết thông thường ở cấp độ này, tải trọng có thể được xử lý hợp lý. Thay vào đó, tập tin gốc gợi ý cung cấp thông tin giới thiệu có thể hữu ích trong phân giải tên DNS để chuyển hướng một truy vấn đến các máy chủ khác được uỷ quyền cho tên nằm bên dưới gốc.|
||Đối với các máy chủ DNS hoạt động riêng trên mạng nội bộ của bạn, giao diện điều khiển DNS có thể học hỏi |
||và thay thế nội dung của tập tin này với các máy chủ gốc nội bộ trên mạng của bạn, miễn là chúng có thể truy cập thông qua mạng khi bạn đang thiết lập và cấu hình máy chủ DNS mới. Nó có thể được cập nhật bằng cách sử dụng giao diện điều khiển DNS từ tab gốc gợi ý nằm dưới các thuộc tính máy chủ hiện hành.|
||Tập tin này có cài đặt sẵn bộ nhớ cache tên máy chủ khi nó được bắt đầu.|
|Root.dns|Tập tin Root zone. Tập tin này có thể xuất hiện tại một máy chủ DNS nếu nó được cấu hình như một máy chủ gốc cho mạng của bạn.|
|zone_name.dns|Được sử dụng khi một zone tiêu chuẩn (hoặc chính hay thứ cấp) được thêm vào và cấu hình cho máy chủ. Loại tệp này không được tạo ra hoặc sử dụng cho zone chính đó là thư mục tích hợp, được lưu trữ trong cơ sở dữ liệu Active Directory.|



Những tập tin này có thể được tìm thấy trong systemroot \ System32 \ Dns thư mục trên máy tính của máy chủ. 


<a name="35"></a>
###3.5 Zones and Zone Transfer

DNS phân phối các cơ sở dữ liệu không gian tên DNS sử dụng những zone DNS, trong đó lưu trữ thông tin tên về một hoặc nhiều miền DNS. Có ba loại khu DNS được hỗ trợ trong Windows Server 2008:

- Zone chính. Các bản sao gốc của một khu vực nơi mà tất cả bản ghi tài nguyên được thêm vào, sửa đổi và xóa.

- Zone thứ hai. Chỉ đọc bản sao của zone chính được tạo ra và Cập Nhật bởi chuyển vùng dữ liệu từ zone chính.

- Khu vực sơ khai. Chỉ đọc bản sao của khu vực chính chỉ chứa các bản ghi tài nguyên DNS cho các máy chủ DNS được liệt kê trong vùng (SOA, NS, và kèm theo một bản ghi tài nguyên).

**Sự khác nhau giữa các zone, domain**

Zone bắt đầu như là một cơ sở dữ liệu lưu trữ cho một tên miền DNS duy nhất. Nếu các tên miền khác được thêm vào bên dưới các tên miền được sử dụng để tạo ra zone, các tên miền này có thể là một phần của zone cùng hoặc thuộc về một zone. Một khi một tên miền phụ được thêm vào, nó sau đó có thể hoặc là:

- Quản lý và bao gồm như là một phần của các hồ sơ ban đầu của khu vực, hoặc

- Ủy quyền đi đến một khu vực tạo ra để hỗ trợ các tên miền phụ

Ví dụ như hình dưới đây cho thấy tên miền microsoft.com, chứa các tên miền cho Microsoft. Khi miền microsoft.com lần đầu tiên được tạo ra tại một máy chủ, nó cấu hình như là một vùng duy nhất cho tất cả các tên Microsoft DNS. Tuy nhiên, nếu các miền microsoft.com nhu cầu sử dụng tên miền phụ, những tên miền phụ phải được bao gồm trong zone, hoặc giao đi tới một zone.

<p align="center">Tên miền DNS và Tên Subdomain</p>

<p align="center"><img src="https://i-technet.sec.s-msft.com/dynimg/IC195470.gif" /></p>


Trong ví dụ này, tên miền example.microsoft.com cho thấy một tên miền phụ mới - miền example.microsoft.com - giao đi từ zone microsoft.com và quản lý trong zone riêng của mình. Tuy nhiên, vùng microsoft.com cần chứa một vài bản ghi tài nguyên để cung cấp các thông tin đoàn tham chiếu đến các máy chủ DNS được uỷ quyền cho miền phụ giao example.microsoft.com.

Nếu khu vực microsoft.com không sử dụng uỷ quyền cho một tên miền phụ, bất kỳ dữ liệu nào cho tên miền phụ vẫn là một phần của zone microsoft.com. Ví dụ, dev.microsoft.com tên miền phụ không được ủy quyền đi nhưng được quản lý bởi zone microsoft.com.

**Chuyển zone gia tăng**

Chuyển vùng gia tăng được mô tả trong RFC 1995 như là một tiêu chuẩn để sao chép các khu DNS DNS bổ sung. Khi gia tăng chuyển được hỗ trợ bởi một máy chủ DNS hoạt động như là nguồn gốc cho khu vực và bất kỳ máy chủ có thể sao chép các khu vực từ nó, chuyển gia tăng cung cấp một phương pháp hiệu quả hơn của tuyên truyền thay đổi khu vực và Cập Nhật.

Trong triển khai DNS trước đó, bất kỳ yêu cầu một bản cập nhật của dữ liệu vùng cần chuyển đầy đủ của toàn bộ cơ sở dữ liệu zone sử dụng một truy vấn AXFR. Với chuyển gia tăng, một loại truy vấn thay thế (IXFR) có thể được sử dụng để thay thế. Điều này cho phép các máy chủ thứ cấp để chỉ kéo những zone thay đổi cần thiết để đồng bộ hóa các bản sao của nó trong những zone có nguồn gốc của nó, hoặc là một bản sao chính hoặc phụ của zone được duy trì bởi một máy chủ DNS.

Với IXFR zone chuyển, sự khác biệt giữa các mã nguồn và các phiên bản sao chép của zone one đầu tiên được xác định. Nếu các zone được xác định là phiên bản tương tự-như được chỉ ra bởi trường số serial trong bản ghi tài nguyên SOA của từng zone — không chuyển giao được thực hiện.

Nếu số serial cho các khu vực tại nguồn là lớn hơn ở các máy chủ thứ cấp yêu cầu, chuyển giao được thực hiện chỉ có những thay đổi để RR cho mỗi phiên bản gia tăng của zone. Đối với một truy vấn IXFR để thành công và thay đổi được gửi đi, các máy chủ DNS nguồn cho các zone phải giữ một lịch sử của những thay đổi zone gia tăng để sử dụng khi trả lời các câu truy vấn. Quá trình chuyển giao gia tăng đòi hỏi ít lưu lượng đáng kể trên một mạng lưới và vùng chuyển được hoàn thành nhanh hơn nhiều.

**Ví dụ: chuyển Zone**

Một chuyển vùng có thể xảy ra trong bất kỳ tình huống sau đây:

- Khi Refresh interval hết hạn

- Khi một máy chủ thứ cấp được thông báo về những thay đổi vùng bằng máy chủ của nó.

- Khi các dịch vụ DNS Server được bắt đầu tại một máy chủ thứ cấp cho zone.

- Khi điều khiển DNS được sử dụng tại một máy chủ thứ cấp cho các khu vực tự bắt đầu chuyển từ máy chủ tổng thể của nó.

Zone chuyển tiếp yêu cầu luôn luôn thực hiện tại máy chủ thứ cấp cho một zone, và sau đó được gửi đến các máy chủ master được cấu hình mà hành động như là nguồn của họ cho zone. máy chủ Master có thể là bất kỳ máy chủ DNS khác đó tải khu vực, chẳng hạn như một trong hai máy chủ chính cho zone hoặc một máy chủ thứ cấp. Khi máy chủ tổng nhận được yêu cầu cho các zone, nó có thể trả lời với một hoặc chuyển nhượng một phần hoặc toàn bộ zone để máy chủ thứ cấp. 

**Quá trình chuyển giao Zone**

Như thể hiện trong hình sau đây, chuyển vùng giữa các máy chủ theo một quá trình đặt hàng. Quá trình này khác nhau, tuỳ thuộc vào một zone đã được nhân rộng trước đó, hoặc nếu nhân rộng ban đầu của một zone mới đang được thực hiện.

<p align="center">Quy trình chuyển Zone</p>

<p align="center"><img src="https://i-technet.sec.s-msft.com/dynimg/IC195472.gif" /></p>

1 .Trong cấu hình mới, máy chủ đích sẽ gửi một chuyển giao đầu tiên "tất cả zone" (AXFR) yêu cầu đến máy chủ tổng DNS được cấu hình như là nguồn của nó đối với zone.

2 .(Nguồn) máy chủ tổng thể đáp ứng đầy đủ và chuyển vùng đến máy chủ thứ cấp (đích). 

Các khu vực được giao cho các máy chủ đích yêu cầu chuyển với phiên bản của nó được thiết lập bằng cách sử dụng một số lĩnh vực nối tiếp trong các thuộc tính cho sự bắt đầu của chính quyền RR. SOA RR cũng có một khoảng thời gian quy định refresh interval trong vài giây (theo mặc định, 900 giây hoặc 15 phút) để cho biết khi máy chủ đích nên yêu cầu tiếp theo để làm mới các khu vực có các máy chủ nguồn.

3 .Khi khoảng refresh interval hết hạn, một truy vấn SOA được sử dụng bởi các máy chủ đích để yêu cầu đổi mới của vùng từ máy chủ nguồn.

4 .Các máy chủ nguồn sẽ trả lời các truy vấn cho các hồ sơ SOA của nó.

Phản ứng này có chứa số serial cho các zone trong tình trạng hiện tại của mình tại máy chủ nguồn.

 Các máy chủ đích kiểm tra số serial của bản ghi SOA trong các phản ứng và xác định làm thế nào để refresh interval khu vực. 

Nếu giá trị của số thứ tự trong các phản ứng SOA bằng số địa phương hiện tại của nó, nó kết luận rằng khu vực là như nhau ở cả hai máy chủ và chuyển giao khu vực không cần thiết. Các máy chủ đích sau đó đổi mới khu vực bằng cách đặt lại khoảng thời gian refresh của nó dựa trên giá trị của lĩnh vực này trong việc ứng phó SOA từ máy chủ nguồn của nó.

Nếu giá trị của số thứ tự trong các phản ứng SOA là cao hơn số địa phương hiện tại của nó, nó kết luận rằng khu vực đã được cập nhật và chuyển giao được yêu cầu.

5 .Nếu máy chủ đích kết luận rằng khu vực đã thay đổi, nó sẽ gửi một truy vấn đến máy chủ IXFR nguồn, chứa giá trị hiện tại địa phương của mình cho số nối tiếp trong các bản ghi SOA cho khu vực.

6 .Các máy chủ nguồn phản ứng với hoặc là chuyển gia tăng hoặc đầy đủ của zone.

Nếu máy chủ nguồn hỗ trợ chuyển gia tăng bằng cách duy trì một lịch sử thay đổi khu vực gia tăng gần đây cho bản ghi tài nguyên sửa đổi, nó có thể trả lời với một IXFR của khu vực.

Nếu máy chủ nguồn không hỗ trợ chuyển gia tăng, hoặc không có một lịch sử thay đổi khu vực, nó có thể trả lời với một (AXFR) đầy đủ chuyển vùng để thay thế.


**EDNS0**

Mở rộng cơ chế cho DNS (EDNS0 như được định nghĩa trong RFC 2671) cho phép DNS người yêu cầu để quảng cáo kích thước của gói UDP và tạo điều kiện cho việc chuyển giao các gói dữ liệu lớn hơn 512 octet, hạn chế DNS gốc cho kích thước gói tin UDP (RFC 1035). Khi một máy chủ DNS sẽ nhận được một yêu cầu trên tầng giao vận UDP, nó xác định kích thước gói tin UDP của người yêu cầu từ tùy chọn (OPT) RR và quy mô của nó phản ứng có chứa càng nhiều bản ghi tài nguyên như được cho phép gói tin UDP tối đa kích thước được chỉ định bởi người yêu cầu.

Hỗ trợ Windows Server 2003 DNS cho EDNS0 được kích hoạt theo mặc định. Nó có thể bị vô hiệu hóa bằng cách sử dụng sổ đăng ký. Xác định vị trí registry subkey sau đây:

HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\DNS\Parameters

Thêm EnableEDNSProbes nhập vào khóa. Cho nhập một giá trị DWORD và đặt nó vào 0x0 để vô hiệu hóa EDNS0.

**Phản ứng ENDS0 UDP**
Trước khi một máy chủ DNS giả định rằng người yêu cầu hỗ trợ EDNS0, máy chủ DNS phải nhận được một truy vấn có chứa một bản ghi tài nguyên OPT. Một bản ghi OPT không chứa dữ liệu DNS thực tế và nội dung của nó liên quan đến lớp chỉ có tin nhắn UDP vận chuyển. 

Khi máy chủ DNS sẽ nhận được một truy vấn có chứa một bản ghi OPT quảng cáo UDP gói kích thước tối đa, nó sẽ cắt ngắn kích thước bất kỳ phản ứng của UDP lớn hơn giới hạn quy định trong hồ sơ OPT. 

Theo mặc định, các máy chủ DNS bao gồm bản ghi tài nguyên OPT chỉ tối đa UDP của nó trong phản ứng với các truy vấn có chứa bản ghi tài nguyên OPT. 

Nếu máy chủ DNS sẽ nhận được một truy vấn mà không chứa một bản ghi tài nguyên OPT, nó giả định máy chủ của người yêu cầu không hỗ trợ EDNS0 và sẽ trả lời cho người yêu cầu giả định rằng người gửi không chấp nhận các gói UDP lớn hơn 512 byte. Trong trường hợp này, máy chủ DNS sẽ cắt kích thước phản ứng UDP của mình đến tối đa là 512 byte.

**Truy vấn EDNS0 UDP**

Trước khi máy chủ DNS yêu cầu gửi một truy vấn, nó sẽ kiểm tra bộ nhớ cache của nó để xác định nếu các máy chủ DNS đáp ứng hỗ trợ EDNS0. Nếu máy chủ DNS đáp ứng hỗ trợ EDNS0, máy chủ DNS yêu cầu gắn một bản ghi tài nguyên OPT phần bổ sung của các truy vấn nó sẽ gửi. (Tất cả các truy vấn có năm phần:. Tiêu đề, câu hỏi, câu trả lời, quyền hạn và bổ sung) Nếu, theo bộ nhớ cache của máy chủ DNS yêu cầu, máy chủ DNS phản ứng không hỗ trợ EDNS0, máy chủ DNS yêu cầu sẽ không được đính kèm một bản ghi tài nguyên OPT để truy vấn trước khi nó được gửi.

**Việc xác định và bộ nhớ đệm EDNS0 hỗ trợ**

Khi máy chủ DNS sẽ nhận được một yêu cầu hoặc phản ứng từ một máy chủ có chứa một bản ghi OPT, máy chủ DNS lưu trữ các phiên bản EDNS hỗ trợ bởi các máy chủ (như EDNS0). Nếu không có hồ sơ OPT trong một yêu cầu hoặc phản ứng từ một máy chủ, bộ nhớ cache của máy chủ DNS sẽ chỉ ra rằng các máy chủ không hỗ trợ EDNS0. Nếu bộ nhớ cache đã chỉ ra rằng các máy chủ hỗ trợ ENDS0, sau đó bộ nhớ cache sẽ không được thay đổi.

Giá trị mặc định cho bao lâu một loạt EDNS0 hỗ trợ thông tin được lưu trữ là 86400 (một ngày được chỉ định trong giây). Giá trị này có thể được thay đổi trong sổ đăng ký.

Các máy chủ DNS xác định rằng một máy chủ không hỗ trợ EDNS0 khi nó yêu cầu một bản ghi tài nguyên OPT và nhận được một phản ứng có chứa một trong các mã phản ứng sau đây (RCODE) giá trị trong tiêu đề, như thể hiện trong bảng sau. 

<p align="center">Giá trị mã thất bại EDNS0</p>

|Tên|Gía trị|Mô tả|
|-----|----------|-------|
|FORMERR|1|Format Error. Các máy chủ tên đã không giải thích các bản ghi tài nguyên OPT.|
|SERVFAIL|2|Server Failure. Các máy chủ tên đã không xử lý truy vấn vì một vấn đề với máy chủ tên.|
|NOTIMPL|4|Not Implemented.  Tên server không hỗ trợ các loại truy vấn yêu cầu.|

<a name="36"></a>
###3.6 Tích hợp Active Directory

Các dịch vụ DNS Server được tích hợp vào thiết kế và thực hiện của Active Directory. Active Directory cung cấp một công cụ doanh nghiệp cấp cho tổ chức, quản lý và định vị các nguồn lực trong một mạng.

Ngoài việc hỗ trợ một cách thông thường của việc duy trì và nhân rộng các tập tin DNS, việc thực hiện của DNS trong Windows Server 2003 có tùy chọn sử dụng Active Directory như là lưu trữ dữ liệu và các công cụ sao chép cho DNS. DNS là miền cơ chế vị trí điều khiển cho Active Directory.

**Lợi ích của việc tích hợp DNS với AD DS**

Sử dụng AD DS như là lưu trữ dữ liệu và các công cụ sao chép cung cấp các lợi ích sau:  

- Nhân rộng DNS được thực hiện bởi Active Directory, do đó, không cần thiết phải hỗ trợ một cấu trúc liên kết nhân rộng riêng biệt cho các máy chủ DNS.

- Active Diẻctory dịch vụ sao chép cung cấp cho bất động sản nhân rộng.

- Active Directory là dịch vụ an toàn. 

- Một máy chủ DNS chính là loại bỏ như một điểm duy nhất của thất bại. Không giống như bản sao DNS gốc, Active Directory Dịch là dịch vụ đa chủ; một bản Cập Nhật có thể được thực hiện cho bất kỳ kiểm soát miền trong nó, và thay đổi sẽ được truyền đến các bộ điều khiển tên miền. Bằng cách này nếu DNS được tích hợp vào dịch vụ Active Directory công cụ sao chép sẽ luôn luôn đồng bộ hoá thông tin zone DNS.

Do đó tích hợp Active Directory đơn giản hoá đáng kể sự quản lý của một không gian tên DNS. Đồng thời, chuyển vùng tiêu chuẩn để các máy chủ DNS khác (máy chủ DNS khác so với Windows 2000 Server, Windows Server 2003 và Windows máy chủ DNS Server 2008, cũng như các phiên bản trước của máy chủ DNS Microsoft) vẫn được hỗ trợ.

**Làm thế nào DNS tích hợp với AD DS**

Khi bạn cài đặt Active Directory trên một máy chủ, bạn có thể quảng bá máy chủ đến vai trò của một bộ điều khiển tên miền cho tên miền được chỉ định. Khi hoàn tất quá trình này, bạn sẽ được nhắc để chỉ định một tên miền DNS cho tên miền Active Directory mà bạn đang tham gia và thúc đẩy các máy chủ.

**Nhân rộng mô hình**

Khi thông tin DNS zone được lưu trữ trong Active Directory và một bản Cập Nhật được thực hiện với một máy chủ DNS, nó viết dữ liệu Cập Nhật vào Active Directory. Active Directory bây giờ là trách nhiệm sao chép dữ liệu cho các bộ điều khiển tên miền. Các máy chủ DNS đang chạy trên bộ điều khiển tên miền khác sẽ thăm dò ý kiến các bản Cập Nhật từ Active Directory.

Bởi vì dịch vụ Active Directory sử dụng các mô hình nhân rộng đa chủ, cập nhật DNS có thể được viết với bất kỳ máy chủ DNS Active Directory tích hợp, và các dữ liệu sẽ tự động được nhân rộng trên tất cả các bộ điều khiển miền. 

Khả năng viết để Active Directory từ bộ điều khiển vùng nhiều cùng một lúc có thể tạo ra một tình huống xung đột, nơi các thay đổi được thực hiện đến cùng một đối tượng trên hai máy chủ DNS khác nhau. Cuộc xung đột cuối cùng sẽ được giải quyết trong lợi của Cập Nhật được thực hiện cho các đối tượng dựa trên timestamps các bản Cập Nhật. Các quy tắc tương tự được áp dụng trong trường hợp mà hai hoặc nhiều nút với cùng tên được tạo ra trên hai hoặc nhiều máy chủ DNS. Cho đến khi cuộc xung đột đã được giải quyết và các máy chủ DNS chứa bản Cập Nhật không hợp lệ, cuộc thăm dò các dữ liệu hợp lệ từ Active Directory, có thể yêu cầu cho các đối tượng tương tự được thực hiện cho hai máy chủ DNS khác nhau sẽ được giải quyết một cách khác nhau. Đây là lý do tại sao cơ sở dữ liệu Active Directory được gọi là lỏng lẻo nhất quán.

Active Directory tích hợp cung cấp một lợi thế đối với zone tin sao lưu. Với khu tập hậu thuẫn, chỉ máy chủ DNS có thẩm quyền chính cho một zone có thể sửa đổi các zone. Với Active Directory tích hợp, tất cả các bộ điều khiển miền cho miền Active Directory, nơi vùng được lưu trữ có thể sửa đổi các zone và sau đó tái tạo những thay đổi để điều khiển tên miền khác. Quá trình sao chép này được gọi là sao chép đa chủ vì nhiều bộ điều khiển miền có thể cập nhật các zone.

Windows Server 2003 domain controller tái tạo bản ghi tài nguyên chứa trong khu Active Directory tích hợp sử dụng bản sao Active Directory. Khu lưu trữ trong Active Directory cũng có thể được chuyển đến các máy chủ thứ cấp để tạo ra các vùng thứ cấp trong cùng một cách mà khu tập hậu thuẫn được chuyển giao.

Active Directory tích hợp cung cấp nhiều lợi ích, bao gồm cả khả năng chịu lỗi, an ninh, quản lý đơn giản, và nhân rộng hiệu quả hơn các khu.

**Zone Active Directory tích hợp**

Khi bạn cấu hình một khu vực chính là Active Directory tích hợp, các khu vực được lưu trữ trong AD DS. 

Hình dưới đây cho thấy cấu hình này. 

<p align="center">Khu Active Directory tích hợp </p>

<p align="center"><img src="https://i-technet.sec.s-msft.com/dynimg/IC195473.gif" /></p>

Các thành phần máy chủ DNS chỉ chứa một bản sao của zone. Khi DNS bắt đầu, nó đọc một bản sao của zone từ các cơ sở dữ liệu Active Directory (bước 1). Sau đó, khi máy chủ DNS sẽ nhận được một sự thay đổi, nó viết thay đổi cơ sở dữ liệu Active Directory (bước 2).

Thông qua bản sao Active Directory,  Ngoài ra, thông qua chuyển khoản tiêu chuẩn zone, các máy chủ DNS có thể gửi bản sao của vùng với bất kỳ máy chủ DNS thứ cấp mà yêu cầu nó. Các máy chủ DNS có thể thực hiện cả hai chuyển zone gia tăng và đầy đủ. Hình dưới đây cho thấy cách cùng một zone có thể được nhân rộng bằng cách sử dụng cả hai Active Directory nhân rộng và chuyển giao zone chuẩn.

<p align="center">Active Directory nhân rộng và chuyển vùng</p>

<p align="center"><img src="https://s-media-cache-ak0.pinimg.com/736x/12/53/3b/12533b1bbf6f6a3da43f43ead0314418.jpg" /></p>

Theo mặc định, khi dịch vụ DNS Server bắt đầu trên một bộ điều khiển tên miền, nó sẽ kiểm tra xem liệu Active Directory có sẵn và nếu nó có chứa bất kỳ vùng DNS. Nếu Active Directory không có zone, các dịch vụ DNS Server tải chúng từ Active Directory. Các dịch vụ DNS Server tự động ghi lại các tập tin khởi động đều đặn. Các tập tin khởi động có thể được cập nhật bằng tay bằng cách sử dụng giao diện điều khiển DNS.

**Vị trí lưu trữ khu Directory tích hợp**

Active Directory là một hướng đối tượng X.500 tương thích cơ sở dữ liệu mà tổ chức các nguồn lực sẵn có trên mạng của bạn trong một cấu trúc giống như cây phân cấp. Cơ sở dữ liệu này được quản lý bởi một bộ điều khiển miền. Các phần của cơ sở dữ liệu Active Directory mà một bộ điều khiển tên miền cụ thể là quyền được đặt trên cùng một máy tính như bộ điều khiển tên miền là. Mọi nguồn lực trong Active Directory được đại diện bởi một đối tượng. Có hai kiểu khác nhau của các đối tượng được hỗ trợ bởi Active Directory: 

-  Container-đối tượng có thể chứa các đối tượng container và lá khác.

- Leafs-đối tượng đại diện cho một tài nguyên cụ thể trong cây dịch vụ Active Directory.

Mỗi đối tượng Active Directory có thuộc tính gắn với nó mà xác định tính chất đặc thù của đối tượng. 

Các lớp học của các đối tượng trong cơ sở dữ liệu Active Directory, cũng như các thuộc tính của từng đối tượng, được định nghĩa trong lược đồ Active Directory. Nói cách khác, các container định nghĩa cho mỗi lớp đối tượng có sẵn trong Active Directory. Sau đây là ví dụ của các đối tượng lớp dịch vụ Active Directory:

- User

- Group

- Organizational Unit

- DnsZone

- DnsNode

Trong Windows 2000 Server, khu tích hợp Active Directory đã được lưu trữ trong vùng miền của thư mục. Khu vựcone lưu trữ tên miền phân vùng được sao chép tới tất cả các bộ kiểm soát miền trong tên miền. Phạm vi mở rộng này không phải là cần thiết cho một số ứng dụng, chẳng hạn như DNS. Windows Server 2003 Active Directory cung cấp một loại mới của phân vùng, được gọi là phân vùng thư mục ứng dụng, để cho phép phạm vi rộng khác nhau. 

**Các đối tượng DNS Active Directory**

Theo mặc định, Windows Server 2003 Active Directory tích hợp khu được lưu trữ trong toàn miền ứng dụng phân thư mục của thư mục. Khu vực thông tin được lưu trữ với các thùng chứa có tên phân biệt là: CN = MicrosoftDNS, DC = tên miền DNS. Thông tin khu cho các khu vực lưu trữ trên bộ kiểm soát miền trong tên miền example.com sẽ được lưu trữ trong CN = MicrosoftDNS, DC = DomainDnsZones, DC = ví dụ, DC = com.

Các phân vùng thư mục ứng dụng DNS không được hiển thị bởi tất cả các công cụ quản trị Active Directory. Để xem các phân vùng thư mục, bạn có thể sử dụng dnscmd (công cụ dòng lệnh) hoặc ADSI Edit (adsiedit.msc) ở công cụ hỗ trợ.

Phạm vi rộng của phân vùng thư mục ứng dụng DNS tùy chỉnh được xác định bởi số lượng các bộ điều khiển vùng cho gia nhập phân vùng. Theo mặc định, chỉ có các thành viên của nhóm quản trị viên của doanh nghiệp có thể tranh thủ một máy chủ DNS trong một phân vùng thư mục ứng dụng DNS.

Khi một máy chủ DNS được gia nhập vào một phân vùng thư mục ứng dụng DNS, bạn có thể lưu trữ các vùng DNS trong đó phân vùng thư mục ứng dụng bằng cách sử dụng giao diện điều khiển DNS. Giá trị FQDN cần chỉ định tên của phân vùng thư mục ứng dụng DNS mới. Bạn phải sử dụng một DNS tên miền đầy đủ.Bảng sau đây liệt kê các loại đối tượng DNS được lưu trữ trong Active Directory.

**Đối tượng DNS lưu trữ trong Active Directory**

|Đối tượng|Mô tả|
|--------------|--------|
|DnsZone|Container được tạo ra khi một zone được lưu trữ trong Active Directory.|
|DnsNode|Leaf đối tượng sử dụng để lập bản đồ và kết hợp một tên trong vùng để tài nguyên dữ liệu.|
|DnsRecord|Đặc tính của một đối tượng dnsNode được sử dụng để lưu trữ các bản ghi tài nguyên liên kết với các đối tượng được đặt tên theo nút.|
|DnsProperty|Đặc tính của một đối tượng dnsZone được sử dụng để lưu trữ thông tin cấu hình zone.|

Các đối tượng MicrosoftDNS chứa một hoặc nhiều đối tượng chứa dnsZone. Mỗi đối tượng dnsZone đại diện cho một zone.

MicrosoftDNS chứa những đối tượng dnsZone sau đây:

- Zone ngược 72.16.172.in-addr.arpa

-  Zone chuyển tiếp tra cứu, example.com

- Root hints , RootDNSServers

Hình ảnh sau đây cho thấy các đối tượng dnsZone trong Active Directory.

<p align="center">Đối tượng DNS trong Active Directory</p>

<p align="center"><img src="https://i-technet.sec.s-msft.com/dynimg/IC213338.gif" /></p>

Hình này cho thấy các đối tượng dnsNode sau trong các đối tượng container dnsZone cho example.com:

- @, cho thấy rằng các nút có tên giống như các đối tượng dnsZone. 

- **delegated**, một tên miền phụ được giao.

- **host.notdelegated**, một máy chủ trong miền không delegated.example.com, một tên miền mà được điều khiển bởi các zone trên example.com.

- **host1**, một máy trong miền example.com

- **mailserver**, mail server trong miền example.com

- **nameserver**, tên server trong miền example.com

- **notdelegated**, tên miền notdelegated.example.com, mà được điều khiển bởi zone trên example.com.

Đối tượng lá dnsNode có một đặc tính được gọi là dnsRecord với một thể hiện của một giá trị cho mỗi bản ghi kết hợp với tên của đối tượng. Trong ví dụ này, dnsNode lá đối tượng mailserver.example.com có một thuộc tính "A" mà chứa địa chỉ IP.

 Nếu bạn muốn xem hệ thống phân cấp tên miền DNS và các hồ sơ liên quan, sử dụng DNS console. Ngoài ra, nếu bạn muốn xem các khu vực, bạn có thể lấy chúng bằng cách sử dụng nslookup. 


<a name="4"></a>
#4.Các qúa trình và tương tác DNS

Các qúa trình và tương tác DNS liên quan đến các thông tin liên lạc giữa các máy khách và máy chủ DNS trong việc giải quyết các truy vấn DNS và cập nhật động, và giữa các máy chủ DNS trong phân giải tên và quản lý zone. Quá trình học và tương tác phụ thuộc vào sự hỗ trợ cho các công nghệ như Unicode và WINS.

<a name="41"></a>
###4.1 Truy vấn DNS hoạt động thế nào

Khi một DNS client cần phải tìm một tên được sử dụng trong một chương trình, nó sẽ truy vấn máy chủ DNS để giải quyết tên. Mỗi thông điệp truy vấn của khách hàng gửi có chứa ba mẩu thông tin, xác định một câu hỏi cho các máy chủ để trả lời:

1 . Một quy định tên miền DNS, trạng thái như là một tên miền hoàn toàn đủ điều kiện.

2 . Một loại truy vấn cụ thể, có thể chỉ định một bản ghi tài nguyên theo loại hoặc một loại đặc biệt của hoạt động truy vấn.

3 . Một lớp được chỉ định cho các tên miền DNS. Đối với các máy chủ DNS Windows, điều này luôn luôn nên được quy định như lớp Internet (IN).

Ví dụ, các tên được chỉ định có thể là FQDN cho máy tính, chẳng hạn như "" host-a.example.microsoft.com. "", và loại truy vấn cụ thể để tìm kiếm một bản ghi địa chỉ (A) tài nguyên của tên đó. Hãy suy nghĩ của một truy vấn DNS là một khách hàng yêu cầu một máy chủ một câu hỏi gồm hai phần, chẳng hạn như "bạn có bất kỳ bản ghi tài nguyên A cho một máy tính được đặt tên 'hostname.example.microsoft.com.' ”? Khi khách hàng nhận được một câu trả lời từ máy chủ, nó đọc và giải thích các trả lời một bản ghi tài nguyên, học các địa chỉ IP cho máy tính mà nó yêu cầu tên.

Truy vấn DNS giải quyết trong một số cách khác nhau. Một khách hàng đôi khi có thể trả lời một truy vấn địa phương sử dụng các thông tin được lưu trữ thu được từ một truy vấn trước đó. Các máy chủ DNS có thể sử dụng bộ nhớ cache riêng của mình thông tin bản ghi tài nguyên để trả lời một truy vấn. Một máy chủ DNS cũng có thể truy vấn hoặc liên hệ với máy chủ DNS khác thay mặt cho các khách hàng yêu cầu để giải quyết đầy đủ tên, sau đó gửi một câu trả lời lại cho khách hàng. Quá trình này được gọi là đệ quy.

Ngoài ra, khách hàng có thể tự cố gắng liên lạc thêm các máy chủ DNS để giải quyết một tên. Khi một khách hàng như vậy, nó sử dụng các truy vấn riêng biệt và bổ sung dựa trên câu trả lời giới thiệu từ các máy chủ. Quá trình này được gọi là sự lặp lại.

Nói chung, quá trình truy vấn DNS xảy ra trong hai phần:

- Một truy vấn tên bắt đầu tại một máy tính khách hàng và được thông qua một trình giải quyết, các dịch vụ DNS Client, giải quyết.

- Khi truy vấn không thể được giải quyết tại địa phương, các máy chủ DNS có thể được truy vấn khi cần thiết để giải quyết tên.

Cả hai quá trình đều được giải thích chi tiết hơn trong các phần sau.

**Phần 1: Dịch vụ giải quyết DNS Client  **

 Hình dưới đây cho thấy một cái nhìn tổng quan về quá trình truy vấn DNS hoàn chỉnh. 

*Tổng quan về quá trình truy vấn DNS *

<p align="center"><img src="https://i-technet.sec.s-msft.com/dynimg/IC195476.gif" /></p>

Như thể hiện trong những bước đầu tiên của quá trình truy vấn, một tên miền DNS được sử dụng trong một chương trình trên máy tính địa phương. Các yêu cầu sau đó được đưa đến dịch vụ DNS Client cho độ phân giải sử dụng thông tin được lưu trữ tại địa phương. Nếu tên truy vấn có thể được giải quyết, các truy vấn được trả lời và quá trình được hoàn thành.

Giải quyết bộ nhớ cache tại địa phương có thể bao gồm thông tin tên được lấy từ hai nguồn:

- Nếu một tập tin máy chủ được cấu hình tại địa phương, bất kỳ máy chủ tên-to-địa chỉ ánh xạ từ tập tin đó được cài đặt sẵn vào bộ nhớ cache khi dịch vụ DNS Client được bắt đầu.

-  bản ghi tài nguyên thu được trong phản ứng trả lời từ các truy vấn DNS trước được thêm vào bộ nhớ cache và lưu giữ trong một khoảng thời gian. 

 Nếu truy vấn không phù hợp với một mục trong bộ nhớ cache, quá trình phân giải tiếp tục với các khách hàng truy vấn máy chủ DNS để giải quyết tên. 

**Phần 2: Truy vấn một DNS Server**

Như được chỉ ra trong hình trước đó, khách hàng truy vấn một máy chủ DNS ưa thích. Các máy chủ thực sự được sử dụng trong các truy vấn ban đầu khách hàng/máy chủ được lựa chọn từ một danh sách toàn cầu.

Khi máy chủ DNS sẽ nhận được một truy vấn, đầu tiên nó sẽ kiểm tra xem nó có thể trả lời các truy vấn có quyền dựa trên các thông tin bản ghi tài nguyên chứa trong một zone cấu hình cục bộ trên máy chủ. Nếu tên truy vấn phù hợp với một bản ghi tài nguyên tương ứng trong thông tin zone địa phương, các máy chủ trả lời có quyền sử dụng thông tin này để giải quyết các tên được truy vấn.

Nếu không có thông tin khu vực tồn tại cho tên truy vấn, máy chủ sau đó sẽ kiểm tra để xem nếu nó có thể giải quyết tên bằng cách sử dụng các thông tin đã lưu ẩn cục bộ từ truy vấn trước đó.  Nếu trùng hợp được tìm thấy ở đây, các máy chủ trả lời với thông tin này. Một lần nữa, nếu máy chủ ưa thích có thể trả lời với một phản ứng tích cực phù hợp từ bộ nhớ cache của nó cho khách hàng yêu cầu, các truy vấn được hoàn thành.

Nếu tên truy vấn không tìm thấy một câu trả lời phù hợp tại máy chủ ưa thích của nó - hoặc từ thông tin bộ nhớ cache hoặc zone của nó - quá trình truy vấn có thể tiếp tục, sử dụng đệ quy để giải quyết đầy đủ tên. Điều này liên quan đến việc hỗ trợ từ các máy chủ DNS khác để giúp giải quyết tên. Theo mặc định, các dịch vụ DNS Client yêu cầu máy chủ để sử dụng một quá trình đệ quy để giải quyết đầy đủ tên đại diện cho khách hàng trước khi trở về một câu trả lời.

Để cho các máy chủ DNS để làm đệ quy đúng cách, đầu tiên nó cần một số thông tin liên lạc hữu ích về các máy chủ DNS khác trong không gian tên miền DNS. Thông tin này được cung cấp dưới hình thức gợi ý gốc, một danh sách các bản ghi tài nguyên sơ bộ mà có thể được sử dụng bởi các dịch vụ DNS để xác định vị trí các máy chủ DNS khác có thẩm quyền đối với thư mục gốc của cây không gian tên miền DNS. máy chủ gốc có thẩm quyền cho các tên miền gốc và miền cấp cao nhất trong cây không gian tên miền DNS.

Bằng cách sử dụng những gợi ý gốc để tìm các máy chủ gốc, một máy chủ DNS có thể hoàn thành việc sử dụng đệ quy. Về lý thuyết, quá trình này cho phép bất kỳ máy chủ DNS để xác định vị trí các máy chủ có thẩm quyền cho bất kỳ tên miền DNS khác sử dụng ở bất kỳ cấp độ nào trong cây không gian tên.

Ba hình sau đây minh họa quá trình mà theo đó các DNS client truy vấn các máy chủ trên mỗi bộ điều hợp.

*Truy vấn DNS Server, Phần 1 *

<p align="center><img src="https://i-technet.sec.s-msft.com/dynimg/IC195477.gif" /></p>

*Truy vấn DNS Server, Phần 2*

<p align="center><img src="https://i-technet.sec.s-msft.com/dynimg/IC195478.gif" /></p>

*Truy vấn DNS Server, Phần 3*

<p align="center><img src="https://technet.microsoft.com/en-us/library/bb457118.f24zs09_big(l=en-us).jpg" /></p>

 Các dịch vụ DNS Client truy vấn các máy chủ DNS theo thứ tự sau: 

1 .  Các dịch vụ DNS Client sẽ gửi các truy vấn tên cho máy chủ DNS đầu tiên trong danh sách các adapter ưa thích của các máy chủ DNS và chờ đợi một giây cho một phản ứng. 


2 .  Nếu dịch vụ DNS Client không nhận được phản hồi từ máy chủ DNS đầu tiên trong vòng một giây, nó sẽ gửi các truy vấn tên cho các máy chủ DNS đầu tiên trên tất cả các adapter mà vẫn đang được xem xét và chờ đợi hai giây cho một phản ứng. 

3 .  Nếu dịch vụ DNS Client không nhận được phản hồi từ bất kỳ máy chủ DNS trong vòng hai giây, các dịch vụ DNS Client sẽ gửi các truy vấn cho tất cả các máy chủ DNS trên tất cả các adapter mà vẫn đang được xem xét và chờ đợi một hai giây cho một phản ứng. 

4 .  Nếu dịch vụ DNS Client vẫn không nhận được phản hồi từ bất kỳ máy chủ DNS, nó sẽ gửi các truy vấn tên cho tất cả các máy chủ DNS trên tất cả các adapter mà vẫn đang được xem xét và chờ đợi bốn giây cho một phản ứng. 

5 .  Nếu các dịch vụ DNS Client không nhận được phản hồi từ bất kỳ máy chủ DNS, máy khách DNS gửi truy vấn cho tất cả các máy chủ DNS trên tất cả các adapter mà vẫn đang được xem xét và chờ đợi tám giây cho một phản ứng. 

 Nếu dịch vụ DNS Client nhận được một phản ứng tích cực, nó ngừng truy vấn tên, cho biết thêm các phản ứng vào bộ nhớ cache và trả về đáp ứng cho khách hàng. Nếu dịch vụ DNS Client đã không nhận được phản hồi từ bất kỳ máy chủ trong vòng tám giây, các dịch vụ DNS Client phản ứng với một thời gian ra. 

Ngoài ra, nếu nó đã không nhận được phản hồi từ bất kỳ máy chủ DNS trên một bộ chuyển đổi nhất định, sau đó trong 30 giây tiếp theo, các dịch vụ DNS Client đáp ứng tất cả các truy vấn dành cho các máy chủ trên rằng adapter với thời gian chờ và không truy vấn các máy chủ . Chỉ có các máy tính chạy Windows 2000 hoặc Windows Server 2003 trả lại thời gian chờ.

Nếu tại bất kỳ điểm nào DNS Client dịch vụ sẽ nhận được một phản ứng tiêu cực từ một máy chủ, nó loại bỏ mỗi máy chủ trên bộ điều hợp rằng từ việc xem xét trong quá trình tìm kiếm này. Ví dụ, nếu ở bước 2, các máy chủ đầu tiên trên thay thế bộ điều hợp A đã cung cấp một phản ứng tiêu cực, các dịch vụ DNS Client sẽ không gửi truy vấn đến bất kỳ máy chủ nào khác trong danh sách để thay thế bộ điều hợp A.

Các dịch vụ DNS Client theo dõi mà các máy chủ trả lời tên truy vấn nhanh hơn, và nó di chuyển máy chủ lên hoặc xuống trong danh sách dựa trên một cách nhanh chóng như thế nào họ trả lời tên truy vấn.

 Hình dưới đây cho thấy cách máy khách DNS truy vấn mỗi máy chủ trên mỗi bộ điều khiển. 

* Multihomed Name Resolution *

<p align="center"><img src="https://i-technet.sec.s-msft.com/dynimg/IC195480.gif" /></p>

**Phản ứng truy vấn thay thế**

 Các mô tả trên đây của các truy vấn DNS giả định rằng quá trình này kết thúc bằng một phản ứng tích cực trở lại cho khách hàng. Tuy nhiên, các truy vấn có thể trả lại câu trả lời khác. Đây là những câu trả lời truy vấn phổ biến nhất: 

- Quyền trả lời 

-  Một câu trả lời tích cực 

-  Một câu trả lời giới thiệu 

-  Một câu trả lời tiêu cực 


Quyền trả lời là một câu trả lời tích cực trở lại cho khách hàng và cung cấp với cơ quan thiết lập bit trong thông điệp DNS để chỉ ra các câu trả lời thu được từ một máy chủ có thẩm quyền trực tiếp cho tên truy vấn.

 Một phản ứng tích cực có thể bao gồm các RR truy vấn hoặc một danh sách các RR (cũng được biết đến như một RRset) phù hợp với các tên miền DNS và ghi loại truy vấn xác định thông điệp truy vấn. 

Một câu trả lời giới thiệu có chứa RR thêm không ghi rõ tên hoặc nhập truy vấn. Đây là loại câu trả lời sẽ được trả về cho khách hàng nếu quá trình đệ quy không được hỗ trợ. Các hồ sơ có nghĩa là hành động tham khảo câu trả lời hữu ích mà khách hàng có thể sử dụng để tiếp tục truy vấn sử dụng lặp đi lặp lại. Một câu trả lời giới thiệu có chứa dữ liệu bổ sung như RR có khác hơn so với các loại truy vấn. 

 Một phản ứng tiêu cực từ các máy chủ có thể chỉ ra rằng một trong hai kết quả có thể được bắt gặp trong khi các máy chủ đã cố gắng để xử lý và giải quyết một cách đệ quy các truy vấn đầy đủ và uy quyền: 

-  Một máy chủ có thẩm quyền thông báo rằng tên truy vấn không tồn tại trong không gian tên DNS. 


-  Một máy chủ có thẩm quyền thông báo rằng tên truy vấn tồn tại, nhưng không có hồ sơ của các loại quy định tồn tại cho tên đó. 


Bộ giải quyết vượt qua các kết quả của các truy vấn, trong các hình thức hoặc là một phản ứng tích cực hay tiêu cực, quay lại chương trình yêu cầu và lưu trữ các phản ứng.

Nếu câu trả lời kết quả cho một truy vấn quá dài để gửi và được giải quyết trong duy nhất một gói tin UDP, các máy chủ DNS có thể bắt đầu một chuyển đổi dự phòng phản ứng trên TCP cổng 53 trả lời khách hàng đầy đủ trong một phiên làm việc  kết nối  giao thức TCP.

Vô hiệu hóa việc sử dụng đệ quy trên một máy chủ DNS thường được thực hiện khi khách hàng  DNS hoàn toàn đang bị giới hạn để giải quyết tên cho một máy chủ DNS cụ thể, chẳng hạn như một đặt trên mạng nội bộ của bạn. Đệ quy cũng có thể bị vô hiệu hóa khi máy chủ DNS không có khả năng giải quyết các tên DNS bên ngoài, và khách hàng được dự kiến ​​sẽ thực hiện chuyển sang một máy chủ DNS cho độ phân giải của các tên này. Nếu bạn vô hiệu hóa đệ quy trên máy chủ DNS, bạn sẽ không thể sử dụng giao nhận trên cùng một máy chủ.

Theo mặc định, máy chủ DNS sử dụng một số mặc định timings khi thực hiện đệ quy một truy vấn và liên lạc với các máy chủ DNS khác. Các giá trị mặc định bao gồm:

-  Một khoảng thời gian đệ quy thử lại trong vòng 3 giây. Đây là khoảng thời gian của dịch vụ DNS đợi trước khi thử lại một truy vấn được thực hiện trong một tra cứu đệ quy. 

-  Một khoảng thời gian chờ đệ quy của 8 giây. Đây là khoảng thời gian của dịch vụ DNS đợi trước khi bị tra cứu đệ quy đã được thử lại. 


**Truy vấn lặp làm việc như thế nào**

 Lặp đi lặp lại là các loại phân giải tên được sử dụng giữa các máy khách và máy chủ DNS khi các điều kiện sau đây là có hiệu lực: 

-  Các khách hàng yêu cầu việc sử dụng đệ quy, nhưng đệ quy được vô hiệu hóa trên máy chủ DNS. 

-  Các khách hàng không yêu cầu sử dụng của đệ quy khi truy vấn các máy chủ DNS. 

Một yêu cầu lặp đi lặp lại từ một khách hàng nói với các máy chủ DNS mà khách hàng mong đợi câu trả lời tốt nhất các máy chủ DNS có thể cung cấp ngay lập tức, mà không liên lạc máy chủ DNS khác.

Khi dùng lặp đi lặp lại, một máy chủ DNS câu trả lời khách hàng dựa trên kiến thức cụ thể của riêng mình về không gian tên đối với các dữ liệu tên được truy vấn.

Khi lặp được sử dụng, một máy chủ DNS có thể tiếp tục hỗ trợ độ phân giải tên truy vấn ngoài cho câu trả lời tốt nhất của nó trở lại cho khách hàng.  Đối với các truy vấn lặp đi lặp lại một khách hàng sử dụng danh sách cấu hình cục bộ của máy chủ DNS để liên lạc với máy chủ tên khác trong cả không gian tên DNS nếu máy chủ DNS chính của nó không thể giải quyết các truy vấn.

**Bộ nhớ đệm Caching làm việc như thế nào**


Khi các máy chủ DNS xử lý truy vấn khách hàng sử dụng đệ quy hoặc lặp đi lặp lại, họ khám phá và có được một kho quan trọng của thông tin về không gian tên DNS. Thông tin này sau đó được lưu trữ bởi máy chủ.

Bộ nhớ đệm cung cấp một cách để tăng tốc độ hiệu suất của DNS phân giải cho các truy vấn tiếp theo của tên phổ biến, trong khi giảm đáng kể lưu lượng truy vấn liên quan đến DNS trên mạng.

Như các máy chủ DNS thực hiện truy vấn đệ quy thay mặt cho khách hàng, họ tạm thời bộ nhớ cache ghi tài nguyên (RR). RR cache chứa các thông tin thu được từ các máy chủ DNS có thẩm quyền đối với tên miền DNS học được trong khi làm cho các truy vấn lặp đi lặp lại để tìm kiếm và hoàn toàn trả lời một truy vấn đệ quy thực hiện thay mặt cho một khách hàng. Sau đó, khi các khách hàng đặt mới truy vấn yêu cầu thông tin RR kết hợp lưu trữ RRs, các máy chủ DNS có thể sử dụng các thông tin lưu trữ RR để trả lời chúng.

Khi thông tin được lưu trữ, một giá trị thời gian để sống (TTL) áp dụng cho tất cả lưu trữ RRs. Miễn là TTL cho RR cache không hết hạn, một máy chủ DNS có thể tiếp tục bộ nhớ cache và sử dụng RR lại khi trả lời các truy vấn của khách hàng phù hợp với các RR. bộ nhớ đệm TTL được sử dụng bởi RRs trong hầu hết các cấu hình khu vực được phân công tối thiểu (mặc định) TTL được thiết lập trong khu vực bắt đầu của chính quyền (SOA) tài nguyên bản ghi. Theo mặc định, tối thiểu TTL là 3.600 giây (một giờ), nhưng có thể được điều chỉnh hoặc, nếu cần thiết, TTLs bộ nhớ đệm riêng lẻ có thể được đặt tại mỗi RR.


<a name="42"></a>
###4.2 Tra cứu ngược

Trong hầu hết các tra cứu DNS, khách hàng thường thực hiện một tra cứu về phía trước, đó là một tìm kiếm dựa trên các tên DNS của máy tính khác như được lưu trữ trong một bản ghi tài nguyên địa chỉ (A). Đây là loại truy vấn hy vọng một địa chỉ IP như dữ liệu tài nguyên cho các phản ứng trả lời.

DNS cũng cung cấp một quá trình tra cứu đảo ngược, cho phép khách hàng sử dụng một địa chỉ IP được biết đến trong một truy vấn tên và tìm kiếm các tên máy tính dựa trên địa chỉ của nó. Một tra cứu đảo ngược có dạng một câu hỏi, chẳng hạn như "Có thể bạn cho tôi biết tên DNS của máy tính sử dụng địa chỉ IP 192.168.1.20?"

DNS không ban đầu được thiết kế để hỗ trợ các loại truy vấn. Một vấn đề để hỗ trợ quá trình ngược lại truy vấn là sự khác biệt trong cách tổ chức các không gian tên DNS và chỉ số tên và cách các địa chỉ IP được gán. Nếu phương pháp duy nhất sẵn sàng trả lời câu hỏi trước để tìm kiếm tất cả các tên miền trong không gian tên DNS, một truy vấn ngược lại sẽ mất quá nhiều thời gian và đòi hỏi quá nhiều qúa trinh để hữu ích.

Để giải quyết vấn đề này, một miền đặc biệt được gọi là miền in-addr.arpa đã được xác định trong các tiêu chuẩn DNS và bảo lưu trong không gian tên DNS Internet để cung cấp một cách thiết thực và đáng tin cậy để thực hiện truy vấn ngược lại. Để tạo ra các không gian tên ngược lại, tên miền phụ trong miền in-addr.arpa được hình thành bằng cách sử dụng đảo ngược thứu tự của những con số trong ký hiệu chấm thập phân của địa chỉ IP.

Điều này đảo ngược trật tự của các tên miền cho mỗi giá trị octet là cần thiết bởi vì, không giống như các tên DNS, khi các địa chỉ IP được đọc từ trái sang phải, chúng được diễn giải theo cách ngược lại. Khi một địa chỉ IP được đọc từ trái sang phải, nó được xem từ các thông tin tổng quát nhất của nó (một địa chỉ mạng IP) trong phần đầu tiên của địa chỉ để các thông tin cụ thể hơn (một địa chỉ IP host) chứa trong octet cuối cùng.

Vì lý do này, thứ tự của octet địa chỉ IP phải được đảo ngược khi xây dựng cây tên miền in-addr.arpa. Các địa chỉ IP của cây DNS in-addr.arpa có thể được giao cho công ty khi họ được giao một tập hợp cụ thể hoặc hạn chế về địa chỉ IP trong các lớp địa chỉ Internet được xác định.

Cuối cùng, các cây miền in-addr.arpa, như xây dựng vào DNS, đòi hỏi thêm một loại RR - con trỏ (PTR) RR - được xác định. RR này được sử dụng để tạo ra một bản đồ trong vùng tra cứu ngược mà thường tương ứng với một host (A) tên là RR cho tên máy tính DNS của một máy chủ trong vùng chuyển tiếp tra cứu của mình.

Tên miền in-addr.arpa áp dụng cho việc sử dụng trong tất cả các mạng TCP / IP dựa trên giao thức Internet phiên bản 4 (IPv4) giải quyết. Các New Zone Wizard tự động giả định rằng bạn đang sử dụng miền này khi tạo một vùng tra cứu ngược mới.

Nếu bạn đang cài đặt DNS và cấu hình vùng tra cứu ngược lại cho một phiên bản Internet Protocol 6 (IPv6) mạng, bạn có thể chỉ định một tên chính xác ở New Zone Wizard. Điều này sẽ cho phép bạn tạo ra các vùng tra cứu ngược lại trong bảng điều khiển DNS có thể được sử dụng để hỗ trợ các mạng IPv6, trong đó sử dụng một tên miền đặc biệt khác nhau, các miền ip6.arpa.


<a name="43"></a>
###4.3 Forwarding (chuyển tiếp)

Một chuyển tiếp là một máy chủ Domain Name System (DNS) trên một mạng được sử dụng để chuyển tiếp các truy vấn DNS cho tên bên ngoài DNS đến các máy chủ DNS bên ngoài của mạng đó. Bạn cũng có thể chuyển các truy vấn theo tên miền cụ thể sử dụng giao nhận có điều kiện.

Một máy chủ DNS trên một mạng được thiết kế như là một chuyển tiếp do các máy chủ DNS khác trong mạng chuyển tiếp các truy vấn mà họ không thể giải quyết tại địa phương đến máy chủ DNS. Bằng cách sử dụng một chuyển tiêp, bạn có thể quản lý phân giải tên cho tên bên ngoài mạng của bạn, chẳng hạn như tên trên Internet, và nâng cao hiệu quả phân giải tên cho các máy tính trong mạng của bạn.

*Chỉ đạo tên truy vấn sử dụng chuyển tiếp*

 Hình dưới đây minh họa cách truy vấn tên bên ngoài đang hướng sử dụng chuyển tiếp. 


<p align="center">Tên truy vấn sử dụng chuyển tiếp bên ngoài</p>

<p align="center"><img src="https://s-media-cache-ak0.pinimg.com/736x/80/96/83/80968315500ac47580b6994696536fd7.jpg" /></p>

Nếu không có một máy chủ DNS cụ thể được xem như là một giao nhận, tất cả các máy chủ DNS có thể gửi các truy vấn bên ngoài của một mạng sử dụng gợi ý gốc của họ. Kết quả là,  rất nhiều thông tin DNS nội bộ, và có thể quan trọng, có thể được tiếp xúc trên Internet. Ngoài vấn đề an ninh và sự riêng tư này, phương pháp này có độ phân giải có thể dẫn đến một khối lượng lớn lưu lượng bên ngoài mà là tốn kém và không hiệu quả cho một mạng lưới với một kết nối Internet chậm hoặc một công ty với chi phí dịch vụ Internet cao.

Khi bạn chỉ định một máy chủ DNS như một máy chuyển tiếp, bạn thực hiện giao trách nhiệm chuyển tiếp xử lý lưu lượng truy cập bên ngoài, do đó hạn chế tiếp xúc với máy chủ DNS với Internet. Một chuyển tiếp sẽ xây dựng một bộ nhớ cache lớn các thông tin DNS bên ngoài bởi vì tất cả các truy vấn DNS bên ngoài trong mạng được giải quyết thông qua nó. Trong một khoảng thời gian ngắn, một nhà chuyển tiếp sẽ giải quyết một phần tốt đẹp của các truy vấn DNS bên ngoài sử dụng dữ liệu được lưu trữ này và do đó làm giảm lưu lượng Internet qua mạng và thời gian đáp ứng cho khách hàng DNS.

**Hành vi của một máy chủ DNS được cấu hình để sử dụng chuyển tiếp**

 Một máy chủ DNS được cấu hình để sử dụng một chuyển tiếp sẽ hành xử khác nhau từ một máy chủ DNS mà không được cấu hình để sử dụng một chuyển tiếp. Một máy chủ DNS được cấu hình để sử dụng một ứng xử chuyển tiếp như sau: 

-  Khi máy chủ DNS sẽ nhận được một truy vấn, nó cố gắng để giải quyết truy vấn này sử dụng các zone sơ cấp và thứ cấp mà nó tổ chức và bộ nhớ cache của nó. 

-  Nếu truy vấn không thể giải quyết được sử dụng dữ liệu địa phương này, sau đó nó sẽ chuyển tiếp các truy vấn đến máy chủ DNS được chỉ định như một người chuyển tiếp. 

-  Các máy chủ DNS sẽ chờ đợi một thời gian ngắn cho một câu trả lời từ chuyển tiếp trước khi cố gắng liên lạc với máy chủ DNS được quy định trong gợi ý gốc của nó. 

**Trình tự chuyển tiếp**

Trình tự giao cấu hình trên một máy chủ DNS được sử dụng được xác định theo thứ tự mà trong đó các địa chỉ IP được liệt kê trên các máy chủ DNS. Sau khi các máy chủ DNS chuyển tiếp các truy vấn để giao nhận với địa chỉ IP đầu tiên, nó chờ đợi một thời gian ngắn cho một câu trả lời từ đó giao nhận (theo các cài đặt thời gian của máy chủ DNS) trước khi tiếp tục các hoạt động chuyển tiếp với địa chỉ IP tiếp theo. Nó tiếp tục quá trình này cho đến khi nó nhận được một câu trả lời khẳng định từ một máy chuyển tiếp.

Không giống như độ phân giải thông thường, nơi một thời gian khứ hồi (RTT) được kết hợp với mỗi máy chủ, các địa chỉ IP trong danh sách giao nhận không được sắp xếp theo thời gian bay và phải được sắp xếp lại bằng tay để thay đổi tuỳ chọn.

**Chuyển tiếp và ủy quyền**

Một máy chủ DNS được cấu hình với một chuyển tiếp và lưu trữ một zone gốc sẽ sử dụng thông tin ủy quyền của nó trước khi chuyển tiếp truy vấn. Nếu không có hồ sơ ủy quyền tồn tại cho các tên DNS truy vấn, sau đó các máy chủ DNS sẽ sử dụng chuyển tiếp của mình để giải quyết các truy vấn.

**Chuyển tiếp và các máy chủ gốc**

Một lỗi thường gặp khi cấu hình chuyển tiếp là cố gắng để cấu hình chuyển tiếp trên các máy chủ gốc của một không gian tên DNS riêng. Mục tiêu của cố gắng để cấu hình chuyển tiếp trên máy chủ gốc cho một không gian tên DNS riêng là để chuyển tiếp tất cả các truy vấn ngoại vi cho máy chủ Internet DNS. Máy chủ gốc không thể được cấu hình với giao nhận tiêu chuẩn. Nếu một máy chủ gốc được truy vấn về bất kỳ tên miền, sau đó nó sẽ đề cập đến một máy chủ DNS có thể trả lời các câu hỏi (từ zone địa phương của nó, bộ nhớ cache), hoặc nó sẽ phản ứng với một thất bại (NXDOMAIN), nhưng nó không thể được cấu hình để chuyển tiếp đến các máy chủ cụ thể.

**Quy định chuyển tiếp**

Một giao nhận có điều kiện là một máy chủ DNS trên một mạng được sử dụng để chuyển các truy vấn DNS theo tên miền DNS trong truy vấn. Ví dụ, một máy chủ DNS có thể được cấu hình để chuyển tiếp tất cả các truy vấn nó nhận cho tên kết thúc với widgets.example.com đến địa chỉ IP của một máy chủ DNS cụ thể hoặc các địa chỉ IP của nhiều máy chủ DNS.

**Độ phân giải tên Intranet**

Giao nhận có điều kiện có thể được sử dụng để cải thiện độ phân giải tên miền trong mạng nội bộ của bạn. Độ phân giải tên mạng nội bộ có thể được cải thiện bằng cách cấu hình máy chủ DNS với giao cho các tên miền cụ thể bên trong. Ví dụ, tất cả các máy chủ DNS trong miền widgets.example.com có thể được cấu hình để chuyển tiếp truy vấn cho các tên kết thúc bằng test.example.com để các thẩm quyền máy chủ DNS cho merged.widgets.example.com, do đó loại bỏ bước của truy vấn các máy chủ gốc của example.com, hoặc loại bỏ các bước cấu hình máy chủ DNS trong zone widgets.example.com với các zone thứ cấp cho test.example.com.

**Độ phân giải tên Internet**

Các máy chủ DNS có thể sử dụng nhà có điều kiện để giải quyết các truy vấn giữa tên miền DNS của các công ty chia sẻ thông tin.


<a name="44"></a>
###4.4 Dynamic Update (cập nhật động)

Cập Nhật động cho phép các máy khách DNS để đăng ký và tự động cập nhật các bản ghi tài nguyên với một máy chủ DNS bất cứ khi nào thay đổi xảy ra. Điều này làm giảm sự cần thiết để hướng dẫn sử dụng quản lý bản ghi zone, đặc biệt là cho các khách hàng thường xuyên di chuyển hoặc thay đổi vị trí và sử dụng dịch vụ DHCP để có được một địa chỉ IP.

Các dịch vụ DNS Client và Server hỗ trợ sử dụng Cập Nhật năng động, như được mô tả trong RFC 2136, "Cập nhật động trong hệ thống tên miền." Dịch vụ máy chủ DNS cho phép cập nhật động được kích hoạt hoặc vô hiệu hóa trên một cơ sở cho một khu vực ở mỗi máy chủ được cấu hình để tải một trong hai khu chính hoặc tích hợp thư mục tiêu chuẩn. Theo mặc định, các dịch vụ Windows Server 2003 DNS Client sẽ tự động cập nhật bản ghi tài nguyên máy chủ (A) trong DNS khi cấu hình TCP/IP. Các dịch vụ Windows Server 2003 DNS Server được cấu hình theo mặc định, cho phép chỉ bảo mật cập nhật động. Bạn phải thay đổi cấu hình này nếu bạn sẽ sử dụng Cập nhật động.

**Mô tả giao thức**

RFC 2136 giới thiệu một định dạng mã máy tin nhắn định dạng mới được gọi là bản Cập Nhật. Các thông báo cập nhật có thể thêm và xóa các bản ghi tài nguyên từ một khu vực cụ thể cũng như kiểm tra các điều kiện tiên quyết. Cập nhật là nguyên tử, có nghĩa là, tất cả các điều kiện tiên quyết phải được thỏa mãn hoặc không có hoạt động cập nhật sẽ diễn ra.

Như trong bất kỳ việc thực hiện quy ước DNS, Cập Nhật zone phải được cam kết trên một máy chủ DNS chính cho zone đó. Nếu một bản Cập Nhật được nhận bởi một máy chủ DNS phụ, nó sẽ được chuyển tiếp lên cấu trúc liên kết nhân rộng cho đến khi nó đạt đến các máy chủ DNS chính. Lưu ý rằng trong trường hợp của một zone tích hợp Active Directory, một Cập Nhật cho bản ghi tài nguyên trong một zone có thể được gửi đến bất kỳ máy chủ DNS đang chạy trên một bộ điều khiển zone Active Directory có lưu trữ dữ liệu chứa trong zone.

Một quá trình chuyển giao zone sẽ luôn luôn khóa một zone vì vậy mà một máy chủ DNS phụ học sẽ nhận được một cái nhìn thống nhất zone trong khi chuyển zone dữ liệu. Khi zone bị khóa nó không còn có thể chấp nhận bản Cập Nhật động. Nếu zone lớn và bị khóa thường xuyên cho mục đích chuyển giao các zone, nó sẽ cạn Cập Nhật động khách hàng và hệ thống có thể trở nên không ổn định. Các dịch vụ Windows Server 2003 DNS Server hàng đợi yêu cầu bản cập nhật mà đến trong khi chuyển zone và xử lý chúng sau khi chuyển zone hoàn tất.

**Làm thế nào khách hàng và máy chủ máy tính cập nhật tên DNS của họ**

Theo mặc định, máy vi tính được cấu hình tĩnh TCP/IP cố gắng tự động đăng ký host (A) và bản ghi tài nguyên trỏ (PTR) cho địa chỉ IP được cấu hình và sử dụng kết nối mạng được cài đặt của họ. Tất cả máy tính đăng ký hồ sơ dựa trên tên miền hoàn toàn đủ điều kiện (FQDN).

Các mặc định sau đây cũng áp dụng cho máy tính như thế nào cập nhật tên DNS của họ:

-  Theo mặc định, máy khách DNS trên Windows XP không cố gắng cập nhật động trên một truy cập từ xa hoặc kết nối mạng riêng ảo (VPN). Để thay đổi cấu hình này, bạn có thể sửa đổi các thiết lập TCP / IP tiên tiến của các kết nối mạng cụ thể hoặc chỉnh sửa đăng ký. 

- Theo mặc định, máy khách DNS không cố gắng cập nhật năng động của miền (TLD) zone cấp cao nhất. Bất kỳ zone được đặt tên với một cái tên duy nhất nhãn hiệu được coi là một zone TLD, ví dụ, com, edu, ...

- Theo mặc định, phần hậu tố DNS chính của FQDN của máy tính là giống như tên của miền Active Directory để mà các máy tính được nối. Để cho phép các hậu tố DNS chính khác nhau, một quản trị viên miền có thể tạo ra một danh sách hạn chế các hậu tố cho phép bằng cách thay đổi các thuộc tính msDS-AllowedDNSSuffixes trong container đối tượng miền. Thuộc tính này được quản lý bởi các quản trị viên miền bằng Active Directory dịch vụ giao diện (ADSI) hoặc Lightweight Directory Access Protocol (LDAP).

** Cập nhật động có thể được gửi cho bất kỳ lý do hoặc các sự kiện sau đây: **

- Một địa chỉ IP được bổ sung, loại bỏ, hoặc sửa đổi trong cấu hình thuộc tính TCP / IP cho bất kỳ một trong các kết nối mạng được cài đặt.

- Một địa chỉ IP thay đổi hợp đồng thuê hoặc làm mới với máy chủ DHCP bất kỳ một trong các kết nối mạng được cài đặt. Ví dụ, khi máy tính được khởi động hoặc nếu ipconfig / renew lệnh được sử dụng.

- Lệnh ipconfig /registerdns được sử dụng để tự lực làm mới một khách hàng tên đăng ký trong DNS.

- Lúc khởi động, khi máy tính được bật.

- Một máy chủ thành viên được thăng lên một bộ điều khiển miền.


Khi một trong những sự kiện trước đó gây ra một Cập Nhật động, Dịch vụ DHCP Client (không phải dịch vụ DNS Client) sẽ gửi thông tin Cập Nhật. Điều này được thiết kế để nếu thông tin địa chỉ IP thay đổi xảy ra vì dịch vụ DHCP, bản Cập Nhật tương ứng trong DNS được thực hiện đồng bộ hoá tên địa chỉ ánh xạ cho các máy tính. Dịch vụ DHCP Client thực hiện chức năng này cho tất cả các kết nối mạng được sử dụng trên hệ thống, bao gồm cả kết nối không được cấu hình để sử dụng DHCP.

Quá trình Cập Nhật được mô tả ở trên giả định rằng cài đặt mặc định có hiệu lực đối với máy tính chạy Windows 2000, Windows XP hoặc máy chủ đang chạy Windows Server 2003. Tên cụ thể và bản Cập Nhật là hành vi ứng nơi thuộc tính TCP/IP nâng cao được cấu hình để sử dụng cài đặt DNS-default.

Ngoài tên đầy đủ máy tính (hoặc tên chính) của máy tính, thêm tên DNS kết nối cụ thể có thể được cấu hình và tùy chọn đăng ký hoặc cập nhật trong DNS.

Bản Cập Nhật động được gửi hoặc làm mới theo định kỳ. Theo mặc định, máy tính gửi làm mới một lần mỗi bảy ngày. Nếu việc Cập Nhật kết quả trong không có thay đổi zone dữ liệu, zone vẫn còn ở phiên bản hiện tại của nó và không có thay đổi được viết.

Khi dịch vụ DHCP Client đăng ký tài ghi A và PTR cho một máy tính, nó sử dụng một bộ nhớ đệm thời gian thực mặc định (TTL) là 15 phút cho các hồ sơ lưu trữ. Điều này xác định bao lâu máy chủ DNS và khách hàng khác bộ nhớ cache của máy tính ghi khi họ được bao gồm trong một phản ứng truy vấn.

**DNS và DHCP client và server**

Windows 2000, Windows XP, và Windows Server 2003 DHCP khách hàng là động cập nhật, nhận thức và có thể bắt đầu quá trình cập nhật động. Một khách hàng dịch vụ DHCP sử dụng quá trình Cập Nhật động với máy chủ DHCP khi khách hàng cho thuê một địa chỉ IP hoặc đổi mới thuê, xác định những máy tính Cập Nhật bản ghi tài nguyên A và PTR của khách hàng. Tùy thuộc vào quá trình đàm phán, các khách hàng DHCP, DHCP server, hoặc cả hai, Cập nhật các bản ghi bằng cách gửi các yêu cầu Cập Nhật động đến các máy chủ DNS chính được uỷ quyền cho những cái tên đang được Cập Nhật.

Khách hàng và máy chủ đang chạy phiên bản Windows trước đó hơn so với Windows 2000 không hỗ trợ cập nhật động. Windows 2000 và Windows Server 2003 dịch vụ DHCP Server có thể thực hiện các Cập Nhật động thay mặt cho khách hàng không hỗ trợ tùy chọn FQDN dịch vụ DHCP Client (trong đó được mô tả trong phần sau). Ví dụ: khách hàng đang chạy Microsoft Windows 95, Windows 98 và Windows NT không hỗ trợ tùy chọn FQDN uy nhiên, chức năng này có thể được kích hoạt trong tab DNS của các thuộc tính cho giao diện điều khiển dịch vụ DHCP. Các máy chủ DHCP đầu tiên lấy tên của khách hàng di sản từ các gói tin DHCP REQUEST. sau đó nó gắn thêm tên miền nhất định cho phạm vi đó và đăng kí các tài nguyên ghi A và PTR.

Trong một số trường hợp, cũ PTR hoặc một bản ghi tài nguyên có thể xuất hiện trên các máy chủ DNS khi hợp đồng thuê của một khách hàng DHCP hết hạn. Ví dụ, khi một Windows 2000, Windows XP hoặc Windows Server 2003 DHCP client cố gắng thương lượng một thủ tục cập nhật năng động với một máy chủ Windows NT 4.0 DHCP, DHCP client phải đăng ký cả hai A và tài nguyên ghi PTR chính nó. Sau đó, nếu Windows 2000, Windows XP hoặc Windows Server 2003 DHCP client là không đúng loại bỏ từ mạng, khách hàng không thể xoá đăng ký A và bản ghi tài nguyên PTR và họ trở thành cũ.

Để cung cấp khả năng chịu lỗi cho bản cập nhật động, xem xét việc tích hợp Active Directory cho những zone chấp nhận nâng cấp động từ Windows Server 2003 khách hàng dựa trên mạng. Để tăng tốc độ phát hiện các máy chủ DNS có thẩm quyền, bạn có thể cấu hình mỗi khách hàng với một danh sách các máy chủ DNS ưa thích và thay thế mà là chính cho rằng zone thư mục tích hợp. Nếu khách hàng không cập nhật các zone có máy chủ DNS ưa thích của mình vì các máy chủ DNS không có sẵn, khách hàng có thể thử một máy chủ thay thế. Khi các máy chủ DNS ưa thích trở thành có sẵn, nó tải Cập Nhật, thư mục, tích hợp các zone bao gồm các bản Cập Nhật từ khách hàng.

**Quá trình cập nhật động cho các kết nối mạng được cấu hình DHCP**

 Để bắt đầu quá trình cập nhật năng động, DHCP client gửi FQDN của nó đến máy chủ DHCP trong gói DHCPREQUEST bằng cách sử dụng các dịch vụ DHCP Client FQDN tùy chọn. Các máy chủ DHCP sau đó trả lời cho khách hàng DHCP bằng cách gửi một thông điệp DHCP nhận (DHCPACK) bao gồm các tùy chọn FQDN (tùy chọn mã 81). 

Bảng sau đây liệt kê các trường tùy chọn FQDN của gói DHCPREQUEST. 

**Các trường trong tùy chọn FQDN của gói DHCPREQUEST **

|Trường|Gải thích|
|----------|------------|
|Code| Chỉ định mã cho tùy chọn này (81). |
|Len| Xác định chiều dài, trong octet, các tùy chọn này (tối thiểu là 4). |
|Flags|Có thể là một trong các giá trị sau:|
|| 0 . Khách hàng muốn đăng ký A RR và yêu cầu các máy chủ cập nhật RR PTR.|
|| 1 . Khách hàng muốn máy chủ để đăng ký A và PTR RR.|
|| 3 .  máy chủ DHCP đăng ký A và PTR RR không phụ thuộc vào yêu cầu của khách hàng. |
|RCODE1 and RCODE 2| Các máy chủ DHCP sử dụng các trường để xác định mã phản hồi từ việc đăng ký A và PTR RR thực hiện thay mặt cho khách hàng và để cho biết nó đã cố gắng cập nhật trước khi gửi DHCPACK. |
|Domain Name| Chỉ định FQDN của khách hàng. |


Các điều kiện theo DHCP mà khách hàng gửi cho các tùy chọn FQDN và hành động thực hiện bởi các máy chủ DHCP phụ thuộc vào hệ điều hành máy khách và máy chủ đang chạy và làm thế nào các khách hàng và máy chủ được cấu hình. 

Khách hàng yêu cầu bản Cập Nhật động tùy thuộc vào việc có hay không nó đang chạy hệ điều hành Windows Server 2003, Windows 2000 hoặc trước đó. Nó cũng phụ thuộc vào khách hàng cấu hình. Khách hàng có thể thực hiện bất kỳ hành động sau đây:

- Theo mặc định, các dịch vụ Windows 2000, Windows XP và Windows Server 2003 DHCP Client gửi các tùy chọn FQDN với lĩnh vực cờ đặt là 0 để yêu cầu các khách hàng Cập Nhật bản ghi tài nguyên A, và các dịch vụ DHCP Server Cập Nhật bản ghi tài nguyên PTR. Sau khi khách hàng gửi các tùy chọn FQDN, nó chờ đợi câu trả lời từ máy chủ DHCP. Trừ khi các máy chủ DHCP thiết lập trường Flags đến 3, khách hàng sau đó khởi tạo một bản Cập Nhật cho bản ghi tài nguyên A. Nếu máy chủ DHCP không hỗ trợ hoặc không được cấu hình để thực hiện đăng ký bản ghi DNS, sau đó FQDN không được bao gồm trong các phản ứng máy chủ DHCP và khách hàng cố gắng đăng ký của các bản ghi tài nguyên A và PTR.

- Nếu DHCP client đang chạy một hệ điều hành Windows trước đó hơn so với Windows 2000, hoặc nếu khách hàng là Windows 2000 và nó được cấu hình không phải đăng ký bản ghi tài nguyên DNS, sau đó khách hàng không gửi các tùy chọn FQDN. Trong trường hợp này, khách hàng không cập nhật hoặc kỷ lục.

Tùy thuộc vào những gì mà khách hàng yêu cầu DHCP, máy chủ DHCP có thể có những hành động khác nhau. Nếu DHCP client gửi một thông điệp DHCPREQUEST mà không có sự lựa chọn FQDN, hành vi phụ thuộc vào loại máy chủ DHCP và làm thế nào nó được cấu hình. Các máy chủ DHCP có thể cập nhật cả hai hồ sơ nếu nó được cấu hình để cập nhật hồ sơ thay mặt cho DHCP client không hỗ trợ tùy chọn FQDN.

 Trong các trường hợp sau đây, máy chủ DHCP không thực hiện bất kỳ hành động: 

- Các máy chủ DHCP (ví dụ, một máy chủ đang chạy Windows NT 4.0) không hỗ trợ cập nhật động.

-  Các máy chủ DHCP đang chạy Windows Server 2008 và được cấu hình để không cập nhật động cho khách hàng mà không hỗ trợ tùy chọn FQDN. 

-  Các máy chủ DHCP đang chạy Windows Server 2008 và được cấu hình không phải đăng ký bản ghi tài nguyên DNS. 

Nếu Windows 2000, Windows XP hoặc Windows Server 2003 DHCP yêu cầu của khách hàng dựa trên mạng mà máy chủ cập nhật các bản ghi tài nguyên PTR nhưng không phải là bản ghi tài nguyên, hành vi này phụ thuộc vào loại máy chủ DHCP và làm thế nào nó được cấu hình. Các máy chủ có thể thực hiện bất kỳ hành động sau đây:

- Nếu máy chủ DHCP đang chạy Windows 2000 hoặc hệ điều hành Windows Server 2003 và được cấu hình không thực hiện cập nhật động, phản ứng của nó không chứa các tùy chọn FQDN và không cập nhật hoặc bản ghi tài nguyên. Trong trường hợp này, khách hàng DHCP cố gắng cập nhật cả hai tài nguyên ghi A và PTR, nếu nó có khả năng.


- Nếu DHCP server đang chạy hệ điều hành Windows 2000 hoặc Windows Server 2003 và được cấu hình để cập nhật theo yêu cầu của các khách hàng DHCP, máy chủ cố gắng để Cập Nhật bản ghi tài nguyên PTR. Thông báo DHCPACK máy chủ DHCP cho khách hàng dịch vụ DHCP có tùy chọn FQDN với cờ đặt thành 0, xác nhận rằng máy chủ DHCP Cập nhật hồ sơ PTR. DHCP client sau đó cố gắng để Cập Nhật bản ghi tài nguyên A, nếu nó có khả năng.

Nếu DHCP server đang chạy hệ điều hành Windows 2000 hoặc Windows Server 2003, và là cấu hình để luôn luôn Cập Nhật A và PTR ghi cả hai máy chủ DHCP cố gắng Cập Nhật bản ghi tài nguyên cả. Thông báo DHCPACK máy chủ DHCP cho khách hàng dịch vụ DHCP có tùy chọn FQDN với cờ set 3, thông báo cho khách hàng DHCP rằng các bản cập nhật máy chủ DHCP A và bản ghi PTR. Trong trường hợp này, khách hàng DHCP không cố gắng để cập nhật hoặc bản ghi tài nguyên.

**Quá trình cập nhật động cho khách được cấu hình tĩnh và truy cập từ xa**

khách hàng được cấu hình tĩnh và các khách hàng truy cập từ xa không dựa trên máy chủ DHCP đăng ký DNS. khách hàng được cấu hình tĩnh tự động cập nhật A và tài nguyên PTR ghi lại mỗi khi khởi động và sau đó mỗi 24 giờ trong trường hợp các hồ sơ bị hỏng hoặc cần được làm mới trong cơ sở dữ liệu DNS.

khách hàng truy cập từ xa có thể tự động cập nhật tài nguyên ghi A và PTR khi một kết nối dial-up được thực hiện. Họ cũng có thể cố gắng để thu hồi, hoặc xoá đăng ký, các nguồn tài nguyên bản ghi A và PTR khi người dùng đóng cửa các kết nối một cách rõ ràng. Máy tính chạy Windows 2000 hoặc hệ điều hành Windows Server 2003 với một kết nối mạng truy cập từ xa cố gắng đăng ký động của các bản ghi A và PTR tương ứng với địa chỉ IP của kết nối này. Theo mặc định, các dịch vụ DNS Client trên Windows XP không cố gắng động cập nhật qua một dịch vụ truy cập từ xa (RAS) hoặc kết nối mạng riêng ảo (VPN). Để thay đổi cấu hình này, bạn có thể sửa đổi các thiết lập TCP / IP tiên tiến của các kết nối mạng cụ thể hoặc chỉnh sửa registry.

Trong tất cả các hệ điều hành, nếu một khách hàng truy cập từ xa không nhận được phản hồi thành công từ sự nỗ lực để xoá đăng ký một bản ghi tài nguyên DNS, hoặc nếu vì lý do nào khác không xoá đăng ký một bản ghi tài nguyên trong vòng bốn giây, DNS client đóng kết nối. Trong trường hợp này, cơ sở dữ liệu DNS có thể chứa một bản ghi cũ.

Nếu khách hàng truy cập từ xa không thành công để xoá đăng ký một bản ghi tài nguyên DNS, nó cho biết thêm một tin nhắn để ghi sự kiện, bạn có thể xem bằng cách sử dụng trình xem sự kiện. Khách hàng truy cập từ xa không bao giờ xóa hồ sơ cũ, nhưng các máy chủ truy cập từ xa cố gắng để xoá đăng ký các bản ghi tài nguyên PTR khi khách hàng được ngắt kết nối.

Windows 2000 quay mạng khách hàng cố gắng để đăng ký các bản ghi A và PTR cho kết nối quay số.  Theo mặc định, Windows XP và Windows Server 2003 DNS Client dịch vụ quay số mạng khách hàng cố gắng tự động Cập Nhật bản ghi A và PTR.   Do tính chất kinh doanh của họ, nó là phổ biến rằng các ISP không cho phép Cập Nhật động của thông tin DNS bởi khách hàng của họ. Nếu bạn sử dụng một ISP không hỗ trợ Cập Nhật động, cấu hình các thuộc tính kết nối để ngăn chặn máy tính thực hiện Cập Nhật động.

**Quá trình cập nhật động cho khách hàng multihomed**

Nếu một khách hàng cập nhật động được multihomed (có nhiều hơn một kết nối mạng và địa chỉ IP liên kết), nó đăng ký địa chỉ IP đầu tiên cho mỗi kết nối mạng theo mặc định. Nếu bạn không muốn nó để đăng ký các địa chỉ IP, bạn có thể cấu hình kết nối mạng để không phải đăng ký địa chỉ IP.

Bản cập nhật khách hàng năng động không đăng ký tất cả các địa chỉ IP với các máy chủ DNS trong tất cả các không gian tên mà các máy tính được kết nối với. Ví dụ, một máy tính multihomed, client1.noam.example.com, được kết nối với cả hai mạng Internet và mạng nội bộ của công ty. Client1 được kết nối vào mạng nội bộ của bộ chuyển đổi A, một bộ điều hợp DHCP với địa chỉ IP 172.16.8.7. Client1 cũng được kết nối với Internet bằng bộ chuyển đổi B, một bộ chuyển đổi truy cập từ xa với địa chỉ IP 10.3.3.9. Client1 giải quyết tên mạng nội bộ bằng cách sử dụng một máy chủ tên trên mạng nội bộ, NoamDC1, và giải quyết tên Internet bằng cách sử dụng một máy chủ tên trên Internet, ISPNameServer.

**Thời gian thực**

Bất cứ khi nào một khách hàng Cập Nhật động đăng ký trong DNS, các liên kết tài nguyên A và PTR hồ sơ bao gồm thời gian thực (TTL), mà theo mặc định được thiết lập để 10 phút cho các hồ sơ đăng ký dịch vụ đăng nhập mạng, và 15 phút đối với hồ sơ đăng ký của dịch vụ DHCP Client.  Nếu dịch vụ DNS Server tự động đăng ký hồ sơ cho các zone riêng của mình, mặc định TTL là 20 phút.  Một giá trị nhỏ gây ra các mục nhập được lưu trữ hết hạn sớm hơn, mà làm tăng lưu lượng truy cập DNS, nhưng giảm nguy cơ hồ sơ lưu trữ trở nên lỗi thời. Hết hạn mục một cách nhanh chóng là hữu ích cho các máy tính thường xuyên làm mới DHCP cho thuê của họ. thời gian lưu dài có ích cho các máy tính mới DHCP cho thuê của họ không thường xuyên.

**Giải quyết tên xung đột**

Khi dịch vụ DNS Client cố gắng để đăng ký một bản ghi A và phát hiện ra rằng zone DNS uỷ quyền đã chứa một bản ghi A cho tên tương tự, nhưng với một địa chỉ IP khác nhau, theo mặc định, các dịch vụ DNS Client cố gắng để thay thế các bản ghi hiện có A ( s) với các bản ghi có chứa địa chỉ IP của máy khách DNS.  Kết quả là, bất kỳ máy tính trên mạng có thể thay đổi hiện tại một hồ sơ trừ khi Cập Nhật động an toàn được sử dụng. Các zone được đặt cấu hình cho bảo mật Cập Nhật động cho phép chỉ những người dùng được ủy quyền để sửa đổi các bản ghi tài nguyên.

Bạn có thể thay đổi các thiết lập mặc định để các dịch vụ DNS Client hủy bỏ quá trình đăng ký và bản ghi lỗi trong Event Viewer, thay vì thay thế hiện tại Một kỷ lục.

**Cập nhật động an toàn**

Cập nhật DNS an ninh chỉ có sẵn cho các zone đã được tích hợp vào Active Directory. Một khi bạn được tích hợp Active Directory vào một zone, danh sách điều khiển truy cập (ACL) tính năng chỉnh sửa có sẵn trong giao diện DNS, do đó bạn có thể thêm hoặc loại bỏ người dùng hoặc nhóm từ ACL cho một zone quy định hoặc hồ sơ tài nguyên. ACL là để kiểm soát truy cập quản lý DNS chỉ, và không ảnh hưởng đến độ phân giải truy vấn DNS.

 Theo mặc định, cập nhật động an toàn cho các máy chủ DNS và khách hàng được xử lý như sau: 

- Khách hàng DNS cố gắng sử dụng cập nhật động không có bảo đảm đầu tiên. Nếu một bản cập nhật không có bảo đảm từ chối, khách hàng cố gắng để sử dụng bản cập nhật bảo mật.

 Ngoài ra, khách hàng sử dụng một chính sách Cập Nhật mặc định cho phép họ để cố gắng ghi đè lên một hồ sơ đăng ký trước tài nguyên, trừ khi họ được đặc biệt bị chặn bởi các bản Cập Nhật bảo mật.

- Khi một khu vực trở thành Active Directory tích hợp, máy chủ DNS đang chạy Windows Server 2003 mặc định chỉ cho phép cập nhật động an toàn.

Khi sử dụng lưu trữ zone chuẩn, mặc định cho các dịch vụ DNS Server là không cho phép cập nhật động trên các zone của nó. Đối với các khu hoặc là tích hợp thư mục hoặc sử dụng tiêu chuẩn dựa trên tập tin lưu trữ, bạn có thể thay đổi khu vực để cho phép tất cả các bản Cập Nhật động cho phép tất cả các bản cập nhật để được chấp nhận.

Cập nhật động hoạt động như thế nào

 Quá trình cập nhật an toàn động được mô tả như sau: 

- Để bắt đầu Cập Nhật động an toàn, DNS client lần đầu tiên bắt đầu quá trình đàm phán bối cảnh an ninh, trong đó các thẻ được truyền giữa máy khách và máy chủ bằng cách sử dụng bản ghi tài nguyên TKEY. Ở phần cuối của quá trình đàm phán bối cảnh an ninh được thành lập.


- Tiếp theo, các DNS client gửi yêu cầu cập nhật động (có chứa bản ghi tài nguyên cho mục đích của việc thêm, xóa, hoặc sửa đổi dữ liệu) đến máy chủ DNS, ký sử dụng bối cảnh an ninh được thiết lập trước đó và đi qua các chữ ký trong các bản ghi tài nguyên TSIG, bao gồm các gói cập nhật động.

- Máy chủ cố gắng để cập nhật các hoạt động thư mục bằng cách sử dụng thông tin đăng nhập của khách hàng và gửi kết quả Cập Nhật cho khách hàng. Những kết quả này được ký kết bằng cách sử dụng bối cảnh an ninh và vượt qua chữ ký trong bản ghi tài nguyên TSIG được bao gồm trong các phản ứng.

Đảm bảo quá trình cập nhật năng động

 Quá trình cập nhật an toàn năng động được mô tả như sau: 

1 . DNS client truy vấn máy chủ DNS ưa thích để xác định máy chủ DNS là uỷ quyền cho các tên miền đó là cố gắng để cập nhật. Các máy chủ DNS ưa thích đáp ứng với tên của zone và các máy chủ DNS chính uỷ quyền cho zone.

2 . Các DNS client cố gắng cập nhật động tiêu chuẩn, và nếu zone được cấu hình để cho phép chỉ đảm bảo cập nhật động (cấu hình mặc định cho các zone Active Directory tích hợp), máy chủ DNS từ chối bản cập nhật không an toàn. Có zone được cấu hình cho tiêu chuẩn Cập Nhật động chứ không phải là bảo mật Cập Nhật động, các máy chủ DNS nào đã chấp nhận DNS client cố gắng để thêm, xóa, hoặc sửa đổi bản ghi tài nguyên trong zone đó.


3 . DNS client và DNS server bắt đầu đàm phán TKEY.

4 . Trước tiên, DNS client và DNS server thương lượng một cơ chế bảo mật tiềm ẩn. Windows Cập Nhật động khách hàng và máy chủ DNS có thể chỉ dùng giao thức Kerberos.

5 . Tiếp theo, bằng cách sử dụng cơ chế bảo mật, DNS client và máy chủ DNS xác minh danh tính tương ứng của họ và thiết lập bối cảnh an ninh.

6 . DNS client gửi yêu cầu Cập Nhật động cho các máy chủ DNS, đăng nhập bằng cách sử dụng bối cảnh an ninh được thành lập. Chữ ký được bao gồm trong lĩnh vực chữ ký của các bản ghi tài nguyên TSIG được bao gồm trong các gói Cập Nhật động yêu cầu. Các máy chủ DNS xác minh nguồn gốc của các gói Cập Nhật động bằng cách sử dụng bối cảnh an ninh và chữ ký TSIG.

7 . Các máy chủ DNS cố gắng thêm, xóa hoặc sửa đổi các bản ghi tài nguyên trong Active Directory. Có hay không nó có thể thực hiện các cập nhật tùy thuộc vào liệu DNS client có quyền thích hợp để thực hiện các Cập Nhật và cho dù điều kiện tiên quyết đã được đáp ứng.

8 . Các máy chủ DNS gửi trả lời cho DNS client nêu rõ cho dù có hay không nó đã có thể thực hiện Cập Nhật, đăng nhập bằng cách sử dụng bối cảnh an ninh được thành lập. Chữ ký được bao gồm trong lĩnh vực chữ ký của các bản ghi tài nguyên TSIG được bao gồm trong các gói Cập Nhật động phản ứng. Nếu DNS client sẽ nhận được một thư trả lời gỉa mạo, nó bỏ qua nó và chờ đợi cho một phản ứng đã ký.

**Bảo mật cho ứng dụng khách DHCP không hỗ trợ tùy chọn FQDN**


Khách hàng Windows DHCP không hỗ trợ tùy chọn FQDN (tùy chọn 81)  không có khả năng cập nhật động. Nếu bạn muốn tài nguyên ghi A và PTR cho các khách hàng tự động đăng ký trong DNS, bạn phải cấu hình máy chủ DHCP để thực hiện nâng cấp động thay mặt họ.

Tuy nhiên, có máy chủ DHCP để thực hiện cập nhật an toàn năng động thay mặt cho khách hàng DHCP mà không hỗ trợ tùy chọn FQDN là không mong muốn bởi vì khi một máy chủ DHCP thực hiện một cập nhật động bảo mật trên một cái tên, mà máy chủ DHCP sẽ trở thành chủ sở hữu của tên đó, và chỉ có máy chủ DHCP có thể cập nhật bất cứ hồ sơ cho tên đó. Điều này có thể gây ra các vấn đề trong một vài hoàn cảnh khác nhau.

Để giải quyết vấn đề này, nhóm được xây dựng trong bảo mật được gọi là DnsUpdateProxy được cung cấp. Nếu tất cả các máy chủ DHCP được thêm vào như là thành viên của nhóm DnsUpdateProxy, một bản ghi máy chủ có thể được Cập Nhật bởi một máy chủ, nếu máy chủ đầu tiên không thành công. Ngoài ra, bởi vì tất cả các đối tượng được tạo bởi các thành viên của nhóm DnsUpdateProxy không bảo đảm, người sử dụng đầu tiên (mà không phải là thành viên của nhóm DnsUpdateProxy) để sửa đổi các thiết lập của các hồ sơ liên quan đến DNS tên trở thành chủ nhân của nó. Khi khách hàng cũ được nâng cấp, họ có thể do đó mất quyền sở hữu của tên hồ sơ của họ tại các máy chủ DNS. Nếu mỗi máy chủ DHCP, đăng ký các bản ghi tài nguyên cho các khách hàng lớn là thành viên của nhóm DnsUpdateProxy, các vấn đề thảo luận trước đó được loại bỏ.

Bảo mật hồ sơ khi sử dụng nhóm DNSUpdateProxy

tên miền DNS được đăng ký bởi các máy chủ DHCP không an toàn khi máy chủ DHCP là một thành viên của nhóm DNSUpdateProxy. Kết quả là, không sử dụng nhóm này trong một Active Directory tích hợp zone mà chỉ cho phép đảm bảo cập nhật động mà không cần dùng các bước bổ sung để cho phép ghi được tạo ra bởi các thành viên của nhóm phải được bảo đảm.

Để bảo vệ chống lại các hồ sơ không có bảo đảm, hoặc cho phép thành viên của nhóm DNSUpdateProxy đăng ký hồ sơ tại các zone mà chỉ cho phép bảo đảm cập nhật năng động, Windows Server 2003 DHCP và DNS cho phép bạn tạo một tài khoản người dùng chuyên dụng và cấu hình máy chủ DHCP để thực hiện DNS động cập nhật với các thông tin tài khoản người dùng (tên người dùng, mật khẩu và tên miền). Các thông tin của một tài khoản người dùng chuyên dụng có thể được sử dụng bởi nhiều máy chủ DHCP.

Tài khoản người dùng chuyên dụng là một tài khoản người dùng chuẩn được sử dụng chỉ được cung cấp các máy chủ DHCP với các thông tin cho DNS đăng ký cập nhật động. Mỗi máy chủ DHCP cung cấp những thông tin khi đăng ký tên thay mặt cho khách hàng sử dụng DHCP DNS cập nhật động. Tài khoản người dùng chuyên dụng được tạo ra trong rừng cùng một nơi mà các máy chủ DNS chính cho zone phải được cập nhật thường trú. Tài khoản người dùng chuyên dụng cũng có thể được đặt trong rừng khác miễn là rừng nó cư trú trong có một sự tin tưởng rừng thành lập với diện tích rừng có máy chủ DNS chính cho zone được cập nhật.

Khi cài đặt trên một bộ điều khiển tên miền, dịch vụ DHCP Server được thừa hưởng các khoản bảo mật của bộ điều khiển tên miền và có quyền cập nhật hoặc xóa bất kỳ bản ghi DNS được đăng ký tại một vùng Active Directory tích hợp an toàn (kể cả hồ sơ được đăng ký một cách an toàn bằng cách máy tính đang chạy Windows 2000 hoặc Windows server 2003, bao gồm các bộ điều khiển miền). Khi cài đặt trên một bộ điều khiển tên miền, cấu hình máy chủ DHCP với các thông tin của tài khoản người dùng chuyên dụng để ngăn chặn các máy chủ từ thừa kế, và có thể lợi dụng, sức mạnh của các bộ điều khiển miền.

 Cấu hình một tài khoản người dùng chuyên dụng và cấu hình dịch vụ DHCP Server với các thông tin tài khoản trong các trường hợp sau đây: 

-  Một bộ điều khiển miền được cấu hình để hoạt động như một máy chủ DHCP. 

-  Các máy chủ DHCP được cấu hình để thực hiện DNS cập nhật động thay mặt cho khách hàng DHCP. 

-  Các zone DNS được cập nhật bởi các máy chủ DHCP được cấu hình để cho phép chỉ đảm bảo cập nhật động. 

**Kiểm soát cập nhật truy cập vào zone và tên**

Danh sách kiểm soát truy cập truy cập vào các zone DNS và ghi tài nguyên được lưu trữ trong Active Directory được kiểm soát (ACL). ACL có thể được chỉ định cho các dịch vụ DNS Server, một zone toàn bộ hoặc cho các tên DNS cụ thể. Theo mặc định, bất kỳ người sử dụng Active Directory xác thực có thể tạo ra các bản ghi A hoặc nguồn PTR trong khu vực bất kỳ. Khi một tên chủ sở hữu đã được tạo ra cho một zone (không phân biệt các loại hồ sơ tài nguyên), chỉ có người dùng hoặc nhóm quy định trong ACL cho tên đó có quyền ghi được kích hoạt để sửa đổi hồ sơ tương ứng với tên đó. Trong khi cách tiếp cận này là mong muốn trong hầu hết các tình huống, một số trường hợp đặc biệt cần phải được xem xét riêng biệt.

**Nhóm DNSAdmins**

Theo mặc định, các nhóm DNSAdmins đã kiểm soát đầy đủ của tất cả các zone và các bản ghi trong Server 2003 miền Windows, trong đó nó được chỉ định. Để cho một người sử dụng để có thể liệt kê các zone trong một miền Windows Server 2003 cụ thể, người sử dụng (hoặc thuộc một nhóm người sử dụng) phải được gia nhập vào nhóm DNSAdmin.

Có thể là một quản trị viên miền có thể không muốn cấp kiểm soát đầy đủ cho tất cả các người dùng được liệt kê trong nhóm DNSAdmins. Thông thường, điều này sẽ là kết quả nếu người quản trị domain muốn cấp quyền kiểm soát đầy đủ cho một zone cụ thể và chỉ đọc kiểm soát đối với các zone khác trong miền đến một tập người dùng. Để thực hiện điều này, các quản trị viên miền có thể tạo một nhóm riêng biệt cho từng zone, và thêm người dùng cụ thể cho từng nhóm. Sau đó, ACL cho từng zone sẽ chứa một nhóm với đầy đủ chỉ zone đó. Đồng thời, tất cả các nhóm sẽ được bao gồm trong nhóm DNSAdmins, mà có thể được cấu hình để chỉ có quyền đọc. Như một kết quả của thực tế là ACL của một zone luôn chứa nhóm DNSAdmins, tất cả người dùng gia nhập vào nhóm zone cụ thể sẽ có quyền đọc cho tất cả các zone trong miền.

**Đặt tên**

Cấu hình dịch vụ DNS Server mặc định cho phép bất kỳ người dùng xác thực để tạo ra một cái tên mới trong một zone có thể không đủ cho môi trường đòi hỏi một mức độ bảo mật cao. Trong trường hợp như vậy, các ACL mặc định có thể được thay đổi để cho phép tạo ra các đối tượng trong một zone của một số nhóm hoặc chỉ người dùng. Để thực hiện việc này, người quản trị tạo ra một hồ sơ cho tên dành riêng và bộ thích hợp danh sách các nhóm hoặc người dùng trong ACL. Kết quả là, chỉ người dùng được liệt kê trong ACL sẽ có thể đăng ký một bản ghi với tên dành riêng.

<a name="5"></a>
#5.Understanding Aging and Scavenging

