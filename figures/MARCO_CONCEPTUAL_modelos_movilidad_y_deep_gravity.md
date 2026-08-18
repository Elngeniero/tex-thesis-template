# Insumos para Marco Conceptual: modelos de movilidad y Deep Gravity

> Este material fue extraído de las versiones anteriores de Introducción y
> Definición del Problema para evitar solapamiento. Está pensado como base
> de redacción para la sección de Marco Conceptual que cubre los modelos
> gravitacional, de oportunidades intermedias, de radiación y Deep Gravity.

## 1. Modelo gravitacional clásico

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

## 2. Modelo de oportunidades intermedias (Stouffer, 1940)

Propone que el número de personas que se desplazan a una distancia dada es
directamente proporcional al número de oportunidades a esa distancia, e
inversamente proporcional al número de oportunidades intervinientes más
cercanas al origen \cite{stouffer1940intervening}. A diferencia del modelo
gravitacional, no depende explícitamente de la distancia geográfica sino
del concepto de "oportunidades acumuladas".

## 3. Modelo de radiación (Simini et al., 2012)

Modelo sin parámetros libres, derivado por analogía con procesos físicos de
radiación y absorción \cite{simini2012universal}. Predice los flujos de
commuting a partir únicamente de la población de origen, destino, y la
población contenida en un radio entre ambos. Ha demostrado buen desempeño
prediciendo diferencias de flujo entre pares de zonas con poblaciones y
distancias similares, un caso donde el modelo gravitacional falla
(ejemplo del paper: condados de Utah vs. Alabama).

## 4. Deep Gravity (Simini et al., 2021)

Deep Gravity \cite{simini2021deep} combina la estructura del modelo
gravitacional con una red neuronal profunda entrenada sobre variables
geoespaciales derivadas de OpenStreetMap (OSM). Estas variables incluyen:

- Uso de suelo (5 features): residencial, comercial, industrial, retail,
  natural.
- Red vial (3 features): longitud de vías residenciales, principales y
  otras.
- Transporte, comida, salud, educación, retail (2 features cada una: POIs
  y edificios asociados).
- Distancia geográfica entre origen y destino.
- Población de origen y destino.

En total, cada flujo se describe mediante 39 features (18 del origen, 18
del destino, distancia, y ambas poblaciones).

**Arquitectura**: red feed-forward de 15 capas ocultas (256 unidades en las
primeras 6 capas, 128 en las restantes), activación LeakyReLU, salida
mediante softmax. Entrenada con RMSprop (momentum 0.9, lr=5e-6),
negative sampling de hasta 512 destinos por origen.

**Validación**: el modelo fue evaluado sobre Inglaterra, Italia y el estado
de Nueva York, mostrando mejoras de hasta 246% (Inglaterra), 66% (Italia) y
1076% (Nueva York) en CPC respecto al modelo de gravedad clásico en las
regiones más densamente pobladas. También demostró buena capacidad de
generalización geográfica (esquema *leave-one-city-out*).

**Explicabilidad**: los autores originales usan SHAP para análisis global y
local de las predicciones, encontrando que la importancia relativa de
población vs. distancia vs. amenities varía entre países (en Inglaterra
domina el tejido urbano; en Italia y NY dominan población y distancia).

**Brecha identificada**: Deep Gravity no ha sido validado en una
metrópolis latinoamericana ni sobre datos posteriores a la pandemia de
COVID-19, condiciones bajo las cuales tanto los patrones de movilidad como
la cobertura y calidad de OSM difieren de los contextos de validación
original.

## 5. Especificidad del contexto latinoamericano (pendiente de citas)

Puntos a desarrollar en Marco Conceptual, con literatura de VGI y
transporte en LatAm (buscar y completar citas reales):

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

**Fuentes candidatas a revisar** (no verificadas, requieren lectura antes
de citar):
- Estudios sobre completitud global de OSM (ej. líneas de trabajo de
  Barrington-Leigh & Millard-Ball).
- Snapshot Geofabrik Chile, ya mencionado en
  `ALCANCE_Y_LINEAMIENTOS_TESIS.md` como fuente de datos, podría servir
  también como referencia empírica de cobertura si se hace un análisis de
  densidad de POIs por comuna.