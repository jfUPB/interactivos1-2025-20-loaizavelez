# Unidad 4


## 🤔 Fase: Reflect


[Enlace a la aplicación a modificar](https://editor.p5js.org/loaizavelez/sketches/_yj7rZ8-_)

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


var gif;
var canvasElement;
var recording = false;

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

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
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
        }
      }
    }
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

      //EVENTO: recepción de datos seriales del micro:bit

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


```



[Video demostratativo](https://youtu.be/BbZjzv5ij_E)

