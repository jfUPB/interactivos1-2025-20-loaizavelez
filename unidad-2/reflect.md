# Unidad 2


## 🤔 Fase: Reflect

### Parte 1: recuperación de conocimiento (Retrieval Practice)

- Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?
  
  R//Una maquina de estados es un programa que permite hacer un proceso especifico, se ejecuta una serie de procesos en armonía sin intervenir un procesos, siempre y cuando, este programado de forma correcta. Los cuatro componentes son: eventos, acciones, transiciones y estados.

- Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender un temporizador y botones “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit. ¿Qué problema soluciona en comparación con usar funciones como sleep()?

  R// el sleep es una función que pausa el programa, esto en programas sencillos no debería generar ningún tipo de problemas, sin embargo en programas más complejos, que la maquina duerma, es pausar procesos anteriores que podrían causar conflictos.

- Imagina que tienes que añadir una nueva funcionalidad a la bomba temporizada: si se agita (shake) el micro:bit mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?

  R// en el esatdo armed agregaria la función de si se agita el aceleremotro, se toma el tiempo actual y se verifica si cruza la franja de tiempo, entre 10 y 60  segs, y se le divie por 2 con el doble (//) para que no arroje decimales.

- Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.

R// un vector de prueba es una herramienta que se usa para verificar si un proceso en el programa se cumple de manera correcta, se viaja por estado en estado, cumpliendo cada condición.

### Parte 2: reflexión sobre tu proceso (Metacognición)

- ¿Qué parte del diseño de la bomba temporizada te resultó más desafiante: crear el diagrama de estados (Actividad 04) o traducir ese diagrama a código MicroPython (Actividad 05)? ¿Por qué?

  R// Lo más complicado fue mostrar el tiempo, no lo logre y al final no supe que debía hacer, se muestra el tiempo que se le asigno al temporizador, pero no su cuenta regresiva. Intente con leds pero el resultado era igual.
  
 - Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?
   
   R// Cuando se llega al estado blow o creeria que incluso en estados anteriores, cuando se presionan los botones para agregar o disminuir tiempo, cuando se vuelve al estado init se aplica ese tiempo 

  
