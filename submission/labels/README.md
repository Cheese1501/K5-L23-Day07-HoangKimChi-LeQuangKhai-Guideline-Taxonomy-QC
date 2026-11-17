# Nhãn của từng thành viên

Mỗi thành viên một file COCO xuất từ CVAT, tên `<mã>.json`, giữ đúng tập ảnh trong phân công. Chạy `python -X utf8 scripts/validate_labels.py --all`.

Bản ZIP export CVAT do 101 cung cấp nằm tại [../exports/101.zip](../exports/101.zip). JSON `annotations/instances_default.json` bên trong khớp từng byte với `101.json` trong thư mục này.

## Trạng thái ngày 2026-11-17

| Bản | Ảnh | Annotation | Nguồn |
|---|---:|---:|---|
| 101.json | 40 | 344 (342 đối tượng, 2 ignore) | Task19/Job14, review có AI hỗ trợ kế thừa backup đã review của 102 |
| 102.json | 40 | 352 (350 đối tượng, 2 ignore) | Export Task35/Job34 do 102 cung cấp, nguồn pre-label và review được ghi trong provenance |

Hai file đạt kiểm tra cấu trúc. Trong bài 101 của tôi, lượt review có 21 shape được sửa theo guideline v1.0, còn 127 mức che 3 và 288 cờ can_review. Tôi khai báo nguồn và công cụ hỗ trợ ở `../qc/annotation_provenance_101.json`; nguồn bản 102 ở `../qc/annotation_provenance_102.json`. Nhật ký sửa tại `../qc/annotation_corrections_101.csv`.

Tôi đã chạy so sánh, lưu đầu ra chuẩn trong `../qc/iaa_summary.json/.md` và giải thích bối cảnh cùng nguồn trong `../qc/QC_REPORT.md`. Bộ bàn giao riêng nằm tại `../qc/labels_calibrated.json/.csv`, có manifest và hai vòng QC. Nhãn cá nhân ở bảng trên giữ trạng thái trước calibration để tái lập phép so sánh. Bản bàn giao có 344 annotation, 289 cờ review và quyết định Hold, chờ xác nhận nhóm. Bản 101 cũ được giữ trong `../qc/history/20261116/`.
