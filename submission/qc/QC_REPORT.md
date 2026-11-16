# Báo cáo QC — nhóm 101–102

**Bản dự thảo báo cáo học tập và thực hành Day 07, cập nhật 2026-11-16.** Trình bày theo [QC_REPORT_TEMPLATE.md](../../docs/QC_REPORT_TEMPLATE.md). Nội dung phân tích dựa trên các tài liệu hiện có; kết quả thực hành chỉ được ghi khi có nhãn, số liệu và phiếu kiểm tương ứng. Hai thành viên cần tự đối chiếu và hoàn thiện bản nộp.

## 1. Mục đích, dữ liệu và phiên bản

- Mục đích và giới hạn sử dụng: xây dựng quy tắc nhất quán cho bài toán phát hiện người và phương tiện bằng bounding box 2D; thực hành gán độc lập, đo đồng thuận, xử lý bất đồng và đánh giá chất lượng nhãn. Bộ 40 ảnh có nhiều ca biên; kết quả thực hành không đủ để kết luận mô hình an toàn khi triển khai giao thông thực tế.
- Nguồn và phép sử dụng dữ liệu: 40 ảnh `img_001.jpg`–`img_040.jpg` trong `data/images/`, nguồn Wikimedia Commons và giấy phép theo từng dòng của `data/ATTRIBUTION.csv`. Khi chia sẻ phải giữ ghi công và điều kiện giấy phép; không đổi tên hoặc thêm bớt ảnh.
- Manifest và checksum nhãn cuối: chưa có `batch_manifest.json` hoặc nhãn cuối; chưa có checksum nhãn để báo cáo.
- Guideline và taxonomy khi gán / khi bàn giao: guideline và taxonomy đã khóa `v1.0` theo xác nhận chung do người dùng cung cấp ngày ghi nhận 2026-11-16 cho nội dung bản r1. Chưa có nhãn sau gán hoặc phiên bản bàn giao sau calibration.

### Nội dung học tập và phân tích ca ảnh

Vấn đề của guideline v0 là nhiều diễn giải chưa đủ cụ thể để hai người xử lý cùng một ảnh giống nhau. Cần phân biệt định nghĩa lớp với thuộc tính, vật ngoài taxonomy với vật cần review, và phần nhìn thấy với phần được suy đoán.

| Ca ảnh | Vấn đề cần giải quyết | Cách xử lý trong bản đề xuất chung | Lập luận / bài học áp dụng |
|---|---|---|---|
| img_002 | Carrier chở nhiều xe; khung che xe con; người cạnh đuôi xe | R-06/R-08: xe chở và từng xe được chở xét riêng; không bỏ người nhìn thấy; box bao phần thấy của một instance | Vị trí trên phương tiện khác không làm mất tính riêng biệt của từng xe. Không vẽ bù xe khuất hoặc box riêng cho thanh khung. |
| img_005 và img_026 | Người lái, hành khách và xe máy chồng lấp; tranh nền ở img_026 | R-06: tách person với motorcycle, cho phép box chồng nhau; R-09 loại hình trong tranh | Cần thử một quy tắc trên ảnh thứ hai để kiểm tra tính nhất quán, không gộp người vào xe. |
| img_017, img_027, img_038 | Tượng người, tượng pickup và xe đồ chơi | R-09: loại khỏi lớp người/phương tiện thật | Hình dáng giống một class chưa đủ để gán class đó; cần xét bản chất vật thể. |
| img_018 và img_020 | Chân dung in, xe sau rào và xe trong gương | R-03/R-09: rào gây che khuất; hình in/phản chiếu không sinh object mục tiêu | Che khuất của vật thật khác với hình mô phỏng hoặc phản chiếu; không dùng ignore để né quyết định ngoài scope. |
| img_005, img_009, img_037 | Van, minibus và pickup gắn canopy dễ nhầm | R-01/R-02: đề xuất van theo thân kín liền, pickup theo cabin/thùng riêng; minibus img_009 ngoài phạm vi | Phân loại theo cấu tạo nhìn thấy, không dựa màu xe hoặc hàng đang chở. Nhóm còn cần xác nhận các mẫu đối chứng. |
| img_021 và img_030 | Nhiều người/xe che nhau, khó tách cá thể | R-07: tách vật rõ, đo chiều cao trên ảnh gốc; chỉ ignore vùng ngoại lệ theo điều kiện chung | Mật độ cao không cho phép gộp toàn cụm thành một object hoặc phủ ignore lên vật đủ điều kiện. |
| img_024, img_028, img_040 | Xe vàng chưa rõ bản chất, ngựa ngoài taxonomy, phần xe sát biên chưa đủ nhận dạng | R-05: phân biệt box ứng viên cần review với vấn đề chưa vẽ được box; không suy đoán phần không thấy | Cần ghi đúng giới hạn quan sát. Ba ca còn cần thành viên đối chiếu; chưa có quyết định ảnh cuối cùng của nhóm. |

