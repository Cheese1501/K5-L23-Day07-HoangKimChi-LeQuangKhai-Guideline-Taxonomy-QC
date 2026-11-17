# Bảng kiểm bài nộp của tôi — 101

Cập nhật2026-11-17 theo SUBMISSION.md và hai mẫu báo cáo. Phần cá nhân dùng sáu mục của mẫu; QC_REPORT.md giữ năm mục và 23 tên trường.

| Nhóm hồ sơ | Kết quả |
|---|---|
| Cá nhân101/102 | Có guideline, COCO và ghi chú; mỗi COCO 40 ảnh |
| Nguồn và phân công | Có TEAM.md, ATTRIBUTION.csv, assignment.csv, hai danh sách ảnh và provenance |
| So sánh | Giữ nguyên iaa_summary.json/.md,604 ca trên 35 ảnh và nháp đồng thuận |
| Calibration |609 dòng có nội dung; phân biệt cách xử lý và xác nhận nhóm còn chờ bằng calibration_resolution_status.json |
| Guideline bàn giao |Có v1.1 editorial và guideline_change.json; giữ nghĩa và ngưỡng v1.0, chờ xác nhận nhóm |
| Nhãn bàn giao |Có labels_calibrated.json/.csv,40 ảnh/344 annotation và input theo tên phiên bản |
| Manifest |Có batch_manifest.json, checksum nhãn, nguồn ảnh và các đầu vào |
| QC vòng 1 |Giữ snapshot 346 annotation, phiếu40 ảnh,3 box thừa và1 người bỏ sót trên2 ảnh |
| QC vòng 2 |Giữ snapshot 344 annotation, phiếu và kết quả40 ảnh; chưa phát hiện lỗi bổ sung trong lượt kiểm có AI hỗ trợ |
| Quyết định |Hold do còn cờ và chưa có xác nhận calibration/nghiệm thu độc lập |

Hai vòng là kiểm trực quan có ChatGPT/Codex hỗ trợ cho mã 101. Vòng 1 xem 10 sheet đủ 40 ảnh, phóng ảnh gốc cho các ca cần đối chiếu. Vòng 2 mở lại overlay của hai ảnh sửa, kế thừa 38 ảnh giữ nguyên từ vòng 1. REVIEW_SCOPE.md từng vòng ghi phạm vi, không coi chỉ số0 lỗi mới là xác nhận giải quyết hết cờ.

Các tệp được yêu cầu trước đây đã có. Phần còn lại là nội dung cần nhóm xác nhận 609 dòng,289 cờ can_review và 127 mức che3, cùng issue ảnh 040. Điều kiện gán thủ công độc lập của Day07 chưa được chứng minh bởi hai bản cùng nguồn. Không thêm taxonomy_v1.1 vì schema giữ nguyên.

## Kiểm tra và truy vết

Chạy `python -X utf8 scripts/validate_labels.py --all` cho hai COCO cá nhân và `python -X utf8 scripts/check_submission.py --round 2` cho bộ bàn giao. Nhãn cuối, CSV và manifest được sinh bởi build_final.py. Vòng cũ giữ nguyên để đọc lỗi, bản sửa và kết quả kiểm lại.

Đã kiểm trên bản clone mới của commit bàn giao trong môi trường Windows: check_submission.py vòng 2 trả 0 lỗi, validator đạt cả hai COCO. .gitattributes giữ nguyên byte của image_issues.csv để Git không đổi xuống dòng làm lệch checksum đầu vào. Kiểm cấu trúc hồ sơ đạt được đọc cùng quyết định Hold và phạm vi kiểm có AI hỗ trợ.

Repo đã dọn 14 file hướng dẫn xuất trùng/walkthrough/.gitkeep; bản sao cục bộ và ZIP nguồn ở work/repo_cleanup_20261117/. Các liên kết, ảnh gốc, script, test, mẫu chấm và lịch sử có dẫn chứng được giữ.

Tôi cập nhật trên main của repo nhóm hiện có. Repo là public fork; kênh riêng tư và xác nhận nhận bài theo hướng dẫn coach trong SUBMISSION.md.
