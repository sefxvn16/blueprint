# Quy tắc chung (game và web/app)

## Mục lục
1. Bộ file trong dự án
2. Chia thư mục design/ (R1–R9)
3. architecture.md: core và module
3b. Cấu trúc thư mục (S1–S8)
4. features.json
5. ideas.md
6. Chất lượng chung
7. Nguồn

## 1. Bộ file trong dự án

| File | Trả lời câu hỏi | Ai sửa |
|---|---|---|
| `design/README.md` | Làm cái gì, cho ai, phạm vi, Không làm, danh sách màn hình, chỉ mục | skill đề xuất, người dùng duyệt |
| `design/<domain>.md` | Chi tiết từng lĩnh vực | như trên |
| `design/features.json` | Danh sách tính năng, tiêu chí xong, trạng thái | skill tạo; trạng thái `pass` chỉ đổi khi có bằng chứng |
| `design/ideas.md` | Ý tưởng chưa được chọn | skill ghi khi người dùng nêu ý tưởng |
| `architecture.md` (gốc dự án) | Xây bằng cách nào: stack, thư mục, core/module, luồng dữ liệu, quyết định kỹ thuật | skill đề xuất, người dùng duyệt |
| `data/*.json` hoặc file config | Số liệu chỉnh được | code của dự án |

Skill này **không tạo, không sửa** `PLAN.md`, `plan.md`, code, CLAUDE.md hay AGENTS.md. Nếu dự án có CLAUDE.md, skill chỉ được **đề xuất** thêm một dòng trỏ tới `design/README.md` và `architecture.md`; người dùng tự quyết.

## 2. Chia thư mục design/

- **R1. Chỉ mục:** `design/README.md` là spec, kết thúc bằng bảng chỉ mục: mỗi file một dòng gồm đường dẫn · chứa gì · đọc khi nào. README trỏ trực tiếp tới mọi file, kể cả file trong thư mục con.
- **R2. Đơn vị chia là lĩnh vực** (giao diện, gameplay, tiến độ, thế giới, nhân vật, đồ họa…), không phải từng thực thể. Sản phẩm không có lĩnh vực đó thì không tạo file.
- **R3. Ngưỡng dưới:** nội dung dưới khoảng 80 dòng thì gộp thành một mục `##` trong file lĩnh vực gần nhất. README là ngoại lệ.
- **R4. Ngưỡng trên:** file vượt 400 dòng hoặc khoảng 25 KB thì tách theo mục `##` lớn nhất, rồi cập nhật chỉ mục.
- **R5. Danh mục thực thể** (nhân vật, pet, quái, vật phẩm, màn chơi, trang): mỗi loại một file, gồm một bảng tổng (mỗi thực thể một dòng) và mỗi thực thể một mục `###` ngắn. Thực thể nào riêng nó vượt khoảng 150 dòng mới có file `design/<loại>/<tên>.md`. Chỉ lồng tối đa một thư mục con.
- **R6. Số liệu không viết trong văn xuôi:**
  - prototype/alpha: mọi giá trị chỉnh được nằm trong một file config duy nhất;
  - từ vertical slice (game) hoặc beta (web/app): tách thành `data/<domain>.json`, và file thiết kế chỉ ghi quy tắc kèm đường dẫn tới file số liệu.
- **R7. Đầu mỗi file:** tiêu đề · `Trạng thái: Nháp | Duyệt | Đã làm` · `Cập nhật: YYYY-MM-DD` · `Liên quan:` · **Mục lục** (bắt buộc khi file dài hơn 100 dòng). Tiêu đề `##` giữ ổn định.
- **R8. Một chủ đề, một nơi:** quy tắc dùng chung viết một lần ở file chủ; nơi khác chỉ trỏ tới.
- **R9. Rà ở mỗi mốc giai đoạn:** đếm dòng từng file, gộp hoặc tách theo R3–R5.

**Ngôn ngữ:** văn xuôi viết tiếng Việt. Tên file, tiêu đề `##`, ID tính năng và khóa dữ liệu viết tiếng Anh.

## 3. architecture.md: core và module

Bắt buộc có trước khi viết code thật: game là trước **vertical slice**, web/app là trước **beta**. Không cần ở prototype/alpha, vì code giai đoạn đó có thể bị bỏ.

