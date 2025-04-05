``` py
from microbit import *


# Lista de imágenes a mostrar
imagenes = [Image.ANGRY, Image.PACMAN, Image.HEART]
indice_imagen = 0  # Índice para rastrear la imagen actual

while True:
    # Muestra la imagen actual
    display.show(imagenes[indice_imagen])
    
    # Espera a que se presione un botón
    if button_a.was_pressed():
        # Cambia a la siguiente imagen
        indice_imagen = (indice_imagen + 1) % len(imagenes)  # Cicla a través de las imágenes
        sleep(400)  # Pequeña pausa para evitar múltiples cambios rápidos

    if button_b.was_pressed():
        # Cambia a la imagen anterior
        indice_imagen = (indice_imagen - 1) % len(imagenes)  # Cicla hacia atrás
        sleep(400)  # Pequeña pausa para evitar múltiples cambios rápidos
```
