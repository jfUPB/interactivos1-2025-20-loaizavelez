
# Evidencias de la unidad 5

### Actividad 2

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




### Actividad 3


¿Qué cambios tienen los programas?

R//

**Codigo original del microbit para datos binarios**
```py
# Imports go at the top
from microbit import *
import struct
uart.init(115200)
display.set_pixel(0,0,9)

while True:
    if accelerometer.was_gesture('shake'):
        xValue = accelerometer.get_x()
        yValue = accelerometer.get_y()
        aState = button_a.is_pressed()
        bState = button_b.is_pressed()
        data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
        uart.write(data)
```


```py
from microbit import *
import struct

uart.init(115200)
display.set_pixel(0, 0, 9)

while True:
    xValue = accelerometer.get_x()
    yValue = accelerometer.get_y()
    aState = button_a.is_pressed()
    bState = button_b.is_pressed()
    # Empaqueta los datos: 2 enteros (16 bits) y 2 bytes para estados
    data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
    # Calcula un checksum simple: suma de los bytes de data módulo 256
    checksum = sum(data) % 256
    # Crea el paquete con header, datos y checksum
    packet = b'\xAA' + data + bytes([checksum])
    uart.write(packet)
    sleep(100)  # Envía datos a 10 Hz
```





 

**Dudas:**

¿porque dibuja en ocasiones?
<img width="1902" height="1026" alt="image" src="https://github.com/user-attachments/assets/37af0026-e3c4-4850-8e6d-0624de6be5a7" />


<img width="836" height="185" alt="image" src="https://github.com/user-attachments/assets/6d970a62-a6dd-405e-bec0-b783599096f3" /> 

parece que hay posibilidad de que los datos empaquetados no lleguen correctamente . lo que hace que no dibuje en ocasiones

 


