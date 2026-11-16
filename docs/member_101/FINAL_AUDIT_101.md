# Final audit — Member 101 — Day 07

> Phụ lục kiểm tra tài liệu tại thời điểm audit, giữ để tra cứu lịch sử. Đây không phải báo cáo học tập hoặc bằng chứng thực hành của 101. Báo cáo theo mẫu lab ở [submission/qc/QC_REPORT.md](../../submission/qc/QC_REPORT.md); ghi chú của người học ở [101.md](../../submission/individual_notes/101.md).

- Ngày audit: **2026-11-16** (Asia/Saigon).
- Phạm vi: bốn tài liệu riêng 101, 40 ảnh assignment và kiểm tra kỹ thuật liên quan. AI thực hiện audit và sửa tài liệu; **chưa có xác nhận của 101**, không phải review nhãn đã vẽ.
- Đã đọc: `README.md`, `GUIDE.md`, `RULES.md`, `RUBRIC.md`, `SUBMISSION.md`, template guideline, guideline v0, taxonomy/schema; đối chiếu thêm `docs/QC_CHEATSHEET.md`, `docs/INDIVIDUAL_NOTE_TEMPLATE.md` và logic sinh cấu hình CVAT.
- Chỉ sửa bốn tài liệu 101 và thêm báo cáo này. Không sửa tài liệu riêng 102, taxonomy, script/test hay nhãn. Các thay đổi có sẵn trước audit (gồm `TEAM.md` và các file chưa được Git theo dõi) được giữ nguyên.
- **Kết quả:** READY FOR 101 REVIEW về bản tài liệu chuẩn bị; **NOT READY cho gói lab đầy đủ**.

## A. Requirement Compliance

Trạng thái đánh giá bằng chứng hiện có sau sửa. PASS cho nội dung đề xuất không có nghĩa là 101 đã tự quyết định/gửi riêng hoặc nhóm đã khóa quy tắc. PARTIAL là có bằng chứng một phần/còn xác nhận; FAIL là thiếu sản phẩm bắt buộc, không phải kết luận về năng lực người làm.

