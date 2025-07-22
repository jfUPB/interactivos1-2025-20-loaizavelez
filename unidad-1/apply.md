# Unidad 1

## 🛠 Fase: Apply

### Actividad 05



### Actividad 06

link programa: [Ver sketch en p5.js](https://editor.p5js.org/loaizavelez/sketches/m7afR7SXl)

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

  // Leer datos del micro:bit y ajustar x
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
