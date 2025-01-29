#### En microbit
``` js
from microbit import *
uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A')  
        sleep(500)  
    if button_b.is_pressed():
        uart.write('B')  
        sleep(500) 
    if accelerometer.was_gesture('shake'):
        uart.write('C') 
        sleep(500)
    if uart.any():
        data = uart.read(1)  
        if data:
            if data[0] == ord('h'):
                display.show(Image.HEART)  
                sleep(500)
                display.show(Image.HAPPY)
```
#### En p5

```js
let port;
let connectBtn;
let circleX;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    
    circleX = width / 2; 

function draw() {
    background(220);
    fill('blue'); 
    ellipse(circleX, height / 2, 50, 50); // Dibuja el círculo

    if (port.availableBytes() > 0) {
        let dataRx = port.read(1); 
        if (dataRx == 'A') {
            circleX -= 10; // Mueve el círculo a la izquierda
        } else if (dataRx == 'B') {
            circleX += 10; // Mueve el círculo a la derecha
        }
        
        // Limita el movimiento del círculo dentro del canvas
        circleX = constrain(circleX, 25, width - 25);
    }

   
    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    } else {
        connectBtn.html('Disconnect');
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
