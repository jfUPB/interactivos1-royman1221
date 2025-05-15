Casos de Prueba

Caso de Prueba 1: Ajuste del tiempo con los botones
Descripción: Se presionan los botones A y B para aumentar y disminuir el tiempo configurado.
Entrada: Botón A presionado repetidamente, luego botón B presionado repetidamente.
Resultado esperado: El tiempo incrementa hasta el máximo permitido (60s) y decrementa hasta el mínimo permitido (10s).
Resultado obtenido: Funcionamiento correcto.
Correcciones: No fueron necesarias.

Caso de Prueba 2: Armado de la bomba con el gesto "shake"
Descripción: Se agita la micro:bit para armar la bomba.
Entrada: Gesto "shake".
Resultado esperado: Cambio de estado a "ARMED" y inicio de la cuenta regresiva.
Resultado obtenido: La detección del gesto era intermitente.
Correcciones: Se ajustó la detección del gesto para mejorar la sensibilidad.

Caso de Prueba 3: Cuenta regresiva y actualización de pantalla
Descripción: Se verifica que el tiempo disminuya correctamente cada segundo y que la pantalla se actualice.
Entrada: Estado "ARMED" activado.

Resultado esperado: El tiempo se muestra en pantalla y decrementa cada segundo.
Resultado obtenido: Ocasionalmente, la pantalla no actualizaba correctamente el tiempo.
Correcciones: Se modificó el manejo del tiempo para mayor precisión.

Caso de Prueba 4: Explosión al llegar a 0
Descripción: Se deja que la cuenta regresiva llegue a 0.
Entrada: Bomba en estado "ARMED" con tiempo decreciendo.
Resultado esperado: Cambio de estado a "EXPLODED", se muestra la imagen de calavera y se reproduce un sonido.
Resultado obtenido: La imagen se mostraba correctamente, pero el sonido no siempre se reproducía.
Correcciones: Se optimizó la llamada a music.play() para asegurar la ejecución del sonido.

Caso de Prueba 5: Reinicio al tocar el logo dorado
Descripción: Se toca el logo dorado para reiniciar la bomba en cualquier estado.
Entrada: Se toca pin_logo.
Resultado esperado: Reinicio al estado "CONFIG" y restablecimiento del tiempo a 20s.
Resultado obtenido: Funcionamiento correcto en la mayoría de los casos, pero en estado "EXPLODED" a veces no reiniciaba inmediatamente.
