# Trình xem 3D

X01 và S02 có Atlas 3D toàn thân để quan sát và xem thông tin nhanh. S02 có chế độ Sơ đồ SVG với cùng ID cơ quan để chọn học liệu và gửi đề xuất. P02 xem mô hình mẫu. S03 xem cấu tạo, điều khiển hoạt ảnh và đánh dấu đã thuộc. Dùng SVG, danh sách hoặc văn bản khi 3D lỗi hay tải chậm. T06/A04 dùng trình xem để xem trước. T05 biên tập SVG và chú thích. [Màn hình](../../../../design/screen-list.md).

## Lớp hiển thị toàn thân

- Bảng lớp điều khiển Xương và sụn, Cơ vân và gân, Nội tạng, Động mạch, Tĩnh mạch, Cấu trúc thần kinh và Da. Mỗi lớp có ô chọn riêng. Mặc định hiện Xương và sụn và Nội tạng. Dùng `visualLayerId` để điều khiển lớp. Hệ và nhánh giải phẫu đọc từ danh mục trong `db.json`.
- Màn rộng đặt bảng lớp bên cạnh mô hình. Màn hẹp đặt bảng lớp dưới vùng xem. Bật hoặc tắt lớp giữ góc nhìn hiện tại. «Đặt lại góc nhìn» trả camera về mặt trước và giữ các lớp đang hiện.
- Kéo ngang trong vùng xem để quay đủ vòng 360° theo cả hai chiều. Kéo dọc để nghiêng góc nhìn, giới hạn gần hai cực để giữ hướng lên của cơ thể. Góc nhìn dừng tại vị trí người học thả tay. Ba nút «Thu nhỏ», «Phóng to» và «Đặt lại góc nhìn» đặt dưới mô hình. Cách kéo trực tiếp và nhóm nút riêng tham chiếu trình xem mô hình của Giaiphau3D. [Mẫu phổi trái](https://app.giaiphau3d.com/respiratory-system/left-lung).
- Các hình minh họa trong Figma được kết xuất lại từ bản GLB giản lược của Human Anatomy 3D, dựa trên Z-Anatomy và BodyParts3D. Bản kết xuất của lớp Nội tạng bỏ mẫu thận có giấy phép khác. [Nguồn và giấy phép mô hình](https://github.com/SeemaBansal1/3d-human-body-anatomy#credits-and-licences).

## Cấu tạo và chọn cấu trúc

1. Hiển thị tên cơ quan, hướng nhìn và hệ liên quan. Dùng hướng giải phẫu của chủ thể cho trái/phải. Chỉ ghi nhãn hướng khi đã có dữ liệu phù hợp.
2. Khi mô hình đang tải, ảnh tĩnh chỉ minh họa. Chọn tên trong danh sách hoặc hình học 3D đã xác minh sẽ đặt cùng một `selectedEntityId`. Lựa chọn mới thay ID trước đó và cập nhật thẻ chi tiết với tên, hệ cơ quan, mô tả, vị trí, chức năng và nguồn theo dữ liệu hiện có.
3. Vùng xem ở trạng thái nghỉ hiển thị mô hình và điều khiển camera. Bỏ nhãn thường trực, chấm chỉ dẫn, đường nối, hotspot theo tọa độ màn hình và công tắc «Hiện nhãn».
4. Nếu cấu trúc nằm trong lớp vừa ẩn, giữ thẻ chi tiết và hiển thị «Cấu trúc nằm trong lớp đang ẩn» kèm «Hiện lớp». Nếu mô hình không ánh xạ được cấu trúc đó, giữ lựa chọn trong danh sách và giải thích phạm vi mô hình.
5. Khi đổi cơ quan, dừng hoạt ảnh và về góc nhìn mặc định của cơ quan mới. «Đặt lại góc nhìn» đặt camera mặc định, giữ cơ quan, lựa chọn, lớp và trạng thái phát. «Xóa lựa chọn» chỉ bỏ cấu trúc đang chọn.

Tại S02, Atlas 3D cung cấp thông tin nhanh ngay trong vùng xem và bảng tên cơ quan. Sơ đồ SVG hoặc danh sách cùng mở thẻ theo `organId`. Bài đã xuất bản mở S03 bằng «Xem học liệu», hoặc «Xem mô hình 3D» khi có GLB dùng được. Cơ quan chưa có bài có nút «Gửi đề xuất học liệu». S03 giữ `structureId` riêng khi chọn bộ phận. [Luồng chọn cơ quan và gửi đề xuất](../../../../design/user-flow.md#f02--định-vị-cơ-quan-và-khám-phá-mô-hình).

## Object Picking và tooltip động

| Trạng thái | Hành vi |
| --- | --- |
| Rê vào hình học hợp lệ tại Atlas | Phủ xanh ngọc 60% lên toàn bộ phần bề mặt đang thấy của mesh cùng ID, theo đường biên thực và độ sâu. Tooltip ghi tên, hệ, vị trí và chức năng của cơ quan gần camera nhất trên tia. |
| Rê sang đối tượng khác, vùng trống hoặc rời vùng xem | Đổi đồng thời tooltip và lớp phủ khi ID đổi. Rời hit hợp lệ hoặc bấm Escape thì ẩn cả hai. |
| Chạm ngắn tại Atlas | Tính hit tại điểm thả. Mở ngay tooltip và lớp phủ của một cơ quan. Chạm cơ quan khác thay cả hai, chạm lại hoặc bấm đóng để ẩn. Phân biệt với kéo, cuộn, chụm, pan và `pointercancel`. |
| Xoay, zoom, pan hoặc quán tính camera | Ẩn thông tin xem nhanh khi bắt đầu thao tác. Khi dừng, desktop tính lại hit nếu con trỏ còn trong canvas. Trình xem S03 giữ cấu trúc đang đọc. |
| Đặt lại góc nhìn, đổi lớp hoặc hệ | Hủy hit tạm cũ ngay. Tính lại sau khi đồng bộ camera, kích thước canvas, lớp và bộ lọc hiện hành. Khi lớp được chọn bị ẩn, chỉ giữ chi tiết với trạng thái «Cấu trúc nằm trong lớp đang ẩn». |
| Chạy, tạm dừng hoặc tua lại hoạt ảnh | Dùng hình học sau khi cập nhật pose và camera ở khung hiện tại, kể cả khi chuột đứng yên. Xóa hoặc đổi hover khi cấu trúc dịch khỏi tia. Nếu tài nguyên biến dạng mà đường picking chưa hỗ trợ pose hiện tại, dùng danh sách để chọn trong lúc phát. |
| Chuyển model, lỗi, tải hoặc dùng ảnh chờ | Xóa hover ngay, loại kết quả từ phiên model cũ. Giữ lựa chọn khi ID hợp lệ trong phạm vi mới, hoặc giải thích trong danh sách khi chưa có hình học tương ứng. |

- Neo tooltip vào điểm chiếu của cơ quan. Canh cách điểm neo khoảng 12–16 px và cách mép vùng xem ít nhất 8 px. Ưu tiên phía còn trống, lật phía khi gần mép. Tránh hình và điều khiển. Tooltip hover bỏ qua sự kiện con trỏ. Bản tap có nút đóng.
- Atlas chỉ phủ một cơ quan mỗi lần. Lớp phủ dùng lại geometry và chỉ hiển thị khi có hit hợp lệ. Cập nhật theo thực thể để giữ màu gốc ở các mesh dùng chung material. S03 quản lý highlight và lựa chọn cấu trúc của trình xem chi tiết.
- Quy đổi tọa độ con trỏ theo khung canvas hiện tại rồi raycast bằng camera hiện tại. Kiểm tra giao điểm theo khoảng cách tăng dần. Bỏ qua lớp chưa tải hoặc đang ẩn, mesh và tổ tiên bị ẩn, phần vật liệu không được vẽ, vùng đã bị cắt và mesh phụ như đèn hiệu, nền, lưới hoặc sprite. Một bề mặt giải phẫu kín đang che phía trước mà chưa có ánh xạ phải trả về không có lựa chọn tại tia đó để tránh gán tên của cơ quan phía sau. Chế độ xuyên lớp, nếu có, phải dùng cùng quy tắc xuyên lớp cho hình và picking. [Raycaster](https://threejs.org/docs/pages/Raycaster.html).

## Ánh xạ hình học và kiểm tra tài nguyên

Mỗi thực thể có `id`, `nameVi`, `systemId`, `descriptionVi`, và `parentId` khi là cấu trúc con của một cơ quan. `layerId` thuộc hình học hiển thị và có thể khác `systemId`, ví dụ `organs` chứa cả Tim và Phổi trái. Mỗi bản xuất mô hình ghi phiên bản và đường dẫn node, mesh hoặc primitive → ID. Dùng cùng ID cho hover, highlight, chi tiết, danh sách và SVG. Mỗi phần hình học hợp lệ có một ID đích trong một cấp xem. Atlas toàn thân ánh xạ những mesh thành phần về cơ quan. Viewer chi tiết có thể dùng ID riêng của cấu trúc con đã xác minh, với quan hệ `parentId` trở về cơ quan. [Hợp đồng dữ liệu](mock-data.md).

Đã đọc scene, node, mesh, primitive, `extras` và animation trực tiếp từ 13 GLB trong `third-part/`. `assets/models/`, `assets/animations/` và `js/` hiện chưa có tài nguyên hoặc mã trình xem của AnatomAR. Kết quả dưới đây dùng để lựa chọn cách chuẩn bị tài nguyên khi triển khai.

| Tài nguyên tham chiếu | Cấu trúc quan sát được | Quyết định thiết kế |
| --- | --- | --- |
| `3d-human-body-anatomy/web/public/models/` | Bảy GLB Draco có 2.198 node mesh gốc, mỗi node có một primitive và `extras.zname`, `zgroup`, `zlayer`, `zmat`. Không có node group trong các scene xuất sẵn. Số mesh theo lớp `skeleton` 271, `organs` 297, `arteries` 417, `veins` 226, `muscles` 476, `nerves` 255, `skin` 256. | Ưu tiên kiểm kê từng cặp lớp và `zname` theo phiên bản. `zgroup` là gợi ý phân loại, cần đối chiếu trước khi gộp. Phần trùng giữa lớp và hai bên cơ thể phải có quy tắc riêng. |
| `Human-Organ3D/models/liver.glb`, `lung.glb` | Gan có 5 mesh theo 5 group có tên, gồm gan, túi mật và ba mạch. Phổi có 2 mesh trong các group `part01` và `part02`, thiếu metadata nhận diện trái/phải ở node. | Dùng đường dẫn group gan khi đã đối chiếu hình. Xác minh từng mesh phổi theo pose giải phẫu và hình học, sau đó mới gán ID. Nếu một mesh có nhiều vùng, kiểm tra khả năng tách các vùng đó trước khi đặt tên riêng. |
| `Human-Organ3D/models/heart.glb`, `stomach.glb` | Mỗi tệp có 1 mesh, 1 primitive. Scene graph hiện không định danh phần bên trong. | Có thể chọn toàn bộ cơ quan sau khi duyệt nguồn. Muốn chọn buồng tim, mạch hoặc vùng dạ dày phải xác minh ranh giới hình học và chuẩn bị asset tương ứng. |
| `Human-Organ3D/models/kidney.glb`, `divide_within_-_medical.glb` | Lần lượt có 12 và 10 mesh, tên kỹ thuật và cùng một material trong mỗi tệp. Các node mesh không có `extras` giải phẫu. | Số mesh không đủ để kết luận số thực thể. Đối chiếu từng mảnh bằng lớp hình học và nguồn trước khi chọn theo cấu trúc. |

Các ID bên dưới có trong `db.json`. Bảng kiểm kê ghi node gốc, ID cấu trúc và quan hệ cha trong danh mục khi đã xác định. [Bảng đối chiếu nguồn](../../../../assets/data/anatomy-source-audit.csv).

| ID | Tên · Hệ · Mô tả | Ví dụ ánh xạ ở atlas toàn thân |
| --- | --- | --- |
| `organ.heart` | Tim · Hệ tuần hoàn · Bơm máu qua hệ mạch. | Mỗi buồng tim trong `organs` có ID riêng và `parentId` trỏ tới Tim. Dùng tổ tiên `organ.heart` cho tooltip cấp cơ quan. |
| `organ.lung-left` | Phổi trái · Hệ hô hấp · Trao đổi khí ở bên trái cơ thể. | `organs`: hai thùy của phổi trái có ID riêng và cùng trỏ tới Phổi trái. |
| `organ.lung-right` | Phổi phải · Hệ hô hấp · Trao đổi khí ở bên phải cơ thể. | `organs`: ba thùy của phổi phải có ID riêng và cùng trỏ tới Phổi phải. |
| `bone.sternum-body` | Thân xương ức · Hệ xương · Phần giữa của xương ức ở trước lồng ngực. | `skeleton`: `Body of sternum`. |

Nếu một mesh chứa nhiều thực thể, ưu tiên tách tại nguồn hoặc gán từng primitive hay vùng tam giác đã xác minh theo phiên bản hình học. Thành phần liên thông, biên vật liệu và nguồn gốc mesh là dữ liệu để đối chiếu. Khi đổi bản xuất do đơn giản hóa, nén hoặc sắp xếp lại chỉ số, kiểm tra lại ánh xạ theo vùng. Khi ranh giới chưa xác minh, giữ thực thể chung nếu đúng nghĩa giải phẫu hoặc dùng danh sách và mô tả cho các mục con. Không suy đoán theo tọa độ màn hình, tên material, số thứ tự hay phần chữ trùng trong tên mesh.

Không GLB nào trong 13 tệp có clip hoặc skin; hai demo minh họa chuyển động bằng JavaScript. Demo toàn thân có `OrbitControls`, `Raycaster` và tăng tốc BVH. Demo cơ quan dùng `OrbitControls` và sprite tạo từ tọa độ khai báo cho nhãn phổi. Tái sử dụng kỹ thuật tải model và điều khiển camera phù hợp khi triển khai. Kiểm tra riêng việc cập nhật pose, ma trận và cấu trúc tăng tốc trước khi chọn trên hình học đang chuyển động.

Nguồn atlas là Z-Anatomy CC BY-SA 4.0, dẫn xuất từ BodyParts3D CC BY-SA 2.1 JP. README ghi ngoại lệ thận CC BY-NC 4.0. Trong `Human-Organ3D`, `asset.extras` ghi tim, thận, dạ dày CC BY-NC 4.0, và phổi, gan, mẫu tổng hợp CC BY 4.0. Ghi tác giả và nguồn theo từng tệp trước khi dùng làm học liệu. [Nguồn atlas](https://github.com/SeemaBansal1/3d-human-body-anatomy#credits-and-licences) · [Nguồn sáu GLB cơ quan](../../../../third-part/Human-Organ3D/models/).

## Điều khiển

| Tác vụ | Chuột / cảm ứng | Nút hoặc tương tác tương đương |
| --- | --- | --- |
| Chọn một cấu trúc | Click/tap vào mesh đã ánh xạ | Danh sách cấu trúc có tên và nút chọn, Enter hoặc Space |
| Xoay | Kéo trong canvas / kéo một ngón sau khi kích hoạt thao tác | Nhóm nút «Xoay trái», «Xoay phải», «Xoay lên», «Xoay xuống», mỗi lần 15° |
| Dịch khung | Kéo phải chuột hoặc hai ngón trong vùng tương tác | Nút hướng trong «Tùy chọn hiển thị», dịch một bước theo khung |
| Phóng to / thu nhỏ | Cuộn trong vùng đã kích hoạt / chụm hai ngón | «Phóng to», «Thu nhỏ», mỗi bước thay đổi khoảng 10%, có giới hạn. Cuộn trang bình thường ngoài vùng đang tương tác. |
| Góc nhìn chuẩn | Đặt lại camera. Trình xem cơ quan có thể cung cấp góc nhìn chuẩn trong tùy chọn. | «Đặt lại góc nhìn». Với cơ quan có góc nhìn chuẩn, thông báo khi áp dụng. |
| Bật lớp | Chọn trong thanh điều khiển | Checkbox từng lớp sẵn có. Nêu lý do khi lớp thiếu dữ liệu. |
| Hoạt ảnh | Chọn clip có tên, bấm phát hoặc dừng | «Phát hoạt ảnh» / «Tạm dừng», «Về đầu» và mô tả chuyển động. Khi mô hình chỉ tĩnh, hiển thị «Mô hình này chưa có hoạt ảnh». |
| Toàn màn hình | Bấm mở/thoát toàn màn hình | Nút «Thoát toàn màn hình» dễ thấy, Escape thoát. Trả focus về nút mở. Nếu không hỗ trợ, tiếp tục dùng vùng xem nhúng. |

Trên mobile, các nút chính hiển thị ngay dưới vùng xem. Nhóm điều khiển phụ có thể mở bằng «Tùy chọn hiển thị». Vùng xem chỉ nhận kéo hoặc cuộn khi đã bật tương tác, có lối «Thoát điều khiển mô hình» và hướng dẫn lần đầu trong phiên. `Tab` đi qua các nút HTML. Phím tắt camera nếu thêm chỉ hoạt động khi focus ở vùng xem, với tên và hướng dẫn thấy được. [Bố cục](layout.md) · [Tiếp cận](accessibility.md).

## Hoạt ảnh và trạng thái

Hoạt ảnh minh họa một quá trình, ví dụ cơ quan chuyển động theo clip đã chuẩn bị. Dùng tên clip tiếng Việt, nhãn «Đang phát» hoặc «Đã tạm dừng» và một câu mô tả có thể đọc độc lập. Mặc định dừng ở khung đầu. Tạm dừng khi tab nền hoặc rời vùng xem. Khi quay về, người dùng chủ động tiếp tục. Với giảm chuyển động, đổi camera tức thời, giữ vị trí cuộn và quyền chủ động bấm phát.

| Trạng thái | Hiển thị và khôi phục |
| --- | --- |
| Chưa bắt đầu | Ảnh tĩnh nếu có, «Mở mô hình 3D» và thông tin cấu trúc. |
| Chưa gắn mô hình | Bài cơ quan vẫn mở. Hiện danh sách cấu trúc, văn bản, ảnh/SVG nếu có và dấu đã thuộc ở S03. |
| Đang tải hoặc giải mã | Giữ tỷ lệ vùng xem, ghi «Đang tải mô hình…». Chỉ hiện phần trăm khi biết tổng tải. Danh sách và chi tiết vẫn đọc được. |
| Sẵn sàng | Góc mặc định, điều khiển tương ứng tài nguyên. Focus giữ ở phần tử vừa thao tác. |
| Thiếu clip hoặc một lớp | Giữ phần đã sẵn sàng và ghi phần thiếu. Dùng ảnh hoặc văn bản mô tả quá trình nếu có. |
| Lỗi tải hoặc không có WebGL | Hiện «Không tải được mô hình 3D» hoặc thông báo WebGL cụ thể. Giữ «Thử lại» khi phù hợp và danh sách có chi tiết bằng văn bản. |
| Mất ngữ cảnh đồ họa | Tạm dừng, giữ lựa chọn và hiện lý do. «Khôi phục mô hình» nếu có thể khởi tạo lại. Người dùng tiếp tục học từ danh sách và văn bản. |

## Dữ liệu và chi phí hiển thị

- Dùng một viewer Three.js cho mỗi trang. Dự kiến `GLTFLoader` cho GLB và `OrbitControls` cho camera. Raycast các mesh con được ánh xạ, giới hạn chọn vào những lớp đang hiện. Module Three.js và add-on dùng cùng một phiên bản. [GLTFLoader](https://threejs.org/docs/pages/GLTFLoader.html) · [OrbitControls](https://threejs.org/docs/pages/OrbitControls.html).
- Tải ảnh tĩnh và phần thông tin trước. Nạp các lớp GLB mặc định trước rồi nạp lớp khác theo lựa chọn. Bản tải gần nhất quyết định nội dung xuất hiện. Dừng vòng lặp hiển thị khi trang ẩn, giải phóng geometry, material, texture và listener khi bỏ khỏi phạm vi dùng. [Quản lý tài nguyên Three.js](https://threejs.org/manual/pages/how-to-dispose-of-objects.html).
- Mục tiêu thử nghiệm cho mẫu mobile là GLB ban đầu khoảng 2 MB trở xuống, có thể thay bằng bản nhẹ hơn. Đo dung lượng thực khi chọn tài nguyên. Dashboard không phụ thuộc vào WebGL.
- Mỗi mô hình có đường dẫn, phiên bản, nguồn, giấy phép, văn bản thay thế, góc mặc định, lớp, ánh xạ cấu trúc và danh sách clip nếu có. T05 chỉnh vị trí trên SVG theo tọa độ chuẩn hóa, bằng click/kéo hoặc nhập số và nút dịch điểm. Chỉ dùng SVG mẫu đã đăng ký. [Hợp đồng dữ liệu](mock-data.md).

## Kiểm tra khi triển khai

| Ca thử | Kết quả chấp nhận |
| --- | --- |
| Rê từ Tim sang Phổi trái, Phổi phải rồi vùng trống | Một tooltip và một lớp phủ theo bề mặt của hit hiện tại. Vùng trống, rời canvas hoặc Escape tắt cả hai. |
| Chọn Tim, chọn Phổi trái rồi xóa lựa chọn | Thẻ chỉ hiển thị Phổi trái sau lần chọn thứ hai. Xóa lựa chọn đưa thẻ về trạng thái chờ chọn và bỏ viền chọn. |
| Rê lên nhiều mesh thuộc Tim hoặc hai thùy Phổi trái | Mọi mesh cùng cơ quan mở cùng bản ghi ở atlas. Không nhấp nháy tooltip khi con trỏ đi qua đường nối giữa các mesh của cùng ID. |
| Hai lớp chồng nhau trước camera | Mô đang thấy phía trước thắng. Tắt lớp phía trước hoặc cắt khuất giao điểm thì chỉ mặt hiện hợp lệ được chọn. Mesh phụ và mesh ẩn không nhận tên. Bề mặt giải phẫu kín chưa ánh xạ không làm lộ nhãn cơ quan phía sau. |
| Rotate, zoom, pan, resize, đổi hướng màn hình và reset khi chuột đứng yên | Tooltip tắt trong thao tác camera, sau đó phản ánh hit mới. Kiểm tra cả khi canvas nằm lệch trên trang hoặc trang đang cuộn. Tooltip tránh hình và không tràn mép. ID đã chọn vẫn giữ. |
| Ẩn lớp vừa chọn, chuyển hệ và đổi model nhanh | Bỏ tooltip và viền của hình học cũ. Bảng giữ ID và trạng thái phù hợp, hoặc về trạng thái chọn cấu trúc khi ID không còn thuộc ngữ cảnh. Tải xong muộn không ghi đè model hiện hành. |
| Phát, tạm dừng, về đầu và đổi góc khi đang phát | Hit và viền bám đúng pose đang hiển thị. Rê đứng yên khi cơ quan đi qua tia đổi hoặc tắt tooltip. Reset giữ trạng thái phát. |
| Chạm Tim rồi Phổi trái, chạm lại, kéo một ngón hoặc chụm | Chạm ngắn xem nhanh đúng ID. Chạm lại ẩn. Cử chỉ camera giữ điều khiển riêng. Danh sách mở được thông tin tương đương. |
| WebGL lỗi, dữ liệu thiếu, chọn bằng bàn phím và giảm chuyển động | Thông tin, đường thay thế và trạng thái khôi phục đúng như đặc tả. Chỉ lựa chọn có chủ đích mới cập nhật nội dung cho trình đọc màn hình. |

Hình minh họa Figma được đối chiếu với các tia mẫu trên GLB. Ở góc trước, tia của Tim chạm `Right ventricle` và tia của Phổi trái chạm `Superior lobe of left lung`. Ở góc nghiêng, tia minh họa vẫn chạm thùy trên phổi trái. Khi bật xương và nội tạng, tia minh họa chạm `Body of sternum` trước `Right ventricle`. Các vị trí này dùng để kiểm tra ảnh kết xuất. Figma thể hiện trạng thái và luồng thành phần. Kiểm thử liên tục về độ sâu, pose và cử chỉ cần chạy trên viewer Three.js khi triển khai. [Bảng trạng thái Figma](https://www.figma.com/design/jzAM858NL0lg4GnAU2SP64/AnatomAR?node-id=70-1020).
