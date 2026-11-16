# Chuẩn bị CVAT và hai lượt gán độc lập

**PENDING TEAM APPROVAL — hướng dẫn chuẩn bị, chưa phải lệnh bắt đầu gán.** Áp dụng sau khi [checklist](NEXT_PHASE_CHECKLIST.md) đáp ứng điều kiện khóa [guideline nhóm](../../submission/guidelines/guideline_v1.0_agreed.md). Không tự annotation thay101/102.

## 1. Những gì đã có và những gì chưa làm

| Thành viên | Danh sách chuẩn bị local | Ảnh upload sau khóa | COCO đầu ra của người gán |
|---|---|---|---|
| 101 | submission/qc/assignments/101.txt —40 ảnh | work/101/images/ | submission/labels/101.json —chưa có |
| 102 | submission/qc/assignments/102.txt —40 ảnh | work/102/images/ | submission/labels/102.json —chưa có |

Local assignment.csv chia mỗi ảnh cho101 và102. Hai bộ giống tập ảnh là đúng thiết kế nhóm hai người; đó là80 lượt được giao, không phải80 lượt hoàn tất. Giữ nguyên file/ảnh đang có, không tạo lại assignment hoặc ghi đè work102. Xác nhận/chia sẻ một bản assignment chung trước upload.

Chưa truy cập instance CVAT của lớp trong vòng này, chưa xác nhận Project/Task/frame count hay export thực tế. Không có COCO/IAA/QC được tạo. Công cụ/test cục bộ không chứng minh quyền truy cập dịch vụ.

## 2. Sau khi hai người xác nhận và khóa

Người được nhóm phân công làm theo thứ tự:

```powershell
$env:PYTHONUTF8 = '1'
$env:PYTHONIOENCODING = 'utf-8'
# Chỉ chạy generator sau khi taxonomy đã được nhóm đổi version v1.0 và chốt definitions.
python scripts/make_cvat_labels.py
```

Giữ enum occluded_level0/1/2/3, truncated no/yes và checkbox can_review. Kiểm output sáu class; năm class object có đủ ba thuộc tính; ignore_region không thuộc tính. Cấu hình enum không chứa nghĩa% che: người gán phải dùng bảng R-03 (0 không che,1 dưới50%,2 từ50%,3 không xác định; không tính truncation). Không thay bằng cờ occluded mặc định của CVAT: đó là trường khác.

Theo [CVAT_SETUP](../CVAT_SETUP.md), tạo Project → Labels → Raw từ JSON vừa sinh. Nhóm chọn mã/tên Project gắn v1.0, không họ tên/tài khoản. Kiểm trực tiếp select/checkbox/default trên Project, không chỉ nhìn file JSON.

## 3. Tạo hai Task và gán độc lập

1. Mỗi người tạo Task riêng dùng mã `101` hoặc `102` và phiên bản v1.0; chọn đúng Project đã khóa.
2. Upload chỉ bộ ảnh của mình; đối chiếu đúng40 frame và tên ảnh với assignments/<mã>.txt, giữ tên gốc img_XXX.jpg.
3. Trước lượt gán, mỗi người tự kiểm class/thuộc tính có thể chọn và quyền Save/Export. Chưa xác minh ở đây; khi có lỗi quyền hỏi coach, không chuyển sang dùng nhãn của bạn cùng nhóm.
4. Human vẽ Rectangle; box phần thấy gồm gương/bánh gắn liền, người–xe riêng; không pre-label bằng mô hình. Đo chiều cao trên ảnh gốc, không theo zoom.
5. Box hợp lý chưa chắc dùng can_review; không xác định box/class thì ghi riêng ảnh/vùng/lý do. Không cùng xem nhãn trong lượt độc lập. Sau khóa nhãn cá nhân mới tập hợp issue cấp ảnh vào file chung.
6. Áp cùng bản khóa cho cả40 ảnh; không tự đổi ngưỡng giữa chừng. Nếu guideline thiếu điều kiện quan trọng thì báo nhu cầu chốt quy tắc theo quy trình, không bí mật tạo luật mới.

## 4. Export và kiểm từng người

Sau khi người gán thực sự đã làm và Save:

1. Actions → Export task dataset → **COCO1.0**, tắt Save images. Tải từ Requests; giải nén lấy annotations/instances_<subset>.json.
2. Mỗi người giữ bản export riêng theo mã; không dùng copy JSON của người kia. Giữ đủ40 ảnh trong phần images, kể cả ảnh không annotation.
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

Chỉ chạy khi đủ hai bộ đúng40 ảnh (80/80 lượt hợp lệ). Đọc matched pairs và N/A, unmatched/ignore; đối chiếu ca tham chiếu cùng sai. Sau đó mới calibration/v1.1, nhãn cuối và QC toàn lô theo GUIDE. Không chạy pipeline để tạo đầu ra giả trong giai đoạn chuẩn bị này.

## 6. Bằng chứng cần ghi khi thực hiện thật

Mỗi người ghi mã Task, version guideline/taxonomy, số frame, kết quả Save/Export, đường dẫn COCO thật và exit code validator vào ghi chú cá nhân của mình. Không điền dữ liệu đăng nhập. Người chốt/reviewer do nhóm xác nhận trong TEAM.md; vòng chuẩn bị không tự tạo tên người hoặc chữ ký.
