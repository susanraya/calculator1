# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-TECHSTACK · approved · source: requirements:tech-stack

Product owner approved a fixed technology stack for calculator1: FastAPI backend, AWS cloud, PostgreSQL database, React frontend. Design must use exactly these components without substitution.

Requirements version 1, delivery scope 'lightweight'. Approved stack and rationale as stated: (1) Backend: FastAPI 0.115 — serves static application files only; no business logic runs server-side since all maths happens in the browser and nothing is stored; kept as platform default. (2) Cloud: AWS — hosts the responsive web app for general users across India, using CloudFront edge locations for fast loads near Indian users; since no personal data is stored there, no DPDP residency constraints apply; covers free anonymous use at any traffic level. (3) Database: PostgreSQL 16 — named only as platform default; nothing is persisted (no accounts, no history, no personal data) so the database slot is unused unless a future feature (e.g., calculation history, currently out of scope) requires it. (4) Frontend: React 19 — implements the on-screen keypad plus physical keyboard input, responsive layout for phone and desktop, and the focus handling/contrast needed for RPwD/WCAG accessibility basics; all calculation logic runs client-side.

**Related:** EPIC-001, EPIC-002, EPIC-003, EPIC-004

- ⚠ Stack is approved but no architecture artifact exists yet that maps these components into an actual component/deployment design.

### REQ-SCOPE · draft · source: requirements:scope

Defines what calculator1 will and will not do: basic arithmetic, percentage, clear/reset, dual input methods, responsive/accessible UI, and open/free/anonymous access, explicitly excluding scientific, financial, and history/memory features.

In scope: addition, subtraction, multiplication, division, percentage calculation, clear/reset, on-screen tap keypad, physical keyboard entry, responsive mobile/desktop layout, accessibility basics (keyboard navigation, visible focus, readable contrast), anonymous no-sign-in use, free use with no billing, and client-side-only computation with nothing stored or transmitted. Out of scope: scientific functions (powers, roots, trig, logs), financial calculators (EMI/loan/tax), and calculation history/memory.

**Related:** EPIC-001, EPIC-002, EPIC-003, EPIC-004

### EPIC-001 · draft · source: requirements:EPIC-001

Core arithmetic epic: addition, subtraction, multiplication, division, percentage, clear/reset, and chaining calculations from a prior result, all computed client-side.

US-001 [critical]: add/subtract/multiply/divide (AC-001: 12+8=20; AC-002: 20-5=15; AC-003: 6×7=42; AC-004: 9÷3=3). US-002 [high]: division by zero must show a non-crashing error (AC-005: 5÷0 shows 'Cannot divide by zero'/'Error'; AC-006: clear/reset after the error returns to cleared start state) — this is also the basis for NFR-008 (system stays stable on invalid input). US-003 [high]: percentage calculation (AC-007: 200×10% = 20; AC-008: 50% = 0.5). US-004 [high]: clear/reset control (AC-009: clear returns display to zero/empty; AC-010: starting a new number after a completed result replaces it rather than appending). US-005 [medium]: chaining from a previous result (AC-011: result 20, +5, = shows 25).

**Related:** US-001, US-002, US-003, US-004, US-005, AC-001, AC-002, AC-003, AC-004, AC-005, AC-006, AC-007, AC-008, AC-009, AC-010, AC-011, NFR-008

### EPIC-002 · draft · source: requirements:EPIC-002

Input methods epic: an on-screen tap keypad and full physical-keyboard operation, so the calculator works equally on touch and desktop devices.

US-006 [critical]: on-screen keypad (AC-012: keypad shows digits 0-9, decimal point, +, −, ×, ÷, %, =, and clear/reset; AC-013: each tap registers the input and updates the display). US-007 [high]: physical keyboard entry (AC-014: typed digits, +, -, *, /, %, Enter, decimal point map to the matching operation; AC-015: Backspace, Escape, or Delete clear the entry/reset consistently with the on-screen clear control).

**Related:** US-006, US-007, AC-012, AC-013, AC-014, AC-015

### EPIC-003 · draft · source: requirements:EPIC-003