Các mục: Stack và lệnh chạy · Bản đồ thư mục · Core · Module · Luồng dữ liệu · Nơi lưu dữ liệu · Quyết định kỹ thuật.

**Tiêu chí phân loại** (ghi vào file để AI không đẩy mọi thứ vào core):
- **Core** là thứ mà từ hai module trở lên cùng phụ thuộc, hoặc mang trạng thái toàn cục:
  - game: vòng lặp/clock, quản lý màn hình (state machine), input, **settings store**, **save service**, âm thanh, i18n, kênh sự kiện;
  - web/app: xác thực/phiên, phân quyền, truy cập dữ liệu, cấu hình, i18n, xử lý lỗi, thông báo.
- **Module** là một tính năng hoặc một màn hình. Module chỉ phụ thuộc vào core, **không import module khác**; muốn trao đổi thì qua sự kiện hoặc một interface do core cung cấp.
- Màn nào cần đọc/ghi thiết lập thì gọi settings store; màn nào cần lưu thì gọi save service. Không màn nào tự làm settings hay save riêng.
- **UI chỉ hiển thị:** UI không giữ và không trực tiếp sửa trạng thái game hay dữ liệu; muốn đổi gì thì gửi lệnh hoặc sự kiện. Logic không tham chiếu trực tiếp tới UI.
- Mọi chữ hiển thị đi qua hệ thống đa ngôn ngữ (i18n), không viết cứng trong code. Hiệu ứng chuyển động bỏ qua được và tôn trọng thiết lập giảm chuyển động. Mọi màn đã thử ở kích thước nhỏ nhất và lớn nhất được hỗ trợ (CCGS `rules/ui-code.md`).

**Rà lại một lần sau vertical slice:** ranh giới thật chỉ lộ ra khi đã làm. Ghi thay đổi vào mục Quyết định kỹ thuật.

**Quyết định kỹ thuật:** mỗi quyết định ghi Ngày · Bối cảnh · Chọn gì · Bỏ gì và vì sao. Không xóa quyết định cũ; nếu thay thì ghi "thay bằng #n".

## 3b. Cấu trúc thư mục

- **S1. Một nguồn sự thật:** cây thư mục nằm ở `architecture.md` › Folder map, dạng cây kèm một dòng mục đích cho mỗi thư mục. Cây phải được người dùng duyệt **trước dòng code thật đầu tiên**, và AI tạo đúng cây đó trước khi viết code.
- **S2. Framework/engine ép cấu trúc thì theo nó:** dùng bố cục chính thức của framework (Vite, Next.js, Godot, Unity…) và ghi rõ trong Folder map là theo framework nào. Không dựng cây riêng chồng lên. Ví dụ CCGS: Unity chỉ biên dịch code trong `Assets/`, Unreal chỉ build code trong `Source/`, còn Vite build những gì `index.html` import.
- **S3. Prototype tách riêng:** mỗi prototype nằm gọn trong `prototypes/<name>/`, bên trong tự do. Code thật không import từ `prototypes/`, và prototype không import từ code thật.
- **S4. Trong code:**
  - `core/`: dịch vụ có trạng thái, dùng chung (theo §3);
  - `modules/<module-id>/`: mỗi module một thư mục, **mọi file của module nằm trong đó**;
  - `shared/`: component hoặc hàm không giữ trạng thái, được ≥2 module dùng.

  Không tạo thư mục kiểu `utils2/`, `new/`, `misc/`, `temp/`, `old/`.
- **S5. Ngoài code:**
  - `design/`; `data/` (số liệu chỉnh được);
  - `assets/` với `images/`, `audio/`, `fonts/`; mỗi asset bên thứ ba ghi nguồn và license trong `assets/CREDITS.md`;
  - `tests/`; `tools/` (chỉ khi có script);
  - `prototypes/`.
