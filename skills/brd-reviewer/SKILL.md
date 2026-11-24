---
name: brd-reviewer
description: Kiểm duyệt bản nháp BRD bằng AI — đóng vai người phản biện để soi lỗi completeness, consistency, ambiguity, testability, traceability trước khi gửi stakeholder. Dùng skill này whenever the user asks to review, check, critique, validate, or audit a BRD draft, tài liệu yêu cầu nghiệp vụ, hoặc nói "soi lỗi", "review giúp", "BRD này đã đủ tốt chưa" — kể cả khi họ không gọi tên skill.
---

# brd-reviewer — Kiểm duyệt BRD bằng AI

Skill này thực hiện **Bước 6** trong quy trình 7 bước viết BRD: tạo một lớp kiểm duyệt bằng AI.

## Nguyên tắc quan trọng nhất

- **Review trong phiên mới.** Người review không được là người (hay phiên) đã viết bản nháp. Nếu đang ở cùng phiên đã viết BRD, nói rõ với người dùng: mở phiên mới, dán bản nháp vào, rồi chạy lại skill này.
- **Chỉ指出 lỗi, không tự sửa.** Nhiệm vụ của reviewer là tìm lỗi và đề xuất sửa — bản nháp chỉ được sửa sau khi người dùng (hoặc BA) quyết định từng finding.
- **Mọi finding phải có evidence.** Không nói chung chung kiểu "BRD này chưa rõ ràng". Phải chỉ rõ: mục nào, dòng nào, câu nào, và vì sao đó là lỗi.

## Cách review

Dùng prompt kiểm duyệt đầy đủ trong `references/review-prompt.md`. Tóm tắt 7 nhóm kiểm tra:

1. **Completeness (đầy đủ)** — còn thiếu mục nào trong 16 mục chuẩn? Mục nào chỉ có tiêu đề mà không có nội dung? Open Questions High nào chưa có owner?
2. **Consistency (nhất quán)** — thuật ngữ có dùng thống nhất không? Số liệu ở mục 3 có khớp với mục 10 không? AS-IS và TO-BE có mâu thuẫn không?
3. **Clarity / Ambiguity (rõ ràng)** — yêu cầu nào có từ mơ hồ ("nhanh", "đầy đủ", "khi cần", "hợp lý") mà không định nghĩa? Ai là actor của yêu cầu này?
4. **Testability (kiểm thử được)** — mỗi requirement có acceptance evidence cụ thể không? Có đo được không? UAT nào kiểm chứng nó?
5. **Traceability (truy vết được)** — mỗi requirement có trace về Objective không? Có trace về nguồn tài liệu không? Requirement nào "mồ côi"?
6. **Feasibility / Risk (khả thi)** — assumption nào chưa validate mà cả BRD đang dựa vào? Risk nào chưa có response/owner? Dependency nào chưa có owner xác nhận?
7. **Privacy / Compliance (riêng tư & tuân thủ)** — yêu cầu nào chạm tới dữ liệu cá nhân mà chưa có privacy control? Audit log có lưu dữ liệu nhạy cảm không che không?

## Output — báo cáo review

Trả về theo đúng format này:

```markdown
## BRD Review Report — [tên BRD, version]

Verdict: [APPROVED / APPROVED WITH COMMENTS / NEEDS REVISION]
Tóm tắt 2–3 câu: bản nháp đang ở mức nào, lỗi nặng nhất là gì.

### Critical (phải sửa trước khi gửi stakeholder)
| # | Mục | Finding | Evidence (trích dẫn) | Gợi ý sửa |
|---|---|---|---|---|

### Major (nên sửa)
| # | Mục | Finding | Evidence | Gợi ý sửa |
|---|---|---|---|---|

### Minor (sửa nếu có thời gian)
| # | Mục | Finding | Evidence | Gợi ý sửa |
|---|---|---|---|---|

### Điểm tốt (giữ lại)
- ...

### Câu hỏi cần stakeholder trả lời
- ...
```

Quy tắc severity:

- **Critical** — lỗi làm BRD không dùng được: requirement mâu thuẫn nhau, thiếu mục bắt buộc, số liệu bịa không ghi rõ là hypothesis, yêu cầu chạm PII nhưng không có privacy control
- **Major** — lỗi làm BRD khó dùng: yêu cầu mơ hồ không test được, thiếu traceability, assumption chưa validate mà BRD dựa vào
- **Minor** — lỗi trình bày: thuật ngữ không thống nhất, lỗi chính tả, format bảng lệch

Nếu không tìm ra lỗi Critical nào thì nói rõ "không tìm thấy lỗi Critical" — không bịa lỗi cho đủ số lượng.

## Tài liệu tham khảo

- `references/review-prompt.md` — prompt kiểm duyệt đầy đủ, dùng được cho mọi AI (copy-paste sang ChatGPT/Claude/Antigravity đều được)
- `references/review-checklist.md` — checklist soát nhanh trước khi gửi stakeholder
- BRD mẫu để đối chiếu: `../brd-writer/references/retail-banking-address-change-brd.md`
