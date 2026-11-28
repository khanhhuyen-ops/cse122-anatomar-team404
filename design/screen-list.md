# Bảng kiểm kê màn hình

Đường dẫn dự kiến nằm trong `pages/`. Tên tệp của 16 trang nền tảng và 9 trang dùng chung theo [yêu cầu dự án §§08–09](../.agents/skills/AnatomAR-project-requirements.md). Mã dùng để nối wireframe, [luồng người dùng](user-flow.md), task và video OBS. Cột người phụ trách dùng [phương án phân công nhóm hai thành viên](../docs/team-assignment.md). Các trang bổ sung được ghi rõ trong bảng.

CRUD dùng C (Tạo), R (Đọc), U (Sửa), D (Hủy/lưu trữ/vô hiệu hóa theo ngữ cảnh). Trang lấy dữ liệu có «Đang tải», rỗng và lỗi có thể thử lại. Biểu mẫu có kiểm tra hợp lệ, đang lưu, thành công và lỗi giữ lại đầu vào. Bảng ghi thêm các trạng thái nghiệp vụ. [Bố cục](../.agents/skills/anatomar-design/references/layout.md) · [Thành phần](../.agents/skills/anatomar-design/references/components.md).

## Dùng chung

| Mã | Mục tiêu và nhiệm vụ | Giao diện · Tệp | CRUD / Trạng thái riêng | Luồng | Phụ trách |
| --- | --- | --- | --- | --- | --- |
| X01 | Hiểu khóa học, khám phá cơ thể 3D toàn thân | Trang chủ · `index.html` | R · Công khai, bật/tắt lớp giải phẫu, tooltip theo hình học, có «Khu vực của tôi» sau đăng nhập | F01, F04 | SV1 |
| X02 | Tiếp tục theo vai trò hoặc quay lại đích hợp lệ | Đăng nhập · `login.html` | C phiên · Sai thông tin, vô hiệu hóa, hết phiên | F04 | SV1 |
| X03 | Bắt đầu học bằng tài khoản mẫu | Đăng ký · `register.html` | C · Email trùng, tạo thành công | F01, F04 | SV1 |
| X04 | Lấy lại quyền vào tài khoản mẫu | Quên mật khẩu · `forgot-password.html` | C/U mô phỏng · Yêu cầu, mã hết hạn, mật khẩu đã đổi | F04 | SV1 |
| X05 | Đọc và sửa thông tin cá nhân | Hồ sơ · `profile.html` | R/U · Chỉ đọc vai trò và email, lưu tên | F04 | SV2 |
| X06 | Điều chỉnh trải nghiệm | Cài đặt · `settings.html` | R/U · Ưu tiên giảm chuyển động, đã lưu | F04 | SV2 |
| X07 | Xem phản hồi đề xuất, nhận đề xuất được phân công và đi tới bản ghi | Thông báo · `notifications.html` | R/U · Chưa đọc, đã đọc, trống | F04, F10, F13 | SV2 |
| X08 | Hồi phục khi thiếu quyền | Không có quyền · `403.html` | R · Thiếu quyền, hết phiên có lối đăng nhập lại | F04 | SV1 |
| X09 | Hồi phục khi đường dẫn thiếu hoặc nội dung đã ẩn | Không tìm thấy · `404.html` | R · Không tồn tại, có đường về danh sách | F01, F04, F10 | SV1 |

## Khách

| Mã | Mục tiêu và nhiệm vụ | Giao diện · Tệp | CRUD / Trạng thái riêng | Luồng | Phụ trách |
| --- | --- | --- | --- | --- | --- |
| P01 | Xem danh mục 11 hệ cơ quan và học liệu mẫu | Hệ cơ quan tổng quan · `visitor-systems-overview.html` | R · Danh mục 11 hệ, trạng thái sẵn có của học liệu mẫu, lọc/tìm rỗng có xóa bộ lọc | F01, F03, F12 | SV1 |
| P02 | Khám phá mẫu công khai, ví dụ tim và xương | Mô hình mẫu · `visitor-organ-preview.html` | R · Sẵn sàng, thiếu hoạt ảnh, tải GLB lỗi, chi tiết dạng văn bản | F01, F02, F12 | SV1 |
| P03 | Đề nghị bổ sung cơ quan hoặc hệ, tra cứu phản hồi | Đề xuất chủ đề · `visitor-topic-suggestion.html` | C/R · Đang chờ, đã chấp nhận, bị từ chối, mã không hợp lệ | F03, F13 | SV1 |

