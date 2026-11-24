# Dùng brd-skills trên Antigravity

Antigravity hỗ trợ Agent Skills theo chuẩn mở `SKILL.md` — cùng một bộ file skill dùng cho Claude và ChatGPT đều dùng được ở đây, chỉ khác đường cài đặt.

## Cài đặt

### Theo project (khuyên dùng)

```bash
# Từ thư mục gốc của project đang làm BRD
mkdir -p .agent/skills
cp -r /đường/dẫn/tới/brd-skills/skills/* .agent/skills/
```

### Toàn máy

Mở **Skills manager** trong Antigravity → **Add skill** → chọn từng thư mục trong `skills/`:

- `skills/brd-writer/` — viết BRD theo quy trình 7 bước
- `skills/brd-reviewer/` — kiểm duyệt bản nháp BRD
- `skills/brd-retail-banking/` — kiến thức domain Retail Banking

Mỗi skill là một thư mục chứa `SKILL.md` + thư mục `references/` — thêm nguyên thư mục, đừng chỉ thêm file `SKILL.md` lẻ.

## Cách dùng

- Nhắc "viết BRD", "review BRD" hoặc gõ `/brd-writer`, `/brd-reviewer` trong agent chat là skill tự kích hoạt.
- Quy trình làm việc giống hệt như mô tả trong `skills/brd-writer/SKILL.md`: đi từng bước 1–7, dừng để soát từng phần, kiểm duyệt ở phiên mới.
- File BRD viết ra nên lưu trong project (ví dụ: `docs/brd-<tên-dự-án>.md`) để Antigravity theo dõi và chỉnh sửa tiếp trong các phiên sau.

## Lưu ý

- **Kiểm duyệt phải mở phiên/agent mới.** Đừng review bản nháp trong cùng phiên đã viết nó — mở agent chat mới, đính kèm file BRD nháp, rồi gọi skill `brd-reviewer`.
- Nếu Antigravity của bạn chưa hiện mục Skills manager, cập nhật Antigravity lên bản mới nhất rồi thử lại — Agent Skills là tính năng theo chuẩn mở, đường dẫn `.agent/skills/` là layout chuẩn của nó.
- Ngôn ngữ: skill viết bằng tiếng Việt, output BRD mặc định tiếng Anh theo mẫu. Muốn BRD tiếng Việt thì nói rõ trong câu đầu tiên.
