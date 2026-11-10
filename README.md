# Predicción de popularidad de videojuegos en Steam

¿Puede la recepción de la comunidad anticipar qué tan jugado va a ser un juego? Este proyecto analiza un catálogo de más de 120.000 juegos de Steam y construye un modelo de regresión que predice el **pico de jugadores simultáneos (Peak CCU)** a partir de las reseñas positivas y negativas.

Trabajo grupal de la **Tecnicatura Universitaria en Ciencia de Datos e Inteligencia Artificial** (Universidad del Gran Rosario).

## Resultados principales

| Métrica | Valor |
|---|---|
| Juegos en el dataset | 120.919 |
| Juegos con datos válidos para el modelo | 17.872 |
| Variación explicada (R² en prueba) | 0,52 |
| Error (RMSE, escala logarítmica) | 1,38 |

Modelo final:

```
log(Peak CCU) = −2,064 + 0,570 · log(reseñas positivas) + 0,098 · log(reseñas negativas)
```

- **El apoyo pesa más que la controversia:** las reseñas positivas pesan unas 6 veces más que las negativas para explicar la popularidad.
- **La transformación logarítmica fue la decisión clave:** el Peak CCU y las reseñas son extremadamente asimétricos (la mediana del Peak CCU es 0), y sin el logaritmo un modelo lineal no era viable.
- **Con solo dos variables el modelo explica el 52 % de la variación.** El resto depende de factores fuera de las reseñas, como el género, el marketing, los streamers o el momento de lanzamiento.

## Datos

[Steam Games Dataset](https://www.kaggle.com/datasets/fronkongames/steam-games-dataset) (Kaggle). Se redujo de 39 a 17 columnas, conservando las variables con valor analítico: Peak CCU, reseñas positivas y negativas, precio, género, tiempo de juego y plataformas.

## Notebooks

| # | Notebook | Contenido |
|---|---|---|
| 01 | [Análisis exploratorio](notebooks/01_analisis_exploratorio.ipynb) | Limpieza y primera exploración del dataset |
| 02 | [Análisis principal](notebooks/02_analisis_principal.ipynb) | Análisis univariado y bivariado, visualizaciones y conclusiones |
| 03 | [Análisis empresarial](notebooks/03_analisis_empresarial.ipynb) | Segmentación de mercado y perfiles de éxito por género |
| 04 | [Modelo](notebooks/04_modelo_regresion.ipynb) | Preparación de datos y modelo de regresión |
| 05 | [Regresión Peak CCU](notebooks/05_regresion_peak_ccu.ipynb) | Regresión del pico de jugadores con transformación logarítmica |

## Metodología

1. **Limpieza:** selección de variables y validación de los datos contra juegos conocidos.
2. **Análisis exploratorio:** medidas de posición y dispersión, distribuciones y correlaciones.
3. **Transformación logarítmica** para corregir la fuerte asimetría de las variables.
4. **Regresión lineal múltiple** con partición 80/20 entre entrenamiento y prueba.

## Herramientas

Python · Pandas · NumPy · Scikit-learn · Matplotlib · Seaborn · Google Colab

## Equipo

Juan Eduardo Botto · Renzo Beribé · Máximo Linzuain · Valentino Panarisi · Santiago Scozziero
