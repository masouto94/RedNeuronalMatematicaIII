# Red neuronal de clasificación

El presente repositorio contiene una red neuonal de clasificación para poder predecir adecuadamente si una palta está madura o no. El dataset de entrenamiento procede de la [siguiente fuente](https://www.kaggle.com/datasets/amldvvs/avocado-ripeness-classification-dataset) y describe una serie de características físicas de la fruta. A partir de las mismas, se llega a una clasificación de madurez del 1 (dura) al 5 (completamente madura).

El dataset es de carácter sintético pero es consistente en su patrón de medición y etiquetado. Se adjuntan algunas notas metodológicas de cómo se llevaron a cabo las medidas:

1) Patrones de peso:
    - Unripe (Hard): 200-300g
    - Pre-conditioned: 180-280g
    - Breaking: 160-260g
    - Firm-ripe: 150-240g
    - Ripe: 150-220g

2) Patrones de tamaño:
    - Unripe (Hard): 100-200 cm³
    - Pre-conditioned: 120-220 cm³
    - Breaking: 140-240 cm³
    - Firm-ripe: 160-260 cm³
    - Ripe: 180-300 cm³

3) Densidad:

    No está medida directamente pero se debe computar como el cociente entre peso y tamaño
    - Hard: 1.4 - 1.8
    - Pre-conditioned: 1.2 - 1.6
    - Breaking: 1.0 - 1.4
    - Firm-ripe: 0.8 - 1.2
    - Ripe: 0.6 - 1.0

4) Medición de color:

    Se utilizó una cámara RGB de alta resolución con luz controlada. Las imágenes tomadas fueron transformadas de RGB a HSB mediante este código:

    ```py
    def rgb_to_hsb(rgb_image):
     hsv_image = cv2.cvtColor(rgb_image, cv2.COLOR_RGB2HSV)
     hue = hsv_image[:, :, 0].astype(np.float32) * 2
     saturation = hsv_image[:, :, 1].astype(np.float32) * (100/255)
     brightness = hsv_image[:, :, 2].astype(np.float32) * (100/255)
     return hue, saturation, brightness
    ```

    |Color Category | Hue (0-360°) | Saturation (0-100%) | Brightness (0-100%)|
    |---|---|---|---|
    |Dark Green|  60-120° | 70-100% | 40-70%|
    |Green  |45-90° | 60-90% | 50-80%|
    |Purple | 270-330°|  50-80%  |30-60%|
    |Black | 0-30°|  30-60%  |10-40%|
