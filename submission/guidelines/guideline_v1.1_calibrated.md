# Guideline gán nhãn — v1.1 — nhóm 101–102

- Ngày biên tập: 2026-11-17; áp dụng cho bộ nhãn review bàn giao ở trạng thái Hold.
- Loại thay đổi: editorial; giữ nghĩa lớp, thuộc tính, box và toàn bộ ngưỡng của v1.0.
- Người biên tập: 101 với ChatGPT/Codex hỗ trợ. Bản này ghi cách xử lý hồ sơ sau review; phần xác nhận calibration chung của 101–102 còn chờ.

## Ghi chú áp dụng cho bản bàn giao

1. Giữ bản COCO cá nhân trước calibration để truy lại phép so sánh. Bộ nhãn bàn giao được tạo riêng.
2. Một dòng calibration là quyết định xử lý ca trong lượt hỗ trợ hiện tại. Dòng có nội dung giữ cờ/chờ xác nhận tiếp tục là ca chưa giải quyết; không diễn giải việc điền bảng thành kết luận người học đã chốt.
3. Giữ can_review và mức che 3 khi chưa đủ căn cứ. Không đổi cờ để đạt Release.
4. Bổ sung hai người lái tuk-tuk ở ảnh 004 theo R-02/R-06, giữ mức che 3 và cờ review để kiểm biên. Tuk-tuk vẫn ngoài taxonomy.
5. Ảnh 012: pickup tiền cảnh có cabin/thùng riêng thuộc truck theo R-08; phần xe tiếp tục ngoài biên phải/dưới dùng truncated=yes theo R-04.
6. Nhãn có tên labels_calibrated được tạo cho quy trình bàn giao; quyết định sử dụng phụ thuộc vòng QC và các ca chưa chốt được ghi trong báo cáo.

7. Kiểm lại QC vòng1 ở ảnh001/034: một pickup không tách cabin thành xe riêng, mỗi người thật là instance riêng, sedan không tách các phần đầu/đuôi thành nhiều car. Đây là áp dụng R-06; giữ cờ cho box đề xuất chưa xác nhận.

## Quy tắc kế thừa từ v1.0

- Phiên bản: **v1.0, đã thống nhất cho lượt gán độc lập**.
- Thành viên duyệt: **101 và 102**; ghi nhận đồng ý toàn bộ bản chung ngày 2026-11-16.
- Phạm vi: bộ 40 ảnh Day 07; nhãn bounding box 2D theo `submission/taxonomy.json` v1.0.
- Đây là guideline chung duy nhất của nhóm. Hai bản cá nhân được giữ riêng để đối chiếu lựa chọn ban đầu.

## 1. Mục tiêu và phạm vi

Nhãn bounding box 2D để huấn luyện phát hiện người và các phương tiện được chọn trên 40 ảnh `img_001.jpg`–`img_040.jpg`. Bỏ sót người, gộp người với xe, sai lớp hoặc dựng phần khuất sẽ làm nhãn lệch ý nghĩa. Đây là bài thực hành; không suy ra độ an toàn triển khai giao thông từ kết quả lab.

Chỉ xét đối tượng thật hiện diện trực tiếp và nhận dạng được. Xe đỗ, xe trong gara/showroom, hoặc xe được vận chuyển không tự bị loại vì bối cảnh. Mỗi người và phương tiện là một instance riêng. Ảnh không có đối tượng vẫn phải nằm trong Task và COCO.

## 2. Taxonomy, inclusion/exclusion và thuộc tính

### 2.1 R-01 — Chọn lớp theo cấu tạo nhìn thấy

Giữ sáu tên lớp và `ignore_class=ignore_region`; không thêm class trong bản v1.0 này. Các định nghĩa trong taxonomy v1.0 đã được đồng bộ theo phạm vi dưới đây.

