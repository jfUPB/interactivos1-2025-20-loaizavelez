
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

  R// Al correr en localhost y estar protegida la red no permite que un dispositivo externo se conecte por temas de seguridad ya que este se convierte en el mismo servidor y siempre buscara el computador. Por eso se abre un servidor en ña nube en dev tunnels. Enviando los datos atraves de este servidor, sin

Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.

  R//

Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?

  R//

Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal)

  R//

