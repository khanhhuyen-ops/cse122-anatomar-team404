# Bố cục đáp ứng

Thiết kế từ viewport hẹp, giữ thứ tự DOM theo trình tự sử dụng. Các nhóm cột mở rộng theo chiều rộng và khả năng đọc. Tham chiếu [mã màn hình](../../../../design/screen-list.md).

## Khung và breakpoint

| Viewport | Lưới / lề ngoài / rãnh | Điều hướng | Atlas và dữ liệu |
| --- | --- | --- | --- |
| 320–639 px | 4 cột / 16 px / 12 px | Header gọn, nút «Menu». Dashboard có tên vai trò trong menu. | Một cột; vùng xem, cấu trúc và thông tin theo chiều dọc. |
| 640–1023 px | 8 cột / 24 px / 16 px | Header ngang nếu đủ chỗ. Menu thu gọn ở trang nhiều mục. | Atlas có thể đặt danh sách bên cạnh nếu vùng xem và thanh điều khiển còn đủ chỗ. |
| 1024–1279 px | 12 cột / 32 px / 24 px | Dashboard có sidebar 216 px, thu gọn nếu zoom. | Atlas hai cột. Sidebar cấu trúc khoảng 280 px, vùng xem chiếm phần còn lại. |
| Từ 1280 px | 12 cột / 32–48 px / 24 px | Sidebar dashboard 232 px. | Atlas tối đa ba vùng. Dành khoảng 240 px cho điều khiển và 288 px cho thông tin khi vùng xem còn ít nhất 520 px. |

Khung thông thường rộng tối đa 1280 px. Atlas tối đa 1440 px. Auth rộng tối đa 448 px. Study rộng tối đa 720 px. Nội dung ưu tiên căn trái. Form có nhóm trường theo thứ tự thao tác. Sticky header và thanh hành động chừa khoảng cuộn, safe area và khoảng trống cho focus. Bật zoom trình duyệt và cho hàng điều khiển xuống dòng.

## Public và Auth

X01 mở bằng tiêu đề, mô tả ngắn, nút «Khám phá các hệ cơ quan» và atlas 3D. Trên desktop, atlas cạnh nội dung. Trên mobile, tiêu đề và nút đứng trước atlas. Tooltip nằm trong vùng xem khi có hover hợp lệ, chi tiết khi chạm nằm bên dưới vùng xem. P01 đặt bộ lọc trước danh sách. P03 đặt «Gửi đề xuất» và «Tra cứu đề xuất» thành hai vùng có tiêu đề để có thể đến trực tiếp bằng liên kết. Trang xác thực giữ cùng khung logo, tiêu đề, form, thông báo và liên kết chuyển bước.

```text
X01 desktop                   X01 mobile / X02–X04
[Trang chủ | Khám phá | …]     [AnatomAR    Menu]
[Học giải phẫu] [Bản vẽ]       [Tiêu đề / mô tả]
[Khám phá các hệ cơ quan]      [Hành động / Form xác thực]
[Các hệ cơ quan]               [Sơ đồ / Lối về đăng nhập]
```

## Atlas và mô hình

S02 mở mô hình 3D toàn thân. P02 và S03 mở mô hình cơ quan. Header có tên hệ/cơ quan và hành động học liên quan. Thanh điều khiển nằm ngay dưới hoặc bên cạnh vùng xem. Mobile đưa bảng lớp, danh sách và một thẻ chi tiết xuống dưới vùng xem. Desktop đặt thẻ cạnh vùng xem. Khi xóa lựa chọn hoặc hủy biểu mẫu, trả focus về mục tương ứng trong danh sách nếu còn khả dụng. Khi bật bàn phím ảo, trang vẫn có thể cuộn tới các nút và văn bản.

```text
S02 / S03 desktop
[Điều hướng / Hệ cơ quan / Tên cơ quan]
[Hệ, lớp, tìm cấu trúc] [Mô hình 3D]                [Một cấu trúc]
[Danh sách cấu trúc]   [Điều khiển và góc nhìn]    [Vị trí, chức năng, nguồn]
                       [Trạng thái tải hoặc lỗi]

S02 / S03 mobile
[Tên hệ hoặc cơ quan]
[Chọn hệ]
[Vùng xem: tỷ lệ 4:3, giữ kích thước khi tải]
[Điều khiển thiết yếu] [Tùy chọn hiển thị]
[Tìm và chọn cấu trúc]
[Tên / Vị trí / Chức năng / Nguồn]
[Đánh dấu đã thuộc / Mở học liệu nếu phù hợp]
```

