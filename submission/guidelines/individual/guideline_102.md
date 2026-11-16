# Guideline gán nhãn cá nhân — bản đề xuất — 102

> Thành viên 102 đồng ý với các quy tắc đề xuất trong bản này và chia sẻ để nhóm thảo luận. AI hỗ trợ soạn thảo; mục 4 còn chờ bổ sung ID ảnh và quan sát thực tế. Đây là bản đề xuất cá nhân, chưa phải guideline v1.0 chung đã khóa của nhóm.

- Phiên bản: `individual-102-draft`.
- Ngày soạn: 2026-11-16.
- Người đề xuất / duyệt quy tắc: 102; AI hỗ trợ soạn thảo.
- Trạng thái: quy tắc đã được 102 chấp thuận; ví dụ ảnh chưa hoàn tất; chờ nhóm thống nhất.
- Phạm vi: bộ 40 ảnh trong `data/images/`, bounding box bằng CVAT, xuất COCO 1.0.

## 1. Mục tiêu

Tạo nhãn cho mô hình phát hiện người và một số loại phương tiện thật trong ảnh đường phố 2D. Mỗi đối tượng được chọn cần có một box, một lớp và các thuộc tính theo taxonomy.

Ưu tiên tránh bỏ sót người, nhầm lớp phương tiện và đặt box không nhất quán khi vật bị che. Bộ ảnh phục vụ thực hành xây dựng đặc tả và QC; kết quả bài lab không đủ để kết luận mô hình an toàn cho triển khai giao thông thực tế.

## 2. Lớp và thuộc tính

### 2.1. Lớp

Ví dụ trong bảng là ví dụ khái niệm, chưa gắn với ảnh đã kiểm tra.

| Lớp | Định nghĩa đề xuất | Ví dụ | Phản ví dụ / dễ nhầm |
|---|---|---|---|
| `car` | Ô tô chở người dạng sedan, hatchback, SUV hoặc crossover; không có thùng chở hàng tách biệt. | Sedan, SUV. | Pickup có thùng hàng → `truck`; xe buýt ngoài phạm vi. |
| `truck` | Phương tiện chở hàng có cabin và phần chở hàng tách biệt về cấu trúc, gồm pickup, xe tải và đầu kéo. | Pickup có thùng mở hoặc gắn nắp; xe tải thùng. | Van có khoang kín liền thân → `van`. |
| `van` | Xe có cabin và khoang sau tạo thành thân xe kín liền khối dạng van, không có thùng hàng riêng. | Van giao hàng, van chở người. | SUV → `car`; tải thùng có cabin riêng → `truck`. |
| `motorcycle` | Xe hai bánh có động cơ, gồm mô tô và xe tay ga; không bao gồm người ngồi trên xe. | Mô tô, xe máy. | Xe đạp, xe ba bánh tuk-tuk ngoài phạm vi của bản đề xuất này. |
| `person` | Người thật có phần cơ thể nhìn thấy và đủ căn cứ nhận biết, gồm người đi bộ, người lái và hành khách. | Người đi bộ, người ngồi trên xe máy. | Tượng, ma-nơ-canh, chân dung trên biển quảng cáo. |
| `ignore_region` | Vùng ngoại lệ nơi đối tượng mục tiêu quá nhỏ hoặc không thể tách thành từng cá thể theo quy tắc đã chốt. | Cụm người rất nhỏ không tách được. | Một ô tô lớn nhưng khó phân biệt lớp: cần review, không tự che bằng ignore. |

**R-01 — Chọn lớp:** mỗi vật có một lớp đối tượng. Dựa vào cấu trúc nhìn thấy, không suy đoán hãng, công dụng hoặc cấu trúc bị khuất. Nếu không đủ bằng chứng phân biệt lớp, dùng quy trình R-09.