| Yêu cầu | File bằng chứng | PASS/PARTIAL/FAIL | Nhận xét |
|---|---|---|---|
| A01 — Xem đủ 40 ảnh, mô tả có căn cứ | `IMAGE_ANALYSIS.md`, mục B | PASS | Đã mở riêng 40 file gốc; sửa mô tả sai/bỏ sót; ba ảnh còn bất định được ghi PARTIAL ở B, không đoán. |
| A02 — Mục tiêu và cấu trúc guideline | `submission/guidelines/individual/guideline_101.md` mục 1–6 | PASS | Nêu mục tiêu detection 2D, phạm vi, lớp/thuộc tính, box, ca khó, QC, phiên bản; có tác hại của gộp vật/suy đoán box. |
| A03 — Ca thật có ID và lập luận | Guideline mục 4; `submission/individual_notes/101.md` mục 2 | PASS | Carrier, rider/passenger, tượng, tranh nền, phản chiếu, pickup, thiếu class đều truy được ảnh và lý do. |
| A04 — Định nghĩa, inclusion/exclusion, ví dụ/phản ví dụ | Guideline mục 2.1–2.2 | PASS | Đủ sáu class; tách object với ignore; không tự tạo bus/bicycle/tuk-tuk. Mapping pickup là đề xuất. |
| A05 — Mức thuộc tính rõ và giữ nghĩa v0 | Guideline mục 2.3 | PASS | Giữ giá trị taxonomy; sửa mức 3 về không rõ; 0%, trên 0–25%, trên 25% không chồng biên. Mốc 25% cần nhóm chốt. |
| A06 — Box, che/cắt mép, vật nhiều phần, ego | Guideline I101-01–10 | PASS | Box phần thấy, người/xe riêng; carrier/sidecar có quyết định đề xuất; thêm ego, không dựng phần khuất. |
| A07 — `can_review` và vấn đề cấp ảnh | Guideline mục 2.3, I101-08–09 | PASS | Box ứng viên hợp lệ mới tick; thiếu class thì ghi issue; minibus chỉ dùng van khi scope cho phép. |
| A08 — Vật nhỏ/đám đông/ignore | Guideline I101-06; phân tích `img_027` | PASS | Giữ <20 px; không ignore thay class thiếu/tượng; cụm không tách cần rule nhóm hoặc issue. |
| A09 — QC có quy trình và ngưỡng đúng | Guideline mục 5 | PASS | Đủ IAA/matched-pair, hai mẫu số lỗi, kiểm toàn lô, lỗi lặp, Hold/Rework/Release và trách nhiệm chốt/kiểm lại. |
| A10 — Ghi chú nêu ca mơ hồ, lý do và giới hạn bằng chứng | `submission/individual_notes/101.md` | PASS | Nêu các ca cụ thể và nguyên nhân; chưa biến kế hoạch calibration thành kết quả; giảm phần checklist lặp. |
| A11 — Tự viết, tự kiểm và gửi riêng bản cá nhân | Ghi chú mục 6–7; `RULES.md`, `GUIDE.md` Pha 1 | PARTIAL | Công khai AI hỗ trợ soạn/phân tích/audit; chưa có bằng chứng Chi tự kiểm và gửi riêng. Không thể xác nhận yêu cầu độc lập chỉ từ văn bản. |
| A12 — Assignment và ảnh đúng phạm vi | `submission/qc/assignment.csv`, `assignments/101.txt`, `work/101/images/` | PASS | 40 tên duy nhất; 40 ảnh; hash trùng nguồn. Assignment hiện có 2 người/ảnh là phân công, chưa phải hoàn tất 80 lượt. |
| A13 — Taxonomy/schema/CVAT và ngưỡng cố định | Taxonomy/schema, `cvat/labels_generated.json` | PASS | Schema và kiểm nghĩa nội bộ đạt; class, select/checkbox, default khớp; rules bằng HEAD. Version vẫn v0, chưa khóa v1.0. |
| A14 — Nhãn cá nhân thật, hợp lệ theo v1.0 | `submission/labels/101.json` chưa có | FAIL | Chưa có COCO để kiểm box, thuộc tính, ảnh trống hoặc độ phủ gán thật; chưa chạy validator trên file thiếu. |
| A15 — Guideline/taxonomy nhóm v1.0 đã khóa | `submission/guidelines/guideline_v1.0_agreed.md` chưa có; taxonomy v0 | FAIL | Chưa có quyết định nhóm; không thể coi bản 101 là bản agreed. |
| A16 — IAA/calibration và bản cuối có truy vết | `submission/qc/`, guideline v1.1/nhãn cuối chưa có | FAIL | Chưa có dữ liệu thực tế; không tạo quyết định/số đo thay thế. |
| A17 — QC review/báo cáo và gói bàn giao đầy đủ | `submission/qc/reviews/`, `QC_REPORT.md` chưa có; mục E | FAIL | Checker dừng ở thiếu nhãn; chưa đủ điều kiện xét Release hoặc quyết định QC thực tế. |
| A18 — Ghi chú hoàn chỉnh theo các pha | Ghi chú mục 7; mẫu ghi chú lab | PARTIAL | Đã có ô trạng thái cho Pha 2–5, nhưng chưa có bất đồng nhóm, số box/cờ review, ca lệch thật để phản ánh. Không điền số giả. |
| A19 — Kiểm tra kỹ thuật toàn bộ sạch | Mục E | PARTIAL | 19/20 test đạt; 1 ERROR quyền symlink Windows. Compile/schema/CVAT/kiểm cấu trúc đạt. |
| A20 — Bàn giao riêng tư, xác nhận và tái lập trọn lab | `SUBMISSION.md`, ghi chú/tiến độ 101 | PARTIAL | Đường dẫn dùng mã, nguồn ảnh giữ nguyên; chưa có bằng chứng kênh gửi riêng, gói hoàn chỉnh, reviewer ngoài nhóm lần theo ca hoặc quyền CVAT. |

**Tổng A: 20 tiêu chí = 12 PASS / 4 PARTIAL / 4 FAIL.** Không cộng số ảnh hoặc các hàng rubric vào tổng này.

## B. Image Verification

Đã mở riêng từng ảnh bằng công cụ xem ảnh tại đường dẫn `work/101/images/img_XXX.jpg`, đủ bốn lượt 001–010, 011–020, 021–030, 031–040. Không dùng việc có dòng trong bảng để kết luận PASS. Sau sửa, đối chiếu lại mô tả với quan sát này.

PASS: mô tả ứng viên/quy tắc phù hợp những gì nhìn thấy, có thể dùng để 101 rà soát. Không xác nhận số box cuối, tọa độ, phần trăm che hay pixel của từng vật nhỏ vì chưa có annotation/đo box. PARTIAL: một đặc điểm ảnh ảnh hưởng quyết định vẫn chưa xác định. Các ID `Fxx` trỏ tới mục D.

