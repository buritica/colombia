# Retenciones en la Fuente 2026

Canonical retention rates by concept and vendor regime. Base: subtotal (before IVA) unless noted.

Art. 365–419 Estatuto Tributario.

## ReteRenta

| Concepto | Declarante | No declarante | Régimen Simple |
|----------|-----------|---------------|----------------|
| Construcción | 2% | 2% | 0% (self-retain) |
| Honorarios — persona natural | 10% | 11% | 0% |
| Honorarios — persona jurídica | 11% | 11% | 0% |
| Servicios generales | 4% | 6% | 0% |
| Compras generales | 2.5% | 3.5% | 0% |
| Arrendamiento inmuebles | 3.5% | 3.5% | 0% |

## ReteIVA

15% of the IVA value (standard). Art. 437-1 ET.

Exceptions:
- Régimen Simple: 0%
- Cuenta de cobro: N/A (no IVA charged)
- Autorretenedor de IVA: 0% (vendor self-retains)
- Gran contribuyente buying from non-gran-contribuyente: 15%

## ReteICA (Bogotá)

Municipality-dependent, applied on subtotal. Rates set by each municipality's acuerdo.

### Bogotá rates by CIIU activity

| Activity group | Tarifa | Reference |
|---------------|--------|-----------|
| Servicios generales / actividades varias | 0.966% | Acuerdo 65 de 2002 |
| Comercio al por menor | 0.414% | |
| Construcción | 0.690% | |
| Actividades financieras | 1.380% | |
| Actividades inmobiliarias | 0.966% | |

Default for unknown CIIU in Bogotá: **0.966%**.

If vendor CIIU maps to a known Bogotá tarifa, use the specific rate. If CIIU unavailable or outside Bogotá: flag, don't guess.

### Other municipalities

ReteICA rates vary by municipality. Without confirmed municipality data, do not apply ReteICA — flag for manual review.

## Concept Classification

Map invoice description to one of the retention categories:

| Pattern | Category |
|---------|----------|
| Construction, civil works, obra, instalación | Construcción |
| Professional services, asesoría, consultoría, diseño | Honorarios |
| General services, mantenimiento, limpieza, vigilancia | Servicios generales |
| Materials, supplies, compra de, ferretería | Compras generales |
| Rent, arriendo, lease, canon | Arrendamiento inmuebles |

If the concept doesn't clearly fit one category: flag "concepto ambiguo — clasificación incierta, verificar con contador" and default to **Servicios generales** (most conservative rate).