| Lớp | Inclusion — định nghĩa đã chốt | Ví dụ ảnh thật | Exclusion / phản ví dụ |
|---|---|---|---|
| `car` | Sedan, hatchback, SUV/crossover, wagon và taxi chở người, không có thùng hàng riêng. | Sedan ở img_023; SUV ở img_012; taxi ở img_040. | Pickup có thùng riêng → truck; bus/minibus; đồ chơi img_038. |
| `truck` | Xe chở hàng có cabin và phần hàng tách biệt về cấu trúc; gồm pickup, pickup gắn canopy, xe tải thùng, đầu kéo nối trailer. | img_002, img_012, img_028, img_036, img_037. | Van thân kín liền; tuk-tuk img_004; tượng pickup img_027. |
| `van` | Xe dạng van cỡ nhỏ có cabin và khoang sau kín liền thân, chở hàng hoặc người; không có cabin/thùng tải riêng. | Xe thân van phía sau người ở img_005; van trắng img_016. | SUV → car; pickup có canopy → truck; bus/minibus thân lớn như img_009 ngoài scope. Không đoán số ghế/chiều dài thực từ ảnh. |
| `motorcycle` | Xe hai bánh có động cơ, gồm scooter; mô tô với sidecar gắn liền tính một instance xe. | img_005, img_026; sidecar img_022. | Xe đạp/xích lô; tuk-tuk/auto-rickshaw; tác phẩm kim loại img_011. |
| `person` | Mỗi người thật có phần cơ thể nhìn thấy và nhận biết được, kể cả lái xe, hành khách, người nhìn qua kính. | img_005, img_026, người cạnh carrier img_002. | Tượng img_017, mannequin img_033, hình người in img_018, mascot không thấy người thật. |
| `ignore_region` | Rectangle ngoại lệ cho vật mục tiêu dưới 20 px và cụm không tách được đúng điều kiện R-07; đây là vùng, không phải instance người/xe. | Vật nhỏ cần đo trong img_021, img_025, img_030. | Không thay class thiếu; không che một vật rõ ≥20 px; không khoanh tượng/đồ chơi hoặc toàn ảnh tùy tiện. |

**R-02 — Ngoài scope:** bus/minibus (loại xe img_009 và bus img_031, img_037), xe đạp, xích lô, tuk-tuk, động vật và vật rời không có box object. Người vận hành nhìn thấy vẫn xét person. Không dùng ignore chỉ vì vật ngoài taxonomy. Khi van/minibus chưa phân biệt được theo cấu tạo: box ứng viên có class hợp lý và can_review nếu đủ căn cứ; nếu chỉ có căn cứ là bus ngoài scope thì loại, không ép van. Không nhận ra class/box thì ghi issue. Cặp mẫu phân biệt là van img_005 và minibus img_009; trường hợp chưa rõ trong khi gán xử lý theo R-05.

### 2.2 R-03 — `occluded_level`: mức che khuất

Giữ enum chuỗi `"0"`, `"1"`, `"2"`, `"3"`, mặc định `"0"`. Mỗi box phải được người gán kiểm lại, không coi default là kết luận thị giác.

| Giá trị | Nghĩa | Điều kiện chọn |
|---|---|---|
| `0` | Không bị che, nhìn rõ về che khuất. | p = 0%; không có phần trong ảnh bị vật khác che. Blur không tự biến thành occlusion. |
| `1` | Bị che dưới 50%. | 0 < p < 50%; có che thật, ước lượng đủ tin cậy dưới một nửa. |
| `2` | Bị che từ 50% trở lên. | p >= 50%; đúng 50% thuộc mức 2, vẫn phải thấy phần đủ nhận dạng và đủ chiều cao xét gán. |
| `3` | Không xác định được mức che. | Vẫn nhận dạng được class/box nhưng không ước lượng được mức che; đặt can_review=true và ghi lý do. Không đồng nghĩa che nặng nhất. |

`p` là tỷ lệ diện tích hình chiếu của đối tượng **bị vật khác che trong khung ảnh**, chia cho tổng diện tích hình chiếu của chính đối tượng nằm trong khung (phần thấy + phần bị che). Không dùng diện tích rectangle làm mẫu số. Phần ngoài khung không nằm trong tử số hoặc mẫu số: đó là truncation. Đây là ước lượng, không cần dựng box amodal hay polygon phần khuất.

