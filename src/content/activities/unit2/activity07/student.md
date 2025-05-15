``` py
# Imports go at the top
from microbit import *
import music

# Variable para controlar la pausa
pausado = False

while True:
    # Chequea si el botón A ha sido presionado para pausar/reanudar
    if button_a.was_pressed():
        pausado = not pausado
        sleep(50)  # Pequeña pausa para evitar rebotes del botón

    # Si no está pausado, reproduce los sonidos
    if not pausado:
        # Sonido 1: Tono simple (Duración ajustada a 1 segundo)
        pin0.write_digital(1)
        sleep(5000)  # Mantiene el tono por 1 segundo
        pin0.write_digital(0)
        sleep(200)   # Pausa breve antes de continuar

        # Sonido 2: Melodía predefinida (Duración ajustada a 1 segundo)
        music.play(music.PYTHON, wait=False)  # Reproduce la melodía sin bloquear
        sleep(5000)  # Espera 1 segundo mientras suena la melodía
        music.stop()  # Detiene la melodía después de 1 segundo
    
    # Chequea si el botón B ha sido presionado para reproducir un sonido diferente
    if button_b.was_pressed() and not pausado:
        music.play(music.ENTERTAINER, wait=False)  # Reproduce la melodía sin bloquear
        sleep(5000)  # Espera 1 segundo mientras se reproduce
        music.stop()  # Detiene la melodía después de 1 segundo

    else:
        # Si está pausado, muestra un mensaje y espera
        display.show('P')
        sleep(100)
```
