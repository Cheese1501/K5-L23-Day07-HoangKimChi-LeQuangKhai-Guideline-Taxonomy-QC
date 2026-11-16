# Tiến độ Lab Day 07 — thành viên 101

- **Mã thành viên:** 101
- **Ngày cập nhật:** 2026-11-16
- **Phạm vi:** assignment, ảnh và tài liệu riêng của 101.
**Trạng thái tổng thể:** tài liệu đã chuẩn bị để 101 đối chiếu; guideline/annotation chính thức còn chờ 101 tự rà soát và nhóm chốt.

## 1. Kết quả đã chuẩn bị

| Hạng mục | Trạng thái | Bằng chứng |
|---|---|---|
| Assignment và ảnh 101 | `COMPLETED` | `submission/qc/assignments/101.txt` có 40 tên ảnh duy nhất; `work/101/images/` có 40 ảnh duy nhất và khớp danh sách. |
| Phân tích ảnh | `PREPARED` | `IMAGE_ANALYSIS.md` có một mục cho từng `img_001.jpg`–`img_040.jpg`, bao gồm class ứng viên, vật ngoài taxonomy, tình huống đặc biệt, box/attributes và lý do đề xuất. |
| Guideline cá nhân | `PREPARED` | `submission/guidelines/individual/guideline_101.md` diễn giải class v0, bounding box, thuộc tính, ca khó, QC và kết luận. Các quy tắc đề xuất mang mã `I101-xx`, không phải rule nhóm. |
| Ghi chú cá nhân | `PREPARED` | `submission/individual_notes/101.md` có các điểm mơ hồ, ca khó tiêu biểu, đề xuất/rủi ro/QC, nội dung calibration và cách dùng công cụ. Không ghi nhận hoạt động chưa xảy ra. |
| Taxonomy/CVAT cấu hình | `PREPARED` | `submission/taxonomy.json` vẫn là `v0`. `cvat/labels_generated.json` có đúng sáu class v0; năm class object có `occluded_level`, `truncated`, `can_review`, còn `ignore_region` không có attributes. Đây chưa phải taxonomy nhóm v1.0. |

## 2. Kết quả rà soát ảnh

Đã lập bảng cho đủ 40 ảnh dựa trên nội dung trực quan của các ảnh gốc và đối chiếu các ca cần phân tích kỹ hơn, gồm xe chở xe (`img_002`), nhiều người/xe máy chồng lấp (`img_005`), tượng (`img_017`), người trên xe máy và tranh nền (`img_026`), xe diễu hành/mascot (`img_019`), pickup chở ngựa (`img_028`), bãi xe đông (`img_030`) và người ở tiền cảnh trước taxi (`img_040`).

Các nhóm cần đối chiếu với v1.0: bus/minibus, tuk-tuk/auto-rickshaw, xe đạp/xích lô, pickup/van/truck, tượng/mannequin/đồ chơi/hình in, phản chiếu và vật dưới 20 px. Không có tọa độ hoặc nhãn COCO nào được tạo.

## 3. CVAT và annotation

- Hướng dẫn cấu hình, tạo task và export COCO có trong `docs/CVAT_SETUP.md`.
- Assignment và bản sao ảnh khớp: **40/40**, không thiếu/thừa.
- `submission/labels/101.json`: **chưa có**.
- Đăng nhập instance CVAT của lớp, tạo task, upload, vẽ box và export của 101: **chưa được xác nhận**.
- Nhãn chính thức: `BLOCKED_HUMAN` cho tới khi guideline/taxonomy nhóm `v1.0` được nhóm chốt và thành viên 101 thực hiện annotation độc lập trong CVAT.

## 4. Kiểm tra và bằng chứng

- Số tên assignment: 40; số tên duy nhất: 40.
- Số ảnh trong `work/101/images/`: 40; số ảnh duy nhất: 40.
- Tập tên assignment và tập tên ảnh trong thư mục làm việc trùng khớp.
- Taxonomy còn `v0`; không sửa class, attributes hoặc `rules`.
- Chưa có COCO của 101 nên chưa chạy `validate_labels.py submission/labels/101.json`.
- Không tạo kết quả IAA, calibration, QC review hoặc Release.
- Đã kiểm tra tài liệu CVAT và taxonomy; chưa xác minh quyền truy cập instance CVAT bên ngoài.

## 5. Công việc còn lại của thành viên 101

1. Rà lại 40 ảnh gốc và sửa mô tả trong `IMAGE_ANALYSIS.md` nếu có điểm không khớp.
2. Đọc guideline 101, chỉnh quy tắc cá nhân nếu cần và chỉ gửi phiên bản đã tự xác nhận.
3. Thảo luận với nhóm về phương tiện thiếu class, xe được chở, ngưỡng `occluded_level` và phạm vi `ignore_region`.
4. Chờ khóa guideline/taxonomy v1.0; không dùng v0 cho annotation chính thức nếu quy trình yêu cầu v1.0.
5. Sau khi v1.0 được chốt, tạo task riêng trong CVAT, gán nhãn độc lập cả 40 ảnh, export COCO vào `submission/labels/101.json` và chạy validator.
6. Chỉ cập nhật ghi chú về hoạt động đã thực hiện; không thêm số liệu IAA/QC/calibration khi chưa có kết quả thật.

## 6. Mức độ sẵn sàng nộp bài

**NOT READY.** Tài liệu đã có nội dung để 101 đọc, đối chiếu và chỉnh sửa, nhưng chưa thay thế việc 101 tự rà soát và xác nhận, quyết định guideline/taxonomy v1.0 của nhóm, annotation thật trong CVAT hoặc các artifact của những pha sau. Quyền truy cập CVAT bên ngoài cũng chưa được xác minh.

## 7. Final audit 2026-11-16

Đã thực hiện vòng AI audit: đọc yêu cầu/rubric, mở riêng 40 tệp ảnh gốc và sửa các lỗi có căn cứ trong ba tài liệu nội dung. Xem [FINAL_AUDIT_101.md](FINAL_AUDIT_101.md) để biết từng ảnh, tiêu chí, lỗi sửa và kết quả kiểm thử thực tế. Đây chưa phải xác nhận của 101.

Trạng thái tài liệu: **READY FOR 101 REVIEW**; trạng thái hoàn tất lab/nộp đầy đủ vẫn **NOT READY**. Các điểm ảnh chưa rõ, xác nhận cá nhân, annotation thật và các pha nhóm còn thiếu được ghi riêng trong báo cáo.
