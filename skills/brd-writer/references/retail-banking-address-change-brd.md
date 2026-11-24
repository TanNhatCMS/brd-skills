# Business Requirements Document

## Customer Address Management Modernization

| Document control | Detail |
|---|---|
| Document ID | BRD-CAM-001 |
| Version / status | 1.0 / Draft for stakeholder validation |
| Project / domain | Customer Address Management / Retail Banking |
| Prepared by | Business Analysis Team (illustrative) |
| Date | 20 November 2026 |
| Classification | Fictional sample for training; not approved requirements |

Purpose: demonstrate a professionally structured BRD with traceable, reviewable business requirements, business rules, measures, and approval gates. All entities, data, thresholds, and targets are illustrative.

*Source: full PDF "BRD Retail Banking" (BRD-CAM-001), shared via Google Drive 2026-11-24. This file is the complete transcription of that PDF — sections 1–16 plus Appendix A. The earlier screenshot transcription (sections 1, 2, 3, 8, 11, 12, 13, 14) matches this document verbatim.*

---

## 1. Executive Summary

The bank currently receives customer address changes through branch staff and contact-centre agents. Changes can be re-entered across customer and product systems, creating delays, inconsistent records, avoidable rework, and customer complaints. This initiative proposes a governed address-maintenance process across assisted and digital channels.

Business decision requested: approve a consistent address-change capability with validation, auditability, downstream distribution, exception handling, and measurable service targets. Solution design remains subject to architecture, privacy, and regulatory review.

## 2. Business Problem and Opportunity

| Current pain point | Business consequence |
|---|---|
| Multiple entry points without common rules | Inconsistent customer experience and policy application |
| Manual re-keying or delayed downstream updates | Data inconsistency and returned communications |
| Limited status visibility | Repeat calls and uncertain resolution |
| Incomplete standardized audit evidence | Higher operational and compliance review effort |

## 3. Objectives and Success Measures

| ID | Objective | Illustrative measure / target |
|---|---|---|
| OBJ-01 | Reduce address-update turnaround time | 95% of eligible updates reflected in the master customer record within 5 minutes after acceptance |
| OBJ-02 | Improve record consistency | 99.5% downstream delivery within 30 minutes, excluding approved maintenance windows |
| OBJ-03 | Improve control and evidence | 100% of change requests have actor, timestamp, previous/new address, decision, and channel logged |
| OBJ-04 | Reduce handling effort | 25% reduction in address-change-related follow-up contacts within 90 days of rollout |

Measurement note: targets are proposed hypotheses. Operations and technology owners must baseline current performance and confirm achievable targets before sign-off.

## 4. Stakeholders and Governance

| Role | Accountability |
|---|---|
| Business Sponsor — Retail Operations | Owns expected outcomes, funding decision, and business acceptance |
| Product Owner — Customer Servicing | Prioritizes capabilities and resolves business policy questions |
| Compliance / Privacy | Reviews retention, authorization, consent, and audit obligations |
| Customer Service / Branch Operations | Validates assisted-channel workflows, exception handling, and training |
| Technology / Data Architecture | Assesses feasible integration patterns and system ownership |
| QA / UAT Lead | Defines test approach and coordinates business acceptance evidence |

## 5. Scope

### 5.1 In Scope

Address-change initiation by authenticated customers and authorized staff; address verification and policy checks; capture of effective dates; master customer record update; notification to registered channels; controlled distribution to approved downstream systems; exceptions, retry, reconciliation, status inquiry, and audit reporting.

### 5.2 Out of Scope

Legal name changes; contact-number and email updates; changes to third-party or joint-account owners without separate authorization; replacement of postal delivery vendors; historical address cleansing beyond necessary migration or correction controls.

### 5.3 Boundaries and Dependencies

Dependent on customer identity and access management, existing customer master ownership, address reference/validation capability, downstream interface inventories, data retention policy, and channel release readiness. Final integration mechanisms are not prescribed by this BRD.

## 6. AS-IS Process

