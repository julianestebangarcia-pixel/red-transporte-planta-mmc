# Análisis y optimización de una red interna de transporte en una planta manufacturera

Proyecto final de la asignatura **Métodos y Modelos Computacionales** — Maestría en Ingeniería Eléctrica.

**Autor:** Julián Esteban Garcia Castaño

## Descripción

Este proyecto modela la red interna de transporte de una planta manufacturera como un dígrafo y resuelve, sobre él, cuatro problemas de métodos y modelos computacionales:

1. **Análisis topológico y caminos mínimos** — construcción de la red, verificación de fuerte conexidad y comparación de los algoritmos de Dijkstra y A\* con heurística geométrica, incluyendo un estudio de complejidad y escalabilidad empírica.
2. **Estimación de velocidades** — solución de una ecuación no lineal de velocidad efectiva por cinta mediante el método de Newton-Raphson, con análisis de sensibilidad a la inicialización.
3. **Optimización de la modernización** — modelo de programación entera binaria (tipo mochila) para seleccionar qué cintas modernizar bajo un presupuesto limitado.
4. **Análisis de sensibilidad del presupuesto** — exploración del desempeño de la red al variar el presupuesto entre el 10 % y el 100 % del costo total.

La red base consta de **16 estaciones** en **7 zonas funcionales** conectadas por **31 cintas dirigidas**, y es fuertemente conexa.

## Estructura del repositorio

```
.
├── README.md                     # este archivo
├── requirements.txt              # dependencias de Python
├── proyecto_mmc.ipynb            # notebook principal con todo el desarrollo
└── salidas/                      # (opcional) tablas y figuras generadas
    ├── estaciones.csv
    ├── cintas.csv
    ├── comparacion_rutas.csv
    ├── escalabilidad.csv
    ├── newton_raphson.csv
    ├── sensibilidad_nr.csv
    ├── escenarios_modernizacion.csv
    ├── sensibilidad_presupuesto.csv
    ├── red_base.png
    ├── escalabilidad.png
    └── sensibilidad_presupuesto.png
```

## Cómo ejecutar

### Opción A — Google Colab (recomendada)

1. Abre el notebook `proyecto_mmc.ipynb` en [Google Colab](https://colab.research.google.com/).
2. Ejecuta las celdas en orden (menú *Entorno de ejecución → Ejecutar todo*).
3. No requiere GPU. Las dependencias se instalan desde el propio notebook (`pip install pulp`).

### Opción B — Local

```bash
# 1. Clonar el repositorio
git clone https://github.com/USUARIO/NOMBRE-DEL-REPO.git
cd NOMBRE-DEL-REPO

# 2. (opcional) crear un entorno virtual
python -m venv venv
source venv/bin/activate        # en Windows: venv\Scripts\activate

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Ejecutar el notebook
jupyter notebook proyecto_mmc.ipynb
```

## Reproducibilidad

Todos los experimentos usan una semilla aleatoria fija (`SEED = 42`), de modo que la generación de los parámetros de la red y de las redes de prueba es determinista y los resultados son reproducibles entre ejecuciones.

## Dependencias

- numpy
- pandas
- matplotlib
- networkx
- pulp

(Ver `requirements.txt` para detalles.)

## Resultados principales

- La red base cumple todas las condiciones del enunciado y es fuertemente conexa.
- Dijkstra y A\* entregan rutas óptimas idénticas; A\* expande entre 14 % y 30 % menos nodos.
- Los tiempos de ejecución escalan de forma consistente con la complejidad teórica *O((|V|+|E|)·log|V|)*.
- Newton-Raphson converge para las 31 cintas en un promedio de 3.58 iteraciones, de forma robusta frente a la inicialización.
- Con el 30 % del presupuesto total se logra una reducción del 22 % del indicador de desempeño, con claros rendimientos decrecientes.

## Nota sobre el uso de IA

El uso de herramientas de inteligencia artificial durante el desarrollo del proyecto se declara de forma explícita en la sección correspondiente del informe técnico (PDF).
