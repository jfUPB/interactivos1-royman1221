``` py
from microbit import *

uart.init(115200)
display.set_pixel(0,0,9)

while True:
    xValue = accelerometer.get_x()
    yValue = accelerometer.get_y()
    aState = button_a.is_pressed()
    bState = button_b.is_pressed()
    data = "{},{},{},{}\n".format(xValue, yValue, aState, bState)
    uart.write(data)
    sleep(100)
```
1.  ¿Qué información se está enviando?

* xValue: valor del eje X del acelerómetro.

* yValue: valor del eje Y del acelerómetro.

* aState: estado del botón A (True o False).

* bState: estado del botón B (True o False).

2. ¿Cómo se está enviando?

Se están enviando a través del puerto serial (UART) en formato de texto plano, usando una cadena separada por comas y terminada con un salto de línea (\n).

¿Qué significa esta parte del código?

``` py
"{},{},{},{}\n".format(xValue, yValue, aState, bState)
```
Esto es una cadena formateada, donde:

{} son marcadores de posición para insertar valores.

.format(...) reemplaza cada {} por el valor correspondiente (en orden).

3. ¿Qué puedes inferir de la estructura de los datos?

* Es una línea CSV (valores separados por comas).

* Esto facilita su lectura y separación posterior en p5.js o cualquier otro software.

* La línea termina con un salto de línea, lo cual indica el fin del paquete de datos.

 4. ¿Por qué se separan los datos con comas y se termina con un salto de línea?

 Las comas permiten separar y distinguir cada valor individual.

El salto de línea (\n) indica que todos los valores de una "medición" ya fueron enviados. Esto es útil para el receptor (como p5.js) que espera leer línea por línea.

5. ¿Qué pasaría si no se separan los datos con comas y no terminan con un salto de línea?

Sin comas: los valores estarían pegados, y sería difícil separarlos correctamente. Sin salto de línea: el receptor no sabría cuándo termina una muestra y empieza otra, lo que causaría problemas de sincronización de datos.

6. ¿Para qué se usa la función sleep(100)? ¿Qué pasaría si no se usara?

* sleep(100) detiene el programa por 100 ms, es decir, envía los datos cada 0.1 segundos (10 Hz).

* Si no se usara, el micro:bit enviaría datos demasiado rápido, saturando la conexión y haciendo que el receptor no pueda procesarlos a tiempo (lo que puede causar errores o pérdidas).

7. ¿Qué valores toman xValue y yValue al inclinar el micro:bit?

   xValue:

* Izquierda: valor negativo (hasta ~ -1024).

* Derecha: valor positivo (hasta ~ 1024).

  yValue:

* Adelante: valor positivo (hasta ~ 1024).

* Atrás: valor negativo (hasta ~ -1024).

* En reposo (horizontal), ambos tienden a estar cerca de 0.


8. ¿Qué valores toman aState y bState cuando presionas los botones A y B?

* Si presionas A: aState = True.

* Si sueltas A: aState = False.

* Lo mismo con B.

9. ¿Diferencias entre is_pressed() y was_pressed()?

   is_pressed():

* Devuelve True mientras el botón está presionado.

  was_pressed():

* Devuelve True solo una vez después de que se presiona el botón, luego vuelve a False.

10.  Si se envían estos datos: xValue: 969, yValue: 652, aState: True, bState: False, ¿qué bytes se enviarían?

Se enviaría esta cadena de texto:

969,652,True,False\n

Bytes en ASCII (hexadecimal):

39 36 39 2C 36 35 32 2C 54 72 75 65 2C 46 61 6C 73 65 0A

* 969 = 39 36 39

* , = 2C

* 652 = 36 35 32

* True = 54 72 75 65

* False = 46 61 6C 73 65

* \n = 0A










