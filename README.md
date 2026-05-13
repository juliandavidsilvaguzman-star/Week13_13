# Week13_13 Implementación de un Autoencoder en una Red Denoising usando el dataset MNIST



markdown
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

