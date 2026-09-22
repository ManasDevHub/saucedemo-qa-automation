# Master Test Plan: SauceDemo Web Application

## 1. Document Control
- **Project:** SauceDemo QA Automation & Portfolio
- **Application Under Test:** [SauceDemo E-Commerce](https://www.saucedemo.com/)
- **Author:** QA Automation Engineer
- **Document Version:** 1.0.0
- **Status:** Draft / Ready for Manual Execution
- **Last Updated:** September 2026

---

## 2. Introduction & Objective
The objective of this test plan is to establish a rigorous, industry-standard quality assurance strategy for the SauceDemo web application. SauceDemo serves as an e-commerce platform demonstrating modern storefront behaviors, customer purchase funnels, catalog filtering, shopping cart state management, and multi-step checkout workflows.

This document defines the scope of testing, validation techniques, environmental parameters, entry and exit criteria, risk management measures, and the multi-phase roadmap guiding this project from manual verification through test automation.

> **Note on Project Phase:**
> This test plan represents Phase 1 (Documentation and Manual Verification Baseline). Automation test scripts (Playwright/Pytest) and automated CI/CD pipeline executions will be designed, implemented, and linked in subsequent phases following manual validation.

---

## 3. Application Under Test (AUT)
- **Application Name:** SauceDemo (Swag Labs)
- **URL:** [https://www.saucedemo.com/](https://www.saucedemo.com/)
- **Architecture:** Client-side Single Page Application (React-based) interacting with session-driven state and simulated back-end logic.
- **Primary Business Functions:**
  - Customer authentication and role-based validation.
  - Product catalog navigation and detail inspection.
  - Dynamic product sorting (alphabetic and price-based).
  - Item addition, removal, and persistent cart badge tracking.
  - Multi-tier checkout process: Customer information capture, order overview reconciliation, and confirmation dispatch.

---

## 4. Scope of Testing

### 4.1 In Scope (Functional & Behavioral)
The testing activities cover end-to-end user journeys and individual component validations across the following 7 core modules:

1. **Login Module:**
   - Valid credential authentication for standard users.
   - Authentication prevention for locked-out accounts.
   - Field validations (empty username, empty password, missing both).
   - Invalid credential handling and user-facing error message verification.
   - Session persistence and explicit logout behavior via the burger menu.

2. **Products (Catalog & Inventory) Module:**
   - Accurate rendering of product cards (image, item title, item description, and price).
   - "Add to cart" toggle interaction and dynamic transformation to "Remove".
   - Header shopping cart counter badge synchronization.
   - Navigation to detailed item view (`/inventory-item.html`) and return navigation.

3. **Product Sorting Module:**
   - Default sorting state verification (`Name (A to Z)`).
   - Alphabetic reverse sorting (`Name (Z to A)`).
   - Numeric ascending price sorting (`Price (low to high)`).
   - Numeric descending price sorting (`Price (high to low)`).
   - UI consistency of the active sort selector label upon selection.

4. **Cart Module:**
   - Item row representation inside the shopping cart (`/cart.html`): Quantity, Item Name, Description, and Unit Price.
   - Direct item removal from within the cart view and badge count decrement.
   - Navigation continuity via "Continue Shopping".
   - Progression into checkout via "Checkout".
   - Cart persistence across page reloads and back/forward browser navigation.

5. **Checkout Information Module (Step One):**
   - User detail capture (`First Name`, `Last Name`, `Zip/Postal Code`).
   - Field-level mandatory validation (empty first name, empty last name, empty postal code).
   - Navigation controls: "Cancel" button redirection back to cart.
   - Successful transition to Checkout Overview upon entering valid information.

6. **Checkout Overview Module (Step Two):**
   - Line item review (item title, quantity, price).
   - Verification of static order metadata: Payment Information (SauceCard identifier), Shipping Information (Pony Express).
   - Financial calculation verification: Subtotal (sum of individual item prices), Tax calculation, and Total price.
   - Navigation controls: "Cancel" button redirection back to products inventory.
   - Order finalization via "Finish".

7. **Order Completion Module:**
   - Confirmation screen presentation (`Checkout: Complete!`).
   - Verification of dispatch messaging ("Thank you for your order!").
   - Verification that the shopping cart is flushed and the badge is cleared upon completion.
   - "Back Home" navigation routing back to the primary inventory view.

### 4.2 Out of Scope
The following areas are explicitly excluded from this phase of testing:
- **Backend Infrastructure / API Mocking:** Directly querying server databases or modifying third-party CDN endpoints.
- **Payment Gateway Processing:** Live credit card transactions or third-party processor integration (SauceDemo utilizes simulated payment identifiers).
- **Cross-site Penetration / Security Vulnerability Testing:** DDoS attacks, SQL injection, or malicious server exploitation.
- **Load and Stress Testing:** Concurrent multi-thousand user load simulations.
- **Localization / Multi-language Support:** Testing in languages other than English (the application does not offer multi-locale switching).

---

## 5. Testing Types & Methodologies
- **Manual Functional Testing:** Verification of discrete business flows, positive user paths, and negative error conditions against documented specifications.
- **Black-Box Testing:** Testing strictly against user-accessible interface controls without relying on internal code modification.
- **Exploratory Testing:** Scenario-driven exploration to identify layout quirks, session discrepancies, and boundary-handling limitations.
- **UI & Layout Verification:** Alignment, typography, image rendering, and button state integrity across desktop screen resolutions.
- **Regression Testing (Future Phase):** Planned automated test suites running via Playwright to ensure zero regressions across releases.

---

## 6. Test Environment & Platform Matrix

### 6.1 Hardware & Operating System
- **Operating System:** Windows 11 / Windows Server environments
- **Display Resolution:** 1920 x 1080 (Primary Desktop Target)

### 6.2 Browser Matrix
| Browser | Engine | Target Version | Mode |
| :--- | :--- | :--- | :--- |
| Google Chrome | Chromium | Latest Stable | Desktop (1920x1080) |
| Mozilla Firefox | Gecko | Latest Stable | Desktop (1920x1080) |
| Microsoft Edge | Chromium | Latest Stable | Desktop (1920x1080) |

---

## 7. Entry & Exit Criteria

### 7.1 Entry Criteria
1. The target application ([https://www.saucedemo.com/](https://www.saucedemo.com/)) is reachable and operational.
2. Requirements specification (`Requirements.md`) and Test Scenarios (`Test_Scenarios.xlsx`) are established and peer-reviewed.
3. Test Cases (`Test_Cases.xlsx`) with unambiguous steps, preconditions, and expected outcomes are authored.
4. Bug reporting workbook and module-specific evidence repositories are configured.

### 7.2 Exit Criteria
1. 100% of authored functional test cases have been manually executed.
2. All identified anomalies or defects are formally logged in `Bug_Report.xlsx` with reproducible steps and supporting visual evidence.
3. Traceability matrix (`RTM.xlsx`) is fully updated reflecting executed test coverage.
4. No unresolved Critical (Blocker) defects remain unanalyzed.
5. Test Execution Summary is documented, signaling readiness for Phase 2 (Playwright test automation).

---

## 8. Defect Severity & Priority Classification

### Severity Levels
- **Critical (S1):** Complete disruption of core workflow (e.g., inability to log in, crash on checkout submission, total cart failure).
- **Major (S2):** Significant feature failure without an intuitive workaround (e.g., sorting calculation misplacement, tax computation error).
- **Minor (S3):** Non-critical operational inconsistency or localized UI defect (e.g., incorrect error message grammar, image ratio distortion).
- **Trivial (S4):** Minor visual polish or cosmetic discrepancies that do not affect functionality.

### Priority Levels
- **High (P1):** Must be addressed or retested immediately before further progression.
- **Medium (P2):** Essential fix required within the current testing cycle.
- **Low (P3):** Desirable fix; can be addressed in subsequent iterations.

---

## 9. Risk Assessment & Mitigation

| Risk | Impact | Probability | Mitigation Strategy |
| :--- | :--- | :--- | :--- |
| Application state resets unexpectedly during testing | Medium | Low | Maintain discrete, atomic test cases that authenticate and initialize their own prerequisites. |
| Third-party asset downtime (images hosted externally) | High | Low | Validate whether broken assets are network-induced or inherent to the test user persona (e.g., `problem_user`). |
| Discrepancies between browser rendering engines | Low | Medium | Cross-browser sanity sweeps across Chromium, Gecko, and WebKit engines. |
| Over-reliance on synthetic assumptions | High | Low | Ground all requirements solely on observable, demonstrable system behaviors. |

---

## 10. Assumptions & Dependencies
- The application under test is maintained as a stable reference platform by Sauce Labs.
- Publicly documented test accounts (`standard_user`, `locked_out_user`, `problem_user`, etc.) remain active with uniform passwords (`secret_sauce`).
- Network connectivity remains stable during manual and automated execution runs.
