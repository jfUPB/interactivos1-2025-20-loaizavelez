# Unidad 1

## 🛠 Fase: Apply

### Actividad 05



### Actividad 06

link programa: [Ver programa en p5.js](https://editor.p5js.org/loaizavelez/sketches/m7afR7SXl)

## Codigo py
~~~py
from microbit import *

uart.init(baudrate=115200)
display.show(Image.ARROW_N)

while True:
    if button_a.was_pressed():
        uart.write('A')
    if button_b.was_pressed():
        uart.write('B')
    if accelerometer.was_gesture('shake'):
        uart.write('U')
        sleep(100)

~~~

## codigo p5js
~~~ js
let port;
let connectBtn;
let connectionInitialized = false;
let x = 200; 

function setup() {
  createCanvas(400, 400);
  background(220);
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(80, 300);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  background(220);

  // Inicializa el puerto una vez abierto
  if (port.opened() && !connectionInitialized) {
    port.clear();
    connectionInitialized = true;
  }

  
  if (port.availableBytes() > 0) {
    let dataRx = port.read(1);
    if (dataRx === "A") {
      x -= 20;
    } else if (dataRx === "B") {
      x += 20;
    }
  }

 
  fill("pink");
  circle(x, 200, 50);

 
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  } else {
    connectBtn.html("Disconnect");
  }
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}
~~~

## Explicación codigo pythoon.

El codigo pythoon permite al micro:bit en un emisor por medio del protocolo UART, permitiendo la comuniación del micro:bit con el computador para ejecutar el programa P5.JS, usando un cable USB. El baudrate son la cantidad de datos por segundo que el micro:bit envía al PC.

Para identificar que el codigo se exporto correctamente al micro:bit decidi que los leds del mismo mostraran una flecha. dentro de pythoon se asignaron los botones "a" y "b" del micro:bit, para que al ser preisonados escriban un par de letras en este caso, "A" y "B". Se busco agregar una función para que al ser sacudido se escribiera la letra "U" esto se hizo con el proposito de que el programa en p5.js tuviera la opción de, al ser sacudido, regresar a la posición original dentro del canvas al circulo, teniendo una espera de una decima de segundo despúes de cada sacudida.

## Explicación codigo p5.js

1. Primero se incializan las variables que permitan la comunicación del PC para el micro:bit en este caso let port, que permite la comunicación de la USB, ConnectBtn, permite abrir y cerrar la conexión con el micro:bit y el connectionInitialized.
   
2. Se crea el canvas con sus dimensiones, la saturación del fondo si es más claro o más obscuro. Se crea y se ubica el boton para inicar la conexión con el micro:bit y se asigna que input debe recibir para enlazarse.

3. En conjunto con pythoon lee el caracter "A" y el caracter "B" si se cada uno tiene ajustado un valor en x que se mueve en positivo o negativo, desplazando el circulo.

### Inputs:

1. con el uso del micro:bit se presionan los botones "a" y "b" y se sacude, dentro del porgrama de p5.js, el input sería darle click al boton de conectar al micro:bit.

### Outputs:

1. Con el codigo en pythoon el micro:bit muestra la imagen que se esta pidiendo, en este caso una flecha con dirección norte.
2. Dentro de p5:js 






