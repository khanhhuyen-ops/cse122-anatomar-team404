# Đặc tả thiết kế AnatomAR

AnatomAR hỗ trợ dạy và học giải phẫu cơ thể người trong học phần CSE122. Sinh viên đi từ sơ đồ cơ thể đến cơ quan, quan sát cấu trúc và chuyển động, rồi tự kiểm tra bằng thẻ ghi nhớ hoặc trắc nghiệm. Giảng viên xây dựng học liệu trực quan và theo dõi mức ghi nhớ. Quản trị viên duy trì tài khoản, danh mục và cấu hình.

## Phạm vi

[Tài liệu yêu cầu dự án](../.agents/skills/AnatomAR-project-requirements.md) là căn cứ về chức năng, tên tệp, phạm vi vai trò và minh chứng. Brief thiết kế bổ sung yêu cầu hoạt ảnh cơ quan 3D, giao diện tiếng Việt và ưu tiên HTML, CSS, JavaScript thuần, SVG, Three.js, API JSON mô phỏng.

- **Cốt lõi** gồm 16 tệp nền tảng, 9 trang dùng chung và các màn hình bổ sung cần để hoàn thành luồng. [Bảng kiểm kê](screen-list.md) ghi CRUD, trạng thái, luồng và phụ trách theo yêu cầu §§08–09, 15.
- **Cách vận hành đề xuất** gồm phạm vi tài khoản và lớp, phân công duyệt học liệu và đề xuất chủ đề, cách tính tiến độ, chấm điểm, cách giả lập phiên và lưu dữ liệu. Các quyết định này cụ thể hóa luồng để nhóm triển khai và có thể điều chỉnh khi duyệt.
- **Mở rộng** gồm ba ý tưởng AI ở §12, đặc tả ở cuối [luồng người dùng](user-flow.md). Chế độ tối toàn trang, PWA và cá nhân hóa lộ trình ở ngoài phạm vi MVP. Vùng 3D có nền tối cố định như một phần định hướng hình ảnh.

## Định hướng hình ảnh

**Medical Education × Interactive Anatomy Atlas.** Trang chủ mở bằng mô hình 3D toàn thân có bảng bật tắt từng lớp giải phẫu. Nền xanh đậm của vùng xem tách biên mô hình. Trên nền sáng, bố cục đọc từ hệ cơ quan đến cấu trúc, vị trí, chức năng và nguồn. Dashboard dùng cùng hệ chữ và màu nhấn. Bảng, danh sách và thứ tự nội dung giúp mỗi vai trò nhận ra việc cần làm.

