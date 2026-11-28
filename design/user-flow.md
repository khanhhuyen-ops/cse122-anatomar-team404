# Luồng người dùng AnatomAR

Các mã màn hình trỏ đến [bảng kiểm kê](screen-list.md). Phạm vi chức năng theo [yêu cầu dự án §§06–13, 22](../.agents/skills/AnatomAR-project-requirements.md). Các quy tắc bên dưới dùng chung cho Desktop, Mobile và dịch vụ mock. [Hợp đồng dữ liệu](../.agents/skills/anatomar-design/references/mock-data.md).

## Sitemap

| Phạm vi | Điểm vào và trang trực thuộc |
| --- | --- |
| Công khai | X01 → P01 hệ cơ quan, P02 mô hình mẫu, P03 gửi hoặc tra cứu đề xuất. X02 đăng nhập → X03 đăng ký hoặc X04 đặt lại mật khẩu. |
| Sinh viên | S01 → Lớp của tôi → nhập mã lớp. S01 → S02 học theo hệ. Atlas 3D mở thông tin nhanh tại chỗ. SVG hoặc danh sách → S03 chi tiết cơ quan hoặc hộp thoại đề xuất → X07. S01/S02/S03 → S04 → S06 hoặc S05, giữ hệ và cơ quan khi có. |
| Giảng viên | T01 → T02 cơ quan và mô hình → T06 biên tập. T01 → T03 câu hỏi, T05 sơ đồ SVG, T08 thẻ hoặc T07 quản lý lớp. T07 → tạo lớp → sao chép mã, xem thành viên hoặc mở T04. Hộp thoại Đề xuất học liệu mở từ T01 hoặc X07. |
| Quản trị viên | A01 → A02 tài khoản, A03 hệ cơ quan, A04 thư viện, A05 hàng đợi, A06 cấu hình công khai. A05 dùng ngăn chi tiết cho học liệu và đề xuất. |
| Sau đăng nhập | Menu của phiên → X05 hồ sơ, X06 cài đặt, X07 thông báo, xác nhận đăng xuất → X01. Logo về X01, «Khu vực của tôi» về dashboard theo vai trò. X08 xử lý thiếu quyền hoặc hết phiên. X09 xử lý bản ghi thiếu, đã ẩn hoặc nằm ngoài phạm vi bản ghi của vai trò hiện tại. |

Các bước đặt lại mật khẩu, kết quả tra cứu, CRUD ngắn, xem trước, chỉnh chú thích và xác nhận nằm trong trang mở chúng. Desktop và Mobile dùng cùng mã màn hình và cùng đích nghiệp vụ. Mobile đưa các đích vào menu chạm và mở ngăn chi tiết gần toàn màn hình.

## F01 · Khám phá khóa học và học liệu mẫu

**Khách · X01 → P01 → P02.** Từ trang chủ chọn «Khám phá các hệ cơ quan». Xem tổng quan, lọc theo tên hoặc hệ rồi chọn mô hình công khai, ví dụ tim hoặc xương. P02 hiển thị tên, phần học mẫu, nguồn và điều khiển mô hình. Từ đây có thể mở mô hình mẫu khác, trở lại danh sách hoặc đăng ký bằng X03 để học sâu hơn.

Nếu lọc không có kết quả, «Xóa bộ lọc» khôi phục danh sách công khai. Nếu mẫu đang lưu trữ hoặc đã bị gỡ, trở về P01 qua X09. Nút quay về giữ bộ lọc còn hợp lệ.

Tại X01, khách có thể khám phá mô hình 3D toàn thân ngay trên trang chủ. Mỗi lớp giải phẫu có điều khiển riêng để quan sát một lớp hoặc chồng nhiều lớp.

