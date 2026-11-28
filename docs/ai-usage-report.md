# Báo cáo sử dụng AI

Mỗi prompt làm việc trên AnatomAR có một mục riêng theo thứ tự thời gian. Mục ghi rõ phần AI thực hiện, phần nhóm tự sửa và kết quả kiểm chứng thực tế.

## 2026-11-26 · Tổ chức cấu trúc dự án cho nhóm hai thành viên

- **Công cụ**. Codex, PowerShell, Python, Git và Node.js.
- **Prompt chính**. Sau mỗi prompt, khai báo việc dùng AI. Bổ sung cấu trúc thư mục theo yêu cầu CSE122 cho nhóm hai thành viên và giữ các thư mục hiện có để dễ tra cứu, sửa lỗi và nâng cấp.
- **Phần AI sinh**. Tạo các thư mục còn thiếu, tệp nhận diện thư mục rỗng, tệp nền CSS và JS có chú thích, liên kết Figma, tài liệu đề xuất và phân công. Cập nhật README, quy ước báo cáo và người phụ trách của 32 màn hình.
- **Phần nhóm tự sửa**. Nhóm cung cấp số thành viên và yêu cầu bảo toàn cấu trúc hiện có. Chưa ghi nhận chỉnh sửa thủ công của nhóm sau đầu ra AI. Phân công dùng mã `SV1` và `SV2` để nhóm đối chiếu.
- **Cách kiểm chứng**. Đối chiếu mục §20, kiểm tra đường dẫn Markdown, dữ liệu JSON, cú pháp hai tệp JS và phân công 16 màn hình mỗi người. Thử tải bảy tệp qua HTTP cục bộ. So sánh mã băm bốn tệp có sẵn và trạng thái Git của hai demo. Lần kiểm tra bảng đầu tiên gặp lỗi mã hóa dấu gạch trong khoảng mã màn hình. Đã chỉnh phép kiểm tra và chạy lại thành công. Phép thử HTTP chỉ kiểm tra các tệp tĩnh ở giai đoạn chuẩn bị triển khai.
- **Điều học được**. Một bảng kiểm kê duy nhất giúp đối chiếu mã màn hình, người phụ trách, tệp và minh chứng. Khi sắp xếp cấu trúc, kiểm tra đường dẫn và dữ liệu riêng với hành vi ứng dụng để biết phần nào đã được xác minh.

## 2026-11-27 · Hoàn thiện thiết kế Figma và đối chiếu CSE122

- **Công cụ**. Codex, Figma MCP, Figma Desktop với plugin phát triển cục bộ, Edge, PowerShell, Python và Git.
- **Prompt chính**. Rà soát và chỉnh trực tiếp thiết kế AnatomAR trên Desktop và Mobile. Bổ sung SVG tương tác, hoàn thiện nghiệp vụ bốn vai trò, các trạng thái và tài liệu bàn giao theo đề CSE122. Phạm vi thiết kế UI/UX và đặc tả nghiệp vụ.
- **Phần AI sinh**. Thêm chế độ SVG và các vùng chọn Tim/Phổi trái, bổ sung trình soạn trắc nghiệm A–D, chú thích SVG, hộp thoại CRUD, đề xuất, duyệt và phản hồi. Nối điều hướng theo vai trò và cập nhật Design System, sitemap, user flow, kiểm kê và hợp đồng Mock API.
- **Phần nhóm tự sửa**. Nhóm cung cấp thiết kế, đề bài và yêu cầu hiệu chỉnh. Chưa ghi nhận sửa thủ công sau lần cập nhật này. Nhóm cần duyệt nội dung giải phẫu, xác nhận nguồn tài nguyên, hoàn thiện minh chứng và tự giải thích luồng trước khi nộp.
- **Cách kiểm chứng**. Figma MCP hết hạn mức Starter. Bản cập nhật được thực hiện trong Figma Desktop rồi mở lại từ liên kết prototype trong Edge. Kiểm tra cấu trúc 64 màn hình nền và đích liên kết trên hai trang. Bấm thử nhánh SVG → Phổi trái → gửi đề xuất trên Mobile, tooltip và chọn Tim trên Desktop, từ chối trắc nghiệm → lý do → phản hồi → mở lại trình soạn. Kiểm tra ảnh xuất trước và sau khi chỉnh chồng chữ.
- **Điều học được**. Điểm chọn di chuyển theo tư thế dựng sẵn giúp kiểm tra tương tác trong Figma. Picking theo hình học, quy tắc che khuất và clip GLB cần kiểm bằng viewer thật. Gói Starter giới hạn thao tác kết hợp nên các kết quả duyệt dùng những frame phản hồi đã nối. Đồng bộ xuyên màn hình và phiên, form nhập tự do, phân quyền, chấm điểm và thiết bị cảm ứng còn chờ nhóm kiểm chứng khi triển khai.

