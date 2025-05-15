Estado: Configuración

Funciones del estado:

* Muestra el tiempo configurado en la matriz de LEDs del micro:bit.

* Al presionar el Botón A, el tiempo aumenta en intervalos de 1 segundo.

* Al presionar el Botón B, el tiempo disminuye en intervalos de 1 segundo.

* Se limita el tiempo entre 10 y 60 segundos para evitar valores inválidos.

Cambio de estado:

* Si se detecta un movimiento tipo “shake”, se transita al estado Cuenta Regresiva.

Estado: Cuenta Regresiva

Funciones del estado:

* Inicia un temporizador que cuenta hacia atrás desde el tiempo configurado.

* El tiempo restante se muestra en la pantalla LED durante todo el proceso.

Cambio de estado:

* Si el temporizador llega a 0, se cambia automáticamente al estado Explosión.

* Si el usuario toca el sensor (evento Touch), se cancela la cuenta regresiva y se regresa a Configuración.

Estado: Cuenta Regresiva

Funciones del estado:

* Inicia un temporizador que cuenta hacia atrás desde el tiempo configurado.

* El tiempo restante se muestra en la pantalla LED durante todo el proceso.

Cambio de estado:

* Si el temporizador llega a 0, se cambia automáticamente al estado Explosión.

* Si el usuario toca el sensor (evento Touch), se cancela la cuenta regresiva y se regresa a Configuración.

Estado: Explosión

Funciones del estado:

* Se reproduce un sonido de alerta a través del altavoz.

* Se despliega un patrón visual tipo explosión en la pantalla del micro:bit.

Cambio de estado:

* Si el usuario toca el sensor nuevamente (evento Touch), el sistema vuelve a Configuración.

| Nº | Escenario                                                 | Resultado Esperado                                       |
| -- | --------------------------------------------------------- | -------------------------------------------------------- |
| 1  | En estado de configuración, presionar botón A             | Incrementa tiempo en 1s, permanece en Configuración      |
| 2  | En estado de configuración, presionar botón B             | Decrementa tiempo en 1s, permanece en Configuración      |
| 3  | En configuración, realizar un movimiento (shake)          | Cambia a Cuenta Regresiva e inicia conteo                |
| 4  | En Cuenta Regresiva, el tiempo llega a 0                  | Transición automática a Explosión                        |
| 5  | En Cuenta Regresiva, tocar el micro\:bit                  | Se cancela la cuenta regresiva y regresa a Configuración |
| 6  | En Explosión, tocar el micro\:bit                         | Retorna al estado de Configuración                       |
| 7  | En Configuración, intentar bajar tiempo por debajo de 10s | El tiempo se mantiene en 10s, sin cambios                |
| 8  | En Configuración, intentar subir tiempo por encima de 60s | El tiempo se mantiene en 60s, sin cambios                |



| Caso | Descripción del Error                                                        | Solución Implementada                                                                   |
| ---- | ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| 3    | El sistema no cambiaba al estado de Cuenta Regresiva al agitar el micro\:bit | Se añadió detección correcta del evento "shake" en el controlador de eventos            |
| 7    | Permitía configurar tiempo menor a 10s                                       | Se implementó condición para validar el límite inferior del tiempo antes de modificarlo |