Nếu không ước lượng được do che dày, phối cảnh hoặc nhòe, chọn 3 + review khi class/box vẫn nhận biết; nếu không nhận ra class thì ghi vấn đề cấp ảnh, không vẽ box đoán. Vật hoàn toàn khuất không sinh instance. Không tự lấy ví dụ “bóng mờ” làm vật mục tiêu nếu chưa nhận ra đối tượng thật.

Ví dụ thị giác: thanh carrier che các xe ở img_002, người/xe chồng nhau img_005, hàng rào che xe img_018. Không gán sẵn mức 1/2 cho từng vật khi chưa ước lượng bởi người gán. Kiểm biên lý thuyết: không che →0; che rõ dưới nửa →1; đúng nửa/trên nửa →2; không biết →3. Đây không phải nhãn hoặc tỷ lệ đã đo trên các ảnh.

### 2.3 R-04 — `truncated`

Enum `"no"`, `"yes"`, mặc định `"no"`. Chỉ yes khi vật tiếp tục ra ngoài và bị biên ảnh cắt; chạm sát mép chưa đủ kết luận. Box dừng tại biên, không kéo tọa độ ra ngoài. Vật bị xe/người/cột che bên trong ảnh không phải truncation. Một vật có thể vừa truncated=yes vừa occluded_level bất kỳ theo phần trong ảnh. Ví dụ xe máy cắt biên dưới img_026, người/taxi cắt biên img_040; che bởi carrier img_002 không tự tạo truncated.

### 2.4 R-05 — `can_review` và issue

Checkbox mặc định false, chỉ bật khi có box ứng viên hợp lý thuộc class có thể gán nhưng chưa chắc lớp/biên/thuộc tính/bản chất vật. Mức che 3 luôn cần review. Vật rõ ngoài scope bị loại, không dùng can_review để hợp thức hóa class sai. Chưa vẽ được box hoặc chưa nhận dạng class: ghi riêng ảnh, vùng, lý do; sau khóa nhãn độc lập tập hợp `submission/qc/image_issues.csv` với `image,annotator,region,note`. Không mở nhãn của người kia để hỏi trong lượt độc lập. Chỉ chốt sửa ở calibration; giữ dấu vết thay đổi.

`ignore_region` không có ba thuộc tính trên, theo cấu hình CVAT của lab.

## 3. Quy tắc bounding box

### R-06 — Một vật, một rectangle theo phần nhìn thấy

- Box trục thẳng nhỏ nhất chứa toàn bộ phần nhìn thấy của một instance; không thêm lề, không vẽ bù phần khuất/ngoài khung.
- Bao gương, bánh, phần thân và phụ kiện cấu trúc gắn liền nhìn thấy; không bao bóng đổ, phản chiếu, khói, người, hàng rời hoặc nền. Một gương không là instance xe riêng.
- Nhiều phần thấy rời nhau của cùng vật dùng một box bao các phần đó. Rectangle có thể chứa khoảng trống/vật che ở giữa; “box phần thấy” không có nghĩa vẽ nhiều box cho một vật hoặc cắt một mảnh bỏ mảnh khác.
- Từng người lái/hành khách nhận dạng được có person riêng; xe có box riêng, được chồng lấn. Mũ bảo hiểm thuộc hình dáng người, không là object riêng và không chứng minh có xe khuất.
- Trong img_005 và img_026, thử cùng nguyên tắc tách người–xe; không cố định số box toàn ảnh từ ví dụ nếu vật không đạt điều kiện. Với hai người/xe chính ở img_026, ứng viên là hai person + một motorcycle, còn phải xét kích thước và biên.

### R-07 — Vật nhỏ và cụm đông

Chiều cao là chiều cao rectangle phần thấy ở ảnh gốc, không theo mức zoom. `<20 px`: không box object, dùng ignore đúng vùng vật mục tiêu; `=20 px` hoặc lớn hơn: gán object nếu nhận dạng được. Không suy chiều cao amodal để vượt ngưỡng.

