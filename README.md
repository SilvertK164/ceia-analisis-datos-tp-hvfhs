# Trabajo Práctico Integrador — Análisis de Datos

**Carrera de Especialización en Inteligencia Artificial (CEIA) — FIUBA — 3B 2026**

Análisis exploratorio y preparación de datos sobre los viajes de **Uber y Lyft en la ciudad
de Nueva York**, con vistas a un problema de Machine Learning supervisado.

| | |
|---|---|
| **Grupo** | `[COMPLETAR]` |
| **Integrantes** | `[COMPLETAR]` |
| **Dataset** | High Volume For-Hire Vehicle (HVFHV) — NYC Taxi & Limousine Commission |
| **Período analizado** | Agosto 2025 |
| **Volumen** | 19.271.461 viajes × 25 variables |

---

## El trabajo

El dataset registra **todos** los viajes de Uber y Lyft realizados en Nueva York. Cada fila
es un viaje, con su origen, destino, horarios, distancia, tarifa, propina y lo que cobró el
conductor.

El notebook recorre, en 20 secciones:

1. Exploración y comprensión del dataset (§1 a §6)
2. Calidad de los datos: faltantes con su tipo, errores y outliers (§7 y §8)
3. Planteo del problema de ML supervisado y definición de la target (§9)
4. Preparación: limpieza, split, faltantes, outliers, codificación, escalado y balance (§10 a §16)
5. Reducción de dimensionalidad: selección de features y PCA (§17 y §18)
6. Datasets de train y test listos para entrenar (§19) y conclusiones (§20)

**El problema planteado:** clasificación binaria — ¿el pasajero dejará propina?
Variable target `dio_propina = (tips > 0)`, con una distribución de 18,52 % / 81,48 %.

> El entrenamiento del modelo no forma parte de la consigna: se pide *plantear* el problema
> y *preparar* los datos.

**Por qué un solo mes:** el año 2025 completo son unos 240 millones de registros en 12
archivos de ~480 MB. Analizar un único mes fue sugerencia de la cátedra dada esa magnitud.
Agosto por sí solo aporta más de 19 millones de viajes.

---

## Cómo ejecutar el notebook

### 1. Descargar los datos

Los archivos de datos **no están en este repositorio**: pesan unos 480 MB cada uno y GitHub
limita a 100 MB por archivo. Se descargan gratis desde la página oficial del NYC TLC:

**https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page**

En la sección **"High Volume For-Hire Vehicle Trip Records"**, descargar
`fhvhv_tripdata_2025-08.parquet`.

Conviene bajar también el **diccionario de datos** (`data_dictionary_trip_records_hvfhs.pdf`)
desde esa misma página: explica el significado de cada columna y es la fuente que el
notebook consulta para clasificar los datos faltantes.

### 2. Instalar las dependencias

```bash
python -m venv .venv
.venv/Scripts/activate        # Windows
# source .venv/bin/activate   # Linux o macOS

pip install -r requirements.txt
```

### 3. Indicar dónde están los datos

En la celda de configuración del notebook (§0) hay una variable `RUTA_DATOS`. Hay que
apuntarla a la carpeta donde se guardó el archivo `.parquet`.

### 4. Ejecutar

```bash
jupyter notebook TP_analisis_datos_hvfhs.ipynb
```

Las celdas se ejecutan en orden, de arriba hacia abajo. La corrida completa toma unos cinco
minutos y necesita alrededor de 6 GB de memoria libre.

### Qué genera

- La carpeta `figuras/` con los gráficos en PNG.
- La carpeta `datos_preparados/` con cuatro archivos listos para entrenar un modelo: train
  y test con las features seleccionadas, y train y test con los componentes principales.
  Los cuatro incluyen la variable target.

Ninguna de las dos carpetas se versiona: son resultados derivados que se regeneran al
ejecutar el notebook.

---

## Contenido del repositorio

| Archivo | Qué es |
|---|---|
| `TP_analisis_datos_hvfhs.ipynb` | El notebook con todo el análisis, ya ejecutado |
| `requirements.txt` | Dependencias |

---

## Fuente de los datos

NYC Taxi & Limousine Commission — *High Volume For-Hire Vehicle Trip Records*.
Datos públicos y de libre acceso.
https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
