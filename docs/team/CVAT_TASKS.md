# Task thực hành độc lập — nhóm 101–102

CVAT local: http://localhost:8080, phiên bản đã chuẩn bị 2.74.1. Các liên kết chỉ mở trên máy chạy CVAT; đây là hướng dẫn thao tác, không phải bằng chứng đã hoàn thành gán nhãn.

**Cập nhật2026-11-16:** Task15 và16 theo phân công cũ hiện trả về404, không còn mở được. Cần chuẩn bị lại Task riêng nếu tiếp tục lượt gán thủ công độc lập; bảng dưới chỉ lưu tham chiếu cũ. Không thay Task độc lập bằng bản nhãn AI.

Task review 101 hiện tại, cập nhật ngày 2026-11-17, là [Task19/Job14](http://localhost:8080/tasks/19/jobs/14), kế thừa backup đã review của 102 rồi sửa theo guideline v1.0. COCO 40 ảnh/344 annotation nằm ở `submission/labels/101.json`, trạng thái Hold. Nguồn và giới hạn trong `submission/qc/annotation_provenance_101.json`. Bản cũ từ [Task17/Job12](http://localhost:8080/tasks/17/jobs/12) được giữ tại `submission/qc/history/20261116/`.

| Mã | Task | Job | Phân công |
|---|---|---|---|
| 101 | [Task 15](http://localhost:8080/tasks/15) | [Job 10](http://localhost:8080/tasks/15/jobs/10) | img_001.jpg–img_040.jpg |
| 102 | [Task 16](http://localhost:8080/tasks/16) | [Job 11](http://localhost:8080/tasks/16/jobs/11) | img_001.jpg–img_040.jpg |

1. Kiểm Task đúng mã, đủ 40 ảnh và cấu hình từ `cvat/labels_generated.json`.
2. Tự vẽ box theo [guideline v1.0](../../submission/guidelines/guideline_v1.0_agreed.md); không dùng pre-label hoặc xem nhãn người kia.
3. Box hợp lý nhưng chưa chắc thì can_review; chưa xác định được box/class thì ghi ảnh, vùng và lý do riêng.
4. Save, export COCO 1.0, tắt Save images; lưu `submission/labels/<mã>.json`, giữ cả ảnh không có box.
5. Chạy validator cho bản cá nhân và nộp riêng. Chỉ tập hợp nhãn sau khi cả hai hoàn tất.

Quy trình đầy đủ theo [GUIDE.md](../../GUIDE.md) và [CVAT_SETUP.md](../CVAT_SETUP.md).
