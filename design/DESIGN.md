# Đặc tả thiết kế AnatomAR

AnatomAR hỗ trợ dạy và học giải phẫu cơ thể người trong học phần CSE122. Sinh viên đi từ sơ đồ cơ thể đến cơ quan, quan sát cấu trúc và chuyển động, rồi tự kiểm tra bằng thẻ ghi nhớ hoặc trắc nghiệm. Giảng viên xây dựng học liệu trực quan và theo dõi mức ghi nhớ. Quản trị viên duy trì tài khoản, danh mục và cấu hình.

## Phạm vi

[Tài liệu yêu cầu dự án](../.agents/skills/AnatomAR-project-requirements.md) là căn cứ về chức năng, tên tệp, phạm vi vai trò và minh chứng. Brief thiết kế bổ sung yêu cầu hoạt ảnh cơ quan 3D, giao diện tiếng Việt và ưu tiên HTML, CSS, JavaScript thuần, SVG, Three.js, API JSON mô phỏng.

- **Cốt lõi** gồm 32 màn hình hiện có, trong đó có 16 tệp nền tảng, 9 trang dùng chung và 7 trang bổ sung để hoàn tất luồng. Giữ bốn vai trò, mã, tên tệp và bố cục Desktop/Mobile. Dùng hộp thoại, tab hoặc ngăn chi tiết trong các trang hiện có cho các trạng thái bổ sung. [Bảng kiểm kê](screen-list.md).
- **Nghiệp vụ MVP** gồm danh mục 11 hệ, Atlas, SVG tương tác, bài học cơ quan, thẻ theo nhóm, quiz theo bộ, tiến độ cá nhân, lớp tham gia bằng mã, biên tập và duyệt học liệu, tài nguyên, cấu hình mẫu và đề xuất đến khi hoàn tất. Dùng chung dịch vụ mock, form có kiểm tra và trạng thái tải/rỗng/thành công/lỗi. [Luồng người dùng](user-flow.md).
- **Ngoài MVP** gồm ba ý tưởng AI ở §12, chế độ tối toàn trang, PWA, cá nhân hóa và tích hợp dịch vụ thật. Vùng 3D giữ nền tối như bản hiện tại.

## Định hướng hình ảnh

**Medical Education × Interactive Anatomy Atlas.** Trang chủ mở bằng mô hình 3D toàn thân có bảng bật tắt từng lớp giải phẫu. Nền xanh đậm của vùng xem tách biên mô hình. Trên nền sáng, bố cục đọc từ hệ cơ quan đến cấu trúc, vị trí, chức năng và nguồn. Dashboard dùng cùng hệ chữ và màu nhấn. Bảng, danh sách và thứ tự nội dung giúp mỗi vai trò nhận ra việc cần làm.

