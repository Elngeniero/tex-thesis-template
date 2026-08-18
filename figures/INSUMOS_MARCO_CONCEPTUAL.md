# Insumos consolidados para el Marco Conceptual

> Este documento unifica el contenido de `analisis_contenido_v1.md` (inventario de
> contenido reutilizable) y `MARCO_CONCEPTUAL_modelos_movilidad_y_deep_gravity.md`
> (prosa redactada de modelos). Sirve como base de redacción para `marco_conceptual.tex`.
>
> Introducción y Definición del Problema están **terminadas** (✅). No modificar.

---

## 1. Mapa de contenido para el Marco Conceptual

Inventario de temas que deben desarrollarse en `marco_conceptual.tex`, con su origen y estado:

| Contenido | Sección en Marco Conceptual | Estado | Origen |
|-----------|----------------------------|--------|--------|
| Modelo gravitacional: formalización, ecuación, historia (Zipf 1946, Erlander & Stewart 1990) + 4 limitaciones en `enumerate` | Modelo gravitacional clásico | 📝 Prosa lista (ver §2.1) | def_problema v0 + MARCO_CONCEPTUAL §1 |
| Modelo de oportunidades intermedias (Stouffer, 1940): fundamentos y limitaciones | Modelos clásicos | 📝 Prosa lista (ver §2.2) | introduccion_v1 + MARCO_CONCEPTUAL §2 |
| Modelo de radiación (Simini et al., 2012): enfoque libre de parámetros; sobreestimación viajes cortos | Modelos clásicos | 📝 Prosa lista (ver §2.3) | introduccion_v1 + MARCO_CONCEPTUAL §3 |
| Deep Gravity: arquitectura (15 capas, LeakyReLU, softmax), 39 variables OSM, entrenamiento (RMSprop) | Deep Gravity | 📝 Prosa lista (ver §2.4) | def_problema v0 + MARCO_CONCEPTUAL §4 |
| Deep Gravity: capacidades técnicas (variables sin forma funcional, relaciones no lineales, generalización) | Deep Gravity | ⬜ Pendiente de redactar | introduccion_v1 |
| Métricas de evaluación: CPC, divergencia Kullback-Leibler, correlación de Pearson | Métricas / Evaluación | ⬜ Pendiente de redactar | introduccion_v1 |
| Resultados cuantitativos: +66% Italia, +246% Inglaterra, +1.076% NY en CPC vs. gravitacional | Deep Gravity — resultados | 📝 Prosa lista (ver §2.4) | introduccion_v1 + MARCO_CONCEPTUAL §4 |
| Tabla comparativa: gravity, radiation, Deep Gravity, GNNs, SECTRA/DTPM (columnas: Amenities OSM, Explicable, Validado LatAm) | Estado del arte | ⬜ Pendiente de redactar | def_problema v0 |
| Brecha entre capacidad predictiva y explicabilidad en modelos DL; rol de XAI / SHAP | Explicabilidad / XAI | ⬜ Pendiente de redactar | introduccion_v1 |
| Segregación socioeconómica LatAm, transporte informal, cobertura OSM heterogénea | Contexto latinoamericano | ⬜ Pendiente + citas (ver §2.6) | MARCO_CONCEPTUAL §5 |

---

## 2. Contenido redactado por sección

### 2.1 Modelo gravitacional clásico

El modelo de gravedad clásico asume que el flujo entre dos zonas es
proporcional al producto de sus poblaciones e inversamente proporcional a
una función de la distancia que las separa (Zipf, 1946) \cite{zipf1946p}.

Limitaciones documentadas en la literatura \cite{zipf1946p, simini2012universal, liu2024interdisciplinary}:

- Impone relaciones paramétricas monótonas entre población, distancia y
  flujo, lo que genera un ajuste deficiente ante fenómenos no lineales
  (ej. subcentros de empleo, corredores de transporte masivo).
- Requiere calibración manual para cada contexto geográfico, limitando su
  transferibilidad entre ciudades.