| Image ID | Đã đối chiếu trực quan | Kết quả | Lỗi phát hiện | Đã sửa |
|---|---|---|---|---|
| img_001.jpg | Có — gốc | PASS | Không thấy lỗi mô tả chính: pickup, người thật; xe cắt phải/dưới, người bị che. | Không cần |
| img_002.jpg | Có — gốc, ca trọng tâm | PASS | F01: thiếu người đứng bên phải đuôi carrier. Xe con hai tầng và khung chở đúng. | Có — thêm person riêng/occlusion |
| img_003.jpg | Có — gốc | PASS | F02: ô tô nền chưa được nêu thành ứng viên rõ. | Có — thêm car, giữ xe đạp ngoài class |
| img_004.jpg | Có — gốc | PASS | Hai tuk-tuk, người thật; không ép xe ba bánh vào motorcycle/truck. | Không cần |
| img_005.jpg | Có — gốc, ca trọng tâm | PASS | F03: thiếu ô tô bạc sát mép trái phía sau van; tách người/xe và người cắt dưới hợp lý. | Có — thêm car |
| img_006.jpg | Có — gốc | PASS | Xe máy, người, ô tô trái và xe đạp phải khớp; không lẫn phương tiện. | Không cần |
| img_007.jpg | Có — gốc | PASS | F04: pickup trắng và “xe con trắng” bị kể như hai xe. | Có — hai xe tải ứng viên, không bịa xe thứ ba |
| img_008.jpg | Có — gốc | PASS | F05: chưa nêu pickup/khoang cao và tuk-tuk giữa nền. | Có — ghi ứng viên/ràng buộc class, không đoán xe xa |
| img_009.jpg | Có — gốc | PASS | Minibus và người/xe nền khớp; van là quyết định scope cần nhóm chốt. | Giữ ca thiếu class; F23 làm rõ can_review |
| img_010.jpg | Có — gốc | PASS | Người và xe máy quanh xe hàng đúng; hàng/xe đẩy ngoài taxonomy. | Không cần |
| img_011.jpg | Có — gốc | PASS | F06: bỏ xe trắng sọc xanh nền phải sau tượng. | Có — thêm ứng viên car, bị tượng che |
| img_012.jpg | Có — gốc | PASS | F07: thiếu xe thùng phía trước; gọi xe bạc là sedan trong guideline sai kiểu thân. | Có — thêm truck, đổi SUV, cắt biên pickup |
| img_013.jpg | Có — gốc | PASS | Người đi bộ, xe nền và nguy cơ nhầm đèn/phản chiếu khớp. | Không cần |
| img_014.jpg | Có — gốc | PASS | Hai người rõ và người/xe nhòe khớp; không dựng box cả vệt blur. | Không cần |
| img_015.jpg | Có — gốc | PASS | Ô tô thật và phản chiếu, xe cắt hai bên khớp. | Không cần |
| img_016.jpg | Có — gốc | PASS | F08: thiếu pickup nền trái; truncation của người tiền cảnh chưa rõ trong mô tả. | Có — thêm truck, cắt biên từng instance |
| img_017.jpg | Có — gốc, ca trọng tâm | PASS | Tượng cưỡi ngựa, cone trên đầu đúng; không có person mục tiêu ở tượng. | Không cần |
| img_018.jpg | Có — gốc | PASS | F09: chỉ nêu car, thiếu pickup đỏ/xe khoang cao sau hàng rào. | Có — thêm truck ứng viên, tách hình in |
| img_019.jpg | Có — gốc | PASS | Xe diễu hành có bánh/thân/đèn, người lái và đám đông; mascot chưa thấy cơ thể người thật. Không suy ra người ẩn trong đạo cụ. | Không cần; giữ quy tắc chỉ box người thật thấy được |
| img_020.jpg | Có — gốc | PASS | F10: giải thích phản chiếu như thể vật không có vị trí vật lý; thiếu rule ego ở guideline. | Có — giải thích lựa chọn scope; F23 thêm ego |
| img_021.jpg | Có — gốc | PASS | Dòng xe máy, người và ô tô khớp; không gộp đám đông thành person. | Không cần |
| img_022.jpg | Có — gốc | PASS | F11: nhắc cây che xe chính dù không thấy che trực tiếp; dẫn rule carrier cho sidecar chưa phù hợp. | Có — bỏ gợi ý che bởi cây, sửa dẫn rule |
| img_023.jpg | Có — gốc | PASS | Sedan đen, người đạp xích lô, xe máy và người dọc đường khớp. | Không cần |
| img_024.jpg | Có — gốc | PARTIAL | Xe vàng nhỏ trên nóc có bánh/thân xe nhưng chưa đủ căn cứ phân biệt xe thật/mô hình; ảnh gốc không giải quyết chắc bản chất vật. | Giữ bất định trung thực, không tự chốt car |
| img_025.jpg | Có — gốc | PASS | F12: pickup xanh và cấu phần thùng bên xe máy chưa được nêu rõ. | Có — truck ứng viên, liên hệ đề xuất sidecar |
| img_026.jpg | Có — gốc, ca trọng tâm | PASS | F13: thiếu truncation xe máy ở biên dưới. Hai người và tranh tường được nhận đúng. | Có — bổ sung cắt dưới trong phân tích/guideline |
| img_027.jpg | Có — gốc | PASS | F14: câu ngoại lệ ignore cho tượng làm lệch quy tắc chung. | Có — không ignore thay class cho tượng |
| img_028.jpg | Có — gốc, ca trọng tâm | PARTIAL | F15: khẳng định ngựa che pickup quá chắc, bỏ tình huống pickup che xe đỏ. Bản chất thật/mô hình của ngựa chưa kết luận; dù loại nào cũng ngoài class. | Có — sửa khẳng định; mức che chính xác chờ 101, không đoán |
| img_029.jpg | Có — gốc | PASS | Người, xe máy, xe đạp và thanh dài khớp; không bao hàng dài vào xe. | Không cần |
| img_030.jpg | Có — gốc | PASS | Bãi xe dày, người ở lối đi và poster nền khớp; quy tắc không gộp cả bãi hợp lý. | Không cần |
| img_031.jpg | Có — gốc | PASS | F16: bỏ xe máy/người lái làn trái; bus nhìn thấy rõ hơn mô tả cũ. | Có — thêm motorcycle/person, giữ bus ngoài v0 |
| img_032.jpg | Có — gốc | PASS | F17: xe thân kín nền chưa được nêu thành ứng viên. | Có — thêm van có điều kiện, không suy ra bus |
| img_033.jpg | Có — gốc | PASS | Mannequin, ảnh in và phản chiếu cửa kính; không có người thật nhìn trực tiếp rõ để box. | Không cần |
| img_034.jpg | Có — gốc | PASS | F18: thiếu người đi xe đạp ngay phải ô tô giữa nền. | Có — bổ sung person, xe đạp ngoài class |
| img_035.jpg | Có — gốc | PASS | F19: bỏ ô tô sáng giữa ảnh/bên phải. | Có — thêm car và occlusion |
| img_036.jpg | Có — gốc | PASS | F20: thiếu người lộ sau cabin; có hình người quảng cáo dễ nhầm. | Có — thêm person có điều kiện 20 px, loại hình in |
| img_037.jpg | Có — gốc | PASS | Pickup có nắp cao, bus và người đi bộ khớp; mapping pickup là đề xuất, bus thiếu class. | Không cần |
| img_038.jpg | Có — gốc | PASS | Mô hình xe và đồ chơi sau kính; không gán như xe/người thật. | Không cần |
| img_039.jpg | Có — gốc | PASS | Người đi bộ, xe máy, xe đạp, xe xa khớp; không suy động cơ từ người lái. | Không cần |
| img_040.jpg | Có — gốc, ca trọng tâm | PARTIAL | F21: khẳng định người đứng, thiếu tuk-tuk và gương/phần xe hai bánh ở dưới; mép taxi mô tả chưa chuẩn. Class/box xe tiền cảnh vẫn chưa đủ rõ. | Có — ghi bộ phận nhìn thấy, bỏ suy tư thế, giữ cần reviewer |