Responsive, WCAG-aligned accessible interface epic: adapts to mobile/desktop screens and supports keyboard navigation, visible focus, and readable contrast, scoped as MVP-level basics under the RPwD Act 2016.

US-008 [high]: responsive mobile/desktop layout (AC-016: mobile keypad/display resize with non-overlapping, tappable keys — ties to NFR-006, NFR-007; AC-017: desktop layout uses available space, remains legible). US-009 [high]: keyboard navigation with visible focus (AC-018: Tab moves through all controls in logical order with a visible focus indicator; AC-019: Enter/Space activates the focused control exactly as a tap would) — ties to NFR-002. US-010 [medium]: readable contrast (AC-020: display/key contrast ratio meets WCAG-aligned minimum of at least 4.5:1 for normal text) — ties to NFR-003. RPwD Act 2016 / WCAG-aligned accessibility: NFR-004 states the interface follows WCAG-aligned basics (keyboard operation, visible focus, readable contrast) in line with RPwD Act 2016 expectations. NFR-005 is an explicitly accepted risk: accessibility scope is deliberately limited to these basics at MVP level; fuller WCAG/GIGW conformance is not addressed.

**Related:** US-008, US-009, US-010, AC-016, AC-017, AC-018, AC-019, AC-020, NFR-002, NFR-003, NFR-004, NFR-005, NFR-006, NFR-007

- ⚠ NFR-005 is an accepted-risk limitation: full WCAG/GIGW accessibility conformance beyond the basics (keyboard, focus, contrast) is explicitly out of scope — confirm this is acceptable for the target user base, including users with disabilities beyond these basics.

### EPIC-004 · draft · source: requirements:EPIC-004

Open, private, free-access epic: no sign-in, no payments, and fully client-side computation with nothing stored or transmitted, with an explicit assumption that this removes most DPDP obligations.

US-011 [critical]: anonymous use (AC-021: all functions usable immediately on first load with no sign-in/registration/identity prompt). US-012 [high]: client-side-only computation (AC-022: all computation happens in-browser, nothing persisted or transmitted to a server; AC-023: reloading/closing the page retains no history or memory of prior calculations) — this is the basis for NFR-001. US-013 [medium]: free of charge (AC-024: no payment, subscription, billing, or paywall at any point). DPDP Act 2023 (notice/consent, data-principal rights): assessed in the requirements as not materially applicable because no personal data is collected, stored, or transmitted (NFR-001, US-012). Data residency / sector localisation rules (DPDP, RBI, SEBI, IRDAI): also assessed as not applicable for the same no-data-storage reason, per the AWS rationale in REQ-TECHSTACK.

**Related:** US-011, US-012, US-013, AC-021, AC-022, AC-023, AC-024, NFR-001

- ⚠ This 'DPDP does not materially apply' assumption is stated in the requirements but has not been independently reviewed or signed off by a compliance owner.
- ⚠ Verifiable parental consent / no tracking-or-targeted-advertising-to-children provisions of DPDP are not addressed by any requirement (plausibly not applicable since no data is collected at all, but not explicitly confirmed).
- ⚠ Breach notification duties (DPDP Act notification to the Data Protection Board and affected people; CERT-In 6-hour incident reporting and 180-day ICT log retention) are not addressed by any requirement, even though the app will run on AWS infrastructure.
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v1  
**Delivery scope:** lightweight  
**Approved:** 2026-10-29

**Capabilities in scope:** Addition, subtraction, multiplication and division, Percentage calculation, Clear / reset, On-screen tap keypad, Physical keyboard entry, Responsive mobile and desktop layout, Accessibility basics: keyboard navigation, visible focus, readable contrast, Open, anonymous use with no sign-in or accounts, Free to use with no payments or billing, Calculations run in the browser with nothing stored or transmitted

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | FastAPI | The calculator does its maths in the browser and stores nothing, so there is no business logic for a server to run. FastAPI is kept here only to serve the application files to visitors. It is the platform default and is more than enough for that one job; you are not building any API behind it. |
| cloud | AWS | You need somewhere to host a responsive web app reliably for general users across India. AWS is the platform default, serves your static files close to Indian users (via CloudFront edge locations) for fast loads, and since you store no personal data there are no DPDP residency constraints to satisfy. It comfortably covers a free, anonymous, no-sign-in tool at any traffic level. |
| database | PostgreSQL | You confirmed nothing is persisted — no accounts, no history, no personal data — so the product genuinely needs no database. PostgreSQL is named only as the platform default to fill this slot; nothing will be written to it unless you later add a feature that stores data, such as calculation history (currently out of scope). |
| frontend | React | Your whole product lives in the browser: an on-screen keypad that also takes physical keyboard input, working the same on a phone and a desktop. React is the platform default and handles this well — a responsive layout, focus handling and contrast you need for the RPwD/WCAG accessibility basics, and keyboard events all come naturally. Since every calculation runs client-side and nothing is saved, React alone delivers essentially the entire calculator. |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-001: Core Arithmetic Operations

