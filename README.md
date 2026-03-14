# WEEKLY REPORT
**Sprint 3, Week 2**

**I. GROUP INFORMATION:**
- **Group:** Nhóm Ứng dụng Đặt Món Ăn
- **Project name:** Food Order App
- **Prepared by:** Trần Mạnh Hùng
- **Members:**
  - Trần Mạnh Hùng
  - Bùi Dương Duy Cường
  - Nguyễn Anh Khoa
  - Ninh Văn Khải
  - Thắng
- **Meeting date:** 14/03/2026
- **All members are present.**

**II. ACHIEVEMENTS SINCE LAST WEEK:**
Dựa vào bảng theo dõi tiến độ công việc, nhóm đã hoàn thành các công việc lập trình tính năng (FE & BE):

| Item | Description | Responsibility | Complete |
| --- | --- | --- | --- |
| 1 | **Quản lý tài khoản:** Đăng nhập, Đăng ký, Quên MK, Hồ sơ cá nhân | Trần Mạnh Hùng | 100% |
| 2 | **Tìm kiếm cơ bản:** Mới hoàn tất tìm theo tên & danh mục, lưu lịch sử | Trần Mạnh Hùng | 100% |
| 3 | **Giao diện người dùng (Trang chủ & Chi tiết):** Slideshow, Gợi ý món, Xem chi tiết món và Đánh giá nhận xét | Bùi Dương Duy Cường | 100% |
| 4 | **Giỏ hàng & Đặt hàng:** Xử lý logic giỏ hàng đầy đủ, Tạo đơn hàng, Lịch sử mua hàng, Thanh toán COD | Nguyễn Anh Khoa | 100% |
| 5 | **Quản lý Admin:** Quản lý món ăn, Cập nhật trạng thái đơn đặt hàng, Xem doanh thu theo ngày | Thắng | 80% |
| 6 | **Phản hồi & Tính năng AI:** Quản lý phản hồi, Tích hợp AI phân tích cảm xúc, Dự đoán xu hướng món ăn, AI Dashboard | Ninh Văn Khải | 100% |

**III. ISSUES AND IMPACTS:**
- Các tính năng nâng cao (Sort món ăn mới nhất/giá, Contact page, Danh sách yêu thích) mới được triển khai và đang cần kiểm thử thêm.
- Tích hợp Thanh toán MoMo / ZaloPay và gửi Thông báo đẩy đang chậm hơn dự kiến.
- Nhờ việc chuẩn bị trước schema Database (Supabase) rất chi tiết nên BE và FE kết nối mượt mà, giúp nhóm hoàn thiện đa số tính năng trọng yếu để chuẩn bị cho giai đoạn tiếp theo.

**IV. GOALS FOR NEXT WEEK:**
Giai đoạn này hệ thống cũng đang phục vụ đồ án Phân tích Yêu cầu, nên mục tiêu tuần tới hướng về thu thập thêm yêu cầu:

| Item | Description | Due Date | Responsibility | Priority |
| --- | --- | --- | --- | --- |
| 1 | Soạn list câu hỏi phỏng vấn | 16/03/2026 | Bùi Dương Duy Cường | Cao |
| 2 | Đánh giá và gợi ý cải thiện câu hỏi phỏng vấn | 18/03/2026 | Trần Mạnh Hùng, Nguyễn Anh Khoa | Trung bình |
| 3 | Phỏng vấn người dùng và viết báo cáo biên bản phỏng vấn | 20/03/2026 | Cả nhóm (mỗi người 2-3 người) | Trung bình |
| 4 | Đánh giá và gợi ý cải thiện form khảo sát | 18/03/2026 | Bùi Dương Duy Cường, Ninh Văn Khải | Trung bình |
| 5 | Khảo sát người dùng thực tế (gửi form) | 22/03/2026 | Cả nhóm (KPI 25 người/thành viên) | Trung bình |

