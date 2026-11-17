# Tóm tắt IAA (taxonomy v1.0)

- Ảnh được so sánh (có >=2 người gán): **40**; số người gán: 2
- Lượt gán đủ **80/80**.
- IoU trung bình và % cùng lớp **chỉ tính trên các cặp box đã ghép** (IoU >= 0.5, ghép 1-1 không phân biệt lớp). Box chưa ghép được thống kê riêng ở cột bỏ sót/thừa.
- Mẫu số: 342 cặp box ghép (tổng mọi cặp người gán, ảnh chung).

| Cặp | Ảnh | Cặp box ghép | IoU TB | Cùng lớp | Cùng occluded_level | Cùng truncated | Chưa ghép (A/B) | Bỏ qua do ignore | Đạt IAA |
|---|---|---|---|---|---|---|---|---|---|
| **TỔNG** | 40 | 342 | 1.000 | 98.2% | 98.8% | 98.5% | 0/8 | 0 | ĐẠT |
| 101|102 | 40 | 342 | 1.000 | 98.2% | 98.8% | 98.5% | 0/8 | 0 | ĐẠT |

Ngưỡng IAA: IoU TB >= 0.85, đồng thuận lớp >= 95%.

Số ca bất thường: 604 ({'bo_sot_thua': 8, 'co_can_review': 580, 'sai_thuoc_tinh': 9, 'sai_lop': 6, 'can_review_anh': 1}), trên 35 ảnh cần calibration.
