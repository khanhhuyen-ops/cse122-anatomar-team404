# Dữ liệu và trạng thái nghiệp vụ mô phỏng

Thiết kế theo [yêu cầu dữ liệu §§10, 13](../../AnatomAR-project-requirements.md). `db.json` ở gốc là nguồn đọc ban đầu, với ID và thời điểm tạo/cập nhật. Chuẩn bị 5–8 bản ghi mẫu cho mỗi thực thể tối thiểu ở giai đoạn triển khai. Có thể đọc tệp qua một module dữ liệu và lưu thay đổi bản demo trong trình duyệt. JSON Server hoặc MockAPI có thể thay cho adapter nếu nhóm chọn. Dùng dữ liệu giả lập. Kiểm tra vai trò mô phỏng hành vi giao diện. Phiên, địa chỉ email và mật khẩu dùng cho demo trong môi trường học tập.

## Thực thể tối thiểu

| Tập dữ liệu | Trường nghiệp vụ | Người xem hoặc sửa |
| --- | --- | --- |
| `users` | `id`, tên, email mẫu, vai trò, trạng thái hoạt động/vô hiệu hóa, tùy chọn hiển thị | Chủ tài khoản xem và sửa tên/tùy chọn. Quản trị viên tạo và quản lý tài khoản mẫu. |
| `bodySystems` | ID, tên và thứ tự của 11 hệ theo OpenStax. Nội dung học có tóm tắt, đề mục, SVG minh họa và trạng thái riêng. | Khách xem danh mục công khai. Sinh viên xem học liệu đã xuất bản. Quản trị viên quản lý nội dung học. |
| `organs` | Hệ, tên và tên gọi khác, vị trí, chức năng, cấu trúc, tọa độ SVG, tài sản và nguồn | Khách xem mẫu trong cấu hình. Sinh viên xem bản đã xuất bản. Giảng viên soạn bản mình phụ trách; quản trị viên duyệt. |
| `organModels` | Mã cơ quan, loại tệp GLB/SVG/ảnh, đường dẫn, nguồn, giấy phép, văn bản thay thế và metadata xem | Cấu hình và lưu trữ qua A04. T06 chọn hoặc đề nghị liên kết tài nguyên. P02/S03 đọc tài nguyên của nội dung đang hiển thị. |
| `quizQuestions` | Hệ, bộ câu hỏi, thứ tự, nội dung, lựa chọn, đáp án đúng và giải thích | Giảng viên soạn. Sinh viên nhận nội dung bài và lựa chọn, xem đáp án sau khi nộp. |
| `quizAttempts` | Sinh viên, hệ, mã bài, bản câu hỏi cố định, đáp án đã chọn, trạng thái và kết quả | Sinh viên tạo, cập nhật khi nháp, nộp và xem lượt của mình. Giảng viên xem qua báo cáo lớp. |
| `flashcards` | Hệ, cơ quan liên quan nếu có, nhóm, thứ tự, gợi nhớ, đáp án, metadata hình và trạng thái | Giảng viên soạn. Sinh viên đọc thẻ đã xuất bản. |
| `memorizedMarkers` | Mã sinh viên, mã cơ quan, thời điểm đánh dấu và trạng thái hoạt động nếu lưu lịch sử | Sinh viên xem, đánh dấu và bỏ dấu của mình. Giảng viên đọc số liệu qua báo cáo lớp mình. |

Thực thể giải phẫu dùng ID duy nhất, ổn định qua 3D, SVG, danh sách và chi tiết. `systemId` chỉ hệ chính. `systemIds` và `memberships` giữ liên kết qua nhiều hệ, với vai trò `primary`, `functional` hoặc `context`. `parentId` thể hiện quan hệ bộ phận. `anatomicalRelationships` giữ các quan hệ nối, dẫn lưu, phân nhánh hoặc đi qua. Tọa độ `x` và `y` chuẩn hóa theo `viewBox` thuộc sơ đồ SVG. Mỗi phiên bản mô hình khai báo `visualLayerId`, ánh xạ hình học đã xác minh tới ID thực thể, góc mặc định và clip nếu có. Nhiều mesh có thể trỏ cùng ID. [Đối chiếu các nguồn giải phẫu](../../../../docs/anatomy-audit.md).

## Dữ liệu bổ trợ đề xuất

