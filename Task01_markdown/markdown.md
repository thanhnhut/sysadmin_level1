# I.Giới thiệu
- __Markdown__là một ngôn ngữ đánh dấu với cú pháp văn bản thô, được thiết kế để có thể dễ dàng chuyển thành HTML và nhiều định dạng khác sử dụng một công cụ cùng tên.
- Năm 2004, cùng với sự giúp đỡ của __Aaron Swartz, John Gruber__ đã tạo ra ngôn ngữ Markdown với mục tiêu tạo ra một định dạng văn bản thô "dễ viết, dễ đọc, dễ dàng chuyển thành XHTML (hoặc HTML). Markdown dùng các dấu hiệu từ các quy ước cho văn bản thô trong email, như __setext__ - một ngôn ngữ được thiết kế để có thể đọc bình thường mà không phải lục lọi giữa các thẻ định dạng, khác với văn bản trong __ngôn ngữ đánh dấu__ như RTF hay HTML, vốn chứa nhiều thẻ và cú pháp khó đọc. Gruber đã viết một công cụ nhỏ bằng Perl, Markdown.pl, cho phép chuyển đổi đoạn văn bản đã đánh dấu theo chuẩn Markdown sang XHTML hoặc HTML. Tiện ích này có thể dùng một mình, hoặc dùng như là plugin cho __Bloxom__ hoặc __Movable Type__, hoặc là một bộ lọc cho __BBEdit__. Markdown sau đó đã được hoàn thiện thành một mô đun Perl và công bố trên __CPAN__ (Text::Markdown) cũng như trên một vài ngôn ngữ khác. Nó được phân phối theo __giấy phép BSD__ và được nhúng sẵn, hoặc là plugin của một số __hệ thống quản lý nội dung__.. Một số trang web như GitHub, reddit, Diaspora, Stack 
- __Markdown__ được dùng để:

_ Nó thường được dùng để tạo các tập tin readme, viết tin nhắn trên các diễn đàn, và tạo văn bản có định dạng bằng một trình biên tập văn bản thô.

_ Có thể dùng để viết sách, phần lớn sách, truyện đều có kết cấu (về mặt format) đơn giản: phân thành các chương, phần đề mục chương, trong chương thì có các đoạn văn, có các list gạch đầu dòng, có một vài tấm ảnh, chữ đậm, chữ nghiêng,... 

_ Có thể dùng để viết blog, tin tức

_ Ngoài ra cũng có một số người  đã kết hợp Markdown và __impress.js__ (một thư viện web nguồn mở để tạo slide presentation 3D như __prezi.com - seriously, press that impress.js link xD__) thành một công cụ presentation vô cùng độc đáo là __Hekyll__

#II.Các lệnh cơ bản 

__II.1 Tạo Tiêu Đề__

 # Tiêu đề 1 (h1)
 
 ## Tiêu đề 2 (h2)
 
 ### Tiêu đề 3 (h3)

Để tạo tiêu đề trong Markdown  chỉ cần chèn ký tự # ngay phía trước. Số lượng ký tự # sẽ xác định độ sâu của tiêu đề .

__II.2 Định Dạng Chữ__

 **  ** hoặc __ __ bên trong là in đậm
 
 ** hoặc _ _ bên trong là in nghiêng 

~~ ~~ bên trong là chũ gạch ngang


__II.3 Tạo Danh Sách__

Tạo danh sách dạng số:

1. danh sách 1
2. danh sách 2
3. danh sách 3

Tạo danh sách dạng bullet:

- danh sách 1
- danh sách 2
- danh sách 3

__II.4 Tạo Liên Kết__

Để tạo ra một liên kết văn bản,cần phải bọc nội dung trong dấu ngoặc vuông [ ], với URL trong dấu ngoặc đơn ( )

__II.5 Tạo liên kết tự động__

Chỉ cần gõ đường link tuyệt đối (có HTTP hoặc HTTPS) Markdown sẽ tạo liên kết tự động

