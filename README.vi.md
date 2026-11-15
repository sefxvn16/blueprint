# Blueprint (tiếng Việt)

Plugin Claude Code giúp vibe code game (kể cả game chạy trên trình duyệt) và web/app không thiếu màn hình, luồng, thiết lập cơ bản, và biết lúc nào thì chuyển giai đoạn. Plugin chỉ lập và rà **bản thiết kế**; không viết code. [English](README.md)

## Cài
Trong Claude Code:
```
/plugin marketplace add sefxvn16/blueprint
/plugin install product-blueprint@blueprint
```
Bật/tắt bằng `/plugin`. Plugin không có hook hay script và không phụ thuộc plugin nào khác, nên tắt đi không ảnh hưởng gì.

## Dùng
Gọi `/blueprint`, hoặc nói tự nhiên:

| Muốn | Nói | Chế độ |
|---|---|---|
| Bắt đầu game hoặc web/app mới | "làm game nuôi pet chạy trên web" | new |
| Biết còn thiếu gì, có sang giai đoạn sau được chưa | "game này còn thiếu màn gì?" | check |
| Ghi lại ý tưởng chợt nghĩ ra, chưa làm ngay | "thêm tính năng câu cá được không?" | idea |

## Tạo ra gì trong dự án
```
design/README.md      spec: tầm nhìn, phạm vi, Keep, Không làm, danh sách màn, chỉ mục
design/<domain>.md    chi tiết từng lĩnh vực
design/features.json  tính năng, tiêu chí xong, trạng thái (pass cần bằng chứng)
design/ideas.md       ý tưởng chờ chọn ở mốc giai đoạn
architecture.md       stack, cây thư mục (Folder map), core/module, lưu dữ liệu
```
Cây thư mục được duyệt và tạo sẵn trước dòng code thật đầu tiên. Sau đó, file mới phải nằm trong thư mục có trong Folder map. Plugin không đụng tới `PLAN.md`, CLAUDE.md hay code.

## Giấy phép
MIT: dùng miễn phí cho mọi mục đích, kể cả thương mại; chỉ cần giữ dòng bản quyền. Nguồn tham khảo: [SOURCES.md](product-blueprint/SOURCES.md).

## Giới hạn đã biết
- Ngưỡng chia file (80 / 400 dòng, 25 KB) là ước tính.
- Game nhiều người chơi có danh mục phòng (tạo, vào, duyệt, kick, chuyển chủ phòng, sảnh chờ, rời, kết nối lại, kết quả, bảng xếp hạng, báo cáo); chưa có ghép trận với người lạ và danh sách bạn bè.
- Đã chạy thử thật chế độ new và check. Bản 0.2.0 sửa chế độ check: đọc điều kiện hiển thị, kiểm cài đặt có được áp dụng, chạy app, đối chiếu thiết kế của dự án. Chế độ idea chưa chạy thử.
