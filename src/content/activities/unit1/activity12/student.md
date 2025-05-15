#### En micro
```py
from microbit import *

# Inicializa UART para comunicación
uart.init(baudrate=115200)

while True:
    if uart.any():
        command = uart.read(1)  
        if command:
            if command[0] == ord('H'):
                display.show(Image.HAPPY) 
            elif command[0] == ord('S'):
                display.show(Image.SAD)  
            elif command[0] == ord('G'):
                display.show(Image.GIRAFFE)  
            elif command[0] == ord('P'):
                display.show(Image.PACMAN) 
```

#### En p5
``` js
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 350);
    connectBtn.mousePressed(connectBtnClick);

    // Crear botones para cada imagen
    createButton('Happy').position(50, 50).mousePressed(() => sendCommand('H'));
    createButton('Sad').position(50, 100).mousePressed(() => sendCommand('S'));
    createButton('Giraffe').position(50, 150).mousePressed(() => sendCommand('G'));
    createButton('Pacman').position(50, 200).mousePressed(() => sendCommand('P'));
}

function draw() {
    background(220);
    
    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    } else {
        connectBtn.html('Disconnect');
    }
}

function sendCommand(command) {
    if (port.opened()) {
        port.write(command); 
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close(); // Desconecta
    }
}
```
