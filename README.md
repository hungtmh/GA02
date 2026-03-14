# WEEKLY REPORT
**Week 2, 07/03/2026 – 14/03/2026**

**I. GROUP INFORMATION:**
- **Group 06**
- **Project name:** Food Application
- **Prepared by:** Trần Mạnh Hùng
- **Members:**
  - 23127033 – Bùi Dương Duy Cường
  - 23127391 – Nguyễn Anh Khoa
  - 23127195 – Trần Mạnh Hùng
  - 23127060 – Ninh Văn Khải
  - 23127259 – Nguyễn Tấn Thắng
- **Meeting date:** 12/03/2026
- **All members are present.**

**II. ACHIEVEMENTS SINCE LAST WEEK:**
Dưới đây là bảng tổng hợp liền mạch toàn bộ các chức năng đã được lập trình và tích hợp thành công vào dự án tính đến thời điểm hiện tại:

| STT | Tính năng | Mô tả chi tiết các công việc đã hoàn thành | Người phụ trách | Tiến độ | Hạn hoàn thành |
| --- | --- | --- | --- | --- | --- |
| 1 | Quản lý tài khoản | Hoàn thiện luồng đăng nhập, đăng ký, chức năng quên và đặt lại mật khẩu (gửi mã xác thực qua Email bằng giao thức SMTP), đổi mật khẩu (Custom Auth), cập nhật hồ sơ cá nhân và đăng xuất. | Trần Mạnh Hùng | 100% | 08/03/2026 |
| 2 | Tìm kiếm món ăn | Tìm kiếm món ăn bằng từ khóa, bộ lọc theo danh mục món ăn. Hệ thống tự động lưu trữ và cho phép người dùng xóa lịch sử tìm kiếm. | Trần Mạnh Hùng | 100% | 12/03/2026 |
| 3 | Sắp xếp danh sách | Xây dựng bộ nút lọc hiển thị trực quan cho phép người dùng sắp xếp kết quả tìm kiếm theo: giá từ thấp đến cao, giá từ cao xuống thấp, đánh giá cao nhất và món ăn mới nhất. | Trần Mạnh Hùng | 100% | 14/03/2026 |
| 4 | Thông tin liên hệ | Xây dựng trang liên hệ tích hợp các giao thức kết nối trực tiếp (gọi Điện thoại, gửi Email, mở Facebook, Zalo, Skype, YouTube) và nhúng Google Maps có chức năng xem và chỉ đường. | Trần Mạnh Hùng | 80% | 11/03/2026 |
| 5 | Món yêu thích | Cho phép người dùng thêm hoặc bỏ món ăn khỏi danh sách yêu thích ngay trên giao diện danh sách và chi tiết món. Tích hợp trang chuyên biệt trong mục Tài khoản để quản lý các món đã lưu. | Trần Mạnh Hùng | 100% | 14/03/2026 |
| 6 | Giao diện trang chủ | Xây dựng thành công Slideshow giới thiệu các món ăn phổ biến (tự động cuộn slide) và danh sách hiển thị các món ăn được gợi ý cho người dùng. | Bùi Dương Duy Cường | 100% | 09/03/2026 |
| 7 | Chi tiết món ăn | Trình bày đầy đủ thông tin hình ảnh, tên món, giá niêm yết và giá khuyến mãi, điểm đánh giá, mô tả. Cho phép tùy chỉnh số lượng hiển thị linh hoạt trước khi thêm vào giỏ. | Bùi Dương Duy Cường | 100% | 10/03/2026 |
| 8 | Đánh giá và nhận xét | Hiển thị các bài nhận xét của người dùng khác. Thiết kế hộp thoại (Dialog) để người dùng có thể gửi đánh giá mức độ hài lòng (theo sao) cùng văn bản bình luận. | Bùi Dương Duy Cường | 100% | 12/03/2026 |
| 9 | Quản lý giỏ hàng | Xử lý logic đưa món ăn vào giỏ, cập nhật tổng tiền theo thời gian thực khi tăng/giảm số lượng. Hỗ trợ thao tác xóa từng món riêng lẻ hoặc dọn dẹp toàn bộ giỏ hàng với thông báo xác nhận. | Nguyễn Anh Khoa | 100% | 07/03/2026 |
| 10 | Đặt hàng và thanh toán | Trích xuất thông tin khách hàng từ hồ sơ cá nhân để điền sẵn vào đơn hàng. Ghi nhận thành công đơn trên cơ sở dữ liệu, cấp mã đơn và áp dụng phương thức thanh toán tiền mặt khi nhận hàng (COD). | Nguyễn Anh Khoa | 70% | 12/03/2026 |
| 11 | Lịch sử mua hàng | Phân loại đơn hàng theo các thẻ trạng thái (Chờ xác nhận, Chờ chế biến, Đã phục vụ, Đã hủy). Mở tính năng cho phép người dùng tự hủy đơn khi đơn hàng vẫn còn đang chờ xác nhận. | Nguyễn Anh Khoa | 80% | 14/03/2026 |
| 12 | Tiện ích món ăn (Admin) | Giao diện cho quản trị viên thêm mới, chỉnh sửa, xóa và tìm kiếm món ăn. Cho phép kích hoạt các thẻ trạng thái như tỷ lệ giảm giá, tính khả dụng và đưa vào danh sách đề xuất. | Nguyễn Tấn Thắng | 100% | 08/03/2026 |
| 13 | Quản lý duyệt đơn (Admin) | Tạo bảng tổng hợp các đơn mua của hệ thống. Thay thế thao tác menu đổ xuống bằng thao tác nút bấm trực tiếp và nhanh chóng hơn khi thay đổi trạng thái (Xác nhận, Phục vụ, Hủy đơn). | Nguyễn Tấn Thắng | 90% | 13/03/2026 |
| 14 | Thống kê doanh thu (Admin) | Xây dựng bộ lọc tính toán doanh thu bán ra theo từng ngày cụ thể hoặc theo một khoảng thời gian nhất định do quản trị viên chọn. Thống kê và hiển thị danh sách các món ăn có lượt bán cao nhất. | Nguyễn Tấn Thắng | 90% | 14/03/2026 |
| 15 | Quản lý phản hồi (Admin) | Danh sách tiếp nhận mọi nhận xét và đánh giá của khách hàng. Phân quyền cho quản trị viên đọc, rà soát và xóa các nội dung phản hồi. | Ninh Văn Khải | 100% | 09/03/2026 |
| 16 | Phân tích AI Insights (Admin) | Sử dụng AI để phân tích sắc thái biểu cảm của các nhận xét từ người dùng (Tích cực, tiêu cực, trung lập). Trực quan hóa dữ liệu bằng Dashboard và gợi ý các xu hướng món ăn sắp tới. | Ninh Văn Khải | 50% | 13/03/2026 |

