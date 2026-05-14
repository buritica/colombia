# Document Types: Factura vs Cuenta de Cobro

Two primary invoice document types in Colombian accounting, with different tax treatment.

## Comparison

| | Factura electrónica | Cuenta de cobro |
|--|---------------------|----------------|
| Who issues | IVA-responsible vendors | Non-IVA-responsible vendors (Régimen Simple, personas naturales no responsables) |
| IVA | Yes (19% standard) | No |
| ReteIVA | Applies | N/A |
| DIAN resolución | Required (autorización de facturación) | Not present |
| Format | Standardized XML/PDF (DIAN spec) | Free-form |
| Legal basis | Art. 615–618 ET | Art. 771-2 ET |

## Processing Rules

### Factura electrónica
Standard tax invoice. DIAN-mandated for IVA-responsible vendors. Contains:
- Resolución DIAN (autorización de numeración)
- IVA breakdown (base + 19%)
- Vendor regime declaration
- QR code / CUFE (Código Único de Factura Electrónica)

All three retention types (ReteRenta, ReteIVA, ReteICA) potentially apply.

### Cuenta de cobro
Non-IVA-responsible vendors. No IVA, no ReteIVA, no DIAN resolución. Free-form format — no standardized structure.

Only ReteRenta and ReteICA apply. ReteIVA is always N/A.

## Document Type Detection

When processing a PDF:
1. Check for DIAN resolución number → factura
2. Check for IVA line item → factura
3. Check for "cuenta de cobro" in header → cuenta de cobro
4. Check for QR/CUFE → factura
5. If ambiguous: flag as "tipo de documento no confirmado"
