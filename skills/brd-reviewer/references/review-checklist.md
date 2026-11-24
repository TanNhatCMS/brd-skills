# Review Checklist — Soát nhanh BRD trước khi gửi stakeholder

Checklist 5 phút. Mục nào chưa đạt thì đánh dấu và quay lại sửa trước khi gửi. Dùng kèm với `review-prompt.md` khi cần review sâu.

## Cấu trúc

- [ ] Đủ 16 mục + Appendix A (theo `brd-template.md`)
- [ ] Document Control điền đầy đủ (ID, version, ngày, người viết, classification)
- [ ] Không có mục nào chỉ có tiêu đề mà không có nội dung

## Yêu cầu (mục 8)

- [ ] Mỗi requirement có ID duy nhất (BR-001...) và mức Must/Should/Could
- [ ] Viết theo mẫu "The [actor] shall..." — có actor rõ ràng
- [ ] Mỗi requirement có rationale + acceptance evidence
- [ ] Không có từ mơ hồ chưa định nghĩa (nhanh, đầy đủ, khi cần, hợp lý)
- [ ] Không có số liệu bịa — target chưa baseline thì ghi rõ là proposed hypothesis

## Truy vết

- [ ] Mọi requirement trace về ít nhất một Objective (mục 14)
- [ ] Mọi Objective có ít nhất một requirement
- [ ] Mọi requirement truy được về nguồn (Appendix A)
- [ ] Không còn requirement "mồ côi"

## Nhất quán

- [ ] Thuật ngữ dùng thống nhất xuyên suốt
- [ ] Số liệu mục 3 khớp mục 10 (ví dụ: 95% trong 5 phút)
- [ ] AS-IS và TO-BE không mâu thuẫn
- [ ] Không có requirement nào mâu thuẫn Business Rule

## Ngoại lệ & rủi ro

- [ ] Đủ 6 nhóm exception cơ bản (invalid input, duplicate, partial failure, concurrent changes, multiple products, cancel)
- [ ] Mỗi risk có response + owner
- [ ] Mỗi assumption có cách validate + hệ quả nếu sai
- [ ] Open Questions High đều có decision owner

## Privacy & compliance

- [ ] Yêu cầu chạm PII đều có privacy control (masking, retention, least-privilege)
- [ ] Audit log không lưu dữ liệu nhạy cảm dạng không che
- [ ] Notification không gửi dữ liệu nhạy cảm qua kênh chưa phê duyệt

## Chốt

- [ ] Đã chạy review bằng phiên mới (skill `brd-reviewer`), không tự review trong phiên viết
- [ ] Không còn lỗi Critical nào chưa sửa
- [ ] Bảng chữ ký mục 16 đã gửi đúng người phê duyệt
