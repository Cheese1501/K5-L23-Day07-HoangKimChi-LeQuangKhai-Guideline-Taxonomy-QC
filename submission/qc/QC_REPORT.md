# Báo cáo QC — nhóm 101–102

Báo cáo học tập và thực hành Day 07, cập nhật ngày 2026-11-16. Nhóm đã có hai bản guideline cá nhân, guideline chung v1.0 và phân công. Phần gán nhãn, IAA, calibration và QC chưa đủ sản phẩm để báo cáo kết quả hoàn thành.

## 1. Mục đích, dữ liệu và phiên bản

- Mục đích và giới hạn sử dụng: thực hành viết đặc tả nhãn bounding box 2D cho người và phương tiện, gán độc lập và kiểm tra chất lượng. Bộ 40 ảnh phục vụ học cách xử lý ca biên; không đại diện đầy đủ cho giao thông thực tế hoặc chứng minh độ an toàn của mô hình.
- Nguồn và phép sử dụng dữ liệu: `data/images/img_001.jpg`–`img_040.jpg`, nguồn và giấy phép theo `data/ATTRIBUTION.csv`. Giữ tên ảnh, ghi công và điều kiện sử dụng khi bàn giao.
- Manifest và checksum nhãn cuối: chưa có `batch_manifest.json` và nhãn cuối; chưa có checksum để ghi nhận.
- Guideline và taxonomy khi gán / khi bàn giao: dùng `guideline_v1.0_agreed.md` và `taxonomy.json` phiên bản v1.0 cho lượt gán độc lập. Hai thành viên đã đồng ý toàn bộ bản chung. Chưa có phiên bản sau calibration để bàn giao.

### Kết quả xây dựng guideline

| Nội dung | Vấn đề trong các bản đầu | Quy tắc chung và lý do |
|---|---|---|
| Che khuất | 101 đề xuất mốc 25%; 102 đề xuất 30%/70% và hiểu mức 3 khác v0 | R-03: 0 không che, 1 dưới 50%, 2 từ 50%, 3 không xác định mức che. Mức 3 thể hiện không biết, không phải che nặng nhất. Không tính phần ngoài ảnh vào tỷ lệ che. |
| Người và phương tiện | Dễ gộp người lái/hành khách vào xe | R-06: từng người và xe là instance riêng; box được chồng nhau. Dùng img_005 và img_026 để đối chiếu cùng nguyên tắc. |
| Xe chở xe, pickup, sidecar | Chưa rõ đâu là một phương tiện và đâu là bộ phận | R-08: tổ hợp đầu kéo/trailer đang nối là một truck; xe được chở xét riêng (img_002). Pickup có thùng riêng là truck; mô tô gắn sidecar là một motorcycle (img_022). |
| Van/minibus | Tên gọi hoặc kích thước trong ảnh dễ dẫn tới ép lớp | R-01/R-02: xét cấu tạo; van thân kín liền như img_005 khác minibus img_009 ngoài phạm vi. Pickup gắn canopy không tự thành van. |
| Vật không thật và phản chiếu | Hình dạng giống lớp mục tiêu nhưng không phải instance trực tiếp | R-09: loại tượng img_017/img_027, đồ chơi img_038, hình in và xe trong gương img_020. Xe thật trưng bày vẫn xét theo lớp. |
| Vật nhỏ, cụm đông | Dễ dùng ignore để né một vật khó hoặc che vật rõ | R-07: đo chiều cao trên ảnh gốc; dưới 20 px xử lý bằng vùng ignore đúng phạm vi. Tách từng cá thể đủ điều kiện, không ignore cả đám đông tùy tiện. |

Với img_024, chưa kết luận xe vàng là xe thật hay mô hình; với img_040, không suy một xe đầy đủ từ mũ/gương hoặc bộ phận sát mép. Nhóm dùng R-05 để xử lý ứng viên cần review hoặc ghi vấn đề cấp ảnh. Ở img_028, ngựa nằm ngoài taxonomy dù là thật hay mô hình; chỉ tính occlusion của xe khi có phần xe thực sự bị che. Các ví dụ này là hướng dẫn trước gán, chưa phải quyết định calibration trên annotation.

## 2. Phân công và đồng thuận trước calibration

- Lượt hoàn thành / được giao: chưa có COCO để xác nhận lượt hoàn thành / **80 lượt được giao**. Cả 101 và 102 được giao toàn bộ 40 ảnh theo `assignment.csv`; mỗi ảnh cần hai lượt độc lập.
- Số cặp box ghép, IoU TB, đồng thuận lớp và mẫu số: N/A — chưa có hai bộ COCO độc lập hợp lệ để ghép cặp.
- Box chưa ghép, loại do ignore, bất đồng vùng ignore: chưa có kết quả so sánh, không ghi số lượng bằng 0.
- Ca hai người có thể cùng sai sau khi đối chiếu tham chiếu: chưa thực hiện đối chiếu nhãn với tham chiếu. Khi có nhãn cần kiểm nguy cơ cùng bỏ người trên xe hoặc cùng gán tượng thành người; chưa coi đây là lỗi đã xảy ra.

