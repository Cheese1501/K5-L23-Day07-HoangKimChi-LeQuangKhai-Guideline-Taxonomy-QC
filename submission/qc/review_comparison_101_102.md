# Đối chiếu bản review 101 với nguồn 102

Ngày 2026-11-17. Bản 101 kế thừa backup đã review của 102; các số đo phản ánh thay đổi sau sửa. Không đủ điều kiện diễn giải thành IAA độc lập.

| Đại lượng | Kết quả |
|---|---:|
| Ảnh mỗi bản | 40 |
| Annotation 101 / 102 | 344 / 352 |
| Đối tượng 101 / 102 | 342 / 350 |
| Cặp ghép | 342 |
| IoU trung bình | 1.0000 |
| Cùng lớp | 336/342 (98.25%) |
| Chưa ghép 101 / 102 | 0 / 8 |
| Cùng occluded_level | 338/342 (98.83%) |
| Cùng truncated | 337/342 (98.54%) |
| Cùng can_review | 338/342 (98.83%) |
| Vùng ignore mỗi bản | 2 |

Ghép bằng `scripts/common.py::match_boxes`, tham lam 1–1 theo IoU giảm dần, không phân biệt lớp, ngưỡng 0.5. Hai vùng ignore được loại khỏi danh sách đối tượng. Không bỏ thêm đối tượng theo độ phủ ignore. Hòa điểm ở box trùng tọa độ được giải theo thứ tự danh sách, vì vậy số cặp lệch lớp có thể khác số thao tác đổi lớp. Nguồn ở ảnh 024 có hai box truck/car trùng tọa độ, có thể ghép car giữ lại với truck nguồn trước khi xét car nguồn.

Lượt sửa gồm 21 shape trên 13 ảnh: xóa 8, cập nhật 13. IoU giữ nguyên vì sửa nhãn, thuộc tính và xóa box thừa. Còn 127 mức che không xác định và 288 cờ review; chưa có QC toàn lô. Nhật ký trước/sau tại `annotation_corrections_101.csv`; số đo, ngưỡng và checksum tại `review_comparison_101_102.json`.
