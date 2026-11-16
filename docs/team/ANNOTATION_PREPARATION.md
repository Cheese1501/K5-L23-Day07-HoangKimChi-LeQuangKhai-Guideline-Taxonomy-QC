# Chuẩn bị CVAT và hai lượt gán độc lập

**GUIDELINE v1.0 ĐÃ KHÓA.** Người dùng xác nhận cả 101 và 102 đã đồng ý toàn bộ bản chung ngày ghi nhận 2026-11-16. Dùng [guideline nhóm](../../submission/guidelines/guideline_v1.0_agreed.md) và kiểm [điều kiện Task](NEXT_PHASE_CHECKLIST.md) trước khi vẽ. Không tự annotation thay101/102. CVAT: http://localhost:8080.

## 1. Những gì đã có và những gì chưa làm

| Thành viên | Danh sách chuẩn bị local | Ảnh upload sau khóa | COCO đầu ra của người gán |
|---|---|---|---|
| 101 | submission/qc/assignments/101.txt —40 ảnh | work/101/images/ | submission/labels/101.json —chưa có |
| 102 | submission/qc/assignments/102.txt —40 ảnh | work/102/images/ | submission/labels/102.json —chưa có |

Local assignment.csv chia mỗi ảnh cho 101 và 102. Hai bộ giống tập ảnh là đúng thiết kế nhóm hai người; đó là 80 lượt được giao, không phải 80 lượt hoàn tất. Giữ nguyên file/ảnh đang có, không tạo lại assignment hoặc ghi đè work102. Assignment đã lưu trên main; cả hai dùng chính bản chung này, không tạo lại phân công.

CVAT local đã phản hồi tại http://localhost:8080, phiên bản 2.74.1. Đã đăng nhập và tạo Project 2, Task 15/16; xem [liên kết từng Job](CVAT_TASKS.md). Chưa có export nhãn thật. Không có COCO/IAA/QC được tạo. Mỗi người đăng nhập để mở đúng Job của mình.

### Gói upload đã kiểm tra

| Thành viên | Gói ảnh local | Số ảnh | Nội dung |
|---|---|---|---|
| 101 | work/annotation_upload/day07_101_images_v1.0.zip | 40 | Chỉ JPEG, tên gốc, hash khớp nguồn |
| 102 | work/annotation_upload/day07_102_images_v1.0.zip | 40 | Chỉ JPEG, tên gốc, hash khớp nguồn |

Hai gói có cùng tập ảnh theo thiết kế nhóm hai người nhưng dùng cho hai lượt gán riêng. Không có annotation trong ZIP. Không đưa work vào gói nộp.

## 2. Cấu hình đã chuẩn bị từ taxonomy v1.0

Người được nhóm phân công làm theo thứ tự:

```powershell
$env:PYTHONUTF8 = '1'
$env:PYTHONIOENCODING = 'utf-8'
# Taxonomy đã là v1.0; cấu hình đã sinh. Chỉ chạy lại nếu cần tái lập đúng cùng taxonomy.
python scripts/make_cvat_labels.py
```

Giữ enum occluded_level0/1/2/3, truncated no/yes và checkbox can_review. Kiểm output sáu class; năm class object có đủ ba thuộc tính; ignore_region không thuộc tính. Cấu hình enum không chứa nghĩa% che: người gán phải dùng bảng R-03 (0 không che,1 dưới50%,2 từ50%,3 không xác định; không tính truncation). Không thay bằng cờ occluded mặc định của CVAT: đó là trường khác.

Theo [CVAT_SETUP](../CVAT_SETUP.md), tạo Project → Labels → Raw từ JSON vừa sinh. Project đã tạo: `day07-team-101-102-v1.0` (ID2); Task 101 ID15/Job 10, Task 102 ID16/Job 11. Không tạo thêm bản trùng; dùng [CVAT_TASKS.md](CVAT_TASKS.md) mở đúng Job. Kiểm trực tiếp select/checkbox/default trên Project, không chỉ nhìn file JSON.

## 3. Tạo hai Task và gán độc lập

1. Hai Task riêng đã tạo trong Project 2 v1.0. Mỗi người mở đúng Job 101/102, không tạo lại Task khi đã có bản đúng.
2. Ảnh đã upload, đối chiếu đúng 40 frame/tên/thứ tự ở mỗi Task. Kiểm lại frame đầu/cuối khi mở; không upload bổ sung hoặc đổi tên ảnh.
3. Trước lượt gán, mỗi người tự kiểm class/thuộc tính có thể chọn và quyền Save/Export. Chưa xác minh ở đây; khi có lỗi quyền hỏi coach, không chuyển sang dùng nhãn của bạn cùng nhóm.
4. Human vẽ Rectangle; box phần thấy gồm gương/bánh gắn liền, người–xe riêng; không pre-label bằng mô hình. Đo chiều cao trên ảnh gốc, không theo zoom.
5. Box hợp lý chưa chắc dùng can_review; không xác định box/class thì ghi riêng ảnh/vùng/lý do. Không cùng xem nhãn trong lượt độc lập. Sau khóa nhãn cá nhân mới tập hợp issue cấp ảnh vào file chung.
6. Áp cùng bản khóa cho cả40 ảnh; không tự đổi ngưỡng giữa chừng. Nếu guideline thiếu điều kiện quan trọng thì báo nhu cầu chốt quy tắc theo quy trình, không bí mật tạo luật mới.

## 4. Export và kiểm từng người

Sau khi người gán thực sự đã làm và Save:

1. Actions → Export task dataset → **COCO 1.0**, tắt Save images. Tải từ Requests; giải nén lấy annotations/instances_<subset>.json.
2. Mỗi người giữ bản export riêng theo mã; không dùng copy JSON của người kia. Giữ đủ 40 ảnh trong phần images, kể cả ảnh không annotation.
3. Chạy validator trên chính bản thật:

```powershell
# 101 chạy cho bản export101 thật:
python scripts/validate_labels.py submission/labels/101.json
# 102 chạy cho bản export102 thật:
python scripts/validate_labels.py submission/labels/102.json
```

4. Kiểm can_review và select attributes tồn tại trong export; validator pass chỉ xác nhận cấu trúc/tập ảnh/hình học cơ bản. Người gán vẫn phải kiểm đúng vật/class/độ ôm và bỏ sót trên ảnh.
5. Gửi riêng trước khi tập hợp cả hai bản, theo GUIDE/RULES và kênh coach. Không tạo annotation JSON rỗng để “kiểm export” hoặc làm đủ lượt khi chưa gán thật.

## 5. Sau cả hai nộp và khóa nhãn độc lập

```powershell
python scripts/validate_labels.py --all
python scripts/qc_compare.py
python scripts/viz_disagreement.py --images flagged
```

Chỉ chạy khi đủ hai bộ đúng 40 ảnh (80/80 lượt hợp lệ). Đọc matched pairs và N/A, unmatched/ignore; đối chiếu ca tham chiếu cùng sai. Sau đó mới calibration/v1.1, nhãn cuối và QC toàn lô theo GUIDE. Không chạy pipeline để tạo đầu ra giả trong giai đoạn chuẩn bị này.

## 6. Bằng chứng cần ghi khi thực hiện thật

Mỗi người ghi mã Task, version guideline/taxonomy, số frame, kết quả Save/Export, đường dẫn COCO thật và exit code validator vào ghi chú cá nhân của mình. Không điền dữ liệu đăng nhập. Người chốt/reviewer do nhóm xác nhận trong TEAM.md; vòng chuẩn bị không tự tạo tên người hoặc chữ ký.
