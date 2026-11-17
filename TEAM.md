# Thông tin nhóm

- Tên nhóm: Nhóm 101–102.
- Mã thành viên (ba chữ số): 101, 102.
- Người điều phối: chưa phân công.
- Người review bản cuối: chưa phân công.
- Commit chốt bài: chưa chốt gói bàn giao cuối.

## Kết quả tóm tắt

- Guideline chung và taxonomy: v1.0, hai thành viên đã đồng ý; giữ nguyên ngưỡng của lab.
- Lượt gán hoàn tất / được giao: chưa có đủ COCO thủ công độc lập để xác nhận / 80 lượt (40 ảnh × 2 người).
- Bản thực hành review 101: `submission/labels/101.json`, 40 ảnh/344 annotation (342 đối tượng, 2 ignore), Task19/Job14 ngày 2026-11-17; kế thừa backup review của 102, sửa 21 shape trên 13 ảnh. Đạt kiểm tra cấu trúc; còn 127 mức che 3 và 288 cờ review, chưa có xác nhận người học từng sửa.
- IAA trước calibration (kèm mẫu số): chưa có hai bộ nhãn độc lập hợp lệ. So sánh bản sửa cùng nguồn có 342 cặp, IoU TB 1.0000, cùng lớp 336/342 (98.25%), box chưa ghép 101/102 là 0/8; không diễn giải thành IAA độc lập. Xem `submission/qc/review_comparison_101_102.md`.
- Số ảnh phải calibration: chưa xác định.
- Vòng QC và số ảnh đã duyệt / cả lô: chưa thực hiện / 40 ảnh cần duyệt.
- Tỉ lệ lỗi: N/A, chưa có phiếu duyệt.
- Quyết định: **Hold**, do thiếu nhãn độc lập, calibration và bằng chứng QC; chưa bàn giao lô nhãn.

## Hồ sơ học tập

- [Guideline chung v1.0](submission/guidelines/guideline_v1.0_agreed.md).
- Guideline cá nhân: [101](submission/guidelines/individual/guideline_101.md), [102](submission/guidelines/individual/guideline_102.md).
- Ghi chú cá nhân: [101](submission/individual_notes/101.md), [102](submission/individual_notes/102.md). Mỗi người chịu trách nhiệm hoàn thiện phần của mình; bản 102 đã có ghi chú và COCO 40 ảnh/352 annotation sau review, đạt kiểm tra cấu trúc; nguồn và giới hạn tại `submission/qc/annotation_provenance_102.json`.
- [Báo cáo nhóm theo mẫu QC](submission/qc/QC_REPORT.md) và [phân công](submission/qc/assignment.csv).

Phần thử YOLO/SAM và review nhãn từ nguồn khác không tính là kết quả gán độc lập Day 07.