http://example.com

__II.6 Tạo Hình Ảnh__

Chèn một hình ảnh cũng tương tự như cách thêm một liên kết văn bản ( link ). Trong Markdown, một hình ảnh, được bắt đầu với một dấu chấm than !. Bọc thông tin hình ảnh ( title, alt ) trong dấu " và URL hình ảnh trong dấu ngoặc đơn ( )

__II.7Tạo Trích Dẫn (Blockquotes)__

Để tạo trích dẫn bạn chèn > ngay phía trước

  >câu trích dẫn

__II.8 Tạo Đường Kẻ Gạch Ngang__

Bạn gõ --- hoặc *** hoặc ___

---
***
___

__II.9 Tạo Điểm Nhấn (highlight)__

==text==

__II. Inline Code__

` inline code`

__II.10 Tạo chú thích cuối trang__

Chú thích[^1] chú thích[^2].  

- [^1]: chú thích 1 
- [^2]: chú thích 2

__II.11 Bảng__

| Header | Header | Right  |
|:-------|:------:|-------:|
|  Cell  |  Cell  |   $10  |
|  Cell  |  Cell  |   $20  |
| ====== | ====== | =====: |
| Footer | Footer | Footer |


Kí tự | bắt đầu một hàng

Kí tự - tách phần header của bảng

Kí tự = tách phần footer

Kí tự : gióng hàng trong cột (trái, phải hoặc 2 bên là gióng giữa)

#III.Kết luận

__Ưu điểm của markdown__

Trong quá trình sử dụng computer và làm việc với internet, ta thường gặp những vấn đề sau:Lưu trữ thông tin dạng text một cách đơn giản, dễ dàng. Dễ dùng tool để so sánh, chỉnh sửa sự thay đổi của dữ liệu text. Text có thể dễ dàng view được qua internet như 1 trang web thực sự mà ko phải viết nhúng mã HTML vào file thì Markdown là đinh dạng hoàn hảo để giải quyết các vấn đề trên.

__Nhược điểm của markdown__

Có lẽ nhược điểm lớn nhất  là không có khả năng cộng tác trong Markdown và theo dõi những thay đổi (một ngoại lệ đáng chú ý này, mặc dù, là plugin StackEdit cho Google Docs). Nó chỉ thích hợp cho những dự án nhỏ lẻ, những bài blog cá nhân vì đòi hỏi công sức quá lớn khi biên tập cho những quyển sách, do tối giản hết mức có thể mà có rất nhiều tính năng nâng cao mà Markdown không hỗ trợ.

__Tại sao phải sử dụng markdown__

_ Sự phổ biến của HTML khiến ngôn ngữ đánh dấu này được sử dụng rộng rãi trong các ứng dụng sử dụng internet từ các trang web tới nội dung email hay rất nhiều các tài liệu hướng dẫn online cũng đều sử dụng ngôn ngữ này. Tuy nhiên một vấn đề gặp phải của HTML đó là cú pháp của ngôn ngữ này không được thân thiện lắm với người dùng.

_ Nếu như không có kiến thức về ngôn ngữ HTML thì bạn rất khó có thể đọc được nôi dung của đoạn văn hay văn bản.

_ Markdown giải quyết vấn đề trên bằng việc đưa ra cú pháp để giúp đánh dấu văn bản một cách dễ hiểu và ngắn gọn hơn.

#IV.Tài liệu tham khảo

http://tuantda.github.io/blog/markdown-cheatsheet.html

https://techmaster.vn/posts/33367/cu-phap-markdown-la-gi

https://nguyenthethang.com/2013/08/16/keyword-ngon-ngu-markdown-la-gi-what-is-markdown/

http://www.hoclaptrinh.org/bai-viet/Markdown-La-Gi

https://vi.wikipedia.org/wiki/Markdown

http://ngochin.com/2013/01/03/markdown/