| Tập dữ liệu | Công dụng |
| --- | --- |
| `classes` | Tên lớp, mã tham gia duy nhất `joinCode`, giảng viên phụ trách, danh sách ID sinh viên, trạng thái mở/lưu trữ. |
| `quizzes` | Nhóm các câu hỏi theo hệ, phiên bản, tiêu đề và quy trình xuất bản. |
| `flashcardReviews` | Lượt ôn theo sinh viên/hệ, vị trí đang xem, đánh giá từng thẻ và thời điểm hoàn thành. |
| `visualLessons` | Sơ đồ/học liệu SVG theo hệ, mẫu SVG, danh sách chú thích, liên kết mô hình và phiên bản. |
| `moderationRequests` | Loại nội dung, người gửi, bản cần duyệt, quyết định, lý do và thời điểm xử lý. |
| `topicSuggestions` | Loại chủ đề, tên, lý do, trạng thái và phản hồi. Đề xuất công khai có mã tra cứu. Đề xuất từ S02 Sơ đồ SVG tham chiếu sinh viên, cơ quan, hệ và người nhận theo phạm vi phụ trách hoặc hàng đợi quản trị viên. |
| `notifications` | Người nhận, hành động, bản ghi đích và thời điểm đọc. |
| `publicSettings` | Hệ ưu tiên, thứ tự và danh sách mẫu công khai đang dùng. |

## Trường dùng trong prototype

| Màn hình | Trường và kiểm tra khi triển khai |
| --- | --- |
| S02, T05 | `bodySystems.id`, `organs.id/systemId`, `visualLessons.annotations[]` gồm `id, organId, labelVi, x, y`. Tọa độ neo chuẩn hóa từ 0 đến 1 trong `viewBox`, quy đổi cùng hình. SVG kiểm tra mô hình đã xuất bản và đề xuất đang chờ theo `organId`. Atlas đọc tên, hệ, vị trí và chức năng. |
| T03, S04, S06 | `quizQuestions` có `quizId, order, promptVi, options, correctOptionId, explanationVi`. `options` gồm bốn ID ổn định A–D và văn bản. Kết quả dùng bộ câu cố định trong `quizAttempts`. |
| P03, S02, T01, A05 | `topicSuggestions` lưu `source, topicType, name, bodySystemId, organId, note, status, reply`. Khách có `lookupCode`. Sinh viên có `requesterId` và `assigneeId` khi phân công được. Quyền tra cứu giới hạn theo mã hoặc phiên của người gửi. |
| S01, T07, T04 | `classes` lưu `id, name, joinCode, teacherId, studentIds, status`. T07 tạo mã tự động, hiển thị mã cho giảng viên phụ trách. S01 nhập mã và đọc danh sách lớp của phiên sinh viên. T04 dùng cùng `studentIds` khi lọc báo cáo. |
| A02, X05 | `users` lưu `displayName, email, role, status`. X05 chỉnh `displayName`. A02 chỉnh quyền và trạng thái theo phạm vi quản trị. |
| A04, T06 | `organModels` lưu `organId, fileType, path, author, sourceUrl, license, altText, status` cùng metadata 3D nếu có. Tài nguyên thiếu nguồn hoặc giấy phép ở bản nháp. |
| A05, X07 | `moderationRequests` lưu `entityType, entityId, versionId, submittedBy, status, reviewReason`. `notifications` lưu mã yêu cầu và vai trò đích. Sinh viên chỉ nhận bản xem được khi phiên bản đã xuất bản. |

Mã demo `AR-7DH3` trỏ đề xuất Hệ nội tiết. Nguyễn Hà thuộc Giải phẫu A1 và có đề xuất Phổi trái. Tim dùng `organ.heart`, Phổi trái dùng `organ.lung-left`. Bộ «Tim và hệ mạch» dùng câu về buồng tim nối động mạch chủ với đáp án D, Tâm thất trái. `db.json` hiện có danh mục và liên kết giải phẫu. Tài khoản, học liệu xuất bản và bản ghi nghiệp vụ của các ví dụ trên dùng dữ liệu riêng khi triển khai.

## Chuyển trạng thái và kiểm tra

| Đối tượng | Chuyển trạng thái và điều kiện |
| --- | --- |
| Tài khoản | Hoạt động ↔ Vô hiệu hóa. Tài khoản quản trị mẫu chỉ đọc. Trước khi khóa hoặc đổi vai trò giảng viên cần xử lý các lớp đang mở do họ phụ trách. Phiên của tài khoản vừa vô hiệu hóa mất hiệu lực khi kiểm tra lại. |
| Lớp | Mở → Lưu trữ. `joinCode` là duy nhất trong kho dữ liệu, kể cả mã lớp đã lưu trữ. Khi tạo lớp, cấp mã và lưu bản ghi trong cùng thao tác. Chỉ lớp mở nhận thêm thành viên. Lớp lưu trữ và báo cáo giữ ở chế độ chỉ đọc. |
| Học liệu | Bản nháp → Đang chờ → Đã xuất bản hoặc Bị từ chối. Sửa bản bị từ chối rồi gửi bản mới. Hủy gửi khi đang chờ trả phiên bản về nháp, yêu cầu duyệt ghi «Đã hủy». Phiên bản xuất bản trước tiếp tục xuất hiện đến khi bản mới được duyệt. |
| Danh mục và tài nguyên | Nháp → Đang sử dụng/Đã xuất bản → Đã lưu trữ. Chặn lưu trữ khi còn nội dung xuất bản hoặc mẫu công khai đang tham chiếu. Giữ tham chiếu lịch sử phục vụ kết quả đã lưu. |
| Đề xuất | Đang chờ → Đã chấp nhận hoặc Bị từ chối. Chỉ nhận một quyết định cho mỗi phiên bản. Tra cứu bằng mã trả nội dung và phản hồi dành cho khách. |
| Trắc nghiệm | Đang làm → Đã nộp. Chỉ một bản nháp đang mở cho mỗi sinh viên và bài. Sau nộp, giữ bộ câu hỏi và kết quả của lượt. «Làm lại» tạo lượt riêng. |
| Ôn thẻ | Đang ôn → Hoàn thành khi đã đánh giá mọi thẻ trong lượt. Mỗi đánh giá là «Đã thuộc» hoặc «Cần ôn lại». Lượt «Ôn lại thẻ cần ôn» dùng tập thẻ chưa thuộc của lượt vừa xong. |
| Dấu ghi nhớ | Không có dấu ↔ Đã thuộc, duy nhất nhận diện theo cặp sinh viên–cơ quan. Dấu của cơ quan đã lưu trữ vẫn giữ trong lịch sử và tạm rời mẫu số hiện hành. |

