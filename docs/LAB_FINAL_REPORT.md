# Day 07 Lab — Báo cáo trạng thái hiện tại

> **Đây là báo cáo trạng thái giữa kỳ, không phải xác nhận lab hoàn tất.**
> Submission: **NOT READY**. Không có nhãn, IAA, calibration, QC review hoặc quyết định Release được tạo trong phiên này.

## A. Trạng thái các pha

| Pha | Trạng thái | Tiến độ theo mốc | Bằng chứng |
|---|---|---:|---|
| 0. Audit | BLOCKED_ENVIRONMENT | 5/7 | Python/dependencies, 40 ảnh + attribution, taxonomy schema, CLI/syntax được kiểm. 19/20 test qua; test symlink cần quyền Windows; CVAT chưa được xác nhận. |
| 1. Guideline cá nhân | BLOCKED_HUMAN | 1/3 | Khung guideline 101/102 đã có; hai người cần tự hoàn thiện sau khi xem 40 ảnh. |
| 2. Guideline/taxonomy chung | BLOCKED_HUMAN | 0/4 | Cần so bản cá nhân và xác nhận AGREED. |
| 3. Assignment/annotation | BLOCKED_HUMAN | 1/4 | Assignment 40 ảnh × 2 đã được tạo. Chưa có hai COCO. |
| 4. IAA | BLOCKED_HUMAN | 0/2 | Chưa đủ nhãn độc lập. |
| 5. Calibration | BLOCKED_HUMAN | 0/4 | Chưa có ca hoặc quyết định được người thật xem. |
| 6. QC | BLOCKED_HUMAN | 0/4 | Chưa có nhãn cuối/reviewer evidence. |
| 7. Submission | NOT_STARTED | 0/2 | Chưa đủ artifact để chạy checker cuối. |

Theo checklist 30 mốc trong `LAB_PROGRESS.md`, 7/30 mốc đã hoàn thành (23%). Tỷ lệ này là phần chuẩn bị/kiểm chứng, không phải tỷ lệ chất lượng nhãn.

## B. Files đã tạo hoặc cập nhật

- `docs/LAB_AUDIT.md` — kết quả kiểm môi trường, repo, dữ liệu, taxonomy và test.
- `docs/LAB_PROGRESS.md` — trạng thái, cách tính tiến độ và blockers.
- `docs/LAB_EXECUTION_GUIDE.md` — thứ tự thao tác riêng cho mã 101/102, gồm lệnh PowerShell.
- `docs/LAB_FINAL_REPORT.md` — báo cáo trạng thái này.
- `TEAM.md` — thêm mã 101/102; phần điều phối/reviewer/kết quả còn chờ nhóm.
- `submission/qc/assignment.csv`, `submission/qc/assignments/101.txt`, `102.txt` — phân công deterministic; 40 ảnh mỗi người, hai người/ảnh.
- `work/101/images/`, `work/102/images/` — bản sao dùng upload CVAT; không đưa vào submission.
- `submission/guidelines/individual/guideline_101.md`, `guideline_102.md` và `submission/individual_notes/101.md`, `102.md` — cấu trúc PREPARED_TEMPLATE, không phải bằng chứng cá nhân đã hoàn thành.

## C. Test results

- **PASS:** 40 ảnh JPEG đọc/verify được; đủ 40 dòng attribution khớp tên file.
- **PASS:** taxonomy v0 qua `schemas/taxonomy.schema.json`; không thay đổi `rules`.
- **PASS:** `python -m compileall -q scripts tests`.
- **PASS:** 9 script CLI có `--help` chạy trong UTF-8 mode.
- **PASS:** 19/20 unit tests với `PYTHONUTF8=1`.
- **BLOCKED_ENVIRONMENT:** 1 test tạo symlink thất bại với `WinError 1314` (Windows yêu cầu quyền tạo symlink). Không sửa/bỏ test.
- **BLOCKED:** chạy checker cuối chưa phù hợp vì thiếu annotation, IAA, QC và báo cáo thật.

Lệnh PowerShell để tránh lỗi mã hóa console:

```powershell
$env:PYTHONUTF8 = '1'
$env:PYTHONIOENCODING = 'utf-8'
```

## D. Việc con người cần làm

| Ai | Việc | Input cần | Output/bằng chứng |
|---|---|---|---|
| 101 | Viết guideline cá nhân và gán nhãn độc lập | 40 ảnh, guideline v0, danh sách assignment 101 | `guideline_101.md`, COCO `101.json`, gửi riêng |
| 102 | Viết guideline cá nhân và gán nhãn độc lập | 40 ảnh, guideline v0, danh sách assignment 102 | `guideline_102.md`, COCO `102.json`, gửi riêng |
| 101 + 102 | Chốt guideline/taxonomy v1.0 sau khi gửi guideline riêng | Hai bản cá nhân, ảnh gốc, thảo luận ca biên | Guideline v1.0, taxonomy v1.0 được cả hai xác nhận |
| 101 + 102 | Họp IAA/calibration sau khi nộp hai COCO | Hai COCO hợp lệ và outputs của qc_compare | Quyết định mỗi ca, guideline v1.1 và nhãn cuối |
| Reviewer (nhóm phân công) | Xem đủ 40 ảnh và lập báo cáo | Nhãn cuối, guideline, rule IDs | Phiếu QC, báo cáo, quyết định có bằng chứng |
| Nhóm | Xác nhận CVAT/kênh nộp/điều phối | Tài khoản và yêu cầu của coach | Cấu hình hoạt động và trường TEAM hoàn chỉnh |

## E. Submission readiness

**NOT READY.** Điều kiện còn thiếu: CVAT access, hai guideline cá nhân đã gửi riêng, guideline/taxonomy v1.0, hai COCO độc lập, validate pass, IAA, quyết định và nhãn calibration, full-lot QC, individual notes, báo cáo và checker pass.

Không chạy `qc_compare.py`, `build_final.py`, `qc_sample.py`, `qc_report.py` hoặc `check_submission.py` để tạo kết quả hình thức trước khi có các đầu vào tương ứng.

## F. Git diff summary

Các file đã nêu ở mục B là thay đổi được tạo trong phiên này. `work/` bị `.gitignore`; không push/commit. Trước khi commit, nhóm cần xem `git status --short`, xác nhận guideline cá nhân đã được tự viết và chỉ thêm kết quả thật.
