# Estado del Marco Conceptual — Cap. 2

> **Última actualización:** 23 de agosto de 2026
> **Rol de este archivo:** registro de estado, trazabilidad y material reservado para capítulos siguientes.
> **Renombrado desde:** `figures/INSUMOS_MARCO_CONCEPTUAL.md` → `ESTADO_MARCO_CONCEPTUAL.md`

---

## 1. Estado actual de `marco_conceptual.tex`

Todas las secciones están completas y compilando. El capítulo tiene **8 subsecciones** y **12 ecuaciones numeradas**.

| Sección | Contenido clave | Estado |
|---|---|---|
| §2.1 Movilidad urbana y OD | Def. formal matriz OD (`eq:matriz_od`), formulación del problema | ✅ Completa |
| §2.2.1 Modelo gravitatorio | Eqs. no restringido + restringido (`eq:gravedad`, `eq:gravedad_restringida`), limitaciones | ✅ Completa |
| §2.2.2 IO Model (Stouffer) | Eqs. diferencial + integral, eq. formal P_ij (`eq:io_formal`), def. m_l, s_ij, S_ij, z, limitación alfa | ✅ Completa (ampliada 22 ago. 2026) |
| §2.2.3 Modelo de radiación | Eqs. probabilidad + flujo, variantes Ren/Kang/Yang, limitación intraurbana | ✅ Completa (ampliada 22 ago. 2026) |
| §2.3 Aprendizaje profundo | Eq. feedforward (`eq:feedforward`), LeakyReLU, aplicaciones | ✅ Completa |
| §2.4 Deep Gravity | Eqs. GLM→DG, arquitectura, 39 features, CPC, resultados, tabla comparativa | ✅ Completa (tabla agregada 23 ago. 2026) |
| §2.5 XAI | Eq. SHAP (`eq:shap`), 3 propiedades, Integrated Gradients (`eq:ig`) | ✅ Completa |
| §2.6 OpenStreetMap | Modelo de datos, amenities, cobertura heterogénea en Santiago | ✅ Completa |
| §2.7 Contexto Santiago | EOD 2012/2017, DTPM Nov 2024, 3.6M viajes | ✅ Completa |

---

## 2. Tabla comparativa de modelos (agregada 23 ago. 2026)

La tabla `tab:comparacion_modelos` al final de §2.4 compara 5 modelos en 5 dimensiones:

| Modelo | Variables urbanas | Libre de parámetros | Escala intraurbana | XAI | LatAm |
|---|:---:|:---:|:---:|:---:|:---:|
| Gravitatorio | No | No | Parcial | No | Parcial |
| IO Model | No | No | Parcial | No | No |
| Radiación | No | Sí | No | No | No |
| Mod. avanz. IO | No | Sí | Sí | No | No |
| **Deep Gravity** | **Sí** | No | **Sí** | **Sí** | †(esta memoria) |

---

## 3. Bibliografía cubierta en el capítulo

| Clave | Sección |
|---|---|
| `zipf1946p` | §2.2.1 |
| `stouffer1940intervening` | §2.2.2 |
| `liu2020intervening` | §2.2.2 |
| `simini2012universal` | §2.2.3 |
| `ren2014predicting` | §2.2.3 |
| `kang2015generalized` | §2.2.3 |
| `yang2014limits` | §2.2.3 |
| `yan2014population` | §2.2.3 |
| `liu2024interdisciplinary` | §2.1, §2.2.1, §2.3 |
| `simini2021deep` | §2.3, §2.4 |
| `luca2024tsmob` | §2.3 |
| `lundberg2017shap` | §2.5 |
| `sundararajan2017axiomatic` | §2.5 |
| `haklay2008openstreetmap` | §2.6 |
| `BarringtonLeigh2017` | §2.6 |
| `dtpm_informe` | §2.7 |

---

## 4. Material reservado para Cap. 4 — Propuesta de Solución

| Contenido | Sección sugerida en Cap. 4 | Detalle |
|---|---|---|
| Actores y usuarios (DTPM, SECTRA, MTT, municipalidades, universidades, empresas) | Actores y usuarios | Sección completa lista para desarrollar |
| Alcances (área: Gran Santiago; período: nov. 2024; modos: DTPM; modelos: Deep Gravity + baselines; features: OSM; XAI: SHAP) | Alcance metodológico | Lista detallada |
| Fuera de alcance (predicción temporal, calibración de políticas, datos telco, modos no observados) | Limitaciones del estudio | Lista de exclusiones explícitas |
| Justificación — 5 puntos (volatilidad post-pandemia, costo EOD, modelos lineales, opacidad, escasez LatAm) | Justificación metodológica | Expandir con consecuencias concretas |

---

## 5. Trazabilidad vs. capítulos anteriores

| Elemento | Introducción | Marco Conceptual | Estado |
|---|:---:|:---:|---|
| Contexto movilidad | ✅ condensado | ✅ desarrollado | OK |
| Modelo gravitatorio | ✅ mención | ✅ con ecuaciones | OK |
| IO Model | ✅ mención | ✅ con eq. formal | OK |
| Modelo de radiación | ✅ mención | ✅ con variantes | OK |
| Modelos avanzados IO (PWO, Universal) | ❌ | ✅ en Cap. 3 §3.3 | OK |
| Deep Gravity — técnico | ✅ condensado | ✅ completo | OK |
| Tabla comparativa modelos | ❌ | ✅ tab:comparacion_modelos | OK (23 ago.) |
| Brecha de investigación | ✅ condensado | ✅ §2.4 + §2.6-2.7 | OK |
| XAI / SHAP | ✅ introducido | ✅ §2.5 con ecuaciones | OK |
| Contexto latinoamericano | ✅ breve | ✅ §2.6 + §2.7 | OK |
| Datos DTPM Nov 2024 | ✅ mencionado | ✅ §2.7 | OK |
