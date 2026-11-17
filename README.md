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
| Quyết định hiện tại | **Hold**, tiếp tục calibration và QC trước khi bàn giao nhãn cuối |

Trong lượt review 101, tôi sử dụng backup đã review của 102 và công cụ AI hỗ trợ. Hai bản có chung nguồn đầu vào, vì vậy tôi đọc số đo so sánh cùng thông tin nguồn nhãn. Quy trình này chưa đáp ứng yêu cầu hai lượt vẽ box thủ công độc lập của RULES Day07.

## Hồ sơ bài nộp

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
| Phân tích nguồn và mức thay đổi | [review_comparison_101_102.md](submission/qc/review_comparison_101_102.md) |
| Chuẩn bị calibration | [calibration_candidates.csv](submission/qc/calibration_candidates.csv), [calibration_decisions.csv](submission/qc/calibration_decisions.csv), [calibration_context.json](submission/qc/calibration_context.json) |
| Ảnh cần xem và nháp đồng thuận | [flagged_images.txt](submission/qc/flagged_images.txt), [image_scores.csv](submission/qc/image_scores.csv), [consensus_draft.json](submission/qc/consensus_draft.json) |
| Nguồn và nhật ký sửa của tôi | [annotation_provenance_101.json](submission/qc/annotation_provenance_101.json), [annotation_corrections_101.csv](submission/qc/annotation_corrections_101.csv) |
| Kiểm tra file và phần cần hoàn thiện | [SUBMISSION_AUDIT_101.md](docs/member_101/SUBMISSION_AUDIT_101.md) |
| Nguồn và phép sử dụng ảnh | [data/README.md](data/README.md), [ATTRIBUTION.csv](data/ATTRIBUTION.csv) |

`consensus_draft.json` là bản nháp tự động. Bảng quyết định calibration hiện chờ nhóm điền và kiểm lại. Tôi chưa dùng hai file này thay cho nhãn cuối đã nghiệm thu.

## Kiểm tra độ đầy đủ của bài nộp

Phần hồ sơ cá nhân đã có guideline, COCO và ghi chú cho cả 101 và 102. Hồ sơ chung đã có phân công, taxonomy, nguồn ảnh, kết quả so sánh và báo cáo QC theo mẫu. Hai COCO đạt validator và các liên kết tài liệu trong repo đã được kiểm tra.

Gói bàn giao cuối còn các mục sau theo SUBMISSION.md.

| Tệp hoặc nhóm tệp còn thiếu | Việc cần hoàn thiện |
|---|---|
| `submission/guidelines/guideline_v1.1_calibrated.md` | Chốt quy tắc sau calibration |
| `submission/guideline_change.json` | Ghi loại và nội dung thay đổi của guideline đã chốt |
| `submission/qc/labels_calibrated.json` | Sửa và gộp nhãn theo quyết định calibration |
| `submission/qc/labels_calibrated.csv` | Xuất bảng nhãn cuối bằng build_final.py |
| `submission/qc/batch_manifest.json` | Sinh manifest nguồn, phiên bản và checksum của nhãn cuối |
| `submission/qc/reviews/round-01/` | Lập phiếu duyệt toàn lô rồi sinh kết quả QC |

`calibration_decisions.csv` đã có 604 dòng tương ứng các ca, còn chờ nhóm điền quyết định và bằng chứng kiểm lại. `taxonomy_v1.1.json` chỉ cần khi đổi schema. Bài hiện ở trạng thái **Hold**; chưa đủ điều kiện bàn giao nhãn cuối.

## Kiểm tra và chạy lại

Chạy từ thư mục gốc với Python 3.9+ sau khi cài `python -m pip install -r requirements.txt`.

```bash
python -X utf8 scripts/validate_labels.py --all
python -X utf8 scripts/qc_compare.py
python -X utf8 scripts/viz_disagreement.py --images flagged
python -X utf8 scripts/check_submission.py --round 1
```

Validator đã đạt cho cả 101 và 102. Lệnh so sánh sinh số đo và các ca cần xem từ đúng hai COCO hiện tại. Lệnh kiểm toàn gói vẫn báo thiếu vòng QC và `qc_result.json`; phần còn thiếu được liệt kê trong bảng kiểm bài nộp. Ảnh overlay có thể sinh lại tại `work/viz/`, thư mục này dùng cục bộ.

## Tài liệu lab

[Hướng dẫn các pha](GUIDE.md), [quy tắc](RULES.md), [rubric](RUBRIC.md), [yêu cầu bàn giao](SUBMISSION.md), [lệnh và định dạng phiếu](scripts/README.md), [Task CVAT](docs/team/CVAT_TASKS.md), [ngưỡng QC](docs/QC_CHEATSHEET.md).

Tôi cập nhật bổ sung lên nhánh `main` của repo nhóm hiện có. Việc nhận bài và kênh nộp chính thức thực hiện theo hướng dẫn của coach trong SUBMISSION.md.
