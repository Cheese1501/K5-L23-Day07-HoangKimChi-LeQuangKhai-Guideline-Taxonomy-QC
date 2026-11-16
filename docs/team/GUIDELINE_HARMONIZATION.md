# Đối chiếu và đề xuất guideline nhóm 101–102

**ĐÃ XÁC NHẬN QUY TẮC CHUNG v1.0.** Ngày 2026-11-16, người dùng xác nhận “Cả hai đã đồng ý toàn bộ bản chung” cho bản `team-v1.0-draft-2026-11-16-r1`. Ghi nhận đồng ý chung theo thông tin này, không tạo chữ ký riêng. Bảng so sánh giữ nguyên nội dung hai bản cá nhân để thấy lý do chọn quy tắc nhóm.

## 1. Nguồn và ý nghĩa trạng thái

- 101: [guideline cá nhân](../../submission/guidelines/individual/guideline_101.md) tại HEAD `0ee4ceaa93dd64cd417604824c478202fa0e19b9`, mục 2–5; [phân tích ảnh](../member_101/IMAGE_ANALYSIS.md) và [audit](../member_101/FINAL_AUDIT_101.md).
- 102: **chỉ** `git show origin/main:submission/guidelines/individual/guideline_102.md`, sau fetch; origin/main `7cc09717659b9fb359fc93765bd13c2b11580f83`. [Nguồn remote cố định](https://github.com/Cheese1501/K5-L23-Day07-HoangKimChi-LeQuangKhai-Guideline-Taxonomy-QC/blob/7cc09717659b9fb359fc93765bd13c2b11580f83/submission/guidelines/individual/guideline_102.md). Không lấy template 102 local làm nội dung nguồn; không sửa file riêng 102.
- Nguồn bắt buộc: README, GUIDE, RULES, RUBRIC, SUBMISSION, guideline v0/template, taxonomy/schema, CVAT_SETUP và QC_CHEATSHEET. Đã đọc lại trong vòng này.
- Đã mở lại file gốc img_002, img_005, img_009, img_018, img_021, img_022, img_024, img_026, img_028, img_030, img_037, img_040. Ví dụ khác dẫn từ phân tích/audit 101; chưa giả định 102 đã tự xác nhận các ảnh.

Ảnh nguồn để nhóm mở đối chiếu: [carrier img_002](../../data/images/img_002.jpg), [người/van img_005](../../data/images/img_005.jpg), [minibus img_009](../../data/images/img_009.jpg), [rào img_018](../../data/images/img_018.jpg), [xe vàng img_024](../../data/images/img_024.jpg), [pickup img_028](../../data/images/img_028.jpg), [taxi/gương img_040](../../data/images/img_040.jpg).

`AGREED` chỉ dùng khi có bằng chứng cả hai xác nhận **bản nhóm**. `PENDING_CONFIRMATION` là có đề xuất cụ thể, cần hai người duyệt; kể cả hai bản gốc nói giống nhau cũng chưa tự đổi sang AGREED. `NEEDS_EVIDENCE` là còn thiếu quan sát/ca tham chiếu để chốt quyết định. Các quy tắc chung đã được xác nhận qua thông tin người dùng; bốn mục NEEDS_EVIDENCE vẫn chỉ đặc điểm ảnh/ca chưa có ví dụ, được xử lý bằng policy review/issue đã chốt.

## 2. Bảng đối chiếu từng nhóm quy tắc

Rule ID R-01–11 trong cột đề xuất là mã của [bản nhóm](../../submission/guidelines/guideline_v1.0_agreed.md), không mặc nhiên cùng nghĩa với R-xx bản 102.

| Chủ đề / nguồn | Bản 101 | Bản 102 remote | Đề xuất chung và lý do | Ảnh thật / ảnh hưởng annotation | Trạng thái |
|---|---|---|---|---|---|
| Mục tiêu / mục 1 hai bản | Người/xe thật, detection 2D | Cùng mục tiêu, cảnh báo giới hạn an toàn | Giữ scope detection, mỗi instance một class; không coi lab là bằng chứng an toàn | Toàn bộ 40 ảnh; ảnh hưởng chọn object | AGREED |
| Car, truck / mục 2.1 | Sedan/SUV/taxi; pickup→truck | Cùng mapping; truck gồm đầu kéo | R-01 giữ mapping cấu tạo, không theo hàng đang chở | img_012, img_023, img_028, img_037; class | AGREED |
| Van/minibus / I101-08 và R-01–02 của 102 | Van khoang kín nhỏ, minibus chờ nhóm | Van gồm chở người; bus ngoài scope | R-01–02: van cỡ nhỏ thân kín liền có thể chở người; loại minibus thân lớn img_009. Dùng cặp mẫu thay suy số ghế | img_005 vs img_009, img_016; class và chọn/loại | AGREED |
| Motorcycle / bảng class | Hai bánh động cơ, gồm sidecar | Hai bánh động cơ, chưa chốt sidecar | R-01/R-08: một motorcycle cho sidecar gắn liền; phù hợp cấu phần một xe | img_022, img_026; box/count | AGREED |
| Person / I101-02 và R-05 của 102 | Từng người thật gồm lái/hành khách | Cùng hướng, nêu người qua kính | R-06: người thật nhìn được xét riêng dù xe ngoài class; không suy người khuất | img_002, img_005, img_026; count | AGREED |
| Ngoài taxonomy | Không ép tuk-tuk/bicycle/bus; nhóm chốt minibus | Loại bus/bicycle/cyclo/tuk-tuk | R-02 loại danh sách này, không ignore thay class; van dùng cặp mẫu | img_004, img_009, img_023, img_035; scope | AGREED |
| Occlusion / mục 2.3 vs 2.2 | 1 trên 0–25%; 2 trên 25%; 3 không rõ | 1 trên 0–30%; 2 trên 30–70%; 3 trên 70% | R-03 theo người dùng: 0 không che; 1 trên 0 đến dưới 50%; 2 từ 50%; 3 không xác định. Giữ nghĩa 3 v0, không chọn mặc định bản cá nhân | img_002, img_005, img_018; thuộc tính toàn lô | AGREED |
| Truncation / I101-05 và R-03 của 102 | Chỉ cắt bởi biên, box dừng ở biên | Cùng hướng, không tính phần ngoài ảnh vào che | R-04 giữ; tỷ lệ che chỉ xét hình chiếu trong ảnh | img_026, img_040; attributes/geometry | AGREED |
| Can_review / mục thuộc tính và R-09 của 102 | Box ứng viên hợp lệ; thiếu class thì issue | Box hợp lý chưa chắc thì review, chưa box thì issue | R-05 giữ, occlusion 3 cần review; class rõ ngoài scope thì loại | img_024, img_040; cờ và issue | AGREED |
| Box phần thấy / I101-01,04 và R-04 của 102 | Không vẽ bù, không bao nền/hàng | Bổ sung gương/bánh, một box bao các phần thấy rời nhau | R-06 nhận diễn giải chi tiết của 102 để tránh chia một xe thành nhiều box | img_002, img_005; geometry | AGREED |
| Người–xe / I101-02 và R-05 của 102 | Tách person/motorcycle, overlap hợp lệ | Cùng nguyên tắc và điều kiện kích thước | R-06; thử lại trên hai ảnh trước khóa | img_005, img_026; class/count/box | AGREED |
| Vật nhỏ / I101-06 và R-08 của 102 | <20 px ignore, đúng20 xét gán | Cùng ngưỡng; cao phần thấy | R-07 giữ; không sửa min_box_height_px | img_021, img_025; đo trên file gốc | AGREED |
| Cụm đông / I101-06 và R-08 của 102 | Cần rule nhóm, chưa rõ thì issue | Đề xuất ignore phần không tách tin cậy | R-07 chấp nhận có điều kiện: tách mọi cá thể rõ, chỉ vùng ngoại lệ không phủ vật rõ; nếu không khoanh được thì issue | img_021, img_030; vùng ignore có thể thay mẫu so IAA | AGREED |
| Xe chở xe / I101-03 và R-06 của 102 | Carrier một truck, xe trên sàn riêng | Cùng hướng; trailer nối là một truck | R-08 giữ tổ hợp nối, không box cấu phần | img_002; count/box/occlusion | AGREED |
| Trailer/sidecar tách rời | Chưa có rule cụ thể | Trailer rời cần quyết scope | Không tự gán; issue nếu xuất hiện. Cần ảnh thật trước khi mở rộng rule | Chưa xác nhận ảnh trailer rời trong bộ; ảnh img_002 chỉ minh họa tổ hợp nối | NEEDS_EVIDENCE |
| Tượng/đồ chơi/hình in | Loại I101-07,09 | Cùng hướng R-07; thêm màn hình | R-09 giữ scope vật thật trực tiếp; không ignore thay class | img_017, img_018, img_026, img_027, img_033, img_038; loại box thừa | AGREED |
| Phản chiếu/ego | Loại phản chiếu, ego đủ căn cứ | Cùng hướng, có quy trình review | R-09; phân biệt phản chiếu với người thật nhìn qua kính | img_015, img_020; chọn object | AGREED |
| Xe trưng bày/diễu hành, mascot | Xe thật vẫn gán, không suy người ẩn | Quy tắc thật/mô phỏng chung, chưa ca cụ thể | R-09 giữ xe thật dù bối cảnh lạ; mascot chỉ person khi thấy cơ thể người thật | img_019, img_024; scope/class | AGREED |
| Blur và nhận dạng | Chỉ class/box nhận dạng được; không box vệt nhòe | Không đoán class/biên, review | R-03/05: blur không chứng minh che; mức3 không cứu một object không nhận dạng được | img_014; bỏ box đoán | AGREED |
| img_024 | Bản chất xe vàng chưa chắc | Chưa có ID ảnh/quan sát | Các xe thật khác gán; xe vàng theo review/issue, chưa tự chốt thật hay mô hình | Bản chất vật quyết định chọn/loại | NEEDS_EVIDENCE |
| img_028 | Pickup/xe đỏ, ngựa ngoài class; che có điều kiện | Chưa có nhận xét ảnh | R-01–03: truck/car riêng; ngựa không box; không kết luận thật/mô hình từ suy đoán | Cần người kiểm mức che, không ảnh hưởng loại ngựa | NEEDS_EVIDENCE |
| img_040 | Person/taxi; xe hai bánh sát mép chưa rõ | Chưa có nhận xét ảnh | Không dựng toàn xe từ mũ/gương; nhận dạng box phần thấy thì review, không thì issue | Có/không motorcycle và truncation | NEEDS_EVIDENCE |
| QC, phiên bản / mục5 hai bản | Full-batch, mẫu số ảnh/object, ngưỡng cố định | Cùng quy trình; phân biệt IAA và ngưỡng box nhỏ | R-10–11 giữ ngưỡng; human review, calibration có truy vết; không báo số liệu chưa làm | Toàn lô; điều kiện vào IAA/QC | AGREED |

Tổng: **23 chủ đề; 19 AGREED, 0 PENDING_CONFIRMATION, 4 NEEDS_EVIDENCE**. Đây là trạng thái chốt nhóm, không phải điểm rubric hoặc số ca annotation.

## 3. Kiểm tra lại occlusion trên ảnh và thay thế các định nghĩa cũ

Đã mở lại img_002 (thanh carrier che xe), img_005 (người/xe chồng lấn), img_018 (hàng rào che xe), img_021 và img_030 (cụm dày). Quan sát xác nhận có vật che; **không có phép đo vùng khuất hoặc xác nhận hai người đủ để chứng minh vật nào ở 25%, 30% hay sát 50%**. Vì vậy không ghi một phần trăm giả hoặc tuyên bố đã calibration các mốc.

Yêu cầu cuối của người dùng thay việc chọn mốc 25/30 bằng bảng mới. Không tiếp tục dùng hai mốc cũ làm luật song song. R-03 định nghĩa 0%, trên0–dưới50%, từ50%, không xác định; tỷ lệ tính phần hình chiếu trong ảnh, loại phần ngoài khung do truncation. Nếu không ước lượng được chọn3+review, chỉ khi class/box còn hợp lệ. Không đồng nhất “mờ” với “bị che”.

Thử hiểu trước khóa (chưa phải kết quả đã làm): hai người cùng chỉ rõ một xe ở carrier và một người ở img_005, nêu phần thấy/phần bị vật nào che/phần bị biên cắt, chọn mức kèm lý do hoặc chọn3 nếu không biết. Không vẽ nhãn chính thức, không gán trước số liệu IAA. Kiểm biên khái niệm 0%, dưới50%, đúng50%, trên50%, không biết; không dùng ví dụ khái niệm như phép đo ảnh thật.

Đã tìm định nghĩa bằng rg trên toàn repo với Markdown/HTML/JSON (bỏ work và .git), gồm docs/submission/guideline, và đọc riêng remote 102. Danh mục khác nghĩa hoặc chưa đủ định lượng:

| Tài liệu / vị trí | Hiện có | Cách xử lý hiện tại / sau xác nhận |
|---|---|---|
| guideline_101.md mục2.3 dòng58–62; lịch sử cuối file | Mốc25%, mức3 không rõ | Giữ bản cá nhân làm bằng chứng lựa chọn ban đầu. Sau nhóm chốt, thêm liên kết/quyết định Pha 2; không xóa lịch sử hoặc giả rằng cá nhân ban đầu dùng50% |
| individual_notes/101.md dòng62,77 | Nhắc25% để thảo luận | Sau xác nhận, 101 ghi bất đồng và lý do chuyển sang bảng nhóm50%; không ghi cuộc họp chưa diễn ra |
| FINAL_AUDIT_101.md A05, mụcC, F22 | Đánh giá bản101 tại thời điểm audit, có25% | Giữ báo cáo lịch sử; nếu cần bổ sung phụ lục dẫn bản nhóm mới, không sửa PASS cũ như thể đã audit bản mới |
| Remote guideline_102.md dòng43–55 | 30/70%, mức3 che trên70% | 102 tự ghi nhận quyết định nhóm thay nghĩa mức3 và ngưỡng50%; không sửa file riêng102 trong vòng này |
| K5-L23-Day07-Guideline-Taxonomy-QC.md dòng88 | Ví dụ hướng dẫn1–30%/31–70%/>70%, mức3 che nặng | Giữ tài liệu nguồn của lớp; không dùng ví dụ này làm định nghĩa song song trong bản nhóm. Chỉ đạo hiện tại của người dùng chọn bảng50%/không xác định |
| K5-L23-Day07-Guideline-Taxonomy-QC.html — đoạn giải thích CP1 và dữ liệu nội dung checkpoint | Cùng ví dụ30/70% và câu hỏi ngưỡng1–30% | Giữ bản hướng dẫn, ghi khác nghĩa tại đây; không sửa HTML hoặc tái sinh PDF hướng dẫn của lớp |
| Local guideline_102.md bảng thuộc tính | Template chưa điền mức | Không là bản remote mới; không dùng để khóa hoặc tự ghi thay102 |
| guideline/guideline_v0_starter.md dòng35 | 0 rõ/1 ít/2 nhiều/3 không rõ, chưa có% | Giữ nguồn starter theo chỉ dẫn không sửa; bản nhóm định lượng lại nhẹ/nhiều, giữ nghĩa3 |
| docs/member_101/IMAGE_ANALYSIS.md và PROGRESS_101.md | Dùng tên thuộc tính, chưa gán% từng vật | Không có mốc đối nghịch cần thay hàng loạt; sau nhóm chốt dẫn rule/version chung |
| taxonomy.json, schema, CVAT JSON | Chỉ enum/default; không lưu định nghĩa% | Giữ enum/default/rules. Sau duyệt đổi version/definition lớp nếu cần, sinh config; % ghi trong guideline, không thêm trường trái schema |

Tỷ lệ25% tiến độ trong LAB_PROGRESS, ngưỡng2.5% lỗi ảnh và 50px chiều cao là đại lượng khác, không phải định nghĩa occlusion và không được thay hàng loạt. Các bản cá nhân/hồ sơ cũ vẫn có mốc cũ để bảo toàn lịch sử; bản nhóm là nguồn chung duy nhất **sau khi** được xác nhận/khóa.

## 4. Chính sách xử lý mục cần chứng cứ và cập nhật sau xác nhận

- 101 và 102 xác nhận cùng revision, không suy từ việc 102 đồng ý bản cá nhân. Bản nhóm đã ghi ngày ghi nhận và nguồn xác nhận chung của người dùng; không thay bằng chữ ký riêng.
- Chốt van img_005 và minibus img_009, sidecar img_022 và vùng ignore ở img_021/030 bằng quan sát chung. Không cần sáng tạo kích thước thật/số ghế hay tỷ lệ che chính xác.
- Với img_024/028/040, hai người bổ sung quan sát hoặc cùng xác nhận chính sách xử lý bất định R-05 làm quy tắc dùng chung. Không cần giả vờ bản chất vật đã được chứng minh để khóa policy. Ghi rõ trường hợp còn phải review sau gán.
- Trailer rời chưa có ca thật: giữ ngoài scope/issue trong bản đề xuất, không biến ảnh carrier nối thành bằng chứng trailer rời.
- Giữ nguyên các bản cá nhân để so quyết định nhóm, cập nhật ghi chú Pha 2 sau hoạt động thật. Checklist chuyển pha ở [NEXT_PHASE_CHECKLIST.md](NEXT_PHASE_CHECKLIST.md).

## 5. Chuyển Pha 3

Nhóm đã đồng ý R-01–11 và policy R-05/R-07 cho các ca chưa rõ. Taxonomy v1.0 đồng bộ định nghĩa lớp, enum/default/rules giữ nguyên. Không coi việc đồng ý policy là chứng minh xe vàng/ngựa/phần xe tiền cảnh đã được xác định bản chất. Khi annotation, có ứng viên hợp lý thì can_review; chưa box/class thì issue. Các checklist thảo luận ở mục 4 là căn cứ giải thích, không còn là yêu cầu xin lại cùng xác nhận đã có.
