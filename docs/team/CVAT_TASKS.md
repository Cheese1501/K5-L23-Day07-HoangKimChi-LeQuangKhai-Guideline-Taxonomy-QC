# Pha 3 — Project và Task gán độc lập của nhóm 101–102

- Ngày chuẩn bị: 2026-11-16.
- Guideline và taxonomy dùng khi gán: **v1.0 đã khóa**, theo xác nhận chung của người dùng rằng cả 101 và 102 đã đồng ý toàn bộ bản r1.
- CVAT local: http://localhost:8080, phiên bản 2.74.1.
- Project: [day07-team-101-102-v1.0 — ID2](http://localhost:8080/projects/2).

## 1. Phân công thao tác

| Thành viên | Task | Job để bắt đầu vẽ | Ảnh được giao |
|---|---|---|---|
| 101 | [Task 15 — day07-101-independent-v1.0](http://localhost:8080/tasks/15) | [Job 10](http://localhost:8080/tasks/15/jobs/10) | 40 ảnh, img_001.jpg–img_040.jpg |
| 102 | [Task 16 — day07-102-independent-v1.0](http://localhost:8080/tasks/16) | [Job 11](http://localhost:8080/tasks/16/jobs/11) | 40 ảnh, img_001.jpg–img_040.jpg |

Mỗi người chỉ làm Task đúng mã của mình, không xem nhãn người kia trước khi nộp riêng. TênTask thể hiện phân công học tập; chưa thay thế việc nhóm cấp đúng tài khoản/quyền truy cập cho từng người. Không tạo thêm tài khoản hoặc thay quyền trong lần chuẩn bị này. Các liên kết localhost mở trên máy đang chạy CVAT; máy khác cần địa chỉ instance được nhóm cấp quyền phù hợp, không tự mở cổng/chia sẻ ra ngoài.

## 2. Nội dung đã kiểm tra

Hai Task đều có đúng 40 frame, tên và thứ tự ảnh khớp assignment. Project có sáu lớp; năm lớp object có occluded_level/truncated/can_review đúng type/default/giá trị select; ignore_region không có attributes. CVAT lưu danh sách giá trị checkbox rỗng dưới dạng một chuỗi rỗng; checkbox vẫn có type checkbox, default false, không thay enum hay ý nghĩa thuộc tính.

Tại thời điểm kiểm tra, mỗi Task có **0 shapes, 0 tracks, 0 tags**. Đây là trạng thái trước gán, không phải40 ảnh đã hoàn thành hoặc đã đượcQC. Không có annotation do mô hình/AI tạo. CVAT có định dạng export COCO 1.0 được bật; chưa thực hiện export nhãn thật, vì hai người chưa gán.

## 3. Bắt đầu thực hành

1. Đăng nhập CVAT và mở Job đúng mã. Kiểm frame đầu/cuối, menu lớp và thuộc tính trước khi gán.
2. Đọc [guideline chung v1.0](../../submission/guidelines/guideline_v1.0_agreed.md), vẽ Rectangle theo phần nhìn thấy; người và xe tách riêng; giữ nguyên ngưỡng20px và bảng che0/dưới50%/từ50%/không xác định.
3. Có box hợp lý nhưng chưa chắc thì can_review. Chưa xác định được box/class thì ghi ảnh/vùng/lý do riêng; chỉ tập hợp issue sau khóa nhãn độc lập.
4. Save thường xuyên. Sau gán, từng người export COCO 1.0, tắt Save images, lưu đúng submission/labels/101.json hoặc 102.json, giữ ảnh không box.
5. Mỗi người chạy validator cho bản thật của mình và gửi riêng trước khi tập hợp. Chưa đo IAA hoặc calibration khi chưa đủ hai bản hợp lệ.

Hướng dẫn chi tiết: [ANNOTATION_PREPARATION.md](ANNOTATION_PREPARATION.md). Báo cáo học tập: [QC_REPORT.md](../../submission/qc/QC_REPORT.md); bổ sung trải nghiệm và số liệu thực hành sau khi có kết quả, không đưa thông tin đăng nhập vào tài liệu.
