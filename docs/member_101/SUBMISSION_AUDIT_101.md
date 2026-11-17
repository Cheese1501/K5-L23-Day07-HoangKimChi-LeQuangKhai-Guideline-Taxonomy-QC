# Kiểm phần cá nhân 101 — 2026-11-17

| Hạng mục | Kết quả |
|---|---|
| Bản CVAT | Task19/Job14, `DAY07-101-REVIEW-40frames`, kế thừa backup đã review của 102 |
| COCO | `submission/labels/101.json`, 40 ảnh, 344 annotation (342 đối tượng và 2 ignore) |
| Sửa có bằng chứng | 21 shape trên 13 ảnh, xóa 8 và cập nhật 13; ảnh, rule, trước/sau trong `submission/qc/annotation_corrections_101.csv` |
| Nguồn | `submission/qc/annotation_provenance_101.json`, có checksum backup, export, 101 và 102 |
| Báo cáo | `submission/qc/QC_REPORT.md` giữ các trường của mẫu QC; `submission/individual_notes/101.md` giữ sáu phần của mẫu cá nhân |
| So sánh | `submission/qc/review_comparison_101_102.json` và `.md`, 342 cặp, IoU 1.0000, cùng lớp 336/342; nêu rõ bản kế thừa cùng nguồn |
| Bản cũ | `submission/qc/history/20261116/`, gồm nhãn 101 và bằng chứng trước lần cập nhật này |
| Validator | `python -X utf8 scripts/validate_labels.py --all` đạt cho cả 101 và 102 |
| Kiểm thử workflow | 20/20 test đạt trong môi trường Linux của container; trên Windows có một test symlink bị chặn bởi quyền hệ điều hành |

## Giới hạn của bài hiện có

Quy trình review dùng box đề xuất và xem nhãn 102 trước khi sửa, nên không đáp ứng lượt gán thủ công độc lập của RULES Day07. IoU cao do giữ tọa độ nguồn trong các box còn lại. Các khác biệt được sửa theo lỗi nhìn thấy, không tạo độ lệch ngẫu nhiên để thay đổi chỉ số.

Đã xem tổng quan 40 ảnh qua sheet có box, chưa nghiệm thu từng đối tượng. Còn 127 box occluded_level=3 và 288 can_review=true. Chưa có xác nhận của người học đối với từng sửa, họp calibration, guideline v1.1, nhãn cuối, manifest hoặc QC toàn lô. Quyết định hiện tại là Hold.

`python -X utf8 scripts/check_submission.py --round 1` vẫn báo hai lỗi do trường vòng QC chưa là số vòng đã thực hiện và thiếu `reviews/round-01/qc_result.json`. Đây là yêu cầu chưa hoàn thành của toàn gói, không sửa bằng tạo phiếu chưa duyệt. SUBMISSION.md cho phép nộp bằng chứng hiện có ở trạng thái Hold.

## Kênh cập nhật

Người dùng yêu cầu cập nhật main của repo nhóm hiện có sau khi kiểm remote. Repo là public fork của starter lab; GitHub API trả 422 khi đổi riêng tư, với lý do `Public forks can't be made private`. Việc push main ghi nhận bàn giao artifact trên repo hiện có; chưa xác minh coach đã nhận bài hoặc kênh này được coach chấp thuận thay yêu cầu riêng tư trong SUBMISSION.md. Không tìm thấy tài khoản GitHub coach trong cấu hình hoặc tài liệu repo.
