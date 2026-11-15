---
name: blueprint
description: Lập và rà bản thiết kế sản phẩm cho game hoặc web/app trước và trong khi vibe code. Bản thiết kế gồm design/README.md (spec), các file lĩnh vực, features.json, ideas.md và architecture.md. Skill đảm bảo đủ màn hình, luồng và thiết lập cơ bản (title, menu, settings, pause, save/continue, tài khoản, profile, admin, trang lỗi) cùng giai đoạn, cổng và cấu trúc thư mục. Dùng khi người dùng bắt đầu một game hoặc web/app mới, hỏi game/app còn thiếu màn hay luồng gì, muốn kiểm đã đủ điều kiện sang giai đoạn sau, hoặc nêu một ý tưởng tính năng mới giữa chừng. Không dùng để viết hay sửa code, thiết kế bố cục/thẩm mỹ giao diện, hay quản lý PLAN.md.
---

# Blueprint

Skill này quyết định **làm cái gì** và **khi nào là xong**. Skill không viết code và không quyết định bố cục thẩm mỹ.

Các file tham chiếu (đọc file nào khi cần, đọc trọn file đó):
- [references/common.md](references/common.md): bộ file trong dự án, quy tắc chia `design/`, core/module, `features.json`, `ideas.md`, chất lượng chung.
- [references/game.md](references/game.md): câu hỏi đầu dự án, giai đoạn và cổng, màn hình theo điều kiện, save, phát hành (game).
- [references/webapp.md](references/webapp.md): câu hỏi đầu dự án, pha và cổng, màn hình theo vai trò, tài khoản, trạng thái, phát hành (web/app).
- `templates/`: [design-readme-game.md](templates/design-readme-game.md), [design-readme-webapp.md](templates/design-readme-webapp.md), [domain-file.md](templates/domain-file.md), [architecture.md](templates/architecture.md), [features.json](templates/features.json), [ideas.md](templates/ideas.md), [check-report.md](templates/check-report.md).

Luôn đọc `common.md`. Đọc `game.md` cho game và `webapp.md` cho web/app; game có tài khoản, bảng xếp hạng hay nhiều người chơi thì đọc cả hai.

## Quy tắc cứng

1. **Không viết, không sửa code.** Khi bản thiết kế đã sẵn sàng, nói feature nào nên làm trước rồi dừng.
2. **Không ghi file trước khi người dùng duyệt:** trình bày bản nháp (danh sách file và nội dung chính), chờ đồng ý rồi mới ghi. Ngoại lệ: chế độ idea và báo cáo check được ghi ngay.
3. **Không tạo, không sửa** `PLAN.md`, `plan.md`, CLAUDE.md, AGENTS.md hay cấu hình công cụ. Chỉ được đề xuất một dòng trỏ tới `design/README.md` cho CLAUDE.md của dự án.
4. **Màn hoặc luồng bắt buộc** (bảng ở `game.md` §3, `webapp.md` §3) luôn được đưa vào `features.json` khi điều kiện của nó đúng. Bỏ một mục thì phải hỏi người dùng, được đồng ý mới ghi vào mục Không làm / No-gos của README và đặt `dropped`.
5. **`pass` cần bằng chứng** theo `common.md` §4. Không tự đánh `pass` vì "code có vẻ đã có". Ở chế độ check, ghi "có" cũng cần đã đọc điều kiện hiển thị hoặc đã chạy app (chế độ check, bước 2).
6. File có sẵn của người dùng: sửa phần nào thì đọc trọn phần đó trước; không ghi đè cả file khi chỉ cần sửa một mục.
7. **Không đọc được file tham chiếu hoặc template thì dừng:** báo người dùng lỗi gì, và rằng cần cấp quyền đọc thư mục của skill. Không tự dựng danh mục, tên giai đoạn hay cấu trúc file theo trí nhớ.

## Chọn chế độ

| Tình huống | Chế độ |
|---|---|
| Bắt đầu sản phẩm mới, hoặc dự án chưa có `design/README.md` mà người dùng muốn lập | **new** |
| Hỏi còn thiếu gì, muốn sang giai đoạn sau, mở lại dự án đang làm dở, hoặc dự án có code nhưng chưa có `design/` | **check** |
| Nêu một ý tưởng hay tính năng **chưa có** trong `features.json`, khi đã có `design/README.md` | **idea** |

Yêu cầu làm một feature **đã có** trong `features.json` không phải ý tưởng mới: skill không can thiệp, để việc code diễn ra như bình thường.

Không rõ thì hỏi một câu để chọn chế độ.

## Chế độ new

1. Xác định loại sản phẩm (game / web/app / game có tài khoản).
2. **Hỏi gộp một lượt** các câu ở `game.md` §1 hoặc `webapp.md` §1, câu nào cũng kèm mặc định. Người dùng nói "bạn chọn" thì dùng mặc định và ghi rõ là mặc định. Câu bắt buộc người dùng tự trả lời (ý tưởng, hoặc vấn đề của người dùng) mà chưa có thì hỏi lại, không tự bịa.
3. Lập bản nháp theo giai đoạn đầu:
   - `design/README.md` từ template tương ứng, có mục Không làm / No-gos;
   - `design/features.json`: mọi mục bắt buộc thỏa điều kiện, cộng với các tính năng lõi của ý tưởng; mỗi mục có acceptance đo được;
   - `design/ideas.md`: ghi sẵn các tính năng "để sau" của thể loại (`game.md` §1), để chúng không bị chen vào bản đầu.

   Chưa tạo file lĩnh vực và `architecture.md` ở giai đoạn đầu, trừ khi người dùng yêu cầu.
