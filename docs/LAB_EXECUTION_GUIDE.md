# Hướng dẫn thực thi Day 07 — nhóm 101/102

Tài liệu này bổ sung cách chạy lab trên Windows và ghi rõ điểm nào cần người xác nhận. Quy trình chính vẫn là `GUIDE.md`; luật nộp và rubric trong `RULES.md`, `SUBMISSION.md`, `RUBRIC.md` là tiêu chuẩn.

## Mã và độc lập

- `101` và `102` là mã đã xác nhận. Không ghi họ tên, email, mã học viên hay tài khoản vào artifact nộp.
- Hai người phải viết guideline riêng và gán nhãn riêng. Không trao đổi cách gán trước khi nộp riêng ở Pha 1 và Pha 3.
- AI/tài liệu có thể hỗ trợ hiểu quy trình và lỗi lệnh; quyết định box/lớp và review ảnh Day 07 do người thật thực hiện.

## 0. Môi trường và assignment đã chuẩn bị

Trong PowerShell mở ở thư mục gốc repo, đặt UTF-8 cho output tiếng Việt và cài dependency nếu máy chưa có:

```powershell
$env:PYTHONUTF8 = '1'
$env:PYTHONIOENCODING = 'utf-8'
python --version
python -m pip install -r requirements.txt
```

Assignment đã được tạo bằng:

```powershell
python scripts/split_assign.py --members 101,102 --copy-images
```

Kết quả hiện có: `submission/qc/assignment.csv` gồm 40 ảnh, mỗi ảnh có `101|102`; danh sách riêng ở `submission/qc/assignments/101.txt` và `102.txt`; mỗi người được giao 40 ảnh. Các ảnh đã copy vào `work/101/images/` và `work/102/images/`. **Không nộp `work/`.**

## 1. Guideline cá nhân — mỗi người tự làm

1. Mở `data/images/`, xem từng ảnh `img_001.jpg` tới `img_040.jpg`; chưa mở nhãn của người kia.
2. Hoàn thiện file khung tương ứng:
   - `submission/guidelines/individual/guideline_101.md`
   - `submission/guidelines/individual/guideline_102.md`
3. Với từng ca khó ghi ID ảnh, quyết định ban đầu và lý do. Xem xét người đi xe máy, xe chở xe, che/cắt mép, vật nhỏ, tượng/hình in/đồ chơi/phản chiếu, thuộc tính và ignore region.
4. Gửi riêng theo hướng dẫn của coach. File hiện tại chỉ là template; không nộp nếu chưa được chính thành viên hoàn thiện.

## 2. Họp chốt guideline/taxonomy v1.0

1. Chỉ họp sau khi cả hai đã gửi bản cá nhân; so sánh bất đồng và chốt rule bằng ID `R-01`, `R-02`, …
2. Tạo `submission/guidelines/guideline_v1.0_agreed.md`; chỉ ghi **AGREED** khi cả hai xác nhận.
3. Cập nhật `submission/taxonomy.json` cho khớp. Giữ nguyên từng giá trị trong `rules` (schema cũng khóa các ngưỡng).
4. Sau khi xác nhận, chạy:

   ```powershell
   python scripts/make_cvat_labels.py
   ```

5. Trong CVAT, tạo Project từ `cvat/labels_generated.json`; kiểm tên lớp và thuộc tính.

Các tên lớp/ngưỡng gợi ý trong tài liệu hướng dẫn dài là ví dụ thảo luận, không thay quyết định của nhóm.

## 3. Gán nhãn độc lập trên CVAT

1. Mỗi người tạo Task riêng từ ảnh trong `work/<mã>/images/`; số frame phải bằng 40 và trùng danh sách phân công.
2. Gán theo đúng guideline v1.0. Chưa chắc thì đánh dấu `can_review`; chưa thể vẽ box thì ghi vấn đề cấp ảnh vào `submission/qc/image_issues.csv` sau khi cả hai khóa nhãn.
3. Ảnh không có vật vẫn phải hiện trong COCO. Export COCO 1.0, tắt Save images, lấy `annotations/instances_*.json`, lưu thành:
   - `submission/labels/101.json`
   - `submission/labels/102.json`
4. Mỗi người chỉ gửi file của mình riêng trước khi tập hợp.
5. Sau khi cả hai đã nộp, chạy:

   ```powershell
   python scripts/validate_labels.py submission/labels/101.json
   python scripts/validate_labels.py submission/labels/102.json
   python scripts/validate_labels.py --all
   ```

## 4. IAA và calibration

Chỉ sau khi validate pass đủ hai file:

```powershell
python scripts/qc_compare.py
python scripts/viz_disagreement.py --images flagged
```

Đọc `submission/qc/iaa_summary.md`, `calibration_candidates.csv`, `flagged_images.txt` và ảnh overlay `work/viz/`. Ghi rõ mẫu số. IAA trên matched pairs không kiểm chứng vật cùng bị bỏ sót hoặc hai người cùng hiểu sai; xem ảnh gốc và guideline.

Không dùng số liệu minh họa trong `K5-L23-Day07-Guideline-Taxonomy-QC.md` như số liệu của nhóm này. Khi cả nhóm thực sự xem từng ca, chạy quy trình calibration:

```powershell
python scripts/build_final.py
python scripts/prepare_calibration.py
```

Điền từng dòng quyết định có mã quy tắc, người chốt và kiểm lại. Sửa ảnh trong CVAT, export đúng đường dẫn có phiên bản/hash do script in. Nếu quy tắc thay đổi ngữ nghĩa, ghi `kind=semantic`, đánh phạm vi `lo` và rà cả lô. Không tự điền quyết định cho ca chưa được xem.

Sau khi đủ đầu vào và COCO hiệu chỉnh hợp lệ:

```powershell
python scripts/build_final.py
```

Kiểm tra `labels_calibrated.json`, `labels_calibrated.csv`, `batch_manifest.json`.

## 5. Review QC và bàn giao

1. Sau khi có nhãn cuối:

   ```powershell
   python scripts/qc_sample.py --round 1
   ```

2. Mở ảnh trong `work/review/round-01/`; reviewer xem đủ 40 ảnh rồi ghi `submission/qc/reviews/round-01/qc_review.csv`. Không tạo dòng `khong` trước khi thật sự xem ảnh.
3. Nhóm hai người nên đổi vai; reviewer ghi mã của mình ở mọi dòng. Với lỗi, ghi loại lỗi, `rule_id`, vùng/object id và ghi chú.
4. Tạo báo cáo:

   ```powershell
   python scripts/qc_report.py --round 1
   ```

5. Điền `submission/qc/QC_REPORT.md`, hai cá nhân tự hoàn thiện `submission/individual_notes/<mã>.md`, rồi:

   ```powershell
   python scripts/check_submission.py --round 1
   ```

6. Nếu Rework, giữ vòng 1, sửa theo phạm vi có bằng chứng, tạo `--round 2`, và bàn giao theo vòng cuối. Với 40 ảnh, một ảnh lỗi là `1/40 = 2.5%`, vượt ngưỡng 2%. Lấy mẫu demo không đủ điều kiện Release.

## Chờ thao tác người thật

- Đăng nhập và xác nhận quyền trên CVAT instance của lớp.
- Tự xem 40 ảnh và viết/gửi riêng hai guideline.
- Họp và xác nhận guideline/taxonomy v1.0.
- Vẽ box cho cả hai bộ COCO, duyệt bất đồng/calibration, và reviewer xem QC toàn lô.
- Điền quyết định, ghi chú cá nhân, báo cáo và quyết định bàn giao dựa trên bằng chứng.
