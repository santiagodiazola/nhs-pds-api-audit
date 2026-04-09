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

* **Documentation:** [Full Master Test Plan & Bug Reports (Notion)](https://www.notion.so/Project-Audit-NHS-Personal-Demographics-Service-PDS-32af1e8fc465809eb8fb0d1e88b0ee85a?source=copy_link)
* **Project Management:** Managed via Jira (See [Sprint Execution Evidence](/evidence/Jira_Sprint_Board.png))

## 🚀 How to Run this Suite
1. **Import** the collection and environment files from the `/postman` folder into Postman.
2. **Configure** your NHS API Key in the environment variables.
3. **Run** the collection using the Postman Collection Runner.

