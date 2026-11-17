# Bài thực hành Day 07 — Guideline, Taxonomy & QC

Nhóm chúng tôi gồm hai thành viên **101 và 102**, thực hành xây dựng guideline, gán nhãn và kiểm tra chất lượng trên 40 ảnh đường phố. Tôi dùng mã **101** cho phần bài cá nhân trong repo này.

![Mẫu ảnh trong bộ dữ liệu](docs/assets/sample_grid.jpg)

## Kết quả hiện có

| Hạng mục | Kết quả |
|---|---|
| Guideline | Hai bản cá nhân và guideline chung v1.0, taxonomy v1.0 |
| Nhãn của tôi — 101 | 40 ảnh, 344 annotation gồm 342 đối tượng và 2 ignore |
| Nhãn 102 | 40 ảnh, 352 annotation gồm 350 đối tượng và 2 ignore |
| Review bản 101 | 21 chỉnh sửa trên 13 ảnh, có nhật ký trước/sau |
| So sánh hai bản hiện có | 342 cặp, IoU TB 1.0000, cùng lớp 336/342 (98.25%), chưa ghép 0/8 |
| Ca cần calibration | 604 ca trên 35 ảnh, gồm cả cờ chưa chắc; chưa phải 604 lỗi xác nhận |
| Bộ nhãn bàn giao |40 ảnh,344 annotation; guideline v1.1 editorial, có JSON/CSV và manifest |
| QC có AI hỗ trợ | Vòng 1 phát hiện2/40 ảnh lỗi, đã sửa; vòng 2 ghi 0/40 lỗi mới, còn cờ chờ xác nhận |
| Quyết định hiện tại | **Hold**, tiếp tục calibration và QC trước khi bàn giao nhãn cuối |

Trong lượt review 101, tôi sử dụng backup đã review của 102 và công cụ AI hỗ trợ. Hai bản có chung nguồn đầu vào, vì vậy tôi đọc số đo so sánh cùng thông tin nguồn nhãn. Quy trình này chưa đáp ứng yêu cầu hai lượt vẽ box thủ công độc lập của RULES Day07.

## Hồ sơ bài nộp

File COCO 101 đã được đối chiếu với bản export tôi cung cấp, `job_14_annotations_2026_11_17_04_17_59_coco 1.0.zip`. JSON bên trong khớp từng byte với `submission/labels/101.json`, đủ 40 ảnh và 344 annotation.

| Nội dung | Tệp |
|---|---|
| Thông tin nhóm và tiến độ | [TEAM.md](TEAM.md) |
| Guideline của tôi | [guideline_101.md](submission/guidelines/individual/guideline_101.md) |
| Guideline cá nhân 102 | [guideline_102.md](submission/guidelines/individual/guideline_102.md) |
| Guideline chung và taxonomy | [v1.0](submission/guidelines/guideline_v1.0_agreed.md), [taxonomy.json](submission/taxonomy.json) |
| Nhãn COCO | [101.json](submission/labels/101.json), [102.json](submission/labels/102.json) |
| Phân công và vấn đề cấp ảnh | [assignment.csv](submission/qc/assignment.csv), [image_issues.csv](submission/qc/image_issues.csv) |
| Báo cáo QC theo mẫu | [QC_REPORT.md](submission/qc/QC_REPORT.md) |
| Ghi chú cá nhân | [101](submission/individual_notes/101.md), [102](submission/individual_notes/102.md) |
| Kết quả so sánh do script sinh | [iaa_summary.md](submission/qc/iaa_summary.md), [iaa_summary.json](submission/qc/iaa_summary.json) |
| Chuẩn bị calibration | [calibration_candidates.csv](submission/qc/calibration_candidates.csv), [calibration_decisions.csv](submission/qc/calibration_decisions.csv), [calibration_context.json](submission/qc/calibration_context.json) |
| Ảnh cần xem và nháp đồng thuận | [flagged_images.txt](submission/qc/flagged_images.txt), [image_scores.csv](submission/qc/image_scores.csv), [consensus_draft.json](submission/qc/consensus_draft.json) |
| Nguồn và nhật ký sửa của tôi | [annotation_provenance_101.json](submission/qc/annotation_provenance_101.json), [annotation_corrections_101.csv](submission/qc/annotation_corrections_101.csv) |
| Nguồn và phép sử dụng ảnh | [data/README.md](data/README.md), [ATTRIBUTION.csv](data/ATTRIBUTION.csv) |