The calculator performs everyday arithmetic — addition, subtraction, multiplication, division and percentage — and allows the user to clear or reset the current calculation. All computation runs client-side in the browser.

### US-001: Add, subtract, multiply and divide numbers

**Priority:** critical

> As a general user in India, I want to add, subtract, multiply and divide numbers, so that I can carry out everyday arithmetic quickly.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | the calculator is open with a cleared display | I enter 12, press +, enter 8 and press equals | the display shows 20 |
| AC-002 | the calculator is open with a cleared display | I enter 20, press -, enter 5 and press equals | the display shows 15 |
| AC-003 | the calculator is open with a cleared display | I enter 6, press ×, enter 7 and press equals | the display shows 42 |
| AC-004 | the calculator is open with a cleared display | I enter 9, press ÷, enter 3 and press equals | the display shows 3 |

### US-002: Handle division by zero gracefully

**Priority:** high

> As a general user, I want a clear, non-crashing response when I divide by zero, so that I understand the operation is not valid and can continue.

| ID | Given | When | Then |
|---|---|---|---|
| AC-005 | the calculator is open | I enter 5, press ÷, enter 0 and press equals | the display shows an error indication (such as 'Cannot divide by zero' or 'Error') instead of crashing or freezing |
| AC-006 | a division-by-zero error is shown on the display | I press clear/reset | the display returns to its cleared starting state and is ready for a new calculation |

### US-003: Calculate a percentage

**Priority:** high

> As a general user, I want to calculate percentages, so that I can work out discounts, shares and simple proportions.

| ID | Given | When | Then |
|---|---|---|---|
| AC-007 | the calculator is open with a cleared display | I enter 200, press ×, enter 10 and press the percent (%) key | the display shows 20 |
| AC-008 | the calculator is open with a cleared display | I enter 50 and press the percent (%) key | the display shows 0.5 |

### US-004: Clear and reset the calculation

**Priority:** high

> As a general user, I want to clear the current entry or reset the whole calculation, so that I can correct mistakes and start fresh.

| ID | Given | When | Then |
|---|---|---|---|
| AC-009 | the display shows an in-progress or completed calculation | I press the clear/reset (C/AC) control | the display returns to its cleared starting state (zero/empty) ready for a new calculation |
| AC-010 | the display shows the result of a completed calculation | I begin entering a new number without first pressing clear | the previous result is replaced by the new entry rather than appended to it |

### US-005: Chain operations in sequence

**Priority:** medium

> As a general user, I want to continue calculating from a previous result, so that I can perform multi-step everyday sums without re-typing.

| ID | Given | When | Then |
|---|---|---|---|
| AC-011 | the display shows the result 20 from a prior calculation | I press +, enter 5 and press equals | the display shows 25 |

## EPIC-002: Input Methods: Keypad and Physical Keyboard

Users can operate the calculator through an on-screen tap keypad and through a physical keyboard, so it is comfortable on both touch devices and desktops.

### US-006: Operate the calculator with the on-screen keypad

**Priority:** critical

> As a general user on a touch or pointer device, I want a familiar on-screen keypad of digits and operations, so that I can enter calculations by tapping or clicking.

| ID | Given | When | Then |
|---|---|---|---|
| AC-012 | the calculator is displayed | I view the keypad | it shows digit keys 0–9, a decimal point, the operations +, −, ×, ÷, percent (%), equals, and clear/reset |
| AC-013 | the calculator is displayed | I tap the digit and operation keys | each tap registers the corresponding input and updates the display accordingly |

