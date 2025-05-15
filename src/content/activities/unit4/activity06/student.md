1. ¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial?
Un protocolo es un conjunto de reglas que define cómo se intercambian los datos entre dispositivos. En comunicación serial es crucial para que el receptor interprete correctamente la información recibida. Por ejemplo, en mi código uso un protocolo que separa valores con comas y termina con un salto de línea para indicar el fin del mensaje:

```py
serial.write("{},{},{},{}\n".format(x, y, aState, bState))

```
2. ¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos?
Las comas actúan como delimitadores que permiten identificar cada valor individual dentro de la cadena de texto recibida. Esto facilita dividir la cadena en partes usando funciones como split(",") en p5.js.

3. ¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje?
Porque la función readUntil("\n") en p5.js espera hasta encontrar ese carácter para saber que el mensaje está completo y listo para procesar. Sin este carácter, la lectura se bloquearía indefinidamente.

4. ¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js?
Para gestionar diferentes comportamientos según el estado de la conexión con el micro:bit, como esperar a que se abra el puerto o procesar datos cuando está activo. Esto evita errores y mantiene el flujo controlado.

5. ¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial?
Se convierten en una cadena de texto con valores separados por comas y terminada en salto de línea, por ejemplo:

```py
uart.write("{},{},{},{}\n".format(xValue, yValue, aState, bState))
```
6. ¿Qué significa que los datos enviados por el micro:bit están codificados en ASCII?
Significa que cada carácter de la cadena es representado por un número que corresponde a su código ASCII, lo que permite transmitir texto legible y fácil de interpretar en el receptor.

7. ¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos?
Para evitar intentar leer cuando no hay datos, lo que podría causar errores o bloqueos en el programa. Por eso se usa:

```py
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
}
```

8. ¿Cómo se elimina el retorno de carro o salto de línea de un string en p5.js?
Usando el método trim(), que elimina espacios en blanco y caracteres de nueva línea al inicio y final de la cadena.

9. Si una cadena tiene información separada por espacios y quieres dividir dicha información en varias cadenas individuales ¿Qué función de p5.js usarías?
La función split(" ") permite dividir la cadena en un arreglo de subcadenas separadas por espacios.

10. ¿Por qué es necesario en la aplicación del caso de estudio convertir las cadenas a números enteros antes de usarlas en el sketch de p5.js?
Porque los datos recibidos son texto y para realizar operaciones matemáticas o evaluar condiciones booleanas es necesario convertirlos a su tipo numérico o lógico con funciones como int() o boolean().

11. Si el micro:bit tiene los siguientes datos xValue: 123, yValue: 756, aState: False, bState: True ¿Qué bytes se enviarían por el puerto serial?
Se enviarían los códigos ASCII de los caracteres que forman la cadena "123,756,False,True\n", es decir:

49, 50, 51, 44, 55, 53, 54, 44, 70, 97, 108, 115, 101, 44, 84, 114, 117, 101, 10

12. ¿Qué aprendiste nuevo del micro:bit que no sabías antes?
Aprendí cómo formatear datos para enviarlos por puerto serial y cómo controlar sus sensores y botones para interactuar con programas externos.

13. ¿Qué aprendiste nuevo de p5.js que no sabías antes?
Descubrí cómo usar la biblioteca p5.webserial para establecer comunicación serial y cómo procesar datos recibidos en tiempo real para controlar gráficos y animaciones.
