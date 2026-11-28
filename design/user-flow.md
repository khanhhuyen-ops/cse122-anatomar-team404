# Luồng người dùng AnatomAR

Các mã màn hình trỏ đến [bảng kiểm kê](screen-list.md). Phạm vi chức năng theo [yêu cầu dự án §§06–13, 22](../.agents/skills/AnatomAR-project-requirements.md). Phân công người duyệt, phạm vi lớp, chính sách mock và cách tính tiến độ là quy tắc thiết kế đề xuất. [Trạng thái và dữ liệu](../.agents/skills/anatomar-design/references/mock-data.md).

## Sitemap

| Phạm vi | Điểm vào và trang trực thuộc |
| --- | --- |
| Công khai | X01 → P01 hệ cơ quan, P02 mô hình mẫu, P03 gửi hoặc tra cứu đề xuất. X02 đăng nhập → X03 đăng ký hoặc X04 đặt lại mật khẩu. |
| Sinh viên | S01 → Lớp của tôi → nhập mã lớp → xem lớp đã tham gia. S01 → S02 học theo hệ. Atlas 3D mở thông tin nhanh tại chỗ. Sơ đồ SVG → chọn hệ và cơ quan → S03 mô hình chi tiết hoặc hộp thoại đề xuất → X07 Thông báo. S01/S02 → S04 → S06. S01/S03 → S05. |
| Giảng viên | T01 → T02 cơ quan và mô hình → T06 biên tập. T01 → T03 câu hỏi, T05 sơ đồ SVG, T08 thẻ hoặc T07 quản lý lớp. T07 → tạo lớp → sao chép mã, xem thành viên hoặc mở T04. Hộp thoại Đề xuất học liệu mở từ T01 hoặc X07. |
| Quản trị viên | A01 → A02 tài khoản, A03 hệ cơ quan, A04 thư viện, A05 hàng đợi, A06 cấu hình công khai. A05 dùng ngăn chi tiết cho học liệu và đề xuất. |
| Sau đăng nhập | Menu của phiên → X05 hồ sơ, X06 cài đặt, X07 thông báo, xác nhận đăng xuất → X01. X08 thiếu quyền hoặc hết phiên. X09 nội dung không còn truy cập được. |

Các bước đặt lại mật khẩu, kết quả tra cứu, CRUD ngắn, xem trước, chỉnh chú thích và xác nhận nằm trong trang mở chúng. Desktop và Mobile dùng cùng mã màn hình và cùng đích nghiệp vụ. Mobile đưa các đích vào menu chạm và mở ngăn chi tiết gần toàn màn hình.

## F01 · Khám phá khóa học và học liệu mẫu

**Khách · X01 → P01 → P02.** Từ trang chủ chọn «Khám phá các hệ cơ quan». Xem tổng quan, lọc theo tên hoặc hệ rồi chọn mô hình công khai, ví dụ tim hoặc xương. P02 hiển thị tên, phần học mẫu, nguồn và điều khiển mô hình. Từ đây có thể mở mô hình mẫu khác, trở lại danh sách hoặc đăng ký bằng X03 để học sâu hơn.

Nếu lọc không có kết quả, «Xóa bộ lọc» khôi phục danh sách công khai. Nếu mẫu đang lưu trữ hoặc đã bị gỡ, trở về P01 qua X09. Nút quay về giữ bộ lọc còn hợp lệ.

Tại X01, khách có thể khám phá mô hình 3D toàn thân ngay trên trang chủ. Mỗi lớp giải phẫu có điều khiển riêng để quan sát một lớp hoặc chồng nhiều lớp.

Người học kéo để xoay quanh cơ thể và dùng điều khiển thu phóng. Trên desktop, rê trên bề mặt cơ quan để làm nổi và xem thông tin nhanh. Trên mobile, chạm cơ quan để mở thông tin ngay trong vùng xem, kéo một ngón để xoay và chụm hai ngón để thu phóng.

## F02 · Định vị cơ quan và khám phá mô hình

**Khách · P02. Sinh viên · S02.** P02 mở mô hình mẫu. S02 có hai chế độ cùng điều hướng.

