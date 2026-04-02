# Phân tích Yêu cầu Dư án: Diễn đàn học tập

## 1. Danh sách các Yêu cầu chức năng (Functional Requirements - FRs)

Dựa trên tài liệu `project-requirements.txt`, dưới đây là danh sách các yêu cầu chức năng (FRs) được ký hiệu từ FE-01 đến FE-34:

### Nhóm tính năng dành cho Khách & Người dùng cơ bản
*   **FE-01**: Khám phá nội dung công khai 
*   **FE-02**: Tìm kiếm và duyệt tài liệu cơ bản
*   **FE-03**: Xem trước (Preview)
*   **FE-04**: Tiếp cận tri thức (Blog/Tin tức)
*   **FE-05**: Tương tác xã hội cơ bản (Chia sẻ link)
*   **FE-06**: Đăng ký/Đăng nhập (SSO)

### Nhóm tính năng dành cho Người dùng đã đăng nhập (Sinh viên/Học sinh)
*   **FE-07**: Tìm kiếm và lọc nâng cao
*   **FE-08**: Quản lý bộ sưu tập cá nhân
*   **FE-09**: Cá nhân hóa đề xuất (theo trường/ngành)
*   **FE-10**: Theo dõi tác giả
*   **FE-11**: Chat với AI từ tài liệu
*   **FE-12**: Tóm tắt tài liệu thông minh (AI)
*   **FE-13**: Đánh giá và bình luận
*   **FE-14**: Đóng góp tài liệu và chia sẻ
*   **FE-15**: Báo cáo vi phạm
*   **FE-16**: Nâng cấp tài khoản Premium
*   **FE-17**: Mua lẻ tài liệu (Điểm thưởng/Tiền)

### Nhóm tính năng dành cho Cộng tác viên (CTV) & Giảng viên
*   **FE-18**: Quản lý nội dung cá nhân (CTV)
*   **FE-19**: Đăng tải nội dung có xác thực (Giảng viên)
*   **FE-20**: Tương tác với người học (CTV/Giảng viên)
*   **FE-21**: Bảng điều khiển doanh thu và thống kê (CTV)
*   **FE-22**: Quản lý ví doanh thu và rút tiền (CTV)

### Nhóm tính năng dành cho Quản trị viên (Admin)
*   **FE-23**: Quản lý tài khoản người dùng (Quản trị viên)
*   **FE-24**: Phân quyền hệ thống (Quản trị viên)
*   **FE-25**: Kiểm duyệt tài liệu (Quản trị viên/Người kiểm duyệt)
*   **FE-26**: Xử lý báo cáo vi phạm (Quản trị viên/Người kiểm duyệt)
*   **FE-27**: Quản lý danh mục học thuật (Quản trị viên)
*   **FE-28**: Quản lý nội dung quảng bá (Quản trị viên)
*   **FE-29**: Bảng điều khiển tổng quan doanh thu (Quản trị viên)
*   **FE-30**: Quản lý thanh toán và hoa hồng (Quản trị viên)
*   **FE-31**: Quản lý gian lận và khiếu nại (Quản trị viên)
*   **FE-32**: Quản lý cấu hình hệ thống (Quản trị viên)
*   **FE-33**: Giám sát và Bảo mật (Quản trị viên/DevOps)
*   **FE-34**: Sao lưu và Khôi phục (Quản trị viên/DevOps)

---

## 2. Bảng ánh xạ màn hình (Screen Mapping Table)

Dựa trên các chức năng hệ thống ở trên, thực hiện ánh xạ cụ thể những tính năng với các màn hình giao diện (Screens) dự kiến tương ứng:

| Tên màn hình (Screen)            | Các tính năng (FRs) tích hợp | Mô tả ngắn gọn                                                                 |
| :---                             | :--- | :--- |
| **Màn hình Trang chủ**            | FE-01, FE-09, FE-28 | Hiển thị nội dung công khai, các tài liệu nổi bật, banner quảng bá, và đề xuất cá nhân hóa theo ngành/trường. |
| **Màn hình Xác thực**             | FE-06 | Giao diện đăng ký, đăng nhập hệ thống qua Email/SSO (Google, Microsoft).       |
| **Màn hình Tìm kiếm & Khám phá** | FE-02, FE-07 | Nơi nhập từ khóa, sử dụng bộ lọc nâng cao (cấp bậc, trường, môn học) để duyệt xuất tài liệu. |
| **Màn hình Chi tiết tài liệu**    | FE-03, FE-05, FE-11, FE-12, FE-13, FE-15, FE-17 | Nơi hiển thị thông tin tài liệu, cho phép xem trước, chat AI, tóm tắt, thả bình luận, báo cáo vi phạm và mua lẻ. |
| **Màn hình Tin tức / Blog**       | FE-04 | Nơi hiển thị các bài viết chia sẻ kinh nghiệm học tập.                         |
| **Màn hình Upload / Đóng góp**    | FE-14, FE-18, FE-19 | Cung cấp công cụ upload tài liệu, thiết lập giá (cho CTV) hoăc đăng tải xác thực cho giảng viên. |
| **Màn hình Hồ sơ (User Profile)** | FE-08, FE-10, FE-16 | Quản lý bộ sưu tập cá nhân, theo dõi tác giả và giao diện nâng cấp Premium. |
| **Trang Dashboard CTV/Creator**   | FE-20, FE-21, FE-22 | Dành cho người sáng tạo nội dung quản lý các phản hồi, theo dõi doanh thu và rút tiền từ ví nội bộ. |
| **Trang Dashboard Quản trị/Admin** | FE-23, FE-24, FE-25, FE-26, FE-27, FE-29, FE-30, FE-31, FE-32, FE-33, FE-34 | Dashboard dành cho Ban quản trị quản lý người dùng, nội dung kiểm duyệt, tài chính, báo cáo, và giám sát bảo mật hệ thống. |
