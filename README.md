# Agro Hub × TraceRoot — master data portal

Guided wizard for Agro Hub to enter **masters only**: company, LOVs, products
(with packaging multi-select), customers (pick products → packs appear),
forwarders. Sample PDFs/emails are a checklist on the last step.

Progress saves in the browser. **Download JSON** (canonical) or **Download Excel**
(multi-sheet export matching the old workbook layout).

## Local preview

```bash
npx serve .
```

## Deploy to Vercel

```bash
npx vercel --prod
```

Or: Vercel → import **this** folder / sibling repo only (static `index.html`).  
Do **not** connect the SilverBirch-FE monorepo as the project root unless this
folder is configured as the root directory.

## Client flow

1. **Company** — letterhead + banks  
2. **Dropdowns** — payment, Inco, ports, packaging, pallet  
3. **Products** — name, HS, UoM; tick packaging types from LOVs  
4. **Customers** — address/defaults; tick products; optionally narrow packs  
5. **Forwarders** — portal vs manual  
6. **Samples & send** — tick docs/emails to attach → download JSON/Excel → email TraceRoot with files  

## JSON shape (v2)

```json
{
  "version": 2,
  "kind": "agro-hub-masters",
  "company": {},
  "banks": [],
  "lovs": {
    "payment_terms": ["Net 30", "CAD"],
    "packaging": ["25 kg bags", "Bulk (kg)"]
  },
  "products": [{
    "sku": "",
    "name": "",
    "hsCode": "",
    "uom": "KG",
    "packaging": ["25 kg bags", "Bulk (kg)"]
  }],
  "customers": [{
    "id": "",
    "name": "",
    "productSkus": ["AH-SALT-FINE"],
    "productPackaging": {
      "AH-SALT-FINE": ["Bulk (kg)"]
    }
  }],
  "forwarders": [],
  "sampleChecks": { "docs": {}, "emails": {} }
}
```

LOVs are **values only** (no codes/keys). If `productPackaging[sku]` is omitted,
the customer may use **all** packs defined on that product.
