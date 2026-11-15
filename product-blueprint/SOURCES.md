# Nguồn tham khảo của product-blueprint

> File dành cho người đọc. Skill `blueprint` không tham chiếu file này nên AI không nạp nó khi chạy.
> Cột "Mức đọc": **đọc** = đã mở và đọc trang hoặc file gốc; **tóm** = chỉ qua kết quả tìm kiếm hoặc bản tóm tắt; **chưa đọc** = mới biết tên.
> Ngày tra cứu: 2026-11-16.

## 1. Mã nguồn tham khảo (giấy phép)

**Claude-Code-Game-Studios** (Donchitos), bản 1.3.0, commit `abc0de7` (2026-11-09). https://github.com/Donchitos/Claude-Code-Game-Studios
Giấy phép MIT, "Copyright (c) 2026 Donchitos". product-blueprint **không chép mã hay văn bản** của repo này; chỉ học ý tưởng và diễn đạt lại.

| Ý học được | File trong repo | Dùng ở | Mức đọc |
|---|---|---|---|
| 7 giai đoạn, bước khai báo file đầu ra | `.claude/docs/workflow-catalog.yaml` | game.md §2 | đọc |
| Checklist cổng giai đoạn | `.claude/skills/gate-check/references/gate-*.md` | game.md §2 | đọc (dòng checklist) |
| Màn hình quyết theo điều kiện từ brief | `.claude/skills/prototype/references/one-shot-2-build.md` | game.md §3 | đọc |
| Mỗi lần làm một tính năng, Keep/Undo | `.../one-shot-5-grow.md` mục 9 | common.md §4 | đọc |
| 3 lần đổi hướng thì cân nhắc bỏ | `.claude/skills/prototype/SKILL.md` | game.md §2 | đọc |
| Cây thư mục, code root theo engine | `.claude/docs/directory-structure.md` | common.md §3b | đọc |
| Phân loại hệ thống (Core, Persistence…) | `.claude/docs/templates/systems-index.md` | common.md §3 | đọc |
| Tier accessibility | `.claude/docs/templates/accessibility-requirements.md` | common.md §6 | đọc một phần |
| Launch checklist | `.claude/docs/templates/launch-checklist.md` | game.md §8 | đọc |
| Hook chặn đọc file >40 KB | `.claude/hooks/validate-read.sh` | common.md R4 | đọc phần đầu |
| Mức chơi trực tuyến | `.claude/genres/online-and-devices.md` | game.md §1 | đọc |
| Lựa chọn thể loại, mục "để sau" | `.claude/genres/chipsets/pet-raising.md`, `chipsets.yaml` | game.md §1 | đọc |
| UI chỉ hiển thị; giá trị lấy từ config; state machine | `.claude/rules/ui-code.md`, `gameplay-code.md` | common.md §3, game.md §4 | đọc |
| Cắt phạm vi, ngày đóng băng tính năng | `.claude/skills/cut/SKILL.md` | common.md §6 | đọc một phần |
| Checklist itch.io | `.claude/docs/templates/certification-itch.md` | game.md §8 | đọc |
| Tự đo: brief 1 trang tốt hơn 30 tài liệu | `README.md` | thiết kế chung | đọc (số liệu tác giả tự báo cáo) |

## 2. Tài liệu chính thức của các hãng và tổ chức

