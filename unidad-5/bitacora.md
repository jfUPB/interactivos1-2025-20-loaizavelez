
# Evidencias de la unidad 5


### Actividad 1

**Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?**

R// El programa de p5js se comunica por un puerto serial uart, a 115200 baudios, con un tiempo de espera de 100 milisegundos, este está conectado a un microbit por un puerto **COM**. Los datos enviados están en codigo ASCII, es decir, envia caracteres con valores númericos, pueden ser números o estados booleanos.

En este ejercicio, el micro:bit envia los datos por medio de los siguientes sensores:

- Acelerometro, captura la posición en el eje coordenado (x,y).
- Botón A, iniclaizado en False
- Botón B, inicializado en False


<a name="pre1"></a>
¿Cómo es la estructura del protocolo ASCII usado?

En el codigo de micropython, la estructura es la siguiente:

```py
data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
```

en texto se lee así:

12,88,True,False

80,8,False,True

384,80,False,True

448,-48,False,False

340,-108,True,False

----------------------------------------------------------
Y en Hex así:

38 32 38 2c 32 34 2c 46 61 6c 73 65 2c 46 61 6c 73 65 0a

38 31 36 2c 32 34 2c 46 61 6c 73 65 2c 46 61 6c 73 65 0a 

Cabe resaltar que el caracter **/n** no es en si un valor o un estado, es el break o el enter, se usa para separar los datos y que no se junten y den un resultado errado.




Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla y ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?.

```js
 if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
      if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length == 4) {
          microBitX = int(values[0]) + windowWidth / 2;
          microBitY = int(values[1]) + windowHeight / 2;
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";
          updateButtonStates(microBitAState, microBitBState);
        } else {
          print("No se están recibiendo 4 datos del micro:bit");
        }
      }
    }
  

```
- **let data = port.readUntil("\n");** Como se menciono anteriormente, el break es el que permite terminar de leer la línea y que no se mezclen los datos de otros valores.

- **microBitX = int(values[0]) + windowWidth / 2; ... microBitY = int(values[1]) + windowHeight / 2;** Estos dos se encargan de recopilar la inforamción del aceletrometro, convienrten el valor en un número enetero y lo ubican al centro de la pantalla.

-   **microBitAState = values[2].toLowerCase() === "true";...microBitBState = values[3].toLowerCase() === "true";...updateButtonStates(microBitAState, microBitBState);** Convierte los valores de "A" y "B" en un booleano y actualiza las transiciones de estados con el updateState.

Visualmente se vería así: **12,88,True,False**


### Hipotesis. 

- **¿Que pasaría si se quita el "/n" del micropython?**

R// Despues de verificar en el serialTerminal, el resultado es el esperado, directamente, el programa deja de leer correctamnete los valores, cortando palabras y combinandolas, haciendo que sea ininteligible.

- 72,528,False,False60,492,FalseFalse12,512,False,alse168

<img width="1178" height="122" alt="image" src="https://github.com/user-attachments/assets/1a97fd91-a7bd-41b7-996b-844b6069e45c" />

<img width="1171" height="114" alt="image" src="https://github.com/user-attachments/assets/883eb2f1-61f9-44a8-a333-ae92d03979cb" />

Vease que no hay caractér 0a en la imagen.

- **¿Qué pasaria si se ejecuta en el js sin el break en python?**

```py
data = "{},{},{},{}".format(xValue, yValue, aState,bState)
 ```

```js
let data = port.readUntil("\n");

```

Se puede ver que no detecta los botones ni ninguno de los gestos con el acelerometro. ¿Porqué?, la clave está en **let data = port.readUntil("\n");** al no llegar a un final, significa que el mensaje aún no termina, por lo tanto queda en un tiempo de espera mientras este se acumula, por lo tanto no se genera ningún dibujo. Esto aplica también si se elimina del el **js**, ejemplo, **let data = port.readUntil();** isgue buscando el delimitador y al o encontarlo vyelve a pasar lo mismo

