Los enlaces estan en la unidad anterior 

https://p5js.org/examples/repetition-kaleidoscope/


Código modificado

``` c#

let serialBuffer = [];

function readSerialData() {

  let newData = port.readBytes(port.availableBytes());
  serialBuffer = serialBuffer.concat(newData);


  while (serialBuffer.length >= 8) {
    // 2.1 Buscar header (0xAA)
    if (serialBuffer[0] !== 0xAA) {
      serialBuffer.shift();
      continue;
    }


    let packet = serialBuffer.slice(0, 8);
    let dataBytes = packet.slice(1, 7);
    let checksum = packet[7];


    if (dataBytes.reduce((s, v) => s + v, 0) % 256 !== checksum) {
      console.log("Error de checksum");
      serialBuffer.splice(0, 8);
      continue;
    }


    let view = new DataView(new Uint8Array(dataBytes).buffer);
    microBitX = view.getInt16(0) + width/2;
    microBitY = view.getInt16(2) + height/2;
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;

    serialBuffer.splice(0, 8);
  }
}
```