## 2026-11-27 · Phân lại tương tác Atlas 3D và Sơ đồ SVG

- **Công cụ**. Codex, Figma MCP, Figma Desktop với plugin phát triển cục bộ, Edge, PowerShell, Python, OpenCV và trình kết xuất của mô hình tham chiếu.
- **Prompt chính**. Giữ thiết kế hiện có. Dùng Atlas 3D để quan sát và xem thông tin nhanh. Dùng Sơ đồ SVG để chọn hệ, mở học liệu hoặc gửi đề xuất và theo dõi phản hồi. Đồng bộ Desktop, Mobile, prototype và tài liệu.
- **Phần AI sinh**. Trích vùng bề mặt Tim và Phổi trái từ các hình chiếu của GLB hiện có. Cập nhật tooltip và variant hover/tap cho X01 và S02. Neo hotspot theo vùng hình của từng hệ, chuyển form và xác nhận đề xuất cũ sang SVG, thêm trạng thái đang chờ và lối về thông báo. Đồng bộ các tài liệu thiết kế.
- **Phần nhóm tự sửa**. Nhóm cung cấp cơ chế tương tác và phạm vi. Chưa ghi nhận chỉnh sửa thủ công sau lượt này. Nhóm còn cần duyệt nguồn học liệu, kiểm mặt che khuất và thao tác trên thiết bị thật khi triển khai.
- **Cách kiểm chứng**. Figma MCP còn hết hạn mức Starter. Chỉnh trực tiếp trong Figma Desktop, kiểm tra cấu trúc 24 variant camera trên cả hai trang và sáu variant hotspot trên mỗi trang. Mở lại prototype trong Edge và thử hover, tap mô phỏng, zoom, xoay, reset, tắt/bật Nội tạng, nhánh Tim mở S03 và nhánh Phổi trái gửi đề xuất đến Thông báo. Ví dụ chuyển Quản trị viên đi đến xác nhận.
- **Điều học được**. Một variant hover cho mỗi góc tránh hai tooltip chồng nhau. Đặt vùng tương tác vào variant Nội tạng đang hiện giúp ẩn tương tác cùng mô hình. Figma thể hiện các hình chiếu và dữ liệu mẫu. Kiểm depth theo mọi tổ hợp lớp, hiệu năng, cử chỉ thật và định tuyến người nhận theo dữ liệu cần thực hiện khi triển khai.

## 2026-11-27 · Rà soát giải phẫu và chuẩn hóa 11 hệ cơ quan

- **Công cụ**. Codex, OpenStax, FIPAT TA2, Figma Desktop, PowerShell, Python và Git.
- **Prompt chính**. Rà đủ 11 hệ cơ quan. Chuẩn hóa tên, quan hệ và phân nhóm trong dữ liệu AnatomAR, Atlas, sơ đồ SVG và mô hình 3D. Giữ thiết kế giao diện, tài nguyên và các luồng khác. Đánh dấu thông tin thiếu căn cứ.
- **Phần AI sinh**. Thêm danh mục 11 hệ, 45 phân nhóm, 209 mục và 21 quan hệ có nguồn trong `db.json`. Lập bảng đối chiếu từng node của 13 GLB và 408 mục mô tả cấu trúc cho demo tham chiếu. Bổ sung năm thẻ hệ còn thiếu vào P01 Desktop và Mobile, đồng bộ tên Hệ xương, nhánh thần kinh và các nhãn lớp Atlas. Ghi các ngoại lệ trong [báo cáo rà soát giải phẫu](anatomy-audit.md).
- **Phần nhóm tự sửa**. Nhóm xác định phạm vi và hai nguồn chuẩn. Chưa ghi nhận chỉnh sửa thủ công sau lượt này. Nhóm còn cần duyệt các tên Việt, kiểm hình học và bên của 123 node được đánh dấu, chuẩn bị tài nguyên cho các hệ còn thiếu và đối chiếu tọa độ hotspot trên SVG thực.
- **Cách kiểm chứng**. Kiểm tra ID, cây cha–con, quan hệ nhiều hệ, mã TA2, liên kết nội bộ và 37 trang OpenStax. So sánh mã băm của 13 GLB, đối chiếu 2.229 node và liên kết của 408 mục JSON. Mở lại Figma Desktop, xuất hai khung P01 để kiểm đủ thẻ và bố cục, kiểm nhãn tại bốn khung Atlas, đối chiếu Tim/Phổi trái trên các trạng thái SVG và kiểm tra các đích liên kết sẵn có của P01.
- **Điều học được**. Tách hệ cơ quan, nhánh giải phẫu và công tắc hiển thị giúp phát hiện sai nhóm do dùng tên lớp làm hệ. Mã TA2 và tên node hỗ trợ kiểm tra thuật ngữ. Xác nhận hình dạng, phạm vi và bên của một mesh cần thêm bằng chứng hình học.