- No incorpora el tejido urbano (puntos de interés, uso de suelo,
  infraestructura de transporte) como variables explicativas.

> **Nota de redacción:** Ampliar con la formalización matemática (ecuación con
> exponentes α, β, γ) y cita a Erlander & Stewart (1990). Las 4 limitaciones
> pueden formatearse como `\begin{enumerate}` en LaTeX.

---

### 2.2 Modelo de oportunidades intermedias (Stouffer, 1940)

Propone que el número de personas que se desplazan a una distancia dada es
directamente proporcional al número de oportunidades a esa distancia, e
inversamente proporcional al número de oportunidades intervinientes más
cercanas al origen \cite{stouffer1940intervening}. A diferencia del modelo
gravitacional, no depende explícitamente de la distancia geográfica sino
del concepto de "oportunidades acumuladas".

> **Nota de redacción:** Añadir descripción conceptual y limitaciones prácticas
> (dificultad de operacionalizar "oportunidades" en ausencia de datos detallados).

---

### 2.3 Modelo de radiación (Simini et al., 2012)

Modelo sin parámetros libres, derivado por analogía con procesos físicos de
radiación y absorción \cite{simini2012universal}. Predice los flujos de
commuting a partir únicamente de la población de origen, destino, y la
población contenida en un radio entre ambos. Ha demostrado buen desempeño
prediciendo diferencias de flujo entre pares de zonas con poblaciones y
distancias similares, un caso donde el modelo gravitacional falla
(ejemplo del paper: condados de Utah vs. Alabama).

> **Nota de redacción:** Mencionar explícitamente la sobreestimación de viajes
> cortos y subestimación de viajes largos como limitación del modelo de radiación.

---

### 2.4 Deep Gravity (Simini et al., 2021)

Deep Gravity \cite{simini2021deep} combina la estructura del modelo
gravitacional con una red neuronal profunda entrenada sobre variables
geoespaciales derivadas de OpenStreetMap (OSM). Estas variables incluyen:

- Uso de suelo (5 features): residencial, comercial, industrial, retail, natural.
- Red vial (3 features): longitud de vías residenciales, principales y otras.
- Transporte, comida, salud, educación, retail (2 features cada una: POIs
  y edificios asociados).
- Distancia geográfica entre origen y destino.
- Población de origen y destino.

En total, cada flujo se describe mediante 39 features (18 del origen, 18
del destino, distancia, y ambas poblaciones).

**Arquitectura:** red feed-forward de 15 capas ocultas (256 unidades en las
primeras 6 capas, 128 en las restantes), activación LeakyReLU, salida
mediante softmax. Entrenada con RMSprop (momentum 0.9, lr=5e-6),
negative sampling de hasta 512 destinos por origen.

**Validación:** el modelo fue evaluado sobre Inglaterra, Italia y el estado
de Nueva York, mostrando mejoras de hasta 246% (Inglaterra), 66% (Italia) y
1076% (Nueva York) en CPC respecto al modelo de gravedad clásico en las
regiones más densamente pobladas. También demostró buena capacidad de
generalización geográfica (esquema *leave-one-city-out*).

**Explicabilidad:** los autores originales usan SHAP para análisis global y
local de las predicciones, encontrando que la importancia relativa de
población vs. distancia vs. amenities varía entre países (en Inglaterra
domina el tejido urbano; en Italia y NY dominan población y distancia).

**Brecha identificada:** Deep Gravity no ha sido validado en una
metrópolis latinoamericana ni sobre datos posteriores a la pandemia de
COVID-19, condiciones bajo las cuales tanto los patrones de movilidad como
la cobertura y calidad de OSM difieren de los contextos de validación
original.

> **Nota de redacción:** Añadir la sección de capacidades técnicas del modelo
> (incorporar variables sin forma funcional a priori, aprender relaciones no
> lineales, generalizar a nuevas áreas). Estas estaban en `introduccion_v1` y
> no fueron incluidas en la introducción final.

---

### 2.5 Explicabilidad / XAI