- **Atlas 3D.** Xoay, thu phóng, đặt lại góc nhìn và bật/tắt lớp. Rê vào bề mặt cơ quan đang thấy để phủ xanh ngọc bán trong suốt và mở tooltip theo vị trí cơ quan, gồm tên, hệ, vị trí và chức năng. Rời vùng hợp lệ ẩn cả hai. Trên Mobile, chạm cơ quan để mở, chạm lại hoặc bấm đóng để ẩn. Chọn trong bảng «Thông tin nhanh» là đường thay thế để đọc nội dung.
- **Sơ đồ SVG.** Chọn hệ. Bấm hoặc chạm hotspot neo vào `viewBox` của sơ đồ, hoặc chọn cơ quan tương ứng trong danh sách. Cả hai mở cùng ID, vị trí, chức năng và tình trạng học liệu. Desktop dùng hover để báo vùng tương tác. Chạm chọn trực tiếp trên Mobile. Chuyển hệ đưa về sơ đồ mặc định của hệ mới.
- **Có mô hình 3D đã xuất bản và được phép xem.** Từ chi tiết trên SVG, «Xem mô hình 3D» mở S03 cho cơ quan tương ứng. Quay lại S02 ở sơ đồ và cơ quan đang học.
- **Chưa có học liệu.** Từ chi tiết trên SVG, «Gửi đề xuất học liệu» mở form hiện có với cơ quan, hệ và người nhận. Bản ghi đang chờ đưa người dùng đến Thông báo. Xem F03.

Khi triển khai, lưu hệ và lựa chọn học liệu cho chế độ SVG. Atlas giữ camera, zoom và lớp trong phiên. Tooltip chỉ tồn tại trong chế độ Atlas. Trong SVG, hiện «Đang kiểm tra học liệu…» khi chờ. Khi kiểm tra lỗi, giữ cơ quan đã chọn và cho thử lại.

Ở P02/S03, người dùng chọn một cấu trúc từ danh sách hoặc hình học đã ánh xạ. Sau xoay, dịch, zoom, reset hoặc thay lớp, hover tính theo hình đang thấy. Khi phát hoạt ảnh, hover được kiểm tra theo pose hiện tại ngay cả khi con trỏ đứng yên. Khi lớp chứa ID đang chọn bị ẩn, thẻ chi tiết giữ ID và cho «Hiện lớp». Khi WebGL hoặc GLB lỗi, danh sách và chi tiết bằng văn bản giữ bộ phận đang học. [Điều khiển và trạng thái 3D](../.agents/skills/anatomar-design/references/viewer-3d.md).

## F03 · Gửi và tra cứu đề xuất chủ đề

**Khách · P01 → P03.** Chọn «Đề xuất chủ đề». Chọn loại «Hệ cơ quan» hoặc «Cơ quan», nhập tên chủ đề và lý do. Kiểm tra các trường rồi «Gửi đề xuất». Thành công hiển thị mã tra cứu và trạng thái «Đang chờ». Khách dùng mã ở phần «Tra cứu đề xuất» để đọc trạng thái và phản hồi hiển thị công khai cho chính đề xuất đó.

**Sinh viên · S02 Sơ đồ SVG → X07.** Từ cơ quan chưa có học liệu, mở biểu mẫu, xem người nhận, nhập nội dung và xác nhận gửi. Form điền giảng viên phụ trách theo lớp hoặc hệ. Khi chưa có người phụ trách, form điền «Quản trị viên» và gửi vào hàng đợi quản trị. Thành công hiện «Đã gửi đề xuất», «Đang chờ phản hồi» và liên kết Thông báo. «Quay lại sơ đồ» giữ cơ quan đã chọn và hiện nút «Mở Thông báo». Nếu đã có đề xuất đang chờ của cùng sinh viên và cơ quan, dùng trạng thái đang chờ.

Khi ghi lỗi, giữ nội dung rồi «Thử gửi lại». Chặn tạo bản ghi trùng nếu người dùng gửi lại cùng yêu cầu đang xử lý. Mã sai có hướng dẫn kiểm tra lại. Sau F13, P03 hiển thị «Đã chấp nhận» hoặc «Bị từ chối» cùng lý do phù hợp. Chấp nhận ghi nhận đề xuất cho danh mục cần bổ sung.

