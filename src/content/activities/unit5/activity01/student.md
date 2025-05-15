Comunicación entre micro:bit y p5.js

Datos enviados por el micro:bit

El micro:bit transmite por UART (serial) los siguientes datos cada 100 ms (10 veces por segundo):

* Valor del acelerómetro en X (xValue)

* Valor del acelerómetro en Y (yValue)

* Estado del botón A (aState, True/False)

* Estado del botón B (bState, True/False)

Estructura del protocolo ASCII

* Separador de campos: coma (,).

* Fin de mensaje: salto de línea (\n).

* Orden de los datos: xValue, yValue, aState, bState.

* Tipos de datos:

    * xValue, yValue: enteros (acelerómetro)

    * aState, bState: booleanos (True/False)

Lectura y transformación de datos en p5.js

En el sketch de p5.js, la lectura y procesamiento ocurre en el ciclo principal (draw()):

* Se verifica si hay datos disponibles en el puerto serial.

* Se lee la cadena hasta el salto de línea.

* Se eliminan espacios y saltos de línea.

* Se divide la cadena en partes usando la coma como separador.

* Si hay cuatro valores, se convierten:

    * xValue e yValue se transforman en enteros y se ajustan al centro de la pantalla sumando windowWidth/2 y windowHeight/2.

    * aState y bState se convierten a booleanos (comparando si el string es "true").

    * Se llama a la función updateButtonStates() para procesar los eventos de botones.

Fragmento de código

``` js
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    }
  }
}
```
Generación de eventos "A pressed" y "B released"

La función updateButtonStates() compara el estado actual y el anterior de los botones para detectar cambios:

* Si el botón A pasa de no presionado a presionado (false → true), se genera el evento "A pressed" y se actualizan variables relacionadas con el dibujo.

* Si el botón B pasa de presionado a no presionado (true → false), se genera el evento "B released" y se cambia el color de dibujo.

* Al final, los estados anteriores se actualizan para la siguiente comparación.

Fragmento de código

``` js
function updateButtonStates(newAState, newBState) {
  if (newAState === true && prevmicroBitAState === false) {
    lineModuleSize = random(50, 160);
    clickPosX = microBitX;
    clickPosY = microBitY;
    print("A pressed");
  }
  if (newBState === false && prevmicroBitBState === true) {
    c = color(random(255), random(255), random(255), random(80, 100));
    print("B released");
  }
  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}
```


