# AnatomAR

Website giáo dục giải phẫu cho Khách, Sinh viên, Giảng viên và Quản trị viên. Nhóm hiện có hai thành viên. Dự án đang ở giai đoạn thiết kế và chuẩn bị cấu trúc triển khai. Các mục trong bảng kiểm kê là màn hình dự kiến.

- [Đề xuất dự án](docs/project-proposal.md)
- [Thiết kế AnatomAR trên Figma](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=0-1)
- [Yêu cầu dự án CSE122](.agents/skills/AnatomAR-project-requirements.md)
- [Đặc tả thiết kế](design/DESIGN.md)
- [Bảng kiểm kê màn hình](design/screen-list.md)
- [Luồng người dùng](design/user-flow.md)
- [Phân công hai thành viên](docs/team-assignment.md)
- [Báo cáo sử dụng AI](docs/ai-usage-report.md)

## Cấu trúc thư mục

```text
AnatomAR/
├── README.md
├── AGENTS.md
├── docs/
│   ├── project-proposal.md
│   ├── screen-list.md
│   ├── team-assignment.md
│   └── ai-usage-report.md
├── design/
│   ├── DESIGN.md
│   ├── figma-link.txt
│   ├── screen-list.md
│   ├── user-flow.md
│   └── mockups/
├── pages/
├── assets/
│   ├── images/
│   ├── icons/
│   ├── data/
│   ├── organ-svg/
│   ├── models/
│   └── animations/
├── css/
│   ├── style.css
│   └── responsive.css
├── js/
│   ├── main.js
│   ├── api.js
│   └── modules/
├── db.json
├── third-part/
└── .agents/
```

## Tra cứu và sửa lỗi

| Cần tìm | Nơi xem |
| --- | --- |
| Tên tệp, mã màn hình, người phụ trách | [Bảng kiểm kê gốc](design/screen-list.md). `docs/screen-list.md` dẫn về cùng bảng. |
| Bố cục, trạng thái và luồng | `design/` và các tài liệu tham chiếu của [skill AnatomAR](.agents/skills/anatomar-design/SKILL.md). |
| Trang HTML và kiểu hiển thị | `pages/` chứa trang. `css/style.css` dành cho kiểu dùng chung và `css/responsive.css` dành cho bố cục theo kích thước màn hình. |
| Tương tác và dữ liệu | `js/main.js` là điểm khởi tạo dự kiến. `js/modules/` chứa logic theo nghiệp vụ. `js/api.js` là điểm truy cập mock dự kiến từ `db.json`. |
| Tài nguyên | `assets/` chứa tài nguyên của AnatomAR theo loại. `assets/data/` dành cho dữ liệu phụ trợ. `third-part/` giữ hai demo tham khảo riêng. |

Khi sửa một lỗi giao diện, tìm mã màn hình trong bảng kiểm kê, mở luồng để xác định trạng thái, rồi đối chiếu trang và các tệp CSS, JS hoặc dữ liệu liên quan. Các tệp CSS và JS hiện mới có chú thích về trách nhiệm để nhóm có điểm bắt đầu khi triển khai. Giữ đường dẫn tài nguyên tương đối và ghi nguồn khi thêm ảnh, SVG hoặc mô hình.
