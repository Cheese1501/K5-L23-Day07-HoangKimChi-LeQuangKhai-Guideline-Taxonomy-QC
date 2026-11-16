# Nhãn của từng thành viên

Mỗi thành viên **một file COCO 1.0** export từ CVAT: `<mã>.json` (ví dụ `101.json`).
Chỉ chứa các ảnh được giao trong `submission/qc/assignments/<mã>.txt`. Chạy `python scripts/validate_labels.py submission/labels/101.json` trước khi gửi riêng.

## Trạng thái file 101 hiện tại

`101.json` là bản export COCO từ Task17/Job12 sau lượt sửa nhãn có AI hỗ trợ: 40 ảnh, 344 annotation (342 đối tượng và 2 vùng ignore). File đạt kiểm tra cấu trúc; **chưa phải bộ nhãn thủ công độc lập đáp ứng RULES của Day07 hoặc nhãn cuối đã QC**.

Nguồn và giới hạn tại [annotation_provenance_101.json](../qc/annotation_provenance_101.json); các thay đổi tại [annotation_corrections_101.csv](../qc/annotation_corrections_101.csv). Còn 312 box có mức che3 và cả342 box đối tượng còn can_review=true; cần review ý nghĩa và độ đầy đủ trên ảnh. Không dùng bản này để khẳng định đã hoàn thành lượt độc lập hoặc đo IAA thủ công với102.
