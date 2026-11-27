# Đặc tả thành phần

Dùng [token chung](design-system.md) và bố cục theo [mẫu trang](layout.md). Các tên ở đây mô tả vai trò của thành phần trong giao diện để nhóm có thể dùng lại cùng cấu trúc HTML và CSS.

## Điều hướng, thao tác và nhập liệu

| Thành phần | Cấu tạo và biến thể | Hành vi và trạng thái |
| --- | --- | --- |
| Header, sidebar | Logo về X01. Liên kết theo vai trò. Menu tài khoản chứa Hồ sơ, Cài đặt, Thông báo và Đăng xuất. | `nav` có nhãn và `aria-current="page"` cho trang hiện tại. Nút menu công bố mở/đóng. Mục hiện tại có chữ và dấu chọn. |
| Breadcrumb | Danh sách «Hệ cơ quan / Hệ tuần hoàn / Tim». Mục cuối là trang hiện tại. | Liên kết quay về giữ hệ và bộ lọc trong URL. Tiêu đề dài được xuống dòng. |
| Nút và liên kết | Chính, phụ, văn bản, cảnh báo, biểu tượng. Vùng tương tác tối thiểu 44 × 44 px. | `button` cho thao tác, `a` cho điều hướng. Mặc định, hover, focus, nhấn, đang xử lý, vô hiệu hóa. Nút biểu tượng có tên đọc được. Dùng `aria-pressed` cho nút bật/tắt có nhãn cố định. |
| Trường form | Nhãn hiển thị, dấu bắt buộc, ô nhập, trợ giúp, lỗi. `fieldset` và `legend` cho nhóm lựa chọn. | Tự điền phù hợp. Nêu yêu cầu trước khi nhập. Lỗi kết nối với trường, giữ dữ liệu hợp lệ. Trường chỉ đọc còn có thể đọc/sao chép. |
| Tìm kiếm và bộ lọc | Ô tìm, danh sách hệ/trạng thái, số kết quả và «Xóa bộ lọc». | Tìm hỗ trợ không dấu và tên khác có nguồn. Lựa chọn hiển thị nguyên dấu. Bộ lọc nối URL, Enter vẫn có thể thực hiện tìm. Lỗi giữ giá trị. |
| Chuyển nhóm nội dung | Liên kết dạng tab khi có URL riêng. Dùng tab bàn phím chuẩn cho nhóm panel cùng trang. | Chỉ báo mục hiện tại có chữ và gạch/viền. `Tab` tới widget, phím mũi tên đổi tab nội bộ. Panel rỗng có hướng dẫn. |
| Nhãn trạng thái | Nhãn ngắn, icon tùy chọn, nền theo nghĩa. Dùng trong bảng, thẻ và báo cáo. | Hiển thị trọn nhãn hoặc cho xuống dòng. Ý nghĩa còn đọc được khi tắt màu. Nhãn «Vô hiệu hóa» của tài khoản khác trạng thái nút bị vô hiệu hóa. |
| Hộp thoại / ngăn chi tiết | Tiêu đề, bối cảnh, tác động, nút đóng/«Hủy» và nút hành động. | Dùng dialog khi cần quyết định hoặc khi mở ngăn modal. Khoanh focus, hỗ trợ Escape trước khi gửi, trả focus. Khi thay đổi chưa lưu, hiển thị xác nhận theo [tương tác](interaction.md). |
| Phản hồi và tải | Banner/vùng lỗi, toast ngắn, skeleton, progress, thông báo rỗng. | Lỗi cần xử lý và thông báo mất kết nối tồn tại tại vùng liên quan. Toast chỉ xác nhận thao tác nhẹ; lỗi quan trọng có cách khôi phục. Skeleton giữ kích thước và thông báo tải qua vùng trạng thái. |

## Atlas và học liệu

