# Nightmare Headline Game Examples

Field-tested examples of the Nightmare Headline Game across industry domains, showing the translation from disaster to technical root cause and exploratory charters.

---

## 1. E-Commerce & Retail

- **Nightmare Headline:** *"Online Retailer Gives Away Luxury Watches for $0 During Cyber Monday Flash Sale."*
  - **Contributing Causes:** Negative quantities in cart, coupon stacking without total check, race condition between currency conversion and payment authorization.
  - **Resulting Charter:** *Explore cart checkout with negative quantities, extreme coupon combinations, and rapid currency switching to discover pricing calculation vulnerabilities.*

- **Nightmare Headline:** *"Customers Discover Order Histories of Strangers After System Update."*
  - **Contributing Causes:** Inadequate tenant isolation in cache keys, session cookie reuse across users.
  - **Resulting Charter:** *Explore user session handling with concurrent logins across multiple browser profiles to discover cross-account data leakage in cached views.*

---

## 2. Healthcare & Life Sciences

- **Nightmare Headline:** *"Hospital System Dispenses Double Doses Due to Software Lag."*
  - **Contributing Causes:** UI unresponsiveness leading clinician to click "Submit" twice; unhandled idempotency on medication order API.
  - **Resulting Charter:** *Explore medication administration workflows with duplicate rapid submissions and simulated network latency to discover duplicate record creation.*

---

## 3. Financial Services & Banking

- **Nightmare Headline:** *"Automated Transfer System Drains Customer Savings on Leap Day."*
  - **Contributing Causes:** Date math overflow on February 29th, scheduled recurring transfer loop failing to update next-run timestamp.
  - **Resulting Charter:** *Explore recurring transfer scheduling with edge-case date boundaries (leap days, daylight savings shifts, month-ends) to discover runaway execution loops.*
