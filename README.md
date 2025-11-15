# Visualización Delincuencia Washington DC

## 1. Descripción

Este proyecto es una **visualización interactiva** y **dinámica en 2D** de la criminalidad en Washington DC entre **2015 y 2025**. Utiliza datos oficiales de incidentes delictivos día a día y los representa sobre un mapa dividido por “Neighborhood Clusters” (regiones), permitiendo analizar tendencias, comparar años, filtrar por tipo de delito y ver un ranking de las zonas más afectadas.

---

## 2. Objetivos

* Mostrar la evolución temporal de los incidentes delictivos.
* Permitir al usuario filtrar por tipo de delito y periodo.
* Presentar un ranking de las regiones más peligrosas en tiempo real.
* Ser una herramienta analítica para concienciar sobre la alta tasa de delincuencia.

---

## 3. Funcionalidades

1. **Mapa 3D** con polígonos de distritos (“clusters”)
2. **Animación día a día** con reproducción, pausa o salto directo al final (“Pasar rápido”)
3. **Leyenda de intensidad**, adaptativa según periodo y filtro
4. **Selección de año / rango temporal**
   * Rango completo (2015-2025)
   * Subrango (2015-2020, 2020-2025)
   * Años individuales
5. **Filtro por tipo de delito** (robos, homicidios, incendios, agresiones, etc.)
6. **Ranking de Top 10 regiones** según casos acumulados
7. **Tooltip** con nombre de la región y número de incidentes al hacer clic

---

## 4. Datos y procesamiento

### 4.1 Origen de los datos

Los datos de incidentes delictivos provienen de los conjuntos de datos públicos de **catalog.data.gov** para cada año:

* 2015: [https://catalog.data.gov/dataset/crime-incidents-in-2015](https://catalog.data.gov/dataset/crime-incidents-in-2015)
* 2016: [https://catalog.data.gov/dataset/crime-incidents-in-2016](https://catalog.data.gov/dataset/crime-incidents-in-2016)
* …
* 2025: [https://catalog.data.gov/dataset/crime-incidents-in-2025](https://catalog.data.gov/dataset/crime-incidents-in-2025)

La GeoJson de los “Neighborhood Clusters” proviene de **OpenData DC**:
[https://opendata.dc.gov/datasets/neighborhood-clusters/explore](https://opendata.dc.gov/datasets/neighborhood-clusters/explore)

### 4.2 Limpieza y consolidación de CSV

Para optimizar el rendimiento (especialmente en entornos como CodeSandbox), se realizó un pre-procesamiento:

1. Se descargó cada CSV por año desde catalog.data.gov.
2. Se extrajeron solo las columnas necesarias (“REPORT_DAT”, “NEIGHBORHOOD_CLUSTER”, “OFFENSE”) mediante un script en Python.
3. Los CSV “minímos” de cada año se unificaron en un solo archivo llamado `Crime_Incidents_last_ten_years.csv`.
4. Este archivo reducido se emplea en la visualización para construir una estructura `dayMap` eficiente.

### 4.3 Estructura de datos usada en la visualización

* `dayMap`: objeto donde cada día (string) mapea a otro objeto con contadores por región.
* `clusterMeshes`: cada región tiene su mesh 3D + contador acumulado.
* `maxIncidents`: máximo de la leyenda definido dinámicamente según el filtro de años y tipo de delito.

---

## 5. Bibliografía / fuentes

* **Catalog.data.gov – Crime Incidents**:

  * “Crime Incidents in 2015” – catalog.data.gov
  * “Crime Incidents in 2016” – catalog.data.gov
  * …
  * “Crime Incidents in 2025” – catalog.data.gov
* **OpenData DC**: Neighborhood Clusters – GeoJSON oficial
* **Three.js** — biblioteca para renderizado 3D (threejs.org)
* **PapaParse** — librería para parsear CSV en el navegador (papaparse.com)

---
