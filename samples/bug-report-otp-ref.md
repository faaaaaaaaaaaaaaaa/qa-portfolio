# Sample Bug Report — OTP Reference Missing on Confirm Screen

**Project type:** Web SaaS registration  
**Reporter:** Kanpitcha Sinitwarakun  
**Status (sample):** Open / Needs fix  
**Note:** Sanitized sample. Client product name, UAT URL, and personal phone numbers removed.

---

## Summary

After a successful OTP send, the OTP confirmation screen does not display the OTP reference (ref) that should identify the verification request. Users and support cannot match the on-screen challenge to the SMS/reference channel.

---

## Environment

| Field | Value |
|-------|--------|
| Platform | Web (desktop Chromium) |
| Build / env | UAT (details on request) |
| Browser | Chromium (Playwright + manual) |
| Date found | During registration E2E testing |

---

## Severity / Priority

| Field | Value |
|-------|--------|
| **Severity** | Medium–High (UX + supportability; may block confident verification) |
| **Priority** | P2 — fix before production if ref is required by design |

---

## Steps to Reproduce

1. Open the registration page.  
2. Fill valid registration fields and accept Terms of Service.  
3. Submit the form so the system sends an OTP.  
4. Observe the OTP confirmation step.

## Expected Result

- OTP input is shown.  
- An OTP **reference / ref code** is visible (as per design/spec), so the user can confirm they are verifying the correct request.

## Actual Result

- OTP input appears.  
- **OTP reference is missing / shows as empty or null** on the confirmation UI.

---

## Evidence

- Screenshot of OTP step with missing ref (attach when sharing privately).  
- Reproduced in both manual testing and automated headed run.

---

## Impact

- Users cannot confirm they are entering OTP for the correct request.  
- Support troubleshooting becomes harder without a visible correlation ID.  
- May indicate a data-binding or API-response mapping defect (ref present in API but not bound to UI, or ref null from backend).

---

## Hypothesis (for developers)

Possible causes to check:

1. UI binds a wrong field name (e.g. expects `ref` but API returns `otpRef`).  
2. Backend returns `null` / omits ref on this environment.  
3. Component renders before ref state is set (race); no re-render after response.

---

## Suggested verification after fix

1. Retest happy path: ref visible and non-empty after OTP send.  
2. Confirm ref matches value returned by API / SMS channel.  
3. Regression: wrong OTP, resend OTP, and empty-form validation still behave correctly.

---

## Attachments checklist (private share)

- [ ] Screenshot — OTP screen without ref  
- [ ] Optional: network response snippet (redact tokens/PII)  
- [ ] Playwright video clip of reproduction
