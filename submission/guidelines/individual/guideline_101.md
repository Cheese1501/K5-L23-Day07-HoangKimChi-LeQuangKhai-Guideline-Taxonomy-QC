# Guideline gán nhãn cá nhân 101 — diễn giải taxonomy v0

- **Mã thành viên:** 101
- **Phiên bản tham chiếu:** `submission/taxonomy.json` — `v0`
- **Ngày lập bản đối chiếu:** 2026-11-16
- **Phạm vi:** đề xuất quy tắc cho lượt gán cá nhân 101; không phải guideline nhóm `v1.0` và không thay thế taxonomy.

Các quy tắc mang mã `I101-xx` để tra cứu trong phần ca khó và ghi chú cá nhân. Đây là mã nội bộ của bản cá nhân, không phải mã rule nhóm. Các ngưỡng có sẵn trong taxonomy/QC của lab được giữ nguyên. Với điểm v0 chưa định lượng (đặc biệt mức che khuất và pickup/minibus), phần dưới nêu cách diễn giải đề xuất để 101 kiểm tra và mang vào thảo luận nhóm.

## 1. Mục tiêu và phạm vi

Mục tiêu là tạo bounding box 2D nhất quán cho người và phương tiện thật nhìn thấy trong bộ ảnh đường phố được giao cho mã 101. Bộ 101 có 40 ảnh (`img_001.jpg`–`img_040.jpg`). Mỗi vật thể mục tiêu được biểu diễn riêng; người và phương tiện không gộp thành một instance. Ảnh dùng để huấn luyện phát hiện đối tượng nên box, class và thuộc tính phải mô tả vật thể trong ảnh, không phải vật thể được suy đoán ngoài khung.

Khi gán nhãn chính thức, chỉ dùng các đề xuất dưới đây nếu đã được nhóm chấp thuận trong guideline/taxonomy v1.0 đã khóa. Giai đoạn cá nhân hiện dùng taxonomy v0 để hình thành cách hiểu ban đầu. Không bổ sung class hoặc sửa `rules` bằng guideline này.

### Nguyên tắc chung

1. Chỉ gán class có trong taxonomy; không ép vật ngoài taxonomy vào class gần giống.
2. Một người, một xe máy, một xe con hoặc một xe tải là các vật riêng, dù chúng chồng lấp.
3. Box theo vật thể thật nhìn thấy, không theo bóng, phản chiếu, chữ, họa tiết, hàng hóa rời hoặc nền cảnh.
4. Khi class hợp lệ nhưng ranh giới/thuộc tính còn nghi vấn, giữ box ứng viên và bật `can_review`. Khi vật không có class phù hợp, không tạo box giả; ghi ảnh/vùng/lý do để nhóm xử lý.
5. Không bỏ ảnh trống khỏi Task/COCO. Ảnh không có vật thể phù hợp vẫn có trong danh sách ảnh.

## 2. Lớp và thuộc tính

### 2.1 Định nghĩa class và inclusion/exclusion

