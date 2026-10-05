# Sample Test Cases — SaaS Registration Flow

**Project type:** Web SaaS (registration / onboarding)  
**Scope:** Register → OTP → Create password → Login  
**Author:** Kanpitcha Sinitwarakun  
**Note:** Generic sample derived from a real exam/project. Client URLs, brand names, and personal test data removed.

---

## Happy Path

### TC01 — Successful registration and login

| Field | Detail |
|-------|--------|
| **Priority** | High |
| **Type** | Functional / E2E |
| **Preconditions** | Fresh browser session; valid unused phone number available |
| **Steps** | 1. Open registration page<br>2. Enter company name, first name, last name, phone, email<br>3. Enter a valid promo code (if required)<br>4. Accept Terms of Service<br>5. Submit<br>6. Enter OTP sent to phone<br>7. Confirm OTP<br>8. Set password (meet policy)<br>9. Confirm password<br>10. Submit<br>11. Log in with new credentials |
| **Expected** | Account created; user reaches authenticated home/dashboard |
| **Automation** | Covered by Playwright happy-path spec |

---

## Negative / Validation

### TC02 — Submit empty registration form

| Field | Detail |
|-------|--------|
| **Priority** | High |
| **Type** | Validation |
| **Steps** | Open registration → leave all required fields empty → submit |
| **Expected** | Inline/required-field errors; no OTP step; no account created |
| **Automation** | Covered |

### TC03 — Invalid promo code

| Field | Detail |
|-------|--------|
| **Priority** | Medium |
| **Type** | Negative |
| **Steps** | Fill valid registration data → enter invalid promo → accept ToS → submit |
| **Expected** | Clear error for promo; registration does not proceed to OTP |
| **Automation** | Covered |

### TC04 — Wrong OTP

| Field | Detail |
|-------|--------|
| **Priority** | High |
| **Type** | Negative / Security-adjacent |
| **Steps** | Complete registration to OTP step → enter incorrect OTP → confirm |
| **Expected** | Error shown; password step not reached; user can retry or request new OTP per product rules |
| **Automation** | Covered |

### TC05 — Invalid phone format

| Field | Detail |
|-------|--------|
| **Priority** | High |
| **Type** | Validation |
| **Steps** | Enter non-numeric / wrong-length phone → fill other fields → submit |
| **Expected** | Phone validation error; no OTP sent |
| **Automation** | Covered |

### TC06 — Submit without accepting Terms of Service

| Field | Detail |
|-------|--------|
| **Priority** | Medium |
| **Type** | Validation |
| **Steps** | Fill all required fields → leave ToS unchecked → submit |
| **Expected** | Blocked submit or ToS error; no OTP step |
| **Automation** | Covered |

---

## Edge cases (manual / exploratory — recommended)

| ID | Scenario | Why it matters |
|----|----------|----------------|
| TC07 | Double-click submit on registration | Prevent duplicate accounts / duplicate OTP |
| TC08 | Back browser after OTP success | Session/state consistency |
| TC09 | Password below minimum length | Policy enforcement |
| TC10 | Reuse phone already registered | Clear conflict message |
| TC11 | OTP expired / resend | Timeout UX and security |
| TC12 | Network drop mid-OTP | Error recovery, no corrupt state |

---

## Coverage notes

- Happy path proves the core business flow works end-to-end.  
- Negative cases prove the product fails safely.  
- Automation focuses on stable, high-value regressions first; exploratory/edge cases stay manual until UI is stable.