> **⬜ Pendiente de redactar.**
>
> Contenido a desarrollar:
> - Brecha entre capacidad predictiva y explicabilidad en modelos de DL.
> - Rol de XAI en sistemas de decisión pública (planificación del transporte).
> - SHAP (SHapley Additive exPlanations): fundamento teórico, tipos (Kernel SHAP,
>   Deep SHAP), interpretación de valores de importancia global y local.
> - Relación con los objetivos específicos 5 y 6 de esta memoria.

---

### 2.6 Especificidad del contexto latinoamericano

> **⬜ Pendiente de citas verificadas.**
>
> Puntos a desarrollar, con literatura de VGI y transporte en LatAm:

- Segregación socioeconómica pronunciada y su efecto en patrones de
  movilidad asimétricos.
- Coexistencia de sistemas de transporte formales e informales
  (colectivos, taxis informales).
- Concentración poblacional en zonas periféricas con menor oferta de
  servicios y, por tanto, menor densidad de amenities registradas en OSM.
- Cobertura heterogénea de OpenStreetMap: mayor densidad de mapeo en zonas
  de ingresos medios-altos, menor en periferias — fenómeno documentado para
  VGI en el Sur Global en términos generales, pero que requiere respaldo
  específico para Chile/Santiago.

**Fuentes candidatas a revisar** (no verificadas, requieren lectura antes de citar):
- Estudios sobre completitud global de OSM (ej. líneas de trabajo de
  Barrington-Leigh & Millard-Ball). → ya está en `bibliografia.bib` como `\cite{BarringtonLeigh2017}`.
- Snapshot Geofabrik Chile: podría servir como referencia empírica de cobertura
  si se hace un análisis de densidad de POIs por comuna.

---

## 3. Contenido para otras secciones (no Marco Conceptual)

Este contenido proviene de versiones anteriores de la Definición del Problema y está
reservado para la **Propuesta de Solución** (`propuesta_de_solucion.tex`).
Ya está parcialmente en comentarios TODO de ese archivo.

### Para `propuesta_de_solucion.tex`

| Contenido | Sección sugerida | Detalle |
|-----------|-----------------|---------|
| Actores y usuarios involucrados (DTPM, SECTRA, MTT, municipalidades, universidades, empresas) | Actores y usuarios | Sección completa lista para reubicar |
| Alcances (área geográfica: Gran Santiago; período: nov. 2024; modos: dataset DTPM; modelos: DG + baselines; features: OSM original + extensiones LatAm; técnicas XAI: SHAP) | Alcances | Lista detallada de alcances |
| Fuera de alcance (predicción temporal, calibración de políticas, datos de telco, modos no observados, otros modelos neuronales) | Limitaciones | Lista de exclusiones explícitas |
| Justificación del problema — 5 puntos (volatilidad post-pandemia, costo EOD, modelos lineales, opacidad, escasez en LatAm) | Justificación | Puntos sobre consecuencias concretas pueden expandirse |

---

## 4. Trazabilidad: estado de la introducción (referencia)

Tabla de referencia para no duplicar contenido con `introduccion.tex` (terminada).

| Elemento | ¿En introducción final? | Acción |
|----------|:-----------------------:|--------|
| Contexto general de movilidad | ✅ (condensado) | Ninguna |
| Modelo gravitacional | ✅ (condensado) | Expandir en §2.1 |
| Limitaciones del modelo gravitacional | ✅ (breve) | Expandir en §2.1 |
| Modelos alternativos (radiación, Stouffer) | ✅ (mención breve) | Expandir en §2.2 y §2.3 |
| Deep Gravity — descripción técnica | ✅ (condensado) | Expandir en §2.4 |
| Deep Gravity — capacidades detalladas | ❌ | Desarrollar en §2.4 |
| Brecha de investigación (lista) | ✅ (condensado) | Ya en def. problema ✅ |
| Datos disponibles (EOD, OSM) | ✅ (breve) | Ya en def. problema ✅ |
| XAI / SHAP | ✅ (introducido) | Expandir en §2.5 |