**R-02 — Ngoài phạm vi:** theo lựa chọn đề xuất ở bảng trên, không gán box đối tượng cho xe buýt, xe đạp, xích lô, tuk-tuk hoặc vật không thuộc lớp nào. Không dùng `ignore_region` chỉ vì vật nằm ngoài taxonomy. Nếu muốn thêm lớp hoặc thay cách phân loại, nhóm phải sửa guideline và taxonomy đồng bộ trước khi khóa v1.0.

### 2.2. Thuộc tính

Áp dụng ba thuộc tính sau cho mọi box đối tượng; `ignore_region` không cần thuộc tính.

| Thuộc tính | Giá trị | Nghĩa và cách chọn đề xuất |
|---|---|---|
| `occluded_level` | `0` | Không có phần vật bị vật khác che. |
| `occluded_level` | `1` | Bị che trên 0% đến hết 30% diện tích 2D ước tính của vật trong khung ảnh. |
| `occluded_level` | `2` | Bị che trên 30% đến hết 70%. |
| `occluded_level` | `3` | Bị che trên 70%, nhưng vẫn đủ căn cứ nhận biết đối tượng. |
| `truncated` | `yes` | Có phần vật bị cắt bởi biên ảnh. |
| `truncated` | `no` | Không có phần vật bị cắt bởi biên ảnh. |
| `can_review` | `true` | Có box nhưng người gán chưa chắc về lớp, biên box hoặc thuộc tính. |
| `can_review` | `false` | Không có điểm cần reviewer giải quyết. |

**R-03 — Phân biệt che và cắt:** `occluded_level` chỉ tính che bởi vật khác. Phần nằm ngoài khung ảnh tính bằng `truncated`, không cộng vào phần che. Một vật có thể vừa bị che vừa bị cắt.

Diện tích để ước tính mức che là hình chiếu của chính vật, không phải diện tích hình chữ nhật bao vật hoặc toàn bộ ảnh. Đây là ước lượng bằng mắt; trường hợp gần ngưỡng hoặc khó suy ra hình dạng thì đánh dấu review. Không suy đoán vật hoàn toàn không nhìn thấy.

Các mốc 30% và 70% là đề xuất của bản tham khảo, không phải ngưỡng bắt buộc do script của lab quy định. Nhóm cần kiểm thử bằng ví dụ và thống nhất trước khi dùng.

## 3. Quy tắc vẽ box

### R-04 — Box theo phần nhìn thấy

- Dùng Rectangle, một box cho mỗi đối tượng đủ điều kiện.
- Box nhỏ nhất bao toàn bộ phần nhìn thấy thuộc đối tượng; không thêm lề chủ động.
- Bao các bộ phận gắn liền nhìn thấy được, ví dụ bánh xe và gương xe; không bao bóng đổ, khói, tải hàng là vật riêng hoặc vật đứng cạnh.
- Nếu nhiều phần nhìn thấy của cùng một vật bị ngắt quãng do che khuất, dùng một box bao các phần đó; khoảng trống giữa chúng có thể nằm trong box.
- Không mở rộng box theo kích thước toàn thân tưởng tượng ở phía bị che hoặc ngoài khung ảnh.

### R-05 — Người và phương tiện

- Người và xe là hai đối tượng riêng; không gộp thành một box.
- Một người ngồi trên một xe máy: tối đa một box `person` và một box `motorcycle`, nếu từng đối tượng đạt điều kiện kích thước và nhận biết.
- Hai người trên một xe: tối đa hai box `person` và một box xe; các box có thể chồng nhau.
- Box xe không bao thêm người hoặc hành lý để tạo một cụm chung. Phần xe bị người che được xử lý theo R-03 và R-04.
- Người nhìn qua cửa kính vẫn được xét nếu nhận biết được cơ thể và đạt kích thước; không suy ra hành khách không nhìn thấy.

### R-06 — Xe chở xe và vật lồng nhau

