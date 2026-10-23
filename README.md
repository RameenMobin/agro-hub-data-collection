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
2. Fill **Company**, **Customers**, **Products**, **Partners**, and tick **Documents**.
3. Optional: download CSV templates → fill in Excel → Import CSV.
4. **Download JSON** → email TraceRoot (plus sample files).
5. Optional: **Print**.

## JSON shape

```json
{
  "version": 1,
  "kind": "agro-hub-data-collection",
  "company": {},
  "banks": [],
  "contacts": {},
  "partners": {},
  "defaults": {},
  "customers": [],
  "products": [],
  "documents": { "pi_filled_pdf": true }
}
```

Map `customers[]` into Agro Hub `customers.json` defaults in the TraceRoot profile.

## Related (monorepo)

Reference copy + printable checklist live in SilverBirch-FE:

- `agro-hub-data-collection/` (reference copy)
- `docs/onboarding/agro-hub-source-docs-checklist.html`
