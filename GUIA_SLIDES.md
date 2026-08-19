# Guía de armado de las diapositivas — Grupo 07

> Para rearmar la presentación en tu propia plantilla de Google Slides.
> Cada diapositiva indica **qué va en cada posición**, el **texto literal**, la **figura** y
> **su interpretación**.
>
> El archivo `TP_presentacion_G07.pptx` ya tiene todo esto armado: podés importarlo y
> retocar, o usar esta guía para rehacerlo a mano.

---

## Estructura general

**Carátula + 7 diapositivas.** El orden sigue los bloques del enunciado, que es el orden en
que la cátedra los evalúa.

| # | Etiqueta | Título | Figuras |
|---|---|---|---|
| — | | **Carátula** | — |
| 1 | 01 · IDENTIFICACIÓN DEL DATASET | Qué contiene y de dónde viene | — |
| 2 | 02 · EXPLORACIÓN Y VISUALIZACIÓN | Patrones temporales de uso | `02`, `01` |
| 3 | 03 · CALIDAD DE LOS DATOS | Datos faltantes y su clasificación | `06` (opcional) |
| 4 | 04 · CALIDAD DE LOS DATOS | Errores, valores atípicos y asimetría | `03`, `07` |
| 5 | 05 · PROBLEMA DE ML Y PREPARACIÓN | Variable objetivo y flujo de preparación | `09` |
| 6 | 06 · REDUCCIÓN DE DIMENSIONALIDAD | Selección de features: relevancia y redundancia | `10`, `11` |
| 7 | 07 · RESULTADO Y CIERRE | PCA, datasets finales y conclusiones | `12` |

> ⚠️ **La consigna dice «5 diapositivas como máximo».** Vamos a 7. En el PDF compartido el
> Grupo 1 usó 8 y el Grupo 9 usó 6, así que hay precedente, pero es una decisión consciente.
> Si preferís ajustarte al máximo: fusioná las diapositivas 3 y 4 (calidad de datos) y las 6
> y 7 (reducción).

## Plantilla de cada diapositiva

```
┌──────────────────────────────────────────────────────────────┐
│ ▔▔▔▔▔▔▔▔ franja azul de 2 mm ▔▔▔▔▔▔▔▔                        │
│ 01 · ETIQUETA DE SECCIÓN                        [ GRUPO 07 ] │
│ Título descriptivo de la diapositiva                         │
│                                                              │
│ ███ Banda azul oscuro: el concepto clave, en 2 líneas ███    │
│                                                              │
│              [ figura ]            [ figura ]                │
│                                                              │
│ Columna 1            Columna 2            Columna 3          │
│ título en negrita    título en negrita    título en negrita  │
│ interpretación       interpretación       interpretación     │
│                                                              │
│ HVFHS · Nueva York · Agosto 2025                       n / 7 │
└──────────────────────────────────────────────────────────────┘
```

**Paleta:** azul `#3B82F6` · azul oscuro `#1D4ED8` · azul muy oscuro `#0F2C6B` ·
tinta `#0F172A` · gris `#64748B` · coral `#E85D6B` · verde `#109B76` · ámbar `#C2760C`

---

# CARÁTULA

