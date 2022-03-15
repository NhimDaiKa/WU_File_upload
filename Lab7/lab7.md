# Lab: Web shell upload via race condition

> Phòng lab này chứa lỗ hổng file upload trong phần upload avatar. Mặc dù nó thực hiện xác thực mạnh mẽ trên bất kỳ tệp nào được tải lên, có thể bỏ qua việc xác thực này hoàn toàn bằng cách khai thác điều kiện chủng tộc theo cách nó xử lý chúng.
> 
> Để giải quyết phòng lab, hãy tải lên một web shell PHP cơ bản và sử dụng nó để lấy nội dung của file mật `/home/carlos/secret`. Gửi nội dung lấy được bằng nút **Submit**
>
> Hãy đăng nhập vào account `wiener:peter` để upload avatar

Thử upload file `exploit.php` với nội dung `<?php echo file_get_contents('/home/carlos/secret') ?>` thì nhận được phản hồi ***Sorry, only JPG & PNG files are allowed Sorry, there was an error uploading your file.***

Trang web đã chặn việc tải lên file không phải hình ảnh mặc dù đã thử các cách bypass của những lab trước nhưng vẫn không thành công. Ở đây phải sử dụng extension Turbo của port để có thể tải lên file exploit. 

Bắt POST request khi up file và chuyển vào turbo intruder. Ở request 1 thì dán phần POST request lúc up file và request 2 thì dán phần GET request để mở file. Ấn attack và đợi response :v 
