# Khả năng tiếp cận

Mục tiêu thiết kế là WCAG 2.2 AA. Tỷ lệ màu trong tài liệu áp dụng cho các cặp màu đặc. Kiểm tra toàn bộ giao diện và hành vi thực tế sau khi triển khai. [WCAG 2.2](https://www.w3.org/TR/WCAG22/).

| Chủ đề | Quy ước AnatomAR | Minh chứng cần kiểm tra khi triển khai |
| --- | --- | --- |
| Ngữ nghĩa và tiếng Việt | `lang="vi"`, tiêu đề trang duy nhất, landmark, skip link, thứ bậc heading và nhãn trường hiển thị. Tên Latin có khai báo ngôn ngữ phù hợp nếu cần. | Trình đọc màn hình nhận đúng tên vùng, điều khiển, vai trò và trạng thái. |
| Bàn phím và focus | Thứ tự Tab theo DOM. Dùng focus token 3 px ở cả nền sáng và tối. Sticky header, drawer và footer chừa khoảng cho phần tử focus. Modal khôi phục focus. | Đi hết F01, F02, F05–F07 và form duyệt bằng bàn phím. Escape rời hộp thoại và toàn màn hình. |
| Tương phản và màu | Chữ thường tối thiểu 4,5:1, chữ lớn 3:1, biên điều khiển và thông tin đồ họa thiết yếu theo ngưỡng 3:1. Trạng thái có chữ, hình hoặc kiểu viền. | Kiểm tra cặp màu ở trạng thái nghỉ, chọn, focus, lỗi, hover và trên nền mô hình thực tế. |
| Phóng to và bố cục lại | Dùng cỡ chữ có thể tăng. Giữ thao tác ở chiều rộng 320 CSS px. Bảng và hình cần không gian hai chiều có vùng riêng, danh sách/văn bản cho cùng thông tin thiết yếu. | Kiểm tra zoom 200% và reflow ở 320 CSS px. Header, bảng và thông báo vẫn dùng được. |
| Chạm và thao tác thay thế | Mục tiêu 44 × 44 CSS px cho điều khiển, vùng nút không chồng nhau. Có nút bấm hoặc nhập tọa độ thay kéo/thả, có zoom bằng nút và chọn từ danh sách. | Thử một ngón, bàn phím, chuột và thiết bị cảm ứng lai. Xác nhận trang vẫn cuộn ngoài vùng mô hình. |
| Tooltip 3D | Tooltip chỉ bổ trợ cho danh sách. Escape ẩn tên tạm, không chuyển focus. Chạm ngắn mở chi tiết, giữ vùng xem thoáng để thao tác. | Bàn phím, chạm và picking mở cùng một ID. Trình đọc màn hình thông báo khi chọn, không thông báo liên tục theo hover. |
| SVG, hình và canvas | Ảnh có nội dung dùng mô tả hữu ích, hình trang trí dùng mô tả rỗng. Mỗi cấu trúc có tên, vị trí và chức năng trong DOM. Hình câu hỏi dùng mô tả trung tính để duy trì mục đích kiểm tra và có phương án tương đương khi cần. | Kiểm tra tên cấu trúc và chuyển vùng chọn được ngay cả khi ẩn canvas hoặc tắt WebGL. |
| Chuyển động | Tôn trọng `prefers-reduced-motion` và cài đặt X06. Mặc định hoạt ảnh cơ quan dừng. Có điều khiển phát/dừng và mô tả chuyển động. | Thẻ đổi mặt tức thời, camera đổi góc trực tiếp khi giảm chuyển động, nút tạm dừng ổn định. |
| Form và xác thực | Có label, hướng dẫn, liên kết lỗi, hỗ trợ dán và tự điền. Nút hiện/ẩn mật khẩu có tên rõ. Mã reset demo có đường sao chép/dán. | Đăng nhập và đặt lại mật khẩu qua bàn phím. Sau lỗi nhiều trường, focus tới tóm tắt và quay lại nhập được. |
| Phản hồi | Dùng vùng `status` cho lưu thành công hoặc kết quả tải, vùng cảnh báo cho lỗi cần xử lý ngay. Thay đổi camera liên tục không đưa vào vùng đọc. | Nghe đúng một thông báo hữu ích khi đổi mô hình, lưu dấu hoặc nộp bài. |
| Bảng và biểu đồ | Giữ bảng ngữ nghĩa, caption và tiêu đề cột. Nhãn số liệu và liên kết tới bảng số cho biểu đồ. | Đọc tiến độ theo hệ từ bảng và văn bản bằng trình đọc màn hình. |

Các tiêu chí liên quan gồm tương phản 1.4.3/1.4.11, reflow 1.4.10, bàn phím 2.1.1, focus không bị che 2.4.11, thao tác kéo 2.5.7, kích thước mục tiêu 2.5.8, xác thực 3.3.8 và thông báo trạng thái 4.1.3. Quy ước 44 px là mục tiêu thiết kế của AnatomAR. [WCAG 2.2](https://www.w3.org/TR/WCAG22/) · [Web Interface Guidelines](https://github.com/vercel-labs/agent-skills/blob/main/skills/web-design-guidelines/references/command.md).

Ma trận kiểm tra dự kiến gồm Chrome/Edge với bàn phím, NVDA trên Windows, một trình duyệt cảm ứng và chế độ giảm chuyển động. Kiểm tra ở 320, 390, 768, 1024 và 1440 CSS px. Thử ít nhất một luồng cho từng vai trò, một biểu mẫu có lỗi, một hộp thoại và việc chọn từ danh sách khi WebGL không sẵn sàng.

Với S02, chọn cùng cơ quan qua bàn phím phải cho cùng trạng thái và hành động như chạm trên mô hình. Khi mở hộp thoại, đưa focus đến tiêu đề hoặc điều khiển đầu tiên. Sau khi đóng, trả focus về điểm chọn nếu còn hiện hoặc về cơ quan tương ứng trong danh sách. Trình đọc màn hình cần nhận được trạng thái «Chưa có học liệu» và thông báo kết quả gửi đề xuất.
