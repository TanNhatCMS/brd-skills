# Examples

## Output mẫu

Thư mục `sample-output/` chứa output mẫu khi chạy skill `brd-writer` với một brief ngắn — để người dùng hình dung skill viết ra sao trước khi dùng cho dự án thật.

- `sample-output/brd-email-change-requirements.md` — mục 8 Business Requirements mẫu cho tính năng "đổi địa chỉ email khách hàng" (chỉ là ví dụ minh họa cách viết, không phải BRD thật).

## Cách chạy thử skill

1. Cài skill theo hướng dẫn ở README chính (Claude / ChatGPT / Antigravity).
2. Dùng một trong các test prompt trong `evals/evals.json`.
3. So sánh output với `sample-output/` để xem skill có viết đúng format không (ID, Must/Should, rationale + acceptance evidence, trace về Objective).

## Ghi chú

- Output mẫu được tạo bằng chính skill trong repo (không viết tay) để chứng minh skill chạy được end-to-end.
- Muốn thêm ví dụ mới: chạy skill với brief thật, lưu output vào `sample-output/`, ghi rõ brief đầu vào ở đầu file.