**III. ISSUES AND IMPACTS:**
- Các tính năng nâng cao (Sort món ăn mới nhất/giá, Contact page, Danh sách yêu thích) mới được triển khai và đang cần kiểm thử thêm (tức là phải thêm nhiều món ăn mới test được).
- Tích hợp Thanh toán và gửi Thông báo đẩy đang chậm hơn dự kiến.
- Tính năng AI hiện chỉ có giao diện chưa có dữ liệu, nhóm đang cố gắng xây dựng dữ liệu để train AI.

**IV. GOALS FOR NEXT WEEK**

| Hạng mục (Item) | Mô tả chi tiết (Description) | Hạn hoàn thành (Due Date) | Người phụ trách (Responsibility) |
| --- | --- | --- | --- |
| Train AI | Cố gắng làm cho AI có thể đưa ra dự đoán và phân tích bằng dữ liệu thực tế. | 21/03/2026 | Ninh Văn Khải |
| Hoàn thành quy trình đặt/giao món | Quy trình tương tác giữa admin và acc user về việc đặt hàng và giao hàng hợp logic hơn. | 19/03/2026 | Trần Mạnh Hùng |
| Tích hợp thanh toán ví điện tử | Nghiên cứu và triển khai API thanh toán trực tuyến qua Sepay/PayOS. | 21/03/2026 | Nguyễn Anh Khoa |
| Hệ thống mã giảm giá (Coupon) | Xây dựng tính năng cho phép người dùng nhập mã giảm giá khi thanh toán và giao diện quản lý mã cho Admin. | 20/03/2026 | Nguyễn Tấn Thắng |
| Thông báo đẩy (Notification) | Tích hợp thông báo đẩy (Firebase Cloud Messaging) để báo cáo trạng thái đơn hàng đến người dùng theo thời gian thực. | 22/03/2026 | Bùi Dương Duy Cường |
| Kiểm thử và tối ưu (Testing) | Tiếp tục rà soát lỗi (bugs) trên các thiết bị thực tế, tối ưu hóa giao diện và hiệu năng tải dữ liệu từ Supabase. | 24/03/2026 | Cả nhóm |

