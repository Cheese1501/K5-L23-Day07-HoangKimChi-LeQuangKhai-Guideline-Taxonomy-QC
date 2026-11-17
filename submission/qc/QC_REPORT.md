# Báo cáo QC — nhóm 101–102

Nhóm chúng tôi thực hiện bài Day07 trên 40 ảnh, dùng mã 101 và 102. Tôi phụ trách phần bài 101 và cập nhật báo cáo này ngày 2026-11-17 theo mẫu `docs/QC_REPORT_TEMPLATE.md`. Trong lượt review, tôi sử dụng backup đã review của 102 và công cụ AI hỗ trợ. Báo cáo trình bày kết quả hiện có, nguồn nhãn và phần nhóm cần hoàn thiện trước nghiệm thu.

## 1. Mục đích, dữ liệu và phiên bản

- Mục đích và giới hạn sử dụng: nhóm chúng tôi thực hành đặc tả, review box 2D và đối chiếu bản nhãn trên bộ 40 ảnh Day07. Kết quả không đại diện đầy đủ cho giao thông thực tế.
- Nguồn và phép sử dụng dữ liệu: `data/images/img_001.jpg`–`img_040.jpg`; chúng tôi giữ ghi công và giấy phép trong `data/ATTRIBUTION.csv`.
- Manifest và checksum nhãn cuối: chưa có nhãn cuối và `batch_manifest.json`. Nhãn review 101 có SHA-256 `e996c410d42d9dd0966ab0c7f71774dc90b61a2b14e1d4d0963147839c009921`; bản 102 có SHA-256 `3fe63fec2771eb7e47a2167526d6e208a80b5d1a309a985b721b4bf5f20f67c6`. Nguồn và checksum tại `annotation_provenance_101.json` và `annotation_provenance_102.json`.
- Guideline và taxonomy khi gán / khi bàn giao: guideline chung v1.0 đã đồng ý và `submission/taxonomy.json` v1.0. Giữ các ngưỡng lab. Chưa có guideline v1.1 sau calibration.

## 2. Phân công và đồng thuận trước calibration

- Lượt hoàn thành / được giao: 80/80 lượt ảnh có mặt trong hai COCO, mỗi file đủ 40 ảnh theo `assignment.csv`. Hai bộ có nguồn pre-label và bản 101 kế thừa trực tiếp backup 102, nên 80 lượt có file chưa chứng minh 80 lượt gán thủ công độc lập theo RULES.
- Số cặp box ghép, IoU TB, đồng thuận lớp và mẫu số: so sánh bản sửa với nguồn, 342 cặp đối tượng; IoU trung bình 1.0000; cùng lớp 336/342 = 98.25%. Tôi diễn giải các số đo cùng nguồn đầu vào chung của hai bản. Các sửa trong lượt review tập trung vào lớp, thuộc tính và box thừa, nên tọa độ các box giữ lại được kế thừa.
- Box chưa ghép, loại do ignore, bất đồng vùng ignore: 101 có 0, 102 có 8 box đối tượng chưa ghép. Mỗi bản có 2 vùng ignore cùng hình học, loại khỏi phép ghép đối tượng; phép so sánh này không bỏ thêm đối tượng theo độ phủ ignore. Ghép tham lam theo `common.match_boxes`, không phân biệt lớp, ngưỡng 0.5. Các box trùng tọa độ có thể tạo hòa điểm, nên sáu cặp lệch lớp trong phép ghép không đồng nghĩa sáu thao tác đổi lớp.
- Ca hai người có thể cùng sai sau khi đối chiếu tham chiếu: nhóm chúng tôi chưa có bộ tham chiếu được coach xác nhận. Tôi cần rà nguy cơ cùng bỏ sót ở ảnh 021/030/032; cờ mức che 3 còn nhiều. Xe vàng 024 giữ ứng viên car cần review theo R-05/R-09.

Đồng thuận thuộc tính trên 342 cặp: occluded_level 338/342 = 98.83%; truncated 337/342 = 98.54%; can_review 338/342 = 98.83%. Tôi đã chạy `qc_compare.py`, sinh `iaa_summary.json/.md`, `calibration_candidates.csv`, `image_scores.csv`, `flagged_images.txt` và `consensus_draft.json`. Kết quả có 604 ca cần xem trên 35 ảnh, gồm 580 cờ can_review, 8 ca bỏ sót/thừa, 9 ca thuộc tính, 6 ca lớp và 1 vấn đề cấp ảnh. Đây là các ca do script ghi nhận, chưa phải số lỗi sau xác nhận. Tôi giữ nguyên đầu ra script và đọc chỉ báo đạt ngưỡng trong bối cảnh hai bản cùng nguồn.

## 3. Calibration và kiểm lại

