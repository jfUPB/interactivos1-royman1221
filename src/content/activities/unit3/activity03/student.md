``` py
from microbit import *
Import uart


uart.init(baudrate=115200)

evento_ocurrido = False
evento_tipo = ''

def tareaEventos():
    global evento_ocurrido, evento_tipo

    if button_a.was_pressed():
        evento_ocurrido = True
        evento_tipo = 'A'
    elif button_b.was_pressed():
        evento_ocurrido = True
        evento_tipo = 'B'
    elif accelerometer.was_gesture('shake'):
        evento_ocurrido = True
        evento_tipo = 'S'
    elif pin_logo.is_touched():
        evento_ocurrido = True
        evento_tipo = 'T'

    if uart.any():
        mensaje = uart.read()
        if mensaje:
            mensaje = mensaje.decode().strip()
            if mensaje in ['A', 'B', 'S', 'T']:
                evento_ocurrido = True
                evento_tipo = mensaje

def tareaBomba():
    global evento_ocurrido, evento_tipo

    if evento_ocurrido:
        if evento_tipo == 'A':
            display.show("A")
         
        elif evento_tipo == 'B':
            display.show("B")
         
        elif evento_tipo == 'S':
            display.show("S")
            
        elif evento_tipo == 'T':
            display.show("T")
         
        evento_ocurrido = False
        sleep(500)
        evento_tipo = ''
    else:
        display.clear()

while True:
    tareaEventos()
    tareaBomba()
```

Inicialización del puerto serial:
Se configura la comunicación UART con una velocidad de 115200 baudios para permitir la recepción de datos a través del puerto serial.

Manejo de eventos (tareaEventos):
Esta función se encarga de detectar si se ha producido algún evento en el micro:bit, como la pulsación de los botones A o B, un movimiento de "shake" o un toque ("touch").
Además, verifica si se ha recibido un mensaje válido por el puerto serial. Si es así, almacena el tipo de evento en la variable evento_tipo y establece la bandera evento_ocurrido en True para indicar que hay un evento pendiente por procesar.

Máquina de estados de la bomba (tareaBomba):
Cuando se detecta que evento_ocurrido es True, se muestra el tipo de evento en el display del micro:bit y se ejecuta la acción correspondiente.
Una vez que el evento ha sido procesado, las variables evento_ocurrido y evento_tipo se reinician (evento_ocurrido = False, evento_tipo = "") para dejar el sistema listo para capturar un nuevo evento.

Bucle principal (while True):
En el ciclo principal del programa:

* Se llama a tareaEventos() para capturar eventos del usuario o del puerto serial.

* Se llama a tareaBomba() para procesar cualquier evento detectado.

* Se incluye una pausa de 100 milisegundos (sleep(100)) para evitar que el programa se ejecute demasiado rápido, reduciendo así el consumo de recursos y mejorando la eficiencia del sistema.
