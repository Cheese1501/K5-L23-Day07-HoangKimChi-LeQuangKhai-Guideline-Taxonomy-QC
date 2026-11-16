# Day 07 Lab — Kiểm toán repository

**Trạng thái:** Audit tại workspace ngày 2026-11-16. Đây là báo cáo tình trạng, không phải xác nhận hoàn thành lab.

## Tóm tắt

- Mục tiêu: viết guideline gán nhãn 2D, thống nhất taxonomy, gán độc lập 40 ảnh trên CVAT, đo IAA, calibration có truy vết và review QC toàn lô trước khi bàn giao.
- Nhóm: hai mã thành viên đã được xác nhận là `101` và `102`. Họ tên không được ghi vào artifact nộp.
- Submission hiện **NOT READY**: chưa có guideline đã viết độc lập, COCO, IAA, quyết định calibration, nhãn cuối, QC review hay báo cáo hoàn chỉnh.
- Đã tạo phân công chính thức: 40 ảnh × 2 người = 80 lượt; mỗi thành viên được giao đủ 40 ảnh.
- Không tạo annotation, IAA, QC result hay quyết định Release.

## Bằng chứng kiểm tra

| Thành phần | Kết quả | Bằng chứng / ghi chú |
|---|---|---|
| Git lúc bắt đầu audit | COMPLETED | `git status --short` không có thay đổi trước audit. |
| Python | COMPLETED | Python 3.13.17; đáp ứng yêu cầu Python 3.9+. |
| Dependencies | COMPLETED | Pillow 13.0.0, jsonschema 4.26.0 đã import được; phù hợp `requirements.txt`. |
| Ảnh | COMPLETED | 40 JPEG được Pillow mở và `verify()` thành công. Không sửa/đổi tên ảnh. |
| Ghi công | COMPLETED | 40 ảnh, 40 dòng trong `data/ATTRIBUTION.csv`; không thiếu/không dư tên ảnh. |
| Taxonomy hiện tại | COMPLETED | `submission/taxonomy.json` đang là `v0`, hợp lệ với `schemas/taxonomy.schema.json`; các ngưỡng `rules` được giữ nguyên. Đây chưa phải taxonomy v1.0 đã được nhóm chốt. |
| CLI của script | COMPLETED | 9 script có giao diện CLI trả về help thành công khi đặt encoding UTF-8. `prepare_calibration.py` không có giao diện `--help`; chạy không tham số yêu cầu `iaa_summary.json`, nên không chạy để tránh giả lập đầu vào. |
| Cú pháp Python | COMPLETED | `python -m compileall -q scripts tests` trả về 0. |
| Baseline tests | BLOCKED_ENVIRONMENT | 19/20 test qua khi bật `PYTHONUTF8=1`; test `test_assignment_rejects_unsafe_member_and_symlink_destination` lỗi `WinError 1314` khi Windows không cấp quyền tạo symlink. Chạy không bật UTF-8 gây lỗi mã hóa đầu ra/đọc file trong môi trường console hiện tại. |
| CVAT | BLOCKED_HUMAN | Không có phiên đăng nhập/instance CVAT được kiểm chứng trong phiên này. Nhóm cần đăng nhập CVAT lớp và xác nhận quyền tạo Project/Task, upload và export COCO. |
| Assignment | COMPLETED | `submission/qc/assignment.csv`, `submission/qc/assignments/101.txt`, `102.txt`; 40 ảnh duy nhất, mỗi ảnh có hai annotator. Kết quả lặp lại được với seed mặc định 42. |
| Bản sao ảnh làm việc | COMPLETED | `work/101/images/` và `work/102/images/`, mỗi thư mục 40 ảnh. Thư mục `work/` bị loại khỏi submission theo `.gitignore` và hướng dẫn nộp bài. |
| Nhãn độc lập | BLOCKED_HUMAN | Chưa có `submission/labels/101.json` hoặc `102.json`. Không sinh nhãn giả. |
| IAA / calibration / QC | BLOCKED_HUMAN | Không đủ nhãn và bằng chứng người review; không chạy script downstream. |