| Class | Định nghĩa và trường hợp gán | Ví dụ trong bộ ảnh | Không gán / dễ nhầm |
|---|---|---|---|
| `car` | Ô tô chở người, gồm sedan, hatchback, SUV và taxi. Một chiếc ô tô thật vẫn là `car` khi đỗ, chở hàng nhỏ hoặc tham gia diễu hành. | Ô tô trên carrier ở `img_002`; SUV ở `img_012`, sedan ở `img_023`; taxi ở `img_040`; ô tô diễu hành thật ở `img_019` nếu xác nhận đây là xe cơ giới thật. | Xe tải/pickup có khoang hàng riêng; xe buýt/minibus nếu không được nhóm quy về `van`; xe đồ chơi/tượng/hình xe in; hình xe chỉ trong gương (`img_020`). |
| `truck` | Xe chở hàng có cấu tạo khoang/thùng hàng riêng biệt với cabin. Theo cách hiểu cá nhân đề xuất, pickup có cabin và thùng hàng riêng thuộc `truck`; xe đầu kéo/car-carrier được tính một phương tiện tải. | Pickup ở `img_001`, `img_012`, `img_028`, `img_037`; xe tải nhỏ ở `img_036`; xe chở ô tô ở `img_002`. | Ô tô con chở một vật trong cabin; van có thân kín liền; tuk-tuk ba bánh; tượng pickup ở `img_027`. |
| `van` | Xe cỡ nhỏ có khoang chở hàng kín, thân dạng van. Phân lớp theo cấu tạo xe, không theo màu, hàng đang chở hoặc phối cảnh. | Minivan nền ở `img_005` là ứng viên cần rà theo rule này. | Xe buýt/minibus chở khách không tự động là van (`img_009`, `img_037`); pickup gắn nắp khoang phụ kiện vẫn là pickup nếu cabin/thùng tách biệt; tuk-tuk không phải van. |
| `motorcycle` | Xe hai bánh có động cơ, gồm mô tô và scooter. Mỗi xe là một instance. Đề xuất một box cho mô tô gắn sidecar vì sidecar không có class riêng. | Xe máy ở `img_005`, `img_006`, `img_021`, `img_026`; mô tô-sidecar ở `img_022`. | Xe đạp và xích lô/xe ba bánh không động cơ; tuk-tuk/auto-rickshaw ba bánh; xe máy điêu khắc (`img_011`) hoặc đồ chơi (`img_038`). |
| `person` | Người thật đang đi bộ, đứng, ngồi hoặc điều khiển phương tiện. Mỗi cá thể nhận dạng được có một box, kể cả người lái và hành khách. | Người đi xe máy ở `img_005`, `img_026`; người lái xe diễu hành ở `img_019`; người ở tiền cảnh trước taxi ở `img_040`. | Tượng người (`img_017`), ma-nơ-canh (`img_033`), chân dung in (`img_018`), mascot/đạo cụ không có người thật nhận dạng được, hoặc người chỉ xuất hiện trong phản chiếu. |
| `ignore_region` | Vùng ảnh mà guideline cho phép không gán từng vật thể bên trong; theo QC cheatsheet, dùng cho vật dưới 20 px. Đây là vùng, không phải object hay class dự phòng. | Vật dưới ngưỡng 20 px; vùng đông chỉ khi guideline nhóm chỉ rõ cách khoanh. | Không dùng bao trùm ảnh, thay class bị thiếu, che một box rõ, hoặc che tượng/đồ chơi chỉ để tránh quyết định. `ignore_region` không có thuộc tính trong CVAT. |

### 2.2 Vật thể không có class tương ứng

Taxonomy v0 không có `bus`, `bicycle`, `cyclo`, `tuk_tuk`, `animal`, `toy` hoặc `statue`. Đề xuất cá nhân là không gán các vật này vào `truck`, `motorcycle`, `person` hay `van` chỉ vì hình dáng gần giống. Ví dụ:

- Tuk-tuk ở `img_004`, `img_016`, `img_035`: không đổi thành `motorcycle` vì có ba bánh hoặc thành `truck` vì có khoang chở.
- Bus/minibus ở `img_009`, `img_031`, `img_037`: chờ nhóm định nghĩa có nằm trong `van` hay không; không tự chuyển thành `truck`.
- Xe đạp/xích lô ở `img_003`, `img_023`, `img_029`, `img_039`: không phải `motorcycle`.
- Tượng, đồ chơi, mannequin, poster và phản chiếu: không phải vật thể vật lý thuộc lớp mục tiêu.
- Khi vật ngoài taxonomy gây cản trở khiến không thể gán vật mục tiêu, ghi rõ `image`, `region`, `note` theo quy trình `image_issues.csv` sau khi khóa nhãn. Không dùng `ignore_region` để giải quyết thiếu class nếu nhóm chưa thống nhất.

### 2.3 Thuộc tính

Chỉ các giá trị đã khai báo trong taxonomy được dùng: `occluded_level` = `"0"`, `"1"`, `"2"`, `"3"`; `truncated` = `"no"`/`"yes"`; `can_review` = checkbox. Mọi ngưỡng sau đây giữ nguyên ngưỡng cố định tại taxonomy: `min_box_height_px=20`, `large_px=50`, `iou_thr_large=0.85`, `iou_thr_small=0.7`, `iaa_iou=0.85`, `iaa_class=0.95`, `match_iou=0.5`, `error_rate_img_max=0.02`.

