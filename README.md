# NHS PDS API - Technical Audit & Automation
> **Project Goal:** To validate the resilience, security, and data integrity of the National Health Service (NHS) Patient Demographic Service.

## 📊 Executive Summary
This comprehensive audit evaluated the UK’s "Golden Record" system for patient data. The suite validates HL7 FHIR R4 compliance and security authorization scopes across 13 high-priority scenarios.

---

### 📊 Project Execution Metrics
| Category | Metric | Test Cases |
| :--- | :--- | :--- |
| **Total Test Cases** | 13 | TC-PDS-01 to TC-PDS-13 |
| **Passed** | 10 | Positive, i18n, & Security |
| **Failed** | 1 | TC-PDS-10 (Critical 500 Error) |
| **Blocked** | 2 | TC-PDS-05, TC-PDS-06 (Sandbox Limit) |
| **Pass Rate** | **91%** | (Excluding blocked cases) |

---

## 🚦 Release Readiness Recommendation

**Summary:** The core demographic search modules are stable; however, a critical blocking issue in the Update module prevents a full production release.

* **Search & Discovery: PROCEED** - 91% stability across core identity retrieval.
  - Robust i18n support confirmed (successful UTF-8 parsing for accented characters).
* **Patient Updates: HALT** - **Blocking Issue:** BUG-PDS-001 (500 Internal Server Error).
  - **Risk:** High risk of server-side instability and potential Denial of Service (DoS) if malformed JSON is processed.
  - **Requirement:** Remediate validation middleware before deployment to the Production environment.

---

## 🏗️ Architectural Framework: Environment-Driven Automation
This suite utilizes a **Decoupled Architecture** to ensure security, portability, and enterprise-grade maintainability.

* **Collection-Level Inheritance:** All 13 test cases inherit authorization from the Parent Collection, centralizing security logic.
* **Dynamic Traceability:** The `X-Request-ID` is managed via the `{{api_key}}` variable, which injects a dynamic `{{$guid}}` at runtime. This ensures 100% unique traceability per transaction.
* **Data Isolation:** Strictly separates Test Logic (Collection) from Test Data (Environments).

---

### 🔴 Critical Security Finding: BUG-PDS-001
- **Classification:** Unhandled Parser Exception (CWE-20: Improper Input Validation).
- **Vulnerability:** Lack of input sanitization on the `PATCH /Patient` endpoint triggers a server crash (500) rather than a graceful 400-level rejection.
- **Business Risk:** High risk of service denial in high-traffic clinical environments.
- **Recommendation:** Implement pre-parsing validation middleware to enforce strict RFC 6902 compliance.
- *See [BUG-PDS-001_Evidence.png](/evidence/BUG-PDS-001_Evidence.png) for the full server response log.*

---

## 🛠️ Technical Implementation
- **Automation:** Postman + JavaScript (pm.test assertions).
- **Execution:** 13 Automated Test Cases (91% Pass Rate).
- **Tooling:** Jira for bug tracking, Notion for the Master Test Plan.

---

## 🧪 Key Test Scenarios
- **TC-PDS-01:** Positive Patient Retrieval (Success 200).
- **TC-PDS-11:** i18n Compliance (Search with accented characters like "Díaz").
- **TC-PDS-12/13:** OAuth2 Scope & Token Integrity Validation.

---

## 🚀 How to Run this Suite
1.  **Download:** Save both JSON files (the Collection and the Environment) from the `/postman` folder.
2.  **Import:** In Postman, click the **Import** button and drag both files in.
3.  **Select Environment:** In the top-right corner, click the environment dropdown and select **"NHS - Sandbox Copy."**
4.  **Verify Variables (Optional):** Click the **Environment Quick Look** icon (the eye icon 👁️). You should see:
    * **base_url:** `https://sandbox.api.service.nhs.uk/personal-demographics/FHIR/R4`
    * **nhs_number:** `9000000009`
    * **api_key:** `{{$guid}}`
5.  **Execute:**
    * Open the **Collection Runner** (bottom right of the Postman window).
    * Select the **NHS PDS Audit** collection.
    * Click **Run NHS PDS Audit**.

---

## 📁 Project Artifacts

* **Documentation:** [Full Master Test Plan & Bug Reports (Notion)](https://www.notion.so/Project-Audit-NHS-Personal-Demographics-Service-PDS-32af1e8fc465809eb8f0d1e88b0ee85a)
* **Project Management:** Managed via Jira (See [Sprint Execution Evidence](/evidence/Jira_Sprint_Board.png))

---
> **QA Lead Note:** This audit focuses on **Systemic Resilience**. Beyond functional verification, it validates how the API behaves under non-standard conditions to protect clinical data integrity.
