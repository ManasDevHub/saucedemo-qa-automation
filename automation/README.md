# Test Automation Framework (Playwright & Pytest)

This directory is designated for the automated end-to-end testing suite to be built in Phase 2 of this project.

## Architecture Blueprint (Phase 2)
The automation framework will be engineered using:
- **Language:** Python (3.11+)
- **Test Runner & Assertions:** `pytest`
- **Automation Driver:** `playwright` (Python asynchronous/synchronous API)
- **Design Pattern:** Page Object Model (POM) separating locator strategies and page actions from test assertions
- **Reporting:** Allure Framework & Pytest HTML Reports
- **Configuration Management:** Centralized test parameters, environment base URLs, and timeout settings via `pytest.ini` and environment configuration files.

## Planned Directory Structure
```
automation/
├── pages/                  # Page Object Model classes
│   ├── base_page.py
│   ├── login_page.py
│   ├── inventory_page.py
│   ├── cart_page.py
│   ├── checkout_page.py
│   └── completion_page.py
├── tests/                  # Test suites mapped to Test_Cases.xlsx
│   ├── conftest.py         # Pytest fixtures and browser context setup
│   ├── test_login.py
│   ├── test_inventory.py
│   ├── test_sorting.py
│   ├── test_cart.py
│   └── test_checkout.py
├── utils/                  # Reusable utilities (data loaders, helpers)
└── pytest.ini              # Pytest configuration and CLI options
```

*Note: In strict compliance with the Phase 1 milestone, no test scripts or automation code are generated until manual test verification and defect logging are completed.*
