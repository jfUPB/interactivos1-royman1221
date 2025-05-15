Comparativa: Protocolo ASCII vs Protocolo Binario

| Aspecto         | Protocolo ASCII (Unidad anterior)                | Protocolo Binario (Unidad actual)                   |
| --------------- | ------------------------------------------------ | --------------------------------------------------- |
| Eficiencia      | Menos eficiente (ej: “500,524,1,0\n” = 11 bytes) | Más eficiente (6 bytes + 2 de framing = 8 bytes)    |
| Velocidad       | Más lento (parsing de strings)                   | Más rápido (lectura directa de bytes)               |
| Facilidad       | Más fácil de depurar (legible)                   | Más complejo (requiere conversiones y verificación) |
| Uso de recursos | Más uso de CPU (conversión texto→número)         | Menos uso de CPU (procesamiento directo)            |


¿Por qué fue necesario introducir framing?

Para evitar desincronización en la lectura de paquetes. Sin framing, se observaban valores corruptos como microBitX: 3073.

¿Cómo funciona el framing?

Se utiliza un header (0xAA) que marca el inicio del paquete.

Se incluye un checksum que verifica la integridad.

El paquete tiene un tamaño fijo de 8 bytes.

¿Qué es un carácter de sincronización?

Es el byte 0xAA, que actúa como marca de inicio de un paquete válido.

¿Qué es el checksum?

Es una suma de verificación:

checksum = sum(data) % 256
Se usa para detectar si el paquete fue corrompido durante la transmisión.

¿Para qué sirve la función concat?

Permite acumular los bytes recibidos:

serialBuffer = serialBuffer.concat(newData)
Es esencial porque los datos pueden llegar fragmentados.

¿Por qué se usa el bucle while (serialBuffer.length >= 8)?

Porque el tamaño del paquete completo es de 8 bytes (1 header + 6 datos + 1 checksum). Si hay menos, el paquete está incompleto.

¿Qué significa 0xAA?

Es el número 170 en hexadecimal. Se usa como header por su baja probabilidad de ocurrir naturalmente en los datos.

Funciones shift y continue:

shift(): Elimina el primer byte del buffer.

continue: Salta a la siguiente iteración del bucle.
Uso: Descarta bytes basura hasta encontrar el header 0xAA.

Instrucción break:

Se usa para salir del bucle si no hay suficientes datos para formar un paquete:
if (serialBuffer.length < 8) break;

Diferencia entre slice y splice:

| Función | Acción                                 | Uso en código                        |
| ------- | -------------------------------------- | ------------------------------------ |
| slice   | Copia parte del array (no modifica)    | `slice(0,8)` para copiar el paquete  |
| splice  | Elimina elementos del array (modifica) | `splice(0,8)` para limpiar el buffer |


¿Qué hace reduce?

dataBytes.reduce((acc, val) => acc + val, 0)
Suma todos los bytes del paquete para calcular el checksum.

¿Por qué comparar el checksum?

if (computedChecksum !== receivedChecksum)
Para verificar la integridad del paquete. Si hay discrepancia, se descarta con continue.

¿Para qué se usa DataView?

let view = new DataView(buffer);
Permite leer los datos crudos como tipos específicos:

getInt16(0) → entero de 2 bytes

getUint8(4) → byte como booleano
Sin DataView, los bytes no tienen un tipo definido.












