### US-007: Operate the calculator with a physical keyboard

**Priority:** high

> As a desktop user, I want to type numbers and operators on my physical keyboard, so that I can calculate quickly without using the mouse.

| ID | Given | When | Then |
|---|---|---|---|
| AC-014 | the calculator is focused in a desktop browser | I type digits, +, -, *, /, %, Enter and a decimal point | each keystroke maps to the matching calculator operation and updates the display |
| AC-015 | the calculator is focused | I press Backspace, Escape or the Delete key for clearing | the current entry is removed or the calculation is reset consistently with the on-screen clear control |

## EPIC-003: Responsive and Accessible Interface

The calculator is a responsive web application that adapts to mobile and desktop browsers and follows WCAG-aligned accessibility basics (keyboard navigation, visible focus, readable contrast) in line with the RPwD Act 2016. Assumption: accessibility scope is limited to these basics at this MVP level.

### US-008: Use the calculator across mobile and desktop browsers

**Priority:** high

> As a general user in India, I want a layout that adapts to my screen, so that I can use the calculator comfortably on a phone or a computer.

| ID | Given | When | Then |
|---|---|---|---|
| AC-016 | I open the calculator on a mobile browser | the page loads | the keypad and display resize to fit the smaller screen with keys large enough to tap without overlapping |
| AC-017 | I open the calculator on a desktop browser | the page loads | the layout uses the available space and all keys and the display remain legible and usable |

### US-009: Navigate and operate the calculator by keyboard with visible focus

**Priority:** high

> As a user who relies on keyboard navigation, I want to reach and activate every control by keyboard with a clearly visible focus indicator, so that I can use the calculator without a pointing device.

| ID | Given | When | Then |
|---|---|---|---|
| AC-018 | the calculator is open | I press Tab repeatedly | focus moves through all interactive controls in a logical order and the currently focused control shows a visible focus indicator |
| AC-019 | a calculator control is focused | I press Enter or Space | that control activates exactly as if it had been tapped |

### US-010: Read the display and controls with sufficient contrast

**Priority:** medium

> As a user with low vision, I want readable text and colour contrast on the display and keys, so that I can see numbers and operations clearly.

| ID | Given | When | Then |
|---|---|---|---|
| AC-020 | the calculator is rendered | the display text and key labels are measured against their backgrounds | the contrast ratio meets the WCAG-aligned minimum (at least 4.5:1 for normal text) |

## EPIC-004: Open, Private, Free Access

The calculator is open and anonymous with no sign-in or accounts, free to use with no payments or billing, and runs entirely client-side so that no personal data is collected, stored or transmitted. Assumption: because nothing is persisted or transmitted, India's DPDP consent/residency/breach obligations do not materially apply.

### US-011: Use the calculator anonymously without sign-in

**Priority:** critical

> As a general user in India, I want to use the calculator immediately without creating an account or logging in, so that I can calculate without any barrier or identification.

| ID | Given | When | Then |
|---|---|---|---|
| AC-021 | I open the calculator for the first time | the page loads | I can use all calculator functions immediately with no sign-in, registration, account or identity prompt |

### US-012: Keep all calculation client-side with nothing stored or transmitted

**Priority:** high

> As a privacy-conscious user, I want my calculations to run in my browser and not be saved or sent anywhere, so that no personal data about me is collected.

| ID | Given | When | Then |
|---|---|---|---|
| AC-022 | I perform calculations in the calculator | the calculations run | all computation happens client-side in the browser and no calculation data or personal data is persisted or transmitted to any server |
| AC-023 | I have performed calculations and then reload or close the page | I reopen the calculator | no history or memory of prior calculations is retained, consistent with the no-storage design |

### US-013: Use the calculator free of charge

**Priority:** medium

> As a general user, I want the calculator to be completely free, so that I can use it without any payment.

| ID | Given | When | Then |
|---|---|---|---|
| AC-024 | I use any feature of the calculator | I interact with it | no payment, subscription, billing or paywall is presented at any point |
<!-- sdlc:auto:end epics -->
