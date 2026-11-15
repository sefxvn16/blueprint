# Game: giai đoạn, màn hình bắt buộc, save, phát hành

## Mục lục
1. Câu hỏi đầu dự án
2. Giai đoạn và cổng
3. Màn hình theo điều kiện
4. Quy tắc từng màn
5. Quyết định về save
6. Game chạy trên trình duyệt
7. File lĩnh vực mặc định
8. Checklist phát hành
9. Nguồn

## 1. Câu hỏi đầu dự án (hỏi gộp một lượt, câu nào cũng có mặc định)

| Câu hỏi | Mặc định nếu người dùng nói "bạn chọn" | Ảnh hưởng tới |
|---|---|---|
| Ý tưởng, thể loại, cảm giác muốn có | (bắt buộc người dùng nói) | README |
| Nền tảng: trình duyệt / PC / mobile; điều khiển bằng gì | trình duyệt, bàn phím + chuột | Settings › Điều khiển; Quit; §6 |
| (Nếu là trình duyệt) Phát hành ở đâu: mở file trực tiếp / host riêng / nhúng (itch.io, iframe); có hỗ trợ điện thoại không | host riêng, chỉ máy tính | §6 |
| Chơi thời gian thực hay theo lượt | thời gian thực | Pause |
| Thua là hết, thua mềm, hay không có thua | thua là hết | Game over |
| Có kết thúc không | có | Results, Credits |
| Tiến độ có giữ giữa các lần chơi không; lưu ở máy hay server | có, lưu trên máy | Save, Continue/Load, tài khoản |
| Có tài khoản không; chơi nhiều người ở mức nào (bảng dưới) | không; một người | mức nào cần server thì dùng thêm `webapp.md` §3 |
| Thể loại có những lựa chọn định hình nào; tính năng nào của thể loại để sau | AI liệt kê 3–5 lựa chọn của thể loại (đánh dấu là giả thuyết), người dùng chọn | README › Scope; mục "để sau" ghi sẵn vào `ideas.md` |
| Điều gì phải giữ nguyên dù sau này đổi gì (cảm giác, nhân vật, luật chơi cốt lõi) | để trống, điền sau khi chơi thử | README › Keep |

**Mức chơi nhiều người** (CCGS `online-and-devices.md`): cùng một màn hình (không cần mạng) · async (bảng xếp hạng, thử thách hằng ngày, lượt chơi qua nhiều ngày) · session (trận với bạn bè trên máy riêng) · dedicated server (đấu xếp hạng với người lạ) · persistent world (thế giới chung kiểu MMO). Từ mức async trở lên đều cần server. Bản đầu có thể dùng thay thế (bảng điểm trên máy, bot ghi rõ là bot), nhưng bản thay thế không chứng minh được phần online chạy đúng.
| Có cốt truyện / nhân vật / pet / chiến đấu / nhiều màn chơi không | theo ý tưởng | file lĩnh vực (§7) |
| Có âm thanh, có lời thoại không | có âm thanh, không thoại | Âm thanh, phụ đề |
| Ngôn ngữ giao diện | tiếng Việt | Settings › Ngôn ngữ |
| Tier accessibility | Basic | Settings › Accessibility |

## 2. Giai đoạn và cổng

| Giai đoạn | Tài liệu phải có | Xong khi (đo được) |
|---|---|---|
| concept | `design/README.md` mức one-pager (ý tưởng, core loop, cảm giác, phạm vi, **Không làm**) | người dùng duyệt README |
| prototype | như trên + `features.json` | core loop chơi được (có thể chỉ dùng hình khối); người dùng chơi và chọn **Tiếp / Đổi hướng / Bỏ**. Đổi hướng 3 lần trên cùng một ý tưởng thì phải hỏi thẳng có nên bỏ không |
| vertical-slice | đủ file lĩnh vực, `architecture.md` có Folder map đã duyệt và cây đã được tạo (`common.md` §3b), tier accessibility đã chốt | mọi feature `mandatory` của giai đoạn này là `pass`, gồm đủ các màn bắt buộc ở §3 + 1 màn chơi hoàn chỉnh + save/load chạy được; người mới chơi hiểu cần làm gì trong 2 phút đầu mà không cần ai giải thích |
| alpha | `architecture.md` đã rà lại | mọi feature `pass` hoặc `dropped`; mọi màn đã làm đều có trong `screen list` của README (không có màn "chỉ có trong code") |
| beta | danh sách cắt và polish (`common.md` §6) | chơi được từ đầu đến cuối; ≥3 buổi chơi thử có ghi chép (người mới, giữa game, độ khó); không còn bug Blocker/Critical; không có chỗ nào quá nửa số người chơi bị kẹt mà không biết vì sao |
| release | | checklist §8 đạt |

