# Checklist chuyển sang annotation — nhóm 101–102

**PENDING TEAM APPROVAL.** Đối chiếu ngày 2026-11-16 với bản `team-v1.0-draft-2026-11-16-r1`. `READY` chỉ nghĩa hạng mục chuẩn bị sẵn; không phải toàn pha đã được thông qua. `BLOCKED` là thiếu điều kiện tiên quyết; `NOT STARTED` là chưa có bằng chứng hoạt động tương ứng.

## 1. Điều kiện vào Pha 3

| Hạng mục | Trạng thái | Bằng chứng hiện có / thiếu | Hành động tiếp |
|---|---|---|---|
| Bản nhóm đủ nội dung template | READY | [Guideline v1.0 dự thảo](../../submission/guidelines/guideline_v1.0_agreed.md) có mục tiêu, lớp/thuộc tính, box, ca thật, QC/phiên bản/xác nhận | Hai người đọc cùng revision; nội dung đủ không thay chữ ký |
| Đối chiếu hai bản gốc | READY | [Harmonization](GUIDELINE_HARMONIZATION.md); nguồn101 `0ee4cea`, nguồn102 remote `7cc0971` | Giữ nguyên bản cá nhân để truy vết |
| Bảng occlusion đề xuất mới | READY | R-03:0 không che,1 dưới50%,2 từ50%,3 không xác định; không tính truncation | Đây là đề xuất đã cập nhật theo người dùng, chưa là xác nhận của cả hai |
| Quy tắc occlusion được hai người xác nhận | BLOCKED | Chưa có xác nhận cùng revision/cách ước lượng | Thử giải thích cùng vật ở img_002/005/018; chốt nghĩa3 và biên50% |
| Scope van/minibus, sidecar, cụm ignore | BLOCKED | Đã có lựa chọn cụ thể R-01/02/07/08, chưa đủ bằng chứng nhóm chấp thuận | Chốt img_005–009, img_022, img_021/030 |
| Chính sách img_024/028/040 | BLOCKED | Quan sát AI có, điểm chưa rõ ghi NEEDS_EVIDENCE | Bổ sung quan sát hoặc cùng duyệt policy review/issue cho bất định; không đoán |
| Hoàn tất/xác nhận bản cá nhân | BLOCKED | 101 còn chờ tự kiểm; remote102 mục4 thiếu ID ảnh | Mỗi người tự hoàn thiện ca thật và ghi AI/cách kiểm lại; không viết thay102 |
| Xác nhận nhóm101 | BLOCKED | Ô ngày/bằng chứng để trống | 101 xác nhận revision cụ thể sau đọc/chỉnh |
| Xác nhận nhóm102 | BLOCKED | Chấp thuận bản cá nhân102 không phải bản nhóm | 102 xác nhận cùng revision sau đọc/chỉnh |
| Taxonomy/schema hiện tại hợp lệ | READY | Version v0, sáu class, enum/rules chưa đổi; kiểm kỹ thuật bên dưới | Giữ nguyên cho tới khi đủ xác nhận |
| Taxonomy khớp scope/phiên bản nhóm đã khóa | BLOCKED | Định nghĩa hiện tại ngắn và version v0; draft diễn giải van/pickup rõ hơn | Sau xác nhận: cập nhật definitions theo R-01, version v1.0; giữ enum/default/rules/schema |
| CVAT JSON cục bộ đúng cấu trúc | READY | Sáu class; object có3 attributes, ignore không attributes; chưa được sinh từ taxonomy nhóm v1.0 | Sau cập nhật taxonomy mới chạy generator/kiểm lại; JSON không mang nghĩa% che |
| CVAT Project/Task đúng bản khóa | NOT STARTED | Chưa có bằng chứng Project/Task/version thực tế của hai người | Tạo cấu hình sau khóa; xác nhận mỗi Task đúng40 frame |
| Assignment40 ảnh/người | READY | Local assignment.csv và hai assignments/<mã>.txt có sẵn; kiểm hash bản sao ở work bên dưới | Không chạy split_assign ghi đè; nhóm xác nhận/chia sẻ chính bản hiện có |
| Assignment đã chia sẻ/khóa chung | BLOCKED | Assignment hiện untracked, origin/main chưa có; không commit/push trong nhiệm vụ này | Nhóm chọn bản chung, sau này người được giao bàn giao qua kênh riêng |
| TEAM.md và vai trò | BLOCKED | Local đã có101/102; tên nhóm/điều phối/reviewer chưa xác nhận | Nhóm cung cấp mã người/role thật; tránh diễn giải80/80 lượt được giao thành hoàn tất |
| Khả năng export COCO riêng | NOT STARTED | Chưa có102.json hoặc101.json, chưa có xác minh quyền/export tại instance lớp | Mỗi người thực hiện export riêng theo runbook, không tạo JSON mẫu làm kết quả |
| Annotation độc lập | BLOCKED | Chưa khóa v1.0, chưa cóCOCO | Chỉ bắt đầu khi toàn bộ điều kiện khóa đã đáp ứng |
| Validation nhãn/IAA/calibration/QC | NOT STARTED | Chưa có annotation thật/summary/decisions/reviews | Thực hiện theo thứ tự sau annotation; không tạo artifact giả |