`consensus_draft.json` là bản nháp tự động. Bộ bàn giao có nhãn riêng và hai vòng QC; quyết định hiện tại là Hold. Các dòng calibration đã có quyết định xử lý và ghi rõ phần chờ nhóm xác nhận.

## Kiểm tra độ đầy đủ của bài nộp

Các nhóm file theo SUBMISSION.md đã có. Bằng chứng chất lượng và phần chờ xác nhận được ghi trong báo cáo QC.

| Nội dung hoàn thiện | Tệp |
|---|---|
| Guideline bàn giao và thay đổi | [v1.1](submission/guidelines/guideline_v1.1_calibrated.md), [guideline_change.json](submission/guideline_change.json) |
| Nhãn bàn giao | [labels_calibrated.json](submission/qc/labels_calibrated.json), [labels_calibrated.csv](submission/qc/labels_calibrated.csv) |
| Manifest | [batch_manifest.json](submission/qc/batch_manifest.json) |
| Quyết định và trạng thái calibration | [calibration_decisions.csv](submission/qc/calibration_decisions.csv), [calibration_resolution_status.json](submission/qc/calibration_resolution_status.json) |
| Sửa bổ sung | [calibration_corrections_101.json](submission/qc/calibration_corrections_101.json) |
| QC vòng 1 | [Phiếu](submission/qc/reviews/round-01/qc_review.csv), [kết quả](submission/qc/reviews/round-01/qc_report_auto.md) |
| QC vòng 2 | [Phiếu](submission/qc/reviews/round-02/qc_review.csv), [kết quả](submission/qc/reviews/round-02/qc_report_auto.md), [phạm vi](submission/qc/reviews/round-02/REVIEW_SCOPE.md) |

609 dòng calibration đã ghi cách xử lý, gồm 604 ca so sánh và 5 thao tác sau QC. Xác nhận của nhóm còn chờ. Nhãn bàn giao giữ289 cờ review và 127 mức che3, nên bài vẫn **Hold**. taxonomy_v1.1.json không phát sinh vì schema giữ nguyên.

## Kiểm tra và chạy lại

Chạy từ thư mục gốc với Python 3.9+ sau khi cài `python -m pip install -r requirements.txt`.

```bash
python -X utf8 scripts/validate_labels.py --all
python -X utf8 scripts/qc_compare.py
python -X utf8 scripts/viz_disagreement.py --images flagged
python -X utf8 scripts/check_submission.py --round 2
```

Validator đã đạt cho cả 101 và 102. Lệnh so sánh sinh số đo và các ca cần xem từ đúng hai COCO hiện tại. Kiểm toàn gói dùng vòng 2; kết quả kiểm cấu trúc hồ sơ được đọc cùng quyết định Hold và các điều kiện còn chờ. Ảnh overlay có thể sinh lại tại `work/viz/`, thư mục này dùng cục bộ.

## Tài liệu lab

[Hướng dẫn các pha](GUIDE.md), [quy tắc](RULES.md), [rubric](RUBRIC.md), [yêu cầu bàn giao](SUBMISSION.md), [lệnh và định dạng phiếu](scripts/README.md), [thiết lập CVAT](docs/CVAT_SETUP.md), [ngưỡng QC](docs/QC_CHEATSHEET.md).

Tôi cập nhật bổ sung lên nhánh `main` của repo nhóm hiện có. Việc nhận bài và kênh nộp chính thức thực hiện theo hướng dẫn của coach trong SUBMISSION.md.