Bảng che khuất đề xuất chung là `0`: không che; `1`: che trên 0% và dưới 50%; `2`: che từ 50% trở lên; `3`: không xác định được mức che. Tỷ lệ chỉ tính phần đối tượng trong khung bị vật khác che, không tính phần ngoài khung do truncation. Hai người đã đồng ý quy tắc này theo xác nhận chung của người dùng; chưa phải kết quả calibration trên nhãn.

## 2. Phân công và đồng thuận trước calibration

- Lượt hoàn thành / được giao: chưa có COCO để xác nhận lượt gán hoàn thành; tổng phân công là **80 lượt** trên 40 ảnh, mỗi ảnh giao cả 101 và 102, mỗi người 40 ảnh. Phân công không đồng nghĩa đã gán xong.
- Số cặp box ghép, IoU TB, đồng thuận lớp và mẫu số: N/A — chưa có hai bộ nhãn độc lập hợp lệ để ghép cặp và tính IAA.
- Box chưa ghép, loại do ignore, bất đồng vùng ignore: chưa có kết quả so sánh nhãn; chưa thể xác định số lượng.
- Ca hai người có thể cùng sai sau khi đối chiếu tham chiếu: chưa thực hiện đối chiếu nhãn với ca tham chiếu. Rủi ro cần kiểm là cùng bỏ người trên xe, cùng gán tượng thành vật thật hoặc cùng phủ ignore quá rộng; đây là tình huống cần kiểm, không phải lỗi đã được xác nhận.

Hai guideline cá nhân đã có nội dung để đối chiếu. Khác biệt nổi bật là mốc che nhẹ/nhiều và nghĩa mức 3; bản chung đã chốt phạm vi van/minibus, sidecar và điều kiện ignore đám đông. Bản nhóm dùng bảng che 50% nêu ở mục 1; người dùng đã xác nhận cả hai đồng ý toàn bộ bản chung, được khóa thành v1.0. Việc hai bản cá nhân cùng đề xuất pickup→truck hoặc tách người–xe chưa thay thế việc khóa guideline nhóm.

Phần chuẩn bị Pha 3 đã có Project 2 và hai Task riêng:101 dùng Task 15/Job 10,102 dùng Task 16/Job 11. Mỗi Task40 frame khớp phân công; tại thời điểm kiểm tra chưa có box/track/tag. Chưa có lượt gán hoàn tất hoặcCOCO thật để tính đồng thuận.

**Bài học về đồng thuận:** IAA chỉ tính IoU/lớp trên các cặp ghép được. Ngay cả khi đồng thuận cao, hai người vẫn có thể cùng bỏ sót vật hoặc cùng hiểu sai quy tắc. Khi có nhãn thật cần đọc cả box chưa ghép, bất đồng ignore và ca tham chiếu.

## 3. Calibration và kiểm lại

- Ca đã xử lý, rule ID, bản sửa và người xác nhận: chưa có ca calibration thực tế hoặc `calibration_decisions.csv`; các Rule ID ở mục 1 là quy tắc đề xuất trước gán nhãn.
- Tác động v1.1 lên nhãn và ảnh: chưa có guideline v1.1 hoặc nhãn sau calibration để đánh giá.
- Tham chiếu bằng chứng khi Rework: chưa có vòng QC, quyết định Rework hay bản sửa được kiểm lại.

