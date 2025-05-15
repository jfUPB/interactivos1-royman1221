Casos de Prueba Iniciales
  
Estado: Configuración

| Nº | Descripción                                                  | Resultado Esperado                                               |
| -- | ------------------------------------------------------------ | ---------------------------------------------------------------- |
| C1 | Presionar **UP** (A en micro\:bit o ↑ en p5.js)              | Incrementa el tiempo en 1 segundo. Se mantiene en Configuración. |
| C2 | Presionar **DOWN** (B en micro\:bit o ↓ en p5.js)            | Disminuye el tiempo en 1 segundo. Se mantiene en Configuración.  |
| C3 | Intentar bajar el tiempo por debajo de **10 segundos**       | El tiempo no cambia. Valor mínimo alcanzado.                     |
| C4 | Intentar subir el tiempo por encima de **60 segundos**       | El tiempo no cambia. Valor máximo alcanzado.                     |
| C5 | Realizar un **Shake** (micro\:bit) o presionar **A** (p5.js) | Transición al estado **Armado** e inicia la cuenta regresiva.    |

Estado: Armado

| Nº | Descripción                                                 | Resultado Esperado                                                         |
| -- | ----------------------------------------------------------- | -------------------------------------------------------------------------- |
| C6 | Permitir que el tiempo avance                               | El temporizador disminuye automáticamente cada segundo.                    |
| C7 | Tiempo llega a **0 segundos**                               | Se transita al estado **Explosión**.                                       |
| C8 | Presionar **Touch** (pin0 en micro\:bit o tecla T en p5.js) | Retorna al estado **Configuración** y el tiempo se reinicia a 20 segundos. |
| C9 | Presionar **UP** o **DOWN** en Armado                       | Sin efecto. No se permite modificar el tiempo en este estado.              |

Estado: Explosión

| Nº  | Descripción                            | Resultado Esperado                                                    |
| --- | -------------------------------------- | --------------------------------------------------------------------- |
| C10 | Entrar al estado Explosión             | Se muestra un ícono de explosión en pantalla y se activa el speaker.  |
| C11 | Presionar **Touch** (pin0 o tecla T)   | Retorna al estado Configuración. El tiempo se reinicia a 20 segundos. |
| C12 | Presionar **Shake**, **UP** o **DOWN** | Sin efecto. No se permite cambiar el estado desde Explosión.          |

Casos de Prueba Fallidos y Correcciones

| Caso | Problema                                                                             | Solución Aplicada                                                                                                                                    |
| ---- | ------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| C5   | No se activaba la transición al estado Armado con el evento **shake** en micro\:bit. | Se revisó y corrigió el uso del evento `was_gesture("shake")`. Además, se verificó la correcta transmisión del comando `ARMED` desde p5.js vía UART. |
| C7   | El sistema no cambiaba al estado Explosión cuando el tiempo llegaba a 0.             | Se implementó una condición `if (tiempo == 0)` en el ciclo principal para forzar la transición.                                                      |
| C8   | El botón **Touch** en p5.js no reiniciaba la bomba.                                  | Se corrigió enviando el comando `RESET` a través del canal UART hacia el micro\:bit.                                                                 |


Análisis: Técnica de Máquina de Estados y Pruebas de Regresión

¿Por qué es poderosa la técnica de máquina de estados?

* Manejo claro de eventos concurrentes: Cada estado tiene comportamientos definidos, facilitando el control del flujo incluso con múltiples eventos.

* Modularidad y escalabilidad: Se pueden añadir nuevos estados y transiciones sin romper la lógica existente.

* Depuración efectiva: Al tener límites claros entre estados, es más fácil detectar y corregir errores.

Ventajas y Desventajas del Tipo de Pruebas Realizadas

Ventajas:

* Cobertura completa de los estados posibles.

* Permite detectar errores en transiciones y eventos no considerados.

* Facilita la mejora continua del sistema y la validación de su lógica.

Desventajas:

* Alta demanda de tiempo y recursos por la repetición constante.

* No detectan de forma eficiente errores de integración, especialmente en la comunicación serial UART entre micro:bit y p5.js.

 Importancia de las Pruebas de Regresión
 
* Previenen regresiones: Aseguran que nuevas modificaciones no afecten funcionalidades previamente correctas.

* Mantienen la estabilidad del sistema: Son vitales en entornos con múltiples eventos y sensores, como micro:bit y p5.js.

* Detectan errores ocultos: Validan que todos los estados y transiciones aún funcionen correctamente después de cada cambio.
