**Izquierda (bloque azul oscuro, 4,5" de ancho):**

```
CEIA · FIUBA
Análisis
de Datos
Trabajo Práctico Integrador
3B 2026
```

**Derecha:**

```
Uso de High-Volume
For-Hire Services (HVFHS)
en USA · Agosto 2025          ← esta línea en azul

Análisis exploratorio y preparación de datos para un problema
de Machine Learning supervisado

[ G R U P O   0 7 ]           ← badge azul

PRESENTADO POR
Silvert Kevin QUISPE PACOMPIA

┌────────────────────────────┐
│ REPOSITORIO                │
│ github.com/SilvertK164/    │
│ ceia-analisis-datos-tp-    │
│ hvfhs                      │
└────────────────────────────┘
```

> ⚠️ El link al repositorio es **obligatorio** según la consigna, y en tu carátula actual no
> está.

---

# DIAPOSITIVA 1 — Qué contiene y de dónde viene

**Etiqueta:** `01 · IDENTIFICACIÓN DEL DATASET`

**Banda:**
> **Registro oficial de viajes de alto volumen en Nueva York**
> Cada fila es un viaje despachado por Uber o Lyft: cuándo se pidió, cuándo subió el
> pasajero, cuánto duró, cuánto costó y cuánto cobró el conductor.

**Cuatro tarjetas de dato, en fila:**

| 19.271.461 | 25 | 70,4 % | 29,6 % |
|---|---|---|---|
| viajes registrados | variables por viaje | Uber (HV0003) | Lyft (HV0005) |

**Tres columnas:**

**Origen y ventana temporal**
- Datos publicados por la Comisión de Taxis y Limusinas de Nueva York (TLC), con un
  diccionario oficial que define cada columna.
- Se eligió agosto de 2025. El año completo son unos 240 millones de filas en 12 archivos de
  480 MB, y trabajar con un solo mes fue sugerencia de la cátedra.
- Agosto por sí solo supera los 19 millones de viajes: alcanza para todas las consignas.

**Tipos de variable** *(Clase 1, slides 37-38)*
- 11 cuantitativas: distancia, duración, tarifa base, peajes, impuestos, recargos, propina y
  pago al conductor.
- 14 categóricas: la empresa, las dos bases, las zonas de origen y destino, las cuatro
  marcas de tiempo y los cinco indicadores de sí/no.
- Las variables binarias son un caso particular de las categóricas nominales.

**Una corrección necesaria**
- `PULocationID` y `DOLocationID` vienen guardadas como números enteros, pero no son
  cantidades: son etiquetas de zona.
- La zona 138 no es «más» que la zona 69. Tratarlas como numéricas haría que el modelo les
  asigne un orden que no existe.
- Las reclasificamos como categóricas nominales antes de seguir.

> 📌 **Ojo:** en tu diapositiva anterior decía «24 variables · 11 cuantitativas · 13
> categóricas». El conteo correcto es **25 = 11 + 14**.

---

# DIAPOSITIVA 2 — Patrones temporales de uso

**Etiqueta:** `02 · EXPLORACIÓN Y VISUALIZACIÓN`

**Banda:**
> **Cada gráfico se eligió según el tipo de variable**
> Barras para las categóricas, líneas para lo que evoluciona en el tiempo, histograma para
> las numéricas y boxplot para comparar una numérica entre grupos.

**Figuras, lado a lado, 2,25" de alto:**

| Izquierda | Derecha |
|---|---|
| `02_viajes_por_dia_semana.png` | `01_viajes_por_hora.png` |

**Tres columnas:**

**Patrón semanal**
- Sábado 3.538.584 viajes (18,4 %) contra lunes 2.134.937 (11,1 %): el sábado concentra un
  66 % más.
- El orden de los días es creciente de lunes a sábado, sin excepciones.

**Patrón horario**
- El mínimo es a las 3 de la mañana, con 302.466 viajes, y el máximo a las 18 h, con
  1.118.439.
- Hay un repunte matinal a las 8-9 h, pero es mucho menor que el vespertino, y la actividad
  sigue alta pasada la medianoche.

**Qué se concluye**
- Los dos patrones apuntan a lo mismo: el servicio se usa para ocio, no para ir a trabajar.
  Si fuera laboral, el pico estaría entre semana y a la mañana.
- La demanda está muy repartida: 262 zonas de origen y ninguna supera el 2,2 %.

---

# DIAPOSITIVA 3 — Datos faltantes y su clasificación ⭐

**Etiqueta:** `03 · CALIDAD DE LOS DATOS`

**Banda:**
> **La columna `originating_base_num` está vacía en el 29,5 % de los registros**
> No alcanza con contarlos: hay que determinar de qué tipo son, porque de eso depende el
> tratamiento. Aplicamos el método de la Clase 3, slide 55.

**Tres pasos numerados, en fila:**

| ① Descartar MCAR | ② Evaluar si es estructural | ③ Clasificar como MAR |
|---|---|---|
| Agrupar de distintas maneras y comparar | Consultar la documentación de recolección | Se explica por otra columna: la empresa |

**Columna izquierda — tabla + resultado:**

| Agrupando por | % de faltantes |
|---|---|
| día de la semana | 28 % – 31 % |
| viaje compartido | parejo |
| **empresa: Uber** | **0,00 %** |
| **empresa: Lyft** | **99,64 %** |

> **Resultado.** Es MCAR solo si el porcentaje es parejo al agrupar de distintas maneras.
> Con la empresa no lo es en absoluto: se descarta MCAR.

**Columna central — Lo que dice la documentación**
- El diccionario del TLC define el campo como *«Base number of the base that received the
  original trip request»*, y nada más.
- No menciona a Lyft, así que la documentación no confirma que sea estructural.
- Lo verificamos contra los datos: si el dato no existiera, debería faltar en el 100 % de
  los viajes de Lyft.
- Encontramos que **Lyft sí lo informa en 20.348 viajes**, el 0,36 % de los suyos. El dato
  existe. **No es estructural.**

**Columna derecha — Clasificación final: MAR**
- Queda la definición de la Clase 3 slide 52: *«la falta del valor se relaciona con los
  datos de otras columnas»*. Esa columna es la empresa.
- Es el mismo esquema que el ejemplo de la clase, donde el sueldo faltaba según la edad del
  encuestado.
- Tratamiento: se descarta la columna, pero **por redundante y no por estructural**. Saber
  que falta equivale a saber que el viaje es de Lyft, y eso ya lo informa `empresa`.

*(Figura opcional si sobra lugar: `06_mapa_faltantes.png`)*

---

# DIAPOSITIVA 4 — Errores, valores atípicos y asimetría

**Etiqueta:** `04 · CALIDAD DE LOS DATOS`

**Banda:**
> **Un error y un valor atípico no son lo mismo, y no se tratan igual**
> El error es un valor imposible y se detecta con conocimiento del dominio. El outlier es
> raro pero posible y se detecta con estadística.

**Figuras, apiladas a la izquierda (5,8" de ancho):**

| Arriba | `03_distribucion_distancia_log.png` |
|---|---|
| Abajo | `07_boxplots_outliers.png` |

**Derecha arriba, dos columnas:**

**Errores encontrados**
- espera negativa: 1,164 %
- tarifa igual a cero: 0,962 %
- tarifa negativa: 772 casos
- distancia o duración cero
- Se eliminan: son imposibles. En total se depuró el 2,12 % de las filas.

**Outliers que se conservan**
- Los viajes de más de 100 millas existen: son traslados a otros estados.
- Las tarifas altas corresponden a esos viajes largos.
- Eliminarlos sería perder información válida.

**Derecha abajo, ancho completo:**

**Por qué recortamos por percentil y no por el criterio IQR**
- El método IQR de la Clase 3 marca como atípico todo lo que quede fuera de `Q1 − 1,5×IQR`
  y `Q3 + 1,5×IQR`. Aplicado acá señala entre el 4,5 % y el 7 % de cada variable, es decir
  cientos de miles de viajes perfectamente válidos.
- El motivo es que **el IQR supone una distribución aproximadamente simétrica**, y el
  gráfico de arriba muestra que las nuestras no lo son: en escala normal todo se amontona
  contra el eje, y recién en escala logarítmica aparece la forma real.
- Por eso el IQR se usa como diagnóstico, y para el tratamiento se recorta al percentil 99.

---

# DIAPOSITIVA 5 — Variable objetivo y flujo de preparación

**Etiqueta:** `05 · PROBLEMA DE ML Y PREPARACIÓN`

**Banda:**
> **Problema planteado: clasificación binaria · ¿el pasajero dejará propina?**
> Variable objetivo `dio_propina = tips > 0`. Se predeciría al terminar el viaje, cuando ya
> se conocen la distancia, la duración, la tarifa y las zonas.

**Diagrama de flujo horizontal** (el primer bloque en azul oscuro, «Balancear» en coral):

```
[SPLIT 80/20] ▸ Nulos ▸ Outliers ▸ Discretizar ▸ Codificar ▸ Escalar ▸ [Balancear] ▸ Reducir
```

Debajo, en gris chico:
> Sobre TRAIN se calcula y se aplica · sobre TEST solo se aplica · el balanceo no se hace
> sobre TEST *(Clase 7, slides 5 y 26)*

**Figura:** `09_balanceo_clases.png` (izquierda, 1,72" de alto)

**Debajo de la figura:**

**Por qué el split va antes que todo lo demás** *(Clase 5, slide 5)*
- *«Si usáramos el dataset completo cuando hacemos una transformación, estaríamos
  contaminando el dataset de entrenamiento con pistas de los datos de test.»* TRAIN quedó en
  800.000 filas y TEST en 200.000, con la clase positiva en 18,625 % en ambos: la
  estratificación funcionó.

**Columna central:**

**Decisiones de transformación**
- Faltantes: descartar la columna redundante.
- Outliers: recorte al percentil 99.
- hora y día: codificación cíclica con seno y coseno, para que las 23 h y las 0 h queden
  contiguas.
- Zonas: frequency encoding. Con one-hot, 262 categorías darían más de 500 columnas
  *(Clase 4, slide 42)*.
- Escalado: estandarización, que es la que PCA requiere.

**Columna derecha:**

**Balance de clases**
- La target está desbalanceada 18,5 % contra 81,5 %, una relación de 1 a 4,4.
- No es extremo: la Clase 5 slide 27 reserva ese término para casos de 1 a 1000.
- Comparamos SMOTE con undersampling y elegimos undersampling, porque con 800.000 filas de
  entrenamiento sobran datos y no hace falta generar filas sintéticas.
- TEST conserva la proporción real para que las métricas sean honestas.

---

# DIAPOSITIVA 6 — Selección de features: relevancia y redundancia

**Etiqueta:** `06 · REDUCCIÓN DE DIMENSIONALIDAD`

**Banda:**
> **Dos criterios para descartar variables** *(Clase 7, slide 7)*
> Se buscan las que dicen lo mismo que otra (redundancia) y las que no aportan nada sobre la
> variable objetivo (relevancia).

**Figuras:**

| Izquierda arriba (5,66 × 2,0") | Derecha (3,52 × 3,15") |
|---|---|
| `10_matriz_correlacion.png` | `11_relevancia_features.png` |

**Columna arriba al centro:**

**Resultado: de 19 variables a 11**
- Se descartaron 3 por redundancia y 5 por irrelevancia.
- Dos detalles del procedimiento: la discretización que habíamos creado quedó afuera, porque
  tenía 0,97 de correlación de Spearman con la variable continua; y las variables cíclicas
  se evaluaron de a pares, porque descartar el seno y conservar el coseno rompería la
  codificación.

**Columnas abajo:**

**Redundancia: 6 pares por encima de 0,80**
- El par más fuerte es `base_passenger_fare` con `driver_pay`, en **0,935**: lo que cobra el
  conductor se calcula sobre lo que paga el pasajero.
- También `trip_miles` con `driver_pay` (0,926) y con `duracion_min` (0,842).
- De cada grupo se conserva un solo representante.

**Relevancia: tres métodos comparados**
- ANOVA para las numéricas, Chi² para las categóricas e Información Mutua para ambas, todos
  con `SelectKBest` y normalizados en el mapa de la derecha.
- Las frecuencias de zona resultaron las dos variables más informativas, con 0,039 y 0,033
  de información mutua.

---

# DIAPOSITIVA 7 — PCA, datasets finales y conclusiones

**Etiqueta:** `07 · RESULTADO Y CIERRE`

**Banda:**
> **Extracción de features con PCA** *(Clase 7, slides 10 a 25)*
> A diferencia de la selección, PCA no elige variables: crea variables nuevas combinando las
> originales. Comprime, pero los componentes ya no son interpretables.

**Embudo de tres bloques descendentes, con flechas:**

```
  ┌────┐      ┌────┐      ┌───┐
  │ 19 │  ▸   │ 11 │  ▸   │ 6 │
  └────┘      └────┘      └───┘
 variables    tras la   componentes
 iniciales   selección    de PCA
```

**Dos tarjetas al lado:** `80,1 %` varianza retenida · `28,8 %` explica solo PC1

**Figura:** `12_pca_scree_varianza.png` (derecha arriba, 1,28" de alto)

**Columna izquierda:**

**Ventajas y desventajas de la reducción**
- A favor: los componentes son ortogonales entre sí, así que por construcción no hay
  redundancia, y baja el costo de cómputo.
- En contra: se pierde el 20 % de la varianza y, sobre todo, la interpretabilidad. «PC1» no
  le dice nada a nadie.
- PCA además supone relaciones lineales *(Clase 7, slide 12)*.

**Columna central:**

**Por qué comprimió tan poco**
- El primer componente explica solo el 28,8 %, cuando en un caso favorable los primeros dos
  o tres concentran casi todo.
- PCA únicamente puede comprimir lo que está correlacionado, y la selección previa ya había
  eliminado la redundancia: le quitamos justo lo que podía comprimir.
- **Selección y extracción compiten entre sí.** Para este trabajo conviene la versión
  seleccionada, que es interpretable.

**Bloque azul oscuro a la derecha:**

```
DATASETS FINALES
train  298.004 filas, balanceado
test   200.000 filas, 18,62 % real
0 faltantes · sin fuga de datos

CONCLUSIONES
— El uso es de ocio, no laboral.
— La calidad del dato depende de quién lo carga: Uber y Lyft
  no completan los mismos campos.
— Ninguna variable predice bien la propina, y saberlo antes
  de entrenar también es un resultado.
```

---

## Las 20 figuras disponibles

Las que van en la presentación están en **negrita**.

| Archivo | Qué muestra |
|---|---|
| `00_histograma_trip_miles` | Histograma con media, asimetría y curtosis anotadas |
| **`01_viajes_por_hora`** | Curva de viajes por hora del día |
| **`02_viajes_por_dia_semana`** | Barras por día, fin de semana destacado |
| **`03_distribucion_distancia_log`** | Escala normal contra logarítmica |
| `04_boxplot_por_empresa` | Duración y tarifa comparadas Uber / Lyft |
| `05_distancia_vs_tarifa` | Dispersión distancia contra tarifa |
| `06_mapa_faltantes` | Mapa de valores faltantes (missingno) |
| `06a_missingno_bar` | Datos no nulos por variable |
| **`07_boxplots_outliers`** | Boxplots con las colas largas visibles |
| `07b_hist_desvios` | Histograma con bandas de ±3 desvíos |
| `08_desbalance_target` | Distribución de la variable objetivo |
| **`09_balanceo_clases`** | Original / balanceado / test intacto |
| **`10_matriz_correlacion`** | Pearson y Spearman entre numéricas |
| `10b_cramers_v` | Cramér's V entre categóricas |
| `10c_eta_cuadrado` | Eta cuadrado numérica-categórica |
| **`11_relevancia_features`** | ANOVA / Chi² / MI normalizados |
| **`12_pca_scree_varianza`** | Scree plot y varianza acumulada |
| `13_pca_loadings` | Loadings de los componentes |
| `14_pca_contribuciones` | Qué variable pesa en PC1 y PC2 |
| `15_pca_biplot` | Biplot con las dos clases superpuestas |
