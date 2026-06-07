# 🚗 Simulación del Sistema de Parqueaderos - Supercentro

Este proyecto implementa un modelo de simulación de eventos discretos para evaluar la capacidad y el nivel de servicio del sistema de recaudo y pago electrónico de parqueaderos del centro comercial **Supercentro**. 

El modelo simula el comportamiento de tres (3) cajeros automáticos independientes que operan en paralelo utilizando la teoría de colas (modelado conceptual M/M/1), considerando la alta variabilidad en los tiempos de interacción de diferentes perfiles de usuarios.

## 📋 Características del Proyecto

* **Motor estocástico:** Generación de tiempos de arribo y tiempos de servicio exponenciales mediante el método de la transformada inversa.
* **Mezcla de perfiles de usuario:** Clasificación dinámica de clientes con sus respectivas probabilidades empíricas:
  * Rápidos (25% - 1.0 min de servicio)
  * Normales (20% - 3.0 min de servicio)
  * Lentos (27.5% - 4.0 min de servicio)
  * Muy Lentos (27.5% - 6.0 min de servicio)
* **Análisis de Estado Estable:** Implementación de un algoritmo de promedio móvil suavizado (ventana de 150 observaciones) para identificar y eliminar automáticamente el periodo transitorio (Warm-up period).
* **Validación Científica:** Contraste automático de las métricas empíricas obtenidas frente a las ecuaciones analíticas de la teoría de colas de Kendall.

## 🛠️ Tecnologías Utilizadas

* **Python 3.x**
* **Numpy:** Para la generación de variables aleatorias y manejo de vectores interconectados.
* **Matplotlib:** Para el desarrollo de las librerías gráficas y visualización del estado estable.
* **Scipy (scipy.stats):** Para el cálculo riguroso de Intervalos de Confianza del 95% mediante distribuciones t de Student.

Estructura del Código
El código está estructurado y documentado en 6 bloques lógicos principales para garantizar su fácil lectura y mantenimiento:

Parametrización del Modelo (Calibración): Definición de tiempos teóricos y cálculo de la tasa de llegada efectiva por cajero.

Motor de Eventos Discretos: Lógica de simulación controlando que el inicio del servicio sea el valor máximo entre el arribo del cliente y el fin del servicio anterior.

Eliminación del Estado Transitorio: Suavizado por promedio móvil y purga de los primeros 400 clientes (fase de calentamiento).

Extracción de Resultados: Impresión en consola de las medias, desviaciones estándar e intervalos de confianza del 95%.

Gráfica de Validación M/M/1: Comparativa visual en barras que demuestra la convergencia de la simulación frente a las fórmulas matemáticas clásicas.

Análisis Estratégico: Resumen de las políticas operativas propuestas para la toma de decisiones del grupo de trabajo.

Conclusiones Clave del Estudio
Suficiencia de Infraestructura: La configuración actual de 3 cajeros independientes es completamente SUFICIENTE. Al distribuirse el tráfico de manera equitativa, el factor de utilización real por cajero se sitúa en un cómodo 25.8%, lo que absorbe sin problemas la carga de los usuarios lentos.

Estrategia Recomendada: Se propone implementar una Caja Express Especializada en la primera terminal para aislar al 25% de usuarios rápidos de atascos indeseados provocados por usuarios muy lentos, optimizando la experiencia del cliente sin costos extras de infraestructura física.

### Prerrequisitos

Asegúrate de tener instalado Python en tu sistema. Puedes instalar las librerías necesarias ejecutando el siguiente comando en tu terminal:

```bash
pip install numpy matplotlib scipy

git clone https://github.com/CristianDZ29/centro_comercial_Supercentro_Simulacion

También lo puedes ejecutar en google colab:
https://colab.research.google.com/drive/12V2i3AK2lba04CGav_Ij2na2olE4aGqE#scrollTo=-KXuEWUaXcyb
