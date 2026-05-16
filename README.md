# Traducción del Alfabeto de la Lengua de Signos en Tiempo Real y Acercamiento a la Detección de Signos Dinámicos

> **Proyecto Final de Visión por Computador** — Grupo 8  
> Universidad de Granada

---

## 📋 Resumen

Hemos desarrollado varios modelos de reconocimiento de los signos del abecedario en LSE y un modelo de reconocimiento de signos dinámicos de hasta 64 clases distintas. El trabajo se ha centrado en encontrar la mejor forma de trabajar este problema y poder hacerlo a tiempo real. Principalmente se observa que los mejores resultados provienen de una detección de la posición de las principales partes de la mano para el posterior entrenamiento de los modelos. Además, nos encontramos con una gran falta de trabajo en este ámbito, dado que los datasets preparados para ello son muy escasos. Aún así, los resultados son muy buenos y se puede mejorar mucho la tecnología disponible en torno a este problema.

---

## 🎯 Objetivos

El proyecto se divide en dos líneas de trabajo principales:

1. **Detección de signos estáticos (alfabeto)**  
   Reconocimiento en tiempo real de las letras del alfabeto en Lengua de Signos Española (LSE) mediante imágenes estáticas y transmisiones de video en vivo. Se comparan diferentes arquitecturas y enfoques (CNN, modelos clásicos de Machine Learning y detección de objetos con YOLO).

2. **Reconocimiento de signos dinámicos**  
   Clasificación de gestos dinámicos en video utilizando el dataset [LSA64](https://facundoq.github.io/datasets/lsa64/) (Lengua de Señas Argentina), combinando extracción de características espaciales con redes convolucionales preentrenadas y modelado temporal mediante redes recurrentes (GRU).

---

## 🗂️ Estructura del Repositorio

```
.
├── README.md
├── docs/
│   └── VC_ProyectoFinal_Memoria.pdf      # Memoria completa del proyecto
├── notebooks/
│   ├── 01_CNN_ModelosClasicos_AlfabetoEstatico.ipynb
│   ├── 02_YOLOv4_AlfabetoAmericano.ipynb
│   └── 03_LSA64_SignosDinamicos.ipynb
└── data/                                   # (Datasets no incluidos — ver sección Datasets)
```

---

## 📒 Notebooks

### 1. CNN y Modelos Clásicos — Alfabeto Estático
**Archivo:** `notebooks/01_CNN_ModelosClasicos_AlfabetoEstatico.ipynb`

- Entrenamiento de una CNN ligera (~60k parámetros) sobre el dataset **Sign Language MNIST**.
- *Fine-tuning* de la CNN sobre datasets propios de LSE española.
- Extracción de *landmarks* de mano con **MediaPipe Hands** y entrenamiento de modelos clásicos:
  - Random Forest
  - Regresión Logística
  - K-Nearest Neighbors
  - XGBoost
  - Árbol de Decisión
- Sistema de traducción en **tiempo real** con OpenCV + MediaPipe + Random Forest.
- Evaluación comparativa y matrices de confusión.

**Datasets utilizados:**
- [Sign Language MNIST](https://www.kaggle.com/datamunge/sign-language-mnist)
- [Spanish Sign Language Alphabet (Static)](https://www.kaggle.com/)
- [Lenguaje de Signos Español](https://www.kaggle.com/)

---

### 2. YOLOv4-tiny — Alfabeto Americano (ASL)
**Archivo:** `notebooks/02_YOLOv4_AlfabetoAmericano.ipynb`

- Implementación de **YOLOv4-tiny** con el framework Darknet (AlexeyAB).
- Entrenamiento para detección de objetos (letras del alfabeto americano en ASL).
- Configuración de archivos `.cfg`, `.data`, `.names` y generación de listas de entrenamiento.
- Optimización para ejecución en **tiempo real** con alta velocidad de inferencia.

**Dataset utilizado:**
- [American Sign Language Letters](https://public.roboflow.com/object-detection/american-sign-language-letters/1)

---

### 3. LSA64 — Signos Dinámicos
**Archivo:** `notebooks/03_LSA64_SignosDinamicos.ipynb`

- Reconocimiento de **64 clases** de la Lengua de Señas Argentina (LSA64).
- Extracción de características espaciales con **ResNet50** (preentrenada en ImageNet, pesos congelados).
- Modelado temporal con **GRU bidireccional** + máscaras para secuencias de longitud variable.
- Análisis exploratorio del dataset, preprocesamiento de video y visualización de fotogramas.
- Evaluación en conjunto de test independiente.

**Dataset utilizado:**
- [LSA64 Videos (Kaggle)](https://www.kaggle.com/datasets/marcmarais/lsa64-videos)

---

## 🛠️ Requisitos

Las dependencias principales del proyecto son:

| Librería | Uso |
|----------|-----|
| TensorFlow / Keras | Construcción y entrenamiento de CNNs y modelos secuenciales |
| OpenCV | Procesamiento de imagen/video y captura de cámara |
| MediaPipe | Detección y seguimiento de landmarks de mano |
| scikit-learn | Modelos clásicos de ML y métricas de evaluación |
| XGBoost | Clasificador de boosting |
| NumPy, Pandas, Matplotlib, Seaborn | Manipulación de datos y visualización |

> **Nota:** El notebook de YOLOv4-tiny requiere el framework [Darknet](https://github.com/AlexeyAB/darknet) compilado en el entorno (optimizado para GPU con CUDA/cuDNN).

---

## 🚀 Uso Rápido

1. **Clonar el repositorio:**
   ```bash
   git clone https://github.com/<tu-usuario>/<tu-repo>.git
   cd <tu-repo>
   ```

2. **Instalar dependencias:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Descargar los datasets** correspondientes (ver enlaces en cada notebook) y colocarlos en la carpeta `data/`.

4. **Abrir los notebooks** con Jupyter o Google Colab:
   ```bash
   jupyter notebook notebooks/
   ```

---

## 👥 Autores

- **Younes Aghani** — [@younesaghani](https://github.com/)
- **Álvaro Gómez García** — [@alvarogomez](https://github.com/)
- **Carlos García Jiménez** — [@carlosgarciaj](https://github.com/)
- **Alonso Lucas Juberías** — [@alonsolucasj](https://github.com/)

---

## 📚 Referencias

1. Sign Language MNIST Dataset — [Kaggle](https://www.kaggle.com/datamunge/sign-language-mnist)
2. AlexeyAB / Darknet — [GitHub](https://github.com/AlexeyAB/darknet)
3. Bochkovskiy et al. *YOLOv4: Optimal Speed and Accuracy of Object Detection*. arXiv:2004.10934
4. Redmon et al. *You Only Look Once: Unified, Real-Time Object Detection*. arXiv:1506.02640
5. LSA64 Dataset — [Facundo Quiroga](https://facundoq.github.io/datasets/lsa64/)
6. MediaPipe Hands — [Google AI](https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker)
7. ResNet50 — *Deep Residual Learning for Image Recognition*, CVPR 2016
8. Cho et al. *On the Properties of Neural Machine Translation: Encoder–Decoder Approaches*. arXiv:1409.1259 (GRU)

---

## 📄 Licencia

Este proyecto es de carácter académico. Si utilizas código o ideas de este repositorio, por favor cita la memoria asociada.

---

> *"La tecnología al servicio de la accesibilidad: rompiendo barreras de comunicación para la comunidad sorda."*
