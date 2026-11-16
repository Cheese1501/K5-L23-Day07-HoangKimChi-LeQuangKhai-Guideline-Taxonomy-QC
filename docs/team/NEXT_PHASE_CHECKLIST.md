# Checklist Pha 3 — annotation độc lập — nhóm 101–102

Ngày ghi nhận chuyển pha: 2026-11-16. Người dùng xác nhận: **“Cả hai đã đồng ý toàn bộ bản chung”**, đối với `team-v1.0-draft-2026-11-16-r1`. Bản quy tắc này được khóa thành v1.0, không tạo chữ ký riêng của từng thành viên.

## 1. Điều kiện và trạng thái

| Hạng mục | Trạng thái | Bằng chứng / việc tiếp theo |
|---|---|---|
| Nội dung guideline chung | READY | [v1.0 đã khóa](../../submission/guidelines/guideline_v1.0_agreed.md), R-01–11 |
| Đồng ý của cả 101 và 102 | READY | Xác nhận chung do người dùng cung cấp trong trao đổi chuyển Pha 3, ghi nhận ngày 2026-11-16 |
| Occlusion / scope / box / ignore | READY | Đã đồng ý toàn bộ quy tắc; giữ bảng 0 / 1 dưới 50% / 2 từ 50% / 3 không xác định, không tính truncation |
| Ca img_024/028/040 và trailer rời | READY về chính sách | Không suy ra bản chất vật đã rõ; áp R-05: ứng viên box hợp lý thì review, chưa box/class thì ghi issue |
| Taxonomy | READY | submission/taxonomy.json v1.0; định nghĩa lớp khớp guideline, enum/default/rules giữ nguyên |
| Cấu hình CVAT cục bộ | READY | cvat/labels_generated.json sinh từ taxonomy v1.0; object có 3 thuộc tính, ignore không có thuộc tính |
| Assignment chung | READY | assignment.csv và assignments/101.txt,102.txt đã có trên main; mỗi người40 ảnh, tổng80 lượt được giao |
| Gói ảnh upload | READY | Hai ZIP ở work/annotation_upload/, mỗi gói40 ảnh đúng tên/hash nguồn, không annotation; work không nộp |
| CVAT local | READY | http://localhost:8080 đã phản hồi; phiên bản 2.74.1 |
| Phiên truy cập tạo Project | READY | Đã đăng nhập bằng thông tin người dùng cung cấp, tạo/đọc được Project và Task; không lưu thông tin đăng nhập vào repo |
| Project và hai Task | READY | Project 2; Task 15/Job 10 cho 101, Task 16/Job 11 cho 102; mỗi Task40 frame khớp assignment |
| Save/Export nhãn của người học | NOT STARTED | Export COCO 1.0 có trong danh sách hỗ trợ; từng người cần Save và export nhãn thật sau khi gán |
| Annotation / COCO riêng | NOT STARTED | Chưa có labels/101.json hoặc 102.json; chỉ người học vẽ box |
| Validation nhãn / IAA / calibration / QC | NOT STARTED | Chỉ thực hiện sau khi có nhãn thật và đầu vào tương ứng |
| Điều phối / reviewer | Chưa phân công | Nhóm bổ sung mã người và vai trò vào TEAM.md; chưa tạo quyết định QC |

**Đã hoàn tất khóa đặc tả Pha 2; chuyển sang chuẩn bị thao tác CVAT của Pha 3.** Project/Task đã được kiểm cấu hình và đủ 40 frame; hai người có thể mở đúng Job để bắt đầu gán độc lập. Các yêu cầu hoàn thiện/gửi riêng bản cá nhân vẫn phải được từng thành viên ghi nhận theo RULES; việc chốt bản nhóm không chứng minh các bước đó đã diễn ra.

## 2. Thao tác kế tiếp của từng người

1. Mở CVAT local, đăng nhập bằng tài khoản của mình; kiểm Project dùng taxonomy v1.0.
2. Mở Job 10 cho 101 hoặc Job 11 cho 102 theo [danh sách Task](CVAT_TASKS.md). Ảnh đã upload đủ 40 frame; không tạo lại Task hoặc upload trùng.
3. Người học gán độc lập theo cùng v1.0; không xem nhãn người kia. Ghi ca chưa chắc bằng can_review hoặc ghi chú vùng/ảnh.
4. Export COCO 1.0 riêng, giữ ảnh không box; validate đúng file, gửi riêng rồi mới tập hợp hai bản.
5. Chỉ khi đủ 80/80 lượt hợp lệ mới đo IAA. Không tự bổ sung số liệu hoặc quyết định các pha sau.

## 3. Trạng thái CVAT thực tế

Đã xác thực và tạo Project 2 với Task 15/16; cả hai Task có đúng 40 frame và khớp tên/thứ tự assignment. Cả hai chưa có shapes/tracks/tags tại thời điểm kiểm tra. Định dạng export COCO 1.0 được hỗ trợ nhưng chưa export nhãn thật. Xem [CVAT_TASKS.md](CVAT_TASKS.md) để mở đúng Job theo mã. Không lưu thông tin đăng nhập vào file hoặc Git.

## 4. Tài liệu dùng chung

- [Guideline v1.0](../../submission/guidelines/guideline_v1.0_agreed.md) là quy tắc annotation; [harmonization](GUIDELINE_HARMONIZATION.md) lưu khác biệt hai bản ban đầu.
- [Báo cáo học tập/thực hành](../../submission/qc/QC_REPORT.md) chỉ cập nhật việc có kết quả thật; không ghi việc khởi động công cụ thành kết quả gán nhãn.
- Giữ bản guideline cá nhân ban đầu. Nếu đổi nghĩa quy tắc sau khóa, ghi phiên bản/phạm vi và xác nhận lại theo GUIDE.
