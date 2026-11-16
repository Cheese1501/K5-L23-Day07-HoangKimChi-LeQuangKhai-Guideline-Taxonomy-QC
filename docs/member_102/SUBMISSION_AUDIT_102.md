# Kiểm phần cá nhân 102 — 2026-11-17

## Đã có và đã kiểm

| Hạng mục | Trạng thái / bằng chứng |
|---|---|
| COCO cá nhân | submission/labels/102.json: export nguyên bản CVAT Task 35/Job 34; 40 ảnh, 352 annotation (350 đối tượng, 2 ignore), không kèm ảnh |
| Phân công | assignment.csv và assignments/102.txt trên repo: 40 ảnh; tập ảnh COCO khớp validator |
| Kiểm định dạng | `python scripts/validate_labels.py submission/labels/102.json` PASS; `--all` PASS cho 101 và 102 |
| Guideline cá nhân | Có đủ 5 mục; đề xuất ban đầu được giữ, ca ảnh bổ sung sau review được ghi rõ thời điểm |
| Guideline nhóm | File chung v1.0 và taxonomy v1.0 đã có trên repo; bản cá nhân 30/70% chỉ là lịch sử, không phải quy tắc áp dụng |
| Ghi chú cá nhân | Đã bổ sung các bước/số liệu đã xác minh và cách kiểm lại gợi ý AI; phần trải nghiệm cá nhân cần 102 tự xác nhận |
| Nguồn nhãn | annotation_provenance_102.json ghi nguồn đề xuất và review; source=manual là metadata cuối, không chứng minh vẽ từ đầu |
| Dữ liệu | ATTRIBUTION.csv có trong repo; không đưa credentials, work hoặc môi trường Python vào commit |

## Chưa hoàn tất theo đề

1. RULES Day07 yêu cầu người thật vẽ box độc lập. Quy trình thực tế của 102 dùng nhãn gợi ý YOLO + SAM 3 và review; không đánh dấu yêu cầu gán thủ công độc lập là đạt. Bản 101 cũng dùng nhãn gợi ý cùng nguồn. Cần ghi đúng quy trình thực tế và để coach đánh giá yêu cầu này; không sửa bằng đổi metadata hoặc diễn đạt sai nguồn nhãn.
2. Guideline cá nhân ban đầu chưa có ví dụ ID ảnh ở Pha1; bảng hiện tại bổ sung sau review, không thể tạo lại bằng chứng khảo sát độc lập trong quá khứ.
3. Ghi chú về ca lưỡng lự nhất và điều sẽ làm khác cần 102 tự bổ sung. Không viết trải nghiệm chưa được người học cung cấp.
4. Export còn 292 can_review=true và 134 occluded_level=3. Giữ nguyên; cần giải thích/xử lý ca cụ thể trong calibration. Không tự tắt cờ hoặc gán mức che thay người học.
5. IAA, calibration, guideline v1.1, nhãn cuối, manifest và QC toàn lô là phần tiếp theo của nhóm; chưa làm trong lần nộp cá nhân này. Nếu so sánh hai bản hiện có, phải nêu cùng nguồn nháp thay vì gọi là IAA thủ công độc lập.
6. Repo được kiểm qua GitHub API đang Public tại lần kiểm. SUBMISSION.md yêu cầu repo nộp riêng tư có quyền coach, hoặc gói nén nộp LMS. Chuẩn bị commit trên máy; chỉ push khi repo đã riêng tư hoặc có hướng dẫn khác rõ ràng của coach/người dùng.

## Kiểm gói cuối chưa đạt

`python scripts/check_submission.py --round 1` exit 1: QC_REPORT chưa có số vòng, thiếu reviews/round-01/qc_result.json. Đây là kiểm toàn gói; không tạo vòng QC hoặc số liệu giả để làm xanh. Còn thiếu các bước nhóm khác nên không coi hai lỗi dừng sớm là danh sách đầy đủ phần chưa làm.

## Nộp riêng

101.json đã có trên repo ở commit b3b7245. Bản 102 được khóa bằng checksum trong provenance và export giữ ở work cục bộ. Nộp riêng cho coach theo kênh lớp; không coi commit trên repo chung là đã gửi coach qua LMS. Nhãn đề xuất đã từng được chia sẻ cho review trước đó, vì vậy không khẳng định bảo toàn được điều kiện gán mù độc lập.
