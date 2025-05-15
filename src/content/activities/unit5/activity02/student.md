Experimento 1: Visualización de datos en modo Texto

Configuración:

SerialTerminal en modo “Texto”, con el código original modificado para enviar datos en formato binario.

Resultado:

Se observan caracteres aleatorios, símbolos y a veces espacios en blanco.

Análisis:

El modo texto intenta interpretar los bytes como caracteres ASCII. Como los datos enviados son binarios (no codificados en ASCII), se muestran caracteres sin sentido o símbolos de control no imprimibles.

Ejemplo:

Si xValue = 1024 (hexadecimal 0x0400), se envían los bytes 0x04 y 0x00, los cuales no corresponden a caracteres visibles en ASCII.


Experimento 2: Visualización en modo “Todo en Hex”

Configuración:

SerialTerminal configurado en modo Hexadecimal.

Resultado:

Se observan secuencias de bytes en hexadecimal, por ejemplo:

00 1F 01 A0 00 01

(correspondientes a x = 31, y = 416, a = 0, b = 1)

Relación con struct.pack('>2h2B', ...):

* 2h: dos valores tipo short (2 bytes cada uno) para xValue e yValue

Ejemplo: x = 31 → 00 1F (formato big-endian)

* 2B: dos valores tipo unsigned char (1 byte cada uno) para aState y bState

Ejemplo: a = 0, b = 1 → 00 01

Ventajas y Desventajas: Binario vs ASCII

| **Criterio**  | **Binario**                         | **ASCII**                              |
| ------------- | ----------------------------------- | -------------------------------------- |
| Tamaño        | ✅ Más pequeño (6 bytes por mensaje) | ❌ Más grande (10–15 bytes por mensaje) |
| Velocidad     | ✅ Más rápido de transmitir          | ❌ Más lento                            |
| Legibilidad   | ❌ Difícil (requiere herramientas)   | ✅ Legible para humanos                 |
| Procesamiento | ✅ Directo para la máquina           | ❌ Requiere parsing (ej. `split(",")`)  |


Experimento 3: Envío con “shake” y conteo de bytes
Configuración:
Código modificado para enviar datos solo cuando se agita el micro:bit (shake gesture).

Resultado:
Cada mensaje ocupa exactamente 6 bytes:

* 2 bytes para xValue (ej: 0x00 1F)

* 2 bytes para yValue (ej: 0x01 A0)

*  1 byte para aState (ej: 0x00)

* 1 byte para bState (ej: 0x01)

Relación con struct.pack('>2h2B'):

* 2h = 4 bytes (dos valores short)

* 2B = 2 bytes (dos valores unsigned char)

* Total: 6 bytes por mensaje

Números negativos:

Se representan usando complemento a 2.

Ejemplo: xValue = -10 → 0xFF 0xF6 (big-endian)


Experimento 4: Comparación directa ASCII vs Binario

Configuración:

Se envían ambos formatos al agitar el micro:bit.

Resultado:

* ASCII: "31,416,0,1\n" → 10 bytes (legible)

* Binario: 00 1F 01 A0 00 01 → 6 bytes (compacto)

Diferencias clave:

ASCII:

* ✅ Legible y fácil de depurar
  
❌ Ineficiente por tamaño y parsing

Binario:

* ✅ Eficiente en transmisión (ideal para sensores)
  
❌ Requiere herramientas y documentación para interpretación




















