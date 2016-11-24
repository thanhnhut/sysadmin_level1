## Ubuntu RAID Arrays


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **24/11/2016**

### Mục lục

[1. Giới thiệu](#1)

[2. Các loại RAID](#2)

- [2.1 RAID 0](#21)

- [2.2 RAID 1](#22)

- [2.3 RAID 2](#23)

- [2.4 RAID 3](#24)

- [2.5 RAID 4](#25)

- [2.6 RAID 5](#26)

- [2.7 RAID 6](#27)

- [2.8 RAID 10](#28)








---

<a name="1"></a>
#1. Giới thiệu 

RAID (Redundant Arrays of Inexpensive Disks hoặc Redundant Arrays of Independent Disks) là hình thức ghép nhiều ổ đĩa cứng vật lý thành một hệ thống ổ đĩa cứng có chức năng gia tăng tốc độ đọc/ghi dữ liệu hoặc nhằm tăng thêm sự an toàn của dữ liệu chứa trên hệ thống đĩa hoặc kết hợp cả hai yếu tố trên.

Có 3 lý do chính để áp dụng RAID:

- Dự phòng
- Hiệu quả cao
-  Giá thành thấp

Sự dự phòng là nhân tố quan trọng nhất trong quá trình phát triển RAID cho môi trường máy chủ. Dự phòng cho phép sao lưu dữ liệu bộ nhớ khi gặp sự cố. Nếu một ổ cứng trong dãy bị trục trặc thì nó có thể hoán đổi sang ổ cứng khác mà không cần tắt cả hệ thống hoặc có thể sử dụng ổ cứng dự phòng. Phương pháp dự phòng phụ thuộc vào phiên bản RAID được sử dụng. 

RAID được chia thành 7 cấp độ (level), mỗi cấp độ có các tính năng riêng, hầu hết chúng được xây dựng từ hai cấp độ cơ bản là RAID 0 và RAID 1. Hiện nay 4 loại RAID được sử dụng phổ biến nhât là Raid 0, Raid 1, Raid 10 và Raid 5.


<a name="2"></a>
#2. Các loại RAID 


<a name="21"></a>
###2.1 RAID 0

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/0.png"/></p>

RAID 0 thực ra không phải là cấp độ RAID hợp lệ. RAID 0 cần ít nhất 2 ổ đĩa, tổng quát ta có n ổ đĩa. Dữ liệu sẽ được chia ra nhiều phần bằng nhau ta dùng 2 ổ cứng 80GB thì hệ thống đĩa của chúng ta là 160GB.

 Ưu điểm:
 
 - Tăng tốc độ đọc/ghi đĩa: mỗi đĩa chỉ cần phải đọc/ghi 1/n lượng dữ liệu được yêu cầu. Lý thuyết thì tốc độ sẽ tăng n lần.

Nhược điểm: 

- Tính an toàn thấp. Nếu một đĩa bị hư thì dữ liệu trên tất cả các đĩa còn lại sẽ không còn sử dụng được. Xác suất để mất dữ liệu sẽ tăng n lần so với dùng ổ đĩa đơn.

<a name="22"></a>
###2.2 RAID 1

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/1.png"/></p>

RAID 1 mới là phiên bản thực sự đầu tiên. RAID cung cấp phương pháp dự phòng dữ liệu đơn giản bằng kĩ thuật “mirroring” (nhân bản dữ liệu). Kĩ thuật này cần 2 ổ cứng riêng biệt có cùng dung lượng. Một ổ sẽ là ổ hoạt động, ổ còn lại là ổ dự phòng. Khi dữ liệu được ghi vào ổ hoạt động thì đồng thời nó cũng được ghi vào ổ dự phòng. Các dịch vụ lưu trữ, các website vừa và nhỏ không yêu cầu quá cao về tốc độ đọc ghi (in/out) của ổ cứng. Các đối tượng yêu cầu sự an toàn về dữ liệu như các dịch vụ kế toán,lưu trữ thông tin khách hàng, bất động sản v.v…

Ưu điểm:

- An toàn về dữ liệu

Nhược điểm:

- Dung lượng lưu trữ chỉ lớn bằng dung lượng ổ nhỏ nhất.

- Không tăng hiệu suất thực thi.


<a name="23"></a>
###2.3 RAID 2

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/2.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/21.png"/></p>

RAID 2 gồm hai cụm ổ đĩa, cụm thứ nhất chứa các dữ liệu được phân tách giống như là RAID 0, cụm thứ hai chứa các mã ECC dành cho sửa chữa lỗi ở cụm thứ nhất. Sự hoạt động của các ổ đĩa ở RAID 2 là đồng thời để đảm bảo rằng các dữ liệu được đọc đúng, chính do vậy chúng không hiệu quả bằng một số loại RAID khác nên ít được sử dụng.


<a name="24"></a>
###2.4 RAID 3

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/3.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/31.gif"/></p>

 RAID 3 là sự cải tiến của RAID 0 nhưng có thêm (ít nhất) một ổ cứng chứa thông tin có thể khôi phục lại dữ liệu đã hư hỏng của các ổ cứng RAID 0. Giả sử dữ liệu A được phân tách thành 3 phần A1, A2, A3 (Xem hình minh hoạ RAID 3), khi đó dữ liệu được chia thành 3 phần chứa trên các ổ cứng 0, 1, 2 (giống như RAID 0). Phần ổ cứng thứ 3 chứa dữ liệu của tất cả để khôi phục dữ liệu có thể sẽ mất ở ổ cứng 0, 1, 2. Giả sử ổ cứng 1 hư hỏng, hệ thống vẫn hoạt động bình thường cho đến khi thay thế ổ cứng này. Sau khi gắn nóng ổ cứng mới, dữ liệu lại được khôi phục trở về ổ đĩa 1 như trước khi nó bị hư hỏng. Yêu cầu tối thiểu của RAID 3 là có ít nhất 3 ổ cứng. 

<a name="25"></a>
###2.5 RAID 4

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/4.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/41.gif"/></p>

RAID 4 tương tự như RAID 3 nhưng ở một mức độ các khối dữ liệu lớn hơn chứ không phải đến từng byte. Chúng cũng yêu cầu tối thiểu 3 đĩa cứng (ít nhất hai đĩa dành cho chứa dữ liệu và ít nhất 1 đĩa dùng cho lưu trữ dữ liệu tổng thể)


<a name="26"></a>
###2.6 RAID 5

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/5.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/51.gif"/></p>

 Đây có lẽ là dạng RAID mạnh mẽ nhất cho người dùng văn phòng và gia đình với 3 hoặc 5 đĩa cứng riêng biệt. Dữ liệu và bản sao lưu được chia lên tất cả các ổ cứng. Nguyên tắc này khá rối rắm. Nhìn hình trên đoạn dữ liệu số 1 và số 2 sẽ được ghi vào ổ đĩa 1 và 2 riêng rẽ, đoạn sao lưu của chúng được ghi vào ổ cứng 3. Đoạn số 3 và 4 được ghi vào ổ 1 và 3 với đoạn sao lưu tương ứng ghi vào ổ đĩa 2. Đoạn số 5, 6 ghi vào ổ đĩa 2 và 3, còn đoạn sao lưu được ghi vào ổ đĩa 1 và sau đó trình tự này lặp lại, đoạn số 7,8 được ghi vào ổ 1, 2 và đoạn sao lưu ghi vào ổ 3 như ban đầu. Như vậy RAID 5 vừa đảm bảo tốc độ có cải thiện, vừa giữ được tính an toàn cao. Dung lượng đĩa cứng cuối cùng bằng tổng dung lượng đĩa sử dụng trừ đi một ổ. Tức là nếu bạn dùng 3 ổ 80GB thì dung lượng cuối cùng sẽ là 160GB. RAID 5 cũng yêu cầu tối thiểu có 3 ổ cứng. 

Ưu điểm:

- Tăng dung lượng lưu trữ
- Dữ liệu được dự phòng toàn bộ
- Khả năng hoán đổi nhanh 24x7

Nhược điểm:

- Giá thành cao
- Hiệu quả thực thi giảm trong quá trình phục hồi


<a name="27"></a>
###2.7 RAID 6

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/6.png"/></p>

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/61.jpg"/></p>

RAID 6 phần nào giống như RAID 5 nhưng lại được sử dụng lặp lại nhiều hơn số lần sự phân tách dữ liệu để ghi vào các đĩa cứng khác nhau. Trong RAID 6, ta thấy rằng khả năng chịu đựng rủi ro hư hỏng cứng được tăng lên rất nhiều. Nếu với 4 ổ cứng thì chúng cho phép hư hỏng đồng thời đến 2 ổ cứng mà hệ thống vẫn làm việc bình thường, điều này tạo ra một xác xuất an toàn rất lớn. Chính do đó mà RAID 6 thường chỉ được sử dụng trong các máy chủ chứa dữ liệu cực kỳ quan trọng. RAID 6 yêu cầu tối thiểu 4 ổ cứng. 


<a name="28"></a>
###2.8 RAID 10

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/10.png"/></p>

Raid 10 là sự kết hợp giữa 2 loại raid phổ biến là Raid 1 và Raid 0. Thay vì phân chia dữ liệu giữa các thiết lập ổ đĩa rồi phản chiếu chúng thì hai ổ cứng đầu tiên sẽ được phản chiếu với nhau. Đây là thiết lập RAID lồng. Hai cặp ổ 1 và 2, 3 và 4 sẽ phản chiếu lẫn nhau. Sau đó chúng sẽ được thiết lập thành các dãy phân chia dữ liệu. 

Ưu điểm:

- Tăng hiệu quả thực thi.

- Dữ liệu được dự phòng toàn bộ.

Nhược điểm:

- Yêu cầu số lượng ổ cứng lớn.

- Khả năng truy xuất dữ liệu giảm một nửa.

Bảng so sánh cấp độ RAID

|Cấp độ RAID|Dữ liệu dự phòng|Sử dụng ổ đĩa vật lý|Hiệu suất đọc|Hiệu suất ghi|ổ min|
|-----------------|----------------------|--------------------|------------------|----------------|---------------|
|0|Không|100%|nX **Tốt**|nX **Tốt**|2|
|1|Có|50%|Lên đến nX nếu nhiều quá trình đọc, nếu không 1X|1X|2|
|5|Có|67% - 94%|(N-1)X **Cao cấp** |(N-1)X **Cao cấp** |3|
|6|CÓ|50% - 88%|(N-2)X|(N-2)X|4|
|10, far2|Có|50%|nX **Tốt** tương đương RAID0 nhưng thừa|(N-2)X|2|
|10, near2|Có|50%|Lên đến nX nếu nhiều trình đang đọc, nếu không 1X|(N-2)X|2|


