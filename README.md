# Agro Hub × TraceRoot — export data collection

Standalone portal for Agro Hub to enter company, customer, product, partner, and
source-document information used to configure the TraceRoot export desk.

Progress saves in the browser under an optional draft name. When finished they
**Download JSON** (and optionally use **CSV** for customers/products) and email
TraceRoot. Attach sample PDFs / email examples separately.

## Local preview

```bash
npx serve .
```

## Deploy to Vercel (this repo only)

```bash
npx vercel --prod
```

Or: Vercel → **Add New Project** → import **this** repository → Deploy  
(no framework, no build command — static `index.html`).

Do **not** connect the SilverBirch-FE monorepo.

## Client workflow

1. Open the Vercel URL.
2. Fill **Form sources** — one form at a time (PI, CRO, customs invoice, FI request, …), or **Use typical defaults**.
3. Fill **Company**, **Customers**, **Products**, **Partners**.
4. Optional: CSV templates for customers/products → Import CSV.
5. **Download JSON** → email TraceRoot (plus sample files).
6. Optional: **Print**.

## JSON shape

```json
{
  "version": 1,
  "kind": "agro-hub-data-collection",
  "company": {},
  "isfParties": [
    {
      "role": "seller",
      "name": "",
      "street": "",
      "city": "",
      "state": "",
      "postalCode": "",
      "country": "",
      "contact": "",
      "fdaRegistration": "",
      "sameAsShipper": false
    }
  ],
  "banks": [],
  "contacts": {},
  "partners": {},
  "defaults": {},
  "customers": [],
  "products": [],
  "formSources": {
    "ci_sap": {
      "sources": ["final_pi", "cro_pdf"],
      "canSendSample": true,
      "otherSource": "",
      "notes": ""
    }
  },
  "documents": { "extraNotes": "" }
}
```

Map `customers[]` into Agro Hub `customers.json` defaults in the TraceRoot profile.

## Related (monorepo)

Reference copy + printable checklist live in SilverBirch-FE:

- `agro-hub-data-collection/` (reference copy)
- `docs/onboarding/agro-hub-source-docs-checklist.html`
