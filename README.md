# Real-Time Sign Language Alphabet Translation and Dynamic Sign Detection

> **Computer Vision Final Project** — Group 8  
> University of Granada

---

## 🇪🇸 Resumen en Español

Hemos desarrollado varios modelos de reconocimiento de los signos del abecedario en LSE y un modelo de reconocimiento de signos dinámicos de hasta 64 clases distintas. El trabajo se ha centrado en encontrar la mejor forma de trabajar este problema y poder hacerlo a tiempo real. Principalmente se observa que los mejores resultados provienen de una detección de la posición de las principales partes de la mano para el posterior entrenamiento de los modelos. Además, nos encontramos con una gran falta de trabajo en este ámbito, dado que los datasets preparados para ello son muy escasos. Aún así, los resultados son muy buenos y se puede mejorar mucho la tecnología disponible en torno a este problema.

Para más detalles, consulta la memoria completa en [`docs/VC_ProyectoFinal_Memoria.pdf`](docs/VC_ProyectoFinal_Memoria.pdf).

---

## 📄 Abstract

We have developed several models for recognizing the alphabet signs in Spanish Sign Language (LSE) and a model for dynamic sign recognition with up to 64 distinct classes. The work focused on finding the best approach to solve this problem in real time. The best results mainly come from detecting the position of the main hand parts for subsequent model training. Additionally, we found a significant lack of work in this field, as prepared datasets are very scarce. Nevertheless, the results are very promising, and the available technology around this problem can be greatly improved.

---

## 🎯 Objectives

The project is divided into two main lines of work:

1. **Static Sign Detection (Alphabet)**  
   Real-time recognition of the Spanish Sign Language (LSE) alphabet letters using static images and live video streams. Different architectures and approaches are compared (CNN, classical Machine Learning models, and YOLO object detection).

2. **Dynamic Sign Recognition**  
   Classification of dynamic gestures in video using the [LSA64](https://facundoq.github.io/datasets/lsa64/) dataset (Argentinian Sign Language), combining spatial feature extraction with pretrained convolutional networks and temporal modeling with recurrent networks (GRU).

---

## 🗂️ Repository Structure

```
.
├── README.md
├── LICENSE
├── requirements.txt
├── docs/
│   └── VC_ProyectoFinal_Memoria.pdf      # Full project report (Spanish)
├── notebooks/
│   ├── 01_CNN_ModelosClasicos_AlfabetoEstatico.ipynb
│   ├── 02_YOLOv4_AlfabetoAmericano.ipynb
│   └── 03_LSA64_SignosDinamicos.ipynb
└── data/                                   # (Datasets not included — see Datasets section)
```

---

## 📒 Notebooks

### 1. CNN & Classical Models — Static Alphabet
**File:** `notebooks/01_CNN_ModelosClasicos_AlfabetoEstatico.ipynb`

- Training of a lightweight CNN (~60k parameters) on the **Sign Language MNIST** dataset.
- *Fine-tuning* of the CNN on custom Spanish Sign Language (LSE) datasets.
- Hand landmark extraction with **MediaPipe Hands** and training of classical models:
  - Random Forest
  - Logistic Regression
  - K-Nearest Neighbors
  - XGBoost
  - Decision Tree
- **Real-time** translation system with OpenCV + MediaPipe + Random Forest.
- Comparative evaluation and confusion matrices.

**Datasets used:**
- [Sign Language MNIST](https://www.kaggle.com/datamunge/sign-language-mnist)
- [Spanish Sign Language Alphabet (Static)](https://www.kaggle.com/)
- [Lenguaje de Signos Español](https://www.kaggle.com/)

---

### 2. YOLOv4-tiny — American Alphabet (ASL)
**File:** `notebooks/02_YOLOv4_AlfabetoAmericano.ipynb`

- Implementation of **YOLOv4-tiny** with the Darknet framework (AlexeyAB).
- Training for object detection (American Sign Language alphabet letters).
- Configuration of `.cfg`, `.data`, `.names` files and generation of training lists.
- Optimization for **real-time** execution with high inference speed.

**Dataset used:**
- [American Sign Language Letters](https://public.roboflow.com/object-detection/american-sign-language-letters/1)

---

### 3. LSA64 — Dynamic Signs
**File:** `notebooks/03_LSA64_SignosDinamicos.ipynb`

- Recognition of **64 classes** of Argentinian Sign Language (LSA64).
- Spatial feature extraction with **ResNet50** (pretrained on ImageNet, frozen weights).
- Temporal modeling with **Bidirectional GRU** + masking for variable-length sequences.
- Exploratory data analysis, video preprocessing, and frame visualization.
- Evaluation on an independent test set.

**Dataset used:**
- [LSA64 Videos (Kaggle)](https://www.kaggle.com/datasets/marcmarais/lsa64-videos)

---

## 🛠️ Requirements

The main dependencies of the project are:

| Library | Purpose |
|---------|---------|
| TensorFlow / Keras | Building and training CNNs and sequential models |
| OpenCV | Image/video processing and camera capture |
| MediaPipe | Hand landmark detection and tracking |
| scikit-learn | Classical ML models and evaluation metrics |
| XGBoost | Boosting classifier |
| NumPy, Pandas, Matplotlib, Seaborn | Data manipulation and visualization |

> **Note:** The YOLOv4-tiny notebook requires the [Darknet](https://github.com/AlexeyAB/darknet) framework compiled in the environment (GPU-optimized with CUDA/cuDNN).

Install all dependencies with:
```bash
pip install -r requirements.txt
```

---

## 🚀 Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/siryo169/LSE-Real-Time-Translation.git
   cd LSE-Real-Time-Translation
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Download the datasets** (see links in each notebook section) and place them in the `data/` folder.

4. **Open the notebooks** with Jupyter or Google Colab:
   ```bash
   jupyter notebook notebooks/
   ```

---

## 👥 Authors

- **Younes Aghani** — [@younesaghani](https://github.com/)
- **Álvaro Gómez García** — [@alvarogomez](https://github.com/)
- **Carlos García Jiménez** — [@carlosgarciaj](https://github.com/)
- **Alonso Lucas Juberías** — [@alonsolucasj](https://github.com/)

---

## 📚 References

1. Sign Language MNIST Dataset — [Kaggle](https://www.kaggle.com/datamunge/sign-language-mnist)
2. AlexeyAB / Darknet — [GitHub](https://github.com/AlexeyAB/darknet)
3. Bochkovskiy et al. *YOLOv4: Optimal Speed and Accuracy of Object Detection*. arXiv:2004.10934
4. Redmon et al. *You Only Look Once: Unified, Real-Time Object Detection*. arXiv:1506.02640
5. LSA64 Dataset — [Facundo Quiroga](https://facundoq.github.io/datasets/lsa64/)
6. MediaPipe Hands — [Google AI](https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker)
7. He et al. *Deep Residual Learning for Image Recognition*. CVPR 2016
8. Cho et al. *On the Properties of Neural Machine Translation: Encoder–Decoder Approaches*. arXiv:1409.1259 (GRU)

---

## 📄 License

This project is licensed under the **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International** (CC BY-NC-SA 4.0) — see the [LICENSE](LICENSE) file for details.

If you use code or ideas from this repository, please cite the associated project report.

---

> *"Technology at the service of accessibility: breaking communication barriers for the deaf community."*