4. Trình bày bản nháp ngắn gọn gồm: tóm tắt README, danh sách màn, số feature theo giai đoạn, các mặc định đã dùng. Hỏi duyệt.
5. Được duyệt thì ghi file, rồi nói việc tiếp theo, thường là làm prototype core loop (game) hoặc phác luồng chính (web/app). Prototype đặt gọn trong `prototypes/<name>/` (`common.md` S3).

## Chế độ check

1. Đọc `design/README.md` (nếu có), `features.json`, `architecture.md`, và danh sách file trong `design/`. Xác định giai đoạn hiện tại và giai đoạn tiếp theo.
2. Dò code để tìm bằng chứng cho từng mục bắt buộc thỏa điều kiện: tìm theo tên màn, route, chuỗi hiển thị, chỗ lưu dữ liệu (localStorage, IndexedDB, API). Mỗi mục ghi **có** (file:dòng), **thiếu**, hoặc **chưa rõ**. Không đọc được thì ghi chưa rõ, không đoán.
   - **Thấy tên component, route hay hàm chưa đủ để ghi "có".** Mở component đó, đọc điều kiện hiển thị (`return null`, `if (!x)`, cờ cấu hình, biến môi trường, quyền, trạng thái đăng nhập/khách) và ghi rõ trong trường hợp nào màn **không** hiện. Phụ thuộc cấu hình thì ghi "có, chỉ khi <điều kiện>" và kiểm điều kiện đó ở môi trường thật; chưa kiểm được thì ghi chưa rõ.
   - **Cài đặt và thiết lập:** với mỗi giá trị lưu được, tìm chỗ **đọc** để áp dụng. Lưu mà không ai đọc là thiếu.
   - **Chạy app khi có thể** (lệnh chạy trong `architecture.md`, `package.json` hoặc skill chạy app): đi luồng của từng vai trò từ đầu, gồm khách mới tinh (không cookie), người dùng đăng nhập, quản trị, và ghi màn nào thấy hay không thấy. Không chạy được thì ghi lý do ở mục Not checked; khi đó mục giao diện chỉ dựa trên đọc code phải có nhãn "chưa chạy".
   - Đối chiếu với thiết kế đã duyệt của dự án (spec, file lĩnh vực): luồng thiết kế mô tả mà code không có cũng là thiếu.
3. Chấm cổng sang giai đoạn tiếp theo theo bảng ở `game.md` §2 hoặc `webapp.md` §2. Chỉ những mục có `phase` thuộc giai đoạn hiện tại hoặc giai đoạn tiếp theo mới tính vào cổng; mục của giai đoạn xa hơn thì ghi "chưa tới". Tiêu chí cần người thật (chơi thử, người dùng thử) thì hỏi người dùng; chưa có câu trả lời thì ghi CHƯA ĐẠT.
4. Kiểm file trong `design/`: số dòng, kích thước, mục lục, đầu file theo `common.md` R3–R7. Kiểm cấu trúc thư mục theo `common.md` S8: file và thư mục không có trong Folder map, file rác ở gốc, file của module nằm sai chỗ. Chưa có Folder map mà đã có code thật thì ghi là thiếu.
5. Liệt kê ý tưởng đang chờ trong `ideas.md` nếu sắp qua mốc giai đoạn.
6. Ghi báo cáo `design/check-YYYY-MM-DD.md` theo template, rồi tóm tắt trong chat: số mục thiếu, cổng đạt hay chưa, 3 việc nên làm trước.
7. Dự án chưa có `design/`: báo cáo vẫn dựa trên danh mục; cuối báo cáo đề xuất chạy new, lấy câu trả lời từ code và hỏi người dùng phần còn thiếu.
8. Người dùng đồng ý sang giai đoạn sau thì cập nhật README › Giai đoạn hiện tại, và lập các file mà giai đoạn mới yêu cầu (file lĩnh vực, `architecture.md`) theo quy tắc 2. Khi lập `architecture.md`, đề xuất Folder map theo `common.md` §3b. Được duyệt thì **tạo sẵn cây thư mục rỗng** (thư mục cấp một và một thư mục cho mỗi module). Tạo thư mục không phải viết code nên không vi phạm quy tắc 1.

## Chế độ idea

1. Ghi một dòng vào `design/ideas.md` theo template: ngày · ý tưởng · vấn đề nó giải quyết · công sức ước lượng.
2. **Không code, không sửa `features.json`.** Nói lại một câu: đã ghi ý tưởng, sẽ đưa ra chọn ở mốc giai đoạn tiếp theo.
3. Ngoại lệ:
   - Ý tưởng thực chất là lỗi của một feature đã có: báo đây là bug, đề xuất đặt lại feature đó về `doing`.
   - Người dùng nói rõ muốn làm ngay: nêu nó chen vào giai đoạn nào và làm chậm mục nào, rồi để người dùng quyết. Đồng ý thì thêm vào `features.json` kèm acceptance.

## Kết thúc mỗi lần dùng

Nói ngắn: đã ghi file gì, giai đoạn hiện tại, cổng còn thiếu gì, và **một** việc tiếp theo.