<img width="1919" height="972" alt="image" src="https://github.com/user-attachments/assets/fe93696a-d490-4150-bfb6-3d8f0a24d71f" />




<img width="860" height="161" alt="image" src="https://github.com/user-attachments/assets/ef074983-87ce-4011-b84a-ac7118c0dfde" />



- **¿Qué es el error, TypeError: Supported types are: String, Integer number (0 to 255), Array of integer numbers (0 to 255), Uint8Array
    at undefined:507:9?**


1.) Números enteros entre 0 y 255

2.) Un arreglo de números entre 0 y 255

3.) Uint8Array at undefined:507:9, es un arreglo que guarda valores sin signos de 8 bits.

<img width="803" height="71" alt="image" src="https://github.com/user-attachments/assets/aa2dc339-dff1-4050-a26e-befd6417bbb6" />


Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.

<img width="796" height="733" alt="image" src="https://github.com/user-attachments/assets/57a3f77c-09d8-4e44-851b-7bfdd772b986" />








### Actividad 2

**¿Qué diferencias ves entre los datos en ASCII y en binario?**

R//

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

<img width="1291" height="100" alt="image" src="https://github.com/user-attachments/assets/ccf40c4a-c686-48bb-ab11-671195553ee6" />


<img width="1009" height="171" alt="image" src="https://github.com/user-attachments/assets/9e794664-a994-4700-8584-46a5df4bd78d" />




**Traducción a texto:**�������|p��`��x84�x��4,����P�������4

El programa no es capaz de interpretar los caracteres, el serialTerminal al intentar convertirlo a texto, usa caracteres que no logra interpretar, el binario es distinto del ASCII, por eso saca los simbolos ininteliigibles. 

**Traducción a HEX:** 04 0c ff ac 00 00 02 d0 ff a8 00 00 02 f8 fc 7c 00 00 00 70 ff 1c 00 00 ff 60 fc f0 00 00 04 78 02 38 00 00 02 34 fc 78 00 00 01 a8 fd 34 00 00 00 2c fe b4 00 00 03 94 ff 50 00 00 fd e8 ff e8 00 00 fc bc fd 34 00 00

**Caracteres de quiebre o "Enter":** No hay caracter de quiebre en binario, en su lugar se envia en paquetes.

**¿Cómo se traduce el texto a binario?**

La clave está en "'>2h2B'" este se encarga de organizar el paquete de datos "struct.pack" tomando los valores más significativos primero, pero, ¿Qué es un valor más significativo? se refiere a los valores que representan estados, un true o false, valores de medición, en este caso, las coordenadas en el eje coordenado (X,Y). El formato de empaquetado se denomina Big-endian. El resto de la etsructura comformada por 2h y 2B. 2h son los valores enteros con signo, y 2B son los valores enteros sin signo. El total de datos empaquetados es de 6 bytes.

Un paquete de datos binarios sin organizar se ve así, 04 0c ff ac 00 00 02 d0 ff a8 00 00, organizado se vería así, acff0c04 d0020000 a8ff0000. 

En el hipotetico caso de que el comparador sea mayor que "'<2h2B'" se vería así, 04 0c ff ac 00 00 02 d0 ff a8 00 00, fijese que es igual a como se envian los datos por el puerto de comunicaciones. 



**Usos comunes de Big Endian**

El orden de bytes de la red se utiliza habitualmente en protocolos de red, como el Protocolo de Control de Transmisión (TCP) y el Protocolo de Internet (IP). Esta estandarización del orden de la red garantiza que los datos transmitidos por Internet se interpreten correctamente, independientemente del orden de bytes de los sistemas host involucrados. Además, el orden de bytes de la red es frecuente en muchas arquitecturas RISC (Reduced Instruction Set Computing), como las que se utilizan en los mainframes IBM más antiguos y algunos sistemas basados ​​en UNIX. Este orden de bytes también se encuentra en aplicaciones de procesamiento de señales digitales (DSP), donde la alineación con formatos legibles por humanos es ventajosa para depurar y analizar las salidas de datos. Además, el orden de bytes de la red se utiliza a menudo en formatos de archivos multimedia, como ciertos estándares de imagen y audio, donde la interpretación coherente de los datos es crucial. Comprender los usos comunes del orden de bytes de la red es vital para los desarrolladores que trabajan en campos donde el intercambio de datos entre sistemas heterogéneos se produce con frecuencia.


**Aplicaciones de Little Endian**

El little endian se utiliza ampliamente en la arquitectura de la mayoría de los ordenadores personales y servidores, en particular los que funcionan con procesadores Intel y AMD. Esta adopción generalizada se debe en gran medida a la facilidad que proporciona en las operaciones aritméticas, ya que los procesadores pueden acceder directamente al byte menos significativo para los cálculos, lo que agiliza los procesos y reduce la sobrecarga computacional. El little endian también es frecuente en los formatos de archivo y protocolos que se originan a partir de estas arquitecturas, como los que se utilizan en los sistemas operativos Windows y numerosas estructuras de datos binarios. Además, el little endian se suele emplear en sistemas y dispositivos integrados que priorizan la velocidad y la eficiencia de procesamiento sobre los formatos legibles por humanos. En el ámbito del desarrollo de software, comprender el little endian es crucial cuando se trabaja con lenguajes de programación de bajo nivel, como escribir código ensamblador o desarrollar firmware, donde es necesaria la manipulación directa del orden de bytes. Estas aplicaciones demuestran la practicidad y la eficiencia del little endian en los entornos informáticos modernos.

[El debate entre Big Endian y Little Endian – Wray Castle](https://wraycastle.com/es/blogs/knowledge-base/big-endian-vs-little-endian)



En este caso se modifica el codigo para enviar datos en ASCII y en binario 

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
        uart.write("ASCII:\n")
        data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
        uart.write(data)

```