Prototype được phép thiếu menu và settings. Code prototype có thể bỏ đi; bước sang vertical slice thì viết lại theo `architecture.md`.

## 3. Màn hình theo điều kiện

Đưa vào `features.json` ngay từ concept với `phase: vertical-slice` (trừ ghi chú khác) và `mandatory: true` khi điều kiện đúng.

| id | Màn | Bắt buộc khi |
|---|---|---|
| `shell-first-launch` | Lần chạy đầu: ngôn ngữ, âm lượng, cỡ chữ, phụ đề | game có chữ hoặc âm thanh |
| `shell-title` | Title / Main menu | luôn luôn |
| `shell-settings` | Settings dùng chung | luôn luôn |
| `shell-pause` | Pause | chơi thời gian thực |
| `shell-hud` | HUD | có gameplay trên màn hình |
| `save-new-continue` | New Game / Continue / Load | tiến độ được giữ giữa các lần chơi |
| `shell-tutorial` | Hướng dẫn chơi | có cơ chế cần học (`phase: alpha`) |
| `shell-gameover` | Game over / Restart | thua là hết |
| `shell-restart` | Restart / Reset (không có game over) | thua mềm hoặc không có thua |
| `shell-results` | Results / Victory | game có kết thúc |
| `shell-credits` | Credits | luôn luôn (`phase: release`) |
| `shell-quit` | Quit có xác nhận | PC/desktop (trên trình duyệt không cần) |
| `shell-mute` | Tắt tiếng nhanh | có âm thanh |
| `web-tab-pause` | Tự pause khi chuyển tab / thu nhỏ | trình duyệt + chơi thời gian thực (xem §6) |
| `web-save-export` | Xuất / nhập file save | trình duyệt + chỉ lưu trên máy (`phase: alpha`, xem §6) |

## 4. Quy tắc từng màn

- **Lần chạy đầu:** hiện trước main menu và trước cutscene. Lần sau dùng giá trị đã lưu. Mục ngôn ngữ ghi tên ngôn ngữ bằng chính ngôn ngữ đó ("Tiếng Việt", "English").
- **Title / Main menu:**
  - tên game, **một** hành động chính, 4–6 mục, số phiên bản đặt kín đáo;
  - chưa có save: nút chính là New Game, **ẩn hẳn Continue** (không chỉ làm mờ);
  - đã có save: Continue đứng đầu và ghi rõ tiếp tục từ đâu (chương/màn, thời gian chơi);
  - không đặt modal tin tức chắn trước nút Play; mở ra là có mục được chọn sẵn.
- **Settings:**
  - **một màn duy nhất**, mở được từ main menu và từ pause, nội dung giống nhau ở cả hai nơi;
  - nhóm Gameplay (độ khó) · Hiển thị (độ phân giải/fullscreen, rung màn hình bật/tắt) · Âm thanh (nhạc, hiệu ứng, môi trường, lời thoại, UI chỉnh riêng) · Điều khiển (đổi phím, đảo trục) · Accessibility (cỡ chữ đến 200%, tương phản cao, phụ đề) · Ngôn ngữ;
  - thay đổi có hiệu lực ngay và được lưu; thoát khi chưa lưu thì hỏi lại.
- **Pause:** Resume là hành động chính; có Settings, Restart, Quit to Title. Quit to Title có xác nhận và mặc định chọn phương án an toàn. Pause được cả trong cutscene.
- **HUD:** chỉ hiện thông tin cần cho lúc đang chơi. **Không đặt nút hay thanh trượt cài đặt trên màn chơi**; chỉ có một nút hoặc phím mở Pause. Chữ trên HUD đọc được trên nền sáng nhất của game.
- **Tutorial:** dạy bằng cách cho làm thử; xem lại được bất cứ lúc nào mà không mất tiến độ. Một màn hình tĩnh liệt kê phím không được tính là tutorial.
- **Game over / Results:** có Retry, Continue (nếu có save) và Quit to Title. Results cho thấy người chơi đã đạt được gì.
- **Luồng màn hình:** một state machine có bảng chuyển trạng thái viết rõ trong `shell-ui.md` (trạng thái · sự kiện · sang trạng thái nào), ví dụ `title --New Game--> play --Esc--> pause --Settings--> settings --Back--> pause`. Mọi màn mới phải có dòng trong bảng (CCGS `rules/gameplay-code.md`: state machine có bảng chuyển trạng thái tường minh).
- **Điều hướng:** Back/Esc ở màn con thì về màn cha; Esc trong lúc chơi mở Pause, không thoát game. Dùng được hoàn toàn bằng bàn phím (và tay cầm nếu hỗ trợ).

