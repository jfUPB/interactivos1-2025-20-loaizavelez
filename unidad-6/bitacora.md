
# Evidencias de la unidad 6

### Actvididad 1

``` bash


Admin@DESKTOP-HIHTLMH MINGW64 ~
$ git clone https://github.com/juanferfranco/entangledTest-sfi1-2025-20.git
fatal: destination path 'entangledTest-sfi1-2025-20' already exists and is not an empty directory.

Admin@DESKTOP-HIHTLMH MINGW64 ~
$ ^C

Admin@DESKTOP-HIHTLMH MINGW64 ~
$ cd entangledTest-sfi1-2025-20

Admin@DESKTOP-HIHTLMH MINGW64 ~/entangledTest-sfi1-2025-20 (main)
$ code .

Admin@DESKTOP-HIHTLMH MINGW64 ~/entangledTest-sfi1-2025-20 (main)
$ npm install

added 120 packages, and audited 121 packages in 3s

17 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
npm notice
npm notice New major version of npm available! 10.9.3 -> 11.6.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v11.6.0
npm notice To update run: npm install -g npm@11.6.0
npm notice

Admin@DESKTOP-HIHTLMH MINGW64 ~/entangledTest-sfi1-2025-20 (main)
$ npm star
npm error code EUSAGE
npm error
npm error Mark your favorite packages
npm error
npm error Usage:
npm error npm star [<package-spec>...]
npm error
npm error Options:
npm error [--registry <registry>] [--no-unicode] [--otp <otp>]
npm error
npm error Run "npm help star" for more info
npm error A complete log of this run can be found in: C:\Users\Admin\AppData\Local\npm-cache\_logs\2025-09-23T15_41_46_810Z-debug-0.log

Admin@DESKTOP-HIHTLMH MINGW64 ~/entangledTest-sfi1-2025-20 (main)
$ npma start
bash: npma: command not found

Admin@DESKTOP-HIHTLMH MINGW64 ~/entangledTest-sfi1-2025-20 (main)
$ npm start

> nodejs-test-1@1.0.0 start
> node server.js

Server is listening on http://localhost:3000


```
----
<img width="354" height="298" alt="image" src="https://github.com/user-attachments/assets/7aa457bc-3584-44d1-98f3-9a7fe72114d3" />


----

``` bash

Received win1update from ID: sxg30ZVVJsErrk5uAAAB Data: { x: 0, y: 0, width: 1528, height: 738 }
Debug - Connected clients: 1, Page1: 1, Page2: 0, Synced: 0
Sync status: pages=false, synced=false, clients=1
Debug - Connected clients: 1, Page1: 1, Page2: 0, Synced: 1
Sync status: pages=false, synced=true, clients=1
A user connected - ID: H2Idf3Ei4a4_0_moAAAD
Received win2update from ID: H2Idf3Ei4a4_0_moAAAD Data: { x: 0, y: 0, width: 1528, height: 738 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
Sync status: pages=true, synced=false, clients=2
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
Sync status: pages=true, synced=false, clients=2
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Received win1update from ID: sxg30ZVVJsErrk5uAAAB Data: { x: 228, y: 110, width: 1528, height: 738 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Received win1update from ID: sxg30ZVVJsErrk5uAAAB Data: { x: 84, y: 170, width: 1528, height: 738 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2


```

<img width="1372" height="556" alt="circulos" src="https://github.com/user-attachments/assets/4a57b7a3-6d18-473a-9aa7-ec1845da4fc8" />





**¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?**

   R// al momento de ejecutar el npm install, se descargaron los 121 paquetes con las librerias necesarias para el correcto desarrollo, se auditaron los 121 paquetes, es decir, se buscan virus o errores y al final te muestra si se encontro o no una vulnerabilidad, en este caso, no se detecto ningún tipo de vulnerabilidad.
   
   ```bash
   Admin@DESKTOP-HIHTLMH MINGW64 ~/entangledTest-sfi1-2025-20 (main)
$ npm install

up to date, audited 121 packages in 2s

17 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities



   ```


¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?

  R// en la terminan muestra que el servidor a hora esta escuchando al servidor en el **puerto 30000**, el programa de node js se esta encargando de ejecutar el codigo del servidor.
  
  ```bash
  > nodejs-test-1@1.0.0 start
> node server.js

Server is listening on http://localhost:3000


  ```

<img width="340" height="196" alt="image" src="https://github.com/user-attachments/assets/368d4e0d-b989-499b-8ea5-cc4eb61237ff" />

El servidor escucha pero no sabe a donde debe ir.
  