#### `occluded_level`

Che khuất xảy ra khi một vật khác trong cảnh che một phần vật thể. Đề xuất cách ước lượng để 101 kiểm tra:

| Giá trị | Cách hiểu đề xuất |
|---|---|
| `"0"` | Không bị vật khác che. |
| `"1"` | Bị che nhẹ, ước tính trên 0% đến 25% diện tích vật thể. |
| `"2"` | Bị che nhiều, ước tính trên 25% diện tích vật thể, kể cả trên 50%, khi vẫn nhận dạng được class và ước lượng được mức che. |
| `"3"` | Không rõ mức che theo nghĩa v0, không phải một mức phần trăm cao hơn `2`. Chỉ giữ box ứng viên khi vẫn nhận ra class; bật `can_review` nếu hình dạng/biên box chưa chắc. Nếu không nhận ra class thì không gán box và ghi issue. |

Tỷ lệ là ước lượng trực quan đối với phần vật thể dự kiến, không phải phép đo pixel chính xác. Nếu không xác định được class, không tạo nhãn đoán mò; ghi vấn đề cấp ảnh. Mốc 25% là đề xuất định lượng cá nhân; không dùng mốc 50% để đổi nghĩa mức `3`. Đây là đề xuất vì v0 không đặt ngưỡng phần trăm; cần nhóm thống nhất trước khi dùng chung. Che khuất trong ảnh không làm `truncated=yes`.

#### `truncated`

- `"yes"` khi vật thể tiếp tục ra ngoài khung ảnh và bị đường biên ảnh cắt (ví dụ xe ở `img_015`, xe/người sát mép ở `img_034`, taxi ở `img_040`).
- `"no"` khi toàn bộ vật thể nằm trong khung, dù một phần bị xe/người/hàng rào che.
- Không gán `yes` chỉ vì vật bị cắt bởi vật khác, bị blur hoặc nằm sau hàng rào.
- Box dừng tại biên ảnh; không kéo tọa độ ra ngoài ảnh để vẽ phần không nhìn thấy.

#### `can_review`

- Mặc định `false`.
- Đặt `true` trên box hợp lệ khi class, biên box, mức che hoặc truncation cần reviewer kiểm tra; ví dụ xe chở ở `img_002`, xe ở `img_009` chỉ khi nhóm đã cho phép mapping vào `van`, pickup ở `img_001` hoặc xe trưng bày ở `img_024`.
- Không dùng `can_review` để thay `image_issues.csv` cho vật không có class. Không tick trên box tượng, poster, đồ chơi hoặc vật chỉ có trong gương.
- Sau khi reviewer quyết định, giữ dấu vết theo quy trình calibration; không tự xóa cờ để làm nhãn trông chắc chắn hơn.

## 3. Quy tắc bounding box

### I101-01 — Box riêng, trục thẳng, sát vật

Vẽ rectangle theo trục ảnh, ôm sát phần nhìn thấy của đúng một instance. Loại bỏ bóng đổ, vùng đường, đồ vật rời và khoảng trống không thuộc vật. Không gộp nhiều người/xe thành một box. Hai box khác instance được phép chồng lấn.

### I101-02 — Người và người điều khiển phương tiện

Người đi bộ, người lái và hành khách đều là `person`. Vẽ box cho từng cá thể nhận dạng được, từ phần cơ thể nhìn thấy; mũ bảo hiểm thuộc hình dáng người nhưng không tạo box riêng. Vẽ xe thành box khác. Khi một người bị xe/người khác che, box của người theo phần nhìn thấy, gắn `occluded_level`; không dùng một box chung quanh người và xe. Nếu chỉ thấy mũ/đầu mà không xác định chắc là người thật, bật `can_review` khi có box ứng viên; nếu chỉ là tượng/mascot, không gán `person`.

### I101-03 — Phương tiện được chở

