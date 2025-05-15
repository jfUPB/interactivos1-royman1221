 Estado: Configuración
 
| Nº | Acción                                                         | Resultado Esperado                                              |
| -- | -------------------------------------------------------------- | --------------------------------------------------------------- |
| C1 | Presionar **UP** (A en micro\:bit o ↑ en p5.js)                | Aumenta el tiempo en 1 segundo. Se mantiene en Configuración.   |
| C2 | Presionar **DOWN** (B en micro\:bit o ↓ en p5.js)              | Disminuye el tiempo en 1 segundo. Se mantiene en Configuración. |
| C3 | Intentar bajar el tiempo por debajo de **10 segundos**         | El tiempo no cambia (mínimo alcanzado).                         |
| C4 | Intentar subir el tiempo por encima de **60 segundos**         | El tiempo no cambia (máximo alcanzado).                         |
| C5 | Realizar un **Shake** (ARMED en micro\:bit o tecla A en p5.js) | Se transita al estado Armado e inicia la cuenta regresiva.      |

 Estado: Armado 

 | Nº | Acción                                                      | Resultado Esperado                                                   |
| -- | ----------------------------------------------------------- | -------------------------------------------------------------------- |
| C6 | Permitir que el tiempo avance                               | La cuenta regresiva disminuye automáticamente cada segundo.          |
| C7 | Tiempo llega a **0 segundos**                               | Transición automática al estado Explosión.                           |
| C8 | Presionar **Touch** (pin0 en micro\:bit o tecla T en p5.js) | Regresa a Configuración y el tiempo se restablece a **20 segundos**. |
| C9 | Presionar **UP** o **DOWN** durante la cuenta regresiva     | No se altera el tiempo; se ignoran los botones.                      |

 Estado: Explosión

 | Nº  | Acción                                     | Resultado Esperado                                                         |
| --- | ------------------------------------------ | -------------------------------------------------------------------------- |
| C10 | El sistema entra en Explosión              | Se muestra un ícono de explosión en la pantalla y el altavoz emite sonido. |
| C11 | Presionar **Touch** (pin0 o tecla T)       | Retorna a Configuración y el tiempo se restablece a 20 segundos.           |
| C12 | Intentar usar **Shake**, **UP** o **DOWN** | No se produce ningún cambio; las entradas son ignoradas.                   |

Casos Fallidos Detectados y Soluciones Aplicadas

| Caso | Problema Identificado                                                      | Solución Implementada                                                                                                                  |
| ---- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| C5   | El evento **Shake** no provocaba transición al estado Armado en micro\:bit | Se verificó y corrigió el uso de `was_gesture("shake")`. Además, se ajustó la recepción del comando “ARMED” desde p5.js mediante UART. |
| C7   | El sistema no cambiaba al estado Explosión al llegar a 0 segundos          | Se agregó la condición `if (tiempo == 0)` dentro del bucle principal para activar la transición.                                       |
| C8   | El botón Touch en p5.js no reiniciaba el sistema                           | Se solucionó enviando el comando `RESET` correctamente a través de UART para reiniciar el tiempo y el estado.                          |