## 5. Quyết định về save (ghi vào `architecture.md` › Nơi lưu dữ liệu trước khi viết code save)

1. **Lưu ở đâu:** trên máy (localStorage/IndexedDB với game web) / server (cần tài khoản → `webapp.md` §3) / cả hai (ghi rõ bên nào thắng khi xung đột).
2. **Mô hình:**
   - có cả autosave lẫn save thủ công; chỉ có checkpoint là chưa đủ;
   - autosave ở slot riêng, **không bao giờ ghi đè save thủ công**, và ngược lại;
   - tải lại được ít nhất 3 trạng thái trước;
   - ghi đè save thủ công thì cảnh báo là không hoàn tác được.
3. **Kỹ thuật:**
   - dữ liệu save có số phiên bản và có cách nâng cấp từ bản cũ;
   - ghi ra bản tạm, xong mới thay bản chính;
   - mỗi slot lưu kèm ngày giờ, thời gian chơi và vị trí;
   - không chỉ lưu lúc thoát (game có thể sập trước đó);
   - không autosave lúc khởi động khi chưa nạp dữ liệu thật;
   - save hỏng thì báo lỗi và cho chọn bản khác, game không được sập;
   - settings lưu tách khỏi save tiến độ.
4. **Kiểm:** smoke test có bước save → tải lại trang → Continue → trạng thái khớp.

## 6. Game chạy trên trình duyệt

- **Âm thanh bị chặn cho tới lần tương tác đầu:** trình duyệt chặn phát âm thanh do script khởi động trên tab chưa có cú bấm, chạm hay nhấn phím nào. Vì vậy:
  - màn Title có nút "Bấm để bắt đầu", và cú bấm đó dùng để bật âm thanh (Web Audio / `play()`);
  - âm thanh không bật được thì game vẫn chạy và hiện biểu tượng tắt tiếng, không báo lỗi.
- **Chuyển tab hoặc thu nhỏ cửa sổ:** tab ở nền gần như không nhận `requestAnimationFrame`, còn bộ đếm thời gian bị bóp chậm. Do đó:
  - nghe sự kiện `visibilitychange`: khi trang bị ẩn thì tự mở Pause và tắt âm; quay lại thì **dừng ở Pause chờ người chơi bấm Resume**, không tự chạy tiếp;
  - logic game chạy theo bước cố định (fixed step), không tính theo đồng hồ thật, để không "nhảy cóc" sau khi tab bị ẩn.
- **Lưu trên máy không chắc chắn:**
  - dữ liệu lưu riêng theo origin (domain + cổng), nên đổi nơi host (localhost, itch.io, domain riêng) là mất save cũ;
  - localStorage khoảng 5 MiB mỗi origin; vượt thì trình duyệt ném lỗi `QuotaExceededError`, phải bắt lỗi và báo người chơi;
  - dữ liệu mặc định ở chế độ "best-effort", trình duyệt có thể xóa. Safari xóa dữ liệu do script tạo nếu trang không có tương tác nào trong 7 ngày;
  - cách giảm rủi ro: gọi `navigator.storage.persist()`; có nút **Xuất / Nhập save** ra file; save quan trọng hoặc chơi lâu dài thì lưu trên server.
- **Nhúng trong iframe (itch.io…):** iframe cần `allow="autoplay"` để phát âm thanh (MDN). Có nút toàn màn hình; fullscreen chỉ bật được khi người chơi bấm (thực hành phổ biến, chưa đối chiếu nguồn chính thức).
- **Bàn phím** (thực hành phổ biến, chưa có nguồn chính thức): phím mũi tên và Space không được làm cuộn trang khi đang chơi; game phải có focus thì mới nhận phím (bấm vào khung game, hoặc Title nhắc người chơi bấm).
- **Kích thước:** khung game co giãn theo cửa sổ và giữ đúng tỉ lệ; thử ở ít nhất 2 kích thước cửa sổ. Hỗ trợ điện thoại thì cần thêm điều khiển cảm ứng và thử cả xoay ngang lẫn dọc.

