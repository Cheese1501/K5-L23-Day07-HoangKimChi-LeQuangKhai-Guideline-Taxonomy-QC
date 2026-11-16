# Review bản nháp YOLO11n + SAM 3 — thành viên 101

Đây là nhánh **review nhãn AI**, tách khỏi hai lượt gán thủ công độc lập của Day 07. Nguồn gói theo mô tả người gửi: YOLO11n + SAM 3; các box chưa được người duyệt. Không dùng bản chung này làm hai kết quả độc lập để tính IAA hoặc ghi thành nhãn tự vẽ của từng người.

## 1. Mở bản đã khôi phục

- CVAT local: phiên bản **2.74.1** trên máy 101.
- Task: [17 — DAY07-101-REVIEW-YOLO-SAM3](http://localhost:8080/tasks/17).
- Job để review: [Job 12](http://localhost:8080/tasks/17/jobs/12).
- Gói nguồn: `DAY07-102-YOLO-SAM3-40images-CVAT-backup.zip`.
- SHA-256 gói nguồn: `183b04895d3410a450c6d49868edf7f6163d274b476f1fac6d08ec054973fe0e`.

Gói đã được khôi phục nguyên file bằng **Restore task**, không dùng Upload annotations và không cần tạo Project/labels trước. Ảnh trong backup khớp ảnh nguồn của repository. Nhóm giữ [ATTRIBUTION.csv](../../data/ATTRIBUTION.csv) và [guideline v1.0](../../submission/guidelines/guideline_v1.0_agreed.md) để đối chiếu.

## 2. Trạng thái trước review trên máy 101

Đã đối chiếu sau restore: đúng 40 frame, tên và thứ tự `img_001.jpg`–`img_040.jpg`; 399 rectangle có tọa độ, lớp và giá trị thuộc tính khớp backup. Đây là kiểm tra tính toàn vẹn bản khôi phục, chưa xác nhận nội dung nhãn đúng.

| Class | Số rectangle ban đầu |
|---|---:|
| car | 101 |
| truck | 16 |
| van | 0 |
| motorcycle | 95 |
| person | 185 |
| ignore_region | 2 |
| Tổng | 399 |

397 box đối tượng có `can_review=true`, `occluded_level=3`, `truncated=no`; hai vùng ignore không có thuộc tính. Các giá trị này là **giá trị tạm**, không phải kết luận người duyệt. Chưa sửa box, chưa thực hiện review nội dung hoặc export nhãn sau review. Task 15/16 của hai lượt gán độc lập được giữ nguyên.

## 3. Cách thực hành review

1. Mở Job 12, kiểm lần lượt từng ảnh. So với ảnh gốc để nhận ra box thừa, thiếu, sai lớp hoặc không ôm sát; không chỉ kiểm các box đã có, vì vật bị model bỏ sót cũng cần tìm.
2. Rà kỹ van/minibus/pickup; số van ban đầu bằng 0 không chứng minh ảnh không có van. Kiểm tượng, đồ chơi, hình in, phản chiếu và vùng ignore theo scope nhóm.
3. Kéo/căn lại box hoặc góc, đổi lớp/thuộc tính, xóa box thừa, thêm Rectangle cho vật thiếu khi người duyệt đã xác định. Không dựng phần không nhìn thấy.
4. Kiểm từng mức che: 0 không bị che; 1 che trên 0% và dưới 50%; 2 từ 50%; 3 không xác định được. Không tính phần ngoài biên ảnh do truncation vào tỷ lệ che. Kiểm `truncated` riêng, không giữ mặc định no trên mọi box.
5. Sau khi kiểm chắc mới cập nhật `can_review`; ca còn mơ hồ tiếp tục giữ cờ và ghi ảnh/vùng/lý do. Không xóa cờ hàng loạt để làm kết quả trông đã được duyệt. Lưu sau mỗi nhóm sửa bằng Save.

Các ca cần chú ý gồm img_002, img_005, img_017, img_024, img_026, img_028, img_030, img_037, img_038 và img_040. Quyết định phải dựa vào ảnh và Rule ID, không dựa vào độ tin cậy của model hoặc số box có sẵn.

## 4. Sau khi review thật

Save rồi export **COCO 1.0**, tắt Save images. Giữ kết quả trong nhánh review riêng, không ghi đè `submission/labels/101.json` hoặc `102.json` vốn dành cho các lượt độc lập. Nếu cần chuyển cả Task kèm ảnh, tạo Task Backup mới và giữ gói nguồn để đối chiếu.

Báo cáo bổ sung số ảnh đã xem, các ví dụ sửa có ảnh/Rule ID, lỗi bỏ sót và thuộc tính, phần còn chưa chắc và người kiểm. Chỉ ghi các kết quả thực sự đã làm. Việc khôi phục thành công và con số 399 không phải kết quả QC hoặc quyết định Release.
