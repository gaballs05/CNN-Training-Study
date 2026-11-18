# CNN Training Study
Laboratorio 3 · Aprendizaje máquina

Comparación de AlexNet, VGG11 y una CNN propia en PyTorch para clasificar 10 clases de símbolos. Para estudiar qué cambia en el entrenamiento, mantuve fija la CNN propia y comparé por separado el optimizador, la regularización, el tamaño de lote, el ajuste de la tasa de aprendizaje y la inicialización de pesos.

---

## Guía rápida para abrir el proyecto

El archivo [`nn_training_study.ipynb`](nn_training_study.ipynb) ya incluye las tablas, gráficas y el reporte. Se puede abrir desde GitHub o subir a [Google Colab](https://colab.research.google.com/) desde el iPad. La sección 6 contiene el resumen del laboratorio.

### Ejecutar en Linux

Usé Python 3.12 y PyTorch en CPU para las corridas del reporte.

```bash
git clone https://github.com/gaballs05/CNN-Training-Study.git
cd CNN-Training-Study
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt notebook
jupyter notebook nn_training_study.ipynb
```

Con `RETRAIN = False`, el notebook carga los resultados que ya están guardados. Para repetir el entrenamiento, cambia a `RETRAIN = True`. Usa `RUN_GROUP = "all"` para correr el estudio completo, `"baseline"` para las arquitecturas o una letra de `"A"` a `"E"` para un solo experimento.

---

## Dataset

El dataset tiene 900 imágenes generadas de 32 × 32 píxeles en escala de grises. Separé 600 para entrenamiento, 150 para validación y 150 para prueba. A cada imagen de entrenamiento le agregué nueve variantes para llegar a 6,000 ejemplos por época. Las imágenes de validación y prueba se dejaron como salieron del generador.

## Resultados

| Configuración de la CNN propia | Mejor accuracy de validación, media ± DE | Accuracy en prueba |
|---|---:|---:|
| Baseline con aumento de datos | 76.22 % ± 2.78 pp | — |
| Tasa de aprendizaje constante después del calentamiento | 79.78 % ± 3.15 pp | 75.33 % |

Cada condición se corrió con tres semillas durante 60 épocas. Seleccioné el modelo por validación y evalué su checkpoint en prueba una sola vez. Acertó **113 de 150 imágenes**.

La CNN propia sin aumento terminó con **100 % en entrenamiento y 41.11 % en validación**. Con aumento, terminó con **99.39 % y 73.11 %**, respectivamente. En ambos casos se procesó el mismo número de ejemplos por época.

---

## Archivos

- [`nn_training_study.ipynb`](nn_training_study.ipynb) — código, gráficas y reporte.
- [`requirements.txt`](requirements.txt) — versiones de las dependencias.
- [`resultados/`](resultados/) — métricas por época, configuración y pesos del modelo seleccionado.
