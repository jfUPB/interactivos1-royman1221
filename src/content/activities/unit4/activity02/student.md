Variables globales

* c : Representa el color actual que se utilizará para dibujar.

* lineModuleSize : Define el tamaño del módulo de línea (el objeto que se rota y dibuja).

* angle : Define el ángulo de rotación del módulo.

* angleSpeed : Define la velocidad con la que rota el módulo.

* lineModule : Es un arreglo donde se almacenan las imágenes SVG que se usarán como módulos para dibujar.

* lineModuleIndex : Índice para seleccionar qué módulo SVG utilizar.

* clickPosX y clickPosY : Guardan las posiciones del clic del ratón para controlar la dirección del dibujo.

Funcion preload()

* lineModule[1]: cargará la imagen 'data/02.svg'.

* lineModule[2]: cargará la imagen 'data/03.svg', y así sucesivamente.


funcion Setup ()

* createCanvas(windowWidth, windowHeight): Crea un lienzo de dibujo del tamaño de la ventana del navegador.

* background(255): Establece el color de fondo blanco.

* noCursor(): Elimina el cursor del ratón.

* strokeWeight(0.75): Establece el grosor de la línea utilizada en el dibujo.

* Inicializa el color c con un valor de amarillo: color(181, 157, 0).


Función windowResized()

* Asegura que el lienzo se ajuste automaticamente cuando se cambie el tamaño de la ventana del navegador


Función draw()

* Esta función se ejecuta en un bucle constante mientras la página esté abierta:

* Si el ratón está presionado (click izquierdo), se obtiene la posición del ratón (mouseX y mouseY).

* Si la tecla Shift está presionada, se limita la dirección del dibujo, de modo que se dibuje solo en una línea recta horizontal o vertical, dependiendo de la mayor distancia entre las posiciones inicial y actual.

* Se transforma la posición (translate(x, y)) y la rotación (rotate(radians(angle))) de la figura a dibujar.

* Dependiendo del valor de lineModuleIndex, se dibuja una imagen SVG desde el arreglo lineModule o una línea simple (si lineModuleIndex == 0).

* Luego, el ángulo de rotación se incrementa por angleSpeed, haciendo que la figura gire.

* Si no se presiona el ratón, no se dibuja nada.

Función mousePressed

* Esta función se activa cuando se presiona el ratón:

* Se genera un tamaño aleatorio para el módulo de línea (lineModuleSize).

* Se guarda la posición del clic del ratón (clickPosX, clickPosY).

Función keyPressed()

* Se activan diferentes acciones dependiendo de la tecla presionada:

* Teclas de flecha (Arriba y Abajo): Cambian el tamaño del módulo de línea (lineModuleSize).

* Teclas de flecha (Izquierda y Derecha): Ajustan la velocidad de rotación (angleSpeed).

Función keyReleased()

* Esta función maneja las acciones de las teclas cuando se sueltan:

* Tecla s: Guarda el lienzo como una imagen PNG.

* Teclas Delete o Backspace: Limpian el lienzo.

* Tecla d: Invierte la dirección de rotación y refleja el ángulo.

* Tecla Espacio: Cambia a un nuevo color aleatorio.

* Teclas 1-4: Cambian el color predeterminado.

* Teclas 5-9: Cambian el módulo de línea (SVG).

Interacciones y Funcionalidades

* El sketch es completamente interactivo, usando el ratón para dibujar y las teclas para cambiar parámetros de dibujo (como el color, la dirección de rotación y el tamaño del módulo).

* El color y el módulo de línea pueden cambiar dinámicamente mediante las teclas del 1 al 9 y la barra espaciadora.

* La dirección de rotación se puede invertir con la tecla d, mientras que la velocidad de rotación y el tamaño del módulo se ajustan con las flechas.









































