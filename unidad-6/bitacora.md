
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

**Piensa en una página web simple, como un formulario de login.**

¿Qué parte crees que es HTML (ej. los campos de texto, el botón)?

R// Un HTIML dentro de un Login puede son los campos donde debes ingresar la información vital para un inicio de sesión, si es primera vez debes llenar campos como el nombre, apellidos, localidad y luego la contraseña.

¿Qué parte es CSS (ej. el color del botón, el tipo de letra)?


R// El CSS o Cascading Style Sheets es el estilo visual que se le da a la pagína, colores de los botones, crear usuario, recordar contraseña, fuentes de letra, márgenes y otros agregados visuales como animaciones de ingreo se usuario.


¿Qué parte es JavaScript (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de “contraseña incorrecta” que aparece sin recargar la página)?

R// el Java sería la verificación de los datos, si ya es una cueta existente o una contraseña incorrecta o previamente usada, es el vigilante que se encarga de ejecutar de manera ordenada los eventos de la pagína. 



**Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”.**

¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web?

R// La diferencia con el p5.js es que siempre verifica y actualiza la aplicación, por ejemplo en el trabajo de modificar una aplicación de arte, el draw verificaba en todo momento el estado de la maquina para toda posibilidad, si se presiona un botón o si se mueve el acelerometro. Cuando se mofidica a eventos se deja el pensamiento de "Qué esta pasando" a "Qué va a pasar" al fin y al cabo es una pagína que muchas personas no van a seguir una ruta específica, algunos pueden ir directo a lo que quieren hacer, otros viajaran por las ventanas y otros se quedaran en la pagína de inicio, son muchas cosas que pueden pasar y verificar en todo momento cada estado consume muchos recursos.

¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado?

R// No, no hay sentido en estar refrescando la pagína si no hay nada que haya cambiado, ademas hay que considerar que es una pagína que miles o millones de personas usaran simultaneamente, el cosnumo de recursos es excesivo e injustificado.


¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?

R// usar el mismo lenguaje para ambos casos, cliente y servidor, permite aumentar la vida util de la aplicación o del proyecto web, si todo se centraliza en un solo tipo de lenguaje es más facil darle mantenimiento, imagina que el cliente esta hecho en **C++** o **C#** y el servidor en java, el conflicto entre datos, como carácteres, si hay un error debes modificar ambas aplicaciones para solucionarlo, por ello, centralizarlo en un solo lenguaje agiliza y mejora el ciclo de vida de la pagína web.


Resume con tus propias palabras la diferencia fundamental entre una comunicación HTTP tradicional y una comunicación usando WebSockets/Socket.IO. ¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real?

R// El HTTP es una comuniación basada en peticiones, el cliente envía una petición y el servidor recibe y da la respuesta, es imperativo resaltar que es el cliente el que debe hacer la petición, el servidor no te va a dar una respuesta o una pregunta. Por otro lado, el websocket siempre esta pendiente y siempre se esta comunicando con el cliente, permitiendo respuestas en tiempo real sin tiempos de espera, es util para serivicios de mensajería **instantanea** como lo es messenger y lso mensajes directos de redes sociales o los chats de juegos en linea.

### Actividad 3

Intenta acceder a http://localhost:3000/page1. ¿Funciona?


R// <img width="322" height="101" alt="image" src="https://github.com/user-attachments/assets/0e1a2fc2-cc90-4fdb-82c3-db60edd7622f" /> 

No funciona, no reconoce la dirección de la pagína.


Ahora intenta acceder a http://localhost:3000/pagina_uno. ¿Funciona?


R// <img width="1249" height="285" alt="image" src="https://github.com/user-attachments/assets/42a2ec9f-4bf5-4140-b2ec-cd2889eff6e4" />


Sí, ya funciona. Ahoa ya reconoce la ruta.


¿Qué te dice esto sobre cómo el servidor asocia URLs con respuestas? Restaura el código.

Después de modificar y restaurar el codigo me doy cuenta que la ruta se define en la siguiente linea.


```js
app.get('/page1', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page1.html'));
});

```
dependiendo de la ruta que le pongas, se debe modificar en esta parte y ya te permite visualizar que al momento de refrescar la pagína te salta un error si lo midifcaste y que solo funciona si usas la nueva ruta.



Mueve la ventana de page1. Observa la terminal del servidor. ¿Qué evento se registra (win1update o win2update)? ¿Qué datos (Data:) ves? ; Mueve la ventana de page2. Observa la terminal. ¿Qué evento se registra ahora? ¿Qué datos ves?

los datos recibidos para page1 son:


```bash
Received win1update from ID: 0CLAu5CnFO6rtVMCAAAC Data: { x: -80, y: 96, width: 776, height: 744 }
```

los datos recibidos para page2 son:

```bash
Received win2update from ID: 4FkKbMIeJ8UClXU_AAAD Data: { x: 552, y: 133, width: 776, height: 747 }
```

Para ambos se registra el Identificador y la posición en el eje (x,y) y el tamaño de la ventana.





Experimento clave: cambia socket.broadcast.emit(‘getdata’, page1); por socket.emit(‘getdata’, page1); (quitando broadcast). Reinicia el servidor, abre ambas páginas. Mueve page1. ¿Se actualiza la visualización en page2? ¿Por qué sí o por qué no? (Pista: ¿A quién le envía el mensaje socket.emit?). Restaura el código a broadcast.emit.

