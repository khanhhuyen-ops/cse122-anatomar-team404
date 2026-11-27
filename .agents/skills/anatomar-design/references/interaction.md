# Quy tắc tương tác

## Điều hướng và trạng thái

- Dùng đường dẫn tương đối trong `pages/`. Lưu `system`, `organ`, `structure`, `view`, truy vấn và bộ lọc vào URL khi cần chia sẻ hoặc quay lại. Ví dụ `student-system-view.html?system=circulatory&organ=organ.heart&view=svg`. S02 SVG giữ hệ và cơ quan đang học. Atlas giữ camera và lớp trong phiên. Hover hoặc tap xem nhanh thuộc trạng thái tạm của Atlas.
- Hộp thoại, thông báo tạm, dữ liệu nhập chưa gửi, mã tra cứu đề xuất và mật khẩu nằm ngoài URL. Bản nháp trắc nghiệm chỉ mở với đúng tài khoản. Liên kết thông báo kiểm tra lại quyền bản ghi.
- Giữ lịch sử Back/Forward có ý nghĩa. Thay đổi hệ, cơ quan hoặc chế độ là điều hướng có thể quay lại. Gõ từ khóa chưa áp dụng và điều chỉnh camera chỉ là trạng thái tạm. Khôi phục bộ lọc, vùng cuộn và tiêu điểm khi quay về danh sách.
- Trang báo truy cập X08 cho thiếu quyền hoặc hết phiên. X09 cho bản ghi không còn hoặc riêng tư ngoài phạm vi. Đích đăng nhập lại phải là đường dẫn nội bộ được phép.

## Các trạng thái quan sát được

| Trạng thái | Phản hồi | Hành động tiếp theo |
| --- | --- | --- |
| Đang tải | Khung giữ chỗ, tên tác vụ «Đang tải danh sách…» hoặc «Đang tải mô hình…». Giữ nội dung khác sử dụng được. | Chờ hoặc dùng dữ liệu/2D đã có nếu phù hợp. |
| Rỗng | Phân biệt chưa có dữ liệu và bộ lọc không có kết quả. | Tạo bản đầu tiên, chọn hệ khác hoặc xóa bộ lọc theo quyền. |
| Đang lưu | Nêu trạng thái, tạm chặn lặp thao tác. Giữ luồng đang nhập. | Khi xong, phản hồi ở cùng vùng hoặc chuyển theo luồng. |
| Thành công / hoàn thành | Tên thao tác đã hoàn thành, cập nhật trạng thái. | Mở kết quả hoặc tiếp tục công việc. |
| Lỗi có thể phục hồi | Mô tả nguyên nhân nếu biết, giữ đầu vào và dữ liệu đã xác nhận gần nhất. | Thử lại, sửa trường hoặc chọn phương án thay thế. |
| Vô hiệu hóa | Tài khoản có nhãn trạng thái. Nút không khả dụng có lý do cạnh nút khi cần. | Mở lại theo quyền hoặc thực hiện bước còn thiếu. |
| Đang chờ | Cho biết mục đang đợi duyệt. | Xem, hủy gửi nếu còn chờ, hoặc đợi quyết định. |
| Bị từ chối | Lý do hiển thị theo quyền của người xem. | Sửa và gửi lại học liệu. Đề xuất chủ đề vẫn tra cứu được. |
| Đã hủy / đã lưu trữ | Ghi rõ đối tượng đã dừng xử lý hoặc chuyển chỉ đọc. | Xem lịch sử, về danh sách, hoặc mở bản nháp nếu trước đó hủy gửi. |

Khi tải theo bộ lọc hoặc đổi cơ quan liên tiếp, chỉ áp dụng kết quả của lựa chọn mới nhất. Khi lưu hoặc nộp bài, tạo một thao tác logic cho mỗi lần xác nhận. Nếu phản hồi chưa rõ, dùng cùng mã thao tác khi thử lại. Xung đột phiên bản có «Tải lại dữ liệu», giữ phần người dùng vừa nhập để đối chiếu. [Hành vi API mô phỏng](mock-data.md).

## Form, lỗi và thao tác có tác động

1. Nêu trường bắt buộc và định dạng cạnh trường. Kiểm tra sau khi người dùng rời trường đã chạm hoặc bấm hành động. Giữ văn bản tiếng Việt đang gõ bằng bộ gõ khi xử lý Enter.
2. Khi gửi lỗi nhiều trường, đưa focus tới tóm tắt chứa liên kết về trường tương ứng, đồng thời hiển thị từng lỗi tại chỗ. Giữ nguyên giá trị đã nhập.
3. Cảnh báo khi rời một form có nội dung vừa thay đổi. «Ở lại» giữ form. «Rời trang» dùng bản đã lưu gần nhất. Lượt học và bản nháp đã lưu hiển thị «Học tiếp» sau khi quay lại.
4. Xác nhận trước khi nộp bài, đổi vai trò, vô hiệu hóa tài khoản, lưu trữ nội dung hoặc từ chối. Nêu tên bản ghi, hậu quả và tên hành động cụ thể. Đặt focus ban đầu vào nút «Hủy» khi hậu quả khó đảo.
5. Ưu tiên phản hồi tại vùng thao tác. Dùng toast ngắn khoảng 5 giây cho xác nhận nhẹ vì trạng thái chính đã được cập nhật trên trang. Giữ lỗi quan trọng cho tới khi xử lý. Với thao tác có thể đảo, như bỏ dấu đã thuộc, cho thực hiện thao tác đảo ở cùng vị trí.

## Bảo toàn tiến độ

- Khi đổi thẻ/câu, giữ dữ liệu của bước hiện tại. Thông báo lưu bản nháp khi kết quả thay đổi, tránh đọc lại ở từng lần bấm radio liên tiếp.
- Thẻ ghi nhớ có hành động mở đáp án rõ ràng. Trắc nghiệm có bước kiểm tra câu bỏ trống và xác nhận trước khi nộp. Câu hỏi giữ thứ tự của phiên đã mở.
- Giao diện nộp trắc nghiệm hiển thị số đã trả lời trong số câu. Kết quả riêng biệt có tổng số đúng, đáp án và giải thích. Trạng thái «Chưa có dữ liệu» và kết quả bằng 0 có cách trình bày khác nhau.
- Hộp thoại, thanh điều khiển sticky và thông báo tự động chừa vùng focus, vùng chạm và khoảng cuộn. Hoạt ảnh có thể dừng ngay và bỏ qua hiệu ứng không thiết yếu khi giảm chuyển động được bật.

Áp dụng [luồng người dùng](../../../../design/user-flow.md) cho trạng thái của từng vai trò. Thao tác đồ họa được đặc tả riêng trong [trình xem 3D](viewer-3d.md).