## 7. File lĩnh vực mặc định (áp R2–R5 ở `common.md`)

| File | Chứa | Tạo khi |
|---|---|---|
| `shell-ui.md` | lần chạy đầu, menu, settings, pause, HUD, tutorial, accessibility, ngôn ngữ | luôn luôn |
| `gameplay.md` | core loop, điều khiển, quy tắc, camera, độ khó | luôn luôn |
| `progression-save.md` | cấp độ, mở khóa, tiền tệ, cửa hàng, save/load | có tiến độ hoặc kinh tế |
| `world-levels.md` | bản đồ, vùng; bảng danh sách màn chơi + mỗi màn một mục | có nhiều màn hoặc bản đồ |
| `art-audio.md` | phong cách đồ họa, bảng màu, phong cách UI, hoạt ảnh, âm thanh, nhạc | luôn luôn |
| `combat.md` | chiến đấu, kỹ năng, kẻ địch theo vai trò | có chiến đấu |
| `characters.md` | nhân vật, pet, NPC, quái: bảng tổng + mỗi thực thể một mục | có từ 3 nhân vật trở lên |
| `story.md` | cốt truyện, thoại, lore | có cốt truyện |

Lĩnh vực nhỏ (dưới khoảng 80 dòng) thì gộp vào file gần nhất, ví dụ `combat` gộp vào `gameplay.md`.

## 8. Checklist phát hành

- [ ] Chơi được từ đầu đến cuối; save/load đúng ở mọi trạng thái; tutorial đã thử với người mới
- [ ] Edge case: hết dung lượng lưu, mất mạng (nếu cần mạng), chuyển tab rồi quay lại, đổi kích thước cửa sổ
- [ ] Game trình duyệt: đã thử trên Chrome, Firefox và Safari (hoặc ghi rõ trình duyệt nào chưa thử); đã thử ở đúng nơi sẽ host (origin thật); âm thanh bật sau cú bấm đầu
- [ ] Accessibility đạt tier đã chốt; ít nhất có đổi phím, cỡ chữ, không dùng màu làm dấu hiệu duy nhất
- [ ] Mọi chữ hiển thị nằm trong file ngôn ngữ, không viết cứng trong code
- [ ] Không còn giá trị debug/test, phím gian lận, log thừa
- [ ] Credits đủ; có ghi nguồn cho asset bên thứ ba; privacy policy nếu có thu dữ liệu
- [ ] Không còn bug Blocker/Critical; smoke test đạt trên bản phát hành
- [ ] Số phiên bản trong menu khớp với bản phát hành
- [ ] Phát hành trên itch.io: dung lượng bản build trong giới hạn upload; trang có ảnh bìa, ảnh chụp, mô tả, tag; tag độ tuổi và nội dung khai trung thực; đã quyết bản chơi trên trình duyệt hay bản tải về và đã thử bản đó (CCGS `certification-itch.md`)

## 9. Nguồn
MDN *Page Visibility API* (visibilitychange, rAF và timer ở tab nền) · MDN *Autoplay guide for media and Web Audio APIs* · MDN *Storage quotas and eviction criteria* (5 MiB, QuotaExceededError, best-effort, `persist()`, Safari 7 ngày) ·
Microsoft *Xbox Accessibility Feature Tags* (accessibility on launch, settings trước khi chơi, progress saving options, pausable, on-demand tutorials, custom volume, text size); XAG 112/114 · h-idris *Main menu design* (menu tối thiểu, settings dùng chung, luồng lần đầu / người quay lại) · Steve Bromley *How to save games* · Claude-Code-Game-Studios v1.3.0 (`one-shot-2-build.md` màn theo điều kiện, `gate-production.md` 2 phút đầu, `gate-polish.md` confusion loop và màn chỉ có trong code, `launch-checklist.md`, `prototype/SKILL.md` 3 lần đổi hướng) · Rami Ismail *Milestones* · Game Developer *settings checklist* · Celia Hodent *The Gamer's Brain* (tách HUD khỏi menu, chưa đọc sách) · Game Accessibility Guidelines.
