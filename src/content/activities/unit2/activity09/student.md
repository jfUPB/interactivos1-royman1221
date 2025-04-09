```py
from microbit import *
import utime

class Sem:
    def __init__(self, V1, initState, interval):
        self.state = "Init"
        self.startTime = 0
        self.interval = interval
        self.pixel1 = (V1[0], V1[1] + 2)  # Ahora el rojo está arriba
        self.pixel2 = (V1[0], V1[1] + 1)  # Amarillo en el medio
        self.pixel3 = (V1[0], V1[1])      # Verde abajo
        self.pixelState = initState

    def update(self):
        if self.state == "Init":
            self.startTime = utime.ticks_ms()
            self.state = "rojo"
            display.set_pixel(self.pixel1[0], self.pixel1[1], self.pixelState)

        elif self.state == "rojo":
            if self.pixelState == 9:
                if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval[0]:
                    self.startTime = utime.ticks_ms()
                    self.pixelState = 0
                    self.state = "verde"
            else:
                self.pixelState = 9
            display.set_pixel(self.pixel1[0], self.pixel1[1], self.pixelState)

        elif self.state == "amarillo":
            if self.pixelState == 9:
                if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval[1]:
                    self.startTime = utime.ticks_ms()
                    self.pixelState = 0
                    self.state = "rojo"
            else:
                self.pixelState = 9
            display.set_pixel(self.pixel2[0], self.pixel2[1], self.pixelState)

        elif self.state == "verde":
            if self.pixelState == 9:
                if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval[2]:
                    self.startTime = utime.ticks_ms()
                    self.pixelState = 0
                    self.state = "amarillo"
            else:
                self.pixelState = 9
            display.set_pixel(self.pixel3[0], self.pixel3[1], self.pixelState)

pixel1 = Sem((0, 0), 0, (3000, 700, 2000))

while True:
    pixel1.update()
    utime.sleep(0.1)  # Pequeña pausa para evitar bloqueos

```
