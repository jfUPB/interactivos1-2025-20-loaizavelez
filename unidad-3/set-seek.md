# Unidad 3

## 🔎 Fase: Set + Seek

### semaforo nuevo 

```py
from microbit import *
import utime

class Semaforo:
    def __init__(self,tr,ta,tv,col):
        self.tr = tr
        self.ta = ta
        self.tv = tv
        self.col = col
        display.set_pixel(self.col,0,9)
        self.startTime = utime.ticks_ms()
        self.state = "WAITINRED"
        

    def update(self):
        if self.state == "WAITINRED":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) >= self.tr:

                display.set_pixel(self.col,0,0) ##Apaga el rojo
                display.set_pixel(self.col,1,9) ## enciende el amarillo
                self.startTime = utime.ticks_ms()
                self.state = "WAITINYELLOW"
        
        elif self.state == "WAITINYELLOW":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) >= self.ta:

                
                display.set_pixel(self.col,1,0) ##Apaga el amarillo
                display.set_pixel(self.col,2,9) ## enciende el verde
                self.startTime = utime.ticks_ms()
                self.state = "WAITINGREEN"
            
        elif self.state == "WAITINGREEN":
            
             if utime.ticks_diff(utime.ticks_ms(),self.startTime) >= self.tv:

                
                display.set_pixel(self.col,2,0) ##Apaga el verde
                display.set_pixel(self.col,0,9) ## enciende el rojo
                self.startTime = utime.ticks_ms()
                self.state = "WAITINRED"

        

semaforo1 = Semaforo(5000,2000,3000,0)
semaforo2 = Semaforo(3000,1000,2000,2)
semaforo3 = Semaforo(4000,3000,2000,4)

while True:
    semaforo1.update()
    semaforo2.update()
    semaforo3.update()

```