## Quy trình bắt buộc và tiêu chí chấm

1. Mỗi người đọc 40 ảnh và viết guideline cá nhân độc lập trước khi thảo luận.
2. Nhóm họp, thống nhất guideline v1.0 và taxonomy; giữ nguyên mục `rules` theo `RULES.md` và schema.
3. Gán độc lập theo assignment; với nhóm hai người, từng ảnh có hai nhãn. Validate từng COCO.
4. Chạy IAA sau khi đủ nhãn. IoU/lớp/thuộc tính trên các cặp box ghép; box chưa ghép và vùng ignore báo riêng.
5. Người thật xem các ca bất đồng, ghi từng quyết định calibration, cập nhật guideline và tạo nhãn cuối.
6. Reviewer xem toàn bộ 40 ảnh, ghi phiếu review; báo cáo có mẫu số, quyết định Hold/Rework/Release dựa trên bằng chứng.
7. Chạy `check_submission.py` theo vòng QC cuối; không nộp `work/`, thông tin cá nhân hoặc đăng nhập.

Rubric 100 điểm chia thành guideline cá nhân (15), guideline/taxonomy nhóm (20), phân công/gán nhãn (15), IAA/calibration (25), QC/report (15), tái lập/hợp tác (10). Hold hoặc Rework có căn cứ là kết quả hợp lệ.

## Tài liệu và diễn giải

- Quy trình/nộp bài chính được lấy từ `GUIDE.md`, `RULES.md`, `RUBRIC.md`, `SUBMISSION.md`, schema và `scripts/README.md`.
- `K5-L23-Day07-Guideline-Taxonomy-QC.md` có các ví dụ lớp/ngưỡng và số liệu từ lượt chạy minh họa (bao gồm ví dụ 3 mã thành viên). Không dùng những số liệu mẫu làm kết quả nhóm này. Đề xuất lớp mới/ngưỡng trong tài liệu đó cần được hai thành viên xem ảnh và thống nhất; không tự đưa vào taxonomy.
- Mục `rules` hiện bị ràng buộc bằng `const` trong JSON Schema. Không thay đổi bất kỳ ngưỡng nào.
- `check_submission.py` chỉ kiểm một số hình thức/đối chiếu artifact. Nó không thay thế việc người thật xem ảnh, xác nhận guideline cá nhân, hoặc reviewer xác nhận QC.

## Hạn chế môi trường và cách chạy

Console hiện dùng code page không biểu diễn được một số ký tự tiếng Việt. Trong PowerShell, đặt encoding trước khi chạy script và test:

```powershell
$env:PYTHONUTF8 = '1'
$env:PYTHONIOENCODING = 'utf-8'
```

Test symlink cần quyền Windows tương ứng (ví dụ Developer Mode hoặc chính sách/quyền tạo symlink). Không bỏ test và không thay đổi kiểm tra bảo mật chỉ để làm suite xanh.

## Trạng thái đầu ra

- `TEAM.md`: đã điền hai mã 101/102; phân công điều phối/reviewer và kết quả cuối còn chờ nhóm.
- `submission/guidelines/individual/guideline_101.md`, `guideline_102.md`: cấu trúc đã chuẩn bị, chưa phải guideline cá nhân.
- `submission/individual_notes/101.md`, `102.md`: cấu trúc đã chuẩn bị, chưa có ghi chép cá nhân.
- `submission/taxonomy.json`: giữ nguyên `v0`; chưa tuyên bố AGREED.
- CVAT labels v0 có sẵn từ repo; không tái sinh nhãn Project trước khi taxonomy v1.0 được nhóm duyệt.
- Submission cuối: **NOT READY**; xem `LAB_PROGRESS.md` và `LAB_FINAL_REPORT.md`.
