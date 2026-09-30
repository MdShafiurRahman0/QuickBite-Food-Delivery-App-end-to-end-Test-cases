# 🍔 QuickBite — Test Case Design

![Test Cases](https://img.shields.io/badge/Test%20Cases-83-blue)
![PRD Gaps Found](https://img.shields.io/badge/PRD%20Gaps%20Found-20-orange)
![Platform](https://img.shields.io/badge/Platform-iOS%20%26%20Android-green)
![Design Techniques](https://img.shields.io/badge/Design%20Techniques-5-purple)
![Execution](https://img.shields.io/badge/Execution-Not%20Started-lightgrey)
![Version](https://img.shields.io/badge/Version-v1.0-informational)

A structured **test case design** for **QuickBite**, a food ordering and delivery app for iOS and Android. The suite covers cart, coupons, checkout, payment, order tracking, cancellation/refund and ratings. Every test case is traced to a requirement ID, and the requirement review produced a list of gaps, conflicts and assumptions to be clarified with the Business Analyst / Product Owner.

[![Google Sheet](https://img.shields.io/badge/Test%20Cases-Google%20Sheet-34A853?logo=googlesheets&logoColor=white)](https://docs.google.com/spreadsheets/d/15FfvsfSbLDCeufkETjPgTOq-DkhLvq9Oay9Kkv85Viw/edit?usp=sharing)
[![Presentation](https://img.shields.io/badge/Presentation-Canva-00C4CC?logo=canva&logoColor=white)](https://canva.link/hsbnzfb4fznyio2)
[![Video](https://img.shields.io/badge/Walkthrough-Video-EA4335?logo=googledrive&logoColor=white)](https://drive.google.com/file/d/1xWyM69JmK5tU8zeIWpSV0e6GO6_l4pHg/view?usp=sharing)

---

## Table of Contents

- [Project Overview](#project-overview)
- [Deliverables](#deliverables)
- [Scope](#scope)
- [Test Design Techniques](#test-design-techniques)
- [Test Case Coverage](#test-case-coverage)
- [Boundary Value Coverage](#boundary-value-coverage)
- [Requirement Traceability](#requirement-traceability)
- [Requirement Gaps and Assumptions](#requirement-gaps-and-assumptions)
- [Sample Test Cases](#sample-test-cases)
- [Test Case Template](#test-case-template)
- [Current Status](#current-status)
- [How to Use This Suite](#how-to-use-this-suite)
- [Repository Contents](#repository-contents)
- [Author](#author)

---

## Project Overview

| Field | Details |
|---|---|
| **Project** | QuickBite: Food Ordering & Delivery App |
| **Platform** | iOS and Android |
| **Document** | Test Case Design |
| **Scope** | Cart, Coupons, Checkout, Payment, Order Tracking, Cancellation/Refund, Ratings |
| **Prepared By** | Md. Shafiur Rahman |
| **Date** | 28 September 2026 |
| **Version** | v1.0 |
| **Techniques Used** | Equivalence Partitioning, Boundary Value Analysis, Decision Table, State Transition, Error Guessing |
| **Requirement IDs** | `GUEST`, `FR-1` to `FR-28`, `NFR-1` to `NFR-5`, `BR-1` to `BR-3` |
| **Status** | Design complete. Execution not started (see [Current Status](#current-status)) |

### Highlights

- **83 test cases** across 10 modules: 25 Functional, 19 Negative, 21 Boundary, 12 Edge Case and 6 Non-Functional.
- **Both sides of every boundary** are tested (for example ₹149 / ₹150, ₹2,000 / ₹2,001, 20 / 21 items).
- **Full requirement coverage:** every requirement ID (`GUEST`, `FR`, `NFR`, `BR`) has at least one linked test case.
- **Requirement review:** **20 gaps, conflicts and assumptions** were documented, including two direct conflicts inside the PRD.
- **Server-side and failure scenarios** are covered, such as double taps, payment confirmation loss, a forced COD order through the API, and network switching during payment.

---

## Deliverables

| Deliverable | Description | Link |
|---|---|---|
| **Test Case Workbook** | Google Sheet with 4 tabs: Summary, Test Cases, Requirement Traceability, Assumptions & Questions | [Open Google Sheet](https://docs.google.com/spreadsheets/d/15FfvsfSbLDCeufkETjPgTOq-DkhLvq9Oay9Kkv85Viw/edit?usp=sharing) |
| **Presentation** | Slide deck summarising the approach, coverage and findings | [View on Canva](https://canva.link/hsbnzfb4fznyio2) |
| **Video Walkthrough** | Recorded presentation of the test design | [Watch on Google Drive](https://drive.google.com/file/d/1xWyM69JmK5tU8zeIWpSV0e6GO6_l4pHg/view?usp=sharing) |

### Workbook tabs

| Tab | Purpose |
|---|---|
| **Summary** | Project details, test case counts by module and type, priority and execution status |
| **Test Cases** | All 83 test cases with steps, test data and expected results |
| **Requirement Traceability** | Mapping between requirements and test cases |
| **Assumptions & Questions** | Requirement gaps, the assumption used in testing and the question for the BA / Product Owner |

---

## Scope

| Module | Requirement IDs | Focus |
|---|---|---|
| Guest & Access | `GUEST` | Browsing without login; login required at checkout |
| Cart Management | `FR-1` to `FR-5` | Add/remove items, item and quantity limits, single-restaurant rule, live cart total |
| Coupons & Discounts | `FR-6` to `FR-11` | Valid/invalid coupons, `WELCOME50`, `FLAT20`, stacking, expiry |
| Checkout & Order Value | `FR-12` to `FR-15` | Minimum order, delivery fee, GST and grand total, Pay Now conditions |
| Payment | `FR-16` to `FR-19` | Card, COD and wallet, declines, COD limit, payment confirmation, order confirmation |
| Order Tracking | `FR-20` to `FR-22`, `NFR-5` | Status sequence, ETA, delivery time, push notifications |
| Cancellation & Refund | `FR-23` to `FR-26` | Cancellation window, restaurant acceptance, refund to source |
| Ratings & Reviews | `FR-27`, `FR-28` | Rating rules, separate delivery rating, edit window |
| Business Rules | `BR-1` to `BR-3` | Duplicate accounts, referral bonus, wallet rules |
| Non-Functional | `NFR-1` to `NFR-4` | Performance, peak load, transport security, low-end device, weak network |

---

## Test Design Techniques

| Technique | Where it is applied | Example test cases |
|---|---|---|
| **Equivalence Partitioning** | Valid vs. invalid coupons, first-time vs. existing users, payment methods | TC-013, TC-014, TC-016, TC-019 |
| **Boundary Value Analysis** | Item and quantity limits, coupon thresholds, COD limit, cancellation and edit windows, rating scale, referral amount | TC-004, TC-005, TC-017, TC-018, TC-045, TC-046, TC-058, TC-070, TC-071 |
| **Decision Table** | Conditions that enable Pay Now, coupon eligibility, COD availability | TC-035 to TC-038, TC-016 to TC-020, TC-045 to TC-048 |
| **State Transition** | Order status flow, cancellation before/after restaurant acceptance, payment + acceptance leading to Order Confirmed | TC-053, TC-054, TC-057 to TC-062, TC-050 to TC-052 |
| **Error Guessing** | Double tap, double cancel, simultaneous cancel and accept, coupon expiring mid-checkout, forced COD through the API, lost payment confirmation, network switch | TC-039, TC-065, TC-060, TC-027, TC-048, TC-049, TC-076 |

---

## Test Case Coverage

### By module and type

| Module | Functional | Negative | Boundary | Edge Case | Non-Functional | Total |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| Guest & Access | 1 | 1 | 0 | 0 | 0 | 2 |
| Cart Management | 5 | 0 | 4 | 1 | 0 | 10 |
| Coupons & Discounts | 4 | 4 | 5 | 2 | 0 | 15 |
| Checkout & Order Value | 3 | 4 | 3 | 2 | 0 | 12 |
| Payment | 4 | 4 | 2 | 3 | 0 | 13 |
| Order Tracking | 3 | 1 | 0 | 0 | 1 | 5 |
| Cancellation & Refund | 3 | 1 | 2 | 3 | 0 | 9 |
| Ratings & Reviews | 1 | 2 | 3 | 0 | 0 | 6 |
| Business Rules | 1 | 2 | 2 | 1 | 0 | 6 |
| Non-Functional | 0 | 0 | 0 | 0 | 5 | 5 |
| **Total** | **25** | **19** | **21** | **12** | **6** | **83** |

### By priority

| Priority | Count |
|---|:---:|
| High | 79 |
| Medium | 4 |
| Low | 0 |
| **Total** | **83** |

### By execution status

| Status | Count |
|---|:---:|
| Not Executed | 83 |
| Pass | 0 |
| **Total** | **83** |

---

## Boundary Value Coverage

| Rule | Values tested | Test cases |
|---|---|---|
| Items in cart | 20 (allowed) and 21 (blocked); distinct items vs. total units | TC-004, TC-005, TC-006 |
| Quantity per item | 10 (allowed), 11 (blocked); decrease from 1 | TC-009, TC-010 |
| Minimum order value | ₹99 (below minimum) | TC-028 |
| `FLAT20` minimum subtotal | ₹149 (rejected) and ₹150 (applied) | TC-021, TC-022 |
| Coupon threshold on item removal | Subtotal 150 to 149 | TC-024 |
| `WELCOME50` discount cap | ₹200 (exactly at cap) and ₹201 (capped at ₹100) | TC-017, TC-018 |
| GST rounding | Subtotal ₹110.50 gives GST 5.525, rounded half-up to 5.53 | TC-034 |
| COD limit | ₹2,000 (allowed) and ₹2,001 (blocked) | TC-045, TC-046 |
| Free cancellation window | 2:00 (allowed) and 2:01 or later (still free until acceptance) | TC-058, TC-061 |
| Rating scale | 1 and 5 stars (valid), 0 or none (blocked) | TC-067, TC-068 |
| Rating edit window | 23:59 (allowed), 24:00 and 24:01 (blocked) | TC-070, TC-071 |
| Referral bonus | ₹150 (credited), ₹149 / ₹149.99 (no bonus) | TC-079, TC-080 |

---

## Requirement Traceability

Each test case carries a requirement ID in the **Requirement ID** column. The table below summarises the mapping per module. The full mapping is in the **Requirement Traceability** tab of the workbook.

| Module | Requirement IDs | Test case IDs | Test cases |
|---|---|---|:---:|
| Guest & Access | `GUEST` | TC-001 to TC-002 | 2 |
| Cart Management | `FR-1` to `FR-5` | TC-003 to TC-012 | 10 |
| Coupons & Discounts | `FR-6` to `FR-11` | TC-013 to TC-027 | 15 |
| Checkout & Order Value | `FR-12` to `FR-15` | TC-028 to TC-039 | 12 |
| Payment | `FR-16` to `FR-19` | TC-040 to TC-052 | 13 |
| Order Tracking | `FR-20` to `FR-22`, `NFR-5` | TC-053 to TC-056, TC-077 | 5 |
| Cancellation & Refund | `FR-23` to `FR-26` | TC-057 to TC-065 | 9 |
| Ratings & Reviews | `FR-27`, `FR-28` | TC-066 to TC-071 | 6 |
| Business Rules | `BR-1` to `BR-3` | TC-078 to TC-083 | 6 |
| Non-Functional | `NFR-1` to `NFR-4` | TC-072 to TC-076 | 5 |
| **Total** | | | **83** |

---

## Requirement Gaps and Assumptions

While designing the test cases, the PRD was reviewed for conflicts, ambiguities, missing behaviour and untestable statements. Each finding is logged as `AMB-xx` with the **assumption used in the test cases** and a **question for the BA / Product Owner**. Test cases affected by a finding reference its ID in the **Remarks / Ref** column.

### Findings by type

| Type | Count | IDs |
|---|:---:|---|
| Conflict | 2 | AMB-01, AMB-02 |
| Redundancy | 1 | AMB-03 |
| Missing | 4 | AMB-04, AMB-15, AMB-17, AMB-18 |
| Ambiguity | 10 | AMB-05, 06, 07, 08, 09, 10, 11, 13, 14, 20 |
| Untestable | 2 | AMB-12, AMB-16 |
| Assumption | 1 | AMB-19 |
| **Total** | **20** | |

### Key findings

**AMB-01: Delivery fee can never be charged (Conflict, `FR-12` / `FR-13`)**
Checkout requires a minimum order of ₹100, while free delivery applies above ₹99. Every order that can reach checkout gets free delivery, so the flat ₹25 fee is unreachable. Both rules are tested as written (TC-031). *Question: is the free-delivery threshold a typo (for example ₹299)?*

**AMB-02: Cancellation rules contradict each other (Conflict, `FR-19` / `FR-23` / `FR-25`)**
Free cancellation within 2 minutes conflicts with "no cancellation after the restaurant accepts" when the restaurant accepts inside that window. The test assumes `FR-25` wins (TC-059). *Question: which rule takes priority?*

**AMB-09: Total calculation is under-specified (Ambiguity, `FR-14`)**
The GST base, tax on the platform fee and the rounding rule are not defined. Tests assume `Grand total = (Subtotal - Discount) + Delivery fee + Platform fee (₹5) + GST (5% of Subtotal - Discount)`, rounded to 2 decimals, half-up (TC-016, TC-022, TC-032, TC-033, TC-034).

**AMB-16: Non-functional requirements are not measurable (Untestable, `NFR-1` to `NFR-5`)**
No numbers are given for response time, load, device specification, network or notification delay. Tests assume P95 ≤ 2 s, notification ≤ 5 s, a 2 GB RAM device and 10x peak load (TC-072, TC-073, TC-075, TC-077).

### All findings

| ID | Type | Requirements | Gap found | Test cases linked |
|---|---|---|---|:---:|
| AMB-01 | Conflict | FR-12, FR-13 | Minimum order (₹100) and free-delivery threshold (above ₹99) overlap, so the ₹25 fee is unreachable | 1 |
| AMB-02 | Conflict | FR-19, FR-23, FR-25 | Free cancellation within 2 minutes contradicts the block after restaurant acceptance | 1 |
| AMB-03 | Redundancy | FR-23, FR-24 | Both rules make cancellation free, so the 2-minute mark has no functional effect | 2 |
| AMB-04 | Missing | FR-19, FR-20 | No status or timeout defined for waiting, rejection, no response, failed or cancelled orders | 2 |
| AMB-05 | Ambiguity | FR-2, FR-4 | "20 items" may mean 20 distinct items or 20 total units | 3 |
| AMB-06 | Ambiguity | FR-7 | "First-time user" is not defined; minimum order for `WELCOME50` not stated | 1 |
| AMB-07 | Ambiguity | FR-9 | Basis of the coupon threshold check and re-apply behaviour unclear | 2 |
| AMB-08 | Ambiguity | FR-6, FR-10 | Applying a second coupon (blocked or replaced) is not defined | 2 |
| AMB-09 | Ambiguity | FR-14 | GST base, tax on platform fee and rounding rule not defined | 5 |
| AMB-10 | Ambiguity | FR-17 | COD limit basis (subtotal, discounted value or grand total) and exact ₹2,000 not stated | 2 |
| AMB-11 | Ambiguity | FR-18, FR-26 | Business days, refund components, wallet refund timing and COD cancellation refund not stated | 1 |
| AMB-12 | Untestable | FR-21, FR-22 | ETA accuracy and "30-45 minutes" delivery have no measurable tolerance | 1 |
| AMB-13 | Ambiguity | FR-28 | Number of edits allowed and start of the 24-hour window not stated | 1 |
| AMB-14 | Ambiguity | BR-2 | Referral bonus recipient, qualifying order value, COD timing and cancellation handling unclear | 1 |
| AMB-15 | Missing | BR-1 | Login/OTP flow, number format and duplicate-number handling not described | 1 |
| AMB-16 | Untestable | NFR-1 to NFR-5 | No measurable targets for performance, load, device, network or notification delay | 4 |
| AMB-17 | Missing | FR-15, FR-16 | Wallet partial payment, default payment method and serviceable address rules missing | 1 |
| AMB-18 | Missing | Guest, FR-5, BR-1 | Guest add-to-cart, login timing and cart persistence across devices not stated | 1 |
| AMB-19 | Assumption | All | Currency not stated; assumed Indian rupees (₹) | 0 |
| AMB-20 | Ambiguity | FR-4 | Pressing "-" at quantity 1 could remove the item or be disabled | 1 |

---

## Sample Test Cases

A selection of test cases that show the depth of the suite. All 83 are in the [Google Sheet](https://docs.google.com/spreadsheets/d/15FfvsfSbLDCeufkETjPgTOq-DkhLvq9Oay9Kkv85Viw/edit?usp=sharing).

| TC ID | Module | Scenario | Type | Test data | Expected result |
|---|---|---|---|---|---|
| TC-005 | Cart Management | Add the 21st item (above boundary) | Boundary | 1 more item | Add is blocked with a message such as "Maximum 20 items per order"; cart still has 20 items |
| TC-018 | Coupons & Discounts | `WELCOME50` just above cap | Boundary | 50% of ₹201 = ₹100.50 | Discount capped at ₹100, not ₹100.50 |
| TC-027 | Coupons & Discounts | Coupon expires between applying and placing the order | Edge Case | Coupon set to expire in 2 minutes | Server re-validates; order is not placed with the discount; user is informed and total refreshed |
| TC-033 | Checkout & Order Value | Grand total with `WELCOME50` (cap applied) | Functional | Subtotal ₹300 | Discount 100; GST 10; total = 200 + 0 + 5 + 10 = ₹215.00 |
| TC-039 | Checkout & Order Value | Double tap on Pay Now | Edge Case | None | Only one payment attempt and one order created |
| TC-046 | Payment | COD at ₹2,001 (above boundary) | Boundary | Order value ₹2,001 | COD hidden or disabled with a reason; other methods available |
| TC-048 | Payment | COD above ₹2,000 forced through the API | Negative | Order value ₹2,500 | Server rejects the request; no COD order is created |
| TC-049 | Payment | Amount debited but QuickBite receives no confirmation | Functional | Simulated gateway success and server timeout | Order is not created; auto-refund starts; user is informed |
| TC-059 | Cancellation & Refund | Restaurant accepts at 1:00, user cancels at 1:30 | Edge Case | None | `FR-25` overrides `FR-23`: cancellation not allowed after acceptance; message shown |
| TC-076 | Non-Functional | Network switch and weak network during Pay Now | Non-Functional | 2G throttle, Wi-Fi to 4G switch | No duplicate order; clear error or recovery; state remains consistent |

### Full example

| Field | Details |
|---|---|
| **TC ID** | TC-024 |
| **Module** | Coupons & Discounts |
| **Requirement ID** | FR-9 |
| **Scenario** | Removal crosses threshold exactly (150 to 149) |
| **Type / Priority** | Boundary / High |
| **Precondition** | `FLAT20` applied; cart = item A ₹149 + item B ₹1 (subtotal ₹150) |
| **Test Steps** | 1. Remove item B (subtotal becomes ₹149) |
| **Test Data** | 150 to 149 |
| **Expected Result** | Coupon is auto-removed at ₹149 and the user is notified; at ₹150 it stays applied |
| **Status** | Not Executed |
| **Remarks / Ref** | AMB-07 |

---

## Test Case Template

Every test case in the **Test Cases** tab uses the same 13 columns.

| Column | Description |
|---|---|
| **TC ID** | Unique ID (`TC-001` and up) |
| **Module** | Feature area the test belongs to |
| **Requirement ID** | Requirement being verified (`GUEST`, `FR-x`, `NFR-x`, `BR-x`) |
| **Test Scenario** | What is being tested |
| **Test Type** | Functional, Negative, Boundary, Edge Case or Non-Functional |
| **Priority** | High / Medium / Low |
| **Precondition** | State required before execution |
| **Test Steps** | Numbered steps to execute |
| **Test Data** | Input values used |
| **Expected Result** | Correct system behaviour |
| **Actual Result** | Observed behaviour (filled during execution) |
| **Status** | Execution status (Not Executed, Pass, ...) |
| **Remarks / Ref** | Links to requirement gaps (`AMB-xx`) or other notes |

---

## Current Status

- **Design phase: complete (v1.0).**
- **Execution: not started.** All 83 test cases are marked *Not Executed* and the **Actual Result** column is empty by design. This repository documents the test design, not test results.
- **Open items:** 20 requirement findings (`AMB-01` to `AMB-20`) are waiting for BA / Product Owner clarification. Expected results for the test cases that reference them follow the stated assumptions and may change once answers are received.
- **Priority:** 79 of 83 test cases are High priority because the suite focuses on the money-critical flows (cart, coupons, checkout, payment, cancellation and refund).

---

## How to Use This Suite

1. Open the [Google Sheet](https://docs.google.com/spreadsheets/d/15FfvsfSbLDCeufkETjPgTOq-DkhLvq9Oay9Kkv85Viw/edit?usp=sharing) and start with the **Summary** tab.
2. Read **Assumptions & Questions** before executing. Test cases with an `AMB-xx` reference depend on those assumptions.
3. Run the test cases in the **Test Cases** tab. Record the **Actual Result** and update the **Status**.
4. When the BA / Product Owner answers a question, update the affected expected results and the assumption log.
5. Use **Requirement Traceability** to confirm that every requirement is covered after any change.

---

---

## Author

**Md. Shafiur Rahman**
Test case design prepared on 28 September 2026.
