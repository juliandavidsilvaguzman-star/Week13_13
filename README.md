# Week13_13 Implementación de un Autoencoder en una Red Denoising usando el dataset MNIST

# Integrantes:
DIEGO ALEJANDRO RUIZ ALFONSO - diegoaruiz@ucundinamarca.edu.co
PEDRO PASCUAL MURCIA VARGAS - ppmurcia@ucundinamarca.edu.co 
JHON EDUARD TINJACA CRUZ - jetinjaca@ucundinamarca.edu.co 
JULIAN DAVID SILVA GUZMAN - jdsilva@ucundinamarca.edu.co 

#### Objetivo
Implementar y entrenar un **Autoencoder** para la reconstrucción y denoising de imágenes. El objetivo es que la red aprenda a eliminar el ruido artificial añadido a las imágenes del dataset MNIST, reconstruyendo las imágenes originales sin ruido mediante un proceso de compresión y descompresión de información.

#### Técnica(s) Utilizada(s)

*   **Autoencoder Simple:** Una red neuronal con una arquitectura simétrica compuesta por:
    *   **Encoder:** Comprime la entrada (784 píxeles) a través de capas densas hasta una representación latente comprimida de 32 dimensiones (cuello de botella).
    *   **Decoder:** Reconstruye la imagen original a partir de la representación comprimida, expandiendo desde 32 dimensiones hasta los 784 píxeles originales.

#### Configuración Base
*   **Dataset:** MNIST (60,000 imágenes de entrenamiento, 10,000 de prueba).
*   **Pre-procesamiento:**
    *   Normalización de píxeles (0-1).
    *   Aplanamiento de imágenes: 28×28 → 784 píxeles.
    *   Adición de ruido gaussiano con factor de intensidad 0.5.
*   **Arquitectura del Autoencoder:**
    *   **Entrada:** 784 neuronas (imagen aplanada).
    *   **Encoder:** 784 → 128 → 32 (cuello de botella).
    *   **Decoder:** 32 → 128 → 784 (reconstrucción).
    *   **Capas Ocultas:** Activación ReLU; **Capa de Salida:** Activación Sigmoid (para rango [0,1]).
*   **Optimización:** Optimizador Adam y función de pérdida Binary Crossentropy.
*   **Entrenamiento:** 10 épocas con batch size de 256.

#### Resultado Principal

**Encoder** | Compresión de 784 → 32 píxeles | Extrae características esenciales, descarta ruido
**Decoder** | Reconstrucción de 32 → 784 píxeles | Genera imagen limpia sin ruido original
**Loss (Entrenamiento)** | Disminuye progresivamente | Indica aprendizaje de patrones generales
**Loss (Validación)** | Cercano al de entrenamiento | Ausencia de overfitting; buena generalización
**Calidad Visual** | Imágenes reconstruidas legibles | Denoising efectivo del 50% de ruido

#### Puntos Clave del Ejercicio
*   **El Cuello de Botella (Bottleneck):** La capa de 32 neuronas obliga a la red a comprimir únicamente la información esencial del número, descartando automáticamente el ruido aleatorio.
*   **Compresión sin Supervisión:** El modelo aprende estructuras de datos sin necesidad de etiquetas, utilizando solo la comparación entre entrada ruidosa y salida limpia.
*   **Pérdida Binary Crossentropy:** Adecuada para medir la similitud estadística entre imágenes, considerando cada píxel como una probabilidad.
*   **Activación Sigmoid:** Garantiza que la salida se mantenga en el rango [0,1], compatible con la normalización de píxeles.
*   **Aplicaciones Reales del Denoising:**
    *   Limpieza de imágenes médicas (Rayos X, resonancias magnéticas) con interferencias.
    *   Restauración de grabaciones de audio con ruido de fondo.
    *   Detección de anomalías identificando errores de reconstrucción anormalmente altos.
    *   Compresión de datos preservando información semántica.


# Denoising Autoencoder - MNIST Dataset

Este proyecto implementa y compara diferentes arquitecturas de **Autoencoders** para la eliminación de ruido (denoising) utilizando el popular dataset **MNIST**.

## Descripción del Proyecto

El objetivo principal es entrenar una red neuronal capaz de recibir imágenes de dígitos escritos a mano con ruido artificial (Gaussian Noise) y reconstruir la versión original limpia. Se exploran tres enfoques progresivos:

1.  **Autoencoder Simple (Denso):** Utiliza capas `Dense` para comprimir la imagen a un espacio latente de 32 dimensiones.
2.  **Autoencoder Convolucional (CNN):** Aprovecha capas `Conv2D` y `MaxPooling2D` para capturar mejor la estructura espacial de los dígitos.
3.  **Autoencoder Convolucional con Dropout:** Añade regularización para mejorar la robustez y evitar el sobreajuste.

## Tecnologías Utilizadas

- **Python 3**
- **TensorFlow / Keras**
- **NumPy**
- **Matplotlib** (Visualización)


### Encoder (Compresor)
Reduce la dimensionalidad de la entrada (28x28 píxeles) hasta un "cuello de botella" (bottleneck). En la versión convolucional, esto se logra mediante filtros que detectan patrones esenciales.

### Decoder (Reconstructor)
Toma la representación comprimida y realiza un proceso de "UpSampling" para reconstruir la imagen original de 784 píxeles (o 28x28x1).

##  Resultados y Métricas

- **Función de Pérdida:** `binary_crossentropy`.
- **Optimizador:** `adam`.
- **Robustez:** El modelo fue probado con un factor de ruido extremo (0.75), logrando una **reducción del error (MSE) superior al 85%** en la reconstrucción.

##  Aplicaciones Reales

- Eliminación de ruido en imágenes médicas (Rayos X).
- Compresión de datos semántica.
- Detección de anomalías en sistemas industriales.
- Limpieza de señales de audio.

## Cómo Ejecutar en Colab

### Opción 1: Cargar desde GitHub
1. Abre [Google Colab](https://colab.research.google.com/)
2. Selecciona **"Archivo"** → **"Abrir cuaderno"** → **"GitHub"**
3. Pega la URL del repositorio que contiene este notebook

### Opción 2: Cargar manualmente
1. Descarga el archivo `Actividad13.ipynb` de esta carpeta
2. Abre [Google Colab](https://colab.research.google.com/)
3. Selecciona **"Archivo"** → **"Subir cuaderno"**
4. Elige el archivo descargado

### Requisitos
- NumPy
- Matplotlib
- TensorFlow
- Keras



