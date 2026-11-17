# Báo cáo QC — nhóm 101–102

Tôi phụ trách mã 101 và cập nhật hồ sơ ngày 2026-11-17 theo mẫu báo cáo của lab. Nhóm có 40 ảnh và hai COCO cá nhân. Tôi dùng ChatGPT/Codex hỗ trợ review, lập quyết định xử lý ca và tạo hồ sơ bàn giao. Nguồn hai bộ nhãn được khai báo trong provenance; xác nhận calibration chung và nghiệm thu độc lập còn chờ.

## 1. Mục đích, dữ liệu và phiên bản

- Mục đích và giới hạn sử dụng: tôi thực hành đặc tả và QC box 2D trên 40 ảnh Day07. Bộ bàn giao hiện ở trạng thái Hold, phục vụ kiểm lại và tiếp tục xử lý các cờ. Chất lượng được mô tả trong phạm vi kiểm có AI hỗ trợ của hai vòng đã ghi.
- Nguồn và phép sử dụng dữ liệu: data/images/img_001.jpg–img_040.jpg; ghi công và giấy phép trong data/ATTRIBUTION.csv. Bản 101 được review từ backup đã review của 102, nguồn đề xuất YOLO11n+SAM3 được khai báo.
- Manifest và checksum nhãn cuối: batch_manifest.json ghi phiên bản, nguồn ảnh, checksum các đầu vào và nhãn bàn giao labels_calibrated.json. SHA-256 nhãn hiện tại là `0d4b21be50eb1ebe0eb01c0b0de65e34f75d66d46cbb546bc88c9a088207cbb6`. File CSV tương ứng nằm tại labels_calibrated.csv.
- Guideline và taxonomy khi gán / khi bàn giao: nhãn cá nhân và phép so sánh dùng guideline/taxonomy v1.0. Bản bàn giao dùng guideline v1.1 với thay đổi editorial trong submission/guideline_change.json, giữ nghĩa quy tắc và taxonomy v1.0. Phần xác nhận v1.1 của nhóm còn chờ.

## 2. Phân công và đồng thuận trước calibration

- Lượt hoàn thành / được giao: hai COCO có đủ 80/80 lượt ảnh theo assignment.csv. Điều kiện hai lượt vẽ thủ công độc lập chưa được chứng minh vì hai bản cùng nguồn pre-label và review.
- Số cặp box ghép, IoU TB, đồng thuận lớp và mẫu số: iaa_summary.json/.md ghi 342 cặp; IoU trung bình 1.0000, cùng lớp 336/342=98.25%. Tôi giữ số đo trước calibration; các sửa sau đó nằm trong bộ nhãn bàn giao riêng.
- Box chưa ghép, loại do ignore, bất đồng vùng ignore: phía101/102 có 0/8 box chưa ghép,0 đối tượng bỏ qua do ignore; hai vùng ignore mỗi bản ghép được. Ghép1–1 theo IoU≥0.5, không phân biệt lớp. Cùng nguồn và box trùng tọa độ ảnh hưởng cách diễn giải kết quả.
- Ca hai người có thể cùng sai sau khi đối chiếu tham chiếu: trong vòng 1, tôi phát hiện cùng giữ các box mảnh của sedan ảnh 034 và cabin pickup ảnh 001; các ca này cần áp dụng R-06 một vật/một box. Tôi đối chiếu ảnh gốc, chưa có bộ tham chiếu độc lập do coach xác nhận.

## 3. Calibration và kiểm lại

- Ca đã xử lý, rule ID, bản sửa và người xác nhận: calibration_decisions.csv có 609 dòng gồm 604 ca so sánh và 5 thao tác sửa sau QC. Mỗi dòng có quyết định xử lý, rule, phạm vi, nguồn và cách kiểm. Cột người chốt ghi rõ Codex hỗ trợ101, chờ nhóm xác nhận; không ghi đã họp hoặc được102 nghiệm thu. calibration_resolution_status.json ghi trạng thái từng ca. Nhật ký bổ sung tại calibration_corrections_101.json.
- Tác động v1.1 lên nhãn và ảnh: giữ quy tắc v1.0; bổ sung ghi chú truy vết và ví dụ áp dụng. Sửa trên 35 ảnh thuộc phạm vi bị cờ theo phiên bản input được manifest ghi nhận. So với COCO101 trước calibration, bổ sung hai người lái tuk-tuk ảnh 004, sửa pickup ảnh 012, loại box cabin/box mảnh trùng và khôi phục người bị bỏ sót ảnh 001. Nhãn bàn giao giữ40 ảnh,344 annotation gồm342 đối tượng và2 ignore.
- Tham chiếu bằng chứng khi Rework: reviews/round-01/ giữ nhãn 346 annotation và phiếu phát hiện ba box thừa, một người bỏ sót trên hai ảnh 001/034. Tôi sửa và lưu bộ nhãn 344 annotation, mở reviews/round-02/ rồi kiểm lại hai ảnh đã thay đổi; các ảnh khác giữ nguyên từ vòng 1. File input có tên phiên bản được ghi trong batch_manifest.json.