## F04 · Tài khoản, phiên và thông tin cá nhân

**Người dùng · X01/X02/X03/X04 → S01/T01/A01 → X05/X06/X07.**

1. **Đăng nhập.** Nhập email và mật khẩu mẫu. Phiên hợp lệ đưa người dùng về dashboard theo vai trò, hoặc về đường dẫn nội bộ đã yêu cầu nếu hiện có quyền. Với thông tin sai, báo tại form. Tài khoản bị vô hiệu hóa được hướng dẫn liên hệ quản trị viên.
2. **Đăng ký.** Nhập tên, email, mật khẩu và xác nhận. Email trùng có lối về X02. Tạo tài khoản sinh viên thành công chuyển về X02 với email mẫu đã điền.
3. **Quên mật khẩu.** X04 thực hiện yêu cầu → nhập mã demo → đặt mật khẩu mẫu mới. Dùng cơ chế mô phỏng hiển thị và giải thích mã ngay trong demo. Mã đã dùng hoặc hết hạn có lối «Tạo mã mới». Đổi xong quay về X02.
4. **Sau đăng nhập.** X05 sửa tên hiển thị, email và vai trò ở chế độ chỉ đọc. X06 lưu lựa chọn giảm chuyển động. X07 xem thông báo, đánh dấu đã đọc và mở bản ghi còn được phép. X05–X07 giữ điều hướng của vai trò đang dùng. «Đăng xuất» mở xác nhận, xóa phiên mô phỏng và về X01.
5. **Truy cập.** Hết phiên tại trang riêng thì mở X08 với «Đăng nhập lại». Chọn đích quay lại từ trang nội bộ được phép. Thiếu quyền có «Về khu vực của tôi». X09 dùng cho bản ghi mất, nội dung đã ẩn hoặc bản ghi riêng ngoài phạm vi mà không cần tiết lộ sự tồn tại. Lỗi kết nối ưu tiên thông báo tại vùng nội dung và nút thử lại.

## F05 · Học theo hệ và cập nhật mức ghi nhớ

**Sinh viên · S01 → S02 Sơ đồ SVG → S03 → S01.** Mở hệ cần học từ bảng điều khiển. Chọn cơ quan trên sơ đồ và mở mô hình đã xuất bản theo F02. Tại S03, xem cấu tạo, điều khiển hoạt ảnh rồi dùng «Đánh dấu đã thuộc» để tạo dấu ghi nhớ. Thành công đổi trạng thái thành «Đã thuộc» và cho phép «Bỏ đánh dấu».

Khi quay về S01, từng hệ hiện số cơ quan đã đánh dấu trên tổng cơ quan đang xuất bản của hệ. Hiển thị «Chưa học», «Đang học» hoặc «Hoàn thành» theo số đếm. Hệ chưa có cơ quan hiển thị «Chưa có học liệu». Khi ghi thất bại, giữ trạng thái đã xác nhận trước đó và cho phép thử lại. S01 và T04 dùng cùng cách tính.

## F06 · Ôn thẻ ghi nhớ

**Sinh viên · S01/S03 → S05.** Chọn hệ hoặc nhóm thẻ liên quan và bấm «Bắt đầu ôn». Mỗi bước trình bày một câu gợi nhớ bằng tên hoặc hình. «Hiện đáp án» mở vị trí/chức năng. Chọn «Đã thuộc» hoặc «Cần ôn lại» rồi sang thẻ kế tiếp. Có nút về thẻ trước, chỉ báo thẻ hiện tại trên tổng và «Thoát lượt ôn».

Kết thúc lượt hiển thị số thẻ đã đánh giá và hành động «Ôn lại thẻ cần ôn». Có thể tiếp tục một lượt dở từ S01 hoặc S05. Nếu không có thẻ được xuất bản, S05 dẫn về hệ khác. Đánh giá thẻ thuộc kết quả ôn thẻ. Dấu ghi nhớ cơ quan dùng thao tác riêng tại S03. Giảng viên dùng T08 để soạn và gửi duyệt thẻ theo F09/F10.