Trong `img_002`, đề xuất box riêng cho xe tải/car-carrier và từng xe con đủ nhận dạng được trên sàn. Không vẽ box cho khung sàn, thanh chắn hay bánh carrier như vật thể riêng. Xe chở bị che bởi khung/xe khác ghi `occluded_level`; chỉ dùng `truncated=yes` khi xe thực sự bị mép ảnh cắt. Không suy diễn thêm xe bị che hoàn toàn.

### I101-04 — Che khuất

Box chỉ ôm phần vật thể nhìn thấy; không tự dựng hình học của phần khuất. Chọn `occluded_level` theo mục 2.3. Với nhiều vật thể chồng lấn, từng vật vẫn có box riêng nếu nhận dạng được. Hàng rào, người, xe khác hoặc hàng hóa có thể gây occlusion; bóng tối/phản chiếu không được tính là vật che.

### I101-05 — Cắt mép ảnh

Khi vật thể bị khung ảnh cắt, box chạm đúng biên tương ứng và thuộc tính là `truncated=yes`. Không kéo box ra ngoài khung. Nếu vật vừa bị che vừa bị cắt mép, ghi cả mức occlusion và truncation phù hợp. Mất một phần do người/vật khác che không phải truncation.

### I101-06 — Vật nhỏ và cảnh đông

Đo chiều cao box trên ảnh gốc, không dùng contact sheet hoặc ảnh phóng to. Lab đặt `min_box_height_px=20`; QC cheatsheet hướng dẫn vật thấp hơn 20 px xử lý bằng `ignore_region`. Với chiều cao đúng 20 px trở lên, gán nếu class/biên đủ rõ. `ignore_region` không phủ instance rõ hoặc cả ảnh; chỉ dùng cho cụm không thể tách nếu guideline nhóm đã quy định cách khoanh. Trong đám đông, tạo box riêng cho từng người/xe nhận dạng được; không gộp thành một người/xe. Nếu chưa có rule cho cụm không thể tách, ghi issue để nhóm quyết định.

### I101-07 — Xe trên đường, xe trưng bày, đồ chơi và hình ảnh

- Phương tiện thật có thể đang chạy, đỗ, ở xưởng hoặc tham gia diễu hành; bối cảnh một mình không quyết định class.
- Tượng, tác phẩm điêu khắc, mannequin, đồ chơi/mô hình, hình in và vật chỉ xuất hiện trong gương/phản chiếu không được gán là người/phương tiện thật.
- Xe đầy đủ kích thước nhưng đang trưng bày vẫn là ứng viên class xe nếu là phương tiện thật (ví dụ các xe trong showroom `img_024`). Nếu không xác định được vật trưng bày là xe thật hay mô hình, dùng `can_review` trên box ứng viên, không tự suy đoán.
- Xe thật trong đoàn diễu hành (`img_019`) có thể là `car`; mascot/người hóa trang chỉ là `person` khi cơ thể người thật được nhận dạng, không box đạo cụ thành người.

### I101-08 — Phân loại phương tiện ranh giới

`truck` dựa trên cabin và khoang/thùng hàng riêng; `van` dựa trên thân khoang kín cỡ nhỏ. Pickup có thùng hàng riêng đề xuất vào `truck`, không đổi thành `van` chỉ vì có nắp phụ kiện (`img_037`). Taxi và xe chở người là `car`. Bus/minibus và các xe ba bánh không có class rõ trong v0: không ép nhãn, đưa ra thảo luận. Nếu nhóm chốt mapping khác thì dùng v1.0, không giữ quy tắc cá nhân trái v1.0.

### I101-09 — Blur, phản chiếu và ranh giới không rõ

Với vật bị nhòe (`img_014`), chỉ box khi loại vật và phần nhìn thấy đủ để nhận dạng; không vẽ quanh toàn vệt nhòe. Xe trong gương (`img_020`) hoặc hình xe phản chiếu trên đường ướt (`img_015`) không tạo instance bổ sung. Box class hợp lệ nhưng chưa chắc được bật `can_review`; trường hợp ngoài class không được ép nhãn.

### I101-10 — Xe chủ (ego)