Người học kéo để xoay quanh cơ thể và dùng điều khiển thu phóng. Trên desktop, rê trên bề mặt cơ quan để làm nổi và xem thông tin nhanh. Trên mobile, chạm cơ quan để mở thông tin ngay trong vùng xem, kéo một ngón để xoay và chụm hai ngón để thu phóng. P01 luôn liệt kê 11 hệ. P02 chỉ mở các mẫu đã xuất bản và được đưa vào cấu hình công khai A06. Nếu ảnh hoặc mô hình tải lỗi, P02 vẫn mở phần văn bản của mẫu.

## F02 · Định vị cơ quan và khám phá mô hình

**Khách · P02. Sinh viên · S02.** P02 mở mô hình mẫu. S02 có hai chế độ cùng điều hướng.

- **Atlas 3D.** Xoay, thu phóng, đặt lại góc nhìn và bật/tắt lớp. Rê vào bề mặt cơ quan đang thấy để phủ xanh ngọc bán trong suốt và mở tooltip theo vị trí cơ quan, gồm tên, hệ, vị trí và chức năng. Rời vùng hợp lệ ẩn cả hai. Trên Mobile, chạm cơ quan để mở, chạm lại hoặc bấm đóng để ẩn. Chọn trong bảng «Thông tin nhanh» là đường thay thế để đọc nội dung.
- **Sơ đồ SVG.** Chọn hệ. Bấm hoặc chạm hotspot neo vào `viewBox` của sơ đồ, hoặc chọn cơ quan tương ứng trong danh sách. Cả hai mở cùng ID, vị trí, chức năng và tình trạng học liệu. Desktop dùng hover để báo vùng tương tác. Chạm chọn trực tiếp trên Mobile. Chuyển hệ đưa về sơ đồ mặc định của hệ mới.
- **Có bài học cơ quan đã xuất bản.** Mở S03 bằng «Xem học liệu». Có thể giữ nhãn «Xem mô hình 3D» khi bài có GLB được phép dùng. Khi thiếu hoặc lỗi GLB, vẫn mở S03, đọc cấu tạo và ghi nhớ. Ảnh, SVG và hoạt ảnh có trạng thái riêng. Quay lại S02 giữ hệ, cơ quan và chế độ SVG.
- **Chưa có bài học cơ quan đã xuất bản.** Vẫn xem thông tin định vị của cơ quan. «Gửi đề xuất học liệu» mở form hiện có với `systemId`, `organId` và người nhận. Nếu đã có yêu cầu đang chờ hoặc đã tiếp nhận, hiện trạng thái và lối mở X07. [F03](#f03--gửi-và-tra-cứu-đề-xuất-chủ-đề).

S02 mở Sơ đồ SVG khi truy cập từ liên kết hệ, học liệu hoặc kết quả học. Người dùng có thể chọn Atlas từ tab hiện có. `view=atlas` mở Atlas khi đích yêu cầu rõ chế độ này. Atlas giữ camera, zoom và lớp trong phiên. Khi SVG thiếu hoặc tải lỗi, danh sách vẫn dùng cùng `organId` để mở chi tiết. Phân biệt «Đang kiểm tra học liệu…», lỗi tra cứu và kết quả «Chưa có học liệu».

Ở P02/S03, người dùng chọn một cấu trúc từ danh sách hoặc hình học đã ánh xạ. Sau xoay, dịch, zoom, reset hoặc thay lớp, hover tính theo hình đang thấy. Khi phát hoạt ảnh, hover được kiểm tra theo pose hiện tại ngay cả khi con trỏ đứng yên. Khi lớp chứa ID đang chọn bị ẩn, thẻ chi tiết giữ ID và cho «Hiện lớp». Khi WebGL hoặc GLB lỗi, danh sách và chi tiết bằng văn bản giữ bộ phận đang học. [Điều khiển và trạng thái 3D](../.agents/skills/anatomar-design/references/viewer-3d.md).

## F03 · Gửi và tra cứu đề xuất chủ đề

**Khách · P01 → P03.** Chọn «Đề xuất chủ đề». Chọn loại «Hệ cơ quan» hoặc «Cơ quan», nhập tên chủ đề và lý do. Đề xuất cấp hệ nhằm bổ sung học liệu cho một trong 11 hệ. Kiểm tra các trường rồi «Gửi đề xuất». Thành công hiển thị mã tra cứu và trạng thái «Đang chờ». Khách dùng mã ở phần «Tra cứu đề xuất» để đọc trạng thái và phản hồi dành cho chính đề xuất đó.

**Sinh viên · S02 Sơ đồ SVG hoặc danh sách → X07.** Từ cơ quan chưa có bài học, mở biểu mẫu, xem người nhận, nhập nội dung và xác nhận gửi. Dịch vụ xác định người nhận theo giảng viên phụ trách hệ đang chọn trong A03. Nếu chưa có hoặc tài khoản phụ trách đã mất quyền, đề xuất vào A05. Thành công hiện «Đã gửi đề xuất», «Đang chờ phản hồi» và liên kết Thông báo. Quay lại S02 giữ lựa chọn.

Khi ghi lỗi, giữ nội dung để thử lại cùng thao tác. Với cùng sinh viên và `organId`, dùng lại yêu cầu đang chờ hoặc đã tiếp nhận. Khách tra cứu bằng mã riêng của đề xuất. Nhập sai mã có hướng dẫn kiểm tra lại. Kết quả nhận, từ chối hoặc hoàn tất theo [F13](#f13--xử-lý-và-hoàn-tất-đề-xuất-chủ-đề).

## F04 · Tài khoản, phiên và thông tin cá nhân

**Người dùng · X01/X02/X03/X04 → S01/T01/A01 → X05/X06/X07.**

1. **Đăng nhập.** Nhập email và mật khẩu mẫu. Ưu tiên đích nội bộ trong bảng kiểm kê nếu vai trò và bản ghi hiện còn cho phép mở, rồi dùng dashboard của phiên làm đích mặc định. Xác thực lại mọi tham số. Với thông tin sai, báo tại form. Tài khoản bị vô hiệu hóa được hướng dẫn liên hệ quản trị viên.
2. **Đăng ký.** Nhập tên, email, mật khẩu và xác nhận. Email trùng có lối về X02. Tạo tài khoản sinh viên thành công chuyển về X02 với email mẫu đã điền.
3. **Quên mật khẩu.** X04 thực hiện yêu cầu → nhập mã demo → đặt mật khẩu mẫu mới. Dùng cơ chế mô phỏng hiển thị và giải thích mã ngay trong demo. Mã đã dùng hoặc hết hạn có lối «Tạo mã mới». Đổi xong quay về X02.
4. **Sau đăng nhập.** X05 sửa tên hiển thị, email và vai trò ở chế độ chỉ đọc. X06 lưu lựa chọn giảm chuyển động. X07 xem thông báo, đánh dấu đã đọc và mở bản ghi còn được phép. X05–X07 giữ điều hướng của vai trò đang dùng. «Đăng xuất» mở xác nhận, xóa phiên mô phỏng và về X01.
5. **Truy cập.** X08 xử lý hết phiên với «Đăng nhập lại», hoặc sai vai trò với «Về khu vực của tôi». Khi vào được khu vực nhưng bản ghi thiếu, đã ẩn hoặc ngoài phạm vi, dùng X09. Lỗi kết nối hiển thị ở vùng nội dung và giữ đường thử lại. X01 và P01–P03 dùng được trong mọi phiên. Khu vực Sinh viên, Giảng viên và Quản trị viên kiểm tra đúng vai trò trước khi đọc bản ghi.

## F05 · Học theo hệ và cập nhật mức ghi nhớ

**Sinh viên · S01 → S02 Sơ đồ SVG → S03 → S01.** Mở hệ cần học, chọn cơ quan và mở bài học đã xuất bản. Tại S03, dùng danh sách cấu trúc hoặc phương tiện đang có, rồi chọn «Đánh dấu đã thuộc» hoặc «Bỏ đánh dấu». Dấu dùng cặp `studentId`–`organId` và khả dụng ngay cả khi thiếu tài nguyên hình ảnh, 3D hoặc hoạt ảnh. Các lối sang S04/S05 mang `systemId` và tùy chọn `organId` để lọc bài ôn liên quan.

S01 và T04 dùng cùng phép tính theo tập `organId` có bài học cơ quan đang xuất bản trong hệ. Một cơ quan thuộc nhiều hệ dùng cùng dấu và có thể xuất hiện trong từng hệ liên quan. Tổng 0 hiện «Chưa có học liệu». Tổng dương chạy qua «Chưa học», «Đang học», «Hoàn thành». Khi ghi lỗi, giữ dấu đã xác nhận gần nhất. Thẻ và quiz có kết quả riêng. [Cách tính tiến độ](../.agents/skills/anatomar-design/references/mock-data.md#tiến-độ-và-lịch-sử-học).

## F06 · Ôn thẻ ghi nhớ

**Sinh viên · S01/S02/S03 → S05.** Chọn nhóm thẻ đã xuất bản theo hệ. Khi đến từ cơ quan, ưu tiên nhóm có thẻ liên quan, vẫn cho xem nhóm khác cùng hệ. Một lượt giữ `groupId` và `versionId` lúc bắt đầu. Mỗi bước có gợi nhớ bằng văn bản hoặc hình, «Hiện đáp án», đánh giá «Đã thuộc» hoặc «Cần ôn lại», chỉ báo tiến trình và lối thoát.

Kết thúc lượt hiển thị số thẻ đã đánh giá và hành động «Ôn lại thẻ cần ôn». Có thể tiếp tục một lượt dở từ S01 hoặc S05. Nếu không có thẻ được xuất bản, S05 dẫn về hệ khác. Đánh giá thẻ thuộc kết quả ôn thẻ. Dấu ghi nhớ cơ quan dùng thao tác riêng tại S03. Giảng viên dùng T08 để soạn và gửi duyệt thẻ theo F09/F10.

## F07 · Làm và xem kết quả trắc nghiệm ghi nhớ

**Sinh viên · S01/S02/S03 → S04 → S06.** Chọn bộ quiz đã xuất bản theo hệ, với cơ quan là bộ lọc tùy chọn. «Bắt đầu làm bài» ghim `quizId` và `versionId`, giữ cố định thứ tự, nội dung và thang điểm của bộ câu. Mỗi câu có một đáp án đúng. Có thể quay lại, đổi đáp án và tiếp tục lượt dở. S06 mở bằng `attemptId` và kiểm tra chủ lượt. Thời gian làm do sinh viên tự điều chỉnh.

«Kiểm tra và nộp» mở tóm tắt câu đã trả lời, câu bỏ trống và liên kết đi tới từng câu. Hộp thoại xác nhận ghi rõ câu bỏ trống tính 0 điểm và kết quả sẽ được lưu. Chỉ chuyển sang S06 khi đã ghi nhận lượt làm. Lỗi giữ bản nháp và cho nộp lại cùng lượt.

S06 hiển thị số đúng/tổng, tỷ lệ, đáp án đã chọn, đáp án đúng và giải thích, kể cả câu sai hoặc bỏ trống. «Làm lại» tạo lượt mới. «Xem lại hệ cơ quan» quay về S02 ở đúng hệ. Khi chưa từng làm, S01 hiển thị «Chưa có lượt làm» tại phần điểm.

## F08 · Tạo lớp, tham gia bằng mã và đọc tiến độ

**Giảng viên · T01 → T07.** Chọn «Tạo lớp», nhập tên và lưu. Khi tạo thành công, lớp ở trạng thái «Đang mở» và hệ thống cấp một mã duy nhất. Hộp thoại hiển thị tên lớp, mã dạng chỉ đọc và nút «Sao chép mã» để giảng viên tự chia sẻ. Giảng viên có thể mở lại mã của lớp đang mở từ danh sách lớp mình phụ trách. Đổi tên lớp giữ cùng mã. Lớp đã lưu trữ giữ danh sách và báo cáo ở chế độ chỉ đọc và dừng nhận thành viên qua mã. Giảng viên vẫn có thể thêm tài khoản sinh viên từ danh sách hoặc gỡ thành viên theo quyền hiện có.

**Sinh viên · S01 → Lớp của tôi.** Từ bảng điều khiển, chọn «Tham gia lớp», nhập hoặc dán mã giảng viên cung cấp, rồi xác nhận. Lớp đang mở với mã hợp lệ được thêm ngay vào danh sách và tên lớp xuất hiện trong xác nhận. Cùng thao tác cập nhật danh sách thành viên mà giảng viên xem tại T07 và dùng tại T04. Nếu đã là thành viên, hiện «Bạn đã tham gia lớp này» và giữ một mục trong danh sách. Mã trống, không hợp lệ hoặc lớp đã lưu trữ có thông báo tại form. Khi kết nối lỗi, giữ mã đã nhập để thử lại. Chỉ tài khoản Sinh viên đang hoạt động dùng luồng này.

Sinh viên có thể thuộc nhiều lớp. Trước khi xác nhận tham gia, S01 cho biết giảng viên lớp có thể xem tóm tắt học tập hiện tại của sinh viên. Kho học liệu đã xuất bản dùng chung cho mọi sinh viên đang hoạt động. T07 có thể gỡ thành viên khỏi lớp đang mở. Sau khi gỡ, lớp đó mất quyền xem báo cáo và dữ liệu học cá nhân vẫn tồn tại.

T04 kiểm tra `classId`, giảng viên sở hữu lớp và `studentId` còn trong danh sách lớp. Giảng viên xem theo một hệ hoặc «Tất cả hệ», với tỷ lệ cơ quan đã thuộc, ôn thẻ và quiz gần nhất. Phân biệt «Chưa có dữ liệu» với «0 câu đúng». Lớp lưu trữ chỉ đọc danh sách và bản tóm tắt chốt lúc lưu trữ, ghi rõ thời điểm. Trước khi khóa tài khoản giảng viên, xử lý lớp đang mở theo F11.

## F09 · Soạn cơ quan, trắc nghiệm, sơ đồ và thẻ

**Giảng viên · T01 → T02/T03/T05/T08.**

| Loại | Trình tự | Kiểm tra trước khi gửi duyệt |
| --- | --- | --- |
| Cơ quan và mô hình | T02 lọc bài của mình → T06 chọn `organId` hoặc tạo hồ sơ giải phẫu nháp → soạn bài và chọn tài nguyên A04 khi có → xem trước. T05 quản lý vị trí điểm trên mỗi sơ đồ | Vị trí, chức năng, cấu tạo và nguồn. Bổ sung cơ quan mới cần đối chiếu định danh, hệ và trùng lặp. Ánh xạ 3D chỉ bắt buộc cho các điểm chọn 3D được khai báo |
| Trắc nghiệm | T03 tạo bộ theo một hệ → thêm, sửa, xóa và sắp thứ tự câu → xem thử bản nháp → gửi duyệt cả bộ | Ít nhất một câu, bốn lựa chọn khác nhau, một đáp án đúng và giải thích. `organId` tùy chọn và phải liên quan hệ của bộ |
| Học liệu SVG | T05 chọn hệ và SVG từ A04 → thêm, kéo hoặc sửa tọa độ và xóa chú thích → xem trước cùng bản nháp ở hai kích thước. Mỗi hệ có tối đa một sơ đồ mặc định đang xuất bản trong MVP | Có SVG dùng được và điểm chọn hợp lệ, cùng tên và văn bản thay thế. Hotspot có thể trỏ tới cơ quan đã xác định trong danh mục đang chờ bài học riêng |
| Thẻ ghi nhớ | T08 tạo nhóm theo một hệ → soạn hai mặt, sắp thứ tự, xem trước → gửi duyệt cả nhóm | Ít nhất một thẻ có gợi nhớ và đáp án. Hình đi kèm mô tả. `organId` tùy chọn và phải liên quan hệ của nhóm |

Mỗi học liệu có một giảng viên sở hữu và tối đa một bản đang soạn hoặc chờ duyệt. T02/T03/T05/T08 cho giảng viên sửa nội dung họ sở hữu. Với bài cơ quan đang do giảng viên khác sở hữu, báo rằng bài đã có người phụ trách và hướng xử lý ở A05. Trường «giảng viên phụ trách hệ» dùng định tuyến đề xuất. Quản trị viên có thể bàn giao chủ sở hữu cho một giảng viên đang hoạt động tại A05. «Lưu bản nháp», «Xem trước» và «Gửi duyệt» dùng cùng dữ liệu phiên bản. Bản đang chờ duyệt khóa sửa. Khi lưu hoặc gửi lỗi, giữ nội dung đang nhập.

## F10 · Duyệt, xuất bản và lưu trữ học liệu

**Giảng viên · T02/T03/T05/T06/T08 → Quản trị viên A05 → Thông báo X07.** A05 xét đúng phiên bản gửi. Chỉ Quản trị viên duyệt và xuất bản hoặc từ chối kèm lý do. Kiểm tra nội dung, nguồn và tài nguyên được khai báo. Bài cơ quan đủ nội dung văn bản có thể xuất bản với tài nguyên tùy chọn còn trống. SVG cần tệp SVG hợp lệ. Trắc nghiệm duyệt theo bộ và thẻ duyệt theo nhóm. Kết quả duyệt đi vào X07 của chủ sở hữu.

Chủ sở hữu có thể hủy gửi khi còn chờ, chỉnh bản nháp hoặc tạo bản sửa từ phiên bản bị từ chối rồi gửi lại. Bản xuất bản hiện hành tiếp tục phục vụ trong lúc bản sửa đang chờ. Khi duyệt bản mới, dịch vụ đổi phiên bản hiện hành trong cùng thao tác. Nếu trạng thái vừa đổi, tải lại bản ghi và giữ ngữ cảnh.

Chủ sở hữu có thể lưu trữ nội dung chưa từng công bố sau khi rút yêu cầu đang chờ. Học liệu đang công bố do Quản trị viên lưu trữ sau khi xử lý các liên kết đang dùng. Kết quả và lượt học đã bắt đầu giữ phiên bản đã ghim. Liên kết mở học liệu hiện hành đã lưu trữ dùng X09. Duyệt một phiên bản khớp với đề xuất đã liên kết kích hoạt F13.

## F11 · Quản lý tài khoản và phân quyền

**Quản trị viên · A01 → A02.** Tìm/lọc tài khoản theo tên, email mẫu, vai trò và trạng thái. «Thêm tài khoản» mở biểu mẫu cho vai trò Sinh viên hoặc Giảng viên. Chỉnh sửa tên, vai trò hoặc trạng thái theo từng bản ghi. Email mẫu là duy nhất. Xác nhận đổi vai trò hoặc «Vô hiệu hóa tài khoản» và nêu hiệu lực với truy cập.

Giảng viên cần xử lý lớp đang mở tại T07 trước khi A02 đổi vai trò hoặc vô hiệu hóa. Khi đổi Sinh viên sang vai trò khác, A02 báo trước và cùng thao tác kết thúc tư cách thành viên trong các lớp đang mở. Vô hiệu hóa Sinh viên giữ tư cách thành viên và dữ liệu đã lưu, chặn phiên và hoạt động mới. Khi giảng viên mất quyền, đề xuất còn mở về A05. Học liệu đã công bố giữ hiệu lực. Quản trị viên có thể bàn giao tài liệu tại A05 khi cần chỉnh sửa. Tài khoản quản trị mẫu chỉ đọc. «Kích hoạt lại» yêu cầu xác nhận. Báo lỗi tại trường hoặc vùng danh sách và giữ bộ lọc sau cập nhật.

## F12 · Cấu hình hệ, thư viện mô hình và nội dung công khai

**Quản trị viên · A01 → A03/A04/A06.** A03 cấu hình mô tả, đề mục, thứ tự và giảng viên phụ trách tùy chọn cho 11 hệ chuẩn, có lối mở A04. ID, tên chuẩn và số lượng hệ được giữ cố định. Có thể hủy bản đang sửa hoặc lưu trữ đề mục. A04 đăng ký ảnh, SVG, GLB, clip hoặc hoạt ảnh cùng tác giả, nguồn, giấy phép, mô tả thay thế và điều kiện dùng công khai. A06 chọn các bài cơ quan đã xuất bản và thứ tự mẫu P01/P02. 11 tên hệ vẫn có trong P01.

Giảng viên gắn tài nguyên đã sẵn sàng từ A04 vào bản nháp của mình. A04 có thể lưu tài nguyên nháp, kiểm tra và chuyển sang sẵn sàng. Khi học liệu hiện hành hoặc mẫu công khai còn sử dụng tài nguyên, chỉ lưu trữ sau khi các liên kết đó được đổi hoặc gỡ. Mỗi tệp thay thế có ID mới để giữ phiên bản cũ. Khi cấu hình mẫu công khai, kiểm tra quyền xem riêng cho từng tài nguyên sẽ hiển thị. Mẫu có văn bản vẫn đọc được khi phương tiện thiếu hoặc lỗi tải.

## F13 · Xử lý và hoàn tất đề xuất chủ đề

1. **Đang chờ.** Đề xuất của Khách vào A05. Đề xuất từ S02 vào T01 của giảng viên được giao hoặc A05 nếu chưa có người phụ trách. Quản trị viên xem toàn bộ và có thể chuyển người xử lý. Sau chuyển, chỉ người được giao hiện tại và Quản trị viên còn quyền xử lý. T01 và A05 dùng cùng bản ghi.

2. **Đã tiếp nhận hoặc Bị từ chối.** Người xử lý xác nhận cơ quan hoặc hệ theo danh mục. Với đề xuất tên tự do của Khách, có thể bổ sung hồ sơ cơ quan nháp trong T06 khi cần rồi liên kết đúng ID. «Tiếp nhận» ghi nhận công việc còn phải hoàn thành. «Từ chối» ghi lý do cho người gửi. Sinh viên nhận X07, Khách xem kết quả qua mã P03.
3. **Liên kết học liệu đáp ứng.** Người xử lý nối đề xuất đã tiếp nhận với một bài cơ quan đúng `organId`, hoặc một sơ đồ SVG đúng `systemId` đối với đề xuất cấp hệ. Giảng viên mở T06/T05 để soạn, Quản trị viên có thể giao giảng viên phụ trách. Từ chối bản duyệt giữ đề xuất ở «Đã tiếp nhận» để tiếp tục sửa bài.
4. **Đã hoàn tất.** F10 cập nhật đề xuất đã liên kết khi phiên bản đáp ứng được xuất bản. Nếu liên kết tới học liệu đang công bố, A05 kiểm tra đúng đích và xác nhận hoàn tất. Lưu ID học liệu, ID phiên bản, thời điểm hoàn tất và gửi một thông báo cho sinh viên. X07 mở S03 hoặc S02 đúng ngữ cảnh. P03 cập nhật trạng thái tra cứu, chỉ hiện liên kết mẫu khi A06 đã cho xem công khai. Nếu sau đó học liệu được lưu trữ, giữ lịch sử và hiển thị trạng thái hiện không xem được.

## AI-1 đến AI-3 · Sau MVP (§12)

Nhận diện cơ quan, gợi ý ôn tập và giải thích cấu trúc là ý tưởng mở rộng. MVP dùng hotspot/danh sách, kết quả ôn và mô tả đã duyệt. Điều kiện cho trải nghiệm AI nếu làm sau nằm trong [đề bài §12](../.agents/skills/AnatomAR-project-requirements.md#12tùy-chọn-nâng-cao-ý-tưởng-ai--không-bắt-buộc).