**Tổng B: 40/40 đã mở trực quan; 37 PASS / 3 PARTIAL / 0 FAIL sau sửa.** Không phải 37 ảnh đã QC nhãn; chưa có nhãn để thực hiện QC ấy.

## C. Guideline Quality

Không ước tính điểm coach hoặc cộng điểm toàn lab. Đánh giá nội dung hiện có tách khỏi quyền tác giả/xác nhận cá nhân.

| Tiêu chí rubric | Đánh giá thực chất | Giới hạn bằng chứng |
|---|---|---|
| Hạng mục 1 — 6 điểm ca thật/ID/lập luận | Nội dung có nền tảng tốt: carrier, nhiều người/xe, tượng, tranh, phản chiếu, thiếu class, pickup; mỗi ca có quyết định đề xuất và lý do. | Ba ca B còn bất định. Chi phải tự kiểm, chọn/chỉnh quyết định ban đầu và gửi riêng. Chưa xác nhận đạt 6 điểm. |
| Hạng mục 1 — 5 điểm định nghĩa/ví dụ/phản ví dụ/mức đo được | Đủ định nghĩa và inclusion/exclusion; ví dụ/phản ví dụ có ID; thuộc tính đúng enum/default, ngưỡng pixel/QC rõ. Sửa mức che 3 và biên 0%; mốc 25% ghi rõ đề xuất. | Chưa có annotation để kiểm mức che thực tế; mapping van/pickup và phạm vi các class cần nhóm chốt. |
| Hạng mục 1 — 4 điểm cấu trúc | Năm phần template hiện diện, cộng lịch sử/kết luận; I101-01–10 truy được, bảng Markdown đã kiểm. | Guideline dài nhưng cấu trúc tra cứu được; không gắn mã I101 thành quy tắc nhóm. |
| Hạng mục 2 — đặc tả, bất đồng, ca biên, phiên bản | Bản 101 cung cấp đầu vào về ngoài taxonomy, vật không thật, che/cắt mép, nhỏ/đông, ego. | Chưa có biên bản bất đồng/thống nhất; taxonomy v0 không đủ thay thế nhóm v1.0. Chưa chấm 20 điểm nhóm. |
| Hạng mục 3 — độ phủ, COCO, gán theo v1.0 | Assignment hợp lệ và ghi rõ quy trình độc lập/ca mơ hồ. | Không có COCO; không thể xác nhận đủ lượt/box/thuộc tính. |
| Hạng mục 4 — mẫu số, ca lệch/cùng sai, calibration, v1.1 | Giải thích matched-pairs, N/A và nguy cơ hai người cùng sai là đúng; có kế hoạch truy vết Rule ID, phiên bản, phạm vi. | Chưa có IAA/candidates/decisions/bản sửa thật. Không xem giải thích lý thuyết là bằng chứng đã làm calibration. |
| Hạng mục 5 — hai mẫu số, lỗi, quyết định, script/thị giác | Quy trình bổ sung đủ cả mẫu số ảnh/đối tượng, full-batch, lỗi lặp và ba quyết định; nêu script không thay kiểm mắt. | Chưa có review/QC report nên không có tỉ lệ lỗi hoặc quyết định QC được xác nhận. |
| Hạng mục 6 — tái lập/cá nhân/mã/bàn giao | Tài liệu có liên kết, mã 101, phạm vi và công khai AI; kiểm tra dữ liệu/kỹ thuật tại E. | Chưa hoàn chỉnh gói, bằng chứng tự làm/gửi riêng, reviewer ngoài nhóm và kênh nộp. |