Đề xuất không box các bộ phận của xe gắn camera (gương, cửa, nắp xe) thành instance riêng. `img_020` cho thấy gương và viền cửa xe chủ; xe trong gương loại theo I101-09. V0 chưa quy định ego nên nhóm cần chốt scope này trong Pha 2. Nếu không xác định được xe chủ hay xe khác, ghi vùng/lý do cần xem lại; không suy đoán một box xe đầy đủ từ bộ phận rời.

## 4. Ca khó và quyết định đề xuất

| Ảnh | Vấn đề | Quy tắc áp dụng | Quyết định đề xuất | Giải thích |
|---|---|---|---|---|
| `img_002.jpg` | Xe con xếp nhiều tầng trên carrier; khung che một phần | I101-03, I101-04 | Một box cho xe tải/carrier và box riêng cho từng xe con đủ nhận dạng; occlusion cho phần bị khung/xe khác che; `can_review` cho box xe con ranh giới không rõ. | Xe vận chuyển và xe được chở là các phương tiện riêng; khung chở không phải xe con. |
| `img_005.jpg` | Nhiều người lái/hành khách và xe máy chồng lấp; van nền; người tiền cảnh cắt mép dưới | I101-02, I101-05, I101-08 | Tách người với xe; `truncated=yes` cho người/xe thực sự cắt biên; van chỉ gán nếu đúng định nghĩa, còn không chắc bật `can_review`. | Mũ/áo và tư thế ngồi không làm người thành bộ phận của xe; che bên trong ảnh không phải truncation. |
| `img_009.jpg` | Minibus nhỏ, class v0 chưa rõ | I101-08 | Không tự đổi thành `truck`; đề xuất chờ nhóm quyết định có thuộc `van` hay không, hoặc giữ ngoài taxonomy và ghi issue. | “Nhỏ” không đủ để phân biệt bus với van. |
| `img_011.jpg` | Tượng lớn và tác phẩm kim loại hình xe máy tại sự kiện | I101-07 | Không gán tác phẩm như `person`/`motorcycle`; gán người thật ở hậu cảnh nếu đủ kích thước. | Hình dáng giống class không làm tượng thành phương tiện/người thật. |
| `img_014.jpg` | Giao thông nhòe chuyển động | I101-09 | Chỉ gán phương tiện còn nhận dạng được; không tạo box dựa trên vệt blur. | Box trên vùng blur mơ hồ dễ khác nhau và sai vị trí. |
| `img_017.jpg` | Tượng cưỡi ngựa có cone đặt trên đầu | I101-07 | Không gán `person` hay xe; không dùng `ignore_region` toàn ảnh. | Tượng và cone không thuộc class mục tiêu. |
| `img_019.jpg` | Xe diễu hành hình ô tô và mascot chuột; đông người phía sau rào | I101-02, I101-07 | Xe cơ giới thật là `car`; người lái là `person`; mascot không phải người. Người trong đám đông tạo box riêng nếu nhận dạng được. | Bối cảnh diễu hành không biến xe thật thành đồ chơi; đạo cụ không biến thành người. |
| `img_020.jpg` | Xe xuất hiện trong gương chiếu hậu | I101-07, I101-09 | Không box xe chỉ hiện trong gương. | Phản chiếu không phải instance trực tiếp trong cảnh. |
| `img_022.jpg` | Mô tô gắn sidecar | I101-08 | Đề xuất một box `motorcycle` cho tổ hợp mô tô-sidecar; không box sidecar riêng. | Taxonomy không có class sidecar; một quy tắc thống nhất tránh tách cấu phần tùy ý. |
| `img_023.jpg` | Người đạp xích lô/xe ba bánh và ô tô, xe máy nền | I101-02, I101-08 | Box người; xích lô ngoài taxonomy; gán ô tô và xe máy thấy rõ. | Người có thể thuộc `person` dù phương tiện họ điều khiển không có class. |
| `img_024.jpg` | Showroom và xe vàng đặt trên nóc xe wagon | I101-07 | Box các xe thật; chiếc xe vàng chỉ gán nếu là phương tiện thật, nếu là mô hình/đạo cụ thì bỏ; bật `can_review` nếu chưa xác định. | Bối cảnh trưng bày không đủ để quyết định scale/bản chất chiếc xe vàng. |
| `img_026.jpg` | Hai người trên xe máy; tranh tường ở nền | I101-02, I101-04, I101-07 | Hai box `person`, một box `motorcycle`; xe máy cắt biên dưới đặt `truncated=yes`; không gán hình minh họa trên tường. | Người, xe và hình trên tường là ba thứ khác nhau; hình vẽ không phải instance vật lý. |
| `img_027.jpg` | Tác phẩm điêu khắc hình pickup trên bệ | I101-07 | Không gán như `truck`/`car`. | Đây là vật trưng bày, không phải phương tiện thật. |
| `img_028.jpg` | Pickup chở ngựa trắng; không thể kết luận ngựa thật hay mô hình | I101-04, I101-08 | Box pickup theo phần xe; chỉ ghi occlusion nếu ngựa thực sự che phần xe nhìn thấy; xe đỏ phía sau bị pickup che. Không gán ngựa vì taxonomy không có class động vật; không gọi ngựa là tượng khi ảnh không chứng minh. | Quy tắc bám vào cái nhìn thấy và tránh suy diễn bản chất vật ngoài taxonomy. |
| `img_030.jpg` | Bãi xe máy dày, nhiều xe che nhau | I101-04, I101-06 | Tách từng xe phân biệt được; vật dưới 20 px theo `ignore_region`; cụm lớn không thể tách thì ghi issue nếu guideline nhóm chưa quy định cách khoanh. | Box suy đoán trên toàn cụm gây thừa box và bất đồng lớn. |
| `img_033.jpg` | Mannequin và phản chiếu ở cửa kính | I101-07 | Không gán mannequin, ảnh hoặc phản chiếu thành `person`. | Không có người thật nhận dạng được trong cửa kính. |
| `img_035.jpg` | Tuk-tuk ba bánh chở kiện hàng cao | I101-08 | Không ép tuk-tuk sang `truck`/`motorcycle`; box người/motorcycle thật nếu có; ghi issue cho phương tiện thiếu class. | Hàng hóa cao không biến phương tiện ba bánh thành xe tải theo v0. |
| `img_037.jpg` | Pickup có nắp khoang cao và bus nền | I101-08 | Pickup có cabin/thùng riêng theo đề xuất là `truck`; bus chờ quyết định class. | Nắp phụ kiện không làm xe thành van; bus không được khai báo riêng. |
| `img_038.jpg` | Nhiều xe mô hình và đồ chơi trong cửa hàng | I101-07 | Không gán `car`/`person` cho đồ chơi hoặc thú bông. | Vật trưng bày không phải instance giao thông thật. |
| `img_040.jpg` | Người đội mũ ở tiền cảnh, taxi lớn, bus và xe khác ở nền | I101-02, I101-05, I101-08 | Box người riêng và taxi `car`; gương/phần xe hai bánh sát biên dưới chưa đủ để dựng box cả xe; nếu xác định được motorcycle thì box phần thấy và `can_review`. Taxi và người bị biên ảnh cắt đặt `truncated=yes`; bus ngoài class nếu nhóm chưa có rule. | Mũ bảo hiểm không đủ chứng minh có motorcycle; box dựa trên vật thật trong ảnh. |

