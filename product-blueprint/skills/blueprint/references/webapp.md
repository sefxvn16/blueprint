# Web/app: pha, màn hình theo vai trò, tài khoản, trạng thái

## Mục lục
1. Câu hỏi đầu dự án
2. Pha và cổng
3. Màn hình theo vai trò
4. Quy tắc tài khoản
5. Trạng thái của mọi màn
6. File lĩnh vực mặc định
7. Checklist phát hành
8. Nguồn

## 1. Câu hỏi đầu dự án (hỏi gộp một lượt, câu nào cũng có mặc định)

| Câu hỏi | Mặc định | Ảnh hưởng tới |
|---|---|---|
| Ai dùng, họ đang gặp vấn đề gì (một câu chuyện cụ thể) | (bắt buộc người dùng nói) | README › Vấn đề |
| Công sức tối đa sẵn sàng bỏ cho bản đầu (appetite) | 2 tuần | README › Phạm vi, Không làm |
| Có tài khoản không; đăng nhập bằng gì | có, email + mật khẩu | §3 Xác thực, Người dùng |
| Có những vai trò nào (khách, người dùng, quản trị, …) | khách, người dùng, quản trị | §3 |
| Lưu dữ liệu cá nhân gì | email, tên | xuất/xóa dữ liệu, mức ASVS |
| Có thanh toán / gói trả phí không | không | Billing, ghi chú pháp lý |
| Có thông báo (email / trong app) không | email cho tài khoản | Thông báo |
| Phát hành ở đâu (web / App Store / Google Play) | web | quy tắc xóa tài khoản của store |
| Ngôn ngữ giao diện | tiếng Việt | i18n |

## 2. Pha và cổng (GOV.UK Service Manual, rút gọn cho người làm một mình)

| Pha | Tài liệu phải có | Xong khi |
|---|---|---|
| discovery | `design/README.md` dạng pitch: **Problem** (một câu chuyện cụ thể) · **Appetite** · **Solution** (phác) · **Rabbit holes** · **No-gos** | đã quyết **làm tiếp hay dừng**; có danh sách ý muốn thử và cách đo thành công. Chưa viết code sản phẩm ở pha này |
| alpha | màn hình theo vai trò (§3) trong README; prototype bấm thử được | đã thử giả định rủi ro nhất; người dùng duyệt luồng chính. Code alpha có thể bỏ, không dùng làm code thật |
| beta | đủ file lĩnh vực, `architecture.md` có Folder map đã duyệt và cây đã được tạo (`common.md` §3b), `features.json` | mọi feature `mandatory` của beta là `pass`; đã tự rà theo §7; có vài người dùng thật (private beta) trước khi mở công khai |
| live | danh sách cắt và polish (`common.md` §6) | §7 đạt; có theo dõi lỗi và uptime; **đã thử restore backup ít nhất một lần** |

Mỗi feature được viết theo dạng "As a… I need… So that…", acceptance theo dạng "xong khi…". Chia việc theo **phần của sản phẩm** (ví dụ "Đăng ký", "Danh sách chi tiêu"), không theo tầng code ("front-end", "bugs").

## 3. Màn hình theo vai trò

Cột phase: `beta` là phải xong trước khi mời người dùng thử (private beta); `live` là phải xong trước khi mở công khai.

| id | Màn / luồng | Bắt buộc khi | phase |
|---|---|---|---|
| `public-home` | Trang chủ / landing | luôn luôn | beta |
| `public-404` | Trang không tìm thấy | luôn luôn | beta |
| `public-500` | Trang "có sự cố", có cách liên hệ | luôn luôn | beta |
| `public-legal` | Privacy policy, Terms | có thu dữ liệu cá nhân hoặc phát hành qua store | live |
| `auth-signup` | Đăng ký (+ xác minh email) | có tài khoản | beta |
| `auth-login` | Đăng nhập, đăng xuất | có tài khoản | beta |
| `auth-reset` | Quên / đặt lại mật khẩu | đăng nhập bằng mật khẩu | beta |
| `user-profile` | Hồ sơ cá nhân | có tài khoản | beta |
| `user-settings` | Cài đặt tài khoản: đổi email/mật khẩu, ngôn ngữ, thông báo | có tài khoản | beta |
| `user-export` | Xuất dữ liệu của tôi | lưu dữ liệu cá nhân | live |
| `user-delete` | Xóa tài khoản | có tài khoản | live |
| `admin-users` | Quản lý người dùng và vai trò | có vai trò quản trị | beta |
| `admin-content` | Quản lý nội dung / dữ liệu | có nội dung do người dùng hoặc admin tạo | beta |
| `admin-audit` | Nhật ký thao tác của admin | có vai trò quản trị | live |
| `shared-notify` | Thông báo (email / trong app) | có thông báo | live |

## 4. Quy tắc tài khoản

