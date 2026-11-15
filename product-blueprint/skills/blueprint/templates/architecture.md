# Architecture: <Tên sản phẩm>

Trạng thái: Nháp · Cập nhật: YYYY-MM-DD · Liên quan: design/README.md

## Mục lục
Stack and commands · Folder map · Core · Modules · Data flow · Data storage · Decisions

## Stack and commands
- Ngôn ngữ / framework: <...>
- Chạy: `<lệnh>` · Test: `<lệnh>` · Build: `<lệnh>`

## Folder map
Theo: <tên framework/engine và bố cục chính thức của nó, hoặc "cây mặc định của blueprint"> · Quy ước tên: kebab-case · Duyệt: <ngày, người dùng>

```
<cây thư mục, mỗi thư mục một dòng mục đích>
design/            thiết kế sản phẩm
data/              số liệu chỉnh được
assets/            images/ audio/ fonts/ + CREDITS.md
src/core/          dịch vụ có trạng thái, dùng chung
src/modules/<id>/  mỗi module một thư mục, mọi file của module nằm trong đó
src/shared/        component/hàm không giữ trạng thái, ≥2 module dùng
tests/             unit/ integration/
prototypes/<name>/ prototype, tách khỏi code thật
```

Thêm thư mục cấp một hoặc module mới: sửa cây này trước rồi mới tạo; thư mục cấp một mới cần người dùng đồng ý.

## Core
Tiêu chí: thứ mà từ hai module trở lên cùng phụ thuộc, hoặc mang trạng thái toàn cục.

| Dịch vụ | Trách nhiệm | Ai dùng |
|---|---|---|
| settings | đọc/ghi thiết lập, phát sự kiện khi đổi | mọi màn |
| save | lưu/tải tiến độ, phiên bản dữ liệu | <...> |

## Modules
Quy tắc: module chỉ phụ thuộc core, không import module khác; trao đổi qua sự kiện hoặc interface của core.

| Module | Màn / feature (id) | Phụ thuộc core |
|---|---|---|

## Data flow
<Dữ liệu đi từ đâu tới đâu: input → state → hiển thị → lưu.>

## Data storage
<Lưu ở đâu, định dạng, số phiên bản, cách nâng cấp dữ liệu cũ; settings tách khỏi tiến độ.>

## Decisions
| # | Ngày | Bối cảnh | Chọn | Bỏ và vì sao |
|---|---|---|---|---|
