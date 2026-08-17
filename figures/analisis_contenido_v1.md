# Análisis de Contenido Reutilizable

## Resumen

Se analizaron dos archivos: `introduccion_v1.tex` (versión preliminar de la introducción) y `definicion_del_problema.tex` (versión original, antes de la refactorización del 17/08/2026), para identificar contenido que fue descartado o condensado pero que puede reutilizarse en otras secciones de la memoria.

---

## 1. Contenido reutilizable de `introduccion_v1.tex`

### Para el Marco Conceptual (`marco_conceptual.tex`)

| Contenido | Sección sugerida |
|-----------|-----------------|
| Descripción detallada del modelo de oportunidades intermedias (Stouffer, 1940) y modelo de radiación (Simini et al., 2012), incluyendo sus fundamentos y limitaciones | Modelos clásicos de movilidad |
| Capacidades técnicas de Deep Gravity en formato de lista (incorporar variables sin forma funcional a priori, aprender relaciones no lineales, generalizar a nuevas áreas) | Deep Gravity / Aprendizaje Profundo |
| Métricas de evaluación: divergencia de Kullback-Leibler, CPC, correlación de Pearson | Métricas de evaluación |
| Resultados cuantitativos: mejoras de 66% (Italia), 246% (Inglaterra), 1.076% (NY) respecto al gravitacional | Deep Gravity — resultados reportados |
| Brecha entre capacidad predictiva y explicabilidad en modelos de DL; rol de XAI | Explicabilidad / XAI |

### Para la Definición del Problema (ya incorporado)

| Contenido | Estado |
|-----------|--------|
| Brecha de investigación (4 factores diferenciadores de LatAm) | ✅ Incorporado en nueva def. problema |
| Datos disponibles (EOD 2012, bip!, OSM) | ✅ Incorporado en nueva def. problema |
| Objetivos detallados | ✅ Reformulados como objetivos específicos |

---

## 2. Contenido reutilizable de `definicion_del_problema.tex` (versión original)

La versión original del archivo (~7 páginas) fue condensada a ~4 páginas. El contenido removido se puede reubicar según la siguiente tabla:

### Para el Marco Conceptual (`marco_conceptual.tex`)

| Contenido | Sección sugerida | Detalle |
|-----------|-----------------|---------|
| Descripción del modelo gravitacional (formalización, ecuación, historia) con citas a Zipf (1946) y Erlander & Stewart (1990) | Modelo gravitacional | Incluir las 4 limitaciones en formato `enumerate` |
| Modelo de radiación (Simini et al., 2012) con descripción de su enfoque libre de parámetros | Modelo de radiación | Mencionar sobreestimación de viajes cortos y subestimación de largos |
| Teoría de oportunidades intervinientes (Stouffer, 1940) | Modelos alternativos | Descripción conceptual y limitaciones prácticas |
| Descripción técnica de Deep Gravity (red feed-forward, 15 capas, LeakyReLU, 39 variables OSM) | Deep Gravity | Detalle de arquitectura y variables de entrada |
| Tabla comparativa de soluciones existentes (gravity, radiation, DG, GNNs, SECTRA/DTPM) | Estado del arte | Tabla con columnas: Tipo, Amenities OSM, Explicable, Validado en LatAm |

### Para la Propuesta de Solución (`propuesta_de_solucion.tex`)

| Contenido | Sección sugerida | Detalle |
|-----------|-----------------|---------|
| Actores y usuarios involucrados (DTPM, SECTRA, MTT, municipalidades, universidades, empresas) | Actores y usuarios | Sección completa lista para reubicar |
| Alcances (área geográfica, período temporal, modos, modelos, features, técnicas XAI) | Alcances | Lista detallada de alcances |
| Fuera de alcance (predicción temporal, calibración de políticas, datos de telco, otros modelos) | Limitaciones | Lista de exclusiones explícitas |
| Justificación del problema — 5 puntos (volatilidad post-pandemia, costo EOD, modelos lineales, opacidad, escasez en LatAm) | Justificación | Parcialmente incorporado en la nueva def. problema; los puntos sobre consecuencias concretas pueden expandirse |

---

## 3. Estado del contenido en `introduccion.tex` (versión final)

| Elemento | ¿En v1? | ¿En versión final? | Acción recomendada |
|----------|:-------:|:-------------------:|---|
| Contexto general de movilidad | ✅ | ✅ (condensado) | Ninguna |
| Modelo gravitacional | ✅ | ✅ (condensado) | Expandir en marco conceptual |
| Limitaciones del modelo gravitacional | ✅ | ✅ (breve) | Expandir en marco conceptual |
| Modelos alternativos (radiación, Stouffer) | ✅ | ✅ (mención breve) | Expandir en marco conceptual |
| Deep Gravity — descripción técnica | ✅ | ✅ (condensado) | Expandir en marco conceptual |
| Deep Gravity — capacidades detalladas | ✅ | ❌ | Mover a marco conceptual |
| Brecha de investigación (lista) | ✅ | ✅ (condensado) | Ya en def. problema |
| Datos disponibles (EOD, OSM) | ✅ | ✅ (breve) | Ya en def. problema |
| Objetivos detallados | ✅ | ❌ | Ya en def. problema |
| XAI / SHAP | ❌ | ✅ (introducido) | Expandir en marco conceptual |

## Recomendación General

La redistribución del contenido sigue esta lógica:

1. **Marco Conceptual**: Todos los detalles técnicos de modelos (gravitacional, radiación, Stouffer, Deep Gravity), métricas, arquitectura de redes neuronales, y técnicas XAI.
2. **Definición del Problema**: Contexto de Santiago, brecha de investigación, formulación del problema, árbol, objetivos. (✅ Ya completado)
3. **Propuesta de Solución**: Actores y usuarios, alcances, limitaciones, metodología.
