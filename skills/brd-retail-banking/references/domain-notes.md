# Domain Notes — Retail Banking (cho BRD)

Ghi chú domain dùng khi viết hoặc review BRD ngân hàng bán lẻ. Nội dung rút ra từ BRD mẫu BRD-CAM-001 (Customer Address Management Modernization) và thực tế vận hành phổ biến. Mọi con số trong BRD mẫu đều là illustrative — không dùng làm fact cho dự án thật.

## 1. Customer master record

- Là hồ sơ khách hàng chính, nguồn duy nhất (single source of truth) cho thông tin khách hàng: định danh, địa chỉ, thông tin liên hệ, trạng thái.
- Mọi thay đổi phải commit vào master trước, rồi mới phân phối xuống downstream.
- Không hệ thống downstream nào được tự ý ghi đè master. Muốn sửa dữ liệu master thì phải đi qua quy trình đổi thông tin có kiểm soát (request → validate → confirm → commit).
- Giả định A-01 trong BRD mẫu: "an authoritative customer master exists for the supported products" — nếu thực tế không có master thống nhất thì phải revise scope, không được viết BRD như thể nó đã tồn tại.

## 2. Downstream consumers

Các hệ thống nhận dữ liệu từ master, ví dụ:

| Nhóm | Ví dụ |
|---|---|
| Core banking | Tài khoản, số dư, giao dịch |
| Cards | Thẻ ghi nợ/tín dụng, địa chỉ gửi thẻ/sao kê |
| Loans | Khoản vay, địa chỉ liên hệ thu hồi nợ |
| Statements & communications | Sao kê, thư, email, SMS |
| Collections | Thu hồi nợ quá hạn |
| CRM / Marketing | Hồ sơ khách hàng, chiến dịch |

- Mỗi consumer có delivery state riêng: pending / delivered / failed / reconciled, kèm reason code chuẩn.
- Failed delivery không được "biến mất lặng lẽ" — phải có retry và reconciliation trail, trạng thái hiển thị là partial distribution.
- Dependency D-01: cần approved inventory + ownership của toàn bộ downstream consumers trước design baseline. Không có inventory này thì không biết phân phối cho ai.

## 3. Address types & effective date

- **Address types:** residential (nơi ở), mailing (nhận thư), hoặc phân loại khác theo nghiệp vụ. Một khách hàng có thể có nhiều địa chỉ cùng lúc, mỗi type một địa chỉ hiệu lực.
- **Effective date:** ngày địa chỉ bắt đầu có hiệu lực. Có 3 trường hợp cần rule rõ ràng:
  - Ngày hiện tại (mặc định)
  - Future-dated (địa chỉ mới có hiệu lực từ ngày sau)
  - Backdated correction (sửa sai ngày trong quá khứ) — rule cho backdating là open question (Q-02 trong BRD mẫu), phải do Retail Operations quyết.
- **Country/postal format:** mỗi quốc gia có format riêng (postal code, bắt buộc/tùy chọn của từng field như unit number, region). Validate theo country-specific format trước khi accept (BR-002).

## 4. Channels

| Channel | Đặc điểm |
|---|---|
| Branch (quầy) | Nhân viên thao tác, khách hàng xuất trình giấy tờ; xác thực mạnh nhất |
| Contact centre (tổng đài) | Agent thao tác theo yêu cầu qua điện thoại; xác thực qua câu hỏi bảo mật |
| Digital (app/web) | Khách hàng tự phục vụ; xác thực bằng đăng nhập + OTP/biometrics |

- Cả ba kênh tuân cùng một bộ rule (validation, confirm, audit) — khác nhau chỉ ở cách xác thực và giao diện.
- BRD mẫu nêu rõ: thay đổi có thể được nhập lại ở nhiều hệ thống (re-keying) là nguyên nhân gốc của dữ liệu không nhất quán — TO-BE process loại bỏ re-keying bằng cách commit một lần vào master rồi phân phối.

## 5. Audit trail

- Ghi lại: actor (ai), timestamp (khi nào), channel (qua kênh nào), previous/new address (giá trị cũ/mới), decision (quyết định gì), request ID.
- Audit history là bất biến (immutable): không ai được sửa lịch sử, kể cả admin. Chỉ role được phê duyệt mới đọc được.
- Retention và masking của old/new address tuân theo approved policy (RULE-04) — không lưu PII dạng không che quá thời hạn cho phép.
- Cancel trước confirm cũng phải capture event theo audit policy (không commit nhưng vẫn log).

## 6. Notification

- Khi address change được accept, gửi thông báo cho khách hàng qua kênh theo communication preferences đã đăng ký (SMS, email, thư).
- Kênh bị hạn chế hoặc không gửi được thì tuân theo policy (ví dụ: fallback sang kênh khác hoặc ghi lại là undeliverable).
- Việc đã gửi (hoặc không gửi được) phải được ghi lại — notification là một phần của audit evidence, không phải việc phụ.
- Notification không được chứa dữ liệu nhạy cảm vượt quá mức cần thiết (data minimization).

## 7. Privacy & compliance

- Dữ liệu địa chỉ là PII. Mọi yêu cầu chạm tới PII phải kèm control: least-privilege access, encryption in transit + at rest, masking, retention.
- Compliance/Privacy review retention, authorization, consent và audit obligations trước khi BRD được baseline.
- Risk R-03: notification hoặc audit design có thể lộ dữ liệu cá nhân không cần thiết → privacy review trước implementation.
- Solution design luôn subject to architecture, privacy, and regulatory review — BRD không tự quyết thay các bên này.

## 8. Các lỗi domain thường gặp khi viết BRD ngân hàng

1. Viết requirement cho phép downstream ghi trực tiếp vào master (sai nguyên tắc single source of truth).
2. Quên xử lý partial failure: chỉ viết happy path, không viết khi consumer fail thì sao.
3. Không có rule ordering cho concurrent changes → dữ liệu cũ ghi đè dữ liệu mới.
4. Duplicate submission tạo duplicate outcome.
5. Target số liệu viết như fact trong khi chưa có baseline.
6. Audit log thiết kế lưu full PII không masking.
7. Notification gửi qua kênh khách hàng không đăng ký, hoặc gửi kèm dữ liệu nhạy cảm.
8. Scope không loại trừ rõ: legal name change, contact-number/email update, joint-account owner — những thứ này là quy trình khác, không thuộc address change.
