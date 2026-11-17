# Task và bản xuất của nhóm 101–102

Chúng tôi dùng CVAT local tại http://localhost:8080, phiên bản 2.74.1. Liên kết CVAT mở trên máy chạy dịch vụ; các COCO trong repo là bản bàn giao để đối chiếu.

| Nội dung | Task / Job trên máy hiện tại | Bản trong repo |
|---|---|---|
| Bài review của tôi — 101 | [Task19/Job14](http://localhost:8080/tasks/19/jobs/14), DAY07-101-REVIEW-40frames | submission/labels/101.json, 40 ảnh/344 annotation |
| Backup 102 đã khôi phục | [Task18/Job13](http://localhost:8080/tasks/18/jobs/13), DAY07-102-REVIEWED-40frames | submission/labels/102.json, 40 ảnh/352 annotation; export nguồn ghi nhận Task35/Job34 trong provenance của 102 |

Tôi dùng backup 102 để thực hiện lượt review 101 với công cụ hỗ trợ, lưu 21 chỉnh sửa trên 13 ảnh theo guideline v1.0. Nguồn, checksum và nhật ký tại submission/qc/annotation_provenance_101.json và annotation_corrections_101.csv.

Task15/16 theo phân công cũ trả 404 ở lần kiểm trước. Bản 101 cũ từ [Task17/Job12](http://localhost:8080/tasks/17/jobs/12) được giữ trong submission/qc/history/20261116/ để truy lại lịch sử.

## Đối chiếu và tiếp tục làm bài

1. Kiểm đủ 40 ảnh theo submission/qc/assignments/<mã>.txt, dùng cấu hình cvat/labels_generated.json.
2. Dùng guideline chung v1.0 để kiểm class, phần nhìn thấy, mức che, cắt biên và cờ review. Vùng chưa xác định box/class ghi trong image_issues.csv.
3. Save và export COCO 1.0, tắt Save images, giữ cả ảnh không có đối tượng.
4. Chạy validator, rồi chạy lại so sánh khi hai bản đầu vào thay đổi. Lưu bảng quyết định cũ trước khi tạo context mới.
5. Nhóm chúng tôi hoàn thiện calibration, chốt v1.1, tạo nhãn cuối và mở vòng QC theo GUIDE.md.

Quy trình gán thủ công độc lập của lab trong [GUIDE.md](../../GUIDE.md) và [CVAT_SETUP.md](../CVAT_SETUP.md). Bối cảnh cùng nguồn của lượt review hiện tại được ghi trong báo cáo QC và ghi chú cá nhân.
