
# Evidencias de la unidad 7

### Actividad 1

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

¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?

  R//

  









