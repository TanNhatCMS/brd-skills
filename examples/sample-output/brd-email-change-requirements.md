# Sample Output — Business Requirements (mục 8) cho tính năng đổi địa chỉ email

*File này được tạo bằng skill `brd-writer` trong repo (test prompt eval #1) để chứng minh skill chạy được end-to-end. Nội dung là ví dụ minh họa cách viết, không phải BRD thật.*

**Brief đầu vào:** Khách hàng ngân hàng bán lẻ hiện phải ra quầy hoặc gọi tổng đài để đổi email; nhân viên nhập lại ở nhiều hệ thống gây sai lệch, thư/sao kê gửi nhầm địa chỉ cũ. Mục tiêu: cho khách tự đổi email trên app, validate định dạng, xác nhận qua OTP, cập nhật master record rồi phân phối xuống core banking, cards, CRM.

**Objectives giả định (để trace):** OBJ-01 giảm thời gian đổi email; OBJ-02 cải thiện nhất quán dữ liệu; OBJ-03 tăng kiểm soát và bằng chứng audit.

---

## 8. Business Requirements

| ID / priority | Business requirement | Business rationale / acceptance evidence |
|---|---|---|
| BR-001 / Must | The bank shall allow an authenticated customer to submit an email-change request for their own profile through the mobile app. | Eligible customer + authenticated session produces a request; unauthenticated or staff-initiated requests for another customer's email are rejected and logged. |
| BR-002 / Must | The bank shall validate the email format and domain deliverability before accepting a change. | Invalid or undeliverable addresses receive an actionable error message without changing the master record. |
| BR-003 / Must | The bank shall require OTP confirmation to the new email address before committing the change. | Change commits only after the customer proves control of the new address; unconfirmed requests expire and leave the current email unchanged. |
| BR-004 / Must | The bank shall preserve an immutable audit history of submitted email changes, outcomes, actors, timestamps, and previous/new values, subject to approved privacy controls. | Approved roles can retrieve the request audit trail without modifying historical events. |
| BR-005 / Must | The bank shall distribute accepted email changes to the approved downstream consumer inventory (core banking, cards, CRM) and record delivery outcome by consumer. | Each consumer has a trackable delivery state; failed delivery does not silently disappear. |
| BR-006 / Must | The bank shall provide authorized users with request-level status and reason codes for pending, completed, and exception states. | Authorized users can distinguish master-record completion from downstream distribution status. |
| BR-007 / Should | The bank shall issue a customer notification to the previous email address when an email change is accepted. | Notification is recorded; a notification to the old address alerts the customer if the change was not theirs. |

## Traceability (trích)

| Business goal | Requirement IDs |
|---|---|
| OBJ-01 | BR-001, BR-002, BR-003 |
| OBJ-02 | BR-005 |
| OBJ-03 | BR-004, BR-006, BR-007 |