## 5. Quality Control

### Kiểm tra từng box

- Class có trong taxonomy đã khóa và phù hợp cấu tạo vật thể.
- Box ôm sát phần vật nhìn thấy, không gộp người/xe, không gồm bóng, nền, hàng hóa rời hoặc phản chiếu.
- Không bỏ sót người lái/hành khách nhìn thấy; cũng không tạo person từ tượng, mascot, ảnh in hoặc mannequin.
- `occluded_level` mô tả che bởi vật trong cảnh; `truncated` chỉ mô tả cắt bởi biên ảnh.
- `can_review=true` chỉ khi box thuộc class hợp lệ nhưng cần người khác kiểm; vật thiếu class được ghi thành issue riêng.
- Chiều cao box đo trên ảnh gốc. Vật dưới 20 px xử lý theo quy tắc `ignore_region`; không dùng threshold scale của bản contact sheet.
- Ảnh không có annotation vẫn hiện trong COCO.

### Các ngưỡng QC cố định của lab

Không thay đổi các giá trị trong `taxonomy.json`:

| Kiểm tra | Quy tắc |
|---|---|
| Vật nhỏ | Box thấp hơn 20 px: theo quy tắc vật nhỏ/`ignore_region` của lab. |
| So IoU box | Box cao từ 50 px: ngưỡng 0.85; box thấp hơn 50 px: 0.7. |
| Ghép cặp IAA | Ghép 1:1 khi IoU đạt ít nhất 0.5; chỉ tính thống kê IoU/class trên matched pairs. |
| IAA | IoU trung bình tối thiểu 0.85 và class agreement tối thiểu 95%. Không có matched pair thì ghi N/A. |
| Lỗi theo ảnh | Tối đa 2% ảnh được duyệt. Với 40 ảnh, 1 ảnh lỗi là 1/40 = 2.5%, vượt ngưỡng. |

