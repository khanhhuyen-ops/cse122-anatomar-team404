# Báo cáo sử dụng AI

Mỗi prompt làm việc trên AnatomAR có một mục riêng theo thứ tự thời gian. Mục ghi rõ phần AI thực hiện, phần nhóm tự sửa và kết quả kiểm chứng thực tế.

## 2026-11-26 · Tổ chức cấu trúc dự án cho nhóm hai thành viên

- **Công cụ**. Codex, PowerShell, Python, Git và Node.js.
- **Prompt chính**. Sau mỗi prompt, khai báo việc dùng AI. Bổ sung cấu trúc thư mục theo yêu cầu CSE122 cho nhóm hai thành viên và giữ các thư mục hiện có để dễ tra cứu, sửa lỗi và nâng cấp.
- **Phần AI sinh**. Tạo các thư mục còn thiếu, tệp nhận diện thư mục rỗng, tệp nền CSS và JS có chú thích, liên kết Figma, tài liệu đề xuất và phân công. Cập nhật README, quy ước báo cáo và người phụ trách của 32 màn hình.
- **Phần nhóm tự sửa**. Nhóm cung cấp số thành viên và yêu cầu bảo toàn cấu trúc hiện có. Chưa ghi nhận chỉnh sửa thủ công của nhóm sau đầu ra AI. Phân công dùng mã `SV1` và `SV2` để nhóm đối chiếu.
- **Cách kiểm chứng**. Đối chiếu mục §20, kiểm tra đường dẫn Markdown, dữ liệu JSON, cú pháp hai tệp JS và phân công 16 màn hình mỗi người. Thử tải bảy tệp qua HTTP cục bộ. So sánh mã băm bốn tệp có sẵn và trạng thái Git của hai demo. Lần kiểm tra bảng đầu tiên gặp lỗi mã hóa dấu gạch trong khoảng mã màn hình. Đã chỉnh phép kiểm tra và chạy lại thành công. Phép thử HTTP chỉ kiểm tra các tệp tĩnh ở giai đoạn chuẩn bị triển khai.
- **Điều học được**. Một bảng kiểm kê duy nhất giúp đối chiếu mã màn hình, người phụ trách, tệp và minh chứng. Khi sắp xếp cấu trúc, kiểm tra đường dẫn và dữ liệu riêng với hành vi ứng dụng để biết phần nào đã được xác minh.
