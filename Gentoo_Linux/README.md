<p align="center" ><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Gentoo_Linux/Images/1.png" /></p>

[1 Giới thiệu](#1)

- [1.1 Mở đầu](#11)
    
- [1.2 Làm sao để cài đặt](#12)
    
- [1.3 Các lựa chọn là gì](#13)
    
- [1.4 Một số vấn đề](#14)

[2 Yêu cầu Harware](#2)

[3 Cài CD Gentoo Linux](#3)

- [3.1 CD cài đặt tối thiểu](#31)
    
- [3.2 Gentoo LiveDVD](#32)
    
- [3.3 Giai đoạn sau đó là gì?](#33)

[4. Tải và Burning CD](#4)

[5. Booting CD](#5)

- [5.1 khởi động trình cài đặt](#51)



---

<a name="1"></a>
#1. Giới thiệu


<a name="11"></a>
###1.1 Mở đầu

Trước hết, chào mừng bạn đến Gentoo. Bạn đang bước vào thế giới của sự lựa chọn và hiệu suất. Gentoo là sự lựa chọn. Khi cài đặt Gentoo, điều này được thể hiện rõ nhiều lần - Người sử dụng có thể chọn bao nhiêu họ muốn biên dịch bản thân, làm thế nào để cài đặt Gentoo, những gì logger hệ thống để sử dụng, vv

Gentoo thif nhanh,  meta phân phối hiện đại với một thiết kế sạch sẽ và linh hoạt. Gentoo được xây dựng xung quanh các phần mềm miễn phí và không che giấu đối với người sử dụng. Portage, hệ thống bảo trì gói mà Gentoo sử dụng, được viết bằng Python, có nghĩa là người dùng có thể dễ dàng xem và chỉnh sửa mã nguồn. Hệ thống đóng gói Gentoo sử dụng mã nguồn (mặc dù hỗ trợ cho các gói có sẵn trong biên dịch ) và cấu hình Gentoo xảy ra thông qua các tập tin văn bản thông thường. Nói cách khác, được mở ở khắp mọi nơi.

Nó là rất quan trọng mà mọi người đều hiểu rằng sự lựa chọn là những gì làm cho Gentoo chạy. Chúng tôi cố gắng không buộc người dùng vào bất cứ điều gì họ không thích. Nếu bất cứ ai tin mặt khác,  xin vui lòng báo lỗi.


<a name="12"></a>
###1.2 Làm sao để cài đặt

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
###1.3 Các lựa chọn là gì?

Gentoo có thể được cài đặt bằng nhiều cách khác nhau. Nó có thể được tải về và cài đặt từ một đĩa CD cài đặt Gentoo, từ một phân phối đã được cài đặt, từ một đĩa CD khởi động không Gentoo (như Knoppix), từ một môi trường khởi động từ mạng, từ đĩa mềm , vv

This document covers the installation using a Gentoo Installation CD or, in certain cases, netbooting. 

```
Note:
Để được trợ giúp về phương pháp cài đặt khác, bao gồm không sử dụng đĩa CD Gentoo, vui lòng đọc hướng dẫn cài đặt thay thế của chúng tôi.
```

Chúng tôi cũng cung cấp lời khuyên cài đặt Gentoo và tài liệu thủ thuật cài đặt mà có thể là hữu ích để đọc.

<a name="14"></a>
###1.4 Một sô vấn đề

Nếu một vấn đề được tìm thấy trong quá trình cài đặt (hoặc trong các tài liệu hướng dẫn cài đặt), vui lòng truy cập hệ thống theo dõi lỗi của chúng tôi và kiểm tra nếu lỗi được biết đến. Nếu không, hãy tạo ra một báo cáo lỗi cho nó vì vậy chúng tôi có thể chăm sóc nó. Đừng ngại nói với các nhà phát triển - họ (nói chung) không ăn thịt người :))

Lưu ý rằng, mặc dù tài liệu này là kiến trúc cụ thể, nó có thể chứa tài liệu tham khảo để các kiến trúc khác là tốt. Điều này là do thực tế là phần lớn các mã nguồn sử dụng Cẩm nang Gentoo đó là chung cho tất cả các kiến trúc (để tránh trùng lặp của các nỗ lực và thiếu tài nguyên phát triển). Chúng tôi sẽ cố gắng giữ  đến mức tối thiểu để tránh nhầm lẫn.


<a name="2"></a>
#2. Yêu cầu Hardware 

Trước khi chúng tôi bắt đầu, đầu tiên chúng tôi liệt kê những yêu cầu phần cứng cần thiết để cài đặt Gentoo vào một amd64.

||Minimal CD|LiveDVD
------------|----------|--------            
CPU| 	Any AMD64 CPU or EM64T CPU (Core 2 Duo & Quad processors are EM64T)|
Memory|256 MB|512 MB
Disk space|2.5 GB (excluding swap space)|
Swap space|At least 256 MB| 


<a name="3"></a>
#3. Cài đặt CD Gentoo Linux 


<a name="31"></a>
###3.1 Đĩa CD cài thối thiểu 

Gentoo minimal íntallation CD là một CD khởi động chứa sự tự duy trì môi trường Gentoo. Nó cho phép người sử dụng để khởi động Linux từ đĩa CD. Trong quá trình khởi động của phần cứng được phát hiện và điều khiển thích hợp được nạp. CD này được duy trì bởi các nhà phát triển Gentoo và cho phép bất cứ ai để cài đặt Gentoo nếu một kết nối Internet đang hoạt động có sẵn.

<a name="32"></a>
###3.2  Gentoo LiveDVD

Thỉnh thoảng, một DVD đặc biệt được chế tác bởi dự án Gentoo Ten mà có thể được sử dụng để cài đặt Gentoo. Các hướng dẫn tiếp tục xuống chương này nhắm vào đĩa CD mininal installation có thể là một chút khác nhau. Tuy nhiên, các LiveDVD (hoặc bất kỳ môi trường Linux khởi động khác) hỗ trợ nhận được một dấu nhắc root bằng cách chỉ cần gọi ```sudo su -``` hoặc ```sudo -i``` trong terminal.


<a name="33"></a>
###3.3 Giai đoạn sau đó là gì ?

Một stage3 là một kho lưu trữ có chứa một môi trường minimal Gentoo, thích hợp để tiếp tục cài đặt Gentoo sử dụng các hướng dẫn trong sách hướng dẫn này. Trước đây, Cẩm nang Gentoo mô tả việc cài đặt bằng một trong ba stage tarball. Trong khi Gentoo vẫn cung cấp stage1 và stage2 tarball, phương pháp cài đặt chính thức sử dụng stage3.

Tarball stage3 có thể được tải về từ releases / amd64 / autobuilds / trên bất kỳ website chính thức Gentoo.Ttập tin stage cập nhật thường xuyên và không nằm trên đĩa CD cài đặt.



<a name="4"></a>
#4. Tải và burning  CD


### Burning với Linux

Trên Linux, tập tin ISO có thể được ghi trên đĩa CD bằng cách sử dụng lệnh cdrecord, một phần của gói  ```app-cdr / cdrtools ```.

Ví dụ, để ghi file ISO vào đĩa CD vào thiết bị / dev / sr0 (đây là thiết bị đĩa CD đầu tiên trên hệ thống - thay thế với các tập tin thiết bị phù hợp nếu cần thiết):

```
user $cdrecord dev=/dev/sr0 install-amd64-minimal-20141204.iso
```

Người dùng muốn có một giao diện đồ họacó thể sử dụng K3B, một phần của gói ```app-cdr /k3b```  . Trong K3B, vào Tools và sử dụng Burn CD Image. Sau đó làm theo các hướng dẫn được cung cấp bởi K3B.


<a name="5"></a>
#5. Booting CD



<a name="51"></a>
###5.1 Khởi động trình cài đặt 

Một khi các đĩa CD cài đặt được boot, đó là thời gian để khởi động nó. Hủy bỏ tất cả các phương tiện khởi động từ bên ngoài hệ thống (bao gồm bất kỳ đĩa CD / đĩa DVD hoặc ổ đĩa USB), khởi động lại hệ thống, và nhập vào giao diện người dùng firmware của bo mạch chủ. Điều này thường được thực hiện bằng cách nhấn một phím từ bàn phím như ```DEL``` , ```F1```, ```F10```   or  ```ESC``` trong qúa trình Power-On Self-test (POST). Các 'trigger' key khác nhau tùy thuộc vào hệ thống và bo mạch chủ. Nếu nó không  sử dụng rõ ràng một công cụ tìm kiếm internet và làm một số nghiên cứu sử dụng tên mẫu của bo mạch chủ như các từ khóa tìm kiếm. Kết quả sẽ được dễ dàng để xác định. Một khi bên trong menu firmware bo mạch chủ, thay đổi thứ tự khởi động để các phương tiện khởi động bên ngoài (đĩa CD / DVD hoặc ổ đĩa USB) sẽ được thử trước các thiết bị đĩa nội bộ. Nếu không có sự thay đổi này, hệ thống sẽ nhiều khả năng khởi động lại để các thiết bị đĩa nội bộ, bỏ qua các phương tiện truyền thông khởi động bên ngoài.

Bây giờ đặt các đĩa CD cài đặt vào ổ CD-ROM và khởi động lại. Một dấu nhắc khởi động sẽ được hiển thị. Tại màn hình này, ```Enter```  sẽ bắt đầu quá trình khởi động với các tùy chọn khởi động mặc định. Để khởi động đĩa CD cài đặt với các tùy chọn khởi động tùy chỉnh, xác định một hạt nhân sau đó tùy chọn khởi động và  nhấn ```Enter```. 

Tại dấu nhắc khởi động, người sử dụng có được tùy chọn hiển thị hạt nhân có sẵn ```F1``` và các tùy chọn khởi động ```F2```. Nếu không có lựa chọn sẽ tự thực hiện trong vòng 15 giây (hoặc hiển thị thông tin hoặc sử dụng một hạt nhân) sau đó các đĩa CD cài đặt sẽ  trở lại để khởi động từ đĩa. Điều này cho phép cài đặt để khởi động lại và thử môi trường cài đặt của họ mà không cần phải loại bỏ các đĩa CD từ khay.

Khi đề cập một hạt nhân cụ thể. Trên đĩa CD cài đặt, một số hạt nhân được cung cấp. Mặc định được gọi là gentoo. Hạt nhân khác là cho các nhu cầu phần cứng cụ thể và các biến thể -nofb vô hiệu hóa hỗ trợ bộ đệm khung.

Bảng tiếp theo cho một tổng quan ngắn của các hạt nhân có sẵn.

|Hạt nhân|Mô tả|
|------------|--------|
|gentoo|Hạt nhân mặc định với sự hỗ trợ cho CPU K8 (bao gồm hỗ trợ Numa) và CPU EM64T|
|gentoo-nofb|Tương tự như gentoo nhưng không có hỗ trợ bộ đệm khung|
|memtest86|Kiểm tra cho các lỗi RAM|

Cùng với hạt nhân, tùy chọn khởi động giúp đỡ thêm nữa trong việc điều chỉnh các quá trình khởi động.

|**Tùy chọn Hardware**||
|---------------------------|----------------------------|
|acpi=on |Điều này hỗ trợ cho ACPI và cũng gây ra các daemon acpid được bắt đầu bởi các đĩa CD khởi động, chỉ cần thiết nếu hệ thống yêu cầu ACPI để hoạt động đúng và là không cần thiết để hỗ trợ siêu phân luồng.|
|acpi=off |Hoàn toàn vô hiệu hóa ACPI. Điều này rất hữu ích trên một số hệ thống cũ và cũng là một yêu cầu cho việc sử dụng APM. Điều này sẽ vô hiệu hóa bất kỳ hỗ trợ siêu phân luồng xử lý của bạn.|
|console=X |Thiết lập quyền truy cập giao diện điều khiển nối tiếp cho đĩa CD. Các tùy chọn đầu tiên là thiết bị, thường ttyS0 trên x86, tiếp theo là bất kỳ tùy chọn kết nối, được phân tách ra. Các tùy chọn mặc định là 9600,8, n, 1|
|dmraid=X|Cho phép lựa chọn đi tới hệ thống RAID device-mapper. Tùy chọn nên được gói gọn trong dấu ngoặc kép.|
|doapm|Nạp driver hỗ trợ APM, cũng đòi hỏi rằng acpi = off.|
|dopcmcia|Hỗ trợ cho PCMCIA và phần cứng Cardbus và cũng khiến cardmgr pcmcia được bắt đầu bởi các đĩa CD khởi động. Chỉ cần thiết khi khởi động từ thiết bị PCMCIA / Cardbus.|
|doscsi|Hỗ trợ cho hầu hết các bộ điều khiển SCSI. Đây cũng là một yêu cầu để khởi động hầu hết các thiết bị USB, khi họ sử dụng các hệ thống phụ SCSI của hạt nhân.|
|sda = stroke|Cho phép người sử dụng để phân vùng toàn bộ đĩa cứng ngay cả khi BIOS không thể xử lý các ổ đĩa lớn. Tùy chọn này chỉ được sử dụng trên máy với BIOS cũ. Thay sda với thiết bị cần tùy chọn này.|
|ide = nodma|Buộc vô hiệu hóa DMA trong hạt nhân và là yêu cầu của một số chipset IDE và cũng bởi một số ổ đĩa CD-ROM. Nếu hệ thống đang gặp khó khăn trong việc đọc từ IDE CD-ROM, thử tùy chọn này. Điều này cũng vô hiệu hóa các thiết lập mặc định hdparm được thực thi.|
|noapic|Nô hiệu hóa Advanced Programmable Interrupt Controller mà hiện diện trên bo mạch chủ mới. Nó đã được biết là gây ra một số vấn đề về phần cứng cũ.|
|nodetect| Điều này vô hiệu hóa tất cả các phát hiện tự động được thực hiện bởi CD, bao gồm thiết bị phát hiện tự động và thăm dò DHCP. Điều này rất hữu ích cho việc gỡ lỗi của thất bại đĩa CD hoặc trình điều khiển.|
|nodhcp|Vô hiệu hóa DHCP thăm dò trên card mạng được phát hiện. Điều này rất hữu ích trên mạng với địa chỉ chỉ tĩnh.|
|nodmraid|Tắt hỗ trợ cho ánh xạ thiết bị RAID, chẳng hạn như được sử dụng cho các bộ điều khiển RAID trên bo IDE / SATA.|
|nofirewire|Vô hiệu hóa việc tải các module Firewire. Điều này chỉ cần thiết nếu phần cứng Firewire của bạn đang gây ra một vấn đề với khả năng khởi động đĩa CD.|
|nogpm|Tắt hỗ trợ giao diện điều khiển chuột gpm.|
|nohotplug|Điều này vô hiệu hóa việc nạp hotplug và coldplug init script lúc khởi động. Rất hữu ích cho việc gỡ lỗi của thất bại đĩa CD hoặc trình điều khiển.|
|nokeymap|Điều này vô hiệu hóa việc lựa chọn bố trí bàn phím được sử dụng để chọn bố trí bàn phím-US.|
|nolapic|Điều này vô hiệu hóa APIC địa phương trên bộ xử lý đơn nhân.|
|nosata|Điều này vô hiệu hóa việc nạp các mô-đun ATA nối tiếp. Được sử dụng nếu các hệ thống có vấn đề với các hệ thống phụ SATA.|
|nosmp|Tắt SMP, hoặc đa đối xứng, vào hạt nhân SMP kích hoạt. Hữu ích để gỡ lỗi SMP liên quan đến các vấn đề với trình điều khiển và Bo mạch chủ nhất định.|
|nosound|Hỗ trợ âm thanh và âm lượng được thiết lập. Điều này rất hữu ích cho các hệ thống nơi âm thanh hỗ trợ gây ra vấn đề.|
|nousb|Vô hiệu hóa tự động của mô-đun USB. Gữu ích để gỡ lỗi các vấn đề USB.|
|slowusb|Cho biết thêm một số tạm dừng thêm vào trong quá trình khởi động chậm cho CDROM USB, giống như trong IBM BladeCenter.|
|**Quản lý âm lượng/dịch vụ**||
|dolvm|Cho phép hỗ trợ cho Linux Quản lý Logical Volume.|
|**Tùy chọn khác**||
|debug|Cho phép gỡ lỗi coe. Có thể lộn xộn, vì nó sẽ hiển thị rất nhiều dữ liệu vào màn hình.|
|docache|Lưu trữ toàn bộ phần runtime của CD vào bộ nhớ RAM, cho phép người sử dụng để umount / mnt / cdrom và gắn CD-ROM khác. Tùy chọn này đòi hỏi phải có ít nhất là gấp đôi bộ nhớ RAM có sẵn như kích thước của đĩa CD.|
|doload=X|Gây ra các đĩa RAM ban đầu để tải bất kỳ thành phần được liệt kê, cũng như phụ thuộc. Thay thế X với tên module. Nhiều mô-đun có thể được xác định bởi một danh sách bằng dấu phẩy.|
|dosshd|Bắt đầu sshd khi khởi động, đó là hữu ích cho cài đặt không cần giám sát.|
|passwd = foo|thiết lập bất cứ điều gì bằng như mật khẩu chủ, là cần thiết cho dosshd kể từ khi mật khẩu chủ là theo mặc định tranh giành.|
|noload = X|Gây ra các đĩa RAM ban đầu để bỏ qua việc nạp một module cụ thể mà có thể gây ra một vấn đề. Cú pháp phù hợp của doload.|
|nonfs|Vô hiệu khởi đầu của portmap / nfsmount khi khởi động.|
|nox|Gây ra một LiveCD X-enable để không tự động khởi động X, nhưng đúng hơn, để thả vào dòng lệnh để thay thế.|
|scandelay|Gây ra đĩa CD để tạm dừng 10 giây trong khi một số phần tiến trình khởi động cho phép cho các thiết bị được làm chậm để khởi tạo sẵn sàng sử dụng.|
|scandelay = X|Cho phép người dùng chỉ định một sự chậm trễ nhất định, trong vài giây, sẽ được thêm vào một số phần của tiến trình khởi động để cho phép các thiết bị làm chậm khởi tạo sẵn sàng sử dụng. Thay thế X bằng số giây để tạm dừng.|

```
Đĩa CD sẽ kiểm tra tùy chọn no* trước tùy chọn do*, do đó tùy chọn có thể bị ghi đè trong một trật tự xác định
```
Bây giờ khởi động đĩa CD, chọn một hạt nhân (nếu kernel gentoo mặc định không đủ) và các tùy chọn khởi động. Như một ví dụ, chúng ta khởi động hạt nhân gentoo, với dopcmcia như một tham số hạt nhân.

```
boot:gentoo dopcmcia
```

Tiếp theo người dùng sẽ được chào đón với một màn hình khởi động và thanh tiến trình. Nếu việc cài đặt được thực hiện trên một hệ thống với một bàn phím non-US, hãy chắc chắn để ngay lập tức nhấn ```Alt + F1``` để chuyển sang chế độ verbose và theo dấu nhắc. Nếu không có lựa chọn sẽ tự thực hiện trong 10 giây, mặc định (non-US) sẽ được chấp nhận và quá trình khởi động sẽ tiếp tục. Một khi quá trình khởi động hoàn tất, người dùng sẽ được tự động đăng nhập vào "Live" Gentoo Linux  như là người dùng root, super user. Một dấu nhắc root được hiển thị trên giao diện điều khiển, và có thể chuyển sang console khác bằng cách nhấn ```Alt + F2, Alt + F3 và Alt + F4```.  Quay lại bắt đầu bằng cách nhấn ```Alt + F1```.

