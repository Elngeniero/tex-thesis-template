# Árbol del Problema — Borrador

> **Memoria:** Generación de flujos de movilidad en Santiago de Chile mediante Deep Gravity: evaluación del impacto de las amenities de OpenStreetMap y análisis mediante XAI
>
> Este archivo es un borrador en Markdown del diagrama que se incluirá en `definicion_del_problema.tex` como Figura 1. Una vez aprobado el contenido, se exportará como imagen (TikZ, draw.io, Figma, etc.) e incluirá en el `.tex`.

---

## Estructura del árbol

```
╔══════════════════════════════════════════════════════════════════════════════╗
║                                  EFECTOS                                    ║
╠══════════════════════════════════════════════════════════════════════════════╣
║                                                                              ║
║  ┌──────────────────────┐  ┌─────────────────────┐  ┌────────────────────┐ ║
║  │ Decisiones de        │  │ Incapacidad de       │  │ Opacidad en la     │ ║
║  │ inversión basadas    │  │ anticipar el         │  │ decisión pública;  │ ║
║  │ en datos de hace     │  │ impacto de nuevas    │  │ baja confianza     │ ║
║  │ más de 14 años       │  │ intervenciones       │  │ ciudadana en la    │ ║
║  │ (Metro, BRT,         │  │ urbanas sobre los    │  │ planificación del  │ ║
║  │ ciclovías)           │  │ flujos de movilidad  │  │ transporte         │ ║
║  └──────────────────────┘  └─────────────────────┘  └────────────────────┘ ║
║                                                                              ║
║  ┌──────────────────────────────────────┐  ┌─────────────────────────────┐  ║
║  │ Brecha metodológica frente al        │  │ Subutilización del dataset  │  ║
║  │ state-of-the-art internacional;      │  │ administrativo del DTPM     │  ║
║  │ rezago en investigación sobre        │  │ (noviembre 2024), de alta   │  ║
║  │ movilidad latinoamericana            │  │ resolución y sin explotar   │  ║
║  └──────────────────────────────────────┘  └─────────────────────────────┘  ║
║                                                                              ║
╠══════════════════════════════════════════════════════════════════════════════╣
║                           PROBLEMA CENTRAL                                   ║
╠══════════════════════════════════════════════════════════════════════════════╣
║                                                                              ║
║   La planificación del transporte en Santiago opera con estimaciones de      ║
║   flujos OD basadas en datos desactualizados y modelos que ignoran la        ║
║   complejidad del tejido urbano, sin capacidad de explicar sus predicciones. ║
║                                                                              ║
╠══════════════════════════════════════════════════════════════════════════════╣
║                                  CAUSAS                                      ║
╠══════════════════════════════════════════════════════════════════════════════╣
║                                                                              ║
║  ┌──────────────────────┐  ┌─────────────────────┐  ┌────────────────────┐ ║
║  │ EOD desactualizada   │  │ Modelos de gravedad  │  │ Ausencia de        │ ║
║  │ (última versión      │  │ clásicos con         │  │ features           │ ║
║  │ 2012/2017) y de      │  │ underfitting,        │  │ geográficas        │ ║
║  │ alto costo; bip!     │  │ overdispersión y     │  │ (amenities OSM,    │ ║
║  │ con cobertura        │  │ linealidad forzada   │  │ POIs, uso de       │ ║
║  │ incompleta           │  │                      │  │ suelo, red vial)   │ ║
║  └──────────────────────┘  └─────────────────────┘  └────────────────────┘ ║
║                                                                              ║
║  ┌──────────────────────────────────────┐  ┌─────────────────────────────┐  ║
║  │ Falta de explicabilidad (XAI)        │  │ Sin validación de modelos   │  ║
║  │ en los modelos de distribución       │  │ de deep learning en         │  ║
║  │ de viajes vigentes                   │  │ metrópolis latinoamericanas │  ║
║  └──────────────────────────────────────┘  └─────────────────────────────┘  ║
║                                                                              ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

---

## Contenido detallado por nivel

### CAUSAS (raíces del problema)

| # | Causa |
|---|-------|
| C1 | EOD desactualizada (2012/2017), costosa y de baja periodicidad; tarjeta bip! con cobertura incompleta de modos |
| C2 | Modelos de gravedad clásicos con underfitting, overdispersión e incapacidad de capturar no-linealidades |
| C3 | Ausencia de features geográficas (amenities OSM, POIs, uso de suelo, red vial) en los modelos vigentes |
| C4 | Falta de explicabilidad (XAI) en los modelos de distribución de viajes actualmente en uso en Santiago |
| C5 | Inexistencia de validación de modelos de deep learning para generación de flujos en metrópolis latinoamericanas |

### PROBLEMA CENTRAL

> La planificación del transporte en Santiago opera con estimaciones de flujos OD basadas en datos desactualizados y modelos que ignoran la complejidad del tejido urbano, sin capacidad de explicar sus predicciones.

### EFECTOS (consecuencias del problema no resuelto)

| # | Efecto |
|---|--------|
| E1 | Decisiones de inversión en infraestructura (Metro, BRT, ciclovías) basadas en datos de hace más de 14 años, sin reflejar la redistribución post-pandémica de la demanda |
| E2 | Incapacidad de anticipar el impacto de nuevas intervenciones urbanas (apertura de mall, cierre de eje vial, nueva estación) sobre los flujos de movilidad |
| E3 | Opacidad en la decisión pública; baja confianza ciudadana en la planificación del transporte al no poder auditar las predicciones |
| E4 | Brecha metodológica frente al state-of-the-art internacional; rezago de la investigación chilena sobre la especificidad de la movilidad latinoamericana |
| E5 | Subutilización del dataset administrativo del DTPM (noviembre 2024), de mayor resolución que la EOD y sin explotar para modelado generativo |

---

## Notas de diseño para el diagrama final

- **Herramienta sugerida:** draw.io (gratuito, exporta a PNG/PDF), TikZ (LaTeX nativo), o Figma.
- **Paleta de colores:**
  - Causas: azul claro `#D0E8F5`
  - Problema central: rojo/naranja `#F4B942` (highlight)
  - Efectos: gris claro `#E8E8E8`
- **Tipografía:** Carlito (misma que el documento LaTeX).
- **Referencia visual:** seguir el estilo de la Figura 1 de la memoria de Angélica García (Diagnóstico del árbol del problema).
- **Dimensiones:** ancho de página completo (`width=\textwidth` en LaTeX).
