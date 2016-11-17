<p align="center" ><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Gentoo_Linux/Images/1.png" /></p>

[1 Introduction](#1)

 :  [1.1 Welcome](#11)
    
 :  [1.2 How is the installation structured](#12)
    
 :  [1.3 What are the options](#13)
    
 :  [1.4 Troubles](#14)

[2 Hardware requirements](#2)

[3 Gentoo Linux installation CD](#3)

 :  [3.1 Minimal installation CD](#31)
    
 :  [3.2 The occasional Gentoo LiveDVD](#32)
    
 :  [3.3 What are stages then?](#33)

---

<a name="1"></a>
#1. Introduce

###1.1 Welcome

Trước hết, chào mừng bạn đến Gentoo. Bạn đang bước vào thế giới của sự lựa chọn và hiệu suất. Gentoo là sự lựa chọn. Khi cài đặt Gentoo, điều này được thể hiện rõ nhiều lần - Người sử dụng có thể chọn bao nhiêu họ muốn biên dịch bản thân, làm thế nào để cài đặt Gentoo, những gì logger hệ thống để sử dụng, vv

Gentoo thif nhanh,  meta phân phối hiện đại với một thiết kế sạch sẽ và linh hoạt. Gentoo được xây dựng xung quanh các phần mềm miễn phí và không che giấu đối với người sử dụng. Portage, hệ thống bảo trì gói mà Gentoo sử dụng, được viết bằng Python, có nghĩa là người dùng có thể dễ dàng xem và chỉnh sửa mã nguồn. Hệ thống đóng gói Gentoo sử dụng mã nguồn (mặc dù hỗ trợ cho các gói có sẵn trong biên dịch ) và cấu hình Gentoo xảy ra thông qua các tập tin văn bản thông thường. Nói cách khác, được mở ở khắp mọi nơi.

Nó là rất quan trọng mà mọi người đều hiểu rằng sự lựa chọn là những gì làm cho Gentoo chạy. Chúng tôi cố gắng không buộc người dùng vào bất cứ điều gì họ không thích. Nếu bất cứ ai tin mặt khác,  xin vui lòng báo lỗi.


<a name="12"></a>
###1.2 How is the installation structured

Cài đặt Gentoo có thể được xem như là một thủ tục 10 bước, tương ứng với các tập tiếp theo của chương. Kết quả mỗi bước trong một trạng thái nhất định:

Step|Result 
-----|-------
1|Người sử dụng trong một môi trường làm việc đã sẵn sàng để cài đặt Gentoo
2|Kết nối Internet đã sẵn sàng để cài đặt Gentoo.
3|Các ổ đĩa cứng được tạo để lưu trữ các cài đặt Gentoo.
4|Môi trường cài đặt sẵn và người dùng đã sẵn sàng để chroot vào môi trường mới.
5|Gói Core, gói mà như nhau trên tất cả các cài đặt Gentoo, được cài đặt.
6|Linux kernel được cài đặt
7|Người dùng sẽ cấu hình hầu hết các tập tin cấu hình hệ thống Gentoo.
8|Các công cụ hệ thống cần thiết được cài đặt.
9|Bộ nạp khởi động thích hợp đã được cài đặt và cấu hình.
10|Môi trường Gentoo Linux mới cài đặt đã sẵn sàng để khám phá.


Bất cứ khi nào một sự lựa chọn nhất định được trình bày trong cuốn cẩm nang sẽ cố gắng giải thích những ưu và khuyết điểm của từng lựa chọn. Mặc dù các văn bản sau đó tiếp tục với lựa chọn mặc định (được xác định bởi "Default:" trong tiêu đề), các khả năng khác sẽ được ghi nhận là tốt (đánh dấu bằng "Alternative:" trong tiêu đề). Đừng nghĩ rằng, mặc định là Gentoo khuyến cáo. Tuy nhiên nó là do Gentoo tin rằng đa số người dùng sẽ sử dụng.

Đôi khi một bước tùy chọn có thể được theo sau. Bước này được đánh dấu là "Option:" và do đó không cần thiết để cài đặt Gentoo. Tuy nhiên, một số bước tùy chọn phụ thuộc vào quyết định thực hiện trước đó. Các hướng dẫn sẽ thông báo cho người đọc khi điều này xảy ra, cả hai quyết định đã được thực hiện, và ngay trước khi bước tùy chọn được mô tả.


<a name="13"></a>
###1.3 What are the options

Gentoo có thể được cài đặt bằng nhiều cách khác nhau. Nó có thể được tải về và cài đặt từ một đĩa CD cài đặt Gentoo, từ một phân phối đã được cài đặt, từ một đĩa CD khởi động không Gentoo (như Knoppix), từ một môi trường khởi động từ mạng, từ đĩa mềm , vv

This document covers the installation using a Gentoo Installation CD or, in certain cases, netbooting. 

```
Note:
Để được trợ giúp về phương pháp cài đặt khác, bao gồm không sử dụng đĩa CD Gentoo, vui lòng đọc hướng dẫn cài đặt thay thế của chúng tôi.
```

Chúng tôi cũng cung cấp lời khuyên cài đặt Gentoo và tài liệu thủ thuật cài đặt mà có thể là hữu ích để đọc.

<a name="14"></a>
###1.4 Troubles

Nếu một vấn đề được tìm thấy trong quá trình cài đặt (hoặc trong các tài liệu hướng dẫn cài đặt), vui lòng truy cập hệ thống theo dõi lỗi của chúng tôi và kiểm tra nếu lỗi được biết đến. Nếu không, hãy tạo ra một báo cáo lỗi cho nó vì vậy chúng tôi có thể chăm sóc nó. Đừng ngại nói với các nhà phát triển - họ (nói chung) không ăn thịt người :))

Lưu ý rằng, mặc dù tài liệu này là kiến trúc cụ thể, nó có thể chứa tài liệu tham khảo để các kiến trúc khác là tốt. Điều này là do thực tế là phần lớn các mã nguồn sử dụng Cẩm nang Gentoo đó là chung cho tất cả các kiến trúc (để tránh trùng lặp của các nỗ lực và thiếu tài nguyên phát triển). Chúng tôi sẽ cố gắng giữ  đến mức tối thiểu để tránh nhầm lẫn.


<a name="2"></a>
#2. Hardware requirements

Trước khi chúng tôi bắt đầu, đầu tiên chúng tôi liệt kê những yêu cầu phần cứng cần thiết để cài đặt Gentoo vào một amd64.

------|Minimal CD|LiveDVD
------------|----------|--------            
CPU| 	Any AMD64 CPU or EM64T CPU (Core 2 Duo & Quad processors are EM64T)|
Memory|256 MB|512 MB
Disk space|2.5 GB (excluding swap space)|
Swap space|At least 256 MB| 


<a name="3"></a>
#3. Gentoo Linux installation CD

###3.1 Minimal installation CD

Gentoo minimal íntallation CD là một CD khởi động chứa sự tự duy trì môi trường Gentoo. Nó cho phép người sử dụng để khởi động Linux từ đĩa CD. Trong quá trình khởi động của phần cứng được phát hiện và điều khiển thích hợp được nạp. CD này được duy trì bởi các nhà phát triển Gentoo và cho phép bất cứ ai để cài đặt Gentoo nếu một kết nối Internet đang hoạt động có sẵn.

###3.2 The occasional Gentoo LiveDVD

Thỉnh thoảng, một DVD đặc biệt được chế tác bởi dự án Gentoo Ten mà có thể được sử dụng để cài đặt Gentoo. Các hướng dẫn tiếp tục xuống chương này nhắm vào đĩa CD mininal installation có thể là một chút khác nhau. Tuy nhiên, các LiveDVD (hoặc bất kỳ môi trường Linux khởi động khác) hỗ trợ nhận được một dấu nhắc root bằng cách chỉ cần gọi ```sudo su -``` hoặc ```sudo -i``` trong terminal.

###3.3 What are stages then?

Một stage3 là một kho lưu trữ có chứa một môi trường minimal Gentoo, thích hợp để tiếp tục cài đặt Gentoo sử dụng các hướng dẫn trong sách hướng dẫn này. Trước đây, Cẩm nang Gentoo mô tả việc cài đặt bằng một trong ba stage tarball. Trong khi Gentoo vẫn cung cấp stage1 và stage2 tarball, phương pháp cài đặt chính thức sử dụng stage3.

Tarball stage3 có thể được tải về từ releases / amd64 / autobuilds / trên bất kỳ website chính thức Gentoo.Ttập tin stage cập nhật thường xuyên và không nằm trên đĩa CD cài đặt.

