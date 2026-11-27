---
name: anatomar-design
description: Thiết kế, đặc tả hoặc rà soát giao diện AnatomAR cho bốn vai trò, gồm atlas SVG/3D, học liệu giải phẫu, thẻ, trắc nghiệm, dashboard và các luồng CRUD.
---

# Thiết kế AnatomAR

Đọc [yêu cầu dự án](../AnatomAR-project-requirements.md) và [đặc tả thiết kế](../../../design/DESIGN.md). Xác định vai trò, mã màn hình, tệp và luồng trong [bảng kiểm kê](../../../design/screen-list.md) và [luồng người dùng](../../../design/user-flow.md). Giữ tên tệp nền tảng theo yêu cầu. Khi đổi nghiệp vụ hoặc thêm màn hình, cập nhật cả hai tài liệu và ghi các quyết định đề xuất.

- Dùng ID giải phẫu chung. Atlas 3D xem thông tin nhanh. Sơ đồ SVG chọn hệ và cơ quan để mở học liệu hoặc gửi đề xuất. S03 nghiên cứu cấu tạo, hoạt ảnh và ghi nhớ. T05 quản lý phiên bản SVG và chú thích.
- Atlas 3D dùng Object Picking theo hình học, phủ xanh ngọc lên phần bề mặt đang thấy và hiện tooltip tên, hệ, vị trí, chức năng. Desktop rê, Mobile chạm. Kiểm kê node, mesh và metadata GLB trước khi gán thực thể. [Trình xem 3D](references/viewer-3d.md).
- Với luồng có dữ liệu, xác định đối tượng được xem hoặc sửa, các trạng thái nghiệp vụ và điểm khôi phục. Tham chiếu hợp đồng mock, sau đó dùng các mẫu form, bảng hoặc viewer chung.
- Dùng tiếng Việt có dấu và tiêu đề phản ánh nhiệm vụ. Chọn HTML ngữ nghĩa, CSS, JavaScript thuần, SVG, Three.js và mock JSON khi có yêu cầu triển khai. Thiết kế hình ảnh theo đặc tả AnatomAR và ảnh tham chiếu của người dùng. Ghi nguồn, giấy phép của tài nguyên được chọn.

Đọc tài liệu theo phần cần thiết.

| Công việc | Tài liệu |
| --- | --- |
| Chọn token và kiểu chữ | [Hệ thống thiết kế](references/design-system.md) |
| Dùng thành phần và trạng thái | [Đặc tả thành phần](references/components.md) · [Quy tắc tương tác](references/interaction.md) |
| Đặt bố cục desktop và mobile | [Bố cục và wireframe](references/layout.md) |
| Chỉnh mô hình, sơ đồ hoặc điều khiển | [Trình xem 3D](references/viewer-3d.md) |
| Rà bàn phím, focus, chuyển động và phương án thay thế | [Khả năng tiếp cận](references/accessibility.md) |
| Kiểm tra quyền, trạng thái, CRUD hoặc mock API | [Dữ liệu mô phỏng](references/mock-data.md) |
