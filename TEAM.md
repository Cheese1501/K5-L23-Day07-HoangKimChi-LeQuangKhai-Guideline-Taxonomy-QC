# Thông tin nhóm

- Tên nhóm: Nhóm 101–102.
- Mã thành viên (ba chữ số): 101, 102.
- Người điều phối: chưa phân công.
- Người review bản cuối: chưa phân công.
- Commit chốt bài: chưa chốt gói bàn giao cuối.

## Kết quả tóm tắt

- Guideline chung và taxonomy: v1.0, hai thành viên đã đồng ý; giữ nguyên ngưỡng của lab.
- Lượt gán hoàn tất / được giao: chưa có đủ COCO thủ công độc lập để xác nhận / 80 lượt (40 ảnh × 2 người).
- Bản thực hành review 101: `submission/labels/101.json`, 40 ảnh/344 annotation (342 đối tượng, 2 ignore), Task19/Job14 ngày 2026-11-17; kế thừa backup review của 102, sửa 21 shape trên 13 ảnh. Đạt kiểm tra cấu trúc; còn 127 mức che 3 và 288 cờ review, lượt review cá nhân có công cụ AI hỗ trợ; nhóm tiếp tục calibration và QC.
- Kết quả so sánh trước calibration (kèm mẫu số): đã chạy `qc_compare.py` trên hai bản hiện có. So sánh bản sửa cùng nguồn có 342 cặp, IoU TB 1.0000, cùng lớp 336/342 (98.25%), box chưa ghép 101/102 là 0/8; không diễn giải thành IAA độc lập. Xem `submission/qc/review_comparison_101_102.md`.
- Calibration:604 ca so sánh trên 35 ảnh và 5 thao tác sau QC đã ghi quyết định xử lý;609 dòng còn chờ xác nhận nhóm. Có guideline v1.1 editorial, nhãn bàn giao JSON/CSV và manifest.
- Vòng QC:hai vòng kiểm trực quan có AI hỗ trợ,40/40 ảnh mỗi vòng; vòng 2 kiểm lại hai ảnh sửa và kế thừa 38 ảnh giữ nguyên. Còn chờ nghiệm thu độc lập.
- Tỉ lệ lỗi trong phiếu:vòng 1 có 2/40 ảnh lỗi,3/344 box hiện có lỗi và1 vật bỏ sót; vòng 2 ghi 0/40 lỗi mới và0/342 box lỗi, còn 289 cờ review.
- Quyết định:**Hold**. Đã có bộ file bàn giao, còn xác nhận calibration/nghiệm thu và cờ chưa giải quyết; điều kiện gán độc lập chưa được chứng minh.

## Hồ sơ học tập

- [Guideline chung v1.0](submission/guidelines/guideline_v1.0_agreed.md).
- Guideline cá nhân: [101](submission/guidelines/individual/guideline_101.md), [102](submission/guidelines/individual/guideline_102.md).
- Ghi chú cá nhân: [101](submission/individual_notes/101.md), [102](submission/individual_notes/102.md). Mỗi người chịu trách nhiệm hoàn thiện phần của mình; bản 102 đã có ghi chú và COCO 40 ảnh/352 annotation sau review, đạt kiểm tra cấu trúc; nguồn và giới hạn tại `submission/qc/annotation_provenance_102.json`.
- [Báo cáo nhóm theo mẫu QC](submission/qc/QC_REPORT.md) và [phân công](submission/qc/assignment.csv).

Phần thử YOLO/SAM và review nhãn từ nguồn khác không tính là kết quả gán độc lập Day 07.