Asi se ven los datos combinados: 

```
���lASCII:
-544,-660,False,True
�DASCII:
2040,580,True,False
```


- **¿Qué pasaría si se retira el 2b y solo se deja el 2h y viceversa?**

R// 

- En caso de retirar el 2b se tomarán 4 bytes, en este caso, 04 a0 07 f8, el valor cambia completamente, en lugar de mostrar un eje coordenado, muestra un númeri entero 77361176.

- En caso de reitrar el 2h solo se enviarian 2 bytes y no se leerían los otros 4 bytes, además solo se toman los valores enteros sin signo, es decir, solo los positivos, envía estos datos, 64 78.



<img width="1205/2" height="247/2" alt="image" src="https://github.com/user-attachments/assets/a77cc807-1f84-4080-958b-652464a90109" />



**Qué es el struct.pack**

R// el struck.pack se encraga de caonvertir los valores enteros y booleanos en un paquete de 6 bytes binarios, enviados en el siguiente formato data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState)), se envian en big-endian, es decir que se envian primero los datos de mayor valor.


**¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?**

R// Las ventajas de usar binario en lugar de ASCII son:

- mayor facilidad de envio de datos, al estar empaquetados y ser más cortos se procesan más rapido.
- Lectura rapida por medio del microbit.
- Mayor compatibilidad.


Desventajas.

- Sin herramientas no puede ser legible.
- Probabilidad de que bytes no se envien.
- Su lectura es complejaen HEX.

**¿Qué ventajas y desventajas ves en usar un formato ASCII en lugar de binario?**

R//

Ventajas:

- Alta legibilidad.
- Alta comptabilidad con programás con lectura de texto.
- Se pueden detectar los errores más facilmente.


Desventajas:

- El envio de datos es muy lento.
- Requiere más uso de CPU para convertirlo a texto.
- El espacio que ocupan los bytes son mayores.





### Actividad 3


**Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.**

R// En la unidad anterior todo se enviaba en ASCII, para que los datos enviados fueran interpretados y traducidos a texto para entender que dice, se debía poner un break en este caso, "\n", este se encargaba de delimitar el final del paquete. De esta forma se evitaba que la lectura de datos se viera errada como se vio previamnete. Ahora el archivo binario está delimitado a 6 bytes. Lo siginifica que ya no se debe delimitar el tamaño del paquete, esto no significa que los datos enviados siempre sean los deseados, suele suceder que algunos datos quedan en medio y se envian. 



**¿Qué ves en la consola? ¿Por qué crees que se produce este error?**

```


microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false 
 
Microbit ready to draw 

microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false 
 

microBitX: 524 microBitY: 256 microBitAState: true microBitBState: false 

```


``` 

microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false 
 
Microbit ready to draw 

microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false 
 
Disconnected from serial port 
microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false 
```

Lo primero que note es que el error no se produce siempre, lo ejecute un total de 5 veces y solo en la primera ocasión fue cuando salio el error, por lo que puedo decir que el error ocurre en casos muy concretos, intenté reproducirlo pero no volvió aparecer. 

En este caso se modificó el micropython para dar unos valores en concreto.


```py

Value = 500
    yValue = 524
    aState = True
    bState = False

```

Solo en una ocasión se logro ver el error y es está parte, **microBitX: 524 microBitY: 256 microBitAState: true microBitBState: false**, los valores no coinciden. Una de las complicaciones de enviar paquetes binarios, es que en estos paquetes pueden ir valores errados que quedaron en el camino, es probable que uno de estos valores quedara atrapado y fue enviado por error. 

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


**¿Qué ves?**

Los datos enviados siempre son los mismos. 

```
microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false 
```


 ¿Qué cambios tienen los programas y ¿Qué puedes observar en la consola del editor de p5.js?


```

A pressed 
B released 

A pressed 
B released 

A pressed 
B released 
A pressed 
```

Con el cambio en el codigo del micrpython ahora se muestran los estados de los botones, si se presionan o si se sueltan, ya dibuja de manera normal, anteriormente solo dibujaba un ciruclo en una zona aleatoria de la pantalla.

**¿Qué es un checksum?**

R// El checksum es una sumatoria suma una cantidad de datos en un rango de 1 a 7 y si el resultado es igual a 256 permite enviar ese paquete de datos, en caso de que el checksum arroje un error se descarta el paquete y se da paso al siguiente, asi se verifica y se evitan los errores vistos anteriormente. 

```py
packet = b'\xAA' + data + bytes([checksum])

```

**Estrategios de framing**: hay varios metodos para el framing estrategias de stuffing, estrategias con campos de longitud, violación de código y 
de longitud fija. El articulo está en ingles y la traducción deja mucho que desear.


1. Fixed-size: The frame is of fixed size and there is no need to provide boundaries to the frame, the length of the frame itself acts as a delimiter.  

Drawback: It suffers from internal fragmentation if the data size is less than the frame size
Solution: Padding
2. Variable size: In this, there is a need to define the end of the frame as well as the beginning of the next frame to distinguish. This can be done in two ways: 

Length field - We can introduce a length field in the frame to indicate the length of the frame. Used in Ethernet(802.3). The problem with this is that sometimes the length field might get corrupted.
End Delimiter (ED) - We can introduce an ED(pattern) to indicate the end of the frame. Used in Token Ring. The problem with this is that ED can occur in the data. 

1. Character/Byte Stuffing: Used when frames consist of characters. If data contains ED then, a byte is stuffed into data to differentiate it from ED. 