Xe vận chuyển và từng xe được chở được xét riêng nếu đều là vật thật, nhận biết được và đạt kích thước. Không gộp cả đoàn thành một box duy nhất. Không đếm hai lần cùng một xe. Với rơ-moóc nối đầu kéo, bản đề xuất xem tổ hợp đang nối là một phương tiện `truck`; rơ-moóc tách rời cần quyết định phạm vi trước khi gán.

### R-07 — Vật không thật và xe chủ

- Không gán các hình mô phỏng đối tượng: tượng, đồ chơi, ma-nơ-canh, hình in, hình trên màn hình và ảnh phản chiếu trong gương hoặc kính.
- Không gán phần xe gắn camera xuất hiện trong ảnh, nếu có đủ căn cứ xác định đó là xe chủ.
- Khi chưa chắc vật thật hay hình mô phỏng, hoặc chưa rõ có phải xe chủ, ghi review theo R-09.

### R-08 — Vật nhỏ và đám đông

- Đo chiều cao box theo ảnh gốc, không theo mức zoom trên màn hình.
- Box đối tượng cao từ 20 px trở lên: gán nếu đủ căn cứ nhận biết. Đúng 20 px vẫn thuộc diện xét gán.
- Đối tượng mục tiêu có phần nhìn thấy tạo box cao dưới 20 px: dùng vùng `ignore_region` theo quy tắc vật nhỏ của lab.
- Đám đông: tách từng người nếu nhận biết được từng cá thể và đạt ngưỡng; chỉ dùng ignore cho phần không thể tách đáng tin cậy.
- Vùng ignore cần ôm sát phạm vi ngoại lệ; không phủ rộng sang đối tượng đủ điều kiện ở bên cạnh. Ca không thể khoanh vùng mà không ảnh hưởng đối tượng hợp lệ cần reviewer chốt.
- Vật cao từ 20 px nhưng không đủ căn cứ nhận biết không tự động trở thành ignore; ghi vấn đề theo R-09.

### R-09 — Ca chưa chắc

- Có thể vẽ box hợp lý nhưng chưa chắc lớp, biên hoặc thuộc tính: đặt `can_review=true`, ghi ảnh, vị trí và câu hỏi cụ thể.
- Chưa xác định được box hợp lý: ghi ảnh, vùng, lý do vào ghi chú riêng; sau khi khóa nhãn cá nhân, tập hợp vào `submission/qc/image_issues.csv` với cột `image,annotator,region,note`.
- Không trao đổi nhãn với người kia trong lượt gán độc lập. Giải quyết ca ở buổi calibration sau khi cả hai nộp.

## 4. Ca khó

**Chưa điền ID ảnh vì người học chưa xác nhận quan sát.** Bảng này là gợi ý để bạn tìm ca thật, thay phần giữ chỗ và tự viết quyết định. Không nộp nguyên bảng giữ chỗ như bằng chứng đã xem ảnh.

| Ảnh | Tình huống cần tìm và kiểm tra | Rule ID | Quyết định đề xuất để thử | Lý do |
|---|---|---|---|---|
| Chưa điền | Người ngồi trên xe máy. | R-05 | Tách người và xe; từng box phải đủ điều kiện. | Hai lớp có biên và ý nghĩa riêng. |
| Chưa điền | Xe tải vận chuyển các xe khác. | R-06 | Xét xe chở và từng xe được chở riêng. | Vị trí được chở không tự loại đối tượng thật. |
| Chưa điền | Người hoặc xe bị vật khác che. | R-03, R-04 | Box bao phần nhìn thấy; chọn mức che; không vẽ bù phần khuất. | Thống nhất phạm vi box giữa người gán. |
| Chưa điền | Tượng, ma-nơ-canh, hình in hoặc phản chiếu. | R-07 | Loại nếu xác định được là hình mô phỏng hoặc phản chiếu. | Mục tiêu của đề xuất là vật thật hiện diện trực tiếp. |
| Chưa điền | Tuk-tuk, xe buýt, xe đạp hoặc vật ngoài lớp. | R-02 | Không ép vào lớp gần giống; kiểm lại phạm vi đề xuất. | Giữ định nghĩa lớp nhất quán. |
| Chưa điền | Vật mục tiêu nhỏ hơn 20 px. | R-08 | Khoanh ignore đúng vùng ngoại lệ. | Tuân thủ ngưỡng kích thước của lab. |

