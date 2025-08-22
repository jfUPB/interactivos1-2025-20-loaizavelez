# Unidad 3


## 🛠 Fase: Apply

### Actividad 8
**Parte 1: recuperación de conocimiento (Retrieval Practice)**
- Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?
  R// Una maquina de estados, se podría decir que es un conjunto de procesos, cada proceso se ejecuta dependediendo si esta en ese estado o no, sin embargo también permite pasar entre estados, si se encuentra en estado 3 puede volver al 2.


- Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender varios eventos y tareas “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit o en p5.js. ¿Qué problema soluciona en comparación con usar funciones como sleep()?

  R// el sleep el problema que tiene, es detener el programa. Cuando se detiene el programa se paran todos los procesos, si se tenia un contador este se detiene, retrasando el resto de procesos. Una maquina de estados permite que estos procesos se ejecuten de manera constante y sin interrupciones entre procesos.

- Imagina que tienes que añadir una nueva funcionalidad a la bomba: si se recibe un evento especial (por ejemplo, una combinación de botones o un comando serial) mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?
  
  R//

- Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.

  R//
