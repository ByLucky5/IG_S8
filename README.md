# Visualización Delincuencia Washington DC

## Indice

1. [Descripción](#1-descripción)
2. [Objetivos](#2-objetivos)
3. [Funcionalidades](#3-funcionalidades)
4. [Datos y procesamiento](#4-datos-y-procesamiento)

   * [4.1 Origen de los datos](#41-origen-de-los-datos)
   * [4.2 Limpieza y consolidación de CSV](#42-limpieza-y-consolidación-de-csv)
   * [4.3 Estructura de datos usada](#43-estructura-de-datos-usada-en-la-visualización)
5. [Video de demostración](#5-video-de-demostración)
6. [Bibliografía / Fuentes](#6-bibliografía--fuentes)

---

## 1. Descripción

Este proyecto es una **visualización interactiva** y **dinámica en 2D** de la criminalidad en Washington DC entre **2015 y 2025**. Utiliza datos oficiales de incidentes delictivos día a día y los representa sobre un mapa dividido por “Neighborhood Clusters” (regiones), permitiendo analizar tendencias, comparar años, filtrar por tipo de delito y ver un ranking de las zonas más afectadas.
<p align="center"> <img src="/images/Vista_general.png" width="800"/> </p>

---

## 2. Objetivos

* Mostrar la evolución temporal de los incidentes delictivos.
* Permitir al usuario filtrar por tipo de delito y periodo.
* Presentar un ranking de las regiones más peligrosas en tiempo real.
* Ser una herramienta analítica para concienciar sobre la alta tasa de delincuencia.

---

## 3. Funcionalidades

1. **Mapa 2D** con polígonos de distritos (“clusters”)

   <p align="center">
     <img src="Mapa.png" width="400"/>
   </p>

2. **Animación día a día** con reproducción, pausa, reinicio y salto directo al final (“Pasar rápido”)

   <p align="center">
     <img src="Control.png" width="350"/>
   </p>

3. **Leyenda de intensidad dinámica**
   *Valores máximos adaptables según año, rango o filtro por tipo de delito.*

   <p align="center">
     <img src="Leyenda_intensidad.png" width="200"/>
   </p>

4. **Selección de año o rango temporal**

   * 2015–2025 (modo acumulativo)
   * 2015–2020
   * 2020–2025
   * Años individuales

   <p align="center">
     <img src="Año_rango.png" width="350"/>
   </p>

5. **Filtro por tipo de delito**

   <p align="center">
     <img src="Tipo_delito.png" width="450"/>
   </p>

6. **Ranking de Top 10 regiones con más incidentes**

   <p align="center">
     <img src="Ranking.png" width="350"/>
   </p>

7. **Tooltip al hacer clic en una región**

   <p align="center">
     <img src="Info.png" width="350"/>
   </p>

8. **Controles de personalización y velocidad**

   <p align="center">
     <img src="Personalizacion.png" width="350"/>
   </p>

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

## 5. Video de demostración

<p align="center">
  <a href="https://www.youtube.com/watch?v=X" target="_blank">
    <img src="https://img.youtube.com/vi/X/0.jpg" alt="Ver demo del Sistema Solar" width="480">
  </a>
</p>


---

## 6. Bibliografía / fuentes

* **Catalog.data.gov – Crime Incidents**:

  * “Crime Incidents in 2015” – catalog.data.gov
  * “Crime Incidents in 2016” – catalog.data.gov
  * …
  * “Crime Incidents in 2025” – catalog.data.gov
* **OpenData DC**: Neighborhood Clusters – GeoJSON oficial
* **Three.js** — biblioteca para renderizado 3D (threejs.org)
* **PapaParse** — librería para parsear CSV en el navegador (papaparse.com)