Tách từng người/xe nhận dạng được ở img_021, img_030. Chỉ ignore phần cụm không thể tách cá thể đáng tin cậy; vùng ôm sát, không phủ vật đủ điều kiện bên cạnh. Nếu một rectangle không thể khoanh riêng ngoại lệ mà không che vật rõ, không nới ignore tùy tiện: ghi issue để reviewer chốt. Vật ≥20 px chưa biết class không tự thành ignore. Áp dụng cùng điều kiện này cho cả hai lượt gán; không tự mở rộng vùng ignore.

### R-08 — Pickup, xe chở xe, sidecar và trailer

Pickup có cabin/thùng riêng là truck dù gắn canopy (img_037). Đầu kéo đang nối trailer/carrier là một truck; khung sàn, thanh chắn không thành object riêng. Mỗi xe được chở nhận dạng được là car/truck tương ứng riêng (img_002). Person cạnh đuôi carrier vẫn phải xét riêng.

Mô tô-sidecar gắn liền (img_022): một motorcycle bao toàn bộ phần thấy của tổ hợp; không thêm box cho sidecar. Hành khách thật nếu có xét person. Trailer/sidecar tách rời chưa có ví dụ thực tế được xác nhận: không tự ép class; ghi issue để chốt phạm vi. Phần mở rộng này cần chứng cứ nếu xuất hiện, không giả tạo ví dụ.

### R-09 — Tượng, đồ chơi, hình in, phản chiếu, xe chủ

Loại tượng/điêu khắc (img_017, img_027), xe mô hình/đồ chơi (img_038), mannequin (img_033), nội dung in/tranh/màn hình (img_018, img_026), vật chỉ qua phản chiếu gương/kính/đường ướt (img_020, img_015). Đây là lựa chọn scope nhìn trực tiếp, không phủ nhận vật phản chiếu có thật ngoài cảnh.

Xe thật trong showroom hoặc xe diễu hành vẫn xét class; không suy “đồ chơi” chỉ vì trưng bày hoặc hình dáng khác thường. Mascot/đạo cụ chỉ sinh person khi thực sự nhận dạng được phần cơ thể người thật; không đoán người bên trong. Không box các bộ phận xe chủ gắn camera khi đủ căn cứ xác định ego; chưa rõ thì R-05. Ca thật/mô hình không phân biệt được dùng quy trình review theo R-05, không tự gọi vật là tượng.

## 4. Ca khó — quyết định áp dụng và giới hạn

Ảnh gốc ở `data/images/`; bảng này hướng dẫn áp dụng quy tắc, chưa phải annotation. Ca chưa rõ áp dụng R-05: có ứng viên hợp lý thì đánh dấu review, chưa nhận dạng được thì ghi vấn đề cấp ảnh. Việc thống nhất quy trình xử lý không có nghĩa đã xác định bản chất của mọi vật trong ảnh.

Mở ảnh để đối chiếu: [img_002 — carrier](../../data/images/img_002.jpg), [img_005 — người và van](../../data/images/img_005.jpg), [img_009 — minibus](../../data/images/img_009.jpg), [img_024 — xe vàng](../../data/images/img_024.jpg), [img_028 — pickup](../../data/images/img_028.jpg), [img_040 — taxi và phần xe sát biên](../../data/images/img_040.jpg).

