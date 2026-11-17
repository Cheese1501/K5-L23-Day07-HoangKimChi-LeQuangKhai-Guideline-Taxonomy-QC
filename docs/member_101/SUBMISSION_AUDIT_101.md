# Bảng kiểm bài nộp của tôi — 101

Tôi đối chiếu hồ sơ ngày 2026-11-17 với SUBMISSION.md, GUIDE.md và các mẫu báo cáo. Phần cá nhân dùng ngôi “tôi”, phần chung dùng “nhóm chúng tôi”. Tôi giữ nguồn nhãn và số liệu để người đọc kiểm lại.

## Các tệp đã có

| Yêu cầu | Tệp và kết quả |
|---|---|
| Nhóm và nguồn dữ liệu | TEAM.md, data/ATTRIBUTION.csv; đủ nguồn cho 40 ảnh |
| Guideline | Hai bản cá nhân, guideline chung v1.0 và taxonomy v1.0; rules giữ nguyên |
| Nhãn và phân công | Hai COCO 101/102, assignment.csv và hai danh sách ảnh; mỗi file đủ 40 ảnh |
| Ghi chú cá nhân | submission/individual_notes/101.md và 102.md; phần tôi giữ sáu mục theo mẫu |
| Báo cáo QC | submission/qc/QC_REPORT.md; đủ trường theo mẫu, quyết định Hold |
| Nguồn và dấu vết sửa | Hai provenance và annotation_corrections_101.csv; lịch sử ngày 2026-11-16 được giữ |
| So sánh bản sửa | review_comparison_101_102.json/.md; ghi bối cảnh kế thừa nguồn |
| Vấn đề cấp ảnh | image_issues.csv; phần xe/gương sát biên dưới ảnh 040 |

## Tệp tôi bổ sung trong lần nộp này

Tôi chạy qc_compare.py trên hai COCO hiện tại và giữ nguyên các đầu ra do script sinh.

| Tệp trong submission/qc/ | Nội dung |
|---|---|
| iaa_summary.json, iaa_summary.md | 40 ảnh, 80/80 lượt có file, 342 cặp; IoU TB 1.0000, cùng lớp 336/342 |
| calibration_candidates.csv | 604 ca trên 35 ảnh, mỗi ca có case_id |
| image_scores.csv | Điểm ưu tiên rà soát theo ảnh |
| flagged_images.txt | Danh sách 35 ảnh cần calibration |
| consensus_draft.json | Nháp đồng thuận tự động, giữ đủ 40 ảnh |
| calibration_decisions.csv | 604 dòng có case_id và ảnh; các trường quyết định chờ nhóm điền |
| calibration_context.json | Checksum khóa kết quả so sánh dùng cho bảng quyết định |

Tôi đã sinh overlay cho 35 ảnh tại work/viz/. Có thể chạy lại bằng `python -X utf8 scripts/viz_disagreement.py --images flagged`.

Hai bản nhãn dùng chung nguồn, nên tôi diễn giải chỉ báo “ĐẠT” trong đầu ra script như kết quả vượt ngưỡng số học trên hai file hiện có. Điều kiện gán thủ công độc lập theo RULES Day07 cần được đánh giá riêng. 604 ca gồm 580 cờ can_review, 8 ca bỏ sót/thừa, 9 ca thuộc tính, 6 ca lớp và 1 vấn đề cấp ảnh; chưa phải 604 lỗi được nhóm xác nhận.

## Tệp còn thiếu và việc cần làm

| Tệp hoặc nhóm tệp | Phần còn thiếu | Người thực hiện |
|---|---|---|
| submission/guidelines/guideline_v1.1_calibrated.md | Chốt guideline sau khi giải quyết các ca calibration | Nhóm 101–102 |
| submission/guideline_change.json | Ghi thay đổi editorial/semantic của bản v1.1 đã chốt | Nhóm 101–102 |
| submission/qc/labels_calibrated.json | Sửa nhãn theo quyết định rồi chạy build_final.py | Nhóm 101–102 |
| submission/qc/labels_calibrated.csv | Sinh cùng nhãn cuối bằng build_final.py | Nhóm 101–102 |
| submission/qc/batch_manifest.json | Sinh manifest nguồn, phiên bản và checksum của nhãn cuối | Nhóm 101–102 |
| submission/qc/reviews/round-01/ | Mở vòng QC trên nhãn cuối, điền phiếu rồi sinh qc_result.json | Reviewer cuối do nhóm phân công |

Ngoài các tệp thiếu, 604 dòng trong calibration_decisions.csv còn chờ quyết định, rule, phiên bản, người chốt, phiếu sửa và kiểm lại. taxonomy_v1.1.json chỉ cần nếu nhóm đổi schema. Bản hiện tại giữ taxonomy v1.0.

## Kết quả kiểm tra

- `python -X utf8 scripts/validate_labels.py --all` đạt cho 101 và 102.
- `python -X utf8 scripts/make_cvat_labels.py` kiểm schema và sinh cấu hình CVAT thành công.
- `python -X utf8 scripts/qc_compare.py` chạy thành công; bằng chứng đầu vào và checksum lưu trong iaa_summary.json.
- `python -X utf8 scripts/build_final.py` đã tạo bảng quyết định và context, sau đó dừng tại guideline_change.json chưa có. Chưa tạo nhãn cuối từ các quyết định còn trống.
- `python -X utf8 scripts/check_submission.py --round 1` còn hai lỗi về số vòng QC và qc_result.json. Bảng thiếu tệp mô tả cả các bước chưa tới trong pipeline.
- Bộ kiểm thử workflow trước lần bổ sung đã đạt 20/20 trên Linux. Lần này tôi bổ sung hồ sơ và chạy các lệnh kiểm dữ liệu, không thay mã script.

Tôi nộp bổ sung trên main của repo nhóm hiện có, giữ trạng thái **Hold** tới khi hoàn thiện calibration và QC. Repo hiện là public fork; yêu cầu kênh riêng tư và xác nhận nhận bài theo hướng dẫn coach trong SUBMISSION.md.
