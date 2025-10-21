
# Evidencias de la unidad 7

### Actividad 1

<a name="Actividad_1"></a>


¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?

  R// El link obtenido es, https://ggdqldl3-3000.use2.devtunnels.ms/ la url permite acceder a un servidor en la nube permitiendo la conexión de los dispositivos, celular y pc sin restricciones, permitiendo si se usa el localhost: 3000, no se conectaría si la red esta protegida.



<img width="624" height="60" alt="image" src="https://github.com/user-attachments/assets/33767d80-c5cf-445a-a416-7c528fb90989" />


Describe brevemente qué hace npm install y npm start.

  R// 

  ```bash
  Admin@DESKTOP-HIHTLMH MINGW64 ~/sfiSocketioDesktopMobile (main)
$ npm install

up to date, audited 89 packages in 4s

14 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities

  
  ```
Al igual que el proceso anterior, el npm install descarga las bibliotecas y las actualiza, también muestra si alguna dependencia busca danoaciones. 


```bash
$ npm start 

> sfinteractivesocketiodesktopmobile@1.0.0 start
> node server.js

Server is listening on http://localhost:3000

```

El npm start prende el servidor local den el puerto 3000 y se pone a escuchar.


¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?

  R// Lo que se observa en la terminal al **Iniciarlo**:

  ```bash
  Server is listening on http://localhost:3000
  New client connected
  New client connected
  ```

  Al actualziar la posición tocando la pantalla: 

  ```bash
  Received message => { type: 'touch', x: 177, y: 224 }
  Received message => { type: 'touch', x: 187, y: 240 }
  Received message => { type: 'touch', x: 193, y: 254 }
  Received message => { type: 'touch', x: 195, y: 267 }
  Received message => { type: 'touch', x: 195, y: 274 }

  ```
  Te muestra la posición del touch en la posición (x,y).


Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)

  R// 

  [Comportamiento observado](https://youtube.com/shorts/d1YQROjEisU?feature=share)

  Es funcional, hay un breve retraso al momento de desplazar el circulo por el canvas.


### Actividad 2

<a name="Actividad_2"></a>

Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?

  R// Al correr en localhost y estar protegida la red no permite que un dispositivo externo se conecte por temas de seguridad ya que este se convierte en el mismo servidor y siempre buscara el computador. Por eso se abre un servidor en la nube, en devtunnels. Enviando los datos atraves de este servidor, sin necesidad de tener una red pública, dentro de universidades o lugares donde las redes deben ser privadas, correrlo en un localhost no servirá, el dispositivo no se conectara al no tener los permisos.

Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.

  R// La función touchmoved() funciona como un evento que al presionar la pantalla del dispositivo, actualiza esa posición más reciente, guardando la pisición en (x,y) de hecho la clase del mouseDragged() se activara cuando la función touch() no este declarada, usando las posiciones del mouse con las coordenadas (x,y) El treshold es usado como un umbral. Se define un limite minimo y máximo, se usa para determinar cuando activar la función y que datos basura como temblores no se detecten. Dentro de la documentación de p5.js un ejemplo es:

  ```js
  if (borderWidth > 20) {
  borderWidth = 0.5;
  }
  ```
  y dentro de la aplicación del caso de estudio:

  ```js
  if (dx > threshold || dy > threshold || lastTouchX === null) 

  ```

Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?

  R// Con devtunnels puedes conectar cualquier dispositivo que tenga la URL correspondiente, facilitando la conexión sin depender de configurar la privacidad de la red, no se deben configuran los puertos, ni las conexiones a internet. Una de las desventajas es que debe ser pública, cuando entras a la URL te sale un aviso donde dice que solo debes poner el servidor público si no manejas información delicada.

  Con la IP local la conexión es dentro de la misma red, si cambias a datos o te cambias de red deja de funcionar la conexión, se deben de configurar puertos, como el localhost:3000 para la conexión, es menos seguro porque los firewalls deben estar desactivados y deben darse más privilegios a los dispositivos para su conexión.

  

Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal)

  R//

  <img width="1478" height="116" alt="image" src="https://github.com/user-attachments/assets/fa788d58-bf77-4c15-89c8-4a3029e05f63" />


  <img width="1065" height="259" alt="image" src="https://github.com/user-attachments/assets/db989e99-5a87-4e74-ba3f-2cac685a587c" />


  <img width="818" height="208" alt="image" src="https://github.com/user-attachments/assets/cb0f721c-2d9c-45bc-8029-c43117ae2bd8" />


  <img width="453" height="162" alt="image" src="https://github.com/user-attachments/assets/62944f4f-2d02-49d9-8044-a4a4290992a3" />


  ![Imagen de WhatsApp 2025-10-16 a las 17 58 57_40790927](https://github.com/user-attachments/assets/ad775d5b-5d5e-4910-9f97-8544cf2b0a39)

  <img width="1919" height="926" alt="image" src="https://github.com/user-attachments/assets/c67fb888-18f2-4236-bdfc-81707d14c591" />


  <img width="693" height="332" alt="image" src="https://github.com/user-attachments/assets/9b6da94b-6640-447d-a061-b88840c79565" />




  ### Actividad 3

<a name="Actividad_3"></a>

¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?

  R// 
  dentro del servidor:


  ```js
  const app = express();
  const server = http.createServer(app); 
  const io = socketIO(server); 
  const port = 3000;

  app.use(express.static('public'));

  ```
  Cuando el cliente se conecta, entra directamente a las dependencias públicas estáticas, desde el ordendador, sin necesidad  de definir las rutas, se accede       directamente desde el localhost. Con el app.get, se comunica con el http, la comunicación bidireccional, y se debia declarar cada solicitud.
  

Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?

  R// Para el envio de datos táctiles, se usa la función touchmoved(), la función s eencarga de guardar las posiciones en (x,y) usando el umbral para el uso de los datos, el ``` socket.emit('message', touchData);``` comunica los datos como un mensaje, llamado "message" que guarda los datos del toque, dentro del servidor la parte en cargada de interpretar los datos es ```socket.on('message', (message) => { ```, ```console.log('Received message =>', message);``` y ```socket.broadcast.emit('message', message);```, entonces, se recoge el mensaje con la posición del toque, luego este mensaje se imprime en la consola donde te marcan los datos obtenidos y finalmente se envian los datos a los clientes conectados.

Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?

  R//

  [Prueba](https://youtu.be/frDDTqNAIrI)

  Luego de la prueba, a pesar de haber dos clientes que reciban los datos, no hay interferencia, ambos reciben y se actualizan a la par, esto ocurre por el ```socket.broadcast.emit('message', message);``` se encarga de enviar los datos a todos los clientes, en este caso, ambas ventanas.
  
¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?

  R//

  ```bash
  Server is listening on http://localhost:3000
  New client connected
  New client connected
  New client connected
  Received message => { type: 'touch', x: 161, y: 236 }
  ```

  La información que se imprimie en la termianl muestra la activación con el servidor, si un cliente se conecta o se desconecta y los datos enviados por el touch.


### Actividad 4

<a name="Actividad_4"></a>

Realiza un diagrama donde muestres el flujo completo de datos y eventos entre los tres componentes: móvil, servidor y escritorio. Puedes ilustrar con un ejemplo de coordenadas táctiles (x, y) y cómo viajan a través del sistema.


<img width="870" height="271" alt="diagrama servidor" src="https://github.com/user-attachments/assets/d654ee03-73e1-430e-89c1-889be19d27b3" />



### Actividad 5 Apply 

<a name="Actividad_5"></a>

Diseña una aplicación interactiva que use el touch del móvil para controlar una visuales de tema musical de tu elección. Las visuales correrán en una aplicación de escritorio (desktop). Recuerda que ambas aplicaciones las construirás usando p5.js y utilizando el servidor Node.js como puente.


Lo que deseo hacer con la canción AERODYNAMIC de daftpunk, es simular un festival de fuegos artificiales como se puede ver en el video original. Se buscaran crear fuegos artificiales, que la canción cambie con el ritmo de la música, que salgan naves espaciales dentro del canvas. Los cambios deben ser suaves para que no sean molestos o evidentes a la vista. [video original](https://www.youtube.com/watch?v=L93-7vRfxNs)

```js
let socket;
let song;
let fft;
let fireworks = [];
let ufos = [];

let currentBgColor;
let targetBgColor;
let transitionProgress = 0;

function preload() {
  song = loadSound('AudioDaftPunk.wav');
}

function setup() {
  createCanvas(300, 400);
  socket = io();
  fft = new p5.FFT();
  fft.setInput(song);

  currentBgColor = getRandomFuturisticColor();
  targetBgColor = getRandomFuturisticColor();

  socket.on('connect', () => {
    console.log('Connected to server');
  });

  socket.on('message', (data) => {
    console.log('Received message:', data);
    if (data?.type === 'touch' && typeof data.x === 'number' && typeof data.y === 'number') {
      if (song && !song.isPlaying()) {
        song.play();
      }

      if (fireworks.length < 10) {
        fireworks.push(new Firework(data.x, data.y));
      }

      // 🛸 Genera un nuevo ovni en la posición X del toque
      ufos.push(new UFO(data.x, random(50, height - 50), random(1, 2)));
    }
  });

  socket.on('disconnect', () => {
    console.log('Disconnected from server');
  });

  socket.on('connect_error', (error) => {
    console.error('Socket.IO error:', error);
  });
}

function draw() {
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

  for (let i = fireworks.length - 1; i >= 0; i--) {
    fireworks[i].update();
    fireworks[i].show();
    if (fireworks[i].done()) {
      fireworks.splice(i, 1);
    }
  }
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
  }

  update() {
    this.x += this.speed;
    if (this.x > width + 50) {
      // Elimina el ovni cuando sale del canvas
      this.x = -9999;
    }
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
    for (let p of this.particles) {
      p.update();
    }
  }

  show() {
    for (let p of this.particles) {
      p.show();
    }
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



**HTML**


```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Desktop p5.js Application</title>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/addons/p5.sound.min.js"></script>
  <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>
  <script src="sketch.js" defer></script>
</head>
<body></body>
</html>

```


[interacción](https://youtu.be/roCmkCT1wQw)


### Autoevaluación.

Nota: 5

Se realizaron las actividades propuestas y el apply, para ver la investigación ir a las actividades correspondientes. [Actividad 1](#Actividad_1) [Actividad 2](#Actividad_2) [Actividad 3](#Actividad_3) [Actividad 4](#Actividad_4) [Actividad 5](#Actividad_5)