- **S6. Gốc dự án gọn:** ở gốc chỉ có README, `architecture.md`, CLAUDE.md, PLAN.md (nếu có), file cấu hình của công cụ (package.json, vite.config…, `index.html` nếu framework yêu cầu) và các thư mục ở S4/S5. File tạm, file thử, file log và bản sao không để ở gốc, cũng không để trong `src/`.
- **S7. Thêm mới:**
  - thư mục cấp một mới hoặc module mới: cập nhật Folder map trước, sau đó mới tạo;
  - thư mục cấp một mới cần người dùng đồng ý;
  - file mới phải thuộc một thư mục đã có trong Folder map;
  - tên thư mục và file theo một quy ước duy nhất ghi trong architecture.md (mặc định `kebab-case`);
  - code lồng tối đa 3 cấp dưới `src/`, ví dụ `src/modules/<id>/<file>`.
- **S8. Kiểm:** chế độ check liệt kê file và thư mục **không có trong Folder map**, file rác ở gốc, module không có thư mục riêng, và file của một module nằm ở thư mục khác.

**Cây mặc định, game trình duyệt (Vite + TypeScript, không engine):**
```
index.html          vite.config.ts      package.json
architecture.md     README.md
design/             data/               assets/{images,audio,fonts}/
src/main.ts         src/core/{loop,screens,input,settings,save,audio,i18n,events}.ts
src/modules/<id>/   (title, settings, pause, hud, gameplay, …: mỗi màn hoặc tính năng một thư mục)
src/shared/         tests/{unit,integration}/      prototypes/<name>/
```

**Cây mặc định, web/app:** dùng bố cục của framework đã chọn (S2). Không có framework thì dùng `public/` (file tĩnh) · `src/core/` (auth, session, permissions, data-access, config, errors, i18n) · `src/modules/<area>/` · `src/shared/` · `tests/`, cộng thêm `design/`, `data/`, `architecture.md`.

## 4. features.json

Mảng các đối tượng:
```json
{ "id": "shell-settings", "title": "Màn Settings dùng chung", "area": "shell-ui.md",
  "phase": "vertical-slice", "mandatory": true,
  "acceptance": ["mở được từ main menu và pause, cùng một màn", "đổi âm lượng có hiệu lực ngay và còn sau khi tải lại"],
  "status": "todo", "evidence": "" }
```
- `phase`: game dùng `concept | prototype | vertical-slice | alpha | beta | release`; web/app dùng `discovery | alpha | beta | live`. Một sản phẩm chỉ dùng một bộ, ghi ở README › Giai đoạn hiện tại. Game có tài khoản dùng bộ của game; các mục lấy từ `webapp.md` §3 đổi phase: `beta` → `alpha`, `live` → `release`.
- `status`: `todo | doing | pass | dropped`.
- **`pass` chỉ khi có bằng chứng** trong `evidence`: lệnh test và kết quả, đường dẫn ảnh chụp, hoặc "người dùng đã chơi/dùng thử và xác nhận ngày …". Thay đổi giao diện phải có ảnh chụp hoặc người dùng xác nhận đã nhìn thấy.
- **Bằng chứng có thể cũ hơn code.** Lúc chụp ảnh, ghi kèm mã băm của các file đã đổi. Lần rà sau, so lại: file đã đổi, đã mất, hoặc không có mã băm thì ảnh có thể lỗi thời — ghi điều đó vào báo cáo, không im lặng dùng lại ảnh cũ (CCGS `dev-story`, `test-evidence-review`).
- **Không điền hộ.** Kết quả mà chỉ người dùng mới biết (đã chơi thử, thấy màn nào, cảm giác thế nào) thì để trống chờ họ trả lời, không suy ra từ code. Người dùng nói "có" cho một mục giao diện mà không còn ảnh trên đĩa thì đó là lời khẳng định, không phải bằng chứng.
- **Thứ tự chấm:** lỗi đã biết xét trước (còn Blocker/Critical thì không mục nào `pass`), rồi mới xét bằng chứng từng mục. Mục chưa kiểm được xếp **trên** `pass` và **dưới** lỗi: không có đầu vào thì kết quả là "chưa rõ", không bao giờ mặc định thành đạt (CCGS `team-qa`, `perf-profile`).
- Không xóa mục. Bỏ thì đặt `dropped` và ghi lý do vào `evidence`. Bỏ một mục `mandatory: true` cần người dùng đồng ý và phải ghi vào mục Không làm của README.
- Acceptance viết theo dạng "xong khi…", đo được.

## 5. ideas.md

