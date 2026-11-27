# Hệ thống thiết kế

Các tên dưới đây là tên CSS custom properties dự kiến. Dùng token theo vai trò để nút, form, atlas và dashboard nhất quán. Màu tài liệu và màu mô hình được quản lý riêng.

## Màu giao diện sáng

| Token | Giá trị | Dùng cho |
| --- | --- | --- |
| `--page` | `#F3F8FA` | Nền trang |
| `--surface` | `#FFFFFF` | Nội dung, form, bảng, tooltip sáng |
| `--surface-muted` | `#E8F1F4` | Vùng hỗ trợ, ô chỉ đọc, nền tải |
| `--ink` | `#18313D` | Tiêu đề và văn bản chính |
| `--ink-muted` | `#455D6A` | Chú thích và mô tả phụ |
| `--divider` | `#CFDFE6` | Đường phân cách trang trí giữa các vùng |
| `--control-border` | `#718896` | Biên điều khiển cần nhìn rõ |
| `--primary` | `#086458` | Hành động chính và nhãn chọn |
| `--primary-hover` | `#074D44` | Nút chính khi trỏ |
| `--primary-pressed` | `#073F38` | Nút chính khi nhấn |
| `--on-primary` | `#FFFFFF` | Văn bản trên nền hành động chính |
| `--selected` | `#D9F1E8` | Nền hàng hoặc lựa chọn đang chọn, dùng chữ `--primary` |
| `--link` | `#005BB2` | Liên kết văn bản có gạch chân |
| `--focus` | `#005FCC` | Viền focus ở bề mặt sáng |
| `--danger` | `#A12D3B` | Nút xác nhận từ chối, lưu trữ hoặc vô hiệu hóa, dùng chữ trắng |

## Màu trạng thái

| Ý nghĩa | Token chữ / nền | Giá trị chữ / nền | Ví dụ |
| --- | --- | --- | --- |
| Thông tin | `--info-ink` / `--info-bg` | `#194D7B` / `#E5F0FB` | Đang học, hướng dẫn, đang tải |
| Tích cực | `--success-ink` / `--success-bg` | `#175941` / `#E4F3EB` | Đã thuộc, đã xuất bản, hoàn thành |
| Chờ hoặc cần xem lại | `--warning-ink` / `--warning-bg` | `#714600` / `#FFF0D3` | Đang chờ, cần ôn lại, kết nối gián đoạn |
| Lỗi hoặc từ chối | `--error-ink` / `--error-bg` | `#8C2F3D` / `#FBE7EA` | Lỗi lưu, bị từ chối, vô hiệu hóa |
| Trung tính | `--ink-muted` / `--surface-muted` | `#455D6A` / `#E8F1F4` | Bản nháp, đã hủy, đã lưu trữ, chưa bắt đầu |

Dùng nhãn văn bản cho mọi trạng thái. Bảng và dashboard dùng màu trạng thái trên nhãn nhỏ hoặc thanh tiến độ. Trong biểu đồ, thêm nhãn, hình dạng hoặc họa tiết và bảng số liệu tương ứng.

| Mẫu giao diện | Quy tắc dùng token trong lượt hoàn thiện prototype |
| --- | --- |
| Chuyển Atlas 3D / Sơ đồ SVG | Nút đang chọn dùng `--selected` và `--primary`. Nút còn lại dùng `--surface`, có đường viền. Focus theo nền hiện tại. |
| Trường và lựa chọn A–D | Trường dùng `--control-border`. Chỉ đọc dùng `--surface-muted`. Lỗi có chữ giải thích và viền `--danger`. Mỗi nhóm đáp án có một trạng thái đã chọn. |
| Hộp thoại và ngăn chi tiết | Nền `--surface`, bo `--radius-panel`, hành động tối thiểu `--target-min`. Xác nhận lưu trữ, vô hiệu hóa hoặc từ chối dùng `--danger`. |
| Hotspot SVG | Mặc định vòng nhỏ, Hover mở rộng vòng, Đã chọn có vòng đậm. Dấu kiểm xanh ngọc chỉ có học liệu, dấu trừ hổ phách chỉ chưa có học liệu. Kèm nhãn trạng thái bằng chữ ở chi tiết. Dùng ID và tọa độ trong cùng `viewBox` với hình. |

Thẻ hệ cơ quan dùng nền dịu và chữ đậm theo chủ đề. Tuần hoàn dùng `#FBE7EA` / `#8C2F3D`, hô hấp dùng `#E5F0FB` / `#194D7B`, thần kinh dùng `#F0EAFB` / `#5A4791`, xương khớp dùng `#D9F1E8` / `#086458` và tiêu hóa dùng `#FFF0D3` / `#714600`. Mỗi thẻ có tên hệ bằng chữ và biểu tượng. Ý nghĩa của nhãn quy trình vẫn tuân theo bảng trạng thái.

## Màu vùng atlas

