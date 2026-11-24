# Dùng brd-skills trên ChatGPT

ChatGPT hỗ trợ Skills theo cùng định dạng `SKILL.md` như Claude (chuẩn mở Agent Skills). Có 2 cách dùng:

## Cách 1 — Cài Skills vào ChatGPT (khuyên dùng)

1. Vào **Settings → Skills** (hoặc mục Skills trong sidebar).
2. Chọn **Upload skill** / **Add skill**, tải lên từng thư mục trong `skills/`:
   - `skills/brd-writer/` — viết BRD theo quy trình 7 bước
   - `skills/brd-reviewer/` — kiểm duyệt bản nháp BRD
   - `skills/brd-retail-banking/` — kiến thức domain Retail Banking
3. Mỗi skill là một thư mục chứa `SKILL.md` + thư mục `references/` — tải lên nguyên thư mục, đừng chỉ tải file `SKILL.md` lẻ (skill sẽ mất tài liệu tham khảo).

Sau khi cài, chỉ cần nhắn kiểu "viết BRD cho dự án đổi địa chỉ khách hàng" là skill tự kích hoạt.

## Cách 2 — Tạo một GPT chuyên viết BRD

1. Tạo GPT mới (Create a GPT).
2. Dán nội dung file `gpt-instructions.md` trong thư mục này vào **Instructions**.
3. Tải toàn bộ thư mục `skills/` lên làm **Knowledge** của GPT.
4. Đặt tên gợi ý: "BRD Writer — Retail Banking".

Nhược điểm của cách 2 so với cách 1: GPT không tự "kích hoạt" skill theo ngữ cảnh linh hoạt bằng Skills, và mỗi lần cập nhật skill phải tải lại Knowledge.

## Lưu ý khi dùng trên ChatGPT

- **Luôn viết theo từng phần, đừng ép một prompt sinh toàn bộ BRD.** Hỏi ChatGPT viết từng mục rồi dừng để soát — đúng như Bước 5 trong `brd-writer`.
- **Kiểm duyệt phải mở chat mới.** Đừng review bản nháp trong cùng cuộc trò chuyện đã viết nó — mở chat mới, dán bản nháp vào, dùng prompt trong `skills/brd-reviewer/references/review-prompt.md`.
- ChatGPT không đọc được file đính kèm trong `references/` nếu bạn chỉ dán `SKILL.md` — phải tải cả thư mục skill hoặc dán nội dung file tham khảo vào chat khi cần (ví dụ: dán template khi viết, dán BRD mẫu khi cần đối chiếu).
- Ngôn ngữ: skill viết bằng tiếng Việt, output BRD mặc định tiếng Anh theo mẫu. Muốn BRD tiếng Việt thì nói rõ trong câu đầu tiên.