**Ranh giới quy tắc:** bắt buộc là enum, rules cố định, độc lập/người thật vẽ box, không tạo số liệu và quy trình các pha. Đề xuất cá nhân gồm pickup→truck, một carrier/sidecar, scope loại vật không thật/phản chiếu/ego, mốc che 25%. Nhóm phải chốt các đề xuất trước annotation; quyết định đổi nghĩa ở calibration phải theo phiên bản/phạm vi lô của lab. Không sửa guideline v0 gốc hoặc taxonomy để hợp thức hóa đề xuất cá nhân.

## D. Issues Found & Fixed

Một ID là một nhóm lỗi liên quan cùng ca/chủ đề, không đếm từng câu sửa thành lỗi riêng. 26 lỗi/nội dung cần sửa có căn cứ đã xử lý; bất định còn lại và hoạt động chưa diễn ra nằm ở F, không coi là đã giải quyết bằng cách sửa câu chữ.

| Issue ID | File | Vấn đề | Cách sửa | Trạng thái |
|---|---|---|---|---|
| F01 | IMAGE_ANALYSIS; notes 101 | img_002 thiếu người cạnh đuôi carrier | Thêm person riêng, occlusion theo phần thấy | FIXED |
| F02 | IMAGE_ANALYSIS | img_003 ô tô nền chưa thành ứng viên rõ | Nêu car bên trái/giữa nền | FIXED |
| F03 | IMAGE_ANALYSIS | img_005 thiếu ô tô bạc trái | Thêm car cạnh van | FIXED |
| F04 | IMAGE_ANALYSIS | img_007 kể trùng pickup trắng như xe con khác | Mô tả đúng hai xe, cabin/khoang riêng | FIXED |
| F05 | IMAGE_ANALYSIS | img_008 bỏ xe khoang cao/tuk-tuk nền | Thêm truck ứng viên và thiếu class, giữ điều kiện nhận dạng | FIXED |
| F06 | IMAGE_ANALYSIS | img_011 bỏ xe trắng sau tượng | Thêm car ứng viên, tượng che xe | FIXED |
| F07 | IMAGE_ANALYSIS; guideline 101 | img_012 bỏ xe thùng trước, gọi SUV là sedan | Thêm truck, sửa kiểu xe và truncation | FIXED |
| F08 | IMAGE_ANALYSIS | img_016 thiếu pickup và mô tả cắt mép chưa cụ thể | Thêm truck, xét cắt mép từng vật/người | FIXED |
| F09 | IMAGE_ANALYSIS | img_018 chỉ nêu car sau rào | Thêm pickup/ứng viên truck, cắt mép và occlusion | FIXED |
| F10 | IMAGE_ANALYSIS | img_020 lý do loại phản chiếu diễn giải sai bản chất vật | Đổi sang lựa chọn scope vật nhìn trực tiếp | FIXED |
| F11 | IMAGE_ANALYSIS; guideline 101 | img_022 gợi ý cây che không có chứng cứ, dẫn carrier cho sidecar | Nêu không thấy cây che xe chính, sửa dẫn rule | FIXED |
| F12 | IMAGE_ANALYSIS | img_025 thiếu pickup xanh/cấu phần thùng bên | Thêm truck ứng viên, áp dụng đề xuất sidecar | FIXED |
| F13 | IMAGE_ANALYSIS; guideline 101 | img_026 chưa nêu xe cắt biên dưới | Thêm truncated=yes cho xe máy, không suy sang người | FIXED |
| F14 | IMAGE_ANALYSIS | img_027 ngoại lệ ignore cho tượng lệch rule chung | Không dùng ignore thay class cho tượng | FIXED |
| F15 | IMAGE_ANALYSIS; guideline/notes 101 | img_028 khẳng định ngựa che pickup; bỏ xe đỏ bị che | Điều kiện hóa mức che pickup, bổ sung pickup che xe đỏ | FIXED — còn bất định ở F |
| F16 | IMAGE_ANALYSIS | img_031 bỏ motorcycle/người trái, bus mô tả quá chung | Nêu vật nhìn được, tách bus ngoài taxonomy | FIXED |
| F17 | IMAGE_ANALYSIS | img_032 xe thân kín nền chưa có hướng class | Bổ sung van ứng viên khi cấu tạo rõ | FIXED |
| F18 | IMAGE_ANALYSIS | img_034 thiếu người đi xe đạp giữa nền | Bổ sung người, xe đạp ngoài taxonomy | FIXED |
| F19 | IMAGE_ANALYSIS | img_035 thiếu car | Bổ sung xe sáng giữa/phải và che khuất | FIXED |
| F20 | IMAGE_ANALYSIS | img_036 thiếu người sau cabin, dễ lẫn người in | Thêm person có điều kiện kích thước, loại quảng cáo | FIXED |
| F21 | IMAGE_ANALYSIS; guideline; PROGRESS | img_040 suy tư thế đứng, bỏ bộ phận xe/tuk-tuk, mép taxi chưa đúng | Bỏ suy tư thế; ghi gương/phần xe, bus/tuk-tuk thiếu class và cắt biên thật | FIXED — class xe tiền cảnh còn cần xem |
| F22 | Guideline/notes 101 | Mức che 3 thành >50% trái nghĩa không rõ; mức 1 chồng 0 | Mức 2 trên 25%; mức 3 không rõ; mức 1 trên 0–25%; giữ đề xuất chờ nhóm | FIXED |
| F23 | Guideline 101 | Thiếu ego, câu áp dụng cá nhân như thể đã được nhóm chấp nhận, ví dụ can_review van chưa ràng buộc scope | Thêm I101-10 và điều kiện nhóm khóa/chấp nhận mapping | FIXED |
| F24 | Guideline 101 | QC thiếu lỗi lặp, toàn lô, mẫu số object, trách nhiệm chốt/kiểm | Bổ sung quy trình, không tạo số liệu/người chốt giả | FIXED |
| F25 | Notes 101 | Lặp checklist/rủi ro; thiếu trạng thái theo mẫu Pha 2–5, dễ lẫn kế hoạch với calibration | Rút phần lặp thành link; thêm trạng thái chưa có bằng chứng, khai AI audit | FIXED — ghi chú các pha còn chờ thực hiện |
| F26 | PROGRESS; IMAGE_ANALYSIS | Thiếu dấu vết vòng final audit và phân biệt AI kiểm với 101 xác nhận | Thêm liên kết báo cáo, giới hạn và hai mức sẵn sàng | FIXED |