- Ca đã xử lý, rule ID, bản sửa và người xác nhận: bản review của tôi có 21 shape được sửa trên 13 ảnh với công cụ hỗ trợ, gồm xóa 8 và cập nhật 13. Nhật ký `annotation_corrections_101.csv` có ảnh, chỉ số shape nguồn, ID Task19, rule, lý do và trước/sau. Tôi đã chuẩn bị `calibration_decisions.csv` gồm 604 dòng tương ứng các ca và `calibration_context.json` khóa checksum của lần so sánh. Nhóm chúng tôi còn cần điền quyết định, rule, phiên bản, người chốt và kết quả kiểm lại cho từng ca.
- Tác động v1.1 lên nhãn và ảnh: chưa có v1.1. Các sửa áp dụng quy tắc v1.0 về pickup/van, tuk-tuk, hình in, instance trùng, occlusion và truncation.
- Tham chiếu bằng chứng khi Rework: bản 101 ngày 2026-11-16 được giữ ở `history/20261116/101.json` cùng provenance và nhật ký cũ. Bản hiện tại xuất từ Task19/Job14. Nguồn backup khớp bản 102 trên main ở độ chính xác xuất COCO hai chữ số thập phân.

## 4. Kết quả duyệt

- Vòng QC: chưa mở vòng QC nghiệm thu; lượt review chuẩn bị ngày 2026-11-17 được ghi riêng.
- Người review và ngày: tôi, mã 101, thực hiện phần review cá nhân với ChatGPT/Codex hỗ trợ ngày 2026-11-17. Nhóm chưa phân công người nghiệm thu cuối và chưa lập phiếu QC toàn lô.
- Đã duyệt / cả lô: tôi đã thực hiện lượt review tổng quan 40/40 ảnh với sheet có box và lưu các chỉnh sửa. Nhóm còn cần duyệt chi tiết từng đối tượng, vật bỏ sót và ghi phiếu QC cho toàn bộ 40 ảnh.
- Ảnh lỗi / ảnh đã duyệt: chưa xác định tỷ lệ lỗi QC; 13/40 ảnh có sửa trong lượt review là độ phủ thay đổi, không phải tỷ lệ lỗi còn lại.
- Annotation đối tượng hiện có bị lỗi / annotation đối tượng đã duyệt: chưa có mẫu số nghiệm thu. COCO hiện có 342 đối tượng và 2 ignore; còn 127 box occluded_level=3 và 288 can_review=true.
- Vật bỏ sót, ảnh và vùng: chưa hoàn thành khảo sát bỏ sót từng vùng, cần kiểm kỹ ảnh 003/008/019/021/030/032/039 và người trong cabin/qua kính.
- Ca khó / phần còn lại, lỗi lặp và ví dụ: đã bỏ motorcycle trên hai tuk-tuk ảnh 004 theo R-02, chân dung biển quảng cáo ảnh 018 theo R-09; bỏ box trùng ảnh 001/024/028 theo R-06. Ảnh 024 còn cần xác định bản chất xe vàng, ảnh 040 cần xét riêng phần xe sát dưới, ảnh đông cần kiểm từng instance.
- Một lỗi máy chặn được và một lỗi cần người đọc ảnh: validator kiểm được box vượt biên hoặc thuộc tính ngoài enum; lượt review phát hiện chân dung in bị gán person tại ảnh 018, điều mà validator cấu trúc không quyết định được. `python -X utf8 scripts/validate_labels.py --all` đạt cho 101 và 102.

## 5. Quyết định bàn giao

- Quyết định: Hold
- Lý do, người nhận và phạm vi sử dụng: tôi nộp hồ sơ hiện có để coach xem phần thực hành và các sửa có bằng chứng. Chưa có gán thủ công độc lập, calibration nhóm, nhãn cuối và phiếu QC toàn lô để Release theo RULES.
- Nếu còn việc: tôi tiếp tục rà từng sửa, cờ chưa chắc và vấn đề cấp ảnh; nhóm 101–102 hoàn thiện 604 dòng calibration, chốt v1.1 và guideline_change.json, tạo nhãn cuối cùng manifest, phân công reviewer và mở vòng QC. Tôi cập nhật bổ sung lên main của repo nhóm hiện có; kênh nộp chính thức theo SUBMISSION.md và hướng dẫn coach.
- Kiểm ngược từ báo cáo tới ảnh, rule và nhãn: `img_018.jpg` → R-09 → dòng xóa chỉ số nguồn 153 trong `annotation_corrections_101.csv`; `img_037.jpg` → R-08 → đổi van thành truck, có box và thuộc tính trước/sau; `img_026.jpg` → R-04 → truncated=yes cho xe máy. COCO và checksum xác định đúng bản đã xuất.