1. Customer requests an address change through an agent or branch.
2. Staff authenticate and collect address details.
3. Address information is entered into one or more servicing systems.
4. Some downstream systems are updated through periodic or manual procedures.
5. Staff cannot consistently see delivery status or the reason for downstream failure.

## 7. TO-BE Process

1. Authorized customer or staff member initiates a change.
2. System validates mandatory fields, country/postal format, and applicable business policy.
3. Customer confirms the proposed address and effective date.
4. The authorized master record is updated and a unique request reference is assigned.
5. Changes are delivered to subscribed downstream systems.
6. Failures enter monitored exception handling.
7. Customer and staff can view a clear request status and audit history as permitted.

## 8. Business Requirements

| ID / priority | Business requirement | Business rationale / acceptance evidence |
|---|---|---|
| BR-001 / Must | The bank shall allow an authenticated customer or authorized employee to submit an address-change request for eligible customer profiles. | Eligible actor and profile combinations produce a request; unauthorized combinations are rejected and logged. |
| BR-002 / Must | The bank shall validate mandatory address elements and applicable country-specific formats before accepting a change. | Invalid or missing inputs receive actionable error messages without changing the master record. |
| BR-003 / Must | The bank shall present the proposed normalized address and effective date for confirmation before committing the change. | Confirmation shows material fields; cancellation leaves the current address unchanged. |
| BR-004 / Must | The bank shall preserve an immutable audit history of submitted changes, outcomes, actors, timestamps, and material previous/new values, subject to approved privacy controls. | Approved roles can retrieve the request audit trail without modifying historical events. |
| BR-005 / Must | The bank shall distribute accepted address changes to the approved downstream consumer inventory and record delivery outcome by consumer. | Each consumer has a trackable delivery state; failed delivery does not silently disappear. |
| BR-006 / Must | The bank shall provide authorized users with request-level status and reason codes for pending, completed, and exception states. | Authorized users can distinguish master-record completion from downstream distribution status. |
| BR-007 / Must | The bank shall detect and manage duplicate, out-of-order, and failed distribution events without unintended overwrites. | Replay and retry scenarios preserve the latest authorized address and create exception evidence. |
| BR-008 / Should | The bank shall issue a customer notification when an address change is accepted, using approved communication preferences. | Notification is recorded; restricted or undeliverable channels follow policy. |

## 9. Business Rules

| Rule ID | Rule / decision logic | Owner / status |
|---|---|---|
| RULE-01 | Only authenticated customers for their own eligible profile, or staff with approved entitlements, may initiate a change. | Identity & Access / proposed |
| RULE-02 | Address changes must pass required field and country-specific format checks; external address enrichment must not alter customer intent without confirmation. | Operations / proposed |
| RULE-03 | Where competing effective-dated requests exist, the bank must apply an agreed ordering and conflict-resolution policy. | Product Owner / open |
| RULE-04 | The permitted retention and masking of old/new address values in audit history must follow approved policy. | Privacy / open |
| RULE-05 | A downstream failure does not reverse a successfully committed master record unless a separately approved policy requires it. | Architecture & Ops / proposed |

## 10. Non-Functional Business Expectations

| Category | Expected outcome / validation need |
|---|---|
| Availability | Channel and master-record update availability must align with approved servicing service levels; exact SLA to be agreed. |
| Security | Least-privilege access, encryption in transit and at rest, and controlled access to personal data. |
| Performance | Business target: 95% accepted requests update the master record within 5 minutes; technical decomposition pending. |
| Resilience | Failures must be observable, recoverable, and reconciled without lost or duplicated business outcomes. |
| Accessibility | Customer-facing experiences must follow the bank approved accessibility standard. |
| Privacy | Data minimization, retention, and lawful use must be approved by Privacy/Legal. |

## 11. Exceptions and Edge Cases

| Scenario | Required business outcome |
|---|---|
| Invalid postal code or missing unit number | Reject or prompt correction per local policy; show specific reason. |
| Duplicate submission | Return existing or safely process equivalent request without duplicate outcomes. |
| Master record succeeds; consumer fails | Show partial distribution state; retain retry and reconciliation trail. |
| Two changes submitted close together | Preserve approved sequence and prevent older data overwriting newer data. |
| Customer has multiple products / linked profiles | Apply confirmed address scope and account-level exceptions. |
| Customer cancels before confirmation | Do not commit; capture event consistent with audit policy. |

