# Lab: Web shell upload via extension blacklist bypass

> Phòng lab này chứa lỗ hổng file upload trong phần upload avatar. Phần mở rộng của file upload nằm trong blacklist nhưng vẫn có thể bypass nó bằng một số cách thức đặc biệt.
> 
> Để giải quyết phòng lab, hãy tải lên một web shell PHP cơ bản và sử dụng nó để lấy nội dung của file mật `/home/carlos/secret`. Gửi nội dung lấy được bằng nút **Submit**
>
> Hãy đăng nhập vào account `wiener:peter` để upload avatar

Thử upload file `exploit.php` với nội dung `<?php echo file_get_contents('/home/carlos/secret') ?>` thì nhận được phản hồi ***Sorry, php files are not allowed Sorry, there was an error uploading your file.***

Trang web đã liệt kê những đuôi file có thể gây nguy hại vào blacklist ví dụ như:  `.php, .pHp, .Php, .phP, .pht, .phtml, .php3, .php4, .php5, .php6, .inc, ...`
=> khai thác tệp cấu hình .htacces. Bắt request up file bằng burp thấy rằng trang web đang giao tiếp với máy chủ Apache, chỉnh sửa thông tin tải lên của file 

 -  Sửa phần  `filename`  thành  `.htaccess`.
-   Sửa `Content-Type`  thành  `text/plain`.
- Thay thế nội dung của tệp (PHP payload của mình) bằng lệnh Apache sau: `AddType application/x-httpd-php .l33t`
Điều này ánh xạ một phần mở rộng tùy ý (`.l33t`) thành kiểu MIME có thể thực thi được  `application/x-httpd-php`. Vì máy chủ sử dụng mô-đun `mod_php` nên nó biết cách xử lý điều này.

>![](2.png)

Forward request và trang web báo đã tải lên file ***.htaccess*** thành công. Quay lại trang upload và sửa đuôi file `.php` thành `.l33t` trong `filename` vì lúc này đuôi file `.l33t` đã được chấp nhận như một file `.php` nhờ file `.htaccess`. 

Chuyển sang tab repeater và dùng lệnh `GET /files/avatars/exploit.l33t`