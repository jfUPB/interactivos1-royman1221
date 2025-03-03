Entradas:
Botones A y B: Permite detectar pulsaciones independientes p simultaneas
Sensor de luz: Mide la intensidad de la luz ambiente 
Sensor de temperatura: Mide la intensidad de la temperatura en grados celcius
Acelerometro: Detecta movimientos y aceleraciones 

Salidas: 
Matriz LED: Muestra texto, imagenes y números
Altavoz: Emite sonidos y tonos
Bluetooth y Radio: Envia datos a otros dispositivoa
Pines GPIO: Permite conectar y controlar dispositivos externos como LEDs o motores

Funciones Entrada: 

``` py
from microbit import *

while True:
    if button_a.is_pressed():
        print("Botón A presionado")
    if button_b.is_pressed():
        print("Botón B presionado")
```
``` py
from microbit import *

while True:
    luz = display.read_light_level()
    print("Nivel de luz:", luz)
```
``` py
from microbit import *

while True:
    temperatura = temperature()
    print("Temperatura:", temperatura)
```
Funciones Salida:

``` py
from microbit import *

display.scroll("Hola, mundo!")
```
``` py
from microbit import *

music.play(music.BA_DING)
```
``` py
from microbit import *

pin0.write_digital(1)  # Enciende el LED conectado al pin 0

```
