Thống kê mức ghi nhớ theo hệ lấy số cơ quan đang xuất bản đã đánh dấu chia cho tổng số cơ quan đang xuất bản trong hệ. Tổng bằng 0 hiển thị «Chưa có học liệu». Với tổng dương, 0 là «Chưa học», từ 1 đến dưới tổng là «Đang học», bằng tổng là «Hoàn thành». Thống kê ôn thẻ và điểm trắc nghiệm hiển thị riêng. Điểm lấy số câu đúng chia số câu của lượt, bỏ trống tính sai. Hiển thị số đúng/tổng và phần trăm làm tròn một lần khi trình bày, dùng timestamp ISO ở dữ liệu và định dạng `vi-VN` khi hiển thị.

## Giao diện dữ liệu và phản hồi

Các tên HTTP mô tả hành vi adapter. Bản demo tĩnh có thể cung cấp các thao tác tương đương qua một module JavaScript nhỏ.

| Thao tác | Đọc / ghi khái niệm | Kết quả để dựng giao diện |
| --- | --- | --- |
| Tải hệ và mô hình | `GET /bodySystems`, `GET /organs`, `GET /organModels` | Danh sách có thể rỗng, bản ghi chỉ đọc theo quyền, URL mô hình và nguồn. |
| Gửi / tra cứu chủ đề | `POST /topicSuggestions`, tra cứu theo mã qua adapter hoặc theo phiên sinh viên | Khách nhận mã tra cứu. Sinh viên thấy người nhận, trạng thái và phản hồi của đề xuất của mình. Lỗi giữ bản nháp. Yêu cầu lặp của cùng sinh viên và cơ quan đang chờ dùng lại trạng thái đã có. |
| Đánh dấu / bỏ dấu | Đặt trạng thái theo cặp mã sinh viên và cơ quan | Trạng thái hiện tại và thời điểm. Gửi lại cùng thao tác giữ cùng kết quả. |
| Ôn, lưu và nộp quiz | Tạo lượt, cập nhật bản nháp, gửi xác nhận của lượt | Trạng thái và dữ liệu đã lưu. Đáp án đúng và giải thích của quiz xuất hiện ở kết quả sau nộp. |
| Soạn nội dung và duyệt | Đọc hoặc sửa bản nháp, gửi `moderationRequests`, quyết định theo phiên bản | Trạng thái mới, lý do nếu bị từ chối, thông báo cho người soạn. |
| Quản lý tài khoản / lớp / tài nguyên | Đọc danh sách, tạo/sửa theo vai trò, đổi trạng thái | Bản ghi sau thay đổi, hoặc lý do và danh sách tham chiếu đang chặn. |
| Tham gia lớp bằng mã | Dùng ID sinh viên từ phiên đang hoạt động. Bỏ khoảng trắng hai đầu, chuẩn hóa chữ hoa, tìm đúng mã lớp mở rồi thêm ID vào `studentIds`. | Trả tên lớp và trạng thái tham gia. Lặp lại trả trạng thái đã tham gia và giữ một bản ghi thành viên. Mã sai hoặc lớp lưu trữ giữ nguyên thành viên. Việc kiểm tra trạng thái lớp và ghi thành viên được thực hiện trong cùng thao tác. |

Quy ước lỗi gồm 401 (hết phiên), 403 (thiếu quyền), 404 (không có bản ghi hoặc ngoài phạm vi), 409 (trùng hoặc dữ liệu vừa đổi), 422 (trường không hợp lệ), lỗi mạng (thử lại). Nếu đang nộp, hiển thị đúng một kết quả cho cùng mã thao tác. Khi tải thất bại, giữ dữ liệu đang xem nếu có và thông báo dữ liệu chưa cập nhật. Dữ liệu demo cần mẫu cho cả bốn vai trò, rỗng, lỗi, vô hiệu hóa, chờ, từ chối, hoàn thành và đã hủy/lưu trữ.