[Tipos de framing](https://www.geeksforgeeks.org/computer-networks/framing-in-data-link-layer/)



**¿Qué es un header?**

R// Un header es una secuencia inicial del paquete que no contiene información vital, funciona más como un inicalizador que permite enviar los datos de comunicación serial. Inicializado en **0xAA**


**¿Qué es el dataview?**

R// El dataview es un formato de javascript que permite leer los paquetes binarios, permitiendo interpretar los datos binarios de los booleanos y de los números enteros como es nuetsro caso de estudio.

  





 

**Dudas:**

¿porque dibuja en ocasiones?
<img width="1902" height="1026" alt="image" src="https://github.com/user-attachments/assets/37af0026-e3c4-4850-8e6d-0624de6be5a7" />


<img width="836" height="185" alt="image" src="https://github.com/user-attachments/assets/6d970a62-a6dd-405e-bec0-b783599096f3" /> 

parece que hay posibilidad de que los datos empaquetados no lleguen correctamente . lo que hace que no dibuje en ocasiones




### Actividad 4

```js
// P_2_3_7_01
//
// Generative Gestaltung – Creative Coding im Web
// ISBN: 978-3-87439-902-9, First Edition, Hermann Schmidt, Mainz, 2018
// Benedikt Groß, Hartmut Bohnacker, Julia Laub, Claudius Lazzeroni
// with contributions by Joey Lee and Niels Poldervaart
// Copyright 2018
//
// http://www.generative-gestaltung.de
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

/**
 * Simple drawing tool where mouse input gets mirrored over multiple axes
 *
 * MOUSE
 * left click          : draw line
 *
 * KEYS
 * 1                   : toggle vertical mirror
 * 2                   : toggle horizontal mirror
 * 3                   : toggle diagonal mirror 1
 * 4                   : toggle diagonal mirror 2
 * 5-9                 : change color
 * 0                   : color white (eraser)
 * arrow up            : increase line weight
 * arrow down          : decrease line weight
 * arrow right         : increase number of tiles
 * arrow left          : decrease number of tiles
 * d                   : show/hide mirror axes
 * del, backspace      : clear screen
 * g                   : start/stop gif recording
 * s                   : save png
 *
 * CONTRIBUTED BY
 * [Niels Poldervaart](http://NielsPoldervaart.nl)
*/

let serialBuffer = [];
var gif;
var canvasElement;
var recording = false;
const lineModule = [];
var lineWidth = 3;
var lineColor;

var mv = true;
var mh = true;
var md1 = true;
var md2 = true;
var penCount = 1;

var showAxes = true;

var img;


let port;
let connectBtn;
let connectionInitialized = false;
let microBitConnected = false;

//guardar frame anterior
let prevMicroBitX = 0;
let prevMicroBitY = 0;


const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAITMICROBIT_CONNECTION",
  RUNNING: "RUNNING",}

let appState = STATES.WAIT_MICROBIT_CONNECTION;
let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;




function setup() {
  // Please work with a square canvas
  canvasElement = createCanvas(800, 800);
  noCursor();
  noFill();
  lineColor = color(0);

  // Create an offscreen graphics object to draw into
  img = createGraphics(width, height);
  img.pixelDensity(1);
  
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(0, 0);
  connectBtn.mousePressed(connectBtnClick);

 
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}

function updateButtonStates(newAState, newBState) {
 
  if (newAState === true && prevmicroBitAState === false) {
    // create a new random color and line length
    lineModuleSize = random(50, 160);
    
    clickPosX = microBitX;
    clickPosY = microBitY;
    print("A pressed");
  }


  if (newBState === true && prevmicroBitBState === false) {
    
    lineColor =  color(random(255), random(255), random(255), random(80, 100));
    print("B released");
   
     
  }
  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
} 

 
function readSerialData() {
  // Acumula los bytes recibidos en el buffer
  let available = port.availableBytes();
  if (available > 0) {
    let newData = port.readBytes(available);
    serialBuffer = serialBuffer.concat(newData);
  }

  // Procesa el buffer mientras tenga al menos 8 bytes (tamaño de un paquete)
  while (serialBuffer.length >= 8) {
    // Busca el header (0xAA)
    if (serialBuffer[0] !== 0xaa) {
      serialBuffer.shift(); // Descarta bytes hasta encontrar el header
      continue;
    }

    // Si hay menos de 8 bytes, espera a que llegue el paquete completo
    if (serialBuffer.length < 8) break;

    // Extrae los 8 bytes del paquete
    let packet = serialBuffer.slice(0, 8);
    serialBuffer.splice(0, 8); // Elimina el paquete procesado del buffer

    // Separa datos y checksum
    let dataBytes = packet.slice(1, 7);
    let receivedChecksum = packet[7];
    // Calcula el checksum sumando los datos y aplicando módulo 256
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;

    if (computedChecksum !== receivedChecksum) {
      console.log("Checksum error in packet");
      continue; // Descarta el paquete si el checksum no es válido
    }

    // Si el paquete es válido, extrae los valores
    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0);
    microBitY = view.getInt16(2);
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
    updateButtonStates(microBitAState, microBitBState);

    console.log(
      `microBitX: ${microBitX} microBitY: ${microBitY} microBitAState: ${microBitAState} microBitBState: ${microBitBState}`
    );
  }
}




function draw() {
  //******************************************
  
   background(255);
  image(img, 0, 0);

  img.strokeWeight(lineWidth);
  img.stroke(lineColor);

  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");

  

   
          
          //Guardar posición anterior
          prevMicroBitX = microBitX;
          prevMicroBitY = microBitY;
      
    }
  
   switch (appState) {
    case STATES.WAIT_MICROBIT_CONNECTION:
      // No puede comenzar a dibujar hasta que no se conecte el microbit
      // evento 1:
      if (microBitConnected === true) {
        // Preparo todo para el estado en el próximo frame
        print("Microbit ready to draw");
         // Please work with a square canvas
  canvasElement = createCanvas(800, 800);
  noCursor();
  noFill();
  lineColor = color(0);

  // Create an offscreen graphics object to draw into
  img = createGraphics(width, height);
  img.pixelDensity(1);

  setupGIF();
        appState = STATES.RUNNING;
      }

      break;
      
       case STATES.RUNNING:
       
       
       
      // EVENTO: estado de conexión del microbit
      if (microBitConnected === false) {
        print("Waiting microbit connection");
        cursor();
        appState = STATES.WAIT_MICROBIT_CONNECTION;
      }
       
       readSerialData()
      
     

      if (microBitAState === true) {
     
    var w = width / penCount;
    var h = height / penCount;
    var x = microBitX % w;
    var y = microBitY % h;
    var px = x - (microBitX - prevMicroBitX );
    var py = y - (microBitY - prevMicroBitY );

    for (var i = 0; i < penCount; i++) {
      for (var j = 0; j < penCount; j++) {
        var ox = i * w;
        var oy = j * h;

        // Normal position
        img.line(x + ox, y + oy, px + ox, py + oy);
        // Horizontal mirror or all three other mirrors
        if (mh || md2 && md1 && mv) img.line(w - x + ox, y + oy, w - px + ox, py + oy);
        // Vertical mirror
        if (mv || md2 && md1 && mh) img.line(x + ox, h - y + oy, px + ox, h - py + oy);
        // Horizontal and vertical mirror
        if (mv && mh || md2 && md1) img.line(w - x + ox, h - y + oy, w - px + ox, h - py + oy);

        // When mirroring diagonally, flip X and Y inputs.
        if (md1 || md2 && mv && mh) img.line(y + ox, x + oy, py + ox, px + oy);
        if (md1 && mh || md2 && mv) img.line(y + ox, w - x + oy, py + ox, w - px + oy);
        if (md1 && mv || md2 && mh) img.line(h - y + ox, x + oy, h - py + ox, px + oy);
        if (md1 && mv && mh || md2) img.line(h - y + ox, w - x + oy, h - py + ox, w - px + oy);
      }
    }
        
         // draw pen
    fill(lineColor);
    noStroke();
    ellipse(microBitX, microBitY, lineWidth + 2, lineWidth + 2);
    stroke(0, 50);
    noFill();
    ellipse(microBitX, microBitY, lineWidth + 1, lineWidth + 1);
    
        if (showAxes) {
    var w = width / penCount;
    var h = height / penCount;

    // draw mirror axes and tiles
    for (var i = 0; i < penCount; i++) {
      for (var j = 0; j < penCount; j++) {
        var x = i * w;
        var y = j * h;

        stroke(0, 50);
        strokeWeight(1);
        if (mh) line(x + w / 2, y, x + w / 2, y + h);
        if (mv) line(x, y + h / 2, x + w, y + h / 2);
        if (md1) line(x, y, x + w, y + h);
        if (md2) line(x + w, y, x, y + h);

        stroke(15, 233, 118, 50);
        strokeWeight(1);
        rect(i * w, j * h, w - 1, h - 1);
      }
    }
        
        }
      }
 
}


  //*******************************************


     

function keyPressed() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
  if (keyCode == DELETE || keyCode == BACKSPACE) img.clear();

  if (keyCode == RIGHT_ARROW) penCount++;
  if (keyCode == LEFT_ARROW) penCount = max(1, penCount - 1);

  if (keyCode == UP_ARROW) lineWidth++;
  if (keyCode == DOWN_ARROW) lineWidth = max(1, lineWidth - 1);

  if (key == '1') mv = !mv;
  if (key == '2') mh = !mh;
  if (key == '3') md1 = !md1;
  if (key == '4') md2 = !md2;

  if (key == '5') lineColor = color(0);
  if (key == '6') lineColor = color(15, 233, 118);
  if (key == '7') lineColor = color(245, 95, 80);
  if (key == '8') lineColor = color(65, 105, 185);
  if (key == '9') lineColor = color(255, 231, 108);
  if (key == '0') lineColor = color(255);

  if (key == 'd' || key == 'D') showAxes = !showAxes;
  if (key == 'g' || key == 'G') {
    recording = !recording;
    if (!recording) {
      gif.render();
    }
  }
}

function setupGIF() {
  background(255);
  gif = new GIF({
    workers: 16,
    quality: 10000,
    debug: true,
    workerScript: '../../libraries/gif.js/gif.worker.js'
  });
  gif.on('finished', function(blob) {
    saveAs(blob, gd.timestamp() + '.gif');
    setupGIF();
  });
}
 

}

```


**Qué se agrego?**

- Primero se reemplazo la lectura ASCII:


```js

 if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length == 4) {
          
          //Guardar posición anterior
          prevMicroBitX = microBitX;
          prevMicroBitY = microBitY;
      //-----------------------------

          microBitX = int(values[0]) + windowWidth / 2;
          microBitY = int(values[1]) + windowHeight / 2;
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";
          updateButtonStates(microBitAState, microBitBState);
        } else {
          print("No se están recibiendo 4 datos del micro:bit");

```

y fue reemplazado por la lectura de datos binarios agregandose el checksum:



```js

   let newData = port.readBytes(available);
    serialBuffer = serialBuffer.concat(newData);
  }

  // Procesa el buffer mientras tenga al menos 8 bytes (tamaño de un paquete)
  while (serialBuffer.length >= 8) {
    // Busca el header (0xAA)
    if (serialBuffer[0] !== 0xaa) {
      serialBuffer.shift(); // Descarta bytes hasta encontrar el header
      continue;
    }

    // Si hay menos de 8 bytes, espera a que llegue el paquete completo
    if (serialBuffer.length < 8) break;

    // Extrae los 8 bytes del paquete
    let packet = serialBuffer.slice(0, 8);
    serialBuffer.splice(0, 8); // Elimina el paquete procesado del buffer

    // Separa datos y checksum
    let dataBytes = packet.slice(1, 7);
    let receivedChecksum = packet[7];
    // Calcula el checksum sumando los datos y aplicando módulo 256
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;

    if (computedChecksum !== receivedChecksum) {
      console.log("Checksum error in packet");
      continue; // Descarta el paquete si el checksum no es válido
    }

    // Si el paquete es válido, extrae los valores
    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0);
    microBitY = view.getInt16(2);
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
    updateButtonStates(microBitAState, microBitBState);

    console.log(
      `microBitX: ${microBitX} microBitY: ${microBitY} microBitAState: ${microBitAState} microBitBState: ${microBitBState}`

```

Las partes del codigo fueron tomadas del ejemplo del profe, cabe aclarar que durante el desarrollo solo hubo un error con un corchete "}" de cierre causando que el programa no compilara, despúes de corregido el error el programa continuo funcionando como debería


- **¿Qué hace la linea   console.log(`microBitX: ${microBitX} microBitY: ${microBitY} microBitAState: ${microBitAState} microBitBState: ${microBitBState}`?**

  R// es el encargado de mostrar los envios de paquetes binarios y su correcta interpretación.

  ```
   microBitX: 548 microBitY: -148 microBitAState: true microBitBState: false 
   microBitX: 524 microBitY: -196 microBitAState: false microBitBState: false 
   B released 
   microBitX: 460 microBitY: -100 microBitAState: false microBitBState: true 
   microBitX: 476 microBitY: -44 microBitAState: false microBitBState: true 

  ```

- **¿Qué tipo de framing estamos usando?**

  R// En esta actividad estamos usando Lenght-Field para indicar el tamaño del paquete, mencionado anteriormente es probable que algunos datos lleguen corruptos.

  
Anexos:

<img width="1919" height="946" alt="image" src="https://github.com/user-attachments/assets/1515548f-d494-4a82-962c-d4bf36bced3f" />

En la actividad se usaron todos lo estados agregados, es decir, el estado del botón "a" que permite dibujar y el estado de levantar el botón "b" para cambiar el color del trazo, ademas de usar el aceleroemtro para que cada trazo se viera en el canvas.




### Rúbrica


Despúes de la investigación y los datos aportados de cada unidad se pasra a justificar la nota de la rubrica de cada actividad en un acumulado final.



- Criterio 1 (logrado), profunidad de la indagación: en esta unidad se investigo y se forzaron erroes para indgar en el funcionamiento del envio de datos binarios y su forma de empaquetarse, con los errores se logro entender directamente el funcionamiento completo o parcial del codigo de python o del p5js. También se compararon los valores enviados por ASCII y binario y se vio como reaccionaban los programas al quitar y modificar caracteristicas de cada uno, del ASCII quitando el break y el binario modificando el envio de datos. (esto lo pone el profesor para ilustración del enlazado de evidencias) Por ejemplo en la [pregunta 1](#pre1) demuestro una profundidad... porque según la rúbrica... y mi pregunta demuestra.... Nota final: 4.4


- Criterio 2 (Excelente), calidad de la experimentación: cada experimiento tenia un proposito y era entender el funcionamiento del codigo ASCII y binario, el como se reciben y se envian los datos y ver como los interpreta el serial terminal o el msimo javasricpt, forzando errores para ver como reaccionaban. Nota final: 5.0

- Criterio 3 (logrado), analisis y relflexión: despúes de la investigación puedo decir que logre identificar las debilidades del framing y el como el chekcsum y el header garantizan el envio correcto de los datos, esto se profundizo más en la **actividad 3**. Nota final: 4.4

 - Criterio 4 (logrado), Apropiación y articulación de conceptos: En la bitacoro está explicado el funcionamiento del header, cheksum y el dataview y el como permite identificar y garantizar el envio de datos ademas de explicar su funcionamiento se id ago más a profundidad en la actividad 2 y 3. Nota Final: 4.4


**Nota final: 4.5**







