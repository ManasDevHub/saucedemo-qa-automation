# SauceDemo QA Automation Portfolio

A comprehensive, industry-standard Quality Assurance portfolio project demonstrating end-to-end testing methodologies, test governance, requirement traceability, and structured defect reporting for the [SauceDemo](https://www.saucedemo.com/) e-commerce web platform.

---

## 📌 Project Overview
This repository showcases the complete software quality assurance lifecycle, establishing a structured testing methodology before proceeding to automation engineering. Rather than jumping straight into writing script code, this project follows an authentic QA progression:

```
┌─────────────────┐     ┌──────────────────────┐     ┌───────────────────────┐
│ Manual Testing  │ ──> │  Test Documentation  │ ──> │ Defect Identification │
└─────────────────┘     └──────────────────────┘     └───────────────────────┘
                                                                 │
┌─────────────────┐     ┌──────────────────────┐                 │
│      CI/CD      │ <── │ Automated Reporting  │ <── Playwright Automation
└─────────────────┘     └──────────────────────┘
```

The current milestone focuses on **Phase 1: Test Governance, Documentation, and Manual Verification**. In this phase, test scenarios, detailed test cases, requirements specifications, test data matrices, and traceability mappings are fully established. Manual test execution and genuine defect discovery are performed directly against the live application before automated test suites (Python + Playwright + Pytest) are implemented.

---

## 🎯 Application Under Test (AUT)
- **Application:** SauceDemo (Swag Labs Storefront)
- **Target URL:** [https://www.saucedemo.com/](https://www.saucedemo.com/)
- **Technology Stack:** Single Page Application (React) simulating real-world e-commerce retail workflows.

---

## 🔍 Testing Scope & Primary Modules
Testing covers positive business paths, negative validations, edge cases, and user session continuity across seven (7) primary modules:

1. **Login Module:** Authentication flows for standard and restricted user personas, invalid credential handling, mandatory field validations, error dismissal, and secure session termination (logout).
2. **Products Module:** Storefront catalog rendering (item images, titles, descriptions, pricing), dynamic toggle between "Add to cart" and "Remove", and item detail page navigation.
3. **Product Sorting Module:** Catalog re-ordering across all available sorting criteria: Name (A to Z), Name (Z to A), Price (low to high), and Price (high to low).
4. **Cart Module:** Item inspection within the shopping cart, quantity display, item deletion directly from cart, cart persistence across sessions, and continuation flows.
5. **Checkout Information Module (Step 1):** Customer information intake (First Name, Last Name, Zip/Postal Code), field-level boundary validations, and checkout cancellation.
6. **Checkout Overview Module (Step 2):** Line item verification, static fulfillment metadata (Payment Information, Shipping Method), arithmetic verification of subtotal, tax calculation, and grand total.
7. **Order Completion Module:** Order confirmation validation, dispatch messaging, confirmation that the shopping cart is flushed, and return-to-inventory navigation.

---

## 🛠️ QA Approach & Methodology
- **Specification-Based Testing:** All test cases are derived directly from observable requirements documented in [`docs/requirements/Requirements.md`](docs/requirements/Requirements.md).
- **Equivalence Partitioning & Boundary Value Analysis:** Applied to input fields (authentication inputs, postal code formatting, name fields).
- **State Transition Testing:** Validating shopping cart state and button toggle behavior as items transition between inventory, cart, overview, and completion states.
- **Requirement Traceability:** End-to-end bi-directional traceability maintained in [`docs/rtm/RTM.xlsx`](docs/rtm/RTM.xlsx) linking Requirements ➔ Scenarios ➔ Test Cases ➔ Automation IDs ➔ Execution Status ➔ Defects.
- **Defect Integrity:** Zero synthetic or fictitious bug reports. Defects will be formally documented only upon manual discovery during active exploratory and functional testing.

---

## 📁 Repository Structure
```text
saucedemo-qa-automation/
│
├── README.md                           # Project overview, methodology, and execution roadmap
│
├── docs/                               # Core QA artifacts and test governance
│   ├── test-plan/
│   │   └── Test_Plan.md                # Comprehensive IEEE 829-aligned Master Test Plan
│   ├── test-scenarios/
│   │   └── Test_Scenarios.xlsx         # High-level operational scenarios across all modules
│   ├── test-cases/
│   │   └── Test_Cases.xlsx             # Detailed step-by-step test cases with expected results
│   ├── requirements/
│   │   └── Requirements.md             # Verifiable functional requirements specification
│   └── rtm/
│       └── RTM.xlsx                    # Requirement Traceability Matrix
│
├── defects/                            # Defect logging and tracking infrastructure
│   ├── Bug_Report.xlsx                 # Defect tracking register (populated during manual testing)
│   ├── Login/                          # Module-specific defect reports & reproductions
│   │   └── README.md
│   ├── Products/
│   │   └── README.md
│   ├── Product-Sorting/
│   │   └── README.md
│   ├── Cart/
│   │   └── README.md
│   ├── Checkout-Information/
│   │   └── README.md
│   ├── Checkout-Overview/
│   │   └── README.md
│   └── Order-Completion/
│       └── README.md
│
├── screenshots/                        # Visual proof and failure evidence repositories
│   ├── Login/
│   ├── Products/
│   ├── Product-Sorting/
│   ├── Cart/
│   ├── Checkout-Information/
│   ├── Checkout-Overview/
│   └── Order-Completion/
│
├── test-data/
│   └── Test_Data.xlsx                  # Standardized test data profiles and user credentials
│
├── test-results/
│   └── README.md                       # Execution summaries and test run artifacts
│
├── automation/
│   └── README.md                       # Blueprint for upcoming Playwright/Pytest framework
│
├── .github/
│   └── workflows/
│       └── README.md                   # Blueprint for upcoming CI/CD pipeline
│
├── .gitignore                          # Git ignore rules for Python, IDEs, and artifacts
└── LICENSE                             # Repository license
```

---

## 📋 Manual Testing & Defect Management Workflow
1. **Execution:** The tester executes each scenario in [`docs/test-cases/Test_Cases.xlsx`](docs/test-cases/Test_Cases.xlsx) against `https://www.saucedemo.com/`.
2. **Result Capture:** Once executed, the `Actual Result` is populated and `Status` is transitioned from `Not Executed` to `Pass` or `Fail`.
3. **Defect Filing:** If an anomaly is identified:
   - Log the defect details in [`defects/Bug_Report.xlsx`](defects/Bug_Report.xlsx) with severity, priority, environment, and reproduction steps.
   - Author a dedicated defect markdown report in `defects/<Module>/BUG-[ID]-[title].md`.
   - Save screenshots/recordings in `screenshots/<Module>/BUG-[ID].png`.
   - Link the `Bug ID` back into `Test_Cases.xlsx` and `RTM.xlsx`.

---

## 🚀 Roadmap: Future Automation & CI/CD
- **Phase 2 — Playwright & Pytest Automation Framework:**
  - Implementation of Page Object Model (POM) architecture under `automation/pages/`.
  - Development of robust automated regression suites under `automation/tests/`.
  - Dynamic test data fixtures, cross-browser support (Chromium, Firefox, WebKit), and parallel test execution via `pytest-xdist`.
  - Rich test execution reporting using Allure Framework.
- **Phase 3 — Continuous Integration & Quality Gates:**
  - Automated test triggers via GitHub Actions on every Pull Request.
  - Automated artifact retention (trace files, failure videos, logs).
  - Automated deployment of test reports to GitHub Pages.

---

## 📄 License
This project is open-source and available under the terms of the [MIT License](LICENSE).