- Ý tưởng mới chỉ ghi vào đây; không code, không sửa features.json.
- Mỗi dòng gồm: ngày · ý tưởng · vấn đề nó giải quyết · công sức ước lượng (nhỏ / vừa / lớn).
- Ở mốc giai đoạn (chế độ check), skill liệt kê các ý tưởng để người dùng chọn. Ý tưởng được chọn thành feature có acceptance; ý tưởng không chọn thì giữ nguyên, không phải dọn.
- Ngoại lệ: lỗi làm hỏng một feature đang `pass` không phải ý tưởng. Đó là bug, đưa vào features của chính mục đó (đặt lại `doing`).

## 6. Chất lượng chung

- **Keep (giữ nguyên):** README có mục Keep, gồm những điều người dùng thích và không được làm hỏng. Trước khi đề xuất thay đổi hay cắt bỏ, đối chiếu với Keep và Không làm; đụng tới mục nào thì nói rõ và hỏi.
- **Cắt phạm vi trước phát hành** (ở beta, theo CCGS `cut`), đề xuất cắt theo thứ tự:
  1. mục chưa làm mà Không làm đã loại;
  2. mục đã làm nhưng kiểm không đạt: hỏi cắt hay polish;
  3. mục chưa làm mà không gắn với vision, core loop hay mục tiêu.

  **Không bao giờ đề xuất cắt mục trong Keep.** Danh sách polish chỉ lấy từ bằng chứng (kiểm không đạt, smoke test lỗi, người dùng nêu), không tự nghĩ ra. Sản phẩm để bán thì chốt ngày phát hành và ngày đóng băng tính năng (mặc định ở mốc 70% quãng thời gian từ hôm nay tới ngày phát hành); sau ngày đóng băng chỉ sửa lỗi và polish.
- **Definition of Done của dự án** (ghi trong README): một feature chỉ `pass` khi đạt acceptance, không làm hỏng smoke test, và có bằng chứng.
- **Smoke test** sau mỗi feature:
  - game: mở → menu → New Game → vào màn → chơi 10 giây → save → load → so trạng thái;
  - web: mở trang chủ → đăng nhập → thao tác chính → đăng xuất.
- **Thang bug:** Blocker (không mở được hoặc không vào được luồng chính) · Critical (hỏng save, thanh toán, cơ chế chính) · Major (hỏng nhưng có cách vượt) · Minor · Trivial. Mức nghiêm trọng (severity) tách riêng với độ gấp (priority).
- **Thử với người thật:** khoảng 5 người, quan sát và không nhắc, hỏi sau khi xong. Chỉ hỏi "cái gì gây bối rối?"; từ 3 người trở lên cùng vướng một chỗ thì luật chỗ đó hỏng, không phải người chơi dở. Giao thức đầy đủ, và cách tự chơi thử khi làm một mình: skill `game-feel`, `references/playtest.md` §6–§7.
- **Accessibility:** chốt tier trước khi viết code thật; chưa chốt là không đạt, "Basic" cũng được tính là đã chốt. Game:
  - Basic: chữ đọc được, không dùng màu làm dấu hiệu duy nhất, âm lượng riêng từng loại;
  - Standard: Basic + đổi phím, cỡ chữ, phụ đề, chế độ mù màu, thời gian chỉnh được.

## 7. Nguồn
Anthropic *Skill authoring best practices* (tổ chức theo lĩnh vực, mục lục cho file >100 dòng, tham chiếu 1 cấp) · Anthropic *Effective harnesses for long-running agents* (feature list, pass có kiểm chứng, không xóa test) · Claude-Code-Game-Studios v1.3.0 (`directory-structure.md`: cây chuẩn, code root theo engine, prototypes tách riêng; `systems-index.md`, `gate-*.md`, hook read-guard 40 KB, config từ dòng đầu, tier accessibility) · Shape Up ch.3/6/7/12 (appetite, no-gos, không backlog chung, scope theo cấu trúc) · Scrum Guide 2020 (Definition of Done) · GOV.UK *Writing user stories* (acceptance "it's done when") · Tim Ryan *Anatomy of a Design Document* · ISTQB (severity/priority) · Bugnet (smoke test) · NN/g (5 người dùng).