## E. Technical Validation

Môi trường lệnh: PowerShell tại gốc repo, Python 3.13 theo traceback; đặt `PYTHONUTF8=1`, `PYTHONIOENCODING=utf-8`. Log chạy lại sau sửa lưu cục bộ tại `work/101/audit/` (không thuộc gói nộp); kết quả cốt lõi được ghi đầy đủ dưới đây để báo cáo không phụ thuộc thư mục work.

| Lệnh thực tế | Exit code | Kết quả |
|---|---|---|
| `python -m unittest discover -s tests -v` | 1 | 20 test: 19 OK, 0 assertion failures, 1 ERROR, 0 skipped; lần chạy có log 30.440s. |
| `python -m compileall -q scripts tests` | 0 | Biên dịch thành công; không đổi source scripts/tests. |
| `git diff --check` | 0 | Không lỗi whitespace của tracked diff; file 101 đang untracked nên kiểm bảng/whitespace bổ sung riêng, không dựa riêng lệnh này. |
| `git status --short` | 0 | TEAM.md đã modified và nhiều docs/submission đã untracked từ trước audit. Git cảnh báo không đọc được global ignore do Permission denied; lệnh vẫn exit 0. |
| `python work/101/audit/verify.py` | 0 | Assignment 40/40 duy nhất; so assignment.csv; decode 40 ảnh; SHA-256 mỗi ảnh bằng nguồn; schema/CVAT/rules/Markdown và snapshot ngoài phạm vi đạt. |
| `python work/101/audit/check_report.py` | 0 | Kiểm đủ 20 hàng tiêu chí, 40 hàng ảnh, 26 issue; tổng trạng thái khớp; bảng, liên kết tương đối và whitespace của cả năm tài liệu đạt. |
| `python scripts/check_submission.py --round 1` | 2 | Dừng ngay với “Chưa có file nhãn nào trong submission/labels/”. Không phải checker đã duyệt hết rồi chỉ còn một lỗi; còn nhiều artifact pha sau thiếu. |