**V. SUMMARY:**
Trong đợt làm việc này, mọi người đã tăng tốc đáng kể tiến độ viết code, hoàn thiện tới ~50% khối lượng dự án Android. Phần lớn các tính năng CRUD cho Food, Cart, User và Order đều hoạt động tốt. Tuần tới, nhóm sẽ song song hoàn thiện các module thanh toán còn thiếu, đồng thời đẩy mạnh khảo sát người dùng thực tế để cập nhật và tinh chỉnh lại tài liệu Phân tích Yêu cầu Hệ thống nhằm chuẩn bị cho bản Release cuối cùng.

---

# BÁO CÁO KHAI THÁC TRÍ TUỆ NHÂN TẠO (AI REPORT)
*Mức độ sử dụng AI và thông tin chi tiết từng thành viên:*

**1. Bùi Dương Duy Cường:**
- **Mục đích:** Tham khảo cách đặt câu hỏi, các vấn đề lưu ý khi phỏng vấn, khảo sát.
- **Prompt sử dụng:** *"Tôi đang cần làm một 1 phỏng vấn và một phiếu khảo sát, dựa vào các nguồn tham khảo cũng như yêu cầu của thầy tôi đã cung cấp cho bạn, hãy chỉ giúp tôi xem tôi nên lưu ý gì, soạn kế hoạch theo cấu trúc như thế nào..."*
- **Mục đích:** Xác định xem câu hỏi đã đúng và đủ chưa.
- **Prompt sử dụng:** *"Gửi danh sách các câu hỏi và mục đích... Xác định xem các câu hỏi này có đúng đủ hay không, có cần chỉnh sửa gì hay không, có phù hợp với ý nghĩa và mục tiêu đang hướng tới hay không, nếu ổn thì giữ nguyên chỉnh văn cho mạch lạc, nếu không thì sửa như thế nào."*
- **Mục đích:** Xây dựng cấu trúc Kế hoạch thu thập yêu cầu. Dựa vào yêu cầu và nguồn tham khảo để hình thành phân mục cho báo cáo.

**2. Ninh Văn Khải:**
- **Mục đích:** Kiểm chứng câu hỏi khảo sát người dùng về gói premium (tài liệu/video đề thi).
- **Prompt sử dụng (Gemini 3 Pro):** *"Tôi đang định làm một phần mềm lưu trữ tài liệu đề thi và gói premium... Trong file pdf là các câu hỏi tôi đã tự soạn, bạn có nghĩ rằng tôi đã cover đủ các khía cạnh của người dùng: sinh viên, giáo viên, khách vãng lai chưa?"*
- **Kết quả trả về:** AI phát hiện thiếu sót và đề xuất bổ sung thêm câu hỏi: *"Nếu chỉ được xem thử 30 giây đầu của video giải đề, liệu điều đó có đủ để bạn cân nhắc mua gói không?"*

**3. Trần Mạnh Hùng:**
- **Mục đích:** Xây dựng câu hỏi khảo sát định lượng (thang đo Likert) hỗ trợ đồ án Phân tích yêu cầu ứng dụng.
- **Prompt sử dụng:** *"Nhóm tôi đang thực hiện đồ án môn Phân tích... Đối tượng người dùng là sinh viên và guest. Dựa trên danh sách các chức năng đã xác định, hãy hỗ trợ đề xuất khoảng 20 câu hỏi khảo sát định lượng nhằm đánh giá mức độ quan trọng và tần suất sử dụng của các chức năng trong hệ thống. Thang đo 5 mức: 1. Không ảnh hưởng – 5. Rất quan trọng. 1. Không bao giờ – 5. Luôn luôn."*
- **Kết quả trả về:** Các câu hỏi mang tính chất nền tảng định lượng, được nhóm chắt lọc chọn lựa vào form khảo sát thực tế.

**4. Nguyễn Anh Khoa:**
- **Mục đích:** Diễn đạt, trau chuốt lại câu từ của bảng câu hỏi.
- **Prompt sử dụng:** Sử dụng AI để gợi ý từ vựng rõ ràng, đảm bảo tính khách quan và có văn phong chuyên nghiệp. Prompt được xây dựng dựa trên danh sách cấu trúc và yêu cầu do Cường đã đưa ra trước đó.