Release yêu cầu duyệt toàn bộ lô; vòng lấy mẫu demo luôn Hold. Thiếu bằng chứng/guideline/dữ liệu thì Hold; trên 2% ảnh lỗi hoặc lỗi lặp thì Rework. Nhóm phân công người chốt calibration và người kiểm lại (ưu tiên khác người sửa; nhóm hai người đổi vai), lưu mã người, Rule ID, phiên bản, phạm vi và kết quả kiểm lại; hiện chưa có người được xác nhận.

Báo cả lỗi theo ảnh (ảnh lỗi/ảnh đã duyệt) và theo đối tượng (annotation lỗi/annotation đã duyệt). Tỷ lệ phải ghi đủ tử số/mẫu số. Box không ghép được ghi riêng, không đưa vào mẫu số matched pairs. Quyết định Release/Rework/Hold thuộc reviewer và phải dựa trên review thực tế; cá nhân không tự tạo kết quả QC.

### Checklist trước khi gửi nhãn cá nhân

1. Project CVAT dùng class/attributes đúng phiên bản taxonomy nhóm đã khóa.
2. Task có đúng 40 ảnh trong `submission/qc/assignments/101.txt`, không thiếu ảnh trống.
3. Mỗi box có class, geometry và thuộc tính; `ignore_region` không mang attributes.
4. Xem lại từng ảnh ở độ phân giải gốc, tập trung `img_002`, `img_005`, `img_017`, `img_019`, `img_020`, `img_026`, `img_028`, `img_030`, `img_033`, `img_035`, `img_037`, `img_038`, `img_040`.
5. Export COCO 1.0, tắt Save images và giữ nguyên tên ảnh.
6. Chạy `python scripts/validate_labels.py submission/labels/101.json`; giải quyết mọi lỗi dựa trên ảnh gốc, không sửa tọa độ chỉ để validator pass.
7. Gửi riêng nhãn 101 theo quy trình; không mở/so sánh nhãn thành viên khác trước khi hoàn tất độc lập.

## 6. Kết luận và lịch sử phiên bản

Trọng yếu nhất là tách đúng từng người và phương tiện, không nhầm occlusion với truncation, không gán vật thể in/tượng/đồ chơi/phản chiếu, không ép loại xe thiếu class vào taxonomy, và dùng `can_review` thay cho phỏng đoán. Những đề xuất cá nhân này cần được kiểm tra với ảnh gốc và thay thế bằng quy tắc nhóm v1.0 trước khi annotation chính thức.

| Phiên bản | Nội dung | Căn cứ |
|---|---|---|
| v0 | Guideline khởi đầu của lab; quy tắc lớp, thuộc tính và box còn khái quát. | `guideline/guideline_v0_starter.md`, `submission/taxonomy.json` |
| Audit 2026-11-16 | Giữ mức occlusion 3 là không rõ; làm rõ mốc 0/25%, ego, QC và ví dụ ảnh. Chưa khóa quy tắc nhóm. | `docs/member_101/FINAL_AUDIT_101.md` |
| Bản cá nhân 101 | Bổ sung quy tắc đề xuất và ca ảnh để 101 rà soát; chưa phải guideline nhóm. | 40 ảnh trong `work/101/images/`; chi tiết tại `docs/member_101/IMAGE_ANALYSIS.md` |