## Sinh viên

| Mã | Mục tiêu và nhiệm vụ | Giao diện · Tệp | CRUD / Trạng thái riêng | Luồng | Phụ trách |
| --- | --- | --- | --- | --- | --- |
| S01 | Xem tiến độ, tiếp tục học và tham gia lớp bằng mã giảng viên cung cấp | Bảng điều khiển · `student-dashboard.html` | R/C thành viên · Lớp của tôi, mã trống/sai, lớp đã lưu trữ, đã tham gia, thành công, lỗi có thể thử lại. Tiến độ gồm chưa học, đang học và hoàn thành | F04, F05, F06, F07, F08 | SV1 |
| S02 | Atlas 3D quan sát và xem thông tin nhanh. Sơ đồ SVG chọn hệ và hotspot để mở học liệu hoặc gửi đề xuất. | Học theo hệ · `student-system-view.html` | Atlas R · Hover/tap, lớp đang ẩn. SVG R/C · Mặc định, hover, đã chọn, có/chưa có học liệu, đang gửi, đang chờ, lỗi gửi. | F02, F03, F05, F07 | SV1 |
| S03 | Quan sát một cấu trúc, xoay, phóng to và đánh dấu đã thuộc | Mô hình cơ quan · `student-organ-model.html` | R/U, C/D của dấu ghi nhớ · Thiếu hoạt ảnh, chi tiết dạng văn bản, đã thuộc/bỏ đánh dấu | F02, F05, F06 | SV2 |
| S04 | Chọn hệ, làm bài vị trí/chức năng và nộp | Trắc nghiệm ghi nhớ · `student-memory-quiz.html` | C/R, U bản nháp · Chưa làm, đang làm, nộp lỗi, hoàn thành | F07 | SV2 |
| S05 | Xem từng thẻ, lật và tự đánh giá | Thẻ ghi nhớ · `student-flashcards.html` | R thẻ, C/U kết quả ôn · Hai mặt, đã thuộc/cần ôn lại, kết thúc lượt | F06 | SV1 |
| S06 | Xem điểm, từng câu và giải thích | Kết quả trắc nghiệm · `student-quiz-result.html` (bổ sung) | R · Câu đúng/sai/bỏ trống, làm lại hoặc ôn hệ | F07 | SV2 |

## Giảng viên

