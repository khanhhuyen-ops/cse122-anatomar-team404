# Phân công nhóm hai thành viên

Nhóm dùng mã `SV1` và `SV2` để phân công trong lúc chưa ghi tên thành viên vào tài liệu. Đây là phương án cho nhóm hiện tại. Người phụ trách cụ thể của mỗi màn hình nằm trong [bảng kiểm kê](../design/screen-list.md).

| Thành viên | Màn hình phụ trách | Trách nhiệm tích hợp |
| --- | --- | --- |
| SV1 | X01–X04, X08–X09, P01–P03, S01–S02, S05, A01, A03–A04, A06 | Điều hướng dùng chung, atlas 3D, responsive và dữ liệu danh mục hệ, cơ quan, mô hình. |
| SV2 | X05–X07, S03–S04, S06, T01–T08, A02, A05 | Biên tập và duyệt học liệu, tài khoản, mock API và dữ liệu ôn tập. |

Hai thành viên thống nhất ID và hợp đồng dữ liệu trước khi ghép các phần. SV1 và SV2 review chéo các thay đổi ảnh hưởng tới luồng giữa vai trò. Khi đổi người phụ trách, cập nhật bảng kiểm kê và mục phân công ở đây.

## Luồng thực hiện để làm minh chứng

- **SV1** triển khai luồng khám phá từ P01 đến P02 hoặc luồng chọn cơ quan ở S02. [Luồng F01–F02](../design/user-flow.md).
- **SV2** triển khai luồng tạo câu hỏi tại T03 và chuyển sang bước duyệt A05. [Luồng F09–F10](../design/user-flow.md).

Mỗi người hoàn thành ít nhất một luồng từ thiết kế qua HTML, CSS, JavaScript và dữ liệu mô phỏng. Dùng mã màn hình để tìm task, nhánh, PR, ca kiểm thử và video OBS. Mỗi video gắn với màn hình đã duyệt và phần người phụ trách có thể giải thích, làm lại. [Yêu cầu CSE122 §§15–18](../.agents/skills/AnatomAR-project-requirements.md).
