<p align="center">
  <a href="https://www.uit.edu.vn/" title="Trường Đại học Công nghệ Thông tin" style="border: none;">
    <img src="https://i.imgur.com/WmMnSRt.png" alt="Trường Đại học Công nghệ Thông tin | University of Information Technology">
  </a>
</p>

<h1 align="center"><b>PHÁT TRIỂN ỨNG DỤNG TRÊN THIẾT BỊ DI ĐỘNG</b></h1>

## BẢNG MỤC LỤC
* [Giới thiệu môn học](#gioithieumonhoc)
* [Giảng viên hướng dẫn](#giangvien)
* [Thành viên nhóm](#thanhvien)
* [Đồ án môn học](#doan)
* [Công nghệ sử dụng](#congnghe)
* [Chức năng hệ thống](#chucnang)
* [Cài đặt và Triển khai](#caidat)

## GIỚI THIỆU MÔN HỌC
<a name="gioithieumonhoc"></a>
* **Tên môn học**: Truyền thông đa phương tiện
* **Mã môn học**: NT536
* **Lớp học**: NT536.Q11

## GIẢNG VIÊN HƯỚNG DẪN
<a name="giangvien"></a>
* ThS. **Đỗ thị Hương Lan** - *@uit.edu.vn*

## THÀNH VIÊN NHÓM
<a name="thanhvien"></a>
| STT | MSSV | Họ và Tên | Github | Email | 
| --- | --- | --- | --- | --- | 
| 1 | 23520164 | Nguyễn Hữu Cảm| [nghuucam](https://github.com/nghuucam) | 23520164@gm.uit.edu.vn | 

## ĐỒ ÁN MÔN HỌC
<a name="doan"></a>
**Tên đề tài:** Xây dựng Tổng đài thoại

**Mô tả:** Tổng đài thoại (VoIP) là tổng đài thoại dựa trên kết nối của IP thay vì mạng như thông thường được sử dụng phổ biến trong các tổng đài nội bộ của một công ty hoặc tổ chức.

## CÔNG NGHỆ SỬ DỤNG
<a name="congnghe"></a>
* **Môi trường:** Ubuntu
* **Công nghệ:** Asterisk

## CHỨC NĂNG HỆ THỐNG
<a name="chucnang"></a>
1. Tạo các số extension
− Công ty gồm 4 phòng ban :
o Phòng Giám đốc : ext. 5015 (IAX)
o Phòng nhân sự : ext. 6016 (SIP)
o Phòng kỹ thuật : ext. 7011 (IAX), ext. 7012 (SIP)
o Phòng bán hàng : ext. 8010 (SIP), ext 8016 (IAX), ext 8018 (SIP)
− Số điện thoại 0951000001 là số điện thoại ở ngoài công ty. XX là số nhóm
− Số điện thoại 0952014301 là số điện thoại public của công ty (ở ngoài muốn gọi đến các số nội bộ của công ty phải gọi qua số này).
− Số ext. 4014 là số nội bộ của công ty được dùng khi cần họp toàn công ty thông qua mạng điện thoại với password quản lý và gia nhập lần lược là : 123456 và 654321
2. Liên lạc nội bộ
− Kết nối cho các số nội bộ trong công ty liên lạc bình thường.
− Có thể họp nội bộ công ty qua điện thoại giữa tất cả các phòng.
3. Liên lạc từ trong ra ngoài
- Phải thêm số 9 trước số cần gọi để liên lạc ra ngoài công ty.
4. Liên lạc từ ngoài vào trong
− Khi cuộc gọi từ ngoài đến số public của công ty thì hệ thống asterisk sẽ phát sinh thông điệp “Chào mừng gọi đến công ty ABC, vui lòng nhấn phím 1 để kết nối với phòng bán hàng, nhấn phím 2 để được hỗ trợ về kỹ thuật, nhấn phím 3 để biết thông tin tuyển dụng, nhấn phím 4 để để lại lời nhắn hay góp ý cho Ban Giám Đốc, nhấn phím 5 để nghe lại lời chào” sau đó tùy theo lựa chọn của khách hàng mà thực hiện các thao tác sau đây :
− Người dùng nhấn phím 1:
o Phát thông điệp “Chào mừng bạn đã đến phòng bán hàng, vui lòng đợi trong giây lát để được kết nối với điện thoại viên”.
o Các số ext trong phòng bán hàng sẽ đồng loạt rung chuông.
o Nếu không có điện thoại viên nào nhấc máy, phát thông điệp “Xin lỗi hiện tại các điện thoại viên đều bận, vui lòng để lại lời nhắn sau tiếng pip hoặc thực hiện lại cuộc gọi”
− Người dùng nhấn phím 2:
o Quay số đến phòng kỹ thuật. Các số ext trong phòng kỹ thuật sẽ lần lượt rung chuông cho đến khi có kỹ thuật viên nhấc máy.
o Nếu không có điện thoại viên nào nhấc máy, phát thông điệp “Xin lỗi hiện tại các kỹ thuật viên đều bận, vui lòng chờ trong giây lát để thực hiện lại cuộc gọi”
− Người dùng nhấn phím 3: quay số đến phòng nhân sự.
− Người dùng nhấn phím 4:
o Phát thông điệp “ Xin chân thành cảm ơn bạn đã góp ý cho công ty chúng tôi, vui lòng để lại lời nhắn sau tiếng pip”.
o Phát sinh âm “pip” và bắt đầu ghi lại nội dung lời nhắn vào hộp thư thoại của phòng giám đốc.
− Khi người dùng nhấn phím 5:
o Phát lại thông điệp chào mừng như khi mới gọi vào công t
## CÀI ĐẶT VÀ TRIỂN KHAI
<a name="caidat"></a>
Đối với Máy ảo 1: 
- Truy cập vào thư mục /etc/asterisk/ trên máy ảo.
- Sao chép và ghi đè toàn bộ các tệp cấu hình từ thư mục vm-ware1 trong bộ cài đặt vào thư mục Asterisk của máy.
- Khởi chạy lại dịch vụ bằng lệnh: sudo systemctl restart asterisk.

Đối với Máy ảo 2:
- Tương tự, truy cập vào thư mục /etc/asterisk/ của máy ảo 2.
- Sử dụng các tệp cấu hình nằm trong thư mục vm-ware2 để thay thế cho các tệp mặc định.
- Khởi chạy lại dịch vụ để áp dụng thay đổi.
Lưu ý: Trước khi ghi đè, bạn nên sao lưu các file cấu hình gốc của Asterisk bằng lệnh cp để tránh mất dữ liệu quan trọng nếu có lỗi xảy ra.
