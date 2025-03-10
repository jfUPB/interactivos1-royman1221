Ese código muestra un corazón en la pantalla LED del micro:bit y lo mantiene visible con sleep(1000), repitiéndose indefinidamente dentro de un while True. Para adaptarlo a la recepción de datos seriales, se puede modificar para que en lugar de mostrar un corazón fijo, lea un carácter enviado por el puerto serial y lo muestre en la pantalla.
```py
# Imports go at the top
from microbit import *


# Code in a 'while True:' loop repeats forever
while True:
    display.show(Image.HEART)
    sleep(1000)
```
