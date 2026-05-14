# Contable — Colombian Accounting & Tax

Business accounting and tax compliance for Colombian companies.

## Context

Configure for your use case. The defaults assume a Colombian SAS buyer operating in Bogotá.

### Buyer Profile
- Entity type: SAS (Sociedad por Acciones Simplificada)
- Régimen: Responsable de IVA
- Gran contribuyente: No
- Primary municipality: Bogotá
- Activities: Construction, real estate development

### Vendor Data Source
- Google Sheets "Listado de proveedores" (cloned)
- Columns: NIT, Razón social, Banco, Cuenta, Régimen, Concepto habitual

### Invoice Source
- WhatsApp media (PDFs forwarded by project accountant)
- Google Drive CONTABILIDAD folder (archived invoices)

## Skills

| Skill | Command | What it does |
|-------|---------|-------------|
| retencion | `/contable:retencion` | Compute retenciones from extracted invoice data |

## References

Reference files live inside the skill directory (`skills/retencion/references/`) so they're self-contained when cached by the SDK plugin system.

| File | Content | Update frequency |
|------|---------|-----------------|
| `uvt.md` | UVT value and history | Annual (January) |
| `retenciones-2026.md` | Retention rates by concept and regime | Annual |
| `regimen-matrix.md` | Autorretenedor decision matrix | Stable (changes with tax reform) |
| `document-types.md` | Factura vs cuenta de cobro rules | Stable |
