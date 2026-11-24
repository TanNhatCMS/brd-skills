# BRD Template

Mẫu khung BRD dùng cho mọi dự án. Cấu trúc 16 mục + Appendix theo BRD mẫu BRD-CAM-001 (Customer Address Management, Retail Banking). Xóa mục không dùng, nhưng đừng đổi thứ tự các mục còn lại.

Điền Document Control ở đầu mỗi BRD: Document ID, Version/status, Project/domain, Prepared by, Date, Classification.

---

## 1. Executive Summary

2–3 đoạn ngắn: tình hình hiện tại, vấn đề, đề xuất làm gì, và quyết định kinh doanh đang cần ai phê duyệt. Không đi sâu chi tiết kỹ thuật. Kết thúc bằng câu: giải pháp chi tiết vẫn cần architecture, privacy và regulatory review.

## 2. Business Problem and Opportunity

Bảng 2 cột:

| Current pain point | Business consequence |
|---|---|
| ... | ... |

Mỗi pain point một dòng. Cột hậu quả viết bằng ngôn ngữ kinh doanh (trải nghiệm khách hàng, chi phí, rủi ro tuân thủ), không viết bằng ngôn ngữ kỹ thuật.

## 3. Objectives and Success Measures

| ID | Objective | Illustrative measure / target |
|---|---|---|
| OBJ-01 | ... | ... |

Mỗi objective gắn một measure đo được (%, thời gian, số lượng) và mốc thời gian. Thêm measurement note: target là proposed hypothesis cho tới khi Operations/Technology baseline hiệu năng hiện tại và xác nhận target khả thi trước sign-off.

## 4. Stakeholders and Governance

| Role | Accountability |
|---|---|
| Business Sponsor — ... | Owns expected outcomes, funding decision, and business acceptance |
| Product Owner — ... | Prioritizes capabilities and resolves business policy questions |
| Compliance / Privacy | Reviews retention, authorization, consent, and audit obligations |
| Operations (nơi nghiệp vụ chạy) | Validates workflows, exception handling, and training |
| Technology / Data Architecture | Assesses feasible integration patterns and system ownership |
| QA / UAT Lead | Defines test approach and coordinates business acceptance evidence |

## 5. Scope

### 5.1 In Scope

Liệt kê những gì dự án làm — theo động từ nghiệp vụ (initiation, verification, update, notification, distribution, exceptions, retry, reconciliation, status inquiry, audit reporting).

### 5.2 Out of Scope

Liệt kê rõ những gì KHÔNG làm, để tránh scope creep. Ví dụ: legal name changes, contact-number/email updates, thay vendor, historical data cleansing.

### 5.3 Boundaries and Dependencies

Hệ thống/quy trình/policy nào dự án phụ thuộc vào. Ghi rõ: final integration mechanisms are not prescribed by this BRD (BRD nói "cái gì", không nói "làm thế nào").

## 6. AS-IS Process

Mô tả quy trình hiện tại bằng danh sách bước đánh số (5–7 bước là đủ). Mỗi bước một câu. Kết thúc bằng điểm đau lớn nhất của quy trình hiện tại.

## 7. TO-BE Process

Mô tả quy trình mục tiêu bằng danh sách bước đánh số, theo đúng thứ tự xảy ra: initiate → validate → confirm → commit → distribute → exception handling → status/audit visibility.

## 8. Business Requirements

| ID / priority | Business requirement | Business rationale / acceptance evidence |
|---|---|---|
| BR-001 / Must | The bank shall ... | ... |

Quy tắc:

- Viết theo mẫu "The [actor] shall [hành động] [điều kiện] [kết quả]"
- Priority: Must / Should / Could
- Cột acceptance evidence phải trả lời được: kiểm chứng yêu cầu này bằng cách nào?
- Mỗi requirement trace về ít nhất một Objective (mục 3)

## 9. Business Rules

| Rule ID | Rule / decision logic | Owner / status |
|---|---|---|
| RULE-01 | ... | ... / proposed / open |

Business rules là logic quyết định, khác với requirements: rule nói "trong tình huống X thì áp dụng Y". Ví dụ: ordering khi có 2 request trùng nhau, retention/masking dữ liệu, downstream failure có reverse master record không.

## 10. Non-Functional Business Expectations

| Category | Expected outcome / validation need |
|---|---|
| Availability | ... |
| Security | ... |
| Performance | ... (business target, technical decomposition pending) |
| Resilience | ... |
| Accessibility | ... |
| Privacy | ... |

Viết ở mức business expectation, không viết chi tiết kỹ thuật (không SLA số cụ thể nếu chưa chốt — ghi "to be agreed").

## 11. Exceptions and Edge Cases

| Scenario | Required business outcome |
|---|---|
| ... | ... |

Liệt kê tối thiểu: invalid input, duplicate submission, partial failure (master ok, consumer fail), concurrent changes, multiple products/linked profiles, cancel before confirmation.

## 12. Data Requirements (Business Level)

| Data element | Business meaning / validation |
|---|---|
| ... | ... |

Chỉ liệt kê data element ở mức nghiệp vụ (identifier, type, fields, effective date, request ID/channel/actor/timestamps, delivery status). Không viết schema kỹ thuật.

## 13. Dependencies, Assumptions, Risks

| Type / ID | Description | Response / owner |
|---|---|---|
| Dependency D-01 | ... | ... |
| Assumption A-01 | ... | Validate with ...; otherwise revise scope. |
| Risk R-01 | ... | ... |

Mỗi assumption phải có cách validate và hệ quả nếu sai. Mỗi risk phải có response và owner cụ thể.

## 14. Traceability Matrix (Extract)

| Business goal | Requirement IDs | Evidence / proposed UAT scenario |
|---|---|---|
| OBJ-01 | BR-001, BR-002, BR-003 | UAT-01 ...; UAT-02 ... |
| ... | ... | ... |

Mọi Objective phải có ít nhất một Requirement. Mọi Requirement phải thuộc ít nhất một Objective. Requirement nào "mồ côi" thì hỏi lại hoặc loại bỏ.

## 15. Open Questions and Clarifications

| ID / priority | Question | Decision owner |
|---|---|---|
| Q-01 / High | ... | Product Owner |

Câu hỏi từ bước 4 (phân tích lỗ hổng) đổ vào đây. BRD không được lên baseline khi còn câu hỏi High chưa trả lời.

## 16. Acceptance and Approval Approach

Liệt kê điều kiện để BRD chuyển từ draft sang approved baseline, ví dụ:

(a) high-priority open questions resolved; (b) scope và success measures approved; (c) requirements traceable to agreed goals and evidence; (d) Privacy, Operations, Architecture, Product đã review phần việc của mình; (e) change control established cho requirement mới/thay đổi.

Bảng chữ ký: Business Sponsor, Product Owner, Operations Lead, Technology Lead, Privacy/Compliance — Name/signature + Date/status (Pending/Approved).

## Appendix A. Source and Evidence Register (Sample)

| Source ID | Expected source artifact | Availability |
|---|---|---|
| SRC-01 | ... | Provided / Not provided — validate |

Mọi requirement phải truy được về một source. Thêm traceability disclaimer: requirements trong tài liệu này là ví dụ minh họa, không phải facts thu thập từ dự án thật — cho tới khi source register được điền đầy đủ.