## F07 · Làm và xem kết quả trắc nghiệm ghi nhớ

**Sinh viên · S01/S02 → S04 → S06.** Chọn hệ và bài, đọc mục tiêu, số câu và cách chấm. «Bắt đầu làm bài» mở một bản nháp cố định bộ câu. Mỗi bước hiển thị câu hỏi về vị trí hoặc chức năng cùng nhóm lựa chọn. Cho phép quay lại, đổi đáp án và tiếp tục khi mở lại phiên. Mỗi câu có một đáp án đúng. Thời gian làm do sinh viên tự điều chỉnh.

«Kiểm tra và nộp» mở tóm tắt câu đã trả lời, câu bỏ trống và liên kết đi tới từng câu. Hộp thoại xác nhận ghi rõ câu bỏ trống tính 0 điểm và kết quả sẽ được lưu. Chỉ chuyển sang S06 khi đã ghi nhận lượt làm. Lỗi giữ bản nháp và cho nộp lại cùng lượt.

S06 hiển thị số đúng/tổng, tỷ lệ, đáp án đã chọn, đáp án đúng và giải thích, kể cả câu sai hoặc bỏ trống. «Làm lại» tạo lượt mới. «Xem lại hệ cơ quan» quay về S02 ở đúng hệ. Khi chưa từng làm, S01 hiển thị «Chưa có lượt làm» tại phần điểm.

## F08 · Tạo lớp, tham gia bằng mã và đọc tiến độ

**Giảng viên · T01 → T07.** Chọn «Tạo lớp», nhập tên và lưu. Khi tạo thành công, lớp ở trạng thái «Đang mở» và hệ thống cấp một mã duy nhất. Hộp thoại hiển thị tên lớp, mã dạng chỉ đọc và nút «Sao chép mã» để giảng viên tự chia sẻ. Giảng viên có thể mở lại mã của lớp đang mở từ danh sách lớp mình phụ trách. Đổi tên lớp giữ cùng mã. Lớp đã lưu trữ giữ danh sách và báo cáo ở chế độ chỉ đọc và dừng nhận thành viên qua mã. Giảng viên vẫn có thể thêm tài khoản sinh viên từ danh sách hoặc gỡ thành viên theo quyền hiện có.

**Sinh viên · S01 → Lớp của tôi.** Từ bảng điều khiển, chọn «Tham gia lớp», nhập hoặc dán mã giảng viên cung cấp, rồi xác nhận. Lớp đang mở với mã hợp lệ được thêm ngay vào danh sách và tên lớp xuất hiện trong xác nhận. Cùng thao tác cập nhật danh sách thành viên mà giảng viên xem tại T07 và dùng tại T04. Nếu đã là thành viên, hiện «Bạn đã tham gia lớp này» và giữ một mục trong danh sách. Mã trống, không hợp lệ hoặc lớp đã lưu trữ có thông báo tại form. Khi kết nối lỗi, giữ mã đã nhập để thử lại. Chỉ tài khoản Sinh viên đang hoạt động dùng luồng này.

T04 yêu cầu giảng viên chọn một lớp mình quản lý, một sinh viên trong danh sách và hệ hoặc «Tất cả hệ». Báo cáo ghi tỷ lệ cơ quan đã thuộc theo hệ, tình hình ôn thẻ và lượt trắc nghiệm gần nhất. Giữ trạng thái «Chưa có dữ liệu» riêng với «0 câu đúng». Giảng viên có thể quay về T07 để cập nhật danh sách. Dữ liệu học cá nhân được giữ khi gỡ một sinh viên. Phạm vi xem sinh viên đó được cập nhật theo danh sách lớp.

## F09 · Soạn cơ quan, trắc nghiệm, sơ đồ và thẻ

**Giảng viên · T01 → T02/T03/T05/T08.**