**Kết luận chuyển pha: BLOCKED.** Bản đề xuất đã có đủ phần để hai người review nhưng chưa đủ điều kiện khóa. Một file mang tên agreed và cấu hình schema-pass không tự mở cổng annotation.

## 2. Thứ tự khóa và cập nhật sau khi có xác nhận thật

1. Hoàn tất phần cá nhân và quyết định Pha2, xác nhận R-01–11 và các mục mở trên cùng revision. Nếu sửa nghĩa đề xuất, tăng revision và xin xác nhận lại, không giữ chữ ký cho nội dung mới.
2. Điền ngày/bằng chứng thật ở bảng cuối guideline; khi cả hai hợp lệ mới bỏ cảnh báo pending và ghi bản khóa v1.0. Ghi nhận mã người điều phối/người chốt/reviewer ở TEAM.md; số lượt hoàn tất chỉ ghi khi có nhãn thật.
3. Đồng bộ `submission/taxonomy.json`: version v1.0 và definitions khớp scope đã chọn; enum, defaults và toàn bộ rules giữ nguyên. Không thêm trường occlusion_percentage trái schema.
4. Chạy `python scripts/make_cvat_labels.py`, kiểm schema và so class/attributes/default/ignore trong JSON; dán vào Project CVAT. Định nghĩa mức che vẫn ở guideline, không đổi tên giá trị select để nhét mô tả.
5. Hai người xác nhận cùng assignment40/người đã kiểm. Bàn giao/chốt bản này trước upload; không dùng generator ghi đè các file đang có. Chưa commit/push trong vòng chuẩn bị này.
6. Mỗi người xác minh quyền tạo Task, số frame và export COCO, sau đó annotation độc lập; đọc [runbook](ANNOTATION_PREPARATION.md). Không lấy nhãn của người kia làm mẫu/pre-label.

### Những file cần cập nhật sau nhóm xác nhận

| File | Cập nhật cần làm / người có thẩm quyền |
|---|---|
| submission/guidelines/guideline_v1.0_agreed.md | Nhóm chốt nội dung và bằng chứng hai người, version/revision, trạng thái khóa |
| submission/taxonomy.json | Người được nhóm giao cập nhật version/definition theo bản khóa; không sửa rules/enum |
| cvat/labels_generated.json | Generator sinh sau taxonomy v1.0; người tạo Project kiểm lại |
| TEAM.md | Nhóm xác nhận vai trò và thông tin nhóm bằng mã; không tự điền kết quả các pha |
| docs/team/GUIDELINE_HARMONIZATION.md | Dẫn bằng chứng cho từng AGREED, giữ lịch sử khác biệt, ghi cách xử lý NEEDS_EVIDENCE |
| docs/team/NEXT_PHASE_CHECKLIST.md | Đổi BLOCKED/NOT STARTED chỉ khi có bằng chứng; kiểm lại mọi điều kiện |
| submission/individual_notes/101.md và docs/member_101/PROGRESS_101.md | 101 ghi quyết định nhóm50%, bất đồng/lý do và việc thật đã làm; dẫn rule chung |
| submission/guidelines/individual/guideline_101.md | Giữ đề xuất ban đầu25%; nếu bổ sung, chỉ ghi chú quyết định nhóm/link, không xóa lịch sử |
| submission/individual_notes/102.md; guideline_102.md | 102 tự bổ sung ca ảnh, cách dùng AI, quyết định thay30/70% bằng quy tắc nhóm; không chỉnh thay102 |
| docs/member_101/FINAL_AUDIT_101.md | Giữ audit thời điểm cũ; có thể bổ sung phụ lục mốc mới, không viết lại như audit đã kiểm bản nhóm |
| K5-L23-Day07-Guideline-Taxonomy-QC.md/.html và guideline v0 | Giữ tài liệu lớp làm nguồn lịch sử; bản nhóm đã ghi rõ chọn bảng50%, không áp dụng ví dụ30/70% của bài giảng như luật song song |
| submission/qc/assignment.csv và assignments/101.txt,102.txt | Đang sẵn local; chỉ bàn giao bản đã xác nhận, không cần thay nội dung nếu vẫn đúng40/người |

