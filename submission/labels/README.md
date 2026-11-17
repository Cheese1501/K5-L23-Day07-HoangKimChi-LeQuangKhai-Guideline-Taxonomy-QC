# Nhãn của từng thành viên

Mỗi thành viên một file COCO xuất từ CVAT, tên `<mã>.json`, giữ đúng tập ảnh trong phân công. Chạy `python -X utf8 scripts/validate_labels.py --all`.

## Trạng thái ngày 2026-11-17

| Bản | Ảnh | Annotation | Nguồn |
|---|---:|---:|---|
| 101.json | 40 | 344 (342 đối tượng, 2 ignore) | Task19/Job14, review có AI hỗ trợ kế thừa backup đã review của 102 |
| 102.json | 40 | 352 (350 đối tượng, 2 ignore) | Export Task35/Job34 do 102 cung cấp, nguồn pre-label và review được ghi trong provenance |

Hai file đạt kiểm tra cấu trúc. Bản 101 đã sửa 21 shape có lý do theo guideline v1.0, còn 127 mức che 3 và 288 cờ can_review. Nguồn, checksum và giới hạn ở `../qc/annotation_provenance_101.json` và `../qc/annotation_provenance_102.json`. Nhật ký sửa tại `../qc/annotation_corrections_101.csv`.

Các phép đo trong `../qc/review_comparison_101_102.md` phản ánh hai bản cùng nguồn. Chưa có hai lượt gán thủ công độc lập, calibration nhóm hoặc nhãn cuối được QC nghiệm thu. Bản 101 cũ được giữ trong `../qc/history/20261116/`.
