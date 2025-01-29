#### En micro
```py
from microbit import *

# Inicializa UART para comunicación
uart.init(baudrate=115200)

while True:
    if uart.any():
        command = uart.read(1)  
        if command:
            if command[0] == ord('H'):
                display.show(Image.HAPPY)  # Muestra la imagen feliz
            elif command[0] == ord('S'):
                display.show(Image.SAD)  # Muestra la imagen triste
            elif command[0] == ord('G'):
                display.show(Image.GIRAFFE)  # Muestra la imagen de la jirafa
            elif command[0] == ord('P'):
                display.show(Image.PACMAN)  # Muestra la imagen de Pacman
```
