# Sistema de Recomendación de Parada Óptima para Transporte Público

> **Asignatura:** Inteligencia Artificial (2026)  
> **Institución:** Facultad de Ingeniería - Centro Regional Universitario Córdoba (IUA - UNDEF)  
> **Docente:** Ing. González, Hernando Alexis  
> **Alumnos:** Badami Celeste Antonella [cbadami845@alumnos.iua.edu.ar], Vargas Benjamin[bvargas161@alumnos.iua.edu.ar]  
> **Despliegue / Landing Page:** [https://tu-usuario.github.io/tu-repositorio](https://tu-usuario.github.io/tu-repositorio)

---

## 1. Project Charter (Propuesta Formal PLANTILLA BOCETO)

### 1.1. Definición del Problema
En entornos urbanos, los usuarios del transporte público enfrentan dificultades para seleccionar la parada y ruta óptima al combinar trayectos a pie con líneas de autobús. Los sistemas convencionales suelen basarse únicamente en la distancia euclidiana simple. Este proyecto aborda la recomendación inteligente de paradas y trayectos mediante modelos de aprendizaje automático y optimización en grafos geoespaciales.

### 1.2. Modelado del Entorno (PEAS PLANTILLA BOCETO)
* **Performance (Rendimiento):** Minimización del tiempo total de desplazamiento, precisión en la estimación de tiempos de arribo y reducción de la distancia caminada.
* **Environment (Entorno):** Red de transporte urbano, paradas de autobús, trazas de rutas y condiciones de demanda/tráfico.
* **Actuators (Actuadores):** Interfaz de recomendación que retorna la ordenación óptima de paradas y rutas.
* **Sensors (Sensores):** Coordenadas GPS del usuario, datos geoespaciales KML/GTFS y marcas temporales de consulta.

### 1.3. Origen y Naturaleza de los Datos
* **Fuentes de datos:** Capas geoespaciales en formato `.kml` / `.geojson` con paradas y trazados de rutas, sumado a datasets de tiempos históricos o frecuencias.
* **Volumen e higiene:** Procesamiento de registros vectoriales mediante `geopandas` y `shapely`. Limpieza de coordenadas anómalas, inconsistencias en topología de red y prevención de *data leakage* en la división temporal.

### 1.4. Métricas de Éxito y Baseline
* **Baseline (Punto de comparación sin IA):** Selección por distancia euclidiana fija a la parada más cercana (*Nearest Neighbor* ingenuo).
* **Métrica de Éxito del Modelo:** 
  * Reducción de $\ge 15\%$ en el tiempo estimado de viaje respecto al baseline.
  * $F1\text{-Score} \ge 0.82$ o $MAE < 2.5\text{ min}$ en la predicción del tiempo de arribo / caminata óptima.

### 1.5. Límites del Alcance (Out of Scope)
Para enfocar el desarrollo en el núcleo de IA del Producto Mínimo Viable (MVP):
* **No se incluye:** Gestión de usuarios, autenticación o persistencia de cuentas.
* **No se incluye:** Pasarelas de pago ni procesamiento de boletos.
* **No se incluye:** App móvil nativa (Android/iOS).

---

## 2. Arquitectura del Repositorio PLANTILLA BOCETO

El proyecto sigue la estructura modular exigida para garantizar el desacoplamiento de capas y la limpieza de código:

```text
├── data/           # Datasets y archivos KML/GeoJSON (EXCLUIDO de Git)
├── notebooks/      # Anotadores exploratorios (EDA, prototipado)
├── models/         # Artefactos, pesos del modelo (.pkl, .onnx)
├── src/            # Código fuente modularizado
│   ├── data/       # Procesamiento y carga geoespacial
│   ├── models/     # Arquitectura de entrenamiento e inferencia
│   └── utils/      # Funciones auxiliares y semillas
├── requirements.txt # Manifiesto de dependencias con version pinning
└── README.md