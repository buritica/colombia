---
name: retencion
description: >
  Compute retenciones en la fuente from extracted invoice data — ReteRenta,
  ReteIVA, ReteICA with regime awareness, UVT thresholds, and autorretenedor
  detection. Triggers on: "retencion", "retenciones", "calcular retención",
  "compute retention", "cuánto retener".
---
# Retención en la Fuente

Compute retenciones from extracted invoice data. References in `references/` are the source of truth for rates, thresholds, and regime rules.

## Input

Structured data from Gemini PDF extraction or manual entry:

```
document_type: "factura" | "cuenta_de_cobro" | "unknown"
vendor_name: string
vendor_nit: string
vendor_regime: string
vendor_tipo: string
vendor_autorretenedor: string[]    # e.g. ["renta", "ica"]
vendor_ciiu: string                # CIIU code if available
invoice_number: string
invoice_date: string
subtotal: number                   # before taxes (COP)
iva: number                        # IVA charged
total: number                      # total invoice value
concept: string                    # service description
```

## Computation

**Step 1 — Validate extraction.**
Arithmetic gate: `|subtotal + iva - total| < 1000` COP. If fails: flag but continue (mark as unverified).

**Step 2 — Classify document type.**
See `references/document-types.md`. If `cuenta_de_cobro`: IVA-related retentions = N/A.

**Step 3 — Classify concept and check UVT thresholds.**
Map `concept` using the classification table in `references/retenciones-2026.md`.
Check UVT floor from `references/uvt.md`: if `subtotal < UVT_floor × UVT_value`: zero retention for that concept.

**Step 4 — Check autorretenedor status.**
For each retention type (renta, IVA, ICA), check `vendor_autorretenedor[]` against the matrix in `references/regimen-matrix.md`. If vendor self-retains: skip that retention.

**Step 5 — Apply rates.**

| Retention | Base | Rate source |
|-----------|------|-------------|
| ReteRenta | subtotal | `references/retenciones-2026.md` by concept + declarante status |
| ReteIVA | iva | 15% of IVA (if applicable) |
| ReteICA | subtotal | `references/retenciones-2026.md` by CIIU or Bogotá default 0.966% |

**Step 6 — Compute net.**
`net_to_vendor = subtotal + iva - reteRenta - reteIVA - reteICA`

## Output

```
📋 Factura #[number] — [Vendor Name]
📄 Tipo: Factura electrónica | Cuenta de cobro
Subtotal: $X | IVA: $X | Total: $X ✓

Retenciones calculadas:
• ReteRenta [X%]: $X
• ReteIVA [15%]: $X
• ReteICA [X%]: $X
Neto a pagar: $X

Régimen: [regime]
Tipo contribuyente: [tipo]
```

## Flags

Append when relevant:
- "📄 Cuenta de cobro — no IVA, no ReteIVA"
- "🔄 Vendor es autorretenedor de [X] — no se aplica rete[X]"
- "ℹ️ Subtotal bajo umbral UVT — sin retención [concept]"
- "⚠️ Arithmetic mismatch — verificar PDF"
- "⚠️ ReteICA no calculado — CIIU o municipio desconocido"
- "⚠️ Régimen no confirmado — asumiendo declarante"
- "⚠️ Concepto ambiguo — clasificación incierta, verificar con contador"

## Dedup

An invoice is unique by `invoice_number + vendor_nit`. Duplicates should be flagged, not reprocessed.
