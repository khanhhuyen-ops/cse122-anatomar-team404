# Bảng kiểm kê màn hình

Đường dẫn dự kiến nằm trong `pages/`. Tên tệp của 16 trang nền tảng và 9 trang dùng chung theo [yêu cầu dự án §§08–09](../.agents/skills/AnatomAR-project-requirements.md). Mã dùng để nối wireframe, [luồng người dùng](user-flow.md), task và video OBS. Cột người phụ trách dùng [phương án phân công nhóm hai thành viên](../docs/team-assignment.md). Các trang bổ sung được ghi rõ trong bảng.

CRUD dùng C (Tạo), R (Đọc), U (Sửa), D (Hủy/lưu trữ/vô hiệu hóa theo ngữ cảnh). Trang lấy dữ liệu có «Đang tải», rỗng và lỗi có thể thử lại. Biểu mẫu có kiểm tra hợp lệ, đang lưu, thành công và lỗi giữ lại đầu vào. Bảng ghi thêm các trạng thái nghiệp vụ. [Bố cục](../.agents/skills/anatomar-design/references/layout.md) · [Thành phần](../.agents/skills/anatomar-design/references/components.md).

X01 và P01–P03 dùng công khai. X05–X07 dùng phiên hợp lệ, X08 và X09 xử lý lối khôi phục. Mỗi nhóm S/T/A yêu cầu đúng vai trò, rồi kiểm quyền trên bản ghi theo [F04](user-flow.md#f04--tài-khoản-phiên-và-thông-tin-cá-nhân). Các trạng thái mới dùng thành phần trong 32 màn hình dưới đây.

## Dùng chung

| Mã | Mục tiêu và nhiệm vụ | Giao diện · Tệp | CRUD / Trạng thái riêng | Luồng | Phụ trách |
| --- | --- | --- | --- | --- | --- |
| X01 | Hiểu khóa học, khám phá cơ thể 3D toàn thân | Trang chủ · `index.html` | R · Công khai, bật/tắt lớp giải phẫu, tooltip theo hình học, có «Khu vực của tôi» sau đăng nhập | F01, F04 | SV1 |
| X02 | Tiếp tục theo vai trò hoặc quay lại đích hợp lệ | Đăng nhập · `login.html` | C phiên · Sai thông tin, vô hiệu hóa, hết phiên | F04 | SV1 |
| X03 | Bắt đầu học bằng tài khoản mẫu | Đăng ký · `register.html` | C · Email trùng, tạo thành công | F01, F04 | SV1 |
| X04 | Lấy lại quyền vào tài khoản mẫu | Quên mật khẩu · `forgot-password.html` | C/U mô phỏng · Yêu cầu, mã hết hạn, mật khẩu đã đổi | F04 | SV1 |
| X05 | Đọc và sửa thông tin cá nhân | Hồ sơ · `profile.html` | R/U · Chỉ đọc vai trò và email, lưu tên | F04 | SV2 |
| X06 | Điều chỉnh trải nghiệm | Cài đặt · `settings.html` | R/U · Ưu tiên giảm chuyển động, đã lưu | F04 | SV2 |
| X07 | Xem kết quả duyệt, đề xuất được giao, phản hồi và học liệu đã đáp ứng đề xuất | Thông báo · `notifications.html` | R/U · Chưa đọc, đã đọc, trống, đích không còn xem được | F04, F10, F13 | SV2 |
| X08 | Hồi phục khi thiếu quyền | Không có quyền · `403.html` | R · Thiếu quyền, hết phiên có lối đăng nhập lại | F04 | SV1 |
| X09 | Hồi phục khi đường dẫn thiếu hoặc nội dung đã ẩn | Không tìm thấy · `404.html` | R · Không tồn tại, có đường về danh sách | F01, F04, F10 | SV1 |

## Khách

| Mã | Mục tiêu và nhiệm vụ | Giao diện · Tệp | CRUD / Trạng thái riêng | Luồng | Phụ trách |
| --- | --- | --- | --- | --- | --- |
| P01 | Xem danh mục 11 hệ cơ quan và học liệu mẫu | Hệ cơ quan tổng quan · `visitor-systems-overview.html` | R · Danh mục 11 hệ, trạng thái sẵn có của học liệu mẫu, lọc/tìm rỗng có xóa bộ lọc | F01, F03, F12 | SV1 |
| P02 | Xem mẫu được A06 công khai, ví dụ Tim và Xương | Mô hình mẫu · `visitor-organ-preview.html` | R · Nội dung văn bản, trạng thái ảnh/SVG/GLB/hoạt ảnh riêng, đích công khai đã gỡ | F01, F02, F12, F13 | SV1 |
| P03 | Đề nghị bổ sung cơ quan hoặc hệ, tra cứu và mở mẫu công khai khi có | Đề xuất chủ đề · `visitor-topic-suggestion.html` | C/R · Đang chờ, đã tiếp nhận, bị từ chối, đã hoàn tất, mã không hợp lệ | F03, F13 | SV1 |

## Sinh viên

| Mã | Mục tiêu và nhiệm vụ | Giao diện · Tệp | CRUD / Trạng thái riêng | Luồng | Phụ trách |
| --- | --- | --- | --- | --- | --- |
| S01 | Xem tiến độ, tiếp tục học và tham gia lớp bằng mã giảng viên cung cấp | Bảng điều khiển · `student-dashboard.html` | R/C thành viên · Lớp của tôi, mã trống/sai, lớp đã lưu trữ, đã tham gia, thành công, lỗi có thể thử lại. Tiến độ gồm chưa học, đang học và hoàn thành | F04, F05, F06, F07, F08 | SV1 |
| S02 | Atlas xem nhanh. SVG/danh sách chọn hệ và cơ quan, mở bài, đề xuất hoặc ôn theo ngữ cảnh | Học theo hệ · `student-system-view.html` | Atlas R · Hover/tap và lớp ẩn. SVG/danh sách R/C · Thiếu sơ đồ có danh sách, có bài thiếu GLB, thiếu bài, đang gửi, đang chờ/đã tiếp nhận, lỗi kiểm tra | F02, F03, F05, F06, F07, F13 | SV1 |
| S03 | Mở bài cơ quan, đọc cấu tạo, quan sát qua phương tiện sẵn có, đánh dấu đã thuộc và mở bài ôn liên quan | Mô hình cơ quan · `student-organ-model.html` | R, C/U/D của dấu ghi nhớ · Văn bản, phương tiện thiếu/lỗi riêng, đã thuộc/bỏ đánh dấu | F02, F05, F06, F07, F13 | SV2 |
| S04 | Chọn bộ đã xuất bản theo hệ, lọc theo cơ quan khi có, làm và nộp | Trắc nghiệm ghi nhớ · `student-memory-quiz.html` | C/R, U bản nháp ghim phiên bản · Chưa làm, đang làm, nộp lỗi, hoàn thành | F07 | SV2 |
| S05 | Chọn nhóm thẻ đã xuất bản, lật và tự đánh giá trong lượt ôn | Thẻ ghi nhớ · `student-flashcards.html` | R thẻ, C/U kết quả ôn · Hai mặt, đã thuộc/cần ôn lại, tiếp tục hoặc kết thúc lượt | F06 | SV1 |
| S06 | Xem điểm, từng câu và giải thích | Kết quả trắc nghiệm · `student-quiz-result.html` (bổ sung) | R · Câu đúng/sai/bỏ trống, làm lại hoặc ôn hệ | F07 | SV2 |

## Giảng viên

| Mã | Mục tiêu và nhiệm vụ | Giao diện · Tệp | CRUD / Trạng thái riêng | Luồng | Phụ trách |
| --- | --- | --- | --- | --- | --- |
| T01 | Tổng hợp lớp, theo dõi duyệt, xử lý và liên kết học liệu cho đề xuất được giao | Bảng điều khiển · `teacher-dashboard.html` | R/U · Chưa có lớp, bản chờ duyệt, đề xuất đang chờ, đã tiếp nhận hoặc đã hoàn tất | F04, F08, F09, F10, F13 | SV2 |
| T02 | Quản lý bài cơ quan mình sở hữu, lọc theo hệ, trạng thái và đối chiếu định danh | Quản lý mô hình · `teacher-anatomy-manage.html` | C/R/U/D bản nháp qua T06 · Nháp, chờ, từ chối, bản hiện hành và bản sửa, lưu trữ | F09, F10 | SV2 |
| T03 | Soạn và duyệt theo bộ quiz của một hệ, sửa câu A–D và xem thử | Soạn trắc nghiệm · `teacher-quiz-builder.html` | C/R/U/D bộ/câu trong bản nháp · Nháp, chờ, từ chối, đã xuất bản, xác nhận xóa | F09, F10 | SV2 |
| T04 | Chọn lớp mình phụ trách, thành viên và hệ để xem tiến độ | Tiến độ sinh viên · `teacher-student-progress.html` | R · Chưa có dữ liệu khác điểm 0, báo cáo lớp mở và bản chốt của lớp lưu trữ | F05, F08 | SV2 |
| T05 | Dựng SVG, thêm nhiều chú thích theo cơ quan, đổi vị trí, xóa điểm và xem trước | Dựng học liệu SVG · `teacher-visual-builder.html` | C/R/U/D · Nháp, nhiều chú thích, lỗi tọa độ, xác nhận xóa điểm, xem trước, chờ duyệt, lưu trữ bản | F09, F10 | SV2 |
| T06 | Tạo/sửa bài cơ quan có nguồn, đề xuất định danh mới nếu cần và gắn tài nguyên tùy chọn từ A04 | Biên tập cơ quan · `teacher-organ-editor.html` (bổ sung) | C/R/U · Chưa lưu, lỗi nguồn/tài nguyên, xem trước văn bản và phương tiện, chờ duyệt, lý do từ chối | F09, F10, F13 | SV2 |
| T07 | Tạo lớp có mã duy nhất, sao chép mã, quản lý thành viên và lưu trữ lớp | Quản lý lớp · `teacher-class-management.html` (bổ sung) | C/R/U/D (lưu trữ) · Đang mở, mã đã cấp, đã sao chép, không có thành viên, trùng thành viên, lớp lưu trữ chỉ đọc | F08 | SV2 |
| T08 | Soạn nhóm thẻ theo hệ, sắp thẻ, xem hai mặt và gửi duyệt cả nhóm | Soạn thẻ ghi nhớ · `teacher-flashcard-builder.html` (bổ sung) | C/R/U/D nhóm/thẻ nháp · Nháp, chờ, từ chối, đã xuất bản, lưu trữ | F06, F09, F10 | SV2 |

## Quản trị viên

| Mã | Mục tiêu và nhiệm vụ | Giao diện · Tệp | CRUD / Trạng thái riêng | Luồng | Phụ trách |
| --- | --- | --- | --- | --- | --- |
| A01 | Xem tài khoản, nội dung và đề xuất cần xử lý | Bảng điều khiển · `admin-dashboard.html` | R · Hàng đợi rỗng, tài nguyên thiếu metadata | F04, F11, F12, F13 | SV1 |
| A02 | Thêm, sửa, phân quyền, vô hiệu hóa/mở lại | Quản lý người dùng · `admin-user-management.html` | C/R/U/D (vô hiệu hóa) · Email trùng, hoạt động, vô hiệu hóa, cảnh báo tác động tới lớp theo F11 | F11 | SV2 |
| A03 | Cấu hình đề mục, thứ tự và người phụ trách theo 11 hệ chuẩn, mở A04 | Cấu hình hệ cơ quan · `admin-body-system-config.html` | C/R/U/D của đề mục, R danh mục chuẩn · Nháp cấu hình, hủy, đề mục lưu trữ | F12 | SV1 |
| A04 | Quản lý ảnh, SVG, GLB, hoạt ảnh, giấy phép và quyền dùng công khai | Thư viện mô hình · `admin-model-library.html` (bổ sung) | C/R/U/D (lưu trữ) · Nháp, sẵn sàng, lưu trữ, thiếu nguồn hoặc còn tham chiếu | F12 | SV1 |
| A05 | Duyệt đúng phiên bản, bàn giao chủ học liệu, giao và hoàn tất đề xuất | Hàng đợi duyệt · `admin-review-queue.html` (bổ sung) | R/U · Học liệu chờ/xuất bản/từ chối/hủy/lưu trữ. Đề xuất chờ/tiếp nhận/từ chối/hoàn tất. Xung đột khi vừa có quyết định | F10, F13 | SV2 |
| A06 | Chọn nội dung công khai và mẫu cơ quan mặc định | Cấu hình hệ thống · `admin-system-settings.html` (bổ sung) | R/U · Chưa lưu, mẫu chưa xuất bản, thay đổi đã áp dụng | F12 | SV1 |

Tìm kiếm, bộ lọc, hộp thoại xác nhận, ngăn chi tiết và toàn màn hình 3D thuộc trang mở chúng. Ví dụ `student-system-view.html?system=circulatory&organ=organ.heart&view=svg` mở lại hệ và cơ quan. [Quy ước điều hướng](../.agents/skills/anatomar-design/references/interaction.md).
