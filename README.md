# NHS PDS API - Technical Audit & Automation
> **Project Goal:** To validate the resilience, security, and data integrity of the National Health Service (NHS) Patient Demographic Service.

## 📊 Executive Summary
This audit covered 13 high-priority test cases across 4 Agile sprints. The suite validates FHIR R4 compliance and security authorization scopes.

### 📊 Project Execution Metrics
| Category | Metric | Test Cases |
| :--- | :--- | :--- |
| **Total Test Cases** | 13 | TC-PDS-01 to TC-PDS-13 |
| **Passed** | 10 | Positive, i18n, & Security |
| **Failed** | 1 | TC-PDS-10 (Critical 500 Error) |
| **Blocked** | 2 | TC-PDS-05, TC-PDS-06 (Sandbox Limit) |
| **Pass Rate** | **91%** | (Excluding blocked cases) |

## 🚦 Release Readiness Recommendation

**Summary:** The core demographic search modules are stable; however, a critical blocking issue in the Update module prevents a full production release.

* **Search & Discovery: PROCEED** - 91% stability across core identity retrieval.
  - Robust i18n support confirmed (successful UTF-8 parsing for accented characters).
* **Patient Updates: HALT** - **Blocking Issue:** BUG-PDS-001 (500 Internal Server Error).
  - **Risk:** High risk of server-side instability and potential Denial of Service (DoS) if malformed JSON is processed.
  - **Requirement:** Remediate validation middleware before deployment to the Production environment.
 
## 🛠️ Local Setup & Environment Variables

To execute this test suite in your own Postman instance, you must import the environment template provided in this repository.

### 🔑 Required Variables
| Variable | Description | Value |
| :--- | :--- | :--- |
| `base_url` | NHS Sandbox Entry Point | `https://sandbox.api.service.nhs.uk` |
| `nhs_number` | Test Patient Identifier | `9000000009` |
| `api_key` | Your Sandbox Credentials | `[Your API Key]` |

### 🚀 Instructions
1. Download the `NHS_Sandbox.template.postman_environment.json` from the `/postman` folder.
2. Import it into Postman (**File > Import**).
3. Update the `api_key` variable in the **Current Value** column with your NHS Sandbox key.

### 🔴 Critical Security Finding: BUG-PDS-001
- **Vulnerability:** Unhandled 500 Internal Server Error.
- **Root Cause:** Lack of input sanitization on the PATCH /Patient endpoint during malformed JSON injection.
- **Business Risk:** Potential for Service Denial (DoS) in a clinical environment.
- *See [BUG-PDS-001_Evidence.png](/evidence/BUG-PDS-001_Evidence.png) for the full server response log.*

## 🛠️ Technical Implementation
- **Automation:** Postman + JavaScript (pm.test assertions).
- **Execution:** 13 Automated Test Cases (91% Pass Rate).
- **Tooling:** Jira for bug tracking, Notion for the Master Test Plan.

## 🧪 Key Test Scenarios
- **TC-PDS-01:** Positive Patient Retrieval (Success 200).
- **TC-PDS-11:** i18n Compliance (Search with accented characters like "Díaz").
- **TC-PDS-12/13:** OAuth2 Scope & Token Integrity Validation.

## 📁 Project Artifacts

* **Documentation:** [Full Master Test Plan & Bug Reports (Notion)](https://www.notion.so/Project-Audit-NHS-Personal-Demographics-Service-PDS-32af1e8fc465809eb8f0d1e88b0ee85a)
* **Project Management:** Managed via Jira (See [Sprint Execution Evidence](/evidence/Jira_Sprint_Board.png))

## 🚀 How to Run this Suite
1. **Import** the collection and environment files from the `/postman` folder into Postman.
2. **Configure** your NHS API Key in the environment variables.
3. **Run** the collection using the Postman Collection Runner.