- **Quên mật khẩu (OWASP):**
  - thông báo giống nhau và thời gian phản hồi như nhau, dù email có tồn tại hay không;
  - giới hạn số lần gửi yêu cầu;
  - token ngẫu nhiên an toàn, đủ dài, gắn với một người dùng, dùng một lần, có hạn;
  - link đặt lại dùng HTTPS và không lấy domain từ header Host;
  - chưa có token hợp lệ thì không đổi gì trên tài khoản;
  - đặt mật khẩu mới thì nhập hai lần, cùng chính sách mật khẩu với lúc đăng ký;
  - **xong không tự đăng nhập**; gửi email báo mật khẩu đã đổi; hỏi người dùng có muốn đăng xuất mọi phiên khác không.
- **Phiên:** kiểm phiên và quyền ở server; tạo phiên mới sau khi đăng nhập; đăng xuất là phiên hết hiệu lực ở server.
- **Quản trị:** route admin kiểm quyền ở server, không chỉ giấu link. Mọi thao tác admin ghi nhật ký: thời điểm · ai làm · làm gì · trên đối tượng nào.
- **Xóa tài khoản (Apple 5.1.1(v), áp cho cả web cho nhất quán):**
  - dễ tìm, thường đặt trong cài đặt tài khoản;
  - xóa cả bản ghi tài khoản lẫn dữ liệu đi kèm, kể cả nội dung người dùng đã đăng; chỉ "vô hiệu hóa" là không đủ;
  - được yêu cầu xác thực lại hoặc nhập mã để chắc chắn, nhưng không làm khó;
  - nếu xóa mất thời gian thì báo trước bao lâu và báo khi xong;
  - dữ liệu luật bắt buộc giữ thì nói rõ giữ gì;
  - tài khoản khách do app tự tạo cũng phải xóa được;
  - áp cho mọi người dùng, không chỉ ở nơi có luật.
- **Xuất dữ liệu (GDPR Art. 20):** xuất ở định dạng phổ biến, máy đọc được (JSON/CSV).

## 5. Trạng thái của mọi màn

Mỗi màn có danh sách hoặc dữ liệu phải mô tả và làm đủ: **rỗng** (có hướng dẫn bước tiếp theo, không chỉ "Không có dữ liệu") · **đang tải** · **lỗi** (nói cách khắc phục bằng lời dễ hiểu, không in lỗi API thô) · **thành công** · **quá nhiều** (phân trang/tìm kiếm). Test bằng tài khoản mới tinh, vì tài khoản dev đã có sẵn dữ liệu.

## 6. File lĩnh vực mặc định

| File | Chứa | Tạo khi |
|---|---|---|
| `accounts-roles.md` | vai trò, quyền, đăng ký/đăng nhập, hồ sơ, cài đặt, xóa/xuất | có tài khoản |
| `features-<area>.md` | một khu vực chức năng chính: user story, màn hình, quy tắc | mỗi khu vực một file (R3: khu vực nhỏ thì gộp) |
| `admin.md` | quản lý người dùng, nội dung, cấu hình, nhật ký | có quản trị |
| `shared-pages.md` | trang chung, 404/500, trạng thái, thông báo, pháp lý | luôn luôn |
| `ui-style.md` | phong cách, màu, chữ, component dùng chung | luôn luôn |

## 7. Checklist phát hành

- [ ] Accessibility WCAG 2.2 mức AA cho các luồng chính (bàn phím, nhãn, độ tương phản, thông báo lỗi)
- [ ] Bảo mật theo OWASP ASVS 5.0 mức L1; lên L2 nếu lưu dữ liệu cá nhân hoặc tiền
- [ ] Không có khóa API/mật khẩu trong code; biến môi trường không bị commit
- [ ] Core Web Vitals trong ngưỡng "good" trên trang chính
- [ ] Có backup và đã thử restore; có theo dõi lỗi
- [ ] Privacy policy và Terms đã đăng nếu §3 yêu cầu
- [ ] Mọi màn có đủ trạng thái §5; đã thử bằng tài khoản mới
- [ ] Rà theo 10 heuristic của NN/g trước khi cho người thật dùng thử

## 8. Nguồn
GOV.UK Service Manual: *How the discovery / alpha / beta / live phase works*, *Writing user stories*, *Service Standard* · GOV.UK Design System: *Page not found*, *There is a problem with the service* · Shape Up ch.3 *Set Boundaries*, ch.6 *Write the Pitch*, ch.12 *Map the Scopes* · OWASP *Forgot Password Cheat Sheet*, ASVS 5.0 · Apple *5.1.1(v) Offering account deletion* · Google Play *account deletion* (chưa đọc kỹ) · GDPR Art. 17, 20 · Vince Speelman *Nine States of Design* · W3C WCAG 2.2 · NN/g *10 Usability Heuristics* · Google web.dev Core Web Vitals.