## 3. Kiểm tra kỹ thuật thực tế

Kết quả được cập nhật sau khi chạy kiểm tra trong vòng chuẩn bị này. Không dùng log audit trước như kết quả chạy mới. Script kiểm cục bộ ở `work/team_preflight.py`, chỉ đọc nguồn/assignment/config và kiểm Markdown; không sinh nhãn. Thư mục work không nộp.

| Lệnh / phép kiểm đã chạy | Exit code | Kết quả thực tế |
|---|---|---|
| git fetch origin | 0 | origin/main vẫn7cc0971; đọc102 bằng git show, không checkout/merge |
| python work/team_preflight.py | 0 | Schema/load_taxonomy đạt; taxonomy bằng HEAD và vẫnv0; CVAT class/type/default/values/ignore khớp; 40ảnh/người và80/80hash bản sao bằng nguồn; mọi file cũ, kể cả102/work102, giữ nguyên |
| python work/team_inspect.py | 0 | Matrix23 chủ đề:0AGREED/19PENDING_CONFIRMATION/4NEEDS_EVIDENCE; kiểm thêm ví dụ30/70% trong HTML lớp |
| python -m unittest discover -s tests -v | 1 | Chạy20test trong22.471s:19OK,0 assertion failures,1ERROR,0skipped |
| python -m compileall -q scripts tests | 0 | Biên dịch scripts/tests đạt; không thay source |
| python scripts/validate_labels.py --all | 2 | Chưa có fileCOCO nên argparse dừng: “Truyền file COCO hoặc dùng --all.” Không có nhãn nào đã được validator xác nhận |
| git diff --check | 0 | Tracked diff không lỗi whitespace; các tài liệu mới chưa tracked được kiểm bảng/liên kết/whitespace riêng bằng team_preflight |
| git status --short / kiểmHEAD | 0 | Branch101 giữ nguyên; thêm4tài liệu đề xuất; các thay đổi có sẵn vẫn giữ nguyên, không stage/commit/push |

TestERROR là `test_assignment_rejects_unsafe_member_and_symlink_destination`, `tests/test_workflow.py:238`: tạo symlink gặp `OSError: [WinError 1314] A required privilege is not held by the client`. Đây là lỗi quyền Windows; chưa kiểm xong nhánh symlink trên máy này. Giữ nguyên test/kiểm tra bảo mật, không bỏ test, không đổi quyền hệ thống. Git có cảnh báo quyền đọc global ignore, nhưng diff/status và kiểm hash vẫn chạy được.

Kiểm nhất quán bản nhóm: không còn định nghĩa25/30/70% làm luật hiện hành; biên0% thuộc0, đúng50% thuộc2, không xác định thuộc3+review; phần ngoài khung loại khỏi tỷ lệ che. Ví dụ chưa được gán sẵn% thật. Các mốc cũ chỉ còn trong bản cá nhân/tài liệu nguồn và matrix lịch sử đã được chỉ rõ.

Không dùng full-submission checker để suy rằng chỉ thiếu một file khi nó dừng sớm. Schema/config pass không xác nhận nghĩa lớp hoặc việc người thật đã đồng ý. Các unit test dùng fixture tổng hợp trong thư mục tạm, không phải annotation bài nộp.