## 12. Data Requirements (Business Level)

| Data element | Business meaning / validation |
|---|---|
| Customer identifier | Stable key linking the change to the correct person/profile; access restricted. |
| Address type | Residential, mailing, or other supported business classification. |
| Country / postal code / lines / city / region | Validated fields based on applicable address convention and mandatory-field rules. |
| Effective date | Date on which the address is intended to become applicable; backdating rule open. |
| Request ID / channel / actor / timestamps | Evidence of initiation, confirmation, commit, and distribution. |
| Delivery status by consumer | Pending / delivered / failed / reconciled, with standard reason codes. |

## 13. Dependencies, Assumptions, Risks

| Type / ID | Description | Response / owner |
|---|---|---|
| Dependency D-01 | Approved inventory and ownership of all downstream address consumers. | Data Architecture to confirm before design baseline. |
| Assumption A-01 | An authoritative customer master exists for the supported products. | Validate with Architecture; otherwise revise scope. |
| Risk R-01 | Inconsistent address policies across product lines may create conflicts. | Run policy alignment workshop; Product Owner owns decisions. |
| Risk R-02 | Incorrect event ordering could overwrite a more recent address. | Define ordering contract and reconciliation UAT cases. |
| Risk R-03 | Notification or audit design could expose unnecessary personal data. | Privacy review before implementation. |

## 14. Traceability Matrix (Extract)

| Business goal | Requirement IDs | Evidence / proposed UAT scenario |
|---|---|---|
| OBJ-01 | BR-001, BR-002, BR-003 | UAT-01 successful self-service; UAT-02 invalid address; turnaround metric |
| OBJ-02 | BR-005, BR-007 | UAT-03 consumer failure and recovery; UAT-04 replay/order |
| OBJ-03 | BR-004, BR-006 | UAT-05 audit retrieval by entitled role; UAT-06 status visibility |
| OBJ-04 | BR-006, BR-008 | UAT-07 status inquiry; UAT-08 notification behavior |

## 15. Open Questions and Clarifications

| ID / priority | Question | Decision owner |
|---|---|---|
| Q-01 / High | Which customer types, products, jurisdictions and address categories are eligible for phase one? | Product Owner |
| Q-02 / High | What is the policy for concurrent changes, future dates, and backdated corrections? | Retail Operations |
| Q-03 / High | What is the authoritative record for each address category and product? | Data Architecture |
| Q-04 / High | Which consumers require real-time versus scheduled delivery, and what are the agreed SLAs? | Technology & Consumer Owners |
| Q-05 / High | What audit retention, data masking, and notification rules are mandatory? | Privacy & Compliance |

## 16. Acceptance and Approval Approach

The BRD may move from draft to approved baseline only when: (a) high-priority open questions are resolved; (b) the scope and success measures are approved; (c) business requirements are traceable to agreed goals and evidence; (d) Privacy, Operations, Architecture, and Product have reviewed their respective obligations; and (e) change control is established for new or altered requirements.

| Approver role | Name / signature | Date / status |
|---|---|---|
| Business Sponsor | _______________________ | Pending |
| Product Owner | _______________________ | Pending |
| Operations Lead | _______________________ | Pending |
| Technology Lead | _______________________ | Pending |
| Privacy / Compliance | _______________________ | Pending |

## Appendix A. Source and Evidence Register (Sample)

| Source ID | Expected source artifact | Availability |
|---|---|---|
| SRC-01 | Stakeholder workshop notes and approved decisions | Not provided — validate |
| SRC-02 | Current servicing procedure and exception guide | Not provided — validate |
| SRC-03 | Customer master and downstream interface inventory | Not provided — validate |
| SRC-04 | Privacy, security, and record-retention policy | Not provided — validate |

Traceability disclaimer: all requirements in this document are example requirements, not facts elicited from a real project. The source register illustrates what evidence must be attached before final approval.
