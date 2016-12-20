## DNS Protocol


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **20/12/2016**

### Mục lục

[1.Giới thiệu](#1)

[2.DNS Namespace](#2)

[3. Nameserver và Zone](#3)

[4.DNS Resolvers](#4)

[5.DNS Resource recore](#5)

[6.Recursion Query và Iteration Query](#6)

[7.DNS hoạt động như thế nào?](#7)

---

<a name="1"></a>
#1.Giới thiệu

DNS (viết tắt trong tiếng Anh của Domain Name System - Hệ thống tên miền) là hệ thống xác định địa chỉ cho Internet. Hầu như bất kỳ thứ gì tương tác với Internet (ví dụ: máy tính, thiết bị di động, máy tính xách tay, máy ATM và thiết bị đầu cuối POS) đều dựa vào các dịch vụ DNS để trao đổi thông tin. DNS sử dụng các máy chủ chuyên biệt để dịch (hoặc phân giải) các tên như www.example.com thành địa chỉ dạng số cho phép dữ liệu và thông tin đến được đích của nó. Tất cả các ứng dụng Internet—từ trang web, email, mạng xã hội và ngân hàng trực tuyến đến Voice over Internet Protocol (VoIP), chia sẻ tập tin, và video theo yêu cầu—đều phụ thuộc vào tính chính xác và toàn vẹn của bản dịch này. Nếu không có DNS, Internet không thể hoạt động. DNS không thể thiếu trong cơ sở hạ tầng quan trọng của một quốc gia, các hoạt động kinh doanh trực tuyến và các giao dịch tài chính, và tất cả giao tiếp dựa trên Internet.

<p align="center"><img src="http://bizweb.dktcdn.net/100/104/592/articles/2014824234257497.jpg?v=1468215019213" /></p>

Mỗi máy tính, thiết bị mạng tham gia vào mạng Internet đều giao tiếp với nhau bằng địa chỉ IP (Internet Protocol) . Để thuận tiện cho việc sử dụng và dễ nhớ ta dùng tên (domain name) để xác định thiết bị đó. Hệ thống tên miền DNS (Domain Name System) được sử dụng để ánh xạ tên miền thành địa chỉ IP. Vì vậy, khi muốn liên hệ tới các máy, chúng chỉ cần sử dụng chuỗi ký tự dễ nhớ (domain name) như: http://www.microsoft.com, http://www.ibm.com…, thay vì sử dụng địa chỉ IP là một dãy số dài khó nhớ.

Ban đầu, khi DNS chưa ra đời, người ta sử dụng một file tên Host.txt, file này sẽ lưu thông tin về tên host và địa chỉ của host của tất cả các máy trong mạng, file này được lưu ở tất cả các máy để chúng có thể truy xuất đến máy khác trong mạng. Khi đó, nếu có bất kỳ sự thay đổi về tên host, địa chỉ IP của host thì ta phải cập nhật lại toàn bộ các file Host.txt trên tất cả các máy. Do vậy đến năm 1984 Paul Mockpetris thuộc viện USC’s Information Sciences Institute phát triển một hệ thống quản lý tên miền mới lấy tên là Hệ thống tên miền – Domain Name .

Hệ thống tên miền này cũng sữ dụng một file tên host.txt, lưu thông tịn của tất cả các máy trong mạng, nhưng chỉ được đặt trên máy làm máy chủ tên miền (DNS). Khi đó, các Client trong mạng muốn truy xuất đến các Client khác, thì nó chỉ việc hỏi DNS.


<a name="2"></a>
#2.DNS Namespace

Một domain namespace sẽ chứa một "cây" các domain names. Mỗi node trong cây sẽ giữ thông tin đại diện cho domain name. Mỗi một tổ chức có thể tạo riêng cho mình một domain namespace để tự quản lý các host trong mạng của họ. Trong một domain thì tên dành cho một host là duy nhất, ko thể trùng với nhau đc.

<p align="center"><img src="https://duongtuanan.files.wordpress.com/2012/10/103012_1354_domainnames2.png?w=604" /></p>

Hệ thống tên miền được phân thành nhiêu cấp :

-    Gốc (Domain root): Nó là đỉnh của nhánh cây của tên miền. Nó có thể biểu diễn đơn giản chỉ là dấu chấm “.”

-    Tên miền cấp một (Top-level-domain) : gồm vài kí tự xác định một nước, khu vưc hoặc tổ chức. Nó đươc thể hiện là “.com” , “.edu” ….

-    Tên miền cấp hai (Second-level-domain): Nó rất đa dạng rất đa dạng có thể là tên một công ty, một tổ chức hay một cá nhân.

-    Tên miền cấp nhỏ hơn (Subdomain): Chia thêm ra của tên miền cấp hai trở xuống thường được sử dụng như chi nhánh, phòng ban của một cơ quan hay chủ đề nào đó.

Phân loại tên miền:

- Com     :    Tên miền này được dùng cho các tổ chức thương mại.

- Edu     :    Tên miền này được dùng cho các cơ quan giáo dục, trường học.

- Net     :    Tên miền này được dùng cho các tổ chức mạng lớn.

- Gov     :    Tên miền này được dùng cho các tổ chức chính phủ.

- Org     :    Tên miền này được dùng cho các tổ chức khác.

- Int     :    Tên miền này dùng cho các tổ chức quốc tế.

- Info    :    Tên miền này dùng cho việc phục vụ thông tin.

- Arpa     :     Tên miền ngược.

- Mil     :    Tên miền dành cho các tổ chức quân sự, quốc phòng.

- Mã các nước trên thế giới tham gia vào mạng internet, các quốc gia này được qui định bằng hai chữ cái theo tiêu chuẩn ISO-3166 .Ví dụ : Việt Nam là .vn, Singapo là sg….


<a name="3"></a>
#3.Nameserver và Zone 

Các chương trình lưu trữu toàn bộ thông tin về domain namespace gọi là nameserver. Nameserver thông thường sẽ có thông tin hoàn chỉnh về một phần nào đó của domain namespace gọi là zone, zone này load từ file hoặc từ nameserver khác.

<p align="center"><img src="https://www.nap.edu/openbook/0309096405/xhtml/images/p2000d132g89001.jpg" /></p>

Hình trên cho ta thấy một domain edu đc chia ra thành nhiều zone. Mỗi zone lại đc phân quyền quản lý riêng.

Có 2 kiểu nameserver: primary master và secondary master.
   
-    Primary: chứa tất cả các thông tin cho domain
   
-    Secondary: hoạt động dự phòng, đề phòng trường hợp  Primary fail.

Qúa trình Primary gửi bản sao của nó đến Secondary gọi là zone transfer.



<a name="4"></a>
#4.DNS Resolvers

Là các clients truy cập vào nameservers. Các chương trình chạy host nếu cần thông tin từ domain namespace sẽ sử dụng resolver.

Resolver quản lý:

- Truy vấn nameserver

- Quản lý các trả lời từ nameserver

- Trả thông tin về cho chương trình yêu cầu

<a name="5"></a>
#5.DNS Resource recore

Dữ liệu ứng với domain names đc chứa trong các resource record- bản ghi. Các records đc chia thành các classes, mỗi class chứa các types(kiểu) chịu trách nhiệm phân giải cho từng dịch vụ trong namespace. Các class khác nhau có thể định nghĩa các kiểu record khác nhau. Một số RRs thông dụng:


- Start of Authority (SOA) resource record: định nghĩa các tham số toàn cục cho zone hoặc tên miền. Một tệp tin zone chỉ được phép chứa một mẩu tin SOA và phải nằm ở vị trí đầu tiên trước các mẩu tin khác.

- Name server (NS) resource record: chỉ ra Máy chủ tên miền (Name server) của zone đó.

- A Resource Records (mẩu tin địa chỉ): mẩu tin cho biết địa chỉ IP tương ứng của một tên miền, có dạng như "example IN A 172.16.48.1"

- PTR Records (mẩu tin con trỏ): ngược lại với A record, PTR chỉ ra tên miền tương ứng của một địa chỉ IP, có dạng như "1.48.16.172.in-addr.arpa. IN PTR example.com."

- CNAME Resource Records: một dạng record giúp tạo ra biệt hiệu cho một tên miền, ví dụ mẩu tin CNAME "ftp.example.com. IN CNAME ftp1.example.com." cho phép trỏ tên miền ftp.example.com sang ftp1.example.com

- MX Resource Records (mẩu tin Mail exchange): chỉ ra máy chủ mail của tên miền.

- TXT Resource Records (mẩu tin text): chứa thông tin dạng văn bản không định dạng, thường dùng để chứa các thông tin bổ sung.

Tất cả các DNS Resource Records dựa theo tiêu chuẩn RFC 1035 khi vận chuyển trên Internet:

<p align="center"><strong>Trường Resource recore (RR)</strong></p>

|Trường|Mô tả|Độ dài (octets)|
|----------|---------|--------------------|
|NAME|Tên của nốt có record liên quan|Variable|
|TYPE|Loại RR dạng số (ví dụ, 15 trong MX RRs)|2|
|CLASS|Mã lớp|2|
|TTL|Thời gian theo giây để RR còn hiệu lực (Tối đa 231−1, khoảng 68 năm)|4|
|RDLENGTH|Độ dài trường RDATA|2|
|RDATA|RR bổ sung|Biến đổi, như RDLENGTH|


<a name="6"></a>
#6.Recursion Query và Iteration Query 

Khi DNS Server không phân giải được host name, nó sẽ chuyển đến một DNS Server khác (forwarded) trong mạng. Quá trình này được gọi là kiểu yêu cầu Recursive ( phân giải đệ quy).

Nếu Recursion bị disable thì nó sẽ sử dụng Iterative (tương tác), tức là nó sẽ gởi yêu cầu phân giải lại tên của host name. Khi có một truy vấn từ Client, trước hết nó sẽ tìm trong cơ sở dữ liệu của chính nó, nếu không có, nó sẽ cho biết một máy chủ khác mà từ đó có thể tìm thấy kết quả truy vấn.

Nói cách khác, Recursion chỉ query trong local, còn Iterative có thể query ra ngoài internet.

<p align="center"><img src="https://www.safaribooksonline.com/library/view/windows-server-2012/9780133116007/graphics/10fig11.jpg" /></p>


<a name="7"></a>
#7.DNS hoạt động như thế nào 

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task36_DNS_Protocol/Images/3.png"/></p>



**Bước 1:**  Bạn nhập một tên miền hay địa chỉ web, chẳng hạn như 
www.example.com, vào trình duyệt. Việc trình duyệt của bạn làm là gửi một thông điệp tới mạng yêu cầu giúp đỡ (điều này được gọi là truy vấn).

**Bước 2:** Máy tính của bạn truy vấn (liên hệ) một trong những máy mà ISP cung cấp cho máy tính của bạn, gọi là máy phân giải đệ quy, có địa chỉ IP được lưu trữ trên bộ nhớ đệm, hoặc có thể đi ra ngoài và tìm địa chỉ theo cách “đệ  quy ”.

**Bước 3:** Nếu các máy phân giải đệ quy của ISP không có địa chỉ, chúng sẽ truy vấn các máy chủ tên gốc DNS để tìm địa chỉ  IP.

**Bước 4:** Các máy chủ tên gốc chuyển hướng (hay “giới thiệu”) máy phân giải đệ quy của ISP đến các máy chủ tên TLD thích hợp bằng cách kiểm tra tên miền cấp cao.

**Bước 5:** Mỗi TLD có tập hợp máy chủ tên của riêng mình, và sau khi máy phân giải hỏi chúng về địa chỉ IP, chúng giới thiệu nó tới một tập hợp các máy chủ DNS có thẩm quyền khác (thích hợp hơn) bằng cách xem xét tên miền cấp hai của truy vấn.

**Bước 6:** Máy phân giải đệ quy của ISP sau đó truy vấn các máy chủ tên DNS có thẩm quyền mà nó được giới thiệu để tìm địa chỉ IP.   Mỗi miền có một tập hợp được gán gồm các máy chủ tên DNS có thẩm quyền chịu trách nhiệm biết tất cả mọi thứ về miền, bao gồm địa chỉ   IP.

**Bước 7:** Máy phân giải đệ quy của ISP truy xuất bản ghi A (là bản ghi DNS để ánh xạ các địa chỉ IP) cho www.example.com từ các máy chủ tên có thẩm quyền và lưu trữ bản ghi trong bộ nhớ đệm cục bộ của nó phòng trường hợp người khác truy vấn địa chỉ đó.

**Bước 8:** Cuối cùng, máy chủ đệ quy của ISP trả về bản ghi A đến máy tính của bạn, máy tính của bạn sẽ đọc và chuyển tiếp địa chỉ IP đến trình duyệt của bạn. Sau đó trình duyệt mở một kết nối đến www.example.com. Toàn bộ quá trình thường diễn ra trong mấy phần mười giây và minh bạch với người dùng cuối.

 Ví dụ trình phân giải tên miền :

-    Giả sử người sử dụng muốn truy cập vào trang web có địa chỉ là http://www.google.com

-    Trước hết chương trình trên máy người sử dụng gửi yêu cầu tìm kiếm địa chỉ IP ứng với tên miền http://www.google.com tới máy chủ quản lý tên miền (name Server) cục bộ thuộc mạng của nó (ISP DNS Server).

-    Máy chủ tên miền cục bộ này kiểm tra trong cơ sở dữ liệu của nó có chứa cơ sở dữ liệu chuyển đổi từ tên miền sang địa chỉ IP của tên miền mà người sử dụng yêu cầu không. Trong trường hợp máy chủ tên miền cục bộ có cơ sở dữ liệu này, nó sẽ gửi trả lại địa chỉ IP của máy có tên miền nói trên (www.google.com)

-    Trong trường hợp máy chủ tên miền cục bộ không có cơ sở dữ liệu về tên miền này nó thường hỏi lên các máy chủ tên miền ở cấp cao nhất (máy chủ tên miền làm việc ở mức Root). Máy chủ tên miền ở mức Root này sẽ trả về cho máy chủ tên miền cục bộ địa chỉ của máy chủ tên miền quản lý các tên miền có đuôi .com.

-    Máy chủ tên miền cục bộ gửi yêu cầu đến máy chủ quản lý tên miền có đuôi (.com) tìm tên miền http://www.google.com. Máy chủ tên miền quản lý các tên miền .com sẽ gửi lại địa chỉ của máy chủ quản lý tên miền google.com.

-    Máy chủ tên miền cục bộ sẽ hỏi máy chủ quản lý tên miền google.com này địa chỉ IP của tên miền http://www.google.com. Do máy chủ quản lý tên miền google.com có cơ sở dữ liệu về tên miền http://www.google.com nên địa chỉ IP của tên miền này sẽ được gửi trả lại cho máy chủ tên miền cục bộ.

-    Máy chủ tên miền cục bộ chuyển thông tin tìm được đến máy của người sử dụng.

-    PC của người dùng sẽ sử dụng địa chỉ IP này để mở một phiên kết nối TCP/IP đến Server chứa trang web có địa chỉ http://www.google.com


