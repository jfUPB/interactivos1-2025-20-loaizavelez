
# Evidencias de la unidad 8

### Actividad 1

- Documenta los referentes visuales que te inspiren.

  ![referencia U8 (3)](https://github.com/user-attachments/assets/75833f6e-51c6-40ac-a378-fd17d8524f1b)


  ![referencia U8 (2)](https://github.com/user-attachments/assets/52a27501-8646-42fc-b282-fa4781df117c)


  ![referencia U8](https://github.com/user-attachments/assets/9327e72f-fc51-423b-823e-2ec8f9fbc032)



- Define el concepto de las visuales que quieres crear.
  
  R// Lo que busco crear con esos referentes visuales, es dar un ambiente melancolico y derruido, la idea es usar [We Lost](https://youtu.be/VIs_82VxUHE?si=YKfsJY7-s6alnE_x) de Lorien Testard, los efectos estan basados en el significado de la canción, cuenta de como una familia esta en duelo por la muerte de un ser querida, los visuales se dividen en 2, el primero, los generados por el microbit y el segundo por el tocuh, se controlara el fondo y en centro un corazón, el fondo sera más oscuro y se hara más tetrico y más melancolico el ambiente.

- Explica cómo el móvil y el micro:bit controlarán las visuales.

  R// El touch se encargara del corazón, con el movimiento horizontal aumentara que tan cerca estan ambos corazones, degradandose entre más lejos este cada uno del otro, el microbit usara el acelerometro y los botones A y B, el acelerometro degradara el fondo y los botones A y B agregaran heridas al corazón, siendo "A" agregar heridas y "B" quitarlas.


- Haz un bocetos de todas las interfaces del sistema.

  R//

  <img width="1920" height="1080" alt="boceto U8" src="https://github.com/user-attachments/assets/61cefae7-7ef0-4efc-ad14-d8e2a77f0e1f" />



- Haz un diagrama que explique cómo se comunicarán los diferentes componentes del sistema.

  R//

  <img width="1016" height="587" alt="diagrama U8 drawio" src="https://github.com/user-attachments/assets/2a12b2e7-f852-489c-966d-8fb02d675093" />


### Apply

```js

let socket;
let song;
let fft;
let fireworks = [];
let ufos = [];
let serialBuffer = [];

let currentBgColor;
let targetBgColor;
let transitionProgress = 0;

let port;
let connectBtn;
let microBitConnected = false;

const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAIT_MICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};

let appState = STATES.WAIT_MICROBIT_CONNECTION;
let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;

function preload() {
  song = loadSound('Paintress.wav');
}

function setup() {
  let canvas = createCanvas(300, 400);
  socket = io();
  fft = new p5.FFT();
  fft.setInput(song);
  port = createSerial();

  connectBtn = createButton("Connect to micro:bit");
  setTimeout(() => {
    let x = canvas.position().x + (width / 2) - (connectBtn.size().width / 2);
    connectBtn.position(x, height - 30);
  }, 100);
  connectBtn.mousePressed(connectBtnClick);

  currentBgColor = getRandomFuturisticColor();
  targetBgColor = getRandomFuturisticColor();

  socket.on('connect', () => console.log('Connected to server'));
  socket.on('disconnect', () => console.log('Disconnected from server'));
  socket.on('connect_error', (error) => console.error('Socket.IO error:', error));

  socket.on('message', (data) => {
    if (data?.type === 'touch' && typeof data.x === 'number' && typeof data.y === 'number') {
      if (song && !song.isPlaying()) song.play();
      if (fireworks.length < 10) fireworks.push(new Firework(data.x, data.y));
      ufos.push(new UFO(data.x, random(50, height - 50), random(1, 2)));
    }
  });
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200)
      .then(() => console.log("Serial port opened"))
      .catch(err => console.error("Failed to open serial port:", err));
  } else {
    port.close();
    console.log("Serial port closed");
  }
}

function draw() {
  microBitConnected = port.opened();
  connectBtn.html(microBitConnected ? "Disconnect" : "Connect to micro:bit");

  switch (appState) {
    case STATES.WAIT_MICROBIT_CONNECTION: {
      if (microBitConnected) {
        print("Microbit ready to draw");
        strokeWeight(0.75);
        c = color(181, 157, 0);
        noCursor();
        prevmicroBitAState = false;
        prevmicroBitBState = false;
        appState = STATES.RUNNING;
      }
      break;
    }

    case STATES.RUNNING: {
      if (!microBitConnected) {
        print("Waiting microbit connection");
        cursor();
        appState = STATES.WAIT_MICROBIT_CONNECTION;
        break;
      }

      readSerialData();

      if (frameCount % 90 === 0) {
        targetBgColor = getRandomFuturisticColor();
        transitionProgress = 0;
      }

      transitionProgress = min(1, transitionProgress + 0.01);
      let bgColor = lerpColor(currentBgColor, targetBgColor, transitionProgress);
      currentBgColor = bgColor;
      background(bgColor);

      for (let u of ufos) {
        u.update();
        u.show();
      }
      ufos = ufos.filter(u => !u.dead);

      for (let i = fireworks.length - 1; i >= 0; i--) {
        fireworks[i].update();
        fireworks[i].show();
        if (fireworks[i].done()) fireworks.splice(i, 1);
      }

      break;
    }
  }
}

function readSerialData() {
  let available = port.availableBytes();
  if (available > 0) {
    let newData = port.readBytes(available);
    if (newData && newData.length > 0) {
      serialBuffer = serialBuffer.concat(newData);
    }
  }

  while (serialBuffer.length >= 8) {
    if (serialBuffer[0] !== 0xaa) {
      serialBuffer.shift();
      continue;
    }

    if (serialBuffer.length < 8) break;

    let packet = serialBuffer.slice(0, 8);
    serialBuffer.splice(0, 8);

    let dataBytes = packet.slice(1, 7);
    let receivedChecksum = packet[7];
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;

    if (computedChecksum !== receivedChecksum) {
      console.log("Checksum error in packet");
      continue;
    }

    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0) + width / 2;
    microBitY = view.getInt16(2) + height / 2;
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
    updateButtonStates(microBitAState, microBitBState);
  }
}

function updateButtonStates(newAState, newBState) {
  if (newAState && !prevmicroBitAState) {
    lineModuleSize = random(50, 160);
    clickPosX = microBitX;
    clickPosY = microBitY;
    print("A pressed");
  }
  if (!newBState && prevmicroBitBState) {
    c = color(random(255), random(255), random(255), random(80, 100));
    print("B released");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}

function mousePressed() {
  if (getAudioContext().state !== 'running') {
    getAudioContext().resume().then(() => {
      console.log("AudioContext activado");
    });
  }
}

function getRandomFuturisticColor() {
  let r = random([0, 50, 100, 200]);
  let g = random([0, 100, 255]);
  let b = random([100, 200, 255]);
  return color(r, g, b);
}

class UFO {
  constructor(x, y, speed) {
    this.x = x;
    this.y = y;
    this.speed = speed;
    this.size = random(20, 40);
    this.color = color(random(150, 255), random(150, 255), random(255));
    this.dead = false;
  }

  update() {
    this.x += this.speed;
    if (this.x > width + 50) this.dead = true;
  }

  show() {
    fill(this.color);
    noStroke();
    ellipse(this.x, this.y, this.size, this.size / 2);
    fill(255, 255, 255, 100);
    ellipse(this.x, this.y + this.size / 4, this.size / 2, this.size / 6);
  }
}

class Firework {
  constructor(x, y) {
    this.particles = [];
    for (let i = 0; i < 50; i++) {
      this.particles.push(new Particle(x, y));
    }
  }

  update() {
    for (let p of this.particles) p.update();
  }

  show() {
    for (let p of this.particles) p.show();
  }

  done() {
    return this.particles.every(p => p.lifespan <= 0);
  }
}

class Particle {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D().mult(random(1, 3));
    this.lifespan = 255;
    this.color = color(random(180, 255), random(100, 255), random(200, 255));
  }

  update() {
    this.pos.add(this.vel);
    this.vel.mult(0.95);
    this.lifespan -= 4;
  }

  show() {
    noStroke();
    fill(this.color.levels[0], this.color.levels[1], this.color.levels[2], this.lifespan);
    ellipse(this.pos.x, this.pos.y, 4);
  }
}

```


### Autoevaluación 

**Nota final:** 3

Se realizo la actividad 1 sin emabrgo el codigo del apply no funciona y no encontre forma de hacerlo funcionar por lo tanto la nota final es **3**