## 4. Kết quả duyệt

- Vòng QC: 2
- Người review và ngày: mã 101 với ChatGPT/Codex hỗ trợ ngày 2026-11-17. REVIEW_SCOPE.md trong từng vòng mô tả cách xem sheet, ảnh gốc và overlay. Nhóm chưa có reviewer độc lập xác nhận toàn bộ instance.
- Đã duyệt / cả lô:40/40 ảnh trong lượt kiểm trực quan có AI hỗ trợ; vòng 2 kiểm lại hai ảnh sửa và kế thừa 38 ảnh giữ nguyên từ vòng 1. Các cờ cần xác nhận chi tiết vẫn giữ.
- Ảnh lỗi / ảnh đã duyệt: vòng 1 có 2/40=5.0%; vòng 2 chưa phát hiện lỗi bổ sung trong phạm vi kiểm,0/40=0.0%. Đây là số liệu phiếu, cần đọc cùng phạm vi kiểm và trạng thái chưa nghiệm thu độc lập.
- Annotation đối tượng hiện có bị lỗi / annotation đối tượng đã duyệt: vòng 1 có 3/344=0.87%, ghi riêng1 vật bỏ sót; vòng 2 ghi 0/342=0.0%,0 vật bỏ sót mới. Còn289 box can_review=true và 127 mức che3 trong nhãn bàn giao.
- Vật bỏ sót, ảnh và vùng: vòng 1 ghi người nữ ngồi sau người ngoài cùng trái ở ảnh 001, đầu khoảngx126–198/y114–240; đã thêm box đề xuất và giữ cờ để kiểm biên. Ảnh040 còn issue phần xe/gương sát dưới, tiếp tục chờ xác định.
- Ca khó / phần còn lại, lỗi lặp và ví dụ: vòng 1 có lỗi thừa lặp ở cabin pickup và hai box mảnh sedan. Vòng 2 nhóm ca khó có0/35 lỗi mới được phát hiện, nhóm còn lại0/5. Các ảnh đông021/030/032, xe vàng024 và các cờ chưa chắc vẫn cần xác nhận chi tiết.
- Một lỗi máy chặn được và một lỗi cần người đọc ảnh: validator kiểm được box vượt biên/enum sai; ảnh 001 cho thấy cabin và thùng xe thuộc cùng pickup, ảnh 034 cho thấy box đầu/đuôi thuộc một sedan. Nhận diện cùng instance cần đọc ảnh, vượt ngoài kiểm cấu trúc.

## 5. Quyết định bàn giao

- Quyết định: Hold
- Lý do, người nhận và phạm vi sử dụng: tôi bàn giao bộ file có đủ phiên bản, nhãn, manifest và hai vòng QC để coach/nhóm kiểm lại. Giữ Hold vì còn 609 dòng chờ xác nhận nhóm,289 cờ review và điều kiện gán độc lập chưa được chứng minh. Kết quả0 lỗi mới trong phiếu vòng 2 chưa giải quyết các điều kiện này.
- Nếu còn việc: nhóm 101–102 xác nhận các quyết định, xử lý cờ và issue, kiểm từng instance/vật bỏ sót; nếu sửa nhãn thì tạo input phiên bản mới, chạy build_final.py và mở vòng 3. Reviewer cuối xác nhận trước Release.
- Kiểm ngược từ báo cáo tới ảnh, rule và nhãn: img_034→R-06→phiếu vòng 1 ID 301/304→Q002/Q003 trong calibration_decisions.csv→calibration_corrections_101.json→snapshot và phiếu vòng 2; img_001→R-06→box cabin và người bỏ sót→Q001/Q004/Q005→vòng 2. Manifest khóa checksum của bộ nhãn hiện tại.
