# WannaCry-ish

Kho lưu trữ này cung cấp một chương trình được thiết kế như một nguồn tài nguyên giáo dục để hiểu cách ransomware hoạt động ẩn. Nó không khai thác bất kỳ lỗ hổng nào, nhưng việc thực thi ransomware thường yêu cầu một lỗ hổng trong các tình huống thực tế. Một cuộc tấn công ransomware nổi tiếng là WannaCry, sử dụng lỗ hổng của Microsoft để mã hóa dữ liệu và yêu cầu thanh toán tiền chuộc bằng Bitcoin.

# Tuyên bố miễn trừ trách nhiệm
Chương trình này chỉ dành cho mục đích giáo dục. Nó nhằm mục đích chứng minh các nguyên tắc và quy trình công việc mã hóa thường được ransomware sử dụng. Không bao giờ được sử dụng nó với mục đích độc hại hoặc gây hại cho người khác. Việc sử dụng sai công cụ này cho mục đích độc hại là bất hợp pháp và phi đạo đức. Việc sử dụng trái phép công cụ này có thể vi phạm pháp luật và dẫn đến hậu quả pháp lý nghiêm trọng. Luôn hành động có trách nhiệm và có đạo đức. Các tác giả không xác nhận hoặc dung túng cho bất kỳ hành vi sử dụng trái phép hoặc bất hợp pháp nào của phần mềm này.

# Ransomware hoạt động như thế nào?
Có ba loại khóa liên quan, mỗi loại đóng vai trò quan trọng trong quy trình công việc mã hóa:

1. Khóa AES
Khóa đối xứng được sử dụng để mã hóa và giải mã các tệp trong thư mục đích.
Nhanh chóng và hiệu quả để mã hóa dữ liệu trên quy mô lớn.
Cặp khóa RSA
Khóa công khai: Được sử dụng để mã hóa khóa AES sau khi sử dụng.
Khóa riêng (được kẻ tấn công giữ an toàn): Được sử dụng để giải mã khóa AES trong trường hợp tiền chuộc được trả.
Quy trình làm việc khóa:

Mã hóa
Một khóa AES ngẫu nhiên được tạo để mã hóa tệp.
Khóa AES được sử dụng để mã hóa nội dung của từng tệp trong thư mục đích.
Các tệp gốc được thay thế bằng phiên bản đã mã hóa của chúng.
Khóa AES được mã hóa bằng khóa công khai RSA ngăn nạn nhân giải mã tệp.
Lưu ý rằng khóa riêng RSA được lưu trữ cục bộ cho mục đích trình diễn.
Giải mã
Khóa AES được giải mã bằng khóa riêng RSA.
Khóa AES đã giải mã được sử dụng để khôi phục nội dung tệp gốc.
Tại sao phải giữ bí mật khóa riêng?

Trong trường hợp thực tế, khóa RSA riêng sẽ không bao giờ được lưu trữ cùng với các tệp đã mã hóa. Kẻ tấn công sẽ giữ khóa riêng một cách an toàn để ngăn nạn nhân giải mã khóa AES và do đó là các tệp của họ mà không phải trả tiền chuộc. Trong công cụ giáo dục này, khóa riêng được lưu trữ cục bộ (cùng với khóa AES được mã hóa) chỉ nhằm mục đích trình diễn.

Cách sử dụng
Tạo khóa
Trước khi chạy chức năng mã hóa hoặc giải mã, chúng ta cần tạo các khóa cần thiết:

make run-crypto-key
Hai tệp sẽ được tạo cục bộ trong thư mục làm việc

Khóa AES encrypted_aes_key.bin (được mã hóa bằng khóa công khai RSA để bảo vệ khóa này), sẽ được sử dụng để mã hóa tệp.
Khóa riêng RSA rsa_private_key.pem, sẽ được sử dụng để giải mã khóa AES được mã hóa.
Lưu ý rằng khóa công khai RSA không được lưu trữ cục bộ vì có thể dễ dàng lấy được khóa riêng.
Mã hóa hoặc giải mã tệp
Sau khi tạo khóa, chúng ta có thể mã hóa hoặc giải mã tất cả các tệp trong một thư mục được chỉ định.

Mã hóa

make run-wannacry-ish-encrypt d=DIR_PATH
Khi các tệp được mã hóa, phần mở rộng .cry sẽ được thêm vào mỗi tệp được mã hóa. Nếu mã hóa được chạy trong dữ liệu thư mục mẫu, thì bạn sẽ thấy

omfg.txt.cry
sample.txt.cry
Và nội dung sẽ trông như thế này

OQ<C6><96>c/(<CC><E6><F5>6^R<)<A7><D7><D1><C0>&<BA><9D><9B>^MQ<CD>+^M<94>Co^TS#^L<95>|iS<C8>i\m^S<A6><FB>i<B8>
Giải mã

make run-wannacry-ish-decrypt d=DIR_PATH
Khi các tệp được giải mã, phần mở rộng .cry sẽ bị xóa khỏi mỗi tệp và nội dung của chúng sẽ có thể đọc được trở lại.




   
