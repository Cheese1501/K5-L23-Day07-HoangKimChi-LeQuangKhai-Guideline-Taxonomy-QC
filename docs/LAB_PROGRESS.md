# Day 07 Lab — Tiến độ

**Cập nhật:** 2026-11-16  
**Mã nhóm:** `101`, `102`  
**Trạng thái tổng:** PREPARED / BLOCKED_HUMAN — chưa có nhãn độc lập hoặc review QC.

## Cách tính tiến độ

Tỷ lệ dưới đây đếm các mốc kiểm chứng được trong danh sách 30 mốc của 8 pha (0–7). Một mẫu/template hoặc phân công không được tính là gán nhãn, quyết định hay QC. Mốc chỉ hoàn thành khi có artifact/bằng chứng tương ứng.

**Đã hoàn thành 7/30 mốc = 23.3%** (làm tròn 23%). Đây là tiến độ chuẩn bị và kiểm chứng cục bộ, **không** có nghĩa submission đã hoàn thành 23% về chất lượng nhãn.

## Theo pha

| Pha | Tiến độ | Trạng thái | Bằng chứng / việc còn lại |
|---|---:|---|---|
| 0. Audit môi trường và repo | 5/7 = 71% | BLOCKED_ENVIRONMENT | Python/dependencies, Git, 40 ảnh + attribution, taxonomy schema, CLI/syntax đã kiểm. Full test suite thiếu quyền symlink ở 1 test; CVAT chưa được đăng nhập/xác nhận. |
| 1. Guideline cá nhân | 1/3 = 33% | BLOCKED_HUMAN | Đã tạo cấu trúc cho 101/102. Mỗi người cần tự xem đủ 40 ảnh, viết/hoàn thiện guideline và gửi riêng. |
| 2. Guideline/taxonomy chung | 0/4 = 0% | BLOCKED_HUMAN | Chờ hai bản cá nhân, buổi họp, xác nhận AGREED, taxonomy v1.0 và kiểm CVAT Project. |
| 3. Assignment và annotation độc lập | 1/4 = 25% | IN_PROGRESS / BLOCKED_HUMAN | Assignment đã tạo. Hai người cần gán đủ 40 ảnh, export COCO, validate và nộp riêng. |
| 4. IAA và bất đồng | 0/2 = 0% | BLOCKED_HUMAN | Chỉ chạy khi có đủ nhãn độc lập hợp lệ. |
| 5. Calibration/nhãn cuối | 0/4 = 0% | BLOCKED_HUMAN | Chờ IAA và con người xem/chốt từng ca, sửa nếu cần và kiểm lại. |
| 6. QC review | 0/4 = 0% | BLOCKED_HUMAN | Chờ nhãn cuối; reviewer cần xem đủ 40 ảnh và ký xác nhận bằng mã. |
| 7. Submission/final verification | 0/2 = 0% | NOT_STARTED | Chờ đủ artifact, báo cáo, ghi chú cá nhân và quyết định QC. |

Pha 0 vẫn chưa qua gate đầy đủ; tỷ lệ pha chỉ cho thấy số mốc đã kiểm chứng, không thay thế kết quả test/CVAT còn thiếu.

## Việc đã thực hiện

- Kiểm tra cấu trúc repo, Git ban đầu sạch, Python 3.13.17 và dependency versions.
- Xác thực 40/40 ảnh đọc được, 40/40 dòng attribution khớp; taxonomy v0 pass schema.
- `compileall` và 9 lệnh `--help` chạy với UTF-8 thành công.
- Chạy tests: 19/20 thành công ở UTF-8 mode; một test lỗi vì Windows không cấp quyền tạo symlink.
- Tạo `assignment.csv` theo `--members 101,102 --copy-images`; 40 ảnh đều có hai người được giao, mỗi người 40 ảnh.
- Tạo file khung guideline cá nhân và ghi chú 101/102; các file được đánh dấu PREPARED_TEMPLATE.
- Điền mã 101/102 vào `TEAM.md`; các trường cần quyết định của nhóm vẫn chờ người.

## Hành động tiếp theo

1. **101 và 102:** hoàn thành guideline cá nhân độc lập, gửi riêng trước khi thảo luận.
2. **Cả nhóm:** thống nhất và khóa guideline/taxonomy v1.0; không thay mục `rules`.
3. **101 và 102:** kiểm CVAT, gán 40 ảnh theo assignment, export COCO riêng, chạy validate và gửi riêng.
4. **Cả nhóm:** sau khi nộp độc lập mới chạy IAA và cùng xem bất đồng.
5. **Reviewer:** duyệt đủ 40 ảnh theo vòng, hoàn thành phiếu và báo cáo. Chỉ khi đủ bằng chứng mới chọn Release.

Lệnh thao tác theo thứ tự có trong `LAB_EXECUTION_GUIDE.md`; kết quả kiểm toán trong `LAB_AUDIT.md`.
