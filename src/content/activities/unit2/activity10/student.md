Concurrencia en el Programa
Este programa implementa una máquina de estados finitos para gestionar la secuencia de expresiones faciales en la pantalla del micro:bit, mientras atiende eventos de botón simultáneamente. La concurrencia se logra mediante el uso de:

* Máquina de estados: Define los estados HAPPY, SMILE y SAD, con transiciones basadas en el tiempo y en la pulsación del botón A.
* Manejo de eventos en paralelo: La secuencia de imágenes avanza automáticamente con temporizadores (utime.ticks_ms()), pero el programa también verifica continuamente si el botón A ha sido presionado, permitiendo interrupciones en cualquier momento.
* Condiciones de transición: Si el tiempo de un estado expira, el programa cambia al siguiente estado en la secuencia. Pero si el usuario presiona el botón A, la transición ocurre de inmediato, modificando la secuencia normal.

Vector 1: Secuencia Normal (Sin Pulsaciones)
  
Condición Inicial: El micro:bit inicia en STATE_HAPPY.
Eventos Generados: No se presiona el botón A, solo se espera el cambio de estados por tiempo.
Resultados Esperados:

* HAPPY → SMILE después de 1500 ms.
* SMILE → SAD después de 1000 ms.
* SAD → HAPPY después de 2000 ms.
  
Resultados Obtenidos: Si la secuencia sigue este flujo sin interrupciones, el sistema pasa la prueba.


Vector 2: Interrupción en HAPPY con Botón A

Condición Inicial: El micro:bit está en STATE_HAPPY.
Eventos Generados: Se presiona el botón A antes de que pasen 1500 ms.
Resultados Esperados:

* El micro:bit cambia inmediatamente a STATE_SAD, sin esperar el tiempo de HAPPY.
* SAD dura 2000 ms antes de cambiar a HAPPY.
  
Resultados Obtenidos: Si al presionar A, la cara cambia de HAPPY a SAD sin esperar el tiempo, la prueba se considera exitosa.


Vector 3: Interrupción en SAD con Botón A

Condición Inicial: El micro:bit está en STATE_SAD.
Eventos Generados: Se presiona el botón A antes de que pasen 2000 ms.
Resultados Esperados:

* El micro:bit cambia inmediatamente a STATE_SMILE.
* SMILE dura 1000 ms antes de cambiar a SAD nuevamente.
  
Resultados Obtenidos: Si al presionar A, la cara cambia de SAD a SMILE sin esperar los 2000 ms, la prueba es exitosa.
