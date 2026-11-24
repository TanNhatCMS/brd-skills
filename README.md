# brd-skills

Bộ skill viết và kiểm duyệt tài liệu Business Requirement Document (BRD) bằng AI, dùng chung cho **Claude**, **ChatGPT** và **Antigravity**.

Nguồn quy trình: quy trình 7 bước viết BRD bằng AI (thiết lập bối cảnh → cung cấp tài liệu → bóc tách yêu cầu → phân tích lỗ hổng → viết theo từng phần → kiểm duyệt bằng AI → kiểm tra lần cuối), kèm tài liệu BRD mẫu domain Retail Banking (quy trình đổi địa chỉ khách hàng).

## Skills

| Skill | Làm gì | Khi nào dùng |
|---|---|---|
| `brd-writer` | Viết BRD bằng AI theo quy trình 7 bước | Khi cần viết mới hoặc hoàn thiện một BRD từ tài liệu thô, transcript họp, Jira/Confluence |
| `brd-reviewer` | Đóng vai người phản biện, soi lỗi BRD | Khi đã có bản nháp BRD và cần kiểm duyệt trước khi gửi stakeholder |
| `brd-retail-banking` | Kiến thức domain Retail Banking cho BRD | Khi BRD thuộc domain ngân hàng bán lẻ: tài khoản, địa chỉ khách hàng, kênh giao dịch, audit |

Tất cả skill theo chuẩn mở **Agent Skills** (`SKILL.md` + frontmatter `name`/`description`), nên cùng một bộ file dùng được cho cả ba nền tảng, chỉ khác đường cài đặt.

## Cài đặt

### Claude (Claude Code / Claude.ai)

```bash
# Cài theo project (khuyên dùng)
cp -r skills/* .claude/skills/

# Hoặc cài toàn máy
cp -r skills/* ~/.claude/skills/
```

Gõ `/brd-writer`, `/brd-reviewer` hoặc nhắc "viết BRD", "review BRD" trong chat là skill tự kích hoạt.

### ChatGPT

ChatGPT hỗ trợ Skills theo cùng định dạng `SKILL.md`. Xem hướng dẫn chi tiết trong `chatgpt/README.md`. Tóm tắt:

1. Vào Settings → Skills → Upload, chọn thư mục `skills/`.
2. Hoặc tạo một GPT mới và tải `chatgpt/gpt-instructions.md` làm Custom Instructions + đính kèm thư mục `skills/` làm Knowledge.

### Antigravity

Antigravity hỗ trợ Agent Skills (`SKILL.md`). Xem `antigravity/README.md`. Tóm tắt:

```bash
# Cài theo project
cp -r skills/* .agent/skills/

# Hoặc cài toàn máy (Skills manager trong Antigravity)
```

## Quy trình 7 bước (tóm tắt)

1. **Thiết lập bối cảnh:** mục tiêu dự án, bài toán kinh doanh, bên liên quan, quy trình hiện tại, kỳ vọng đầu ra.
2. **Cung cấp đầy đủ tài liệu đã có:** transcript họp stakeholder, Jira tickets, Confluence, tài liệu quy trình cũ, business rules hiện hành.
3. **Bóc tách yêu cầu trước khi viết:** phân loại thành Business Needs, Requirements, Giả định, Ràng buộc, Phụ thuộc, Câu hỏi mở.
4. **Phân tích lỗ hổng:** hỏi AI còn thiếu thông tin gì để yêu cầu đầy đủ, rõ ràng, nhất quán → lập danh sách câu hỏi follow-up cho stakeholder.
5. **Viết BRD theo từng phần:** đi lần lượt Business Objectives, Scope, AS-IS, TO-BE, Business Requirements, Business Rules, Risks, Success Criteria — không ép AI sinh toàn bộ trong một prompt.
6. **Tạo lớp kiểm duyệt bằng AI:** mở phiên mới, đưa bản nháp vào, yêu cầu AI đóng vai người phản biện (skill `brd-reviewer`).
7. **Kiểm tra lần cuối:** truy ngược từng yêu cầu về tài liệu gốc, mục tiêu kinh doanh và stakeholder tương ứng.

Chi tiết từng bước + prompt mẫu: xem `skills/brd-writer/SKILL.md` và `skills/brd-writer/references/prompt-library.md`.

## Cấu trúc repo

```text
brd-skills/
├── README.md
├── LICENSE
├── skills/
│   ├── brd-writer/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── brd-template.md                  # Mẫu BRD 14 mục
│   │       ├── prompt-library.md                # Prompt từng bước
│   │       └── retail-banking-address-change-brd.md  # BRD mẫu (Retail Banking)
│   ├── brd-reviewer/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── review-prompt.md                 # Prompt kiểm duyệt dùng cho mọi AI
│   │       └── review-checklist.md              # Checklist soát lỗi
│   └── brd-retail-banking/
│       ├── SKILL.md
│       └── references/
│           ├── domain-notes.md                  # Ghi chú domain
│           └── glossary.md                      # Thuật ngữ
├── chatgpt/
│   ├── README.md
│   └── gpt-instructions.md                      # Custom Instructions cho GPT
├── antigravity/
│   └── README.md
├── examples/
│   ├── README.md
│   └── sample-output/                           # Output mẫu khi chạy skill
└── evals/
    └── evals.json                               # Test prompts để kiểm thử skill
```

## Tài liệu mẫu

`skills/brd-writer/references/retail-banking-address-change-brd.md` là bản transcribe đầy đủ từ file PDF "BRD Retail Banking" (BRD-CAM-001, Customer Address Management Modernization, 20/11/2026, bản PDF gốc lưu cùng thư mục: `brd-retail-banking-full.pdf`): Document Control, Executive Summary, Business Problem, Objectives (OBJ-01–04), Stakeholders, Scope, AS-IS, TO-BE, Business Requirements (BR-001–008), Business Rules (RULE-01–05), Non-Functional Expectations, Exceptions, Data Requirements, Dependencies/Assumptions/Risks, Traceability Matrix, Open Questions (Q-01–05), Acceptance & Approval, Appendix A Source Register.

## Đóng góp

Mở issue hoặc PR. Mọi skill mới nên kèm `evals.json` với 2–3 test prompt thực tế.

## License

MIT — xem `LICENSE`.