| Token | Giá trị | Dùng cho |
| --- | --- | --- |
| `--atlas-stage` | `#101F2A` | Nền vùng xem, màu mặc định trong sơ đồ |
| `--atlas-panel` | `#1A303D` | Thanh điều khiển, nền chú thích đặc |
| `--atlas-ink` | `#F3F8FA` | Nhãn trên nền tối |
| `--atlas-muted` | `#BED3DA` | Chú thích phụ và đường dẫn nhãn |
| `--atlas-border` | `#72909E` | Biên điều khiển trên nền tối |
| `--atlas-focus` | `#86DCF2` | Viền focus của nút trong vùng tối |
| `--atlas-selection` | `#79E4C8` | Lớp phủ 60% trên phần bề mặt cơ quan đang thấy ở Atlas, màu nhấn tooltip và viền cấu trúc ở trình xem chi tiết |
| `--atlas-on-selection` | `#0C221E` | Chữ trên nền nhãn chọn |

Giữ màu mô theo dữ liệu đã duyệt. Mọi đường chỉ dẫn phải đọc được ở cả vùng mô sáng và tối bằng đường viền hai tông hoặc nhãn có nền đặc. Ở sơ đồ SVG dùng viền, ký hiệu và danh sách tên để bổ sung cho màu. Thứ tự lớp và cách chọn nằm trong [trình xem 3D](viewer-3d.md).

Đối chiếu màu đặc theo tỷ lệ WCAG. Chữ chính trên trắng đạt 13,59:1, chữ phụ trên nền trang 6,48:1, chữ trắng trên nút chính 7,06:1, biên điều khiển trên nền trang 3,46:1. Chữ atlas trên nền thanh điều khiển đạt 12,79:1. Viền focus đạt 5,04:1 trên nền chọn sáng và 8,82:1 trên nền thanh điều khiển tối. Kiểm tra lại khi thay đổi nền, độ trong suốt hoặc điều kiện hiển thị. [Tiêu chí tương phản WCAG 2.2](https://www.w3.org/TR/WCAG22/#contrast-minimum).

## Kiểu chữ

`--font-reading` dùng Be Vietnam Pro, dự phòng system-ui và sans-serif. `--font-display` dùng Literata, dự phòng Georgia và serif. Cả hai font chính có bộ ký tự tiếng Việt. Dùng weight 400, 600, 700 cho giao diện và 600 cho tiêu đề Literata. Tải font theo dung lượng cần thiết, hiển thị ngay bằng font dự phòng trong lúc tải. [Be Vietnam Pro](https://fonts.google.com/specimen/Be+Vietnam+Pro) · [Literata](https://fonts.google.com/specimen/Literata).

| Token kiểu chữ | Cỡ / dòng | Dùng cho |
| --- | --- | --- |
| `--type-display` | 36–56 px / 1,14 | Tiêu đề mở đầu, tăng theo chiều rộng |
| `--type-h1` | 28–40 px / 1,22 | Tên trang, tên cơ quan, dashboard |
| `--type-h2` | 22–28 px / 1,30 | Nhóm thông tin |
| `--type-h3` | 18–20 px / 1,40 | Tựa thẻ, vùng chi tiết |
| `--type-body` | 16 px / 1,60 | Văn bản mặc định và giá trị nhập liệu |
| `--type-ui` | 14–16 px / 1,45 | Nút, nhãn, bảng. Dùng tối thiểu 16 px cho trường nhập |
| `--type-caption` | 12–13 px / 1,50 | Nguồn, tác giả và metadata phụ |

Dùng `rem` cho cỡ chữ trong triển khai, quy đổi từ mặc định 16 px. Nội dung đọc dài rộng tối đa khoảng 70 ký tự. Cột số căn phải và dùng số có độ rộng đều. Tiêu đề, nhãn và nút dùng kiểu câu tiếng Việt. Giữ dấu tiếng Việt cả khi tìm kiếm có hỗ trợ nhập không dấu.

## Không gian, hình khối và chuyển động

| Token | Giá trị |
| --- | --- |
| `--space-1`, `--space-2`, `--space-3`, `--space-4` | 4, 8, 12, 16 px |
| `--space-5`, `--space-6`, `--space-8`, `--space-10`, `--space-12`, `--space-16` | 20, 24, 32, 40, 48, 64 px |
| `--radius-control`, `--radius-panel`, `--radius-stage` | 8, 12, 16 px |
| `--target-min`, `--target-gap` | 44 × 44 px, khoảng cách 8 px khi xếp nút liền nhau |
| `--focus-width`, `--focus-gap` | 3 px, 3 px. Dùng đường phân cách nền sáng khi focus nút nền đậm |
| `--shadow-overlay` | 0 10px 28px rgba(16, 31, 42, 0.16) |
| `--icon-small`, `--icon-default` | 16, 20 px. Kích thước biểu tượng nằm trong vùng chạm |
| `--motion-quick`, `--motion-panel`, `--motion-camera` | 120, 180, tối đa 240 ms |
| `--ease-ui` | cubic-bezier(0.2, 0, 0, 1) |
| `--z-base`, `--z-sticky`, `--z-popup`, `--z-modal`, `--z-status` | 0, 10, 20, 30, 40 |

Khung nội dung dùng đường viền hoặc khoảng cách. Bóng đổ dành cho lớp phủ. Chuyển động nhẹ giải thích mở/đóng hoặc thay đổi vị trí. Với giảm chuyển động, giữ thay đổi trạng thái và bỏ lật thẻ hoạt hình, chuyển cảnh camera, nền động. Hoạt ảnh giải phẫu chỉ phát khi người dùng yêu cầu.
