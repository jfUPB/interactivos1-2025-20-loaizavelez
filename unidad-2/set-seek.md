# Unidad 2

## 🔎 Fase: Set + Seek

## Actividad 1
**Describe detalladamente cómo funciona este ejemplo.**

R// Este programa esta diseñado para encender dos luces led, cada uno con un intervalo de ticks diferente y una ubicación diferente, los primeros dos dígitos son el espacio que ocupan dentro del microbit, el tercer dígito es el estado de inicio, el ultimo dígito es el tiempo que se muestra el la luz rojan, en el pixel 1 se muestra 1 segundo y en el segundo pixel medio segundo..
```py
pixel1 = Pixel(0,0,0,1000)
pixel2 = Pixel(4,1,0,500)

```
```py
class Pixel:
    def __init__(self,pixelX,pixelY,initState,interval):
        self.state = "Init"
        self.startTime = 0
        self.interval = interval
        self.pixelX = pixelX
        self.pixelY = pixelY
        self.pixelState = initState
```

Esta es la clase Pixel, aquí se crea el constructor, donde se determinan los parametros de ubicación, inicialización, y el tiempo que se muestra. Se define así mismo los parametros que usa el constructor,su ubicación horixontal (x) y su ubicación vertical (y).

```py
def update(self):

        if self.state == "Init":
            self.startTime = utime.ticks_ms()
            self.state = "WaitTimeout"
            display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

        elif self.state == "WaitTimeout":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                if self.pixelState == 9:
                    self.pixelState = 0
                else:
                    self.pixelState = 9
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState)
```



En esta parte el led actualiza su estado, lo que le permite alternar entre encendido y apagado, en esta parte del codigo se analiza si el led cambio de estado con suficiente tiempo, si se elimina esta verificación, el led se vuelve errático, cambiando de estado descontroladamente. El resto del conidiconal, el 9 es si su estado es encendido, y 0 si esta apagado. 


https://github.com/user-attachments/assets/4e4ba3ff-7f06-4984-a482-a1ea8e78d987






**¿Cuáles son los estados en el programa?**
R// sus estados son, el encendido que esta representado como 9 y apagado, representado como 0. Creeria que se puede incluir el breve tiempo de espera para apagarse.



https://github.com/user-attachments/assets/7b35993c-46ee-4dd9-b2cd-b1ee2e8501d7



**¿Cuáles son los eventos/inputs en el programa?**

R// Se pueden considerar inputs el ingresar la ubicación del led, su tiempo de espera y si esta encendido o apagado usando el constructor y modificando su estado.
```py
 def __init__(self,pixelX,pixelY,initState,interval):
```

Los eventos son el "WaitTimeOut" es el tiempo de espera del led, también el estado de "init" que es lo que permite arrancar, como si fuera un vehiculo, el"PixelState" es el que define si esta encendido o apagado.

**¿Cuáles son las acciones en el programa?**
R// las acciones son, el "StartTime" usado para comparar el tiempo desde que se encendio el led, el "SelfState" que define el tiempo de espera.

## Actividad 2

```py
from microbit import *
import utime

class Pixel:
    def __init__(self,pixelX,pixelY,initState,interval):
        self.state = "Init"
        self.startTime = 0
        self.interval = interval
        self.pixelX = pixelX
        self.pixelY = pixelY
        self.pixelState = initState

    def update(self):

        if self.state == "Init":
            self.startTime = utime.ticks_ms()
            self.state = "WaitTimeout"
            display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

        elif self.state == "WaitTimeout":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                if self.pixelState == 9:
                    self.pixelState = 0
                else:
                    self.pixelState = 9
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

pixel1 = Pixel(2,0,0,3000)
pixel2 = Pixel(2,1,0,3000) 
pixel3 = Pixel(2,2,0,1200)
pixel4 = Pixel(2,3,0,1200) 
pixel5 = Pixel(2,4,0,2000) 

while True:
    pixel1.update()
    pixel2.update()
    pixel3.update()

    
    pixel4.update()
    pixel5.update()
   
```
Aqui se busco crear un semaforo usando la misma estructura del codigo anterior, por lo tanto las acciones y eventos son similares, lo que se busco hacer distinto fue usar el intervalo en en el que estan apagados para que uno al encenderse el otro led ya estuviera apagado.
