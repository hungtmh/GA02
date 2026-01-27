# 📸 ĐẶC TẢ ỨNG DỤNG ALBUM ẢNH

> **Dự án**: Ứng dụng Album Ảnh cho Android  
> **Phiên bản**: 1.0  
> **Ngày cập nhật**: 27/01/2026  
> **Nền tảng**: Android  
> **Ngôn ngữ**: Java, XML

---

## 📋 MỤC LỤC

1. [Quản lý ảnh](#1-quản-lý-ảnh)
2. [Xem ảnh](#2-xem-ảnh)
3. [Chỉnh sửa ảnh](#3-chỉnh-sửa-ảnh)
4. [Album](#4-album)
5. [Yêu thích](#5-yêu-thích)
6. [Thùng rác](#6-thùng-rác)
7. [Ảnh ẩn](#7-ảnh-ẩn)
8. [Trình chiếu (Slideshow)](#8-trình-chiếu-slideshow)
9. [Tải ảnh từ URL](#9-tải-ảnh-từ-url)
10. [Giao diện](#10-giao-diện)
11. [Chia sẻ](#11-chia-sẻ)
12. [Tính năng AI](#12-tính-năng-ai)

---

## 1. QUẢN LÝ ẢNH

### 1.1 Màn hình chính
- Hiển thị tất cả ảnh trên thiết bị
- Hiển thị tiêu đề lớn "Photos" ở đầu màn hình
- Hiển thị số lượng ảnh bên dưới tiêu đề (VD: "1,234 Photos")
- Hỗ trợ kéo xuống để làm mới danh sách ảnh

### 1.2 Chế độ xem
- **Chế độ lưới (Grid View)**
  - Hiển thị ảnh theo dạng lưới 3 cột
  - Ảnh hiển thị vuông, cắt giữa (center crop)
  - Khoảng cách giữa các ảnh: 2dp
  - Không có viền, hiển thị sát nhau
  
- **Chế độ danh sách (List View)**
  - Hiển thị ảnh thu nhỏ bên trái (60x60dp, bo góc 8dp)
  - Hiển thị tên file ảnh
  - Hiển thị ngày chụp và kích thước file
  - Có đường kẻ phân cách giữa các mục
  - Có mũi tên chỉ sang phải ở cuối mỗi dòng

- **Chuyển đổi chế độ xem**
  - Sử dụng Segmented Control (2 nút Grid/List)
  - Ghi nhớ chế độ xem đã chọn khi thoát ứng dụng

### 1.3 Sắp xếp ảnh
- **Sắp xếp theo ngày**
  - Mới nhất trước (mặc định)
  - Cũ nhất trước
  
- **Sắp xếp theo tên**
  - A đến Z
  - Z đến A
  
- **Sắp xếp theo kích thước**
  - Nhỏ nhất trước
  - Lớn nhất trước

- Hiển thị menu sắp xếp dạng popup khi nhấn nút Sort
- Đánh dấu tùy chọn đang được chọn

### 1.4 Chụp ảnh
- Nút chụp ảnh (FAB) ở góc dưới bên phải màn hình
- Nhấn nút để mở ứng dụng Camera
- Sau khi chụp, ảnh tự động lưu vào thư mục Pictures/Photos
- Tự động làm mới danh sách ảnh sau khi chụp
- Tên file theo định dạng: IMG_yyyyMMdd_HHmmss.jpg

### 1.5 Trạng thái trống
- Khi không có ảnh nào, hiển thị:
  - Icon ảnh lớn ở giữa màn hình
  - Dòng chữ "No Photos"
  - Dòng hướng dẫn "Take a photo or import from library"

### 1.6 Thao tác với ảnh
- **Nhấn vào ảnh**: Mở màn hình xem ảnh chi tiết
- **Nhấn giữ ảnh**: Hiển thị menu ngữ cảnh
  - Xóa ảnh
  - Chia sẻ ảnh
  - Thêm vào Album
  - Ẩn ảnh
  - Thêm vào Yêu thích

### 1.7 Chế độ chọn nhiều ảnh
- Nhấn giữ để bắt đầu chế độ chọn
- Có thể chọn/bỏ chọn nhiều ảnh
- Hiển thị thanh công cụ với các tùy chọn:
  - Số lượng ảnh đã chọn
  - Xóa tất cả
  - Chia sẻ tất cả
  - Thêm vào Album
  - Hủy chọn

---

## 2. XEM ẢNH

### 2.1 Màn hình xem ảnh
- Hiển thị ảnh toàn màn hình
- Nền đen
- Thanh công cụ trên và dưới (ẩn/hiện khi chạm vào ảnh)

### 2.2 Thanh công cụ trên
- Nút quay lại (góc trái)
- Nút menu thêm tùy chọn (góc phải)

### 2.3 Thanh công cụ dưới
- Nút Yêu thích (thêm/bỏ yêu thích)
- Nút Chỉnh sửa (mở trình chỉnh sửa)
- Nút Chia sẻ
- Nút Xóa

### 2.4 Cử chỉ (Gestures)
- **Chạm 1 lần**: Ẩn/hiện thanh công cụ
- **Chạm 2 lần**: Phóng to/thu nhỏ (chuyển đổi giữa 1x và 2x)
- **Kéo 2 ngón tay (Pinch)**: Phóng to/thu nhỏ tùy ý (1x đến 5x)
- **Vuốt trái/phải**: Chuyển sang ảnh trước/sau
- **Vuốt xuống**: Đóng màn hình xem ảnh (có animation)
- **Nhấn giữ**: Hiển thị menu ngữ cảnh

### 2.5 Thông tin ảnh
- Nhấn nút "Info" hoặc vuốt lên để xem thông tin chi tiết
- Hiển thị các thông tin:
  - Tên file
  - Ngày chụp
  - Kích thước ảnh (width x height pixels)
  - Dung lượng file
  - Vị trí chụp (nếu có)
  - Thiết bị chụp (nếu có)

### 2.6 Điều hướng ảnh
- Hỗ trợ vuốt để chuyển ảnh liên tục
- Hiển thị indicator vị trí ảnh hiện tại (VD: 3/45)
- Animation mượt mà khi chuyển ảnh

---

## 3. CHỈNH SỬA ẢNH

### 3.1 Màn hình chỉnh sửa
- Nút Hủy ở góc trái trên
- Nút Lưu ở góc phải trên
- Vùng xem trước ảnh ở giữa
- Thanh công cụ chỉnh sửa ở dưới
- Panel tùy chọn công cụ ở dưới cùng

### 3.2 Công cụ Xoay (Rotate)
- **Xoay trái**: Xoay ảnh 90° ngược chiều kim đồng hồ
- **Xoay phải**: Xoay ảnh 90° theo chiều kim đồng hồ
- **Lật ngang**: Lật ảnh theo chiều ngang (mirror)
- **Lật dọc**: Lật ảnh theo chiều dọc

### 3.3 Công cụ Bộ lọc (Filter)
- Hiển thị danh sách filter theo chiều ngang, có thể cuộn
- Mỗi filter có ảnh preview nhỏ và tên bên dưới
- Nhấn vào filter để áp dụng ngay lên ảnh xem trước
- **Danh sách 10 bộ lọc:**
  1. **No Effect** - Không có hiệu ứng (ảnh gốc)
  2. **Grayscale** - Đen trắng
  3. **Vintage** - Hiệu ứng cổ điển, tone nâu vàng
  4. **Cream** - Tone kem ấm áp
  5. **Forest** - Tone xanh lá, tự nhiên
  6. **Cozy** - Ấm áp, độ tương phản thấp
  7. **Blossom** - Tone hồng nhẹ nhàng
  8. **Evergreen** - Xanh đậm, tươi mát
  9. **Auto** - Tự động cân bằng màu sắc
  10. **Sharpen** - Làm nét ảnh

### 3.4 Công cụ Vẽ (Brush)
- **Kích thước cọ**: Thanh trượt điều chỉnh từ 5dp đến 50dp
- **Bảng màu**: 10 màu cơ bản
  - Đỏ, Cam, Vàng, Xanh lá, Xanh dương
  - Tím, Đen, Trắng, Nâu, Hồng
- **Độ trong suốt**: Thanh trượt điều chỉnh từ 20% đến 100%
- **Nút Undo**: Hoàn tác nét vẽ cuối cùng
- **Nút Xóa tất cả**: Xóa toàn bộ nét vẽ
- **Nút Tẩy**: Chuyển sang chế độ xóa nét vẽ

### 3.5 Công cụ Cắt (Crop)
- Khung cắt có thể kéo 4 góc và 4 cạnh
- Có thể di chuyển khung cắt
- Vùng ngoài khung cắt tối hơn
- **Tỷ lệ khung hình:**
  - Tự do (Free) - không ràng buộc
  - Vuông (1:1)
  - Dọc (3:4)
  - Ngang (4:3)
  - Màn hình rộng (16:9)
  - Story (9:16)

### 3.6 Lưu ảnh đã chỉnh sửa
- Hiển thị dialog hỏi cách lưu:
  - Lưu thành ảnh mới
  - Ghi đè lên ảnh gốc
- Tùy chọn chất lượng ảnh: Cao (95%), Trung bình (80%), Thấp (60%)
- Hiển thị thông báo khi lưu thành công

---

## 4. ALBUM

### 4.1 Màn hình Album
- Tiêu đề lớn "Albums"
- Hiển thị tổng số album
- Nút tạo album mới ở góc phải

### 4.2 Hiển thị Album
- Hiển thị dạng lưới 2 cột
- Mỗi album hiển thị:
  - Ảnh bìa (ảnh đầu tiên hoặc ảnh được chọn làm bìa)
  - Hiệu ứng xếp chồng 3 ảnh
  - Tên album
  - Số lượng ảnh trong album

### 4.3 Album hệ thống (mặc định)
- **Favorites (Yêu thích)**: Icon ngôi sao, chứa ảnh được đánh dấu yêu thích
- **Trash (Thùng rác)**: Icon thùng rác, chứa ảnh đã xóa
- **Hidden (Ảnh ẩn)**: Icon khóa, chứa ảnh ẩn (cần mật khẩu để xem)
- Các album hệ thống không thể xóa hoặc đổi tên

### 4.4 Tạo Album mới
- Nhấn nút "+" để tạo album
- Hiển thị dialog nhập tên album
- Tên album không được trống
- Tên album không được trùng với album đã có
- Sau khi tạo, chuyển đến màn hình chọn ảnh để thêm vào album

### 4.5 Chi tiết Album
- Thanh tiêu đề hiển thị tên album và số ảnh
- Nút quay lại ở góc trái
- Nút menu ở góc phải
- Hiển thị ảnh dạng lưới 3 cột
- Nút "Thêm ảnh" ở dưới
- Nút "Chọn" để vào chế độ chọn nhiều ảnh

### 4.6 Thao tác với Album
- **Nhấn giữ album**: Hiển thị menu
  - Đổi tên album
  - Đổi ảnh bìa
  - Chia sẻ album
  - Xóa album
- **Xóa album**: Chỉ xóa album, không xóa ảnh gốc

### 4.7 Thêm ảnh vào Album
- Chọn từ màn hình chọn ảnh
- Hiển thị tất cả ảnh với checkbox
- Có thể chọn nhiều ảnh cùng lúc
- Nút "Done" hiển thị số ảnh đã chọn
- Ảnh đã có trong album sẽ được đánh dấu

### 4.8 Xóa ảnh khỏi Album
- Nhấn giữ ảnh trong album → "Xóa khỏi album"
- Chỉ xóa khỏi album, không xóa ảnh gốc
- Hiển thị dialog xác nhận

---

## 5. YÊU THÍCH

### 5.1 Truy cập Yêu thích
- Tab "Favorites" trong Bottom Navigation
- Hoặc từ album "Favorites" trong màn hình Albums

### 5.2 Màn hình Yêu thích
- Tiêu đề "Favorites" với icon ngôi sao
- Hiển thị số lượng ảnh yêu thích
- Hiển thị ảnh dạng lưới 3 cột
- Sắp xếp theo thời gian thêm vào yêu thích (mới nhất trước)

### 5.3 Thêm vào Yêu thích
- Nhấn icon trái tim trống (♡) → Chuyển thành trái tim đỏ (❤️)
- Có animation nhảy khi thêm yêu thích
- Có thể thêm từ:
  - Màn hình xem ảnh
  - Menu ngữ cảnh (nhấn giữ ảnh)
  - Chế độ chọn nhiều ảnh

### 5.4 Bỏ Yêu thích
- Nhấn icon trái tim đỏ (❤️) → Chuyển về trái tim trống (♡)
- Ảnh sẽ biến mất khỏi danh sách Yêu thích
- Ảnh vẫn còn trong thư viện chính

### 5.5 Yêu thích nhanh
- Chạm 2 lần vào ảnh trong màn hình xem → Thêm/bỏ yêu thích
- Hiển thị animation trái tim lớn ở giữa màn hình

---

## 6. THÙNG RÁC

### 6.1 Màn hình Thùng rác
- Tiêu đề "Trash" với icon thùng rác
- Hiển thị số lượng ảnh trong thùng rác
- Thông báo "Items will be deleted after 30 days" (Ảnh sẽ bị xóa sau 30 ngày)
- Hiển thị ảnh dạng lưới 3 cột

### 6.2 Hiển thị ảnh trong Thùng rác
- Mỗi ảnh hiển thị số ngày còn lại trước khi bị xóa vĩnh viễn
- VD: "28d", "15d", "7d", "1d"
- Ảnh sắp hết hạn (< 3 ngày) hiển thị màu đỏ

### 6.3 Xóa ảnh vào Thùng rác
- Từ thư viện chính: Nhấn giữ → Xóa
- Từ màn hình xem ảnh: Nhấn nút Xóa
- Hiển thị dialog xác nhận: "Move to Trash?"
- Ảnh được di chuyển vào Thùng rác, không xóa ngay

### 6.4 Khôi phục ảnh
- Nhấn vào ảnh trong Thùng rác → Menu
- Chọn "Restore" để khôi phục
- Ảnh quay lại thư viện chính và các album trước đó
- Có thể khôi phục nhiều ảnh cùng lúc

### 6.5 Xóa vĩnh viễn
- **Xóa từng ảnh**: Nhấn vào ảnh → "Delete Permanently"
- **Xóa tất cả**: Nhấn nút "Empty Trash"
- Hiển thị dialog cảnh báo: "This action cannot be undone" (Hành động này không thể hoàn tác)
- Yêu cầu xác nhận trước khi xóa

### 6.6 Tự động xóa
- Ảnh trong Thùng rác tự động bị xóa sau 30 ngày
- Hệ thống kiểm tra và xóa mỗi ngày
- Không có thông báo khi tự động xóa

### 6.7 Các nút chức năng
- **Restore All**: Khôi phục tất cả ảnh trong Thùng rác
- **Empty Trash**: Xóa vĩnh viễn tất cả ảnh

---

## 7. ẢNH ẨN

### 7.1 Tính năng Ảnh ẩn
- Cho phép ẩn ảnh riêng tư
- Ảnh ẩn không hiển thị trong thư viện chính
- Cần mật khẩu để truy cập ảnh ẩn
- Mật khẩu được mã hóa SHA-256

### 7.2 Thiết lập mật khẩu lần đầu
- Khi truy cập album Hidden lần đầu, yêu cầu tạo mật khẩu
- Nhập mật khẩu mới (tối thiểu 4 ký tự)
- Nhập lại mật khẩu để xác nhận
- Hiển thị thông báo nếu 2 mật khẩu không khớp
- Lưu mật khẩu đã mã hóa vào bộ nhớ an toàn

### 7.3 Nhập mật khẩu
- Hiển thị màn hình nhập mật khẩu khi truy cập album Hidden
- Bàn phím số tùy chỉnh (0-9)
- Hiển thị dấu chấm (●) cho mỗi ký tự đã nhập
- Nút xóa (backspace)
- Link "Quên mật khẩu?" ở dưới

### 7.4 Xác thực mật khẩu
- So sánh mật khẩu nhập vào với mật khẩu đã lưu (sau khi mã hóa)
- Nếu đúng: Mở album Hidden
- Nếu sai: Hiển thị thông báo "Incorrect password", rung điện thoại
- Sau 5 lần sai: Khóa 30 giây trước khi thử lại

### 7.5 Ẩn ảnh
- Từ thư viện chính: Nhấn giữ ảnh → "Hide"
- Hiển thị dialog xác nhận
- Ảnh được di chuyển vào album Hidden
- Ảnh không còn hiển thị trong thư viện chính và các album khác

### 7.6 Bỏ ẩn ảnh
- Trong album Hidden: Nhấn giữ ảnh → "Unhide"
- Ảnh quay lại thư viện chính
- Có thể bỏ ẩn nhiều ảnh cùng lúc

### 7.7 Đổi mật khẩu
- Vào Settings → "Change Hidden Password"
- Nhập mật khẩu hiện tại
- Nhập mật khẩu mới
- Xác nhận mật khẩu mới
- Hiển thị thông báo thành công

### 7.8 Quên mật khẩu
- Nhấn "Forgot Password?" trong màn hình nhập mật khẩu
- Cảnh báo: Đặt lại mật khẩu sẽ xóa tất cả ảnh ẩn
- Yêu cầu xác nhận trước khi đặt lại
- Sau khi xác nhận: Xóa tất cả ảnh ẩn và cho phép tạo mật khẩu mới

---

## 8. TRÌNH CHIẾU (SLIDESHOW)

### 8.1 Khởi động Slideshow
- Từ màn hình xem ảnh: Nhấn menu → "Slideshow"
- Từ album: Nhấn menu → "Slideshow"
- Bắt đầu từ ảnh hiện tại hoặc ảnh đầu tiên

### 8.2 Màn hình Slideshow
- Hiển thị ảnh toàn màn hình
- Nền đen
- Tự động chuyển ảnh theo thời gian đã cài đặt
- Thanh điều khiển ở dưới (ẩn/hiện khi chạm màn hình)

### 8.3 Thanh điều khiển
- **Nút Play/Pause**: Tạm dừng/tiếp tục slideshow
- **Nút Previous**: Quay lại ảnh trước
- **Nút Next**: Chuyển sang ảnh tiếp theo
- **Nút Settings**: Mở cài đặt slideshow
- **Nút Exit**: Thoát slideshow
- Thanh tiến trình (progress dots)
- Hiển thị vị trí ảnh hiện tại (VD: 3/45)

### 8.4 Cài đặt Slideshow
- **Thời gian mỗi ảnh:**
  - 2 giây
  - 3 giây (mặc định)
  - 5 giây
  - 10 giây

- **Hiệu ứng chuyển cảnh:**
  - Không có (None)
  - Mờ dần (Fade) - mặc định
  - Trượt (Slide)
  - Phóng to (Zoom)

- **Lặp lại (Loop):**
  - Bật: Khi hết ảnh cuối, quay lại ảnh đầu
  - Tắt: Dừng khi đến ảnh cuối

- **Xáo trộn (Shuffle):**
  - Bật: Hiển thị ảnh ngẫu nhiên
  - Tắt: Hiển thị theo thứ tự

### 8.5 Tương tác khi đang chạy Slideshow
- Chạm màn hình: Hiện thanh điều khiển (tự ẩn sau 3 giây)
- Vuốt trái/phải: Chuyển ảnh thủ công
- Nhấn nút âm lượng: Không làm gì (để tránh nhầm)

---

## 9. TẢI ẢNH TỪ URL

### 9.1 Màn hình tải ảnh từ URL
- Tiêu đề "Import from URL"
- Ô nhập URL
- Nút "Preview" để xem trước ảnh
- Vùng hiển thị ảnh preview
- Hiển thị thông tin ảnh (kích thước, dung lượng)
- Nút "Download" để tải ảnh

### 9.2 Kiểm tra kết nối mạng
- Kiểm tra kết nối Internet trước khi tải
- Nếu không có mạng: Hiển thị thông báo "No internet connection"
- Hỗ trợ WiFi và dữ liệu di động

### 9.3 Xác thực URL
- Kiểm tra định dạng URL hợp lệ
- Kiểm tra đuôi file ảnh hỗ trợ: .jpg, .jpeg, .png, .gif, .webp, .bmp
- Nếu URL không hợp lệ: Hiển thị thông báo lỗi

### 9.4 Xem trước ảnh
- Nhấn "Preview" để tải và hiển thị ảnh
- Hiển thị loading indicator khi đang tải
- Hiển thị ảnh preview nếu tải thành công
- Hiển thị thông tin:
  - Kích thước file (ước tính)
  - Độ phân giải ảnh

### 9.5 Tải và lưu ảnh
- Nhấn "Download" để tải ảnh về thiết bị
- Hiển thị thanh tiến trình khi đang tải
- Lưu ảnh vào thư mục Pictures/Photos
- Tên file: IMG_[timestamp].jpg
- Hiển thị thông báo khi tải thành công
- Tự động làm mới thư viện ảnh

### 9.6 Xử lý lỗi
- URL không tồn tại: "Image not found"
- Lỗi mạng: "Network error. Please try again"
- File quá lớn: "File size exceeds limit" (giới hạn 50MB)
- Định dạng không hỗ trợ: "Unsupported image format"

---

## 10. GIAO DIỆN

### 10.1 Chế độ sáng (Light Mode)
- Nền chính: Trắng (#FFFFFF)
- Nền phụ: Xám nhạt (#F2F2F7)
- Chữ chính: Đen (#1C1C1E)
- Chữ phụ: Xám (#8E8E93)
- Màu nhấn: Xanh Apple (#007AFF)
- Đường kẻ: Xám nhạt (#E5E5EA)

### 10.2 Chế độ tối (Dark Mode)
- Nền chính: Đen (#000000)
- Nền phụ: Xám đậm (#1C1C1E)
- Chữ chính: Trắng (#FFFFFF)
- Chữ phụ: Xám (#8E8E93)
- Màu nhấn: Xanh sáng (#0A84FF)
- Đường kẻ: Xám đậm (#38383A)

### 10.3 Chuyển đổi chế độ
- **Tự động**: Theo cài đặt hệ thống (mặc định)
- **Luôn sáng**: Chế độ sáng cố định
- **Luôn tối**: Chế độ tối cố định
- Cài đặt trong Settings → Appearance → Dark Mode

### 10.4 Bottom Navigation
- 5 tab chính:
  1. **Photos**: Thư viện ảnh chính
  2. **Albums**: Quản lý album
  3. **Favorites**: Ảnh yêu thích
  4. **AI**: Tính năng AI
  5. **Settings**: Cài đặt ứng dụng
- Tab đang chọn có màu xanh (#007AFF)
- Tab không chọn có màu xám

### 10.5 Màn hình Settings
- **APPEARANCE (Giao diện)**
  - Dark Mode: Toggle bật/tắt
  - Grid Columns: Chọn 3, 4 hoặc 5 cột

- **PRIVACY (Riêng tư)**
  - Change Hidden Password: Đổi mật khẩu ảnh ẩn
  - Empty Trash: Dọn sạch thùng rác

- **STORAGE (Bộ nhớ)**
  - Clear Cache: Xóa bộ nhớ đệm (hiển thị dung lượng)

- **ABOUT (Thông tin)**
  - Version: Hiển thị phiên bản ứng dụng
  - Privacy Policy: Chính sách bảo mật
  - Terms of Service: Điều khoản sử dụng

### 10.6 Thiết kế chung
- Theo phong cách Apple iOS
- Font chữ: San Francisco (hoặc Roboto trên Android)
- Bo góc các phần tử: 8dp - 12dp
- Padding tiêu chuẩn: 16dp
- Animation mượt mà, tự nhiên
- Haptic feedback (rung nhẹ) cho các thao tác quan trọng

---

## 11. CHIA SẺ

### 11.1 Menu chia sẻ
- Hiển thị bottom sheet với các tùy chọn chia sẻ
- Hàng 1: Các ứng dụng chia sẻ nhanh (Messages, Email, Facebook, Instagram, X/Twitter)
- Hàng 2: Các hành động khác (Save, Copy, Print, Drive, More)
- Tùy chọn "Set as Wallpaper" riêng biệt

### 11.2 Chia sẻ ảnh đơn
- Chọn ảnh → Nút Share
- Mở menu chia sẻ hệ thống Android
- Chia sẻ file ảnh gốc

### 11.3 Chia sẻ nhiều ảnh
- Vào chế độ chọn nhiều → Chọn các ảnh → Nút Share
- Chia sẻ tất cả ảnh đã chọn
- Một số ứng dụng có thể giới hạn số ảnh

### 11.4 Đặt làm hình nền
- Chọn ảnh → Menu → "Set as Wallpaper"
- Mở trình đặt hình nền hệ thống
- Tùy chọn:
  - Màn hình chính (Home screen)
  - Màn hình khóa (Lock screen)
  - Cả hai

### 11.5 Sao chép ảnh
- Chọn ảnh → Menu → "Copy"
- Sao chép ảnh vào clipboard
- Có thể dán vào các ứng dụng khác

### 11.6 Chia sẻ Album
- Trong album → Menu → "Share Album"
- Chia sẻ tất cả ảnh trong album
- Hoặc tạo link chia sẻ (nếu có tích hợp cloud)

---

## 12. TÍNH NĂNG AI

### 12.1 Gắn thẻ tự động (Auto Tagging)
- Tự động phân tích nội dung ảnh
- Gắn các tag mô tả (VD: Beach, Ocean, Sunny, Palm Tree)
- Hiển thị tag trong phần thông tin ảnh
- Cho phép tìm kiếm theo tag
- Hiển thị độ chính xác (VD: 92%)

### 12.2 Nhận diện khuôn mặt (Face Detection)
- Tự động phát hiện khuôn mặt trong ảnh
- Đánh dấu vị trí khuôn mặt
- Nhóm các ảnh có cùng người
- Cho phép đặt tên cho từng người

### 12.3 Album theo người (People Album)
- Tự động tạo album cho mỗi người được nhận diện
- Hiển thị ảnh đại diện (ảnh mặt rõ nhất)
- Hiển thị tên (nếu đã đặt) hoặc "Unknown"
- Hiển thị số lượng ảnh có người đó
- Cho phép gộp/tách người bị nhận nhầm

### 12.4 Tìm kiếm thông minh (Smart Search)
- Tìm kiếm bằng ngôn ngữ tự nhiên
- Ví dụ tìm kiếm:
  - "photos at beach" → Ảnh có tag beach, ocean, sand
  - "selfies" → Ảnh selfie
  - "photos with John" → Ảnh có mặt John
  - "blue sky" → Ảnh có bầu trời xanh
  - "food photos" → Ảnh đồ ăn
- Hiển thị gợi ý tìm kiếm
- Lưu lịch sử tìm kiếm gần đây

### 12.5 Nhận diện chữ (OCR)
- Nhận diện và trích xuất chữ trong ảnh
- Hỗ trợ ảnh chụp màn hình, tài liệu, biển hiệu
- Hiển thị text đã nhận diện
- Các hành động với text:
  - Sao chép (Copy)
  - Tìm kiếm (Search)
  - Chia sẻ (Share)

### 12.6 Xóa nền (Background Removal)
- Tự động tách chủ thể khỏi nền
- Xem trước kết quả trước và sau
- Tùy chọn màu nền:
  - Trong suốt (Transparent)
  - Trắng
  - Đen
  - Màu tùy chỉnh
- Lưu ảnh đã xóa nền

### 12.7 Tự động cải thiện (Auto Enhance)
- Tự động điều chỉnh:
  - Độ sáng (Brightness)
  - Độ tương phản (Contrast)
  - Độ bão hòa (Saturation)
  - Độ nét (Sharpness)
  - Nhiệt độ màu (Temperature)
- Một chạm để áp dụng
- Có thể điều chỉnh thủ công từng thông số
- Nút Reset để hoàn tác

### 12.8 Phân loại cảnh (Scene Detection)
- Tự động phân loại ảnh theo cảnh:
  - Beach (Biển)
  - Mountain (Núi)
  - City (Thành phố)
  - Nature (Thiên nhiên)
  - Food (Đồ ăn)
  - People (Con người)
  - Pet (Thú cưng)
  - Night (Ban đêm)
  - Document (Tài liệu)
  - Art (Nghệ thuật)
- Tự động tạo album theo loại cảnh
- Hiển thị trong mục "Auto Albums"

### 12.9 Tab AI trong Bottom Navigation
- Hiển thị các tính năng AI chính
- **People**: Album theo người
- **Places**: Ảnh theo địa điểm (nếu có GPS)
- **Things**: Ảnh theo đối tượng (xe, động vật, đồ vật...)
- **Text**: Ảnh có chứa chữ
- **Smart Search**: Thanh tìm kiếm thông minh

---

## 📋 GHI CHÚ CHO TEAM PHÁT TRIỂN

### Thứ tự ưu tiên phát triển

| Sprint | Tính năng | Mức độ |
|--------|-----------|--------|
| 1 | Quản lý ảnh (Grid/List, Sort) | Quan trọng |
| 2 | Xem ảnh (Zoom, Swipe) | Quan trọng |
| 3 | Album (Tạo, Xóa, Thêm ảnh) | Cao |
| 4 | Yêu thích, Thùng rác | Cao |
| 5 | Chỉnh sửa (Xoay, Cắt) | Cao |
| 6 | Chỉnh sửa (Filter, Brush) | Trung bình |
| 7 | Ảnh ẩn, Mật khẩu | Trung bình |
| 8 | Slideshow | Trung bình |
| 9 | Chia sẻ, Hình nền | Trung bình |
| 10 | Tính năng AI | Thấp |

### Yêu cầu kỹ thuật
- Android tối thiểu: Android 8.0 (API 26)
- Android mục tiêu: Android 14 (API 34)
- Ngôn ngữ: Java
- Database: Room (SQLite)
- Image loading: Glide
- AI/ML: ML Kit (Google)
- Architecture: MVVM

---

*Phiên bản tài liệu: 1.0*  
*Ngày tạo: 27/01/2026*  
*Tác giả: Team Phát triển*