| Ảnh | Quan sát / tình huống | Rule ID | Xử lý theo v1.0 | Giới hạn / cần xác nhận |
|---|---|---|---|---|
| img_002 | Xe đầu kéo/carrier hai tầng, xe được chở, người cạnh đuôi | R-03, R-06, R-08 | Truck tổ hợp, xe được chở riêng, người riêng; bao các phần thấy rời nhau | Không đoán số xe khuất/mức che phần trăm; ước lượng từng instance |
| img_005 và img_026 | Người và xe máy chồng lấp; van nền ở 005; tranh nền ở 026 | R-01, R-03–06, R-09 | Tách người/xe; loại tranh; van 005 là ứng viên van; xe 026 cắt dưới | Kiểm riêng từng instance theo R-01/R-02; không gộp người với xe |
| img_009 | Xe minibus thân lớn | R-02 | Ngoài scope, không tự gọi van/truck; người/xe hai bánh khác vẫn xét | Đối chiếu cặp tương phản với van img_005; ca chưa rõ dùng R-05 |
| img_018 | Xe sau rào và chân dung in | R-03, R-06, R-09 | Box xe thật theo phần thấy, loại chân dung; rào là occlusion | Người gán ước lượng mức che trong ảnh, không gán sẵn mức từ bảng này |
| img_021 và img_030 | Dòng xe/bãi xe dày | R-05, R-07 | Tách cá thể rõ, đo vật nhỏ; ignore chỉ ngoại lệ khoanh được | Áp dụng R-07 cho ranh giới cụm; không ignore cả bãi |
| img_022 | Mô tô gắn sidecar | R-08 | Một motorcycle cho tổ hợp | Không tạo class sidecar; chưa có ví dụ sidecar tách rời |
| img_024 | Xe vàng nhỏ trên nóc wagon | R-05, R-09 | Các xe thật khác vẫn gán; xe vàng nếu đủ ứng viên car nhưng chưa rõ bản chất thì review; chưa đủ box thì issue | Cần kiểm khi gán: bản chất xe vàng; không tự chốt là thật/mô hình |
| img_028 | Pickup, ngựa trắng trong thùng, xe đỏ sau | R-01–03, R-06 | Pickup truck, xe đỏ car theo phần thấy; không box ngựa; không bao ngựa vào xe | Ngựa thật/mô hình chưa rõ nhưng đều ngoài scope; chỉ tính che pickup nếu có che thật, không suy từ vị trí đứng |
| img_037 | Pickup gắn khoang cao và bus nền | R-01–02, R-08 | Truck cho pickup; bus ngoài scope | Canopy không tự biến pickup thành van |
| img_040 | Người đội mũ, taxi, tuk-tuk/bus nền, gương/phần xe hai bánh sát dưới | R-02–06 | Person/taxi riêng, truncated theo biên; không dựng toàn xe từ mũ/gương | Cần kiểm khi gán: đủ class/box motorcycle chưa? Có ứng viên hợp lý thì review, nếu không thì issue |
| img_017, img_027, img_033, img_038 | Tượng, mannequin, đồ chơi | R-09 | Không box như person/car/truck; không ignore thay class | Đối chiếu vật thật khác nếu có, không loại cả ảnh theo chủ đề |
| img_014, img_015, img_020 | Blur, phản chiếu đường/gương | R-03, R-05, R-09 | Blur không tự là che; phản chiếu không sinh instance | Mức 3 chỉ khi không biết mức che nhưng còn nhận dạng class/box |

## 5. QC, trách nhiệm và phiên bản

### R-10 — Ngưỡng cố định, không đổi

| Khóa taxonomy | Giá trị giữ nguyên | Cách áp dụng |
|---|---|---|
| min_box_height_px | 20 | Object <20 px xử lý R-07 |
| large_px | 50 | Cao ≥50 px là box lớn |
| iou_thr_large | 0.85 | Ngưỡng so box lớn |
| iou_thr_small | 0.7 | Ngưỡng so box nhỏ |
| match_iou | 0.5 | Ghép 1–1 không phân biệt lớp |
| iaa_iou | 0.85 | IoU trung bình trên matched pairs |
| iaa_class | 0.95 | Đồng thuận lớp trên matched pairs |
| error_rate_img_max | 0.02 | Ảnh lỗi/ảnh duyệt tối đa 2% |

Mốc 50% che của R-03 là ranh giới ý nghĩa thuộc tính trong bản v1.0 này, không sửa bất kỳ khóa rules nào. Ngưỡng cao 50 px ở QC là đại lượng khác.

### R-11 — Độc lập, calibration và quyết định QC

