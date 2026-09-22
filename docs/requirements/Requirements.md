# Software Requirements Specification (SRS): SauceDemo Web Application

## 1. Purpose & Scope
This document specifies the observable functional and interface requirements for the SauceDemo e-commerce web application ([https://www.saucedemo.com/](https://www.saucedemo.com/)). Every requirement outlined herein is derived strictly from verified, demonstrable behaviors of the application and forms the contractual baseline for test scenarios, test cases, and future automated checks.

---

## 2. Module Requirements

### Module 1: User Authentication (Login & Session)
- **REQ-LOG-01 (Successful Login):**
  The system shall authenticate a user upon receiving valid credentials (e.g., `standard_user` with password `secret_sauce`) and navigate the browser to the inventory catalog (`/inventory.html`).
- **REQ-LOG-02 (Locked Out Account):**
  The system shall deny authentication to accounts marked as locked (`locked_out_user`) and display the explicit error notification: `Epic sadface: Sorry, this user has been locked out.`
- **REQ-LOG-03 (Invalid Credentials):**
  The system shall reject authentication attempts with unrecognized usernames or incorrect passwords and display the error message: `Epic sadface: Username and password do not match any user in this service` accompanied by red error indicator icons on input fields.
- **REQ-LOG-04 (Empty Field Validations):**
  - Submitting without entering a username shall trigger the message: `Epic sadface: Username is required`.
  - Submitting a valid username with an empty password field shall trigger: `Epic sadface: Password is required`.
- **REQ-LOG-05 (Error Dismissal):**
  The system shall allow the user to dismiss any active login error banner by clicking the error dismissal button (`X`).
- **REQ-LOG-06 (User Logout):**
  The system shall terminate the active session when the user opens the side navigation menu and clicks `Logout`, returning the browser directly to the root login page (`/`).
- **REQ-LOG-07 (Unauthorized Route Protection):**
  The system shall prevent direct unauthenticated access to internal routes (such as `/inventory.html` or `/cart.html`) and redirect unauthenticated requests back to the login interface with an appropriate access warning.

---

### Module 2: Product Catalog & Item Display
- **REQ-PRD-01 (Catalog Rendering):**
  Upon successful login, the inventory page shall render exactly six (6) distinct merchandise cards, each displaying an item thumbnail image, title hyperlink, description body, and formatted dollar price (`$XX.YY`).
- **REQ-PRD-02 (Item Detail Navigation):**
  Clicking on either a product title link or product image shall navigate the user to that item's individual detail page (`/inventory-item.html?id=X`) displaying an enlarged image, full description, price, and cart action button.
- **REQ-PRD-03 (Back to Products Navigation):**
  On the product detail page, clicking `Back to products` shall return the user to the main inventory catalog without losing current session state.
- **REQ-PRD-04 (Add to Cart Action):**
  Clicking `Add to cart` on any product card shall immediately switch the button state to `Remove` and increment the shopping cart header badge count by 1.
- **REQ-PRD-05 (Remove from Catalog Action):**
  Clicking `Remove` on an already-selected product card shall switch the button label back to `Add to cart` and decrement the shopping cart header badge accordingly. If no items remain, the badge shall be removed from view.

---

### Module 3: Product Sorting
- **REQ-SRT-01 (Default Sort State):**
  The inventory view shall default to `Name (A to Z)` sorting order upon initial load.
- **REQ-SRT-02 (Alphabetic Ascending Sort):**
  Selecting `Name (A to Z)` from the sort dropdown container shall arrange all inventory cards in ascending alphabetical order by their title.
- **REQ-SRT-03 (Alphabetic Descending Sort):**
  Selecting `Name (Z to A)` from the sort dropdown container shall rearrange all inventory cards in reverse alphabetical order by title.
- **REQ-SRT-04 (Price Ascending Sort):**
  Selecting `Price (low to high)` from the sort dropdown container shall arrange inventory cards in ascending order of unit price (from lowest to highest).
- **REQ-SRT-05 (Price Descending Sort):**
  Selecting `Price (high to low)` from the sort dropdown container shall arrange inventory cards in descending order of unit price (from highest to lowest).
- **REQ-SRT-06 (Active Sort Label Reflection):**
  The visible active label in the custom dropdown container shall dynamically reflect the currently chosen sort criteria at all times.

---

### Module 4: Shopping Cart Management
- **REQ-CRT-01 (Cart Page Navigation):**
  Clicking the shopping cart icon located in the global header shall direct the user to the cart summary page (`/cart.html`).
- **REQ-CRT-02 (Cart Item Representation):**
  Each item added to the cart shall be displayed with a quantity column (`QTY`), product title hyperlink, description snippet, unit price, and an inline `Remove` button.
- **REQ-CRT-03 (Inline Cart Item Removal):**
  Clicking `Remove` adjacent to any cart item shall immediately delete that line item from the cart list and update the global header cart counter badge in real time.
- **REQ-CRT-04 (Continue Shopping Flow):**
  Clicking `Continue Shopping` within the cart view shall navigate the user back to `/inventory.html`, retaining all remaining items in the cart.
- **REQ-CRT-05 (Cart State Persistence):**
  Items added to the cart shall remain stored across browser refreshes and inter-page navigation within the active session.
- **REQ-CRT-06 (Proceed to Checkout):**
  Clicking `Checkout` from the cart view shall navigate the user to the first checkout phase (`/checkout-step-one.html`).

---

### Module 5: Checkout Information (Step One)
- **REQ-COI-01 (Form Fields Presentation):**
  The checkout step one screen shall present three mandatory user input fields: `First Name`, `Last Name`, and `Zip/Postal Code`.
- **REQ-COI-02 (First Name Required):**
  Submitting the form with an empty `First Name` shall display the validation message: `Error: First Name is required`.
- **REQ-COI-03 (Last Name Required):**
  Submitting with a populated `First Name` but empty `Last Name` shall display: `Error: Last Name is required`.
- **REQ-COI-04 (Postal Code Required):**
  Submitting with valid first and last names but an empty `Zip/Postal Code` shall display: `Error: Postal Code is required`.
- **REQ-COI-05 (Cancel Checkout Step One):**
  Clicking `Cancel` shall abort the checkout sequence and return the user to the cart page (`/cart.html`) with cart contents preserved.
- **REQ-COI-06 (Proceed to Step Two):**
  Providing valid entries in all three fields and clicking `Continue` shall navigate the user to the order overview screen (`/checkout-step-two.html`).

---

### Module 6: Checkout Overview (Step Two)
- **REQ-COO-01 (Item Summary Inspection):**
  The checkout overview screen shall list all items currently staged for purchase, including quantity, item name, and item price.
- **REQ-COO-02 (Payment & Shipping Attribution):**
  The overview shall display static fulfillment details:
  - Payment Information: `SauceCard #31337`
  - Shipping Information: `Free Pony Express Delivery!`
- **REQ-COO-03 (Subtotal Price Calculation):**
  The displayed `Item total:` shall equal the exact arithmetic sum of individual unit prices of all items in the cart.
- **REQ-COO-04 (Tax Computation):**
  The displayed `Tax:` shall reflect the application's calculated sales tax (approx. 8% rounded to two decimal places).
- **REQ-COO-05 (Order Grand Total):**
  The displayed `Total:` shall strictly equal the sum of `Item total` and `Tax`.
- **REQ-COO-06 (Cancel Checkout Step Two):**
  Clicking `Cancel` on Step Two shall abort the transaction and redirect the user back to the primary inventory page (`/inventory.html`).
- **REQ-COO-07 (Finish Order Execution):**
  Clicking `Finish` shall commit the transaction and advance the browser to the order completion screen (`/checkout-complete.html`).

---

### Module 7: Order Completion
- **REQ-ORD-01 (Order Confirmation Display):**
  Upon order completion, the page shall render a primary header `Checkout: Complete!` along with a green circular dispatch icon and the heading `Thank you for your order!`.
- **REQ-ORD-02 (Dispatch Notice):**
  The page shall display the order dispatch message: `Your order has been dispatched, and will arrive just as fast as the pony can get there!`.
- **REQ-ORD-03 (Cart Reset on Completion):**
  Following order completion, the shopping cart shall be fully emptied and the header cart badge counter shall be cleared.
- **REQ-ORD-04 (Return to Catalog Navigation):**
  Clicking the `Back Home` button shall redirect the user back to `/inventory.html` with an empty cart and refreshed catalog state.
