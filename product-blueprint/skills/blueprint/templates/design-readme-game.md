# <Tên game>

Trạng thái: Nháp · Cập nhật: YYYY-MM-DD · Loại: game · Giai đoạn hiện tại: concept

## Mục lục
Vision · Core loop · Audience and platform · Scope · First minute · Keep · Not doing · Screens · Save · Accessibility · Definition of Done · Index

## Vision
<Một đoạn: game này là gì, người chơi cảm thấy gì, khác các game gần nhất ở điểm nào.>

## Core loop
<Người chơi làm gì lặp đi lặp lại: hành động → kết quả → phần thưởng. Phút đầu tiên diễn ra thế nào.>

## Audience and platform
- Người chơi: <ai>
- Nền tảng: <trình duyệt / PC / mobile> · Điều khiển: <...>
- Ngôn ngữ: <...>

## Scope
- Bản đầu gồm: <...>
- Thua: <hết / mềm / không có> · Kết thúc: <có / không> · Thời gian thực: <có / không>

## First minute
<Phút đầu diễn ra thế nào: người chơi thấy gì, làm gì đầu tiên, hiểu được gì. Cổng vertical slice yêu cầu người mới hiểu cần làm gì trong 2 phút.>

## Keep
<Những điều phải giữ nguyên dù sau này đổi gì: cảm giác, nhân vật, luật chơi cốt lõi. Mọi đề xuất thay đổi hoặc cắt bỏ đều đối chiếu với mục này.>

## Not doing
<Những gì cố ý không làm, mỗi dòng một mục, kèm lý do. Màn bắt buộc nào bị bỏ phải ghi ở đây và người dùng đã đồng ý.>

## Screens
| id | Màn | Bắt buộc | Chi tiết ở |
|---|---|---|---|
| shell-title | Title / Main menu | có | shell-ui.md |

## Save
Lưu ở: <máy / server / cả hai> · Mô hình: <autosave + thủ công, số slot> · Chi tiết: architecture.md › Data storage

## Accessibility
Tier: <Basic / Standard> · Ghi chú: <...>

## Definition of Done
Một feature chỉ `pass` khi: đạt acceptance trong features.json · smoke test không hỏng · có bằng chứng (ảnh chụp, lệnh test, hoặc người dùng xác nhận đã chơi).

## Index
| File | Chứa | Đọc khi |
|---|---|---|
| features.json | danh sách tính năng, tiêu chí xong, trạng thái | trước khi làm hoặc đóng một tính năng |
| ideas.md | ý tưởng chưa chọn | khi có ý tưởng mới; ở mốc giai đoạn |
| shell-ui.md | menu, settings, pause, HUD, tutorial | làm bất kỳ màn nào ngoài gameplay |
| ../architecture.md | stack, thư mục, core/module, lưu dữ liệu | trước khi viết code thật |