Describe lo que ves inicialmente en page1 y page2 en tu navegador.

  R// Si unicamente se abre una de las dos paginas, muestra un mensaje de espera, lo que significa que busca sincronizarse con la otra pagina.


  <img width="1254" height="351" alt="image" src="https://github.com/user-attachments/assets/1aa80a67-ba41-42c0-94dc-b3774ae84ee2" />


  <img width="887" height="474" alt="image" src="https://github.com/user-attachments/assets/75011765-0b25-49ca-8470-02d030bba30e" />


  Si se abren ambas paginas, se sincronizan y muestran el ciruclo en el centro de la ventana, se debe separar en ventanas diferentes para poder ver el como cambian.


  <img width="1205" height="601" alt="image" src="https://github.com/user-attachments/assets/753637da-0754-4a87-b75b-fc17b6687762" />


¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?


  R// aparece la conexión del ID del cliente, luego muestra el comportamiento de las ventanas, su posición y altura en el eje coordenado (X,Y)



  ```bash
  Received win2update from ID: BFUK7V-OW6m3_DfiAAAD Data: { x: 550, y: 160, width:
 492, height: 375 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Received win2update from ID: BFUK7V-OW6m3_DfiAAAD Data: { x: 548, y: 160, width:
 492, height: 375 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Received win2update from ID: BFUK7V-OW6m3_DfiAAAD Data: { x: 548, y: 160, width:
 494, height: 376 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced



  ```

Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?

  R// 

  <img width="1629" height="925" alt="image" src="https://github.com/user-attachments/assets/fc2b2ce6-c15d-4c14-a254-25d7c37f64ea" />

  

  <img width="1048" height="663" alt="image" src="https://github.com/user-attachments/assets/8eb4a245-a33c-4404-8225-d8fe97b47dc4" />


  Desplazar las ventanas permiten visualizar el comportamiento de los ciruclos, usando de referencia la esquina superior de la ventana. Se observa que se           conectan con una linea y si las ventanas se superponen se fusión en una sola ventana y ya no se ve el corte.


### Actividad 2



**Piensa en cómo te conectas a Internet en casa o en la Universidad. ¿Usas Wi-Fi? ¿Un cable de red? Eso es simplemente tu “rampa de acceso” a la gran red de carreteras. ¿Qué pasaría si esa rampa se corta? Anota tus ideas.**


  R// Cada vez que una rampa se rompe o se bloquea el vehiculo, en este caso el celular o el dispositivo conectado, perdiendo la conexión. Los mis ocurre si estas conectado por cable, si el cable se daña o alguno de los pines tiene algún desperfecto dejas de tener conexión.



**¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?**

  R// En un restaurante la analogía se da de la siguiente forma, el cliente es la persona que ordena la comida y la cajera o el mesero es el servidor, el cliente ordena por ejemplo una hamburguesa (descargar una imagen) y el cajero guarda esa solicitud y te entrega la orden. 

**Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.google.com) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?**

  R// tomare el ejemplo del siguiente ejemplo de negrogamer (https://www.youtube.com/watch?v=aYkMldZyOQU), en este caso el protocolo es **https** el nombre del dominio es youtube entonces en este caso sería **www.youtube.com** y la ruta específica es **/watch?v=aYkMldZyOQU**, si retiras la ruta específica la plataforma te envia directamente a la pagina principial, donde se encuentran los recomendados y el tablón de videos.


Compara HTTP con los protocolos seriales que usaste.

- ASCII/BINARIO: Se encargar de enviar carácteres empaquetados, ambos tiene un metodo distintos, en nuestros casos de estudio se investigó que son usualmentes usados para comunicaciones seriales.
- HTTPS: El servidor se comunica con el cliente por alguna petición, por ejemplo descargar una imagen y por medio de texto se comunican. Claro no es una conversación como si estuvieras con un chat bot, más interno y no es algo que una persona pueda ver.

¿Qué similitudes encuentras?

  R// La similitud clave es la comunicación, los 3 metodos están diseñados para comunicarse con maquinas, cada protocolo de comunicación debe tener una  aquina que pueda interpretar esa información, un micro:bit no sera capaz de leer un protocolo http porque no esta diseñado para eso.

¿Qué diferencias clave ves?

Los protocolas ASCII y binarios deben enviar paquetes de carácteres HEX y un motor de busqueda no puede interpretar ese código porque no está diseñado para esa comuniación, un microbit no puede interpretar el https porque no se diseña para leer el encabezado, el nombre de dominio y la dirección.

¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?

R// Porque se debe ser más específico, si quieres descargar o ver una imagen no te basta con decir por ejemplo, quiero ver un video, debes decir que plataforma quieres ver el video, el dominio y de quien es el video, debes ser preciso con la información y un paquete binario al estar limitado a una secuencia no sera capaz de describir la petición del usuario.






