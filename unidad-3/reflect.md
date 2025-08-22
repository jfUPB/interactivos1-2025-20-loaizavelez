# Unidad 3


## 🤔 Fase: Reflect


### Actividad 8
- Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?
  
  R// Una maquina de estados, es un programa que se ejecuta sin detener ninguna función o pausandose por completo, ejecuta acción por acción.

- Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender varios eventos y tareas “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit o en p5.js. ¿Qué problema soluciona en comparación con usar funciones como sleep()?

  R// El sleep detiene el programa, todo procesos que se estuviera ejecutando hasta cierta parte, se para, si tenías un reloj este se va a parar, causando retrasos entre el resto de procesos.

-Imagina que tienes que añadir una nueva funcionalidad a la bomba: si se recibe un evento especial (por ejemplo, una combinación de botones o un comando serial) mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?  

  R//

- Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.
  
  R// Un vector de prueba es una herramienta que permite ejecutar y ver los resultados que se esperan, si quieres por ejemplo ver si se muetsra un número en pantalla, haces el vector de prueba y ves si el resultado es correcto.

**Parte 2: reflexión sobre tu proceso (Metacognición)**

- ¿Qué parte del diseño de la bomba te resultó más desafiante: crear el diagrama de estados o traducir ese diagrama a código? ¿Por qué?

  R// Más que todo traducirlo de pythoon a javascript, hubieron una cantidad de funcionalidades que me dejaron atascado por mucho tiempo, ademas de tener que hacer trucos porque función para presionar la tecla era constante, causando que la contraseña siempre fuera incorrecta.

-Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?

  R// Un error muy común fue que el tiempo auemnteba sin control, luego el tiempo disminuía sin control. Lo que pasaba es que la tecla siempre estaba presionada haciendo que en todo momento aumentara.

- El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?

  R// Empece con una bitacora donde iba anontando cada cambio y cada nueva funcionalidad para ir entendiendo que estaba bien y que estaba mal. Mientras agregaba nuevas funciones, por ejemplo sumar tiempo, detectar la contraseña y así.

- Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?

  R//




### Actividad 9

- **Continuar: ¿Qué actividad, explicación o ejemplo de esta unidad te ayudó más a entender el poder de las máquinas de estados? ¿Qué elemento consideras que es indispensable y debería mantener?**
  
  R// La actividad de la bomba.

- **Dejar de hacer: ¿Hubo algún paso o actividad que te pareció confuso? ¿Qué cambiarías o eliminarías?**
  R// La parte más confusa fue la del serial port, pensaba que el codigo ya estaba listo pero resulta que no se comunica.

- Empezar a hacer: ¿Qué te habría ayudado a entender mejor?
  R// Saber como traducir de un idioma a otro para manejar más facil las clases.

- Ritmo y dificultad: En una escala del 1 (muy fácil) al 5 (muy difícil), ¿Cómo calificarías la dificultad de pasar del análisis de un programa a diseñar y programar uno complejo? ¿Por qué?
  
  R// 5, el traducir de un idioma a otro, con estructuras y comportamientos diferentes es complicado, ademas el tiempo me parece que el tiempo de clase que se dio para el uso del microbit.

- Comentario adicional: ¿Hay algo más que te gustaría compartir sobre tu proceso de aprendizaje en esta unidad? ¿Algún momento de frustración o de “¡Aha!” que quieras destacar?

  R// En caso de usar el microbit si se puede dar tiempo de la siguiente clase para terminar y poder usar el microbit para saber si el codigo es util.

  