Nhóm đã chuẩn bị Task riêng cho mỗi người, dùng cấu hình v1.0. Việc có Task hoặc phân công chưa chứng minh đã gán xong. IoU và đồng thuận lớp chỉ tính trên các cặp box ghép được, nên vẫn phải đọc vật bỏ sót, box chưa ghép và vùng ignore.

## 3. Calibration và kiểm lại

- Ca đã xử lý, rule ID, bản sửa và người xác nhận: chưa có `calibration_decisions.csv`; chưa có ca calibration hoàn tất.
- Tác động v1.1 lên nhãn và ảnh: chưa có guideline v1.1 hoặc nhãn sau calibration. Giữ v1.0 cho lượt gán độc lập.
- Tham chiếu bằng chứng khi Rework: chưa có vòng QC và bản sửa để đối chiếu.

Sau khi khóa hai bản độc lập, nhóm sẽ ghi từng ca theo case_id, ảnh, Rule ID, quyết định, người chốt và người kiểm lại. Nếu đổi nghĩa quy tắc, cần rà toàn bộ lô có thể bị ảnh hưởng; không chỉ sửa ảnh minh họa.

## 4. Kết quả duyệt

- Vòng QC: chưa thực hiện.
- Người review và ngày: chưa phân công người review bản cuối; chưa có ngày duyệt.
- Đã duyệt / cả lô: chưa có phiếu review / 40 ảnh cần duyệt sau khi có nhãn cuối.
- Ảnh lỗi / ảnh đã duyệt: N/A — chưa có mẫu số ảnh đã duyệt.
- Annotation đối tượng hiện có bị lỗi / annotation đối tượng đã duyệt: N/A — chưa có mẫu số annotation đã duyệt.
- Vật bỏ sót, ảnh và vùng: chưa có kết quả review để xác nhận.
- Ca khó / phần còn lại, lỗi lặp và ví dụ: img_024, img_028, img_040 là các ca cần chú ý; chưa có bằng chứng lỗi lặp trên nhãn.
- Một lỗi máy chặn được và một lỗi cần người đọc ảnh: chưa có lỗi nhãn thực tế để dẫn. Về chức năng, validator kiểm được lớp/tọa độ không hợp lệ; người đọc ảnh cần phát hiện tượng bị gán person, vật bỏ sót hoặc box không sát. Hai ví dụ này không phải kết quả QC của nhóm.

Ngưỡng của lab được giữ nguyên: IoU box lớn 0.85, box nhỏ 0.7; IAA IoU 0.85 và đồng thuận lớp 95%; tỷ lệ ảnh lỗi tối đa 2%. Với lô 40 ảnh, một ảnh lỗi tương ứng 1/40 = 2.5%: đây là ví dụ cách tính, không phải số liệu đã đo. Báo cáo theo ảnh và theo annotation phải có mẫu số riêng.

## 5. Quyết định bàn giao

- Quyết định: Hold
- Lý do, người nhận và phạm vi sử dụng: hồ sơ chưa đủ nhãn độc lập, calibration, nhãn cuối và phiếu QC để bàn giao lô nhãn. Bản hiện tại dùng để nhóm 101–102 tiếp tục thực hành và để coach xem phần đã làm; Hold phản ánh thiếu bằng chứng, không phải kết quả một vòng duyệt đã hoàn thành.
- Nếu còn việc: mỗi thành viên tự gán 40 ảnh theo v1.0, xuất COCO riêng và validate; nhóm tập hợp sau khi cả hai nộp, đo IAA, calibration, lập v1.1/nhãn cuối, phân công người kiểm và duyệt toàn bộ lô. 102 tiếp tục hoàn thiện ghi chú cá nhân của mình. Nhóm chỉ cập nhật kết quả khi có artifact tương ứng.
- Kiểm ngược từ báo cáo tới ảnh, rule và nhãn: `data/images/img_002.jpg` → R-06/R-08 trong guideline chung. Chưa truy tới object ID hoặc ca calibration vì chưa có nhãn và bảng quyết định; chuỗi bằng chứng bàn giao chưa hoàn chỉnh.

AI được dùng để hỗ trợ diễn giải, gợi ý phân tích ca ảnh và biên tập tài liệu, có khai báo trong ghi chú 101; các gợi ý không thay bằng chứng khảo sát độc lập của thành viên. Bản pre-label YOLO/SAM từ nguồn khác và thử nghiệm tool không được tính là annotation độc lập, IAA hoặc QC của Day 07; không đưa các box đó vào sản phẩm nộp thay cho phần người học tự vẽ.
