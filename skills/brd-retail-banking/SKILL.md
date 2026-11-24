---
name: brd-retail-banking
description: Kiến thức domain Retail Banking (ngân hàng bán lẻ) để viết BRD — customer master, đổi địa chỉ khách hàng, downstream distribution, audit trail, notification preferences, privacy/PII, kênh giao dịch (branch, contact centre, digital). Dùng skill này whenever the user writes or reviews a BRD about retail banking, ngân hàng bán lẻ, customer address change, tài khoản, thẻ, khoản vay, tiền gửi, KYC, hoặc nhắc tới master record, downstream consumer, audit trail trong ngữ cảnh ngân hàng.
---

# brd-retail-banking — Domain Retail Banking cho BRD

Skill này cung cấp kiến thức domain để skill `brd-writer` viết BRD ngân hàng bán lẻ cho sát thực tế, và để `brd-reviewer` soi lỗi domain (ví dụ: requirement nào vi phạm nguyên tắc "master record là nguồn duy nhất", trường hợp nào quên xử lý downstream failure).

## Khi nào dùng

- BRD thuộc domain Retail Banking: tài khoản, thẻ, khoản vay, tiền gửi, dịch vụ khách hàng
- Tính năng liên quan tới hồ sơ khách hàng: đổi địa chỉ, đổi tên, cập nhật thông tin liên hệ, KYC
- Yêu cầu nhắc tới master record, downstream systems/consumers, audit trail, notification
- Review BRD ngân hàng: kiểm tra xem requirement có đúng thực tế vận hành ngân hàng không

## Khái niệm cốt lõi

Đọc `references/domain-notes.md` để lấy chi tiết. Tóm tắt:

- **Customer master record** — hồ sơ khách hàng chính, nguồn duy nhất (single source of truth) cho thông tin khách hàng. Mọi thay đổi phải commit vào master trước, rồi mới phân phối xuống downstream. Không hệ thống downstream nào được tự ý ghi đè master.
- **Downstream consumers** — các hệ thống nhận dữ liệu từ master: core banking, CRM, cards, loans, statements, collections, marketing. Mỗi consumer có delivery state riêng: pending / delivered / failed / reconciled.
- **Address types** — residential (nơi ở), mailing (nhận thư), và các loại theo nghiệp vụ. Một khách hàng có thể có nhiều địa chỉ, mỗi loại một địa chỉ hiệu lực.
- **Effective date** — ngày địa chỉ bắt đầu có hiệu lực. Có thể là ngày tương lai (future-dated) hoặc backdated correction — rule cho backdating phải được Product Owner quyết, không tự mặc định.
- **Audit trail** — lịch sử bất biến: ai làm, khi nào, qua kênh nào, giá trị cũ/mới, quyết định gì. Chỉ role được phép mới đọc được, không ai được sửa lịch sử.
- **Channels** — branch (quầy), contact centre (tổng đài), digital (app/web tự phục vụ). Mỗi kênh có mức xác thực khác nhau và đều phải tuân cùng một bộ rule.
- **Notification preferences** — khách hàng chọn kênh nhận thông báo (SMS, email, thư). Kênh bị hạn chế hoặc không gửi được thì tuân theo policy, và việc đã gửi (hoặc không gửi được) phải được ghi lại.

## Quy tắc domain hay bị viết sai trong BRD

1. **Downstream failure không reverse master record.** Master commit thành công mà consumer fail thì trạng thái là "partial distribution", phải retry/reconcile — không được tự động rollback master trừ khi có policy riêng được phê duyệt (RULE-05 trong BRD mẫu).
2. **Thứ tự thay đổi (ordering) quan trọng hơn nội dung.** Hai lần đổi địa chỉ gửi gần nhau: phải giữ đúng sequence đã phê duyệt, không để dữ liệu cũ ghi đè dữ liệu mới. Đây là risk R-02, cần ordering contract + UAT replay/order.
3. **Duplicate submission không tạo duplicate outcome.** Gửi trùng thì trả về request đã có hoặc xử lý tương đương một cách an toàn — không tạo 2 lần đổi địa chỉ.
4. **Cancel trước confirm thì không commit gì cả**, nhưng event cancel vẫn phải ghi log theo audit policy.
5. **Số liệu target là hypothesis cho tới khi có baseline.** Ví dụ "95% trong 5 phút" chỉ là proposed target — Operations/Technology phải baseline hiệu năng hiện tại trước sign-off. Đừng viết target như fact.
6. **Privacy là requirement, không phải ghi chú.** Yêu cầu nào chạm PII phải kèm control: masking, retention, least-privilege, consent. Audit log lưu old/new address phải tuân policy retention/masking (RULE-04).

## Tài liệu tham khảo

- `references/domain-notes.md` — ghi chú domain chi tiết (master record, downstream, channels, audit, notification, privacy)
- `references/glossary.md` — thuật ngữ Anh–Việt
- BRD mẫu đầy đủ: `../brd-writer/references/retail-banking-address-change-brd.md` (BRD-CAM-001)