| Thành phần | Cấu tạo và biến thể | Hành vi và trạng thái |
| --- | --- | --- |
| Thẻ hệ / cơ quan | Ảnh hoặc SVG, tên tiếng Việt, số cơ quan hoặc mô tả ngắn, liên kết đến hệ/mô hình. | Liên kết chính có tên rõ. Ảnh có kích thước dự kiến. Mẫu công khai, chi tiết sinh viên, chưa có ảnh. Hiển thị nguồn khi mở chi tiết. |
| Vùng atlas và thanh điều khiển | Canvas toàn thân, lớp giải phẫu, điều khiển camera và bảng thông tin nhanh. | Giữ kích thước khi tải. Các điều khiển HTML dùng được cùng nội dung đọc thay thế. [Đặc tả trình xem](viewer-3d.md). |
| Chế độ Sơ đồ SVG | Bóng cơ thể, bộ chọn hệ, hotspot trong hệ tọa độ `viewBox` và danh sách cơ quan. | Hình, danh sách, tình trạng và chi tiết dùng cùng ID. Mỗi hotspot có biến thể Mặc định, Hover, Đã chọn và hai tình trạng học liệu. Bàn phím và chạm dùng cùng hành động chọn. |
| Tooltip Atlas 3D | Tên, hệ, vị trí, chức năng. Nền tối đặc và phủ xanh ngọc bán trong suốt trên phần bề mặt đang thấy. | Neo theo điểm chiếu của cơ quan. Rời bề mặt ẩn cả tooltip và highlight. Mobile chạm để mở, chạm lại hoặc đóng để ẩn. |
| Danh sách và chi tiết cấu trúc | Tên, hệ, mô tả, vị trí, chức năng và nguồn của một cấu trúc. | Chọn từ danh sách tương đương click hoặc chạm hình học đã ánh xạ. Chọn mới thay mục đang học. Chi tiết giữ sau khi di chuột, chuyển focus hoặc thay camera. |
| Thẻ học liệu cơ quan | Tên cơ quan, hệ, trạng thái học liệu và một hành động chính. | «Xem mô hình» khi có mô hình được phép xem. «Chưa có học liệu» và «Gửi đề xuất học liệu» khi thiếu. Thẻ có lối đóng. Khi đang kiểm tra hoặc lỗi, giữ tên và cơ quan đã chọn. |
| Dấu đã thuộc cơ quan | Nút «Đánh dấu đã thuộc» và trạng thái xác nhận «Đã thuộc», với hành động «Bỏ đánh dấu». | Đang lưu, thành công, lỗi có thử lại. Tính tiến độ sau khi thao tác đã lưu. Nút giữ focus khi nhãn đổi. |
| Thẻ ghi nhớ | Bộ đếm, mặt gợi nhớ có tên/hình, nút «Hiện đáp án», mặt vị trí/chức năng, hai nút đánh giá. | Chuyển mặt bằng click và bàn phím. Trình đọc màn hình chỉ đọc mặt đang mở. Giảm chuyển động đổi nội dung ngay. Rỗng, đang ôn, lưu lỗi, kết thúc lượt. |
| Câu hỏi và bảng câu | `fieldset` và radio cho câu một đáp án. Bảng câu là nhóm nút có số và trạng thái. | Có chưa trả lời, đã chọn, đang mở. Đáp án và giải thích xuất hiện ở trang kết quả. Khi chuyển câu, đưa focus tới tiêu đề câu. |
| Chi tiết kết quả | Điểm, số đúng/tổng, lựa chọn đã chọn, đáp án và giải thích. Có bộ lọc «Tất cả / Cần xem lại» nếu danh sách dài. | Đúng/sai/bỏ trống có nhãn chữ. S06 giữ dữ liệu lượt đã nộp. Có «Làm lại» và «Xem lại hệ cơ quan». |
| Editor học liệu SVG | Chọn mẫu, chọn cơ quan, danh sách nhiều chú thích, tọa độ hoặc nút dịch điểm và bản xem trước. | Thêm, sửa, xóa từng chú thích. Bản xem trước đọc cùng bản nháp. Kiểm tra liên kết, phạm vi tọa độ và ưu tiên phím cho tác vụ kéo hoặc sắp thứ tự. |
| Editor trắc nghiệm | Danh sách câu, bốn phương án A–D, một đáp án đúng và lời giải thích cho từng câu. | Có thêm, sửa, xác nhận xóa, lưu nháp, xem trước và gửi duyệt. Form và bản xem trước đọc cùng câu trong bản nháp. |