Test ERROR: `test_assignment_rejects_unsafe_member_and_symlink_destination`, tại `tests/test_workflow.py:238`, gọi `Path.symlink_to(...)` phát sinh `OSError: [WinError 1314] A required privilege is not held by the client`. Đây là quyền Windows tạo symlink, xảy ra trước khi hoàn tất phần kiểm symlink destination. **Chưa xác nhận nhánh test đó trên máy này; không bỏ test, không nới kiểm tra bảo mật hoặc đổi quyền hệ thống.** Các fixture/nhãn tổng hợp của unit test chỉ nằm trong thư mục tạm do test tạo, không phải nhãn bài nộp.

Kiểm chi tiết dữ liệu:

- Assignment: 40 dòng/40 tên riêng cho 101; đúng 40 tệp JPEG. Assignment.csv có 40 ảnh, mỗi ảnh giao 101 và 102; không diễn giải thành hai lượt đã gán xong.
- Ảnh: 40 tệp mở/giải mã được, SHA-256 bằng `data/images/` tương ứng. Kích thước gốc từ 960×414 đến 768×1024/784×1024; chưa đo chiều cao box của từng vật nhỏ.
- Schema: `Draft202012Validator` và `scripts/common.py:load_taxonomy()` đều đạt. CVAT có đúng thứ tự sáu class, ba attributes cùng type/default/values/mutable cho năm class object; ignore không có attributes. Không xác minh được cấu hình đang dùng trong instance CVAT bên ngoài chỉ bằng JSON cục bộ.
- Rules so HEAD: `min_box_height_px=20`, `large_px=50`, `iou_thr_large=0.85`, `iou_thr_small=0.7`, `iaa_iou=0.85`, `iaa_class=0.95`, `error_rate_img_max=0.02`, `match_iou=0.5`; không đổi taxonomy/schema/cấu hình.
- Snapshot SHA-256 trước lần sửa đầu tiên được so lại: chỉ bốn tài liệu 101 cũ thay đổi; phần riêng 102 (guideline, notes, assignment và ảnh) cùng các file còn lại trong snapshot giữ nguyên. Báo cáo này là file mới; script/log audit chỉ ở `work/101/audit/`.
- Không tạo COCO, IAA, calibration decision, nhãn cuối hay QC review trong submission; không giả hoạt động của 101. Không chạy `make_cvat_labels.py` ghi đè artifact vì đã so trực tiếp cấu hình hiện có.

