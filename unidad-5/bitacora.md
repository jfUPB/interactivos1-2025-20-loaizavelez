
# Evidencias de la unidad 5

### Actividad 

**Como se diferencia el envio de datos:**

```py
# Imports go at the top
from microbit import *

uart.init(115200)
display.set_pixel(0,0,9)

while True:
    if accelerometer.was_gesture('shake'):
        xValue = accelerometer.get_x()
        yValue = accelerometer.get_y()
        aState = button_a.is_pressed()
        bState = button_b.is_pressed()
        data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
        uart.write(data)
        sleep(100) # Envia datos a 10 Hz
```
Los siguientes datos muestran datos en ASCCI de las coordenadas en el eje coordenado (x,y) del aceleromtro, el booleano muestra si los botones (a,b) son presionados (True).

**Traducción a texto:** 

- -708,-864,False,False
- -936,-432,False,False

**Traducción a HEX:**
- 0a 2d 37 30 38 2c 2d 38 36 34 2c 46 61 6c 73 65 2c 46 61 6c 73 65 0a 2d 39 33 36 2c 2d 34 33 32 2c 46 61 6c 73 65 2c 46 61 6c 73 65 0a

Los siguientes datos muestran datos en formato binario de las coordenadas en el eje coordenado (x,y) del aceleromtro, el booleano muestra si los botones (a,b) son presionados (True).

**Traducción a texto:**D0l ��8��00��8$��4��@��@��<L��<(0���D��8���� ��,����@L�<,���8��8��@��<��8��8��4��0��4��4��8��4�

El programa no es capaz de interpretar los caracteres. 

**Traducción a HEX:** fe 58 00 9c 00 00 fe 54 00 9c 00 00 fe

**Caracteres de quiebre o "Enter":** Se puede observar un patrón en el comportamiento de los datos, en ASCCI


 



 