| Loại | Trình tự | Kiểm tra trước khi gửi duyệt |
| --- | --- | --- |
| Cơ quan và mô hình | T02 lọc theo hệ/trạng thái → T06 tạo/sửa → chọn hệ, vị trí trên sơ đồ và tệp mẫu từ thư viện → đặt góc mặc định, lớp hiển thị và kiểm tra ánh xạ 3D → xem trước | Tên, hệ hợp lệ, vị trí, chức năng, nguồn và ID khớp hình học đã duyệt |
| Trắc nghiệm | T03 tạo bản nháp theo hệ → thêm, sửa hoặc xóa từng câu → nhập A, B, C, D → chọn một đáp án đúng, nhập giải thích → xem thử từ cùng bản nháp | Ít nhất một câu, bốn lựa chọn có nội dung khác nhau, đúng một đáp án và có giải thích |
| Học liệu SVG | T05 chọn mẫu và hệ → thêm nhiều chú thích theo cơ quan → kéo điểm hoặc sửa x/y → xóa từng mục sau xác nhận → xem trước desktop/mobile từ cùng danh sách | Điểm nằm trong vùng vẽ, có nhãn tiếng Việt, cơ quan tương ứng và điều khiển bằng bàn phím |
| Thẻ ghi nhớ | T08 chọn hệ → soạn mặt gợi nhớ và mặt đáp án → sắp thứ tự, xem trước hai mặt | Có mặt gợi nhớ, đáp án và mô tả văn bản phù hợp nếu dùng hình |

Mỗi form có «Lưu bản nháp» và «Xem trước». «Gửi duyệt» kiểm tra dữ liệu và đưa phiên bản vừa gửi sang «Đang chờ». Bản nháp chưa xuất bản có thể lưu trữ. Muốn sửa mục đã xuất bản thì tạo bản nháp mới. Rời trang khi chưa lưu có «Ở lại» hoặc «Rời trang». Dữ liệu vừa nhập được giữ nếu gửi lỗi.

## F10 · Duyệt, xuất bản và lưu trữ học liệu

**Giảng viên · T02/T03/T05/T06/T08 → Quản trị viên A05 → Thông báo X07.** A05 lọc mục đang chờ theo loại, hệ hoặc tác giả. Quản trị viên xem nội dung, nguồn, hiển thị SVG/3D nếu có và xem trước như sinh viên. «Duyệt và xuất bản» xác nhận khi các liên kết còn hợp lệ. «Từ chối» yêu cầu lý do cho người soạn. Sau quyết định, giảng viên mở thông báo và có thể sửa bản bị từ chối rồi gửi duyệt lại.

Giảng viên có thể «Hủy gửi duyệt» khi yêu cầu còn đang chờ. Bản nháp được giữ để sửa. Nếu trạng thái đã thay đổi ở nơi khác, tải lại hàng đợi và giữ ngữ cảnh. Quản trị viên lưu trữ nội dung đã xuất bản khi không còn phụ thuộc đang hoạt động. Kết quả học đã lưu vẫn hiển thị theo phiên bản tại thời điểm làm. Liên kết đến nội dung không còn được công bố dùng X09.

T01 hiện số học liệu chờ duyệt. Sau khi duyệt một học liệu SVG, sinh viên thấy mục đó trong danh sách học liệu của hệ tại S02.

## F11 · Quản lý tài khoản và phân quyền

**Quản trị viên · A01 → A02.** Tìm/lọc tài khoản theo tên, email mẫu, vai trò và trạng thái. «Thêm tài khoản» mở biểu mẫu cho vai trò Sinh viên hoặc Giảng viên. Chỉnh sửa tên, vai trò hoặc trạng thái theo từng bản ghi. Email mẫu là duy nhất. Xác nhận đổi vai trò hoặc «Vô hiệu hóa tài khoản» và nêu hiệu lực với truy cập.

Khi tài khoản giảng viên còn phụ trách lớp đang mở, hướng dẫn xử lý lớp trước khi đổi vai trò hoặc vô hiệu hóa. Tài khoản quản trị mẫu chỉ đọc. Vô hiệu hóa giữ dữ liệu nghiệp vụ và chặn đăng nhập hoặc tiếp tục phiên cũ. «Kích hoạt lại» yêu cầu xác nhận. Báo lỗi tại trường hoặc vùng danh sách và giữ bộ lọc sau khi cập nhật.

