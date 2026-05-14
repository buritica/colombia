# Autorretenedor & Regime Matrix

Decision matrix for when to apply or skip each retention type based on vendor status.

Art. 368, 437-1, 911 Estatuto Tributario.

## Buyer × Vendor Matrix

| Vendor condition | ReteRenta | ReteIVA | ReteICA |
|-----------------|-----------|---------|---------|
| Regular (declarante) | Apply | Apply | Apply |
| Regular (no declarante) | Apply (higher rate) | Apply | Apply |
| Autorretenedor de renta | Skip | Apply | Apply |
| Autorretenedor de IVA | Apply | Skip | Apply |
| Autorretenedor de ICA | Apply | Apply | Skip |
| Gran Contribuyente + autorretenedor | Per specific list | Per specific list | Per specific list |
| Régimen Simple | Skip (self-retain) | Skip | Skip (Art. 911 ET) |
| Cuenta de cobro (no IVA responsible) | Apply | N/A (no IVA) | Apply |

## Key Rules

**Autorretenedor:** Vendor self-retains the designated tax — buyer does NOT withhold it. Check RUT or vendor declaration for autorretenedor status per tax type. A vendor can be autorretenedor for one tax but not others.

**Gran Contribuyente:** Designated by DIAN resolución. When both buyer and seller are gran contribuyentes, special rules apply — consult the specific DIAN list. Gran contribuyente status does not automatically mean autorretenedor.

**Régimen Simple:** Art. 911 ET exempts Régimen Simple vendors from all three retention types. The vendor self-retains via their simplified regime. This is a common source of over-retention errors.

**No declarante:** Higher ReteRenta rates apply (see retenciones-2026.md). The vendor's declarante status should be on their RUT.

## Vendor Status Sources

| Status | Where to verify |
|--------|----------------|
| Régimen (Simple/Ordinario) | RUT, invoice header |
| Declarante / No declarante | RUT |
| Autorretenedor (renta/IVA/ICA) | RUT, DIAN resolución |
| Gran Contribuyente | DIAN resolución, annual list |
| CIIU code | RUT, Cámara de Comercio |
