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


  









