**V. BÁO CÁO KHAI THÁC TRÍ TUỆ NHÂN TẠO (AI REPORT)**
*Mức độ sử dụng AI và thông tin chi tiết từng thành viên trong quá trình code và phát triển tính năng:*

**1. Trần Mạnh Hùng:**
- **Mục đích:** Xử lý logic gửi mã OTP qua Email Protocol (SMTP) và viết Regex bắt lỗi cho custom Auth. Xây dựng chức năng Contact page liên kết ngoài.
- **Prompt sử dụng:** *"Tôi đang viết tính năng quên mật khẩu trong Android Java. Hãy hướng dẫn tôi cách sử dụng thư viện JavaMail API để gửi 1 mã OTP 6 số đến email người dùng một cách bảo mật, và cách tạo Intent mở URL Zalo, Facebook, Youtube trực tiếp từ ứng dụng Android."*
- **Kết quả:** Code nhanh chóng các Intent Action VIEW, kết nối thành công SMTP với tài khoản Gmail app password.

**2. Bùi Dương Duy Cường:**
- **Mục đích:** Thiết kế UI/UX Animations cho Slideshow ảnh đồ ăn trên trang chủ. Tạo Custom Dialog tùy chỉnh cho phần Đánh giá & Nhận xét.
- **Prompt sử dụng:** *"Làm sao để tạo một Image Slider tự động cuộn (auto-scroll) trong Android dùng ViewPager2? Tôi cũng muốn thiết kế một Custom Dialog Rating Bar có giao diện bo góc để người dùng để lại sao và văn bản nhận xét."*
- **Kết quả:** Xử lý trơn tru ViewPager2 với Runnable handler, có UI trực quan và sinh động cho phần nhận xét món.

**3. Nguyễn Anh Khoa:**
- **Mục đích:** Tối ưu hóa logic truy vấn Cart/Order từ Database. Quản lý luồng dữ liệu tính tổng tiền khi tăng/giảm số lượng món ăn.
- **Prompt sử dụng:** *"Tôi có bảng CartItem chứa FoodID, UserId, Quantity, Price. Hãy viết cho tôi đoạn logic Java Android để tăng giảm quantity món ăn và tự động tính toán Total Price trả về giao diện theo thời gian thực. Cho tôi xin hướng dẫn tích hợp cơ bản API thanh toán Sepay/PayOS."*
- **Kết quả:** Các thao tác giỏ hàng mượt mà, hạn chế crash khi click liên tục. Lấy được tài kiệu PayOS chuẩn bị cho tuần sau.

**4. Nguyễn Tấn Thắng:**
- **Mục đích:** Xử lý lọc, thống kê doanh thu đa chiều trên Android. Xây dựng bộ lọc tiện ích (Xác nhận, Phục vụ, Hủy) thanh lịch cho Admin.
- **Prompt sử dụng:** *"Làm sao để thay thế công cụ thả xuống Spinner thành một dạng nút bấm trực tiếp liên tiếp (Toggle Button Group) để Admin thao tác chuyển trạng thái đơn hàng nhanh hơn trên Android? Hướng dẫn tôi viết logic lọc doanh thu theo 1 khoảng ngày (Range Date) do User tự chọn qua DatePickerDialog."*
- **Kết quả:** Chuyển đổi mượt mà UI admin giúp trải nghiệm filter đơn hàng trực quan và nhanh chóng.

**5. Ninh Văn Khải:**
- **Mục đích:** Nghiên cứu prompt cho AI Insight Model phân tích sắc thái biểu cảm của các nhận xét từ hệ thống.
- **Prompt sử dụng:** *"Tôi đang xây dựng trang phân tích AI Dashboard cho Admin Food App. Tôi có 1 tập dataset các bình luận của user về đồ ăn. Hãy viết cấu trúc hướng dẫn (prompt) để gửi lên API AI nhằm phân loại các review này thành 3 nhóm: Tích cực, Tiêu cực, Trung lập, đồng thời tóm tắt và dự doán xu hướng món ăn sắp tới sẽ hot."*
- **Kết quả:** Xây dựng được bộ mẫu chuẩn form để truyền dữ liệu và có UI biểu đồ tiếp nhận dữ liệu insight từ AI.
