Experimento 1

lectura de botones A y B

Objetivo:

Comprobar como s epueden leer los estados de los botonoes A y B 

Hipotesis:

Se espera que al presionar el boton A, muestre un mensaje indicando que el boton A esta presionado, y lo mismo para el boton B. Ademas, se espera que al presionar ambos botones simultaneamente muestre un mensaje diferente.

```py
from microbit import *

while True:
    if button_a.is_pressed() and button_b.is_pressed():
        display.scroll("A+B")
    elif button_a.is_pressed():
        display.scroll("A")
    elif button_b.is_pressed():
        display.scroll("B")
    sleep(300)
```
Resulados:

Al ejecutar el codigo, el micro:bit muestra os mensajes esperados en la pantalla LED cuandos se presiona los botones A y B o ambos simultaneamente 

Analisis: 

Los resultados se deben a la forma en que el código utiliza las funciones button_a.is_pressed() y button_b.is_pressed() para detectar el estado de los botones. La condición if button_a.is_pressed() and button_b.is_pressed(): permite detectar cuando ambos botones están presionados al mismo tiempo.

Conclusion:

El micro:bit puede leer los estados de los botones A y B de manera efectiva, permitiendo realizar acciones específicas según la combinación de botones presionados

--------------------------------------------------------------
Experimento 2:

Combinacion de botones para acciones especificas

Objetivo:

Comprobar cómo se pueden combinar los botones para realizar acciones específicas, como mostrar un mensaje o realizar una acción cuando se presionan en un orden determinado.

Hipotesis:

Se espera que al presionar los botones en un orden específico (por ejemplo, A y luego B), el micro:bit realice una acción diferente a presionarlos al mismo tiempo o por separado.

``` Py
from microbit import *

orden_correcto = False

while True:
    if button_a.is_pressed() and not orden_correcto:
        orden_correcto = True
        sleep(500)  # Espera medio segundo
    elif button_b.is_pressed() and orden_correcto:
        display.scroll("Si")
        orden_correcto = False
    elif button_b.is_pressed() and not orden_correcto:
        orden_correcto = False
        display.scroll("No")
    sleep(300)
```
Resultados

Al presionar el botón A y luego el botOn B en el orden correcto, el micro:bit muestra el mensaje "si". Si se presiona B primero, muestra "no".

Analisis

Los resultados se deben a la logica implementada en el codigo, que utiliza una variable "Si" para rastrear si el botón A ha sido presionado antes que B.

Conclusion 

El micro:bit permite combinar los botones para realizar acciones específicas basadas en el orden en que se presionan, lo que puede ser útil en juegos o aplicaciones interactivas.



