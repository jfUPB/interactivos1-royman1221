* Compara el código original con el anterior. ¿Qué notas de diferente?
El código original parece estar diseñado para un proyecto de diseño generativo más amplio, con varias dependencias. El nuevo index.html está simplificado, eliminando esas dependencias y añadiendo específicamente la biblioteca p5.webserial para la comunicación con el micro:bit.

* Reflexiona ¿Para qué se usan estas imágenes? ¿Qué representan?
Son “pinceles” o módulos de línea que permiten dibujar formas distintas, controladas directamente por las señales enviadas desde el micro:bit.

* ¿Recuerdas que en las unidades anteriores teníamos un pseudoestado llamado INIT? ¿Dónde está?
La función setup() cumple el rol de INIT, ya que realiza toda la configuración inicial necesaria para la aplicación.

* ¿Qué pasaría al hacer clic en el botón?
El botón alterna entre abrir el puerto serial si está cerrado o cerrarlo si está abierto.

* ¿Para qué abres el puerto serial?
Para establecer una conexión que permita recibir datos del micro:bit, como la posición y el estado de sus botones.

* ¿Por qué solo se leen datos con el puerto abierto?
Porque la comunicación serial solo es posible cuando la conexión está activa; sin ella, no se puede recibir información.

* ¿Se pueden leer datos con el puerto cerrado?
No, ya que sin un puerto abierto no existe canal de comunicación para recibir datos.

* ¿Qué pasa si el micro:bit envía datos con el puerto cerrado?
Los datos enviados se pierden porque no hay una conexión activa para recibirlos.

* ¿Qué pasa si el micro:bit no envía “\n”?
La función readUntil() esperará indefinidamente el carácter de nueva línea, lo que puede bloquear la lectura y evitar que los datos se procesen correctamente.

* ¿Por qué se suma windowWidth/2 y windowHeight/2 a x e y?
Para centrar el origen de coordenadas del micro:bit en el centro de la ventana, facilitando la interpretación visual de las posiciones.

* ¿Cómo verificar los eventos keyPressed y keyReleased?
Observando los mensajes impresos en la consola y el comportamiento visual de la aplicación cuando se presionan o sueltan teclas.

* ¿Qué hace updateButtonStates? ¿Por qué el estado anterior? ¿Qué pasaría sin él?
updateButtonStates detecta cuándo se presionan o sueltan los botones del micro:bit. El estado anterior es necesario para identificar las transiciones entre presionado y liberado; sin él, las acciones se ejecutarían continuamente mientras el botón esté en un estado, sin distinguir cambios.

* ¿Diferencias entre códigos? ¿Eventos del ratón? ¿Barra espaciadora?
El nuevo código está enfocado en controlar el micro:bit, por lo que elimina eventos del ratón y teclado presentes en el código original. La interacción se adapta a los botones y sensores del micro:bit, dejando de lado eventos como la barra espaciadora o clics del ratón.