**Nguyên tắc thực hành cần áp dụng:** sau khi đủ nhãn độc lập và có bất đồng, mỗi ca cần quyết định, lý do, Rule ID, phiên bản, người chốt, dấu vết sửa và kết quả kiểm lại. Nếu thay đổi nghĩa quy tắc thì phải xác định phạm vi cả lô; không chỉ sửa ảnh ví dụ rồi bỏ qua các ảnh tương tự. Phần này sẽ bổ sung trải nghiệm và kết quả thật sau calibration.

## 4. Kết quả duyệt

- Vòng QC: chưa thực hiện; chưa có số vòng QC thực tế.
- Người review và ngày: chưa được phân công/xác nhận; chưa có ngày duyệt.
- Đã duyệt / cả lô: chưa có phiếu QC để xác nhận số ảnh đã duyệt; phạm vi cần duyệt là toàn bộ 40 ảnh sau khi có nhãn cuối.
- Ảnh lỗi / ảnh đã duyệt: N/A — chưa có mẫu số ảnh đã duyệt; không ghi 0% khi chưa review.
- Annotation đối tượng hiện có bị lỗi / annotation đối tượng đã duyệt: N/A — chưa có nhãn cuối và mẫu số annotation đã duyệt.
- Vật bỏ sót, ảnh và vùng: chưa có lỗi bỏ sót được reviewer xác nhận trên nhãn. Các rủi ro trong phân tích ca ảnh chưa phải kết quả duyệt.
- Ca khó / phần còn lại, lỗi lặp và ví dụ: img_024, img_028, img_040 còn cần kiểm lại quyết định quan sát; chưa có phiếu để xác nhận lỗi lặp.
- Một lỗi máy chặn được và một lỗi cần người đọc ảnh: validator có thể phát hiện cấu trúc COCO/geometry/class không hợp lệ; người đọc ảnh mới xác định được box trên tượng, bỏ sót người hoặc box không ôm sát. Đây là phân biệt chức năng kiểm tra, chưa phải hai lỗi đã phát hiện trong nhãn nhóm.

**Bài học về đánh giá chất lượng:** tỉ lệ lỗi theo ảnh và theo đối tượng có mẫu số khác nhau. Nếu duyệt đủ 40 ảnh, một ảnh lỗi là 1/40 = 2.5%, vượt ngưỡng 2%. Các con số này minh họa cách tính, không phải số liệu QC của nhóm. Chỉ duyệt mẫu hoặc chỉ kiểm định dạng chưa đủ điều kiện Release.

## 5. Quyết định bàn giao

- Quyết định: chưa có quyết định Release/Hold/Rework được người review xác nhận.
- Lý do, người nhận và phạm vi sử dụng: hồ sơ hiện mới có guideline cá nhân, đề xuất nhóm và phân công; chưa đủ bằng chứng bàn giao nhãn. Bản dự thảo dành cho 101 và 102 đọc, bổ sung và xác nhận, chưa phải báo cáo nghiệm thu nhãn.
- Nếu còn việc: 101 và 102 hoàn thiện ghi chú cá nhân, kiểm Project/Task dùng đúng cấu hình v1.0 và đủ 40 frame/người; tiếp đó gán độc lập, export/validate COCO, đo IAA, calibration và QC toàn lô. Nhóm cần phân công người chốt và người review bằng mã thành viên.
- Kiểm ngược từ báo cáo tới ảnh, rule và nhãn: ví dụ img_002 → R-06/R-08 trong guideline chung → ảnh gốc `data/images/img_002.jpg`; chưa có annotation để truy tiếp tới object ID. Khi có nhãn và quyết định thật, bổ sung mã ca, object ID, bản sửa và người kiểm lại.

Tài liệu liên quan: [guideline chung](../guidelines/guideline_v1.0_agreed.md), [phân công](assignment.csv), [ghi chú 101](../individual_notes/101.md), [ghi chú 102](../individual_notes/102.md). Báo cáo cần tiếp tục cập nhật bằng kết quả thực hành; không dùng số liệu minh họa trong tài liệu lớp thay cho số liệu của nhóm.
