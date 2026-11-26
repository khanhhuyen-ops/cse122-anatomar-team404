# AnatomAR

Đọc [đặc tả thiết kế](design/DESIGN.md) trước khi sửa giao diện. Dùng [anatomar-design](.agents/skills/anatomar-design/SKILL.md) cho các thay đổi về màn hình, component và tương tác.

- `pages/` chứa các trang của ứng dụng. `css/` chứa kiểu giao diện. `js/` chứa logic phía trình duyệt.
- `assets/models/`, `assets/animations/`, `assets/organ-svg/` và `assets/images/` chứa tài nguyên theo loại.
- `design/` chứa đặc tả, danh sách màn hình, luồng người dùng và mockup. `docs/` chứa tài liệu kỹ thuật.
- `db.json` dành cho dữ liệu JSON của ứng dụng.
- `third-part/` chứa các demo lưu riêng. Thiết kế AnatomAR lấy căn cứ từ yêu cầu CSE122, bộ đặc tả và ảnh tham chiếu do người dùng cung cấp. Mọi tài nguyên được đề xuất cho sản phẩm cần có nguồn và điều kiện giấy phép.
- Nhóm hiện có hai thành viên. Dùng [phân công nhóm](docs/team-assignment.md) và [bảng kiểm kê màn hình](design/screen-list.md) khi gán việc.
- Sau mỗi prompt liên quan đến AnatomAR, thêm một mục vào cuối [báo cáo sử dụng AI](docs/ai-usage-report.md) trước khi trả lời. Ghi công cụ, prompt chính, phần AI sinh, phần nhóm tự sửa, cách kiểm chứng và điều học được. Ghi rõ mục nào còn chờ nhóm tự làm hoặc kiểm chứng. Giữ nguyên các mục trước.