## Dữ liệu, báo cáo và xử lý

| Thành phần | Cấu tạo và biến thể | Hành vi và trạng thái |
| --- | --- | --- |
| Tóm tắt tiến độ | Tên hệ, số đã thuộc/tổng, nhãn trạng thái, thanh tiến độ. Thẻ số liệu có kỳ hoặc phạm vi. | Tổng bằng 0 hiện «Chưa có học liệu». Số liệu có thể đọc bằng văn bản và nhất quán giữa S01/T04. |
| Bảng và phân trang | Caption hoặc tiêu đề, tiêu đề cột, dòng dữ liệu, nút thao tác có tên bản ghi. | Thể hiện thứ tự sắp xếp, giữ bộ lọc khi chuyển trang. Hàng mới/chờ/từ chối có nhãn. Trên mobile dùng danh sách có nhãn hoặc vùng cuộn có tên nếu cần so sánh cột. |
| Danh sách thông báo | Tóm tắt sự kiện, thời gian, trạng thái chưa đọc và đường dẫn tới bản ghi. | Thông báo đã đọc còn truy cập được. Liên kết cũ có đường quay về. Huy hiệu số đi kèm tên «Thông báo chưa đọc». |
| Hàng đợi duyệt | Hai nhóm «Học liệu gửi duyệt» và «Đề xuất chủ đề». Mỗi mục có dữ liệu, trạng thái, người gửi nếu phù hợp, quyết định và lý do. | Từ chối yêu cầu lý do. Duyệt, hủy hay từ chối chỉ chuyển trạng thái khi đã lưu. Xử lý xung đột và thử lại ở cùng mục. |
| Form CRUD | Nhóm thông tin, quan hệ hệ/cơ quan, nguồn hoặc quyền, cuối form là hành động. | Có tạo/sửa/xem chỉ đọc. Chưa lưu có xác nhận rời trang. Lưu trữ/vô hiệu hóa hiển thị tác động và bản ghi phụ thuộc. |

## Nhãn mẫu

| Tình huống | Nội dung và hành động |
| --- | --- |
| Danh sách rỗng do bộ lọc | «Không tìm thấy cơ quan phù hợp.» → «Xóa bộ lọc» |
| Hệ chưa có dữ liệu | «Hệ này chưa có học liệu.» → «Chọn hệ khác» |
| Lỗi lấy mô hình | «Không tải được mô hình 3D.» → «Thử lại» hoặc đọc chi tiết từ danh sách |
| Lỗi ghi dấu | «Chưa lưu được dấu đã thuộc.» → «Thử lại» |
| Form chưa lưu | «Các thay đổi trong biểu mẫu chưa được lưu.» → «Ở lại» hoặc «Rời trang» |
| Thành công gửi chủ đề | «Đã gửi đề xuất.» + mã tra cứu và trạng thái «Đang chờ» |
| Thành công gửi đề xuất từ SVG | «Đã gửi đề xuất», «Đang chờ phản hồi» và «Quay lại sơ đồ». Sinh viên theo dõi phản hồi trong Thông báo. |

Từng thành phần được kiểm tra ở trạng thái nghỉ, focus và lỗi, với nhãn tiếng Việt dài, bàn phím và viewport hẹp. [Yêu cầu tiếp cận](accessibility.md).