## 2026-11-28 · Tạo lớp và tham gia bằng mã

- **Công cụ**. Codex, Figma MCP, Figma Desktop, plugin phát triển cục bộ, PowerShell và Git.
- **Prompt chính**. Cho giảng viên tạo lớp có mã riêng và sinh viên nhập mã do giảng viên cung cấp để tham gia.
- **Phần AI sinh**. Cập nhật T07 để hiển thị và sao chép mã lớp. Thêm mục «Lớp của tôi» và form nhập mã ở S01 trên Desktop/Mobile. Nối các trạng thái tạo lớp, nhập mã, xác nhận, tham gia lại và bổ sung đặc tả F08, sitemap, bảng màn hình, hợp đồng dữ liệu.
- **Phần nhóm tự sửa**. Nhóm nêu rõ quy trình chia sẻ mã qua giảng viên. Chưa ghi nhận thay đổi thủ công sau lượt này. Nhóm cần triển khai sinh mã duy nhất, sao chép thật, kiểm quyền, lưu thành viên và kiểm thử đồng bộ S01/T07/T04.
- **Cách kiểm chứng**. Kiểm tra các đích prototype F08 trên hai trang, đối chiếu mã lớp mẫu, xuất khung T07, S01 và các hộp thoại. Phát hiện và sửa nền thẻ tiến độ trên Mobile để nội dung nằm đúng trong thẻ. Bản Figma dùng mã và trạng thái mẫu.
- **Điều học được**. Mã tham gia thuộc bản ghi lớp. Danh sách sinh viên ở T07 và báo cáo T04 cần đọc cùng dữ liệu thành viên với thao tác tham gia ở S01. Gửi lại cùng mã cần trả trạng thái đã tham gia và giữ một mục thành viên.

## 2026-11-28 · Đồng bộ đặc tả trước khi triển khai MVP

- **Công cụ**. Codex, PowerShell, Python và Git.
- **Prompt chính**. Đối chiếu bộ đặc tả và đề CSE122. Thống nhất điều hướng, quyền, lớp, duyệt học liệu, ID, phương tiện, đề xuất và dữ liệu mock. Giữ các trang đã duyệt và hoãn AI tùy chọn. Phạm vi cập nhật tài liệu hiện có.
- **Phần AI sinh**. Chốt quyền theo vai trò và bản ghi, tạo lớp và tham gia theo mã, phiên bản học liệu, bộ quiz và nhóm thẻ, tiến độ theo cơ quan, điều kiện xuất bản và hoàn tất đề xuất kèm thông báo. Cập nhật điều hướng, thành phần dùng chung, hợp đồng mock và các trường hợp nghiệm thu.
- **Phần nhóm tự sửa**. Nhóm cung cấp đề gốc và yêu cầu thiết kế. Chưa ghi nhận chỉnh sửa thủ công sau lượt này. Nhóm cần xác nhận phương án hai thành viên, chuẩn bị học liệu và dữ liệu mẫu, đối chiếu các trạng thái mới trong Figma, triển khai và kiểm thử.
- **Cách kiểm chứng**. So sánh mã màn hình, tên tệp và phân công của 32 dòng với bản trước. Kiểm đủ 16 tên tệp nền tảng, 9 trang dùng chung, 4 vai trò, 13 mã luồng, 11 hệ và 8 tập dữ liệu tối thiểu. Kiểm liên kết Markdown nội bộ, `git diff --check` và xác nhận đề gốc cùng `db.json` giữ nội dung hiện có. Đây là rà soát tài liệu.
- **Điều học được**. Định danh giải phẫu, phiên bản đã xuất bản và khả năng tải tài nguyên là ba điều kiện khác nhau. Dùng chung phép tính tiến độ và ghi xuất bản cùng kết quả đề xuất để các vai trò đọc trạng thái nhất quán.
