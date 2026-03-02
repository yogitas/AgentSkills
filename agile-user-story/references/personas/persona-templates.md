# 👤 Persona Templates

A library of reusable persona definitions.
Copy the ones relevant to your product into your `USER_CONFIG.personas` list.

---

## 🛍️ Consumer / E-Commerce

| Persona Name | Description |
|---|---|
| `Shopper` | A logged-in customer browsing and purchasing products |
| `Guest Shopper` | An unauthenticated visitor who hasn't created an account |
| `Returning Customer` | A shopper with existing order history and a saved account |
| `Loyalty Member` | A shopper enrolled in a rewards or loyalty programme |
| `Seller / Vendor` | A third-party seller listing products on a marketplace |

---

## 💼 B2B SaaS

| Persona Name | Description |
|---|---|
| `End User` | A team member using the product day-to-day |
| `Account Admin` | A user managing their org's workspace, users, and billing |
| `Super Admin` | An internal employee with full platform access |
| `API Consumer` | A developer integrating via the product's API |
| `Free Tier User` | A user on the free plan with feature restrictions |
| `Pro / Paid User` | A user on a paid plan with full access |
| `Read-Only User` | A collaborator with view access but no edit permissions |
| `Trial User` | A user in a free trial period evaluating the product |

---

## 💳 Fintech / Payments

| Persona Name | Description |
|---|---|
| `Verified User` | A user who has completed KYC and can transact |
| `Unverified User` | A registered user who has not yet completed identity verification |
| `Business Account Owner` | A user managing a business account with sub-users |
| `Compliance Officer` | Internal reviewer monitoring transactions and flagged activity |
| `Support Agent` | Internal team resolving customer issues via admin panel |

---

## 🏥 Healthcare / Regulated Domains

| Persona Name | Description |
|---|---|
| `Patient` | An end user managing their own health data or appointments |
| `Clinician` | A healthcare professional using the platform for patient care |
| `Practice Admin` | Staff managing scheduling, records, and settings for a clinic |
| `Carer / Guardian` | A user managing access on behalf of another person |

---

## 🚀 General / Multi-Domain

| Persona Name | Description |
|---|---|
| `New User` | A user in their first session, unfamiliar with the product |
| `Power User` | An experienced user who uses advanced features regularly |
| `Mobile User` | A user primarily accessing the product via mobile device |
| `Accessibility User` | A user relying on assistive technologies (screen reader, keyboard nav) |
| `Guest / Unauthenticated User` | A visitor with no account |

---

## ✏️ How to Add a Persona to Your Config

```yaml
personas:
  - name: "Shopper"
    description: "A logged-in customer browsing and purchasing products"
  - name: "Guest Shopper"
    description: "An unauthenticated visitor who hasn't created an account"
```

Keep descriptions specific to your product — the more context, the better the stories.
