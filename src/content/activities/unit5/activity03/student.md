Diferencias entre formato de texto delimitado y formato binario

Formato texto (anterior):

* Utiliza delimitadores (comas) y un salto de línea (\n) para separar los datos.

* Ventajas:

    * Legible para humanos, ideal para depuración.

    * Flexible en longitud, útil para datos de distintos tamaños.

    * Fácil de sincronizar: el salto de línea marca el fin de cada paquete.

Formato binario (actual):

* Utiliza una estructura de tamaño fijo (6 bytes por paquete).

* Ventajas:

    * No requiere delimitadores, lo que reduce el tamaño del mensaje.

    * Mayor eficiencia: menos sobrecarga por caracteres innecesarios.

    * Precisión: los valores se mantienen como enteros, sin necesidad de conversión a texto.
 
Comparación entre el código en p5.js anterior y el actual

```jv
let str = port.readUntil("\n");
let values = str.trim().split(",");
microBitX = int(values[0]);
microBitY = int(values[1]);
```
Versión actual (binario):

``` jv
let data = port.readBytes(6);
const view = new DataView(buffer);
microBitX = view.getInt16(0);
microBitY = view.getInt16(2);
```

* Se eliminó el parsing de strings.

* Se usan offsets fijos para extraer datos directamente de los bytes.

* No hay conversión de texto a números, lo que mejora el rendimiento.

Error de sincronización observado

Problema:

* Se registraban valores incoherentes, como microBitX: 3073 y microBitY: 1.

Causa:

* El puerto serial leía desde un byte intermedio del paquete (no alineado al inicio), lo que generaba interpretaciones erróneas.

* Por ejemplo, si xValue = 0x01F4, y se comienza a leer desde el segundo byte (F4 02), el valor interpretado es 0xF402 = 62466.

Solución implementada: Framing con Header y Checksum

Micro:bit:

``` py
packet = b'\xAA' + data + bytes([checksum])  # Paquete total: 8 bytes
```
p5.js:

``` js
if (serialBuffer[0] !== 0xAA) serialBuffer.shift();  // Buscar header
let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;
```

Ventajas del nuevo enfoque:

* Sincronización confiable: el header 0xAA permite detectar el inicio del paquete.

* Detección de errores: el checksum valida la integridad del mensaje.

* Mayor robustez: se ignoran los datos corruptos y solo se procesan paquetes válidos.

Cambios finales en los programas

Micro:bit:

* Lectura de acelerómetro (get_x() y get_y()) y botones físicos (button_a.is_pressed()).

* Implementación de framing (header + checksum).

p5.js:

* Ajuste visual de coordenadas para centrar elementos (+ windowWidth / 2).

* Limpieza de consola: eliminación de logs innecesarios.

Resultado:

* Se obtienen lecturas consistentes, como microBitX: 523 y microBitY: -102, sin errores de interpretación.




