[Video_experimento](https://youtu.be/p-BB4ZRbz8Q)

Después de modificar el codigo, se puede visualizar que ambos circulos no se estan sincronizando, ya no conectan las lineas a su centro, esto pasa porque no se estan comunicando, cuando se retira el broadcast deja de comunicarse, por lo tanto, esos datos se pierden o directamente no salen porque no hay nadie a quien comunicarselo


### Actividad 4


Refresca la página page2.html. Observa la consola del navegador. ¿Ves algún error relacionado con la conexión? ¿Qué indica?

R//

- Estado conectado:


<img width="684" height="215" alt="image" src="https://github.com/user-attachments/assets/cdb01d64-a104-4211-aa9b-34571de5490f" />


- Estado desconectado:

<img width="665" height="545" alt="image" src="https://github.com/user-attachments/assets/8d1bfe5a-8365-4626-a9a5-2a96f4ca306a" />

Este error indica que no logra establecer conexión con el servidor.


Vuelve a iniciar el servidor y refresca la página. ¿Desaparecen los errores?

R// Luego de conectarlo desaparecen los errores.

**Experimento.**

- Comenta la línea socket.emit(‘win2update’, currentPageData, socket.id); dentro del listener connect.

- Reinicia el servidor y refresca page1.html y page2.html.

- Mueve la ventana de page2 un poco para que envíe una actualización.

¿Qué pasó? ¿Por qué?


R// 

<img width="1782" height="763" alt="image" src="https://github.com/user-attachments/assets/a9bfc418-d552-4330-950b-33775b6e4ab5" />

Al comentar la linea, se ve esta situación, anteriormente cuando se elimino el **broadcast** unicamente el circulo no se sincronizaba con el de la pagina 1, pero aun asi seguia apareciendo, en este caso la pagina 2 directamente no es capaz de sincronizarse con la otra ventana. 

<img width="1861" height="788" alt="image" src="https://github.com/user-attachments/assets/0a6c1927-41f3-486f-8257-26d3045b4091" />

Cuando se sincroniza directamente vuelve a tener el comportamiento de cuando se elimina el broadcast.


**Experimenta**

Abre ambas páginas (es posible que ya las tengas abiertas).

Mueve la ventana de page1. Observa la consola del navegador de page2. ¿Qué datos muestra?

R// 

<img width="697" height="527" alt="image" src="https://github.com/user-attachments/assets/1b67a505-c80e-47e1-b37d-03219cede765" />

```html
Connected with ID: uhyf4T185h7OrrFyAAAD
page2.js:44 Received valid remote data: Object
page2.js:51 Sync status: NOT SYNCED
page2.js:51 Sync status: SYNCED
page2.js:44 Received valid remote data: Object
2page2.js:51 Sync status: SYNCED
page2.js:44 Received valid remote data: Object
3page2.js:51 Sync status: SYNCED
page2.js:44 Received valid remote data: Object
2page2.js:51 Sync status: SYNCED

```

Mueve la ventana de page2. Observa la consola de page1. ¿Qué pasa? ¿Por qué?

R//

<img width="1236" height="300" alt="image" src="https://github.com/user-attachments/assets/2c005eaf-fc05-4b6c-ac5d-acbdad361711" />

```html
Connected with ID: PKjM0QH_BO0DQYgdAAAB
page1.js:43 Received valid remote data: Object
2page1.js:50 Sync status: NOT SYNCED
page1.js:43 Received valid remote data: Object
2page1.js:50 Sync status: NOT SYNCED
4page1.js:50 Sync status: SYNCED
page1.js:43 Received valid remote data: Object
2page1.js:50 Sync status: SYNCED
334page1.js:50 Sync status: SYNCED
```

La consola la información de interes es **334page1.js:50 Sync status: SYNCED** muestra la cantidad de actualizaciones en la sincronización con la page2, no muestra el resto de datos como la posición porque esa esta incluida en la page2




🧐🧪✍️ **Experimenta**

Observa checkWindowPosition() en page2.js y modifica el código del if para comprobar si el código dentreo de este se ejecuta.
Mueve cada ventana y observa las consolas. ¿Qué puedes concluir y por qué?

R// la lineas modificadas son las siguientes:


```js
 currentPageData = {
       // x: window.screenX,
       // y: window.screenY,
```

<img width="1836" height="592" alt="image" src="https://github.com/user-attachments/assets/9cbefe25-d2f3-486f-85ef-b665f38df028" />

Luego de comentar esas dos lineas, dejan de sincronizarse las paginas, esto pasa porque al no enviarse los datos de la posición de la ventana, la función del servidor de **isvalidwindowdata** deja de recibir esos datos y ya no puede validarlos.


```js
function isValidWindowData(data) {
    return data && 
           typeof data.x === 'number' && 
           typeof data.y === 'number' && 
           typeof data.width === 'number' && data.width > 0 &&
           typeof data.height === 'number' && data.height > 0;
}

```

otra modificación en esa función es la siguiente, se le suma por una unidad al tamaño de la ventana en ambos ejes.

```js
 currentPageData = {
        x: window.screenX ++,
        y: window.screenY ++,
        width: window.innerWidth,
        height: window.innerHeight
```

El resultado es el mismo.