Sau khi xem ảnh, bổ sung ít nhất một lần áp dụng lại R-05 trên ảnh khác: ID ảnh thứ nhất, ID ảnh thứ hai, số người/xe nhìn thấy đủ điều kiện và lý do kết quả nhất quán. Số ca trong bảng phải phản ánh điều bạn thực sự tìm được, không cần giữ mọi dòng gợi ý.

## 5. QC và phiên bản

### 5.1. Ngưỡng của lab

Giữ nguyên mục `rules` trong `submission/taxonomy.json`.

| Nội dung | Ngưỡng / yêu cầu |
|---|---|
| Chiều cao tối thiểu của box đối tượng | 20 px. |
| IoU dùng ghép cặp 1–1 trước so sánh | Từ 0,5; ghép không phân biệt lớp. |
| Ngưỡng IoU box lớn | 0,85 khi cao từ 50 px. |
| Ngưỡng IoU box nhỏ | 0,7 khi cao dưới 50 px. |
| IAA IoU trung bình | Từ 0,85 trên các cặp ghép được. |
| Đồng thuận lớp | Từ 95% trên các cặp ghép được. |
| Phân công nhóm 2 người | Mỗi người gán 40 ảnh, đủ 80/80 lượt hợp lệ trước khi đo IAA. |
| QC bàn giao | Duyệt toàn bộ 40 ảnh; tỉ lệ ảnh lỗi không quá 2%, không có lỗi lặp theo quy tắc lab và đủ bằng chứng. |

Ngưỡng box nhỏ 0,7 không thay thế ngưỡng IoU trung bình IAA 0,85. Báo riêng box chưa ghép và bất đồng ignore. Không có cặp ghép thì ghi N/A, không coi là đồng thuận hoàn hảo.

### 5.2. Trách nhiệm và quyết định

- Mỗi người gán theo v1.0 đã khóa trên Task riêng. Reviewer và người chốt calibration cần được nhóm xác nhận bằng mã thành viên trước khi thực hiện.
- Khi có thể, reviewer khác người sửa; nhóm hai người đổi vai và ghi rõ.
- Script kiểm định dạng, hình học, tập ảnh và tính số liệu. Người thật kiểm vật trong ảnh, bỏ sót, lớp và độ ôm sát.
- Giữ IAA trước calibration. Mỗi ca cần quyết định, rule ID, phiên bản, người chốt, bản sửa và kết quả kiểm lại.
- Hold nếu thiếu bằng chứng hoặc còn vấn đề guideline/dữ liệu. Rework nếu trên 2% ảnh lỗi hoặc có lỗi lặp. Release chỉ sau khi đủ bằng chứng, số liệu đạt và reviewer xác nhận.
- Một ảnh lỗi trong 40 ảnh là 2,5%, vượt ngưỡng. Chỉ duyệt mẫu thì Hold. Bản đề xuất này chưa có kết quả hoặc quyết định QC.

### 5.3. Lịch sử phiên bản

| Phiên bản | Thay đổi | Lý do / trạng thái |
|---|---|---|
| `individual-102-draft` | AI hỗ trợ soạn; 102 chấp thuận quy tắc và chia sẻ để thảo luận. | Chờ bổ sung ca ảnh thật và thống nhất nhóm; chưa khóa để gán. |

Khi tự hoàn thiện bản cá nhân, ghi nhận sự hỗ trợ AI và cách kiểm lại trong `submission/individual_notes/102.md`. Khi nhóm chốt, tạo v1.0; sau calibration tạo v1.1. Sửa nghĩa quy tắc là thay đổi `semantic` và cần rà lại toàn lô theo hướng dẫn lab; sửa câu chữ giữ nghĩa là `editorial`.