Các ảnh tham chiếu gợi cách dùng thẻ nền sáng, màu nhạt theo chủ đề, tiến độ có số đếm và vùng xem tối. Atlas 3D phủ xanh ngọc bán trong suốt lên bề mặt cơ quan đang được rê hoặc chạm. Tooltip chứa tên, hệ, vị trí và chức năng, neo theo hình học đang thấy. Cách tổ chức theo hệ cơ quan và đường vào mô hình mẫu lấy cảm hứng từ danh mục giải phẫu tiếng Việt. Nội dung, bố cục, bộ nhận diện và hình minh họa được thiết kế riêng cho AnatomAR. [Danh mục Giaiphau3D](https://app.giaiphau3d.com/home).

Literata dành cho tiêu đề mở đầu và tên hệ hoặc cơ quan. Be Vietnam Pro dành cho nội dung, điều khiển và dashboard. Xanh ngọc đậm dùng cho hành động chính. Màu mô và đường chỉ dẫn thuộc minh họa. Tên cấu trúc bằng tiếng Việt xuất hiện trước. Tên Latin chỉ hiển thị khi đã có nguồn. Nhãn và số thứ tự dùng cho chú thích, trình tự hoặc dữ liệu. [Token và hệ chữ](../.agents/skills/anatomar-design/references/design-system.md).

UI/UX Pro Max gợi ý tương phản cao, sắc xanh y khoa, vùng chạm rộng và giảm chuyển động. Frontend Design định hướng dùng bản minh họa giải phẫu làm nội dung chính của trang đầu và đưa «Khám phá các hệ cơ quan» thành hành động nổi bật. Dùng Web Design Guidelines để rà quy tắc về focus, nhập liệu, trạng thái và URL ở mức đặc tả. [UI/UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill/blob/f2f7266b07805025421611656045e9b44b41e2eb/.claude/skills/ui-ux-pro-max/SKILL.md) · [Frontend Design](https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md) · [Web Design Guidelines](https://github.com/vercel-labs/agent-skills/blob/main/skills/web-design-guidelines/SKILL.md).

## Vai trò và điều hướng

| Vai trò hiển thị | Điểm bắt đầu | Nghiệp vụ | Phạm vi |
| --- | --- | --- | --- |
| Khách (Visitor) | X01 · Trang chủ công khai | Xem tổng quan các hệ, khám phá mô hình mẫu, gửi đề xuất chủ đề và xem trạng thái. | Hệ công khai, mô hình mẫu đã xuất bản, đề xuất của mình qua mã tra cứu. |
| Sinh viên (Student) | S01 · Bảng điều khiển | Tham gia lớp bằng mã được cung cấp, học theo hệ, khám phá mô hình, đánh dấu đã thuộc, ôn thẻ, làm trắc nghiệm và xem tiến độ. | Lớp mình tham gia, học liệu đã xuất bản và dữ liệu học của mình. |
| Giảng viên (Teacher) | T01 · Bảng điều khiển | Tạo lớp, chia sẻ mã, xem tiến độ, soạn và gửi duyệt bài cơ quan, SVG, bộ quiz, nhóm thẻ. Xử lý đề xuất được giao. | Học liệu mình sở hữu, mã và thành viên lớp mình quản lý, tiến độ theo quyền lớp và đề xuất mình đang xử lý. |
| Quản trị viên (Admin) | A01 · Bảng điều khiển | Quản lý tài khoản, cấu hình 11 hệ và đề mục, tài nguyên và mẫu công khai. Giao người xử lý đề xuất, duyệt và xuất bản học liệu. | Tài khoản, tài nguyên, danh mục, cấu hình và hàng đợi. Báo cáo cá nhân lớp thuộc khu vực Giảng viên. |

Tài khoản tự đăng ký nhận vai trò Sinh viên. Quản trị viên cấp vai trò và trạng thái tài khoản theo phạm vi đề xuất trong luồng F11. Các tài khoản Quản trị viên dùng để trình diễn có sẵn trong dữ liệu mẫu. Sau khi đăng nhập, «Khu vực của tôi» luôn về dashboard của phiên hiện tại. Những tài liệu riêng của lớp và tài khoản được lọc theo quyền của bản ghi. [Hợp đồng dữ liệu mô phỏng](../.agents/skills/anatomar-design/references/mock-data.md).

T07 cấp mã duy nhất khi tạo lớp. Sinh viên có thể tham gia nhiều lớp từ «Lớp của tôi» ở S01. T07 và T04 đọc cùng danh sách thành viên. Gỡ khỏi lớp chấm dứt quyền xem qua lớp đó. Lớp lưu trữ giữ bản tóm tắt tại thời điểm lưu trữ. Học liệu đã xuất bản dùng chung cho sinh viên đã đăng nhập, kể cả khi chưa vào lớp. [Luồng F08](user-flow.md#f08--tạo-lớp-tham-gia-bằng-mã-và-đọc-tiến-độ).

Bản Figma dùng mã mẫu `GP-C1-7K4Q` của lớp «Giải phẫu C1». Chạm trường mã để điền mẫu trong prototype. Các trạng thái mã sai, lớp đã lưu trữ và lỗi kết nối có frame riêng. Nút sao chép minh họa xác nhận; tạo mã duy nhất và ghi thành viên thuộc hợp đồng dữ liệu khi triển khai. [Trạng thái F08 Desktop](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=167-11953) · [Trạng thái F08 Mobile](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=167-12575).

## Cách truyền đạt kiến thức (§11)

| Cách | Màn hình | Cách thể hiện |
| --- | --- | --- |
| Sơ đồ cơ thể tương tác SVG | S02 · Học theo hệ, T05 · Dựng học liệu SVG | Sinh viên chọn hệ và hotspot để định vị, đọc thông tin nhanh, mở bài cơ quan đã xuất bản hoặc gửi đề xuất khi thiếu bài. Giảng viên tạo chú thích và gửi duyệt theo hệ. |
| Mô hình 3D toàn thân | X01 · Trang chủ, S02 · Học theo hệ | Xoay, nghiêng góc nhìn, thu phóng, đặt lại, bật nhiều lớp và xem thông tin nhanh của cơ quan đang thấy. |
| Mô hình cơ quan và hoạt ảnh | P02 · Mô hình mẫu, S03 · Mô hình cơ quan | Đổi góc nhìn, xoay, phóng to, chọn một cấu trúc và chủ động phát hoạt ảnh có sẵn. Danh sách và chi tiết bằng văn bản vẫn dùng khi 3D gặp lỗi. |
| Thẻ ghi nhớ | S05 · Thẻ ghi nhớ | Nhớ trước khi hiện đáp án. Tự đánh giá «Đã thuộc» hoặc «Cần ôn lại» từng thẻ và ôn lại nhóm cần củng cố. |
| Trắc nghiệm kèm giải thích | S04 · Trắc nghiệm, S06 · Kết quả | Câu hỏi về vị trí hoặc chức năng. Sau khi nộp, hiển thị đáp án, điểm và giải thích, kể cả các câu trả lời sai. |

## Bố cục và hành vi chung

| Mẫu | Công việc chính | Nội dung luôn có |
| --- | --- | --- |
| Public | Khám phá, xem mẫu, gửi đề xuất | Điều hướng, tiêu đề, nội dung theo nhiệm vụ và lối quay về. |
| Atlas 3D | Quan sát giải phẫu | Vùng xem toàn thân, lớp, camera, highlight bề mặt và tooltip thông tin nhanh. |
| Sơ đồ SVG | Chọn cơ quan và học liệu | Bộ chọn hệ, hotspot hoặc danh sách tương đương. Thẻ chi tiết hiện «Xem học liệu» khi có bài, «Xem mô hình 3D» nếu có GLB, hoặc «Gửi đề xuất học liệu» khi thiếu bài. |
| Chi tiết cơ quan | Nghiên cứu cấu tạo | S03 có văn bản, danh sách cấu trúc, các phương tiện đang dùng được, dấu đã thuộc và lối qua bộ quiz/nhóm thẻ liên quan. |
| Auth | Đăng nhập, đăng ký, đặt lại mật khẩu | Một cột, nhãn trường, lỗi gần trường và hành động tiếp theo. |
| Study | Học bằng thẻ hoặc trắc nghiệm | Một thẻ/câu mỗi lượt, chỉ báo tiến trình, điều khiển đi tiếp và phản hồi. |
| Dashboard | Xem tiến độ và việc cần xử lý | Số liệu có mẫu số hoặc kỳ thống kê, liên kết đến danh sách liên quan. |
| Records / Editor | Xem danh sách hoặc sửa bản ghi | Bộ lọc, trạng thái nghiệp vụ, thao tác theo quyền, xem trước và xác nhận khi cần. |

Các mẫu và wireframe desktop/mobile nằm trong [bố cục](../.agents/skills/anatomar-design/references/layout.md). Cấu tạo và hành vi ở [thành phần](../.agents/skills/anatomar-design/references/components.md), [tương tác](../.agents/skills/anatomar-design/references/interaction.md) và [trình xem 3D](../.agents/skills/anatomar-design/references/viewer-3d.md).

Tái sử dụng thanh điều hướng theo vai trò, cảnh báo tải/rỗng/lỗi, form, hộp thoại và ngăn chi tiết. S02/P02/S03 dùng thẻ thông tin cơ quan và trạng thái tài nguyên chung. T02–T08 và A02–A06 dùng cùng mẫu bảng, form và xác nhận khi phù hợp. T03/T08 dùng nhóm điều khiển lưu nháp, xem trước và gửi duyệt chung. S01/T04 dùng cùng thẻ tóm tắt tiến độ.

## Quy ước triển khai sau

- Dùng tiếng Việt có dấu, câu ngắn và động từ cụ thể. Thống nhất «Hệ cơ quan», «Cơ quan», «Cấu trúc», «Lớp hiển thị», «Lớp học», «Thẻ ghi nhớ», «Trắc nghiệm». Dùng `vi-VN` khi hiển thị thời gian và số.
- Dùng HTML ngữ nghĩa, CSS custom properties và JavaScript dạng module theo nhiệm vụ. SVG và Three.js dùng ID ổn định để nối hình minh họa với dữ liệu học. Giữ điều khiển là phần tử HTML.
- Khi triển khai, mọi trang dùng `js/api.js` đọc dữ liệu gốc từ `db.json`, lưu thay đổi demo trong `localStorage` và giữ phiên bằng `sessionStorage`. Dịch vụ thống nhất xác thực, lọc bản ghi, kiểm tra nghiệp vụ, lỗi và thử lại. [Hợp đồng mock](../.agents/skills/anatomar-design/references/mock-data.md).
- Thiết kế mô hình, chú thích và điều khiển theo [đặc tả trình xem](../.agents/skills/anatomar-design/references/viewer-3d.md). Ghi nguồn và giấy phép riêng của mỗi tài nguyên khi chọn dữ liệu cho sản phẩm.
- Dùng WCAG 2.2 AA làm mục tiêu thiết kế. Kiểm tra bàn phím, trình đọc màn hình, zoom, giảm chuyển động và khả năng đọc chi tiết khi WebGL lỗi. [Đặc tả tiếp cận](../.agents/skills/anatomar-design/references/accessibility.md).

### Phân loại giải phẫu

Danh mục dùng 11 hệ theo OpenStax và mã thuật ngữ FIPAT TA2. Atlas, hotspot SVG và mô hình chi tiết dùng chung `organId`. Mỗi cấu trúc có hệ chính, có thể có thêm liên kết chức năng hoặc ngữ cảnh với hệ khác. «Nội tạng» là công tắc hiển thị của Atlas. Danh mục công khai P01 có đủ 11 hệ. Mẫu SVG hiện có của S02 dùng Tim và Phổi trái. [Kết quả rà soát và đối chiếu tài nguyên](../docs/anatomy-audit.md).

A03 cấu hình trình bày, đề mục và giảng viên phụ trách trên 11 ID và tên chuẩn cố định. S02 truyền ID hệ đang học và ID cơ quan qua S03, S04 và S05. S06 dùng ID lượt làm để mở kết quả theo phiên. Tiến độ S01/T04 dùng một dấu cho mỗi cặp sinh viên–cơ quan. Một bài thuộc nhiều hệ có thể đóng góp cho từng hệ và chỉ đếm một lần ở tổng hợp chung.

### Nội dung và tài nguyên

Một bài cơ quan đã xuất bản mở được ở S03 bằng nội dung có nguồn và cấu tạo đã duyệt. Ảnh, SVG minh họa, GLB và hoạt ảnh có tình trạng và quyền hiển thị riêng. Atlas và hotspot có thể giới thiệu một cơ quan đã định danh đang chờ bài học. Sơ đồ hệ xuất bản cần SVG và chú thích hợp lệ. Danh sách S02 và văn bản S03 vẫn dùng khi tài nguyên thiếu hoặc tải lỗi.

T06, T05, T03 và T08 soạn bài cơ quan, sơ đồ, bộ quiz và nhóm thẻ theo phiên bản do một giảng viên sở hữu. A04 quản lý tài nguyên và giấy phép. A05 duyệt đúng bản gửi và cập nhật phiên bản đang công bố. Tiếp nhận đề xuất lưu công việc cần làm. Học liệu đáp ứng đã xuất bản đưa đề xuất sang «Đã hoàn tất» và cập nhật X07 cho sinh viên hoặc tra cứu P03 cho khách. [F09–F13](user-flow.md#f09--soạn-cơ-quan-trắc-nghiệm-sơ-đồ-và-thẻ).

## Duyệt và bàn giao

Các mục bàn giao Figma bên dưới mô tả bản mẫu đã kiểm tra. Dùng đặc tả nghiệp vụ hiện tại cho trạng thái bổ sung như bài chỉ có văn bản, hoàn tất đề xuất và quyền trên bản ghi. Cập nhật các ví dụ tương ứng trong mockup hiện có trước khi nghiệm thu thiết kế cùng nhóm.

### Các trường hợp nghiệm thu MVP

| Trường hợp | Kết quả cần thấy |
| --- | --- |
| S02 → S03 → S04/S05 → S01 | Hotspot và danh sách mở cùng `organId`. Bài có văn bản vẫn học được khi thiếu GLB. Trở về đúng hệ. Một dấu cập nhật tiến độ ở các hệ liên quan và chỉ tính một lần trong tổng hợp. |
| T07 → S01 → T04 | Mã hợp lệ thêm đúng một thành viên. Mã sai hoặc lớp lưu trữ giữ nguyên danh sách. Giảng viên lớp khác và giảng viên đã gỡ sinh viên không xem được tiến độ qua lớp đó. |
| T03/T08 → A05 → S04/S05 | Gửi duyệt cả bộ/nhóm. Từ chối bản sửa giữ bản công bố trước. Xuất bản bản mới phục vụ lượt mới. Lượt dở và kết quả giữ phiên bản đã mở. |
| S02/P03 → T01/A05 → X07/P03 | Tiếp nhận đề xuất giữ trạng thái đang chờ học liệu. Xuất bản đúng học liệu đã liên kết ghi hoàn tất và tạo một thông báo X07 cho sinh viên. P03 cho khách tra cứu hoàn tất và chỉ hiện lối đến mẫu công khai nếu được cấu hình. |
| A04 → A06 → P02 | Tài nguyên sẵn sàng dùng trong học liệu. Mẫu công khai chỉ hiện phương tiện có quyền phù hợp. Lỗi tải phương tiện giữ phần văn bản. Lưu trữ tài nguyên đang được tham chiếu có cảnh báo phụ thuộc. |

### Việc còn mở trước nghiệm thu

- Chọn SVG, GLB, ảnh và clip sản phẩm có nguồn, kiểm giấy phép, ánh xạ cơ quan và xác minh các node đã đánh dấu. Bản mẫu cần tối thiểu đường học SVG tương tác, một mô hình cơ quan có thể xoay/zoom và các lượt ôn bằng thẻ/quiz. [Kiểm kê giải phẫu](../docs/anatomy-audit.md).
- Chuẩn bị dữ liệu nghiệp vụ, kiểm thử quyền theo phiên, lớp, bài thiếu phương tiện, thay phiên bản và thông báo hoàn tất. Bộ nguyên mẫu Figma hiện minh họa các trạng thái đã dựng trước đợt rà soát tài liệu này.
- Phương án hiện hành chia 32 màn hình cho hai thành viên. Đề gốc §15 mô tả nhóm ba người. Xác nhận phương án nộp bài với giảng viên và giữ lát cắt dọc riêng, PR đã review và video OBS theo từng màn hình đã duyệt. [Phân công nhóm](../docs/team-assignment.md).

Tệp Figma chứa tổng quan và thành phần, thiết kế desktop và thiết kế mobile. Tên frame dùng mã trong bảng kiểm kê. Hình tim được tạo bằng ImageGen cho bản mô phỏng giao diện, chờ đối chiếu giải phẫu trước khi dùng làm học liệu. [Thiết kế trên Figma](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=0-1).

Prototype Atlas ở X01 và S02 dùng ảnh kết xuất với ba góc và hai mức zoom. Bề mặt Tim và Phổi trái được trích theo hình học tại góc nhìn minh họa. S02 có hai tab trên Desktop và Mobile. Atlas 3D xem nhanh bằng hover hoặc tap. Sơ đồ SVG cho chọn hệ và hotspot. Tim dẫn đến mô hình chi tiết. Phổi trái mở form đề xuất hiện có, xác nhận chờ phản hồi và Thông báo. Khi triển khai, SVG là lối học dùng được cả khi WebGL gặp lỗi hoặc thiết bị hạn chế. [Bảng trạng thái Figma](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=70-1020) · [Quy tắc Object Picking](../.agents/skills/anatomar-design/references/viewer-3d.md#object-picking-và-tooltip-động).

<details>
<summary>Nguồn hình minh họa tim</summary>

Ảnh PNG gốc dùng trong bản thiết kế. [Minh họa tim](mockups/Minh-hoa-tim.png).

> Create a single original transparent-background cutout image to place inside an educational Vietnamese anatomy atlas UI design. One adult anatomical human heart, front-oblique view, including visible connected aorta and pulmonary vessels, centered and filling almost the entire canvas, no body, no hands and no props. A sophisticated tactile 3D medical textbook illustration, coral-red and deep burgundy natural tissue with blue-green accents on great vessels, substantial soft studio light and confident clear silhouette, suitable above a very dark navy canvas. Anatomy plausible and editorially simplified for an interface mockup. Entire heart and vessels inside the image with 8% clear space, no floor, no cast shadow, no frame, no text, no labels, no watermarks, no additional anatomy. Transparent PNG background.

</details>

1. Duyệt bảng kiểm kê, trách nhiệm, quy tắc nghiệp vụ và các wireframe. Dựng mockup Figma/Canva desktop, responsive, tải/rỗng/lỗi và tương tác SVG ở bước duyệt hình ảnh theo §19.
2. Mỗi thành viên thực hiện ít nhất một luồng từ thiết kế đến dữ liệu, responsive và kiểm thử theo [phân công nhóm hai thành viên](../docs/team-assignment.md). Nối mã màn hình với task Trello, nhánh, commit, PR, review và merge `dev`.
3. Mỗi giao diện thực tế đã duyệt có một video OBS. Trong video, mở đúng mockup và tệp HTML/CSS/JS, giải thích nghiệp vụ, làm một thay đổi nhỏ và chứng minh có thể làm lại. Cập nhật README, bảng kiểm kê và `docs/ai-usage-report.md` theo yêu cầu nhóm. [Yêu cầu minh chứng §§16–23](../.agents/skills/AnatomAR-project-requirements.md).

## Bàn giao cập nhật Figma ngày 27/11/2026

Các cập nhật nằm trong tệp Figma hiện có. Hai trang thiết kế giữ 32 màn hình nền mỗi trang. Các frame có tiền tố «CSE122» chứa trạng thái bổ sung, hộp thoại và bản xem trước dùng chung trong prototype. [Desktop](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=2-96) · [Mobile](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=2-97) · [Design System và sitemap](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=115-15578).

| Màn hình và thành phần | Cập nhật và mục đích |
| --- | --- |
| X01, P01–P03 | Nối lối khám phá, mẫu Tim, đăng ký và đề xuất. P03 có xác nhận gửi, mã mẫu `AR-7DH3`, trạng thái tra cứu và nhánh mã sai. |
| X02–X04, X08, X09 | Thêm liên kết đăng ký, chọn phiên minh họa theo vai trò, mã đặt lại giả lập, mật khẩu mới, mã hết hạn và các lối trở về. |
| X05–X07 | Mỗi vai trò có ngữ cảnh tài khoản của mình, điều hướng về tác vụ, xác nhận đăng xuất và ví dụ thông báo. Vai trò trong hồ sơ ở chế độ chỉ đọc. |
| S01–S03 | Nối mở hệ và học liệu. S02 có chế độ SVG, vùng chọn Tim/Phổi trái, danh sách và chi tiết cùng lựa chọn. Atlas 3D có điểm tương tác đặt trên cơ quan ở các góc minh họa, gắn với công tắc Nội tạng. S03 có trạng thái đã thuộc, bỏ đánh dấu, chi tiết và minh họa nhịp Tim. |
| S04–S06 | Nối vài câu mẫu, bước xác nhận nộp, điểm, làm lại và về hệ. Thẻ có hai mặt, đánh giá và màn kết thúc lượt ôn. |
| T01, T02, T06 | Nối tổng quan với hộp thoại đề xuất Phổi trái, phản hồi và trình biên tập. Quản lý mô hình có mẫu tạo, xem, chỉnh sửa, lưu trữ và cảnh báo tham chiếu. |
| T03 | Bổ sung A–D, trường đáp án đúng, giải thích, mở thêm/sửa/xóa câu và bản xem trước dùng cùng nội dung mẫu. |
| T05, T08 | Bổ sung danh sách chú thích, thêm/sửa tọa độ, xóa và xem mẫu SVG sau cập nhật. Thẻ có xem hai mặt, quản lý và xác nhận lưu trữ. |
| T04, T07 | Nối lớp và tiến độ với form tạo/sửa, quản lý thành viên và xác nhận lưu trữ. |
| A01–A04, A06 | Nối hàng đợi và điều hướng quản trị. Có form tài khoản, phân quyền, vô hiệu hóa, kích hoạt lại, form tên hệ và thứ tự, form tệp, loại, nguồn và giấy phép. Có xác nhận lưu trữ và cảnh báo phụ thuộc. |
| A05 | Có chi tiết SVG, trắc nghiệm, đề xuất của khách hoặc sinh viên. Luồng xác nhận, duyệt, từ chối kèm lý do và xem phản hồi người gửi được mô phỏng bằng các frame trạng thái. |
| Tổng quan và thành phần | Bổ sung bảng trạng thái, ví dụ trường hợp lệ, lỗi và chỉ đọc, mẫu loading/rỗng/lỗi/thành công, mẫu Draft/Pending/Published/Rejected/Archived và biến thể nút. |

### Đối chiếu CSE122

| Điều khoản | Thiết kế hoặc minh chứng |
| --- | --- |
| §§01–05, 07 · Mục tiêu và hành trình | F01–F13 nối khám phá, học/ôn, quản lý, duyệt và phản hồi. |
| §§06, 08, 09 · Vai trò, tên tệp và trạng thái | [Kiểm kê 32 màn hình](screen-list.md) giữ 16 tệp nền tảng, 9 tệp dùng chung và 7 phần bổ sung. Có ví dụ trang, overlay và trạng thái trên cả hai kích thước. |
| §10 · CRUD tám thực thể | T02/T06 và A04 cho `organs`/`organModels`. A03 cho `bodySystems`, A02 cho `users`. T03 cho `quizQuestions`, S04/S06 cho `quizAttempts`, T08/S05 cho `flashcards`, S03 cho `memorizedMarkers`. |
| §11 · Truyền đạt trực quan | S02 SVG tương tác, S03 mô hình và hoạt ảnh, S05 lật thẻ, S04/S06 trắc nghiệm kèm giải thích. |
| §§12–14 · AI tùy chọn, dữ liệu và cách dùng AI | AI tùy chọn được ghi ở cuối tài liệu luồng theo nhóm AI-1–AI-3. Hợp đồng mock mô tả các trường, trạng thái và kiểm tra dữ liệu. Nhật ký AI ghi phần tự kiểm chứng của nhóm. [Hợp đồng mock](../.agents/skills/anatomar-design/references/mock-data.md) · [Nhật ký AI](../docs/ai-usage-report.md). |
| §§15–18 · Nhóm, Git, bảng việc, OBS | Kiểm kê giữ phân công hai thành viên. Cột mã màn hình và tên tệp dùng để gắn task, review, PR và video. Bước triển khai và minh chứng do nhóm thực hiện. [Phân công](../docs/team-assignment.md). |
| §§19–20 · Tài liệu và cấu trúc bàn giao | [Sitemap và user flow](user-flow.md), [kiểm kê](screen-list.md), Figma Desktop/Mobile và bảng component. |
| §§21–25 · Tiêu chí nghiệm thu | Thiết kế có bộ khung theo MVP. Kiểm chứng HTML/CSS/JS, CRUD thật trong adapter mô phỏng, responsive trong trình duyệt, Git và OBS thuộc giai đoạn triển khai. |

### Phần cần kiểm chứng khi triển khai

- Figma minh họa các bản ghi và bước đã dựng. Form nhập tự do, tính điểm cả bộ đề, cập nhật xuyên phiên, kiểm quyền và đồng bộ dữ liệu thực cần adapter mô phỏng. Các nhánh duyệt và từ chối có đích phản hồi riêng. Trạng thái này chưa cập nhật đồng thời toàn bộ màn hình trong bản trình diễn.
- Điểm chọn 3D được đặt theo các ảnh góc nhìn đã dựng. Bản web cần kiểm raycast, che khuất khi bật nhiều lớp, tooltip khi đổi pose, thao tác chạm và giữ camera khi đổi chế độ. Bản Tim minh họa co giãn bằng hai trạng thái. Kiểm clip giải phẫu trên tệp GLB ở bước tích hợp.
- Sơ đồ cơ thể trong prototype minh họa Tim và Phổi trái. Nhóm cần kiểm nội dung giải phẫu, ánh xạ vùng và nguồn tài nguyên trước khi đưa học liệu vào sản phẩm. Metadata trên form tài nguyên là trường mẫu.
- Rà lại chuỗi lỗi mạng, form validation, điều hướng 403/404 theo từng phiên, điểm chạm, bàn phím và đọc màn hình khi triển khai. Bảng trạng thái Figma dùng để khóa mẫu giao diện cần dùng lại.

### Kiểm chứng prototype ở lượt rà soát bốn vai trò

- Kiểm tra cấu trúc 32 màn hình nền trên mỗi trang Desktop/Mobile. Mỗi màn hình có liên kết prototype. Các đích điều hướng được phát hiện trên hai trang đều tồn tại.
- Mở liên kết prototype trong Edge. Trên Mobile, chuyển Atlas 3D → Sơ đồ SVG → chạm vùng Phổi trái → kiểm tra mục được chọn và chi tiết → gửi đề xuất → nhận xác nhận.
- Trên Desktop, rê Tim, Phổi trái rồi vùng trống. Tooltip đổi theo vùng và ẩn khi rời. Bấm Tim cập nhật danh sách và thẻ chi tiết. Mở hàng đợi → từ chối «Tim và hệ mạch» kèm lý do mẫu → xem phản hồi → quay về soạn trắc nghiệm.
- Xem ảnh xuất của Atlas, SVG, trình soạn trắc nghiệm và bảng thành phần. Dùng lại các điểm vào Figma khi nhóm kiểm tra tương tác trên thiết bị cảm ứng thực.

## Cập nhật tương tác Atlas 3D và Sơ đồ SVG

| Giao diện | Tương tác và trạng thái trong Figma |
| --- | --- |
| X01 và S02 · Atlas 3D | Quan sát toàn thân, xoay, zoom, reset và bật/tắt lớp. Hover hoặc tap một cơ quan làm hiện lớp phủ xanh ngọc trên phần bề mặt nhìn thấy và tooltip gồm tên, hệ, vị trí, chức năng. Rời vùng hover, chạm lại hoặc đóng thì trở về mặc định. Tắt Nội tạng ẩn cả hình và vùng tương tác Tim/Phổi trái. |
| S02 · Sơ đồ SVG | Chọn hệ và hotspot theo `viewBox`. Mỗi ID có trạng thái Mặc định, Hover, Đã chọn kết hợp Có/Chưa có học liệu. Tim mở S03. Phổi trái mở form hiện có, xác nhận gửi, trở lại trạng thái đang chờ và có lối tới X07. Prototype có ví dụ người nhận Giảng viên và Quản trị viên. |
| S03 · Mô hình 3D chi tiết | Nghiên cứu cấu trúc, hoạt ảnh và đánh dấu đã thuộc. Lối về hệ mở SVG ở cơ quan đang học. |

[S02 Desktop](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=2-567) · [S02 Mobile](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=2-4171) · [Biến thể hotspot và sitemap](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=115-15578).

SVG dùng dữ liệu giải phẫu và trạng thái học liệu độc lập với GLB. Khi triển khai, tải mô hình theo chế độ xem và kiểm tra độ sâu, tổ hợp lớp, raycast liên tục cùng cử chỉ trên thiết bị thật. Figma minh họa Tim và Phổi trái bằng hình chiếu cố định tại các góc đã dựng. Hai hệ minh họa dùng cùng quy tắc neo SVG ở khung Desktop và Mobile.

Kiểm chứng Figma trong Edge gồm hover đổi cơ quan và rời vùng, tap mở/đổi/đóng, zoom, xoay, reset, tắt và bật lại Nội tạng. Đã bấm nhánh Tim → S03 và nhánh Phổi trái → biểu mẫu → xác nhận → đang chờ → X07. Ví dụ người nhận Quản trị viên mở cùng xác nhận. Kiểm tra cấu trúc 24 variant camera trên cả hai trang và sáu variant hotspot trên mỗi trang.
