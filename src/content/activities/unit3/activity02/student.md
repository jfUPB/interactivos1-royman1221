``` py
from microbit import *
import music

# Definir estados
STATE_CONFIG = 0
STATE_ARMED = 1
STATE_EXPLODED = 2

# Configuración inicial
time_left = 20  # Tiempo predeterminado
current_state = STATE_CONFIG
start_time = 0

# Límites de configuración
MIN_TIME = 10
MAX_TIME = 60

# Secuencia de desactivación
sequence_index = 0  # Índice para seguir la secuencia

while True:
    if current_state == STATE_CONFIG:
        display.show(time_left)  # Mostrar tiempo en pantalla
        if button_a.was_pressed() and time_left < MAX_TIME:
            time_left += 1
            display.show(time_left)  # Refrescar pantalla
        if button_b.was_pressed() and time_left > MIN_TIME:
            time_left -= 1
            display.show(time_left)  # Refrescar pantalla
        if accelerometer.was_gesture("shake"):  # Armar bomba
            current_state = STATE_ARMED
            start_time = running_time()  # Iniciar cuenta regresiva

    elif current_state == STATE_ARMED:
        elapsed_time = running_time() - start_time
        if elapsed_time >= 1000:  # Reducir tiempo cada 1s
            time_left -= 1
            start_time = running_time()
            display.show(time_left)  # Mostrar cuenta regresiva

        # Comprobar secuencia de desactivación
        if sequence_index == 0 and button_a.was_pressed():
            sequence_index += 1  # A presionado correctamente
        elif sequence_index == 1 and button_b.was_pressed():
            sequence_index += 1  # B presionado correctamente
        elif sequence_index == 2 and button_a.was_pressed():
            sequence_index += 1  # A presionado correctamente
        elif sequence_index == 3 and accelerometer.was_gesture("shake"):
            sequence_index += 1  # Shake realizado correctamente
            current_state = STATE_CONFIG  # Desactivar la bomba y volver al modo de configuración
            time_left = 20  # Reiniciar el tiempo
            display.show(time_left)  # Mostrar el tiempo inicial

        # Si la secuencia no se completa correctamente, la bomba sigue con su cuenta regresiva
        if sequence_index > 3:
            sequence_index = 0  # Reiniciar secuencia si no es correcta

        if time_left <= 0:  # Si llega a 0, explota
            current_state = STATE_EXPLODED

    elif current_state == STATE_EXPLODED:
        display.show(Image.SKULL)  # Mostrar calavera (explosión)

        # 🔊 Sonido de explosión usando BA_DING
        music.play(music.BA_DING)

        # Esperar hasta que se toque el logo dorado para reiniciar
        while not pin_logo.is_touched():
            display.show(Image.SKULL)  # Mantener la imagen de explosión

        # Reiniciar la bomba
        time_left = 20
        current_state = STATE_CONFIG

    # Verificar si se toca el logo dorado en cualquier estado
    if pin_logo.is_touched():
        current_state = STATE_CONFIG
        time_left = 20
        display.show(time_left)

    sleep(50)  # Pequeña pausa para optimizar el bucle
``` 