## F12 · Cấu hình hệ, thư viện mô hình và nội dung công khai

**Quản trị viên · A01 → A03/A04/A06.** A03 tạo/sửa hệ, tên, mô tả, đề mục và thứ tự. A04 đăng ký tham chiếu tệp GLB/SVG/ảnh, chọn cơ quan hoặc chế độ sử dụng, nhập tác giả, nguồn, giấy phép và mô tả thay thế. Chạy xem trước, kiểm tra tệp và khai báo hoạt ảnh nếu có. A06 chọn các mẫu công khai và thứ tự hiển thị ở P01/P02.

Xác nhận trước khi lưu trữ hệ hoặc tài nguyên đã dùng. Khi còn cơ quan, mô hình mẫu hoặc học liệu xuất bản tham chiếu, hiển thị danh sách phụ thuộc và hướng dẫn đổi liên kết trước. Chỉ cấu hình mẫu từ các cơ quan đã xuất bản và mô hình còn dùng được. «Hủy» bỏ thay đổi đang nhập theo quy tắc dữ liệu chưa lưu. Công khai đọc cấu hình đã lưu gần nhất.

## F13 · Xử lý đề xuất chủ đề

**Quản trị viên · A01 → A05. Khách · P03.** Mở nhóm «Đề xuất chủ đề», lọc đang chờ và đọc tên, loại, lý do. «Chấp nhận đề xuất» ghi nhận phạm vi cần bổ sung. «Từ chối đề xuất» yêu cầu lý do hiển thị cho người gửi. Quản trị viên đọc kết quả trong hàng đợi. Khách xem kết quả ở P03 bằng mã tra cứu. Nếu một quản trị viên khác đã xử lý, tải lại trạng thái trước khi thao tác tiếp.

**Đề xuất từ Sơ đồ SVG · S02 → X07 → T01/T06 hoặc A05.** Giảng viên nhận đề xuất được phân công qua Thông báo và mở danh sách «Đề xuất học liệu» tại T01. Xem người gửi, cơ quan, hệ và nội dung. Tiếp nhận, nhập phản hồi và mở T06 để soạn nếu phù hợp. Quản trị viên xử lý đề xuất thiếu người phụ trách tại A05. Sinh viên xem phản hồi qua X07. Chấp nhận đề xuất cập nhật trạng thái xử lý. Nút «Xem mô hình 3D» xuất hiện ở chi tiết SVG sau khi mô hình được duyệt theo F10 và đã được xuất bản.

## AI-1 đến AI-3 · Nhánh tùy chọn (§12)

| Nhánh | Điểm mở | Đầu vào và đầu ra | Thao tác thủ công luôn có |
| --- | --- | --- | --- |
| AI-1 · Nhận diện cơ quan | S02 | Chọn vùng hoặc ảnh mẫu → gợi ý cơ quan, cấu trúc liên quan và căn cứ hiển thị → xác nhận hoặc chọn lại. | Danh sách cơ quan và bộ lọc |
| AI-2 · Gợi ý ôn lại | S01/S06 | Chọn phạm vi tiến độ → gợi ý hệ cần ôn, ghi dữ liệu dùng để suy luận → xác nhận, chỉnh hoặc bỏ qua. | Xem tiến độ và chọn hệ |
| AI-3 · Giải thích cấu trúc | S03 | Chọn cấu trúc → xem giải thích và nguồn kiểm chứng nếu có → dùng hoặc bỏ qua. | Thẻ mô tả giải phẫu đã xuất bản |

Nếu thực hiện, mỗi nhánh có kiểm tra đầu vào, «Đang phân tích…», «Chưa đủ dữ liệu», kết quả có giải thích, chưa chắc chắn và lỗi. Cung cấp «Thử lại», «Dùng cách thủ công» và đường báo cáo phản hồi sai. Cho phép chấp nhận, sửa hoặc từ chối trước khi lưu gợi ý phù hợp. Bản gợi ý giữ nhãn và nằm ngoài nội dung đã duyệt cho tới khi được kiểm chứng.