Ở màn hình trung bình, chuyển thẻ chi tiết xuống dưới và giữ danh sách cùng vùng xem nếu đủ chỗ. Vùng xem desktop dành chiều cao khoảng 420–640 px tùy viewport. Mobile ngắn hoặc ngang cho cuộn cả trang. Tải/rỗng/lỗi giữ vùng xem và điều khiển thay thế ở cùng vị trí. Ở 320 px, xếp điều khiển thành nhiều hàng. Toàn màn hình có lối thoát luôn nhìn thấy.

## Study

S04 và S05 dùng một cột, tiêu đề và tiến độ ở trên, câu hỏi hoặc thẻ ở giữa, điều hướng lượt học ở dưới. S06 giữ cùng khung cho điểm và từng câu. Bảng câu hỏi trong trắc nghiệm hiển thị bằng lưới nút có nhãn số/trạng thái, đặt trong mục có thể thu gọn trên mobile.

```text
[Về hệ cơ quan] [Thẻ 3/12 hoặc Câu 3/10]
[Câu gợi nhớ hoặc câu hỏi]
[Đáp án đã mở / Các lựa chọn]
[Quay lại] [Tiếp theo] [Kiểm tra và nộp]
[Trạng thái lưu bản nháp hoặc thông báo tại chỗ]
```

## Dashboard và Records

| Vai trò | Sidebar / menu theo thứ tự | Vùng nội dung ưu tiên |
| --- | --- | --- |
| Sinh viên | Tổng quan, Học theo hệ, Thẻ ghi nhớ, Trắc nghiệm | Học tiếp, số cơ quan đã thuộc theo hệ, lượt học gần đây |
| Giảng viên | Tổng quan, Quản lý mô hình, Học liệu SVG, Trắc nghiệm, Thẻ ghi nhớ, Lớp và tiến độ | Việc chờ xử lý, lớp, tiến độ theo hệ |
| Quản trị viên | Tổng quan, Người dùng, Hệ cơ quan, Thư viện mô hình, Hàng đợi duyệt, Cấu hình | Hàng đợi, số liệu tài khoản và liên kết công việc |

Thông báo, Hồ sơ và Cài đặt nằm trong header hoặc menu tài khoản. Danh sách đặt tiêu đề, hành động tạo và bộ lọc trên dữ liệu. Khi hẹp, cho bộ lọc xuống dòng và hiển thị bản ghi thành danh sách có nhãn trường. Bảng chi tiết cần giữ quan hệ hàng/cột có vùng cuộn đặt tên và cột nhận diện dễ thấy. Mobile vẫn truy cập được tất cả trường.

```text
Desktop                      Mobile
[Header / Hồ sơ / Thông báo]  [Menu] [Tiêu đề]
[Sidebar] [Tiêu đề + Tạo]     [Hành động]
[Sidebar] [Bộ lọc]            [Bộ lọc xếp dọc]
[Sidebar] [Bảng / Báo cáo]    [Danh sách hoặc vùng bảng]
```

## Editor

Form bắt đầu bằng dữ liệu nhận diện, tiếp theo nội dung, tài nguyên và nguồn. Desktop có thể đặt form và bản xem trước cạnh nhau. Mobile dùng nút «Xem trước» và quay về form cùng dữ liệu. Nút «Lưu bản nháp» và «Gửi duyệt» ở cuối nhóm công việc, cùng thông báo lưu. Trong T05, màn hình rộng đặt canvas SVG bên cạnh danh sách chú thích. Màn hình hẹp đặt lựa chọn cơ quan và trường tọa độ trước bản xem trước, giữ lối chỉnh sửa bằng bàn phím. Chi tiết A02/A04/A05 mở inline hoặc drawer khi có ngữ cảnh bảng. Khi hẹp, drawer phủ toàn chiều rộng và khôi phục focus về hàng mở nó.
