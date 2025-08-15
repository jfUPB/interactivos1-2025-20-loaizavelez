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

### Bomba 2.0

```py
# Imports go at the top
from microbit import *
import utime

display.clear()

class BombTask:
    def __init__(self):
        self.PASSWORD = ['A','B','A']
        self.key = ['']*len(self.PASSWORD)
        self.keyindex = 0
        self.count = 20
        self.startTime = utime.ticks_ms()
        self.state = 'CONFIG'
        display.clear()
        display.show(self.count,wait=False)

    def update(self):
        if self.state == 'CONFIG':
            if button_a.was_pressed():
                self.count = min(self.count+1,60)
                display.show(self.count,wait=False)

            if button_b.was_pressed():
                self.count = max(10,self.count-1)
                display.show(self.count, wait=False)

            if accelerometer.was_gesture('shake'):
                self.startTime = utime.ticks_ms()
                self.state = 'ARMED'

        elif self.state == 'ARMED':
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > 1000:
                self.startTime = utime.ticks_ms()
                self.count = self.count - 1
                display.show(self.count,wait=False)
                if self.count == 0:
                    display.show(Image.SKULL)
                    self.state = 'EXPLODED'

            if button_a.was_pressed():
                self.key[self.keyindex] = 'A'
                self.keyindex = self.keyindex + 1

            if button_b.was_pressed():
                self.key[self.keyindex] = 'B'
                self.keyindex = self.keyindex + 1

            if self.keyindex == len(self.key):

                passIsOK = True
                for i in range(len(self.key)):
                    if self.key[i] != self.PASSWORD[i]:
                        passIsOK = False
                        break;
                if passIsOK == True:
                    self.count = 20
                    display.show(self.count,wait=False)
                    self.keyindex = 0
                    self.state = 'CONFIG'
                else:
                    self.keyindex = 0

        elif self.state == 'EXPLODED':
            if pin_logo.is_touched():
                self.count = 20
                display.show(self.count,wait=False)
                self.startTime = utime.ticks_ms()
                self.state = 'CONFIG'

bombTask = BombTask()

while True:
    bombTask.update()
```

### Bomba 3.0

``` py
# Imports go at the top
from microbit import *
import utime

display.clear()

class Event:
    def __init__(self):
        self.value = 0

    def set(self,_val):
        self.value = _val

    def clear(self):
        self.value = 0

    def read(self):
        return self.value

class SerialTask:
    def __init__(self):
        uart.init(baudrate=115200)

    def update(self):
        if uart.any():
            data = uart.read(1)
            if data:
                if data[0] == ord('A'):
                    event.set('A')
                elif data[0] == ord('B'):
                    event.set('B')
                elif data[0] == ord('S'):
                    event.set('S')
                elif data[0] == ord('T'):
                    event.set('T')


class ButtonTask:
    def __init__(self):
        pass

    def update(self):
        if button_a.was_pressed():
            event.set('A')
        elif button_b.was_pressed():
            event.set('B')
        elif accelerometer.was_gesture('shake'):
            event.set('S')
        elif pin_logo.is_touched():
            event.set('T')

class BombTask:
    def __init__(self):
        self.PASSWORD = ['A','B','A']
        self.key = ['']*len(self.PASSWORD)
        self.keyindex = 0
        self.count = 20
        self.startTime = utime.ticks_ms()
        self.state = 'CONFIG'
        display.clear()
        display.show(self.count,wait=False)

    def update(self):
        if self.state == 'CONFIG':
            if event.read() == 'A':
                event.clear()
                self.count = min(self.count+1,60)
                display.show(self.count,wait=False)

            if event.read() == 'B':
                event.clear()
                self.count = max(10,self.count-1)
                display.show(self.count, wait=False)

            if event.read() == 'S':
                event.clear()
                self.startTime = utime.ticks_ms()
                self.state = 'ARMED'

        elif self.state == 'ARMED':
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > 1000:
                self.startTime = utime.ticks_ms()
                self.count = self.count - 1
                display.show(self.count,wait=False)
                if self.count == 0:
                    display.show(Image.SKULL)
                    self.state = 'EXPLODED'

            if event.read() == 'A':
                event.clear()
                self.key[self.keyindex] = 'A'
                self.keyindex = self.keyindex + 1

            if event.read() == 'B':
                event.clear()
                self.key[self.keyindex] = 'B'
                self.keyindex = self.keyindex + 1

            if self.keyindex == len(self.key):

                passIsOK = True
                for i in range(len(self.key)):
                    if self.key[i] != self.PASSWORD[i]:
                        passIsOK = False
                        break;
                if passIsOK == True:
                    self.count = 20
                    display.show(self.count,wait=False)
                    self.keyindex = 0
                    self.state = 'CONFIG'
                else:
                    self.keyindex = 0

        elif self.state == 'EXPLODED':
            if event.read() == 'T':
                event.clear()
                self.count = 20
                display.show(self.count,wait=False)
                self.startTime = utime.ticks_ms()
                self.state = 'CONFIG'

bombTask = BombTask()
serialTask = SerialTask()
buttonTask = ButtonTask()
event = Event()

while True:
    serialTask.update()
    buttonTask.update()
    bombTask.update()
```

