---
name: brd-writer
description: Viết Business Requirement Document (BRD) bằng AI theo quy trình 7 bước — thiết lập bối cảnh, gom tài liệu, bóc tách yêu cầu, phân tích lỗ hổng, viết theo từng phần, kiểm duyệt, kiểm tra lần cuối. Dùng skill này whenever the user asks to write, draft, complete, or improve a BRD, tài liệu yêu cầu nghiệp vụ, business requirements, hoặc nhắc tới BRD, stakeholder, Jira, Confluence, AS-IS/TO-BE, business rules — kể cả khi họ không gọi tên skill.
---

# brd-writer — Viết BRD bằng AI theo quy trình 7 bước

Mục tiêu của skill này: tài liệu BRD do AI tạo ra phải sát nghiệp vụ và dùng được ngay, không chung chung. Nguyên tắc cốt lõi: **không bao giờ sinh toàn bộ BRD trong một prompt duy nhất** — đi từng bước, dừng lại để người dùng chốt trước khi sang bước tiếp theo.

Ngôn ngữ làm việc: theo ngôn ngữ người dùng yêu cầu. Giữ nguyên thuật ngữ nghiệp vụ tiếng Anh (BRD, UAT, downstream, stakeholder, Must/Should...). Bản Markdown là source chỉnh sửa chính; chỉ xuất PDF/Word khi người dùng yêu cầu.

## Quy trình 7 bước

### Bước 1 — Thiết lập bối cảnh

Trước khi viết bất cứ dòng nào, thu thập bức tranh toàn cảnh:

- Mục tiêu dự án và bài toán kinh doanh cần giải quyết
- Các bên liên quan (stakeholder) và vai trò của từng bên
- Quy trình hiện tại (AS-IS) và điểm đau
- Kỳ vọng đầu ra: đối tượng đọc, độ dài, định dạng, deadline

Nếu người dùng chưa cung cấp đủ, hỏi thẳng những điểm còn thiếu — không tự bịa bối cảnh. Output của bước này là một bản tóm tắt bối cảnh khoảng nửa trang để người dùng chốt trước khi đi tiếp.

### Bước 2 — Cung cấp đầy đủ tài liệu đã có

Yêu cầu người dùng tải lên toàn bộ tài liệu thô đang có, ví dụ:

- Transcript buổi họp với stakeholder
- Jira tickets, trang Confluence
- Tài liệu quy trình cũ, SOP, hướng dẫn vận hành
- Các business rules hiện hành

Đọc hết tài liệu trước khi viết. Ghi lại danh sách tài liệu đã nhận (tên file + ngày + nguồn) để làm Source Register ở cuối BRD. Tài liệu nào chưa có thì ghi rõ "Not provided — validate", không giả vờ là đã có.

### Bước 3 — Bóc tách yêu cầu trước khi viết

Chưa viết BRD vội. Phân loại toàn bộ dữ liệu đã thu thập thành từng nhóm riêng biệt:

| Nhóm | Nội dung |
|---|---|
| Business Needs | Nhu cầu kinh doanh, vấn đề cần giải quyết |
| Requirements | Yêu cầu nghiệp vụ (đánh số BR-001...) |
| Giả định (Assumptions) | Điều đang cho là đúng nhưng chưa xác thực |
| Ràng buộc (Constraints) | Giới hạn về pháp lý, kỹ thuật, thời gian, ngân sách |
| Phụ thuộc (Dependencies) | Thứ khác phải xong trước / hệ thống khác phải có |
| Câu hỏi mở | Điểm chưa rõ, cần stakeholder quyết |

Output: bảng bóc tách để người dùng soát. Chỉ khi người dùng đồng ý với bảng này mới sang bước 4.

### Bước 4 — Phân tích lỗ hổng

Đặt câu hỏi cho chính mình (và cho AI): "Còn thiếu những thông tin gì để các yêu cầu trên trở nên đầy đủ, rõ ràng, nhất quán?"

Kiểm tra cụ thể:

- Yêu cầu nào mơ hồ, không đo được, không kiểm thử được?
- Mục tiêu nào chưa có số đo / baseline?
- Trường hợp ngoại lệ nào chưa được nhắc tới?
- Stakeholder nào chưa được hỏi?
- Dữ liệu nào chưa có nguồn xác thực?

Dùng kết quả để lập danh sách câu hỏi follow-up gửi cho các bên liên quan. Ghi các câu hỏi này vào mục Open Questions (mục 15 của template), kèm decision owner và mức ưu tiên.

### Bước 5 — Viết BRD theo từng phần

Viết lần lượt theo trình tự logic, mỗi phần xong thì dừng để người dùng soát rồi mới viết phần tiếp theo. Trình tự đề xuất (theo `references/brd-template.md`):

1. Executive Summary
2. Business Problem and Opportunity
3. Objectives and Success Measures
4. Stakeholders and Governance
5. Scope (In Scope / Out of Scope / Boundaries)
6. AS-IS Process
7. TO-BE Process
8. Business Requirements
9. Business Rules
10. Non-Functional Business Expectations
11. Exceptions and Edge Cases
12. Data Requirements (Business Level)
13. Dependencies, Assumptions, Risks
14. Traceability Matrix
15. Open Questions and Clarifications
16. Acceptance and Approval Approach
- Appendix A: Source and Evidence Register

Quy tắc viết từng yêu cầu (mục 8):

- Mỗi yêu cầu một ID duy nhất (`BR-001`, `BR-002`...), mức ưu tiên Must / Should / Could
- Viết theo mẫu: "The bank shall..." + actor + hành động + điều kiện + kết quả kỳ vọng
- Mỗi yêu cầu kèm rationale và acceptance evidence — tức là làm sao để kiểm chứng được yêu cầu đó đã đạt
- Không bịa số liệu: target nào chưa có baseline thì ghi rõ là proposed hypothesis, cần baseline trước sign-off
- Yêu cầu nào cũng phải trace được về một Objective (mục 3) — yêu cầu không gắn với mục tiêu nào thì bỏ hoặc hỏi lại

### Bước 6 — Tạo một lớp kiểm duyệt bằng AI

Không tự review bản nháp của chính mình trong cùng một phiên. Mở một phiên làm việc hoàn toàn mới, đưa bản nháp BRD vào và dùng skill `brd-reviewer` để AI đóng vai người phản biện soi lỗi. Chỉ sửa bản nháp sau khi đã có báo cáo review.

### Bước 7 — Kiểm tra lần cuối

Kiểm tra từng yêu cầu ngược lại ba thứ:

1. **Nguồn tài liệu gốc** — yêu cầu này lấy từ transcript/ticket/trang Confluence nào? Ghi vào Source Register.
2. **Mục tiêu kinh doanh** — yêu cầu này phục vụ Objective nào? Kiểm tra qua Traceability Matrix.
3. **Stakeholder tương ứng** — ai là người quyết / người chịu trách nhiệm cho yêu cầu này?

Yêu cầu nào không truy ngược được về ít nhất một trong ba thứ trên thì đánh dấu lại, hỏi stakeholder hoặc loại bỏ — không để yêu cầu "mồ côi" trong BRD.

## Tài liệu tham khảo

Đọc các file này khi cần, không đọc hết ngay từ đầu:

- `references/brd-template.md` — mẫu BRD 14+ mục, dùng làm khung cho mọi BRD mới
- `references/prompt-library.md` — prompt copy-paste được cho từng bước 1–7
- `references/retail-banking-address-change-brd.md` — BRD mẫu đầy đủ domain Retail Banking (BRD-CAM-001, 16 mục + Appendix A); bản PDF gốc: `references/brd-retail-banking-full.pdf`

Khi BRD thuộc domain Retail Banking, đọc thêm skill `brd-retail-banking` để lấy kiến thức domain (master record, downstream consumers, audit trail, notification preferences).

## Output

- Mặc định xuất file Markdown theo template, đặt tên `brd-<tên-dự-án>.md`
- Giữ một file Markdown duy nhất làm source — mọi chỉnh sửa sau này sửa trên file này, không tạo bản copy mới
- Chỉ xuất PDF/Word khi người dùng yêu cầu rõ