1. Sau khi khóa v1.0 và schema/config khớp, hai người tạo Task riêng, mỗi người gán 40 ảnh độc lập. Không xem nhãn người kia trước nộp riêng. Mỗi thành viên tự quyết định và vẽ box, không dùng pre-label.
2. Kiểm từng box: đúng class/scope, phần thấy, gương/bánh, người–xe riêng, che/cắt, chiều cao, review; giữ ảnh không box trong COCO. Export COCO 1.0 riêng, tắt Save images; validator kiểm cấu trúc, người kiểm ý nghĩa ảnh.
3. Chỉ đo IAA khi đủ 80/80 lượt hợp lệ. Chỉ tính IoU/class trên matched pairs; không có cặp ghi N/A. Báo riêng box chưa ghép và bất đồng ignore. Giữ IAA trước calibration, đối chiếu ca tham chiếu cùng sai.
4. Calibration: mỗi ca có case_id/ảnh, quyết định, Rule ID, phiên bản, người chốt, phiếu sửa, kiểm lại và phạm vi ảnh/lô. Người chốt/reviewer do nhóm xác nhận; hiện chưa phân công. Semantic change cần rà cả lô theo GUIDE. Sau đó mới tạo v1.1/nhãn cuối từ artifact thật.
5. QC duyệt toàn bộ 40 ảnh; nhóm hai người đổi vai kiểm, ưu tiên khác người sửa và ghi mã. Báo ảnh lỗi/ảnh duyệt và annotation lỗi/annotation duyệt, không trộn mẫu số. Một ảnh lỗi là 1/40=2.5%, vượt ngưỡng.
6. Hold khi thiếu bằng chứng/guideline/dữ liệu hoặc chỉ lấy mẫu demo. Rework khi >2% ảnh lỗi hoặc lỗi lặp. Release chỉ khi số liệu đạt, đủ bằng chứng và reviewer xác nhận. Tài liệu này chưa ghi nhận quyết định QC thực tế.


### Từ bản cá nhân đến quy tắc chung

| Nội dung | Đề xuất ban đầu | Lựa chọn v1.0 và lý do |
|---|---|---|
| Che khuất | 101: 25%, mức 3 không rõ; 102: 30%/70%, mức 3 che trên 70% | Dùng ranh giới 50%; mức 3 giữ nghĩa không xác định của v0. Tách mức độ che khỏi khả năng ước lượng. |
| Van/minibus | Hai bản phân biệt cấu tạo thân van với cabin/thùng tải; v0 chưa rõ minibus | Xét cấu tạo theo R-01/R-02, không ép minibus img_009 vào van vì nhỏ trong ảnh. |
| Sidecar, trailer | 101 có đề xuất riêng cho tổ hợp; chưa có mẫu tách rời đủ căn cứ | Tổ hợp đang gắn theo R-08; phần tách rời chưa rõ thì ghi issue, không tạo lớp mới. |
| Vật nhỏ/đám đông | Cần giới hạn cách khoanh ignore để không che vật rõ | Giữ ngưỡng 20 px và điều kiện R-07; không dùng ignore thay quyết định về lớp. |

### Xác nhận và lịch sử phiên bản

101 và 102 đã cùng đồng ý toàn bộ bản chung trước khi chuyển sang gán độc lập. Bản v1.0 này giữ nguyên nội dung quy tắc đã chốt; không ghi kết quả gán hoặc calibration khi chưa có nhãn.

| Phiên bản | Thay đổi | Lý do (ca nào) |
|---|---|---|
| v0 | Guideline khởi đầu của lab | Làm nguồn cho hai đề xuất cá nhân |
| v1.0 — 2026-11-16 | Thống nhất R-01–11, bảng che 50% và nghĩa mức 3, phạm vi lớp, box và ignore; đồng bộ taxonomy v1.0 | Các bất đồng của hai bản cá nhân và ca img_002, img_005, img_009, img_022, img_024, img_028, img_040 |
| v1.0 — biên tập trình bày | Rút gọn lời dẫn, giữ năm phần theo template; làm rõ nguồn quyết định chung | Không đổi lớp, enum, default, ngưỡng hoặc nghĩa quy tắc đã khóa |

Giữ v1.0 trong suốt lượt gán độc lập. Sau khi đủ nhãn, ghi các quyết định calibration và tạo v1.1 theo GUIDE; thay đổi nghĩa phải nêu phạm vi ảnh/lô cần kiểm lại.