| Nguồn | URL | Dùng ở | Mức đọc |
|---|---|---|---|
| Microsoft: Accessibility Feature Tags (Xbox) | https://learn.microsoft.com/en-us/gaming/game-publishing/concepts/metadata-accessibility | game.md §3–5 | đọc |
| Microsoft: Xbox Accessibility Guidelines 112, 114, 104, 116 | https://learn.microsoft.com/en-us/xbox/accessibility/xbox-accessibility-guidelines/112 | game.md §4 | tóm |
| Microsoft: Xbox Certification Requirements | https://learn.microsoft.com/en-us/gaming/gdk/_content/gc/policies/console/console-certification-requirements-and-tests | tham khảo | tóm |
| Valve: Steam Deck Compatibility | https://partner.steamgames.com/doc/steamdeck/compat | tham khảo | tóm |
| Apple: 5.1.1(v) Offering account deletion | https://developer.apple.com/support/offering-account-deletion-in-your-app/ | webapp.md §4 | đọc |
| Google Play: account deletion | https://support.google.com/googleplay/android-developer/answer/13327111 | webapp.md §4 | tóm |
| Anthropic: Skill authoring best practices | https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices | cấu trúc skill, common.md R1/R7 | đọc |
| Anthropic: Effective harnesses for long-running agents | https://www.anthropic.com/research/effective-harnesses-for-long-running-agents | common.md §4 | đọc |
| Anthropic: Claude Code best practices | https://www.anthropic.com/engineering/claude-code-best-practices | thiết kế chung | tóm |
| GOV.UK Service Manual: discovery / alpha / beta / live | https://www.gov.uk/service-manual/agile-delivery/how-the-discovery-phase-works (và các trang alpha, beta, live) | webapp.md §2 | đọc |
| GOV.UK: Writing user stories | https://www.gov.uk/service-manual/agile-delivery/writing-user-stories | webapp.md §2, common.md §4 | đọc |
| GOV.UK: Service Standard | https://www.gov.uk/service-manual/service-standard | tham khảo | đọc |
| GOV.UK Design System: Page not found, Problem with the service | https://design-system.service.gov.uk/patterns/page-not-found-pages/ | webapp.md §3 | đọc |
| OWASP: Forgot Password Cheat Sheet | https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html | webapp.md §4 | đọc |
| OWASP: ASVS 5.0 | https://owasp.org/www-project-application-security-verification-standard/ | webapp.md §7 | tóm |
| W3C: WCAG 2.2 | https://www.w3.org/TR/WCAG22/ | webapp.md §7 | chưa đọc |
| Scrum Guide 2020 | https://scrumguides.org/scrum-guide.html | common.md §6 | đọc (Definition of Done, Product Goal) |
| Basecamp: Shape Up, chương 3, 6, 7, 12 | https://basecamp.com/shapeup | webapp.md §2, common.md §5 | đọc |
| NN/g: 10 Usability Heuristics | https://www.nngroup.com/articles/ten-usability-heuristics/ | webapp.md §7 | tóm |
| MDN: Page Visibility API | https://developer.mozilla.org/en-US/docs/Web/API/Page_Visibility_API | game.md §6 | đọc |
| MDN: Autoplay guide | https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Autoplay | game.md §6 | đọc |
| MDN: Storage quotas and eviction criteria | https://developer.mozilla.org/en-US/docs/Web/API/Storage_API/Storage_quotas_and_eviction_criteria | game.md §6 | đọc |
| Google web.dev: Core Web Vitals | https://web.dev/articles/vitals | webapp.md §7 | chưa đọc |
| EU GDPR Art. 17, 20 | https://gdpr-info.eu/art-17-gdpr/ · https://gdpr-info.eu/art-20-gdpr/ | webapp.md §4 | chưa đọc |
| Game Accessibility Guidelines | https://gameaccessibilityguidelines.com/full-list/ | common.md §6 | tóm |
| ISTQB Foundation Syllabus v4.0.1 | https://www.istqb.org/wp-content/uploads/2024/11/ISTQB_CTFL_Syllabus_v4.0.1.pdf | common.md §6 | tóm |

## 3. Sách, bài viết, người trong nghề

| Nguồn | Dùng ở | Mức đọc |
|---|---|---|
| Rami Ismail, *Milestones* (https://ltpf.ramiismail.com/milestones/) | game.md §2 | đọc |
| h-idris, *Main menu design* (https://h-idris.com/blog/game-main-menu-design.html) | game.md §4 | đọc |
| Steve Bromley, *How to save games* (https://www.stevebromley.com/blog/2012/06/23/how-to-save-games/) | game.md §5 | tóm |
| Game Developer, *Create better game settings options (checklist)* | game.md §4 | tóm |
| Vince Speelman, *The Nine States of Design* (CSS-Tricks) | webapp.md §5 | đọc phần đầu |
| Tim Ryan, *The Anatomy of a Design Document* (Gamasutra 1999) | common.md R2 | tóm |
| ACM SIGDOC, *Game Design Documentation: Four Perspectives from Independent Game Studios* | common.md R2 | đọc bản tóm tắt |
| Bugnet, *Indie Game QA on a Budget* | common.md §6 | tóm |
| Stone Librande, *One-Page Designs* (GDC 2010) | thiết kế chung | chưa đọc (đã kiểm link) |
| Heather Maxwell Chandler, *The Game Production Handbook* | thiết kế chung | chưa đọc |
| Scott Rogers, *Level Up!* | thiết kế chung | chưa đọc |
| Celia Hodent, *The Gamer's Brain* | game.md §4 (tách HUD khỏi menu) | chưa đọc |
| Clinton Keith, *Agile Game Development with Scrum* | thiết kế chung | chưa đọc |
| Tracy Fullerton, *Game Design Workshop* | common.md §6 | chưa đọc |

## 4. Quy tắc không có nguồn chính thức
Các quy tắc sau là thực hành phổ biến hoặc ước tính của người soạn, được ghi chú ngay trong file tham chiếu:
- Ngưỡng chia file 80 / 400 dòng, 25 KB, 150 dòng cho một thực thể (ước tính từ giới hạn đọc file của công cụ).
- Phím mũi tên và Space không làm cuộn trang; fullscreen chỉ bật khi người chơi bấm.
- Nút xuất/nhập save (cách giảm rủi ro do MDN mô tả, chứ không phải quy định).
- Ngày đóng băng tính năng ở mốc 70% (lấy theo mặc định của CCGS).
