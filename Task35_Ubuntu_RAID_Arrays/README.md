## Ubuntu RAID Arrays


> 
> Thực hiện: **Nguyễn Thanh Nhựt**
> 
> Cập nhật lần cuối: **30/11/2016**

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

[3. Tạo một cấp đọ RAID](#3)

- [3.1 Tạo một mảng RAID 0](#31)

- [3.2 Tạo một mảng RAID 1](#32)

- [3.3 Tạo một mảng RAID 5](#33)

- [3.4 Tạo một mảng RAID 6](34)

- [3.5 Tạo một mảng RAID 10](#35)







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



<a name="3"></a>
#3. Tạo các cấp độ RAID


<a name="31"></a>
###3.1 Tạo một mảng RAID 0

Yêu cầu tối thiểu là 2 thiết bị lưu trữ

Những điều cần lưu ý: Hãy chắc chắn rằng bạn đã sao lưu chức năng. Một thiết bị duy nhất thất bại sẽ phá hủy tất cả dữ liệu trong mảng.

**Xác định các thiết bị**

Để bắt đầu, tìm ra định danh cho các ổ đĩa liệu mà bạn sẽ sử dụng:

```
    lsblk -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINT
```
<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a1.png"/></p>

**Tạo mảng**

```
 $  sudo mdadm --create --verbose /dev/md0 --level=0 --raid-devices=2 /dev/sda /dev/sdb
```

Bạn có thể đảm bảo rằng các RAID đã được tạo thành công bằng cách kiểm tra file /proc/mdstat:

```
 $   cat /proc/mdstat
```

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a2.png"/></p>


**Tạo và Gắn kết hệ thống tập tin**

Tiếp theo, tạo một tập tin hệ thống trên mảng:

```
 $  sudo mkfs.ext4 -F /dev/md0
```

Tạo một điểm gắn kết để gắn hệ thống tập tin mới:


```
 $   sudo mkdir -p /mnt/md0
```


Bạn có thể gắn kết tập tin hệ thống bằng cách gõ:

```
 $   sudo mount /dev/md0 /mnt/md0
```

Kiểm tra xem các không gian mới có sẵn bằng cách gõ:

```
  $  df -h -x devtmpfs -x tmpfs
```
<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a3.png"/></p>

**Lưu Layout Mảng**



Để đảm bảo rằng các mảng được tập hợp lại tự động lúc khởi động, chúng ta sẽ phải điều chỉnh file /etc/mdadm/mdadm.conf . Bạn có thể tự động quét các mảng hoạt động và gắn thêm các tập tin bằng cách gõ:

```
 $   sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
```


Sau đó, bạn có thể cập nhật các initramfs, hoặc hệ thống tập tin RAM ban đầu, do đó, các mảng sẽ có sẵn trong quá trình khởi động sớm:

```
 $   sudo update-initramfs -u
```


Thêm hệ thống tập tin mới tùy chọn gắn kết với tập tin  /etc/fstab để tự động gắn vào khởi động:

```
 $   echo '/dev/md0 /mnt/md0 ext4 defaults,nofail,discard 0 0' | sudo tee -a /etc/fstab
```

<a name="32"></a>
###3.2 Tạo mảng RAID 1

Yêu cầu: tối thiểu là 2 thiết bị lưu trữ

Những điều cần lưu ý: Kể từ khi hai bản sao của dữ liệu được duy trì, chỉ có một nửa của không gian đĩa sẽ được sử dụng được

**Xác định các thiết bị**


Để bắt đầu, tìm ra định danh cho các ổ đĩa liệu mà bạn sẽ sử dụng:

```
$    lsblk -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINT
```
<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a1.png"/></p>

**Tạo mảng**


```
$    sudo mdadm --create --verbose /dev/md0 --level=1 --raid-devices=2 /dev/sda /dev/sdb
```

Nếu các thiết bị thành phần mà bạn đang sử dụng không phải là phân vùng với  cờ kích hoạt boot, bạn có thể sẽ được cung cấp các cảnh báo sau đây. Nó là an toàn để gõ y để tiếp tục:

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a4.png"/></p>

Các mdadm công cụ sẽ bắt đầu để nhân bản ổ đĩa. Điều này có thể mất một thời gian để hoàn thành, nhưng các mảng có thể được sử dụng trong thời gian này. Bạn có thể theo dõi sự tiến độ của mirroring bằng cách kiểm tra file /proc/mdstat:

```
    cat /proc/mdstat
```

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a5.png"/></p>

**Tạo và Gắn kết hệ thống tập tin**

Tiếp theo, tạo một tập tin hệ thống trên mảng:

```
 $  sudo mkfs.ext4 -F /dev/md0
```

Tạo một điểm gắn kết để gắn hệ thống tập tin mới:


```
 $   sudo mkdir -p /mnt/md0
```


Bạn có thể gắn kết tập tin hệ thống bằng cách gõ:

```
 $   sudo mount /dev/md0 /mnt/md0
```

Kiểm tra xem các không gian mới có sẵn bằng cách gõ:

```
  $  df -h -x devtmpfs -x tmpfs
```
<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a6.png"/></p>

**Lưu Layout mảng**



Để đảm bảo rằng các mảng được tập hợp lại tự động lúc khởi động, chúng ta sẽ phải điều chỉnh file /etc/mdadm/mdadm.conf . Bạn có thể tự động quét các mảng hoạt động và gắn thêm các tập tin bằng cách gõ:

```
 $   sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
```


Sau đó, bạn có thể cập nhật các initramfs, hoặc hệ thống tập tin RAM ban đầu, do đó, các mảng sẽ có sẵn trong quá trình khởi động sớm:

```
 $   sudo update-initramfs -u
```


Thêm hệ thống tập tin mới tùy chọn gắn kết với tập tin  /etc/fstab để tự động gắn vào khởi động:


```
$    echo '/dev/md0 /mnt/md0 ext4 defaults,nofail,discard 0 0' | sudo tee -a /etc/fstab
```

<a name="33"></a>
###3.3 Tạo một mảng RAID 5

Yêu cầu: tối thiểu 3 thiết bị lưu trữ

Những điều cần lưu ý: Trong khi các thông tin parity  được phân bố, giá trị một đĩa sẽ được sử dụng cho parity

**Xác định các thiết bị phần**

Để bắt đầu, tìm ra định danh cho các ổ đĩa liệu mà bạn sẽ sử dụng:


```
 $   lsblk -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINT
```
<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a1.png"/></p>


**Tạo mảng **

```
$    sudo mdadm --create --verbose /dev/md0 --level=5 --raid-devices=3 /dev/sda /dev/sdb /dev/sdc
```

Các công cụ mdadm sẽ bắt đầu cấu hình mảng (nó thực sự sử dụng quá trình phục hồi để xây dựng các mảng vì lý do hiệu suất). Điều này có thể mất một thời gian để hoàn thành, nhưng các mảng có thể được sử dụng trong thời gian này. Bạn có thể theo dõi sự tiến độ của mirroring bằng cách kiểm tra file /proc/mdstat:

```
 $   cat /proc/mdstat
```
<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a7.png"/></p>

**Tạo và Gắn kết hệ thống tập tin**

Tiếp theo, tạo một tập tin hệ thống trên mảng:

```
 $  sudo mkfs.ext4 -F /dev/md0
```

Tạo một điểm gắn kết để gắn hệ thống tập tin mới:


```
 $   sudo mkdir -p /mnt/md0
```


Bạn có thể gắn kết tập tin hệ thống bằng cách gõ:

```
 $   sudo mount /dev/md0 /mnt/md0
```

Kiểm tra xem các không gian mới có sẵn bằng cách gõ:

```
  $  df -h -x devtmpfs -x tmpfs
```
<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a8.png"/></p>

**Lưu layout mảng**


Để đảm bảo rằng các mảng được tập hợp lại tự động lúc khởi động, chúng tôi sẽ phải điều chỉnh file /etc/mdadm/mdadm.conf.

Trước khi bạn điều chỉnh cấu hình, kiểm tra một lần nữa để chắc chắn rằng các mảng đã hoàn thành lắp ráp

```
$    cat /proc/mdstat
```
```
Output
Personalities : [raid1] [linear] [multipath] [raid0] [raid6] [raid5] [raid4] [raid10] 
md0 : active raid5 sdc[3] sdb[1] sda[0]
      209584128 blocks super 1.2 level 5, 512k chunk, algorithm 2 [3/3] [UUU]

unused devices: <none>
```

Các đầu ra ở trên cho thấy việc xây dựng lại hoàn tất. Bây giờ, chúng ta có thể tự động quét các mảng hoạt động và gắn thêm các tập tin bằng cách gõ:

```
$    sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
```

Sau đó, bạn có thể cập nhật các initramfs, hoặc hệ thống tập tin RAM ban đầu, do đó, các mảng sẽ có sẵn trong quá trình khởi động:

```
    sudo update-initramfs -u
```

Thêm hệ thống tập tin mới tùy chọn gắn kết với tập tin  /etc/fstab để tự động gắn vào khởi động:

```
    echo '/dev/md0 /mnt/md0 ext4 defaults,nofail,discard 0 0' | sudo tee -a /etc/fstab
```

<a name="34"></a>
###3.4 Tạo một mảng RAID 6


Yêu cầu: tối thiểu là 4 thiết bị lưu trữ

Những điều cần lưu ý: Trong khi các thông tin parity được phân bố, giá trị hai đĩa  sẽ được sử dụng cho parity. RAID 6 có thể bị hiệu suất rất kém khi ở trong tình trạng suy thoái.

**Xác định các thiết bị phần**

Để bắt đầu, tìm ra định danh cho các ổ đĩa liệu mà bạn sẽ sử dụng:


```
 $   lsblk -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINT
```


**Tạo mảng**

<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a1.png"/></p>
```
$    sudo mdadm --create --verbose /dev/md0 --level=6 --raid-devices=4 /dev/sda /dev/sdb /dev/sdc /dev/sdd
```

Các công cụ mdadm sẽ bắt đầu cấu hình mảng (nó thực sự sử dụng quá trình phục hồi để xây dựng các mảng vì lý do hiệu suất). Điều này có thể mất một thời gian để hoàn thành, nhưng các mảng có thể được sử dụng trong thời gian này. Bạn có thể theo dõi sự tiến bộ của mirroring bằng cách kiểm tra /proc/mdstat file:

```
$    cat /proc/mdstat
```
<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a9.png"/></p>

**Tạo và Gắn kết hệ thống tập tin**

Tiếp theo, tạo một tập tin hệ thống trên mảng:

```
 $  sudo mkfs.ext4 -F /dev/md0
```

Tạo một điểm gắn kết để gắn hệ thống tập tin mới:


```
 $   sudo mkdir -p /mnt/md0
```


Bạn có thể gắn kết tập tin hệ thống bằng cách gõ:

```
 $   sudo mount /dev/md0 /mnt/md0
```

Kiểm tra xem các không gian mới có sẵn bằng cách gõ:

```
  $  df -h -x devtmpfs -x tmpfs
```
<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a10.png"/></p>

**Lưu Layout mảng**


*Lưu Layout Mảng**



Để đảm bảo rằng các mảng được tập hợp lại tự động lúc khởi động, chúng ta sẽ phải điều chỉnh file /etc/mdadm/mdadm.conf . Bạn có thể tự động quét các mảng hoạt động và gắn thêm các tập tin bằng cách gõ:

```
 $   sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
```


Sau đó, bạn có thể cập nhật các initramfs, hoặc hệ thống tập tin RAM ban đầu, do đó, các mảng sẽ có sẵn trong quá trình khởi động sớm:

```
 $   sudo update-initramfs -u
```


Thêm hệ thống tập tin mới tùy chọn gắn kết với tập tin  /etc/fstab để tự động gắn vào khởi động:

```
    echo '/dev/md0 /mnt/md0 ext4 defaults,nofail,discard 0 0' | sudo tee -a /etc/fstab
```

<a name="35"></a>
###3.5 Tạo một mảng RAID 10


Yêu cầu: tối thiểu 3 thiết bị lưu trữ

  Những điều cần lưu ý: số lượng công suất giảm cho các mảng được xác định bởi số lượng các bản sao dữ liệu bạn chọn để tiếp tục. Số lượng các bản sao được lưu trữ với  mdadm RAID 10 là cấu hình.

Bạn có thể tìm hiểu thêm về các bố trí bằng cách xem  "RAID10" của này man trang:

```
 $   man 4 md
```

**Xác định các thiết bị phần**

Để bắt đầu, tìm ra định danh cho các ổ đĩa liệu mà bạn sẽ sử dụng:


```
 $   lsblk -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINT
```
<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a1.png"/></p>

**Tạo mảng**


Bạn có thể thiết lập hai bản bằng cách sử dụng bố trí gần bằng không quy định cụ thể một cách bố trí và bản số:

```
$    sudo mdadm --create --verbose /dev/md0 --level=10 --raid-devices=4 /dev/sda /dev/sdb /dev/sdc /dev/sdd
```

Nếu bạn muốn sử dụng một layout khác nhau, hoặc thay đổi số lượng các bản sao, bạn sẽ phải sử dụng bố trí các tùy chọn --layout= , mà phải mất một định danh layout và copy. Layout có n cho near, f cho far, o cho offset. Số lượng các bản sao để lưu trữ được gắn vào sau đó.

Ví dụ, để tạo một mảng có 3 bản trong offset layout, các lệnh sẽ trông như thế này:

```
 $   sudo mdadm --create --verbose /dev/md0 --level=10 --layout=o3 --raid-devices=4 /dev/sda /dev/sdb /dev/sdc /dev/sdd
```

Các công cụ mdadmsẽ bắt đầu cấu hình mảng (nó thực sự sử dụng quá trình phục hồi để xây dựng các mảng vì lý do hiệu suất). Điều này có thể mất một thời gian để hoàn thành, nhưng các mảng có thể được sử dụng trong thời gian này. Bạn có thể theo dõi sự tiến bộ của mirroring bằng cách kiểm tra file /proc/mdstat 

```
$    cat /proc/mdstat
```
<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a11.png"/></p>

**Tạo và Gắn kết hệ thống tập tin**

Tiếp theo, tạo một tập tin hệ thống trên mảng:

```
 $  sudo mkfs.ext4 -F /dev/md0
```

Tạo một điểm gắn kết để gắn hệ thống tập tin mới:


```
 $   sudo mkdir -p /mnt/md0
```


Bạn có thể gắn kết tập tin hệ thống bằng cách gõ:

```
 $   sudo mount /dev/md0 /mnt/md0
```

Kiểm tra xem các không gian mới có sẵn bằng cách gõ:

```
  $  df -h -x devtmpfs -x tmpfs
```
<p align="center"><img src="https://github.com/thanhnhut/sysadmin_level1/blob/master/Task35_Ubuntu_RAID_Arrays/Images/a12.png"/></p>

**Lưu Layout mảng**

Để đảm bảo rằng các mảng được tập hợp lại tự động lúc khởi động, chúng ta sẽ phải điều chỉnh file /etc/mdadm/mdadm.conf . Bạn có thể tự động quét các mảng hoạt động và gắn thêm các tập tin bằng cách gõ:

```
 $   sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
```


Sau đó, bạn có thể cập nhật các initramfs, hoặc hệ thống tập tin RAM ban đầu, do đó, các mảng sẽ có sẵn trong quá trình khởi động sớm:

```
 $   sudo update-initramfs -u
```


Thêm hệ thống tập tin mới tùy chọn gắn kết với tập tin  /etc/fstab để tự động gắn vào khởi động:

```
    echo '/dev/md0 /mnt/md0 ext4 defaults,nofail,discard 0 0' | sudo tee -a /etc/fstab
```