## F. Remaining Issues

**Phần cá nhân 101:**

1. Chi chưa tự kiểm/xác nhận bản AI hỗ trợ hoặc chứng minh đã gửi riêng. Yêu cầu “tự viết” và phạm vi AI được dùng trong RULES cần được Chi kiểm với coach trước khi xem bản chuẩn bị là bài cá nhân đã xác nhận; không thể giải quyết bằng audit tự động.
2. `img_024`: bản chất xe vàng trên nóc. `img_028`: ngựa thật/mô hình và mức che pickup (ngựa ngoài taxonomy dù loại nào). `img_040`: class/ranh giới phần xe hai bánh ở sát biên dưới. Giữ ba ảnh PARTIAL; Chi/reviewer xem ảnh gốc và chốt, không thêm box suy đoán.
3. Vật nhỏ/xa trong các cảnh đông chưa có đo box để áp 20 px hay ghi mức che cụ thể. Đây là việc khi người gán vẽ nhãn, không phải lỗi có thể chữa bằng đoán trong bảng phân tích.
4. Chưa có bằng chứng task/login/export CVAT và `labels/101.json`. Số box/can_review và trải nghiệm thật của Pha 3–5 chưa biết; ghi chú phải cập nhật sau thực hành. Ghi chú vẫn dài hơn gợi ý khoảng một trang của template; đã giảm checklist lặp nhưng giữ phân tích ca theo yêu cầu audit, Chi nên chọn ca tiêu biểu khi tự viết bản nộp cuối.

**Phụ thuộc nhóm/quy trình nộp:** chưa khóa v1.0/taxonomy; chưa thống nhất mapping ngoài taxonomy/pickup/van, sidecar/carrier, ego/phản chiếu, định lượng occlusion và ranh giới ignore. Chưa có các bộ nhãn độc lập, IAA, ca tham chiếu cùng sai, calibration/v1.1/nhãn cuối, QC toàn lô, reviewer/biên bản/gói hoàn chỉnh/kênh nộp được xác nhận. Không dùng guideline 101 thay quyết định nhóm.

**Môi trường:** một test symlink bị chặn bởi quyền Windows; cần chạy lại trên môi trường hỗ trợ symlink khi kiểm trọn bộ. Cảnh báo quyền global Git ignore không làm diff/status thất bại nhưng cần ghi rõ giới hạn. Không yêu cầu đổi quyền để làm đẹp kết quả audit.

## G. Final Verdict

| Phạm vi kết luận | Kết luận |
|---|---|
| 1. Nội dung guideline cá nhân | Có cấu trúc, ca thật, inclusion/exclusion và quy tắc đủ rõ để Chi review; lỗi mức che/ego/QC đã sửa. Các đề xuất chưa có hiệu lực như luật nhóm. |
| 2. Phân tích 40 ảnh | Đã kiểm trực quan 40/40; mô tả sau sửa dùng được cho review; 37 PASS, 3 PARTIAL có lý do. Chưa phải annotation hoặc QC geometry/attributes. |
| 3. Ghi chú cá nhân | Có ca khó/lý do/AI và trạng thái trung thực; còn phải tự xác nhận, rút gọn bản nộp nếu cần và bổ sung các pha thực sự làm sau này. |
| 4. Cấu trúc/kỹ thuật | Assignment, dữ liệu, schema, CVAT cục bộ, ngưỡng và Markdown đạt; 19 test OK, 1 lỗi quyền symlink; full-submission checker chưa đạt do thiếu nhãn. |
| 5. Sẵn sàng để Chi đọc và xác nhận | **READY FOR 101 REVIEW** — mọi điểm chưa chắc/thiếu bằng chứng đã được nêu để Chi quyết định, không yêu cầu tin vào một PASS toàn lab. |
| 6. Sẵn sàng nộp theo lab | **NOT READY cho gói đầy đủ.** Thiếu nhãn thật và các pha nhóm/QC. SUBMISSION cho phép nộp bằng chứng hiện có khi còn thiếu đầu vào theo kênh coach, nhưng chưa có quyết định Hold/QC thực tế hoặc xác nhận nộp để báo cáo thay. |

Tóm tắt định lượng: **20 tiêu chí A: 12 PASS / 4 PARTIAL / 4 FAIL; 40 ảnh đã mở; 26 nhóm lỗi nội dung đã sửa; 3 ca ảnh còn PARTIAL; 19/20 test OK, 1 ERROR quyền Windows.**