Các ảnh tham chiếu gợi cách dùng thẻ nền sáng, màu nhạt theo chủ đề, tiến độ có số đếm và vùng xem tối. Trong 3D, tên cấu trúc chỉ xuất hiện gần con trỏ khi đang trỏ vào hình học hợp lệ. Cách tổ chức theo hệ cơ quan và đường vào mô hình mẫu lấy cảm hứng từ danh mục giải phẫu tiếng Việt. Nội dung, bố cục, bộ nhận diện và hình minh họa được thiết kế riêng cho AnatomAR. [Danh mục Giaiphau3D](https://app.giaiphau3d.com/home).

Literata dành cho tiêu đề mở đầu và tên hệ hoặc cơ quan. Be Vietnam Pro dành cho nội dung, điều khiển và dashboard. Xanh ngọc đậm dùng cho hành động chính. Màu mô và đường chỉ dẫn thuộc minh họa. Tên cấu trúc bằng tiếng Việt xuất hiện trước. Tên Latin chỉ hiển thị khi đã có nguồn. Nhãn và số thứ tự dùng cho chú thích, trình tự hoặc dữ liệu. [Token và hệ chữ](../.agents/skills/anatomar-design/references/design-system.md).

UI/UX Pro Max gợi ý tương phản cao, sắc xanh y khoa, vùng chạm rộng và giảm chuyển động. Frontend Design định hướng dùng bản minh họa giải phẫu làm nội dung chính của trang đầu và đưa «Khám phá các hệ cơ quan» thành hành động nổi bật. Dùng Web Design Guidelines để rà quy tắc về focus, nhập liệu, trạng thái và URL ở mức đặc tả. [UI/UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill/blob/f2f7266b07805025421611656045e9b44b41e2eb/.claude/skills/ui-ux-pro-max/SKILL.md) · [Frontend Design](https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md) · [Web Design Guidelines](https://github.com/vercel-labs/agent-skills/blob/main/skills/web-design-guidelines/SKILL.md).

## Vai trò và điều hướng

| Vai trò hiển thị | Điểm bắt đầu | Nghiệp vụ | Phạm vi mặc định đề xuất |
| --- | --- | --- | --- |
| Khách (Visitor) | X01 · Trang chủ công khai | Xem tổng quan các hệ, khám phá mô hình mẫu, gửi đề xuất chủ đề và xem trạng thái. | Hệ công khai, mô hình mẫu đã xuất bản, đề xuất của mình qua mã tra cứu. |
| Sinh viên (Student) | S01 · Bảng điều khiển | Học theo hệ, khám phá mô hình, đánh dấu cơ quan đã thuộc, ôn thẻ, tự làm trắc nghiệm và xem tiến độ. | Học liệu đã xuất bản, dữ liệu học của mình. |
| Giảng viên (Teacher) | T01 · Bảng điều khiển | Tạo và quản lý cơ quan/mô hình, dựng học liệu SVG, soạn trắc nghiệm và thẻ, quản lý lớp, xem tiến độ. | Học liệu mình phụ trách, danh sách lớp mình quản lý và tiến độ của sinh viên trong lớp. |
| Quản trị viên (Admin) | A01 · Bảng điều khiển | Thêm và phân quyền tài khoản, vô hiệu hóa, cấu hình hệ và đề mục, quản lý thư viện mô hình, xử lý học liệu và đề xuất. | Tài khoản, danh mục, nội dung chờ xử lý và cấu hình. |

Tài khoản tự đăng ký nhận vai trò Sinh viên. Quản trị viên cấp vai trò và trạng thái tài khoản theo phạm vi đề xuất trong luồng F11. Các tài khoản Quản trị viên dùng để trình diễn có sẵn trong dữ liệu mẫu. Sau khi đăng nhập, «Khu vực của tôi» luôn về dashboard của phiên hiện tại. Những tài liệu riêng của lớp và tài khoản được lọc theo quyền của bản ghi. [Hợp đồng dữ liệu mô phỏng](../.agents/skills/anatomar-design/references/mock-data.md).

## Bốn cách truyền đạt kiến thức (§11)

| Cách | Màn hình | Cách thể hiện |
| --- | --- | --- |
| Học liệu SVG riêng | T05 · Dựng học liệu SVG | Giảng viên tạo sơ đồ có chú thích và danh sách tên theo mục tiêu bài học. Học liệu đã duyệt xuất hiện trong danh sách học liệu của hệ. |
| Mô hình 3D toàn thân | X01 · Trang chủ, S02 · Học theo hệ | Kéo trực tiếp để xoay tự do 360° quanh cơ thể, nghiêng góc nhìn, thu phóng và bật nhiều lớp cùng lúc. Mỗi lần chỉ chọn một bộ phận để học. |
| Mô hình cơ quan và hoạt ảnh | P02 · Mô hình mẫu, S03 · Mô hình cơ quan | Đổi góc nhìn, xoay, phóng to, chọn một cấu trúc và chủ động phát hoạt ảnh có sẵn. Danh sách và chi tiết bằng văn bản vẫn dùng khi 3D gặp lỗi. |
| Thẻ ghi nhớ | S05 · Thẻ ghi nhớ | Nhớ trước khi hiện đáp án. Tự đánh giá «Đã thuộc» hoặc «Cần ôn lại» từng thẻ và ôn lại nhóm cần củng cố. |
| Trắc nghiệm kèm giải thích | S04 · Trắc nghiệm, S06 · Kết quả | Câu hỏi về vị trí hoặc chức năng. Sau khi nộp, hiển thị đáp án, điểm và giải thích, kể cả các câu trả lời sai. |

## Bố cục và hành vi chung

| Mẫu | Công việc chính | Nội dung luôn có |
| --- | --- | --- |
| Public | Khám phá, xem mẫu, gửi đề xuất | Điều hướng, tiêu đề, nội dung theo nhiệm vụ và lối quay về. |
| Atlas | Chọn cơ quan và bắt đầu học | Chọn hệ hoặc lớp, nhấn cơ quan trong vùng xem hoặc chọn từ danh sách. Thẻ cơ quan hiện «Xem mô hình» khi có học liệu hoặc «Gửi đề xuất học liệu» khi chưa có. |
| Auth | Đăng nhập, đăng ký, đặt lại mật khẩu | Một cột, nhãn trường, lỗi gần trường và hành động tiếp theo. |
| Study | Học bằng thẻ hoặc trắc nghiệm | Một thẻ/câu mỗi lượt, chỉ báo tiến trình, điều khiển đi tiếp và phản hồi. |
| Dashboard | Xem tiến độ và việc cần xử lý | Số liệu có mẫu số hoặc kỳ thống kê, liên kết đến danh sách liên quan. |
| Records / Editor | Xem danh sách hoặc sửa bản ghi | Bộ lọc, trạng thái nghiệp vụ, thao tác theo quyền, xem trước và xác nhận khi cần. |

Các mẫu và wireframe desktop/mobile nằm trong [bố cục](../.agents/skills/anatomar-design/references/layout.md). Cấu tạo và hành vi ở [thành phần](../.agents/skills/anatomar-design/references/components.md), [tương tác](../.agents/skills/anatomar-design/references/interaction.md) và [trình xem 3D](../.agents/skills/anatomar-design/references/viewer-3d.md).

## Quy ước triển khai sau

- Dùng tiếng Việt có dấu, câu ngắn và động từ cụ thể. Thống nhất «Hệ cơ quan», «Cơ quan», «Cấu trúc», «Lớp giải phẫu», «Lớp học», «Thẻ ghi nhớ», «Trắc nghiệm». Dùng `vi-VN` khi hiển thị thời gian và số.
- Dùng HTML ngữ nghĩa, CSS custom properties và JavaScript dạng module theo nhiệm vụ. SVG và Three.js dùng ID ổn định để nối hình minh họa với dữ liệu học. Giữ điều khiển là phần tử HTML.
- Dữ liệu xuất phát từ `db.json`. Khi triển khai, để một module dữ liệu đọc JSON và áp dụng các thao tác ghi mô phỏng. Dùng tài khoản, mật khẩu và thông tin giả lập. [Mô hình dữ liệu](../.agents/skills/anatomar-design/references/mock-data.md).
- Thiết kế mô hình, chú thích và điều khiển theo [đặc tả trình xem](../.agents/skills/anatomar-design/references/viewer-3d.md). Ghi nguồn và giấy phép riêng của mỗi tài nguyên khi chọn dữ liệu cho sản phẩm.
- Dùng WCAG 2.2 AA làm mục tiêu thiết kế. Kiểm tra bàn phím, trình đọc màn hình, zoom, giảm chuyển động và khả năng đọc chi tiết khi WebGL lỗi. [Đặc tả tiếp cận](../.agents/skills/anatomar-design/references/accessibility.md).

## Duyệt và bàn giao

Tệp Figma chứa tổng quan và thành phần, thiết kế desktop và thiết kế mobile. Tên frame dùng mã trong bảng kiểm kê. Hình tim được tạo bằng ImageGen cho bản mô phỏng giao diện, chờ đối chiếu giải phẫu trước khi dùng làm học liệu. [Thiết kế trên Figma](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=0-1).

Prototype X01 và S02 dùng ảnh kết xuất để minh họa các lớp giải phẫu. Kéo chuyển qua ba góc nhìn dựng sẵn. Nút thu phóng có hai mức, nút đặt lại về mặt trước và giữ lớp đã chọn. Hover chỉ hiện tên và làm nổi cấu trúc theo đặc tả. Click hoặc chạm ngắn thay lựa chọn hiện tại bằng ID mới, dùng cùng bản ghi với danh sách. Luồng xem mô hình chỉ dùng 3D. Trong prototype S02, chọn từ bảng «Cơ quan» để duyệt hai nhánh. Tim dẫn đến mô hình cơ quan, Phổi trái minh họa nhánh chưa có học liệu và gửi đề xuất. Kiểm tra raycast, che khuất, camera liên tục và hoạt ảnh thực hiện khi có viewer Three.js. [Bảng trạng thái Figma](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=70-1020) · [Quy tắc Object Picking](../.agents/skills/anatomar-design/references/viewer-3d.md#object-picking-và-tooltip-động).

<details>
<summary>Nguồn hình minh họa tim</summary>

Ảnh PNG gốc dùng trong bản thiết kế. [Minh họa tim](mockups/Minh-hoa-tim.png).

> Create a single original transparent-background cutout image to place inside an educational Vietnamese anatomy atlas UI design. One adult anatomical human heart, front-oblique view, including visible connected aorta and pulmonary vessels, centered and filling almost the entire canvas, no body, no hands and no props. A sophisticated tactile 3D medical textbook illustration, coral-red and deep burgundy natural tissue with blue-green accents on great vessels, substantial soft studio light and confident clear silhouette, suitable above a very dark navy canvas. Anatomy plausible and editorially simplified for an interface mockup. Entire heart and vessels inside the image with 8% clear space, no floor, no cast shadow, no frame, no text, no labels, no watermarks, no additional anatomy. Transparent PNG background.

</details>

1. Duyệt bảng kiểm kê, trách nhiệm, quy tắc nghiệp vụ và các wireframe. Dựng mockup Figma/Canva desktop, responsive, tải/rỗng/lỗi và tương tác SVG ở bước duyệt hình ảnh theo §19.
2. Mỗi thành viên thực hiện ít nhất một luồng từ thiết kế đến dữ liệu, responsive và kiểm thử theo [phân công nhóm hai thành viên](../docs/team-assignment.md). Nối mã màn hình với task Trello, nhánh, commit, PR, review và merge `dev`.
3. Mỗi giao diện thực tế đã duyệt có một video OBS. Trong video, mở đúng mockup và tệp HTML/CSS/JS, giải thích nghiệp vụ, làm một thay đổi nhỏ và chứng minh có thể làm lại. Cập nhật README, bảng kiểm kê và `docs/ai-usage-report.md` theo yêu cầu nhóm. [Yêu cầu minh chứng §§16–23](../.agents/skills/AnatomAR-project-requirements.md).
