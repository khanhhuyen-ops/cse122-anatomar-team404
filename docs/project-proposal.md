# Đề xuất dự án AnatomAR

AnatomAR là nguyên mẫu frontend cho học phần CSE122. Dự án giúp người học định vị, quan sát và ghi nhớ cấu trúc giải phẫu theo hệ cơ quan. Nhóm hiện có hai thành viên thực hiện.

## Vấn đề và mục tiêu

Hình tĩnh khó thể hiện quan hệ không gian giữa các cấu trúc. Người học cần cách xem mô hình từ nhiều góc và tự kiểm tra kiến thức. Giảng viên cần nơi tạo học liệu và theo dõi tiến độ. AnatomAR kết hợp học liệu SVG, mô hình 3D, thẻ ghi nhớ và trắc nghiệm để phục vụ các nhu cầu này.

## Phạm vi

| Vai trò | Luồng chính |
| --- | --- |
| Khách | Khám phá hệ cơ quan, xem mô hình mẫu và gửi đề xuất học liệu. |
| Sinh viên | Học theo hệ, chọn một bộ phận để xem chi tiết, ôn tập và xem tiến độ. |
| Giảng viên | Biên tập học liệu, quản lý lớp, tạo bài ôn tập và theo dõi tiến độ sinh viên. |
| Quản trị viên | Quản lý tài khoản, danh mục, tài nguyên và hàng đợi duyệt. |

Dự kiến dùng HTML, CSS, JavaScript, Three.js và dữ liệu mô phỏng trong `db.json`. Trình xem 3D chọn theo hình học và ID cấu trúc. Học liệu SVG do giảng viên biên tập theo mục tiêu bài học.

## Tài liệu và minh chứng

- Phạm vi từng màn hình, luồng và trách nhiệm nằm trong [bảng kiểm kê](../design/screen-list.md), [luồng người dùng](../design/user-flow.md) và [phân công nhóm](team-assignment.md).
- Bản thiết kế gồm màn hình desktop, mobile và các trạng thái trình xem. [Đặc tả thiết kế](../design/DESIGN.md) · [Figma](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=0-1).
- Khi triển khai, nối mã màn hình với task, nhánh, PR, bằng chứng kiểm thử và video OBS theo [yêu cầu CSE122](../.agents/skills/AnatomAR-project-requirements.md). Ghi nhận hỗ trợ AI trong [báo cáo](ai-usage-report.md).
