# Prompt Library — Quy trình 7 bước viết BRD bằng AI

Prompt copy-paste được cho từng bước. Thay phần trong [ngoặc vuông] bằng thông tin thật của dự án. Dùng được cho mọi AI (Claude, ChatGPT, Antigravity...). Ngôn ngữ prompt: tiếng Việt cho phần hướng dẫn, output BRD giữ tiếng Anh theo mẫu.

## Bước 1 — Thiết lập bối cảnh

```text
Tôi cần viết một Business Requirement Document (BRD) cho dự án sau:

- Tên dự án: [tên dự án]
- Domain: [ví dụ: Retail Banking]
- Bài toán kinh doanh: [vấn đề đang gặp, ai bị ảnh hưởng, hậu quả hiện tại]
- Mục tiêu dự án: [kết quả mong muốn, đo bằng gì]
- Các bên liên quan: [Sponsor, Product Owner, Operations, Compliance, Technology, QA — kèm tên nếu có]
- Quy trình hiện tại tóm tắt: [AS-IS 3–5 dòng]
- Kỳ vọng đầu ra: BRD tiếng [Anh/Việt], khoảng [số] mục, đối tượng đọc là [ai], deadline [ngày]

Hãy tóm tắt lại bối cảnh thành nửa trang để tôi chốt trước khi đi tiếp. Nếu còn thiếu thông tin quan trọng thì hỏi tôi, đừng tự bịa.
```

## Bước 2 — Cung cấp tài liệu đã có

```text
Dưới đây là toàn bộ tài liệu thô tôi có cho dự án [tên dự án]:
- [liệt kê file đính kèm: transcript họp ngày X, Jira ticket ABC-123, trang Confluence Y, SOP cũ, business rules hiện hành]

Hãy đọc hết và lập danh sách tài liệu đã nhận (tên + ngày + nguồn). Tài liệu nào tôi chưa cung cấp nhưng cần có để viết BRD thì liệt kê riêng và ghi "Not provided — validate". Đừng viết BRD ở bước này.
```

## Bước 3 — Bóc tách yêu cầu trước khi viết

```text
Từ bối cảnh và tài liệu tôi đã cung cấp, hãy bóc tách thành bảng 6 nhóm, CHƯA viết BRD vội:

1. Business Needs — nhu cầu kinh doanh
2. Requirements — yêu cầu nghiệp vụ (đánh số tạm BR-001...)
3. Giả định (Assumptions) — điều đang cho là đúng nhưng chưa xác thực
4. Ràng buộc (Constraints) — giới hạn pháp lý, kỹ thuật, thời gian, ngân sách
5. Phụ thuộc (Dependencies) — thứ khác phải xong trước / hệ thống khác phải có
6. Câu hỏi mở — điểm chưa rõ, cần stakeholder quyết

Mỗi dòng ghi rõ nguồn (lấy từ tài liệu nào, trang/mục nào). Tôi sẽ soát bảng này trước khi sang bước tiếp theo.
```

## Bước 4 — Phân tích lỗ hổng

```text
Nhìn vào bảng bóc tách ở trên, hãy trả lời: "Còn thiếu những thông tin gì để các yêu cầu trên trở nên đầy đủ, rõ ràng, nhất quán?"

Kiểm tra cụ thể:
- Yêu cầu nào mơ hồ, không đo được, không kiểm thử được?
- Mục tiêu nào chưa có số đo hoặc baseline?
- Trường hợp ngoại lệ (exception / edge case) nào chưa được nhắc tới?
- Stakeholder nào chưa được hỏi?
- Dữ liệu nào chưa có nguồn xác thực?

Trả về danh sách câu hỏi follow-up, mỗi câu kèm: hỏi ai (decision owner) và mức ưu tiên (High/Medium/Low). Danh sách này sẽ đưa vào mục 15 Open Questions của BRD.
```

## Bước 5 — Viết BRD theo từng phần

```text
Viết BRD theo template đính kèm (16 mục + Appendix A). Viết LẦN LƯỢT từng phần, mỗi phần xong thì dừng để tôi soát:

Phần 1: Executive Summary
Phần 2: Business Problem and Opportunity
Phần 3: Objectives and Success Measures
Phần 4: Stakeholders and Governance
Phần 5: Scope (In Scope / Out of Scope / Boundaries)
Phần 6: AS-IS Process
Phần 7: TO-BE Process
Phần 8: Business Requirements
Phần 9: Business Rules
Phần 10: Non-Functional Business Expectations
Phần 11: Exceptions and Edge Cases
Phần 12: Data Requirements (Business Level)
Phần 13: Dependencies, Assumptions, Risks
Phần 14: Traceability Matrix
Phần 15: Open Questions and Clarifications
Phần 16: Acceptance and Approval Approach

Quy tắc:
- Yêu cầu viết theo mẫu "The [actor] shall...", kèm ID (BR-001...), mức Must/Should/Could, rationale và acceptance evidence
- Không bịa số liệu: target chưa có baseline thì ghi rõ là proposed hypothesis, cần baseline trước sign-off
- Mọi requirement phải trace về ít nhất một Objective
- Bắt đầu với Phần 1. Đừng viết các phần sau cho tới khi tôi nói tiếp.
```

## Bước 6 — Kiểm duyệt bằng AI (mở phiên mới)

```text
[Chạy trong một phiên làm việc HOÀN TOÀN MỚI, không dùng phiên đã viết BRD.]

Dưới đây là bản nháp BRD của tôi: [dán toàn bộ bản nháp hoặc đính kèm file]

Hãy đóng vai người phản biện (adversarial reviewer) và soi lỗi theo prompt kiểm duyệt trong skills/brd-reviewer/references/review-prompt.md. Chỉ指出 lỗi, không tự sửa bản nháp. Trả về bảng findings kèm severity, evidence và gợi ý sửa.
```

## Bước 7 — Kiểm tra lần cuối

```text
Kiểm tra từng yêu cầu trong BRD ngược lại ba thứ:
1. Nguồn tài liệu gốc — yêu cầu này lấy từ tài liệu nào? Ghi vào Source Register (Appendix A).
2. Mục tiêu kinh doanh — yêu cầu này phục vụ Objective nào? Kiểm tra qua Traceability Matrix.
3. Stakeholder tương ứng — ai quyết / ai chịu trách nhiệm cho yêu cầu này?

Lập bảng 3 cột: Requirement ID | Nguồn | Objective + Owner. Yêu cầu nào không truy ngược được về ít nhất một trong ba thứ trên thì đánh dấu "mồ côi" để tôi quyết giữ hay bỏ.
```
