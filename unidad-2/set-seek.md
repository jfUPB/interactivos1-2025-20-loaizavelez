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

En esta parte el led actualiza su estado, lo que le permite alternar entre encendido y apagado, en esta parte del codigo se analiza si el led cambio de estado con suficiente tiempo, si se elimina esta verificación, el led se vuelve errático, cambiando de estado descontroladamente. []


**¿Cuáles son los estados en el programa?**
R//

**¿Cuáles son los eventos/inputs en el programa?**
R//

**¿Cuáles son las acciones en el programa?**
