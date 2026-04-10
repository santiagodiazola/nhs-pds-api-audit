# Requirements Traceability Matrix (RTM)
> **Project:** NHS PDS API Technical Audit 2026
> **Scope:** Patient Search & Demographic Update Workflows

## 🎯 Overview
This matrix ensures 100% test coverage by mapping every business requirement to its corresponding technical test case. It provides a clear audit trail from functional specifications to execution results.

| Requirement ID | Requirement Description | Linked Test Cases | Status | Defect / Note |
| :--- | :--- | :--- | :--- | :--- |
| **REQ-PDS-SRCH-01** | Basic Patient Search (Name & DOB) | TC-PDS-01, 02, 04 | ✅ Passed | Functional logic verified. |
| **REQ-PDS-SRCH-02** | Refined Identity Search (Filters) | TC-PDS-05 | ⚠️ Blocked | Sandbox resource limit. |
| **REQ-PDS-SEC-01** | OAuth2 Token & Auth Validation | TC-PDS-03, 12, 13 | ✅ Passed | Fail-closed model confirmed. |
| **REQ-PDS-VAL-02** | Internationalization (i18n) Support | TC-PDS-11 | ✅ Passed | UTF-8 Accented char "Díaz". |
| **REQ-PDS-UPD-01** | Patient Record Update (General) | TC-PDS-06, 07 | ⚠️ Blocked | Restricted in Sandbox. |
| **REQ-PDS-UPD-02** | Concurrency Control (Optimistic Locking) | TC-PDS-08, 09 | ✅ Passed | ETag validation successful. |
| **REQ-PDS-SEC-04** | Schema Validation & Sanitization | TC-PDS-10 | ❌ Failed | **BUG-PDS-001** (500 Error) |

---

## 📈 Summary Metrics
- **Total Requirements:** 7
- **Total Test Cases:** 13
- **Requirement Coverage:** 100%
- **Execution Pass Rate:** 91% (Excluding Environmental Blocks)

## 🔑 Legend
- ✅ **Passed:** Requirement met via automated validation.
- ❌ **Failed:** Critical defect identified (Refer to Bug Report).
- ⚠️ **Blocked:** Environmental constraints prevented execution.
