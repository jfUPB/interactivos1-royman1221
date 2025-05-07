``` py
let port;
let connectBtn;
let squareColor = 'blue'; 

function setup() {
    createCanvas(400, 400);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.mousePressed(connectBtnClick);
}

function draw() {
    background(220);
    drawSquare(); 

    if (port.availableBytes() > 0) {
        let dataRx = port.read(1);
        
      
        if (dataRx == 'A') {
            squareColor = 'red'; // Cambiar a rojo
        } else if (dataRx == 'B') {
            squareColor = 'green'; // Cambiar a verde
        } else if (dataRx == 'C') {
            squareColor = 'yellow'; // Cambiar a amarillo
        }
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

function drawSquare() {
    fill(squareColor); 
    rect(width / 2 - 25, height / 2 - 25, 50, 50); 
}
``` 
