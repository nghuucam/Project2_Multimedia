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
Chào Cam, dựa trên những yêu cầu chi tiết về kịch bản tổng đài (IVR) và phân bổ extension mà bạn vừa cung cấp, mình đã hệ thống lại thành một tài liệu hướng dẫn cấu hình chuyên nghiệp. 

Bạn có thể dùng nội dung này để đưa vào báo cáo hoặc làm tài liệu hướng dẫn triển khai cho Asterisk:

---

## CHI TIẾT CẤU HÌNH HỆ THỐNG TỔNG ĐÀI

### 1. Danh sách Extension (Số nội bộ)
Hệ thống phân chia theo các phòng ban với hai giao thức **SIP** và **IAX** như sau:

| Phòng ban | Extension | Giao thức | Ghi chú |
| :--- | :--- | :--- | :--- |
| **Giám đốc** | 5015 | IAX | Nhận VoiceMail từ khách hàng |
| **Nhân sự** | 6016 | SIP | Nhận cuộc gọi hỗ trợ tuyển dụng |
| **Kỹ thuật** | 7011, 7012 | IAX, SIP | Đổ chuông xoay vòng (Round-robin) |
| **Bán hàng** | 8010, 8016, 8018 | SIP, IAX, SIP | Đổ chuông đồng loạt (Ring-all) |
| **Họp nội bộ** | **4014** | - | Password: Admin (123456), User (654321) |

**Thông tin số thuê bao bên ngoài:**
* **Số bên ngoài:** `0951000001` (Dùng để giả lập cuộc gọi vào/ra).
* **Số Public của Công ty:** `0952014301` (Đầu số tiếp nhận IVR).

---

### 2. Kịch bản Liên lạc nội bộ & Hội nghị
* **Liên lạc thông thường:** Các số nội bộ (501, 601, 701, 801) có quyền gọi trực tiếp cho nhau.
* **Hội nghị (MeetMe/ConfBridge):** * Tất cả nhân viên truy cập số **4014** để họp.
    * Yêu cầu nhập mã PIN: `654321` cho nhân viên và `123456` cho người quản lý.

---

### 3. Liên lạc ra mạng ngoài (Outbound Call)
Để thực hiện cuộc gọi ra ngoài công ty (ví dụ gọi số `0951000001`), người dùng phải tuân thủ quy tắc quay số:
> **Cú pháp:** `9` + `[Số điện thoại cần gọi]`
> *Ví dụ: Quay 90951000001 để gọi ra ngoài.*

---

### 4. Kịch bản Tương tác tự động (IVR)
Khi khách hàng gọi vào số **0952014301**, hệ thống Asterisk sẽ kích hoạt lời chào và xử lý theo các phím bấm:

#### Lời chào chính (Main Menu):
*"Chào mừng gọi đến công ty ABC, vui lòng nhấn phím 1 để kết nối với phòng bán hàng, nhấn phím 2 để được hỗ trợ về kỹ thuật, nhấn phím 3 để biết thông tin tuyển dụng, nhấn phím 4 để để lại lời nhắn hay góp ý cho Ban Giám Đốc, nhấn phím 5 để nghe lại lời chào."*

#### Xử lý phím bấm:

* **Phím 1 (Phòng Bán hàng):**
    * Phát thông báo: *"Chào mừng bạn đã đến phòng bán hàng, vui lòng đợi trong giây lát..."*
    * **Cơ chế:** Đổ chuông đồng loạt tất cả máy (8010, 8016, 8018).
    * **Nếu bận/Không nhấc máy:** Phát thông báo yêu cầu để lại lời nhắn hoặc gọi lại sau.

* **Phím 2 (Phòng Kỹ thuật):**
    * **Cơ chế:** Đổ chuông lần lượt (Linear/Round-robin) qua các số 7011, 7012.
    * **Nếu bận:** Thông báo kỹ thuật viên đang bận và mời chờ để thực hiện lại cuộc gọi.

* **Phím 3 (Phòng Nhân sự):** Kết nối trực tiếp đến Ext **6016**.

* **Phím 4 (Góp ý cho Giám đốc):**
    * Phát lời cảm ơn.
    * Sau tiếng "píp", hệ thống tự động ghi âm và chuyển vào **VoiceMail** của Ext **5015**.

* **Phím 5:** Lặp lại lời chào chính.

---

### Gợi ý cho Cam khi viết file `extensions.conf`:
Đối với yêu cầu phím 1 (đổ chuông đồng loạt) và phím 2 (đổ chuông lần lượt), bạn nhớ sử dụng lệnh `Dial` với dấu `&` cho phím 1. Ví dụ:
* **Phím 1:** `Dial(SIP/8010&IAX2/8016&SIP/8018, 20)`
* **Phím 2:** `Dial(IAX2/7011, 10)` tiếp đến `Dial(SIP/7012, 10)`

Bạn có cần mình hỗ trợ viết đoạn code mẫu cho file `extensions.conf` để thực hiện kịch bản IVR này không?

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
