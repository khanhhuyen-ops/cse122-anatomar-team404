# Dữ liệu và trạng thái nghiệp vụ mô phỏng

Hợp đồng triển khai MVP theo [đề bài §§10, 13](../../AnatomAR-project-requirements.md) và [luồng F01–F13](../../../../design/user-flow.md). Dữ liệu giải phẫu hiện có trong [db.json](../../../../db.json). Các bảng dưới đây đặc tả phần dữ liệu nghiệp vụ cần thêm khi triển khai.

## Một dịch vụ mock

- Mọi trang dự kiến dùng chung `js/api.js`. Dịch vụ đọc `db.json` lúc khởi tạo kho demo, lưu thay đổi nghiệp vụ vào một kho `localStorage` có phiên bản schema và giữ phiên hiện tại trong `sessionStorage`. Các trang gọi cùng thao tác qua JavaScript bất đồng bộ. Dữ liệu demo đồng bộ qua điều hướng và đổi vai trò trong cùng trình duyệt. Phạm vi nghiệm thu mock là một tab thao tác tại một thời điểm.
- Mỗi thao tác xác thực lại phiên, vai trò và phạm vi bản ghi. Lấy ID người thực hiện từ phiên. Bản ghi trả về chỉ chứa trường cần cho vai trò và màn hình. Tài khoản, mật khẩu và mã dùng cho demo đều giả lập. Kiểm tra quyền của mock mô tả hành vi frontend. Dịch vụ thật sẽ cần kiểm soát quyền ở máy chủ.
- Mỗi lần ghi kiểm tra dữ liệu trên bản mới nhất rồi lưu một thay đổi thống nhất. Khi nghiệp vụ tạo nhiều kết quả, như xuất bản và hoàn tất đề xuất, các kết quả được ghi cùng lần. Thử lại cùng thao tác dùng lại `operationId`. Phiên bản hoặc trạng thái vừa đổi trả lỗi xung đột. Tải lại trước khi quyết định tiếp.
- Kết quả thao tác trả dữ liệu hoặc mã lỗi, thông báo và lỗi theo trường khi có. `401` hết phiên, `403` sai vai trò ở khu vực riêng, `404` thiếu/đã ẩn/ngoài phạm vi bản ghi, `409` trùng hoặc xung đột, `422` đầu vào sai. Lỗi kết nối giữ đầu vào, cho thử lại và giữ dữ liệu đã xác nhận gần nhất nếu có. X08/X09 theo [F04](../../../../design/user-flow.md#f04--tài-khoản-phiên-và-thông-tin-cá-nhân).

## Các tập dữ liệu và quyền

Mọi bản ghi nghiệp vụ có `id`, `createdAt` và `updatedAt`. Dùng ISO cho thời gian và `vi-VN` khi hiển thị. Chuẩn bị 5–8 bản ghi mẫu có ý nghĩa theo đề bài cho các thực thể nghiệp vụ ở giai đoạn triển khai. `bodySystems` giữ đầy đủ 11 mục. `organs` tiếp tục dùng danh mục đã kiểm kê.

| Tập dữ liệu | Trường và quy tắc chính |
| --- | --- |
| `users` | `displayName, email, role, status`, tùy chọn giảm chuyển động. Chủ phiên sửa tên/tùy chọn. A02 tạo/sửa sinh viên, giảng viên và trạng thái. Tài khoản quản trị mẫu chỉ đọc. |
| `bodySystems` | 11 `id` và tên chuẩn cố định. A03 sửa cấu hình hiển thị, `teacherId` phụ trách đề xuất tùy chọn, đề mục, thứ tự và lưu trữ từng đề mục. |
| `organs` | ID giải phẫu, tên, `systemId, systemIds, memberships, parentId`, nguồn TA2 khi có. T06 có thể đề xuất hồ sơ mới trong bản nháp. A05 đối chiếu, hợp nhất với ID hiện có nếu trùng hoặc đưa ID mới vào danh mục khi duyệt. |
| `organModels` | Thư viện A04 của ảnh, SVG, GLB và hoạt ảnh. `kind, path` hoặc tham chiếu clip nội bộ, `author, sourceUrl, license, altText, publicUseAllowed, status`, ID giải phẫu/ánh xạ và mô tả clip khi có. Quản trị viên đăng ký, kiểm tra và lưu trữ. Giảng viên chọn tài nguyên sẵn sàng. |
| `quizQuestions` | `quizId, versionId, order, promptVi, options, correctOptionId, explanationVi` và `organId` tùy chọn. A–D có ID ổn định trong câu. Đọc đáp án và giải thích ở S06 sau nộp. |
| `quizAttempts` | `studentId, quizId, versionId, answers, status, submittedAt, result`. Một lượt đang làm cho mỗi sinh viên và bộ. Chỉ chủ lượt vào S06. T04 đọc tóm tắt theo quyền lớp. |
| `flashcards` | `groupId, versionId, order, front, back`, `organId` và ảnh tùy chọn. Có ít nhất gợi nhớ và đáp án. Hình mang mô tả phù hợp. |
| `memorizedMarkers` | Một bản ghi cho mỗi cặp `studentId, organId`, với `active, markedAt`. Chỉ sinh viên của phiên đặt hoặc bỏ dấu. Báo cáo dùng chung phép tính bên dưới. |
| `classes` | `name, teacherId, joinCode, studentIds, status`. Giảng viên tạo lớp của mình. Mã duy nhất trong kho, kể cả lớp lưu trữ. Đổi tên giữ mã. Sinh viên có thể thuộc nhiều lớp. |
| `organLessons`, `visualLessons`, `quizzes`, `flashcardGroups` | Mỗi bản ghi có `ownerId, publishedVersionId, archivedAt`. Mỗi `organId` có tối đa một bài cơ quan chưa lưu trữ. Các loại khác gắn một `systemId`. Mỗi hệ có tối đa một sơ đồ đang công bố và có thể có nhiều bộ quiz/nhóm thẻ. |
| `contentVersions` | `contentType, contentId, versionNumber, state` và dữ liệu bản soạn. Mỗi học liệu có tối đa một bản đang soạn hoặc gửi duyệt. Bản bài cơ quan chứa vị trí, chức năng, cấu tạo, nguồn và các tham chiếu tài nguyên tùy chọn. Bản SVG chứa `svgAssetId` và `annotations`. Câu hỏi và thẻ gắn `versionId` trong tập dữ liệu tương ứng. |
| `flashcardReviews` | `studentId, groupId, versionId`, tập thẻ, vị trí, đánh giá và trạng thái. Ưu tiên tiếp tục lượt dở của nhóm. Ôn lại giữ đúng tập «Cần ôn lại» của lượt vừa xong. |
| `moderationRequests` | `contentType, contentId, versionId, submittedBy, status, reviewedBy, decidedAt, reviewReason`. A05 duyệt đúng phiên bản. Chủ sở hữu gửi, rút khi đang chờ và xem quyết định. |
| `topicSuggestions` | `source, topicType, requestedName, note, systemId`, `organId` nếu đã định danh. Sinh viên gửi kèm hai ID từ S02. Đề xuất khách có tên tự do thì gắn ID phù hợp lúc tiếp nhận. Khách có `lookupCode`, sinh viên có `requesterId`. Lưu `assigneeId, status, responseVi`, tham chiếu `targetContentId` lúc liên kết và `fulfilledVersionId, fulfilledAt` lúc hoàn tất. |
| `notifications` | `recipientId, event, entityId, readAt` và tham chiếu bản ghi đích. X07 lọc theo người nhận. Mỗi quyết định hoặc lần hoàn tất gửi một thông báo cho mỗi người nhận. |
| `publicSettings` | Danh sách bài cơ quan mẫu đã xuất bản và thứ tự. A06 chọn mẫu. P01 và P02 cùng đọc cấu hình. P01 vẫn dùng đủ 11 hệ. |

## ID, học liệu và tài nguyên

- `systemId` trong URL là hệ đang học. `organs.systemId` là hệ chính trong danh mục. S02 và tiến độ dùng các liên hệ `primary` và `functional` trong `memberships` để xác định cơ quan của hệ. `context` dùng để tham chiếu giải phẫu. Một `organId` có thể thuộc nhiều hệ. `parentId` thể hiện cấu trúc con, còn `visualLayerId` điều khiển lớp Atlas.
- Atlas ánh xạ node/mesh đã đối chiếu đến ID giải phẫu. S02 lấy cùng `organId` khi bấm hotspot hoặc chọn từ danh sách. `contentVersions.annotations[]` của SVG có `id, organId, labelVi, x, y`. `x, y` chuẩn hóa từ 0 đến 1 trong vùng vẽ của SVG. Hotspot có thể xuất hiện trước khi có bài cơ quan. S03 dùng `organId` đã chọn và `structureId` tùy chọn cho bộ phận.
- Dịch vụ trả tình trạng bài học theo phiên bản đang công bố, riêng với tình trạng từng loại phương tiện. Tài nguyên có vòng đời «Nháp → Sẵn sàng → Lưu trữ». Trình xem phân biệt chưa gắn tài nguyên, đang tải, dùng được và lỗi tải. Ảnh, SVG minh họa của bài cơ quan, GLB và hoạt ảnh là tham chiếu tùy chọn. Tài nguyên gắn vào bản xuất bản phải đáp ứng loại, quyền và nguồn. Bài cơ quan có nội dung văn bản dùng được vẫn mở được khi thiếu phương tiện.
- Bài SVG của hệ cần SVG nguồn và hotspot hợp lệ để xuất bản. Khi chưa có sơ đồ của hệ hoặc SVG tải lỗi, S02 cho chọn cơ quan từ danh sách. Khi thiếu GLB hoặc WebGL lỗi, S03 vẫn đọc nội dung và đặt dấu. Hoạt ảnh phụ thuộc clip/tệp tương thích với mô hình được chọn. Khi thiếu hoạt ảnh, mô hình tĩnh vẫn dùng được. A04 chặn lưu trữ tài nguyên còn tham chiếu từ bản hiện hành hoặc mẫu công khai. Thay tệp dùng bản ghi mới. Bản lịch sử giữ ID cũ.
- T03 quản lý bộ và câu hỏi. T08 quản lý nhóm và thẻ. Gửi duyệt ở cấp bộ/nhóm. `organId` có thể gắn trên từng câu hoặc thẻ để lọc khi bước vào S04/S05 từ S02/S03. Khi mở bộ/nhóm, học trọn nội dung và thứ tự của phiên bản đã chọn.

## Quyền và chuyển trạng thái

| Nghiệp vụ | Quy tắc ghi và phản hồi |
| --- | --- |
| Đổi vai trò và vô hiệu hóa | Xử lý lớp mở của giảng viên trước khi đổi vai trò hoặc vô hiệu hóa. Đổi vai trò của sinh viên xóa ID khỏi danh sách thành viên đang mở trong cùng thao tác và giữ lịch sử học. Vô hiệu hóa sinh viên giữ danh sách lớp và lịch sử. Kiểm tra lại tài khoản ở mọi thao tác của phiên. |
| Tham gia và báo cáo lớp | Sinh viên đang hoạt động nhập mã, dịch vụ bỏ khoảng trắng đầu/cuối và chuẩn hóa chữ hoa. Kiểm tra lớp mở, rồi ghi `studentId` đúng một lần. T07 thêm thủ công dùng cùng quy tắc thành viên. Chỉ chủ lớp sửa, gỡ hoặc lưu trữ. T04 kiểm tra chủ lớp và thành viên hiện tại của lớp mở. Lưu trữ giữ danh sách và tóm tắt tại thời điểm lưu trữ. Gỡ khỏi lớp mở chấm dứt quyền xem qua lớp đó. Dữ liệu cá nhân và quyền truy cập học liệu đã xuất bản vẫn dùng được theo phiên sinh viên. |
| Quyền sở hữu | Chủ học liệu là giảng viên có `ownerId` trên bản ghi. Quản trị viên gán lại chủ ở A05. Giảng viên phụ trách hệ tại A03 nhận đề xuất theo hệ. Khi mất quyền xử lý, đề xuất đang chờ/đã tiếp nhận về A05. Giảng viên chỉ xem và xử lý đề xuất hiện được giao, cùng báo cáo lớp mình. |
| Duyệt và xuất bản | Nháp → Chờ duyệt → Xuất bản hoặc Từ chối. Từ chối cần lý do. Chỉ chủ sở hữu rút yêu cầu đang chờ, trả bản về nháp và giữ yêu cầu đã hủy. Chỉ Quản trị viên xuất bản và lưu trữ bản hiện hành. Cập nhật `publishedVersionId` khi duyệt bản mới. Công chúng và sinh viên tiếp tục thấy bản hiện hành trước đó trong lúc bản sửa chờ duyệt, theo quyền xem. |
| Đề xuất | Đang chờ → Đã tiếp nhận → Đã hoàn tất, hoặc Đang chờ → Bị từ chối. Tra cứu P03 bằng mã, tra cứu của sinh viên bằng phiên. Khi xuất bản học liệu đã liên kết và đúng phạm vi, ghi hoàn tất và một thông báo X07 cho sinh viên. Học liệu hiện hành đã đáp ứng có thể được A05 xác nhận. Khách theo dõi kết quả qua mã. Đề xuất đã tiếp nhận giữ trạng thái khi bản học liệu bị từ chối. Lặp gửi cùng sinh viên/cơ quan trả yêu cầu đang mở. |
| Quiz và thẻ | Xác minh bộ/nhóm đang xuất bản khi bắt đầu. Ghim phiên bản đã chọn. Lượt đã mở có thể tiếp tục bằng phiên bản đó kể cả khi bộ/nhóm đã được thay thế hoặc lưu trữ. Dùng `attemptId` hoặc ID lượt ôn để cập nhật. Nộp lại cùng lượt trả kết quả đã ghi. «Làm lại» tạo lượt mới từ phiên bản đang công bố nếu còn. |
| Dấu ghi nhớ | Đặt trạng thái theo `organId` bằng phiên Sinh viên. Yêu cầu lặp trả cùng trạng thái. Bản bài học lưu trữ giữ dấu lịch sử, rời tập tiến độ hiện hành. |

## Tiến độ và lịch sử học

S01 và T04 dùng cùng phép tính. Với mỗi hệ, mẫu số là tập `organId` duy nhất có bài cơ quan đang xuất bản và quan hệ `primary` hoặc `functional` với hệ. Tử số là các ID trong tập đã có dấu hoạt động của sinh viên. Tổng nhiều hệ hợp nhất các ID trước khi đếm. Tổng 0 hiện «Chưa có học liệu». Tổng dương phân biệt «Chưa học», «Đang học» và «Hoàn thành». Ảnh, SVG, GLB, hoạt ảnh, thẻ và quiz có trạng thái riêng. T04 ở lớp lưu trữ dùng tóm tắt đã chốt.

Điểm quiz lấy số đúng trên tổng số câu của phiên bản đã ghim. Câu bỏ trống tính 0. S06 trình bày số đúng, tổng, tỷ lệ, đáp án và giải thích. Đánh giá thẻ thuộc lượt ôn, lưu riêng với dấu ghi nhớ cơ quan. Bảng tiến độ hiển thị kết quả quiz và thẻ bên cạnh tiến độ cơ quan, kể cả khi chưa có lượt học.

## Nhóm thao tác dùng chung

- Phiên và tài khoản. Đăng nhập, đăng ký, đặt lại mật khẩu mẫu, đọc phiên, đổi vai trò/trạng thái, đăng xuất.
- Danh mục và học liệu. Đọc hệ, chi tiết cơ quan, sơ đồ, mẫu công khai, bộ quiz, nhóm thẻ, trạng thái bài và tài nguyên. Cùng cơ chế tra theo ID cho Atlas, SVG, chi tiết và lối học tiếp.
- Lớp và học tập. Tạo lớp, tham gia, thêm/gỡ thành viên, lưu trữ, đọc tiến độ, đặt dấu, bắt đầu/tiếp tục/nộp quiz và đánh giá thẻ.
- Soạn, duyệt và đề xuất. Lưu nháp, xem trước, gửi/rút, duyệt/từ chối, lưu trữ, bàn giao chủ. Gửi, tra cứu, giao, tiếp nhận/từ chối, liên kết và hoàn tất đề xuất. Đọc và đánh dấu thông báo.

Mẫu Figma dùng `organ.heart`, `organ.lung-left`, đề xuất công khai `AR-7DH3` và lớp `GP-C1-7K4Q`. Demo cần có cả bài đã xuất bản chưa gắn GLB và cơ quan có hotspot chưa có bài học để kiểm tra hai nhánh của S02.