| Mã | Mục tiêu và nhiệm vụ | Giao diện · Tệp | CRUD / Trạng thái riêng | Luồng | Phụ trách |
| --- | --- | --- | --- | --- | --- |
| T01 | Tổng hợp lớp và tiến độ, theo dõi duyệt, mở danh sách đề xuất và phản hồi | Bảng điều khiển · `teacher-dashboard.html` | R/U · Chưa có lớp, chờ duyệt, đề xuất đang chờ, đã tiếp nhận, đã phản hồi | F04, F08, F09, F10, F13 | SV2 |
| T02 | Quản lý nội dung, lọc và gán cơ quan vào hệ | Quản lý mô hình · `teacher-anatomy-manage.html` | C/R/U/D (lưu trữ) qua T06 · Bản nháp, đang chờ, đã xuất bản, bị từ chối, đã lưu trữ | F09, F10 | SV2 |
| T03 | Thêm, sửa, xóa câu hỏi A–D trong cùng bộ, chọn đáp án đúng, nhập giải thích, xem thử theo bản nháp | Soạn trắc nghiệm · `teacher-quiz-builder.html` | C/R/U/D câu hỏi nháp · Nháp, đang chờ, bị từ chối, đã xuất bản, xác nhận xóa | F09, F10 | SV2 |
| T04 | Chọn lớp, sinh viên, hệ và đọc tiến độ chi tiết | Tiến độ sinh viên · `teacher-student-progress.html` | R · Chưa có điểm hoặc dấu đã thuộc, dữ liệu của lớp mình | F05, F08 | SV2 |
| T05 | Dựng SVG, thêm nhiều chú thích theo cơ quan, đổi vị trí, xóa điểm và xem trước | Dựng học liệu SVG · `teacher-visual-builder.html` | C/R/U/D · Nháp, nhiều chú thích, lỗi tọa độ, xác nhận xóa điểm, xem trước, chờ duyệt, lưu trữ bản | F09, F10 | SV2 |
| T06 | Sửa cơ quan, cấu hình mô hình và kiểm tra ánh xạ hình học 3D | Biên tập cơ quan · `teacher-organ-editor.html` (bổ sung) | C/R/U · Chưa lưu, lỗi nguồn/tài nguyên, chờ duyệt, lý do từ chối | F09, F10 | SV2 |
| T07 | Tạo lớp có mã duy nhất, sao chép mã, quản lý thành viên và lưu trữ lớp | Quản lý lớp · `teacher-class-management.html` (bổ sung) | C/R/U/D (lưu trữ) · Đang mở, mã đã cấp, đã sao chép, không có thành viên, trùng thành viên, lớp lưu trữ chỉ đọc | F08 | SV2 |
| T08 | Soạn hoặc sửa thẻ, xem hai mặt và gửi duyệt | Soạn thẻ ghi nhớ · `teacher-flashcard-builder.html` (bổ sung) | C/R/U/D (lưu trữ) · Nháp, đang chờ, bị từ chối, đã xuất bản | F06, F09, F10 | SV2 |

## Quản trị viên

| Mã | Mục tiêu và nhiệm vụ | Giao diện · Tệp | CRUD / Trạng thái riêng | Luồng | Phụ trách |
| --- | --- | --- | --- | --- | --- |
| A01 | Xem tài khoản, nội dung và đề xuất cần xử lý | Bảng điều khiển · `admin-dashboard.html` | R · Hàng đợi rỗng, tài nguyên thiếu metadata | F04, F11, F12, F13 | SV1 |
| A02 | Thêm, sửa, phân quyền, vô hiệu hóa/mở lại | Quản lý người dùng · `admin-user-management.html` | C/R/U/D (vô hiệu hóa) · Email trùng, đang hoạt động, vô hiệu hóa, lớp đang phụ trách | F11 | SV2 |
| A03 | Cấu hình hệ và đề mục, sắp thứ tự hoặc lưu trữ | Cấu hình hệ cơ quan · `admin-body-system-config.html` | C/R/U/D (lưu trữ) · Đã hủy bản nháp, tham chiếu chặn lưu trữ | F12 | SV1 |
| A04 | Quản lý mô hình, hoạt ảnh, SVG và giấy phép nguồn | Thư viện mô hình · `admin-model-library.html` (bổ sung) | C/R/U/D (lưu trữ) · Thiếu tệp, thiếu metadata, đang được sử dụng | F12 | SV1 |
| A05 | Lọc học liệu và đề xuất, xem chi tiết và bản xem trước, duyệt hoặc từ chối kèm lý do | Hàng đợi duyệt · `admin-review-queue.html` (bổ sung) | R/U · Đang chờ, xác nhận, đã chấp nhận/đã xuất bản, bị từ chối, đã hủy, xung đột xử lý | F10, F13 | SV2 |
| A06 | Chọn nội dung công khai và mẫu cơ quan mặc định | Cấu hình hệ thống · `admin-system-settings.html` (bổ sung) | R/U · Chưa lưu, mẫu chưa xuất bản, thay đổi đã áp dụng | F12 | SV1 |

Tìm kiếm, bộ lọc, dialog xác nhận, drawer chi tiết và toàn màn hình 3D là trạng thái của trang mở chúng. Ví dụ `student-system-view.html?system=circulatory&organ=organ.heart` mở lại hệ và cơ quan. Trạng thái điều hướng và truy cập được quy định trong [tương tác](../.agents/skills/anatomar-design/references/interaction.md).
