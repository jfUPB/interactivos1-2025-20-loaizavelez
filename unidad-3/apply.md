# Unidad 3


## 🛠 Fase: Apply


### Primer codigo 

```py
let count
let state
let startT



function setup() {
  
  starTime = 20
  count = 0
  state = 'Config'
  

  
  
  createCanvas(400, 400);
  connectBtn = createButton("A");
  connectBtn.position(80, 300);
  
  
  connectBtn = createButton("B");
  connectBtn.position(350, 300);
  
  connectBtn = createButton("S");
  connectBtn.position(200, 300);
  
  connectBtn = createButton("T");
  connectBtn.position(200, 50);
  
 
 

}

function draw() 
{
  
  background(400);
  text(starTime,40,200)
  textSize(50)
  fill(0)
  
  
  if (state == 'Config')
  {
    if (starTime < 60 && starTime > 10 && connectBtn.mousePressed)
    {
      starTime++
    }
  }
  
}
```

<img width="1513" height="510" alt="codigo 2" src="https://github.com/user-attachments/assets/a0ff869d-0a8c-450b-b072-451fd0a9ddef" />

El tiempo se contiene en el intervalo de 10 segundos y de 60 segundos, pero aumenta sin control sin enviar ningún comando.


### Segundo Codigo.

```js

function setup() {
 
bombTask = new BombTask()
  
  
  createCanvas(400, 400);
  connectBtn = createButton("A");
  connectBtn.position(80, 300);
  
  
  connectBtn = createButton("B");
  connectBtn.position(350, 300);
  
  connectBtn = createButton("S");
  connectBtn.position(200, 300);
  
  connectBtn = createButton("T");
  connectBtn.position(200, 50);
  
 
 

}

class BombTask
{
  BombTask()
  {
    this.Password = ['A','B','A']
    this.key = new Array(this.Password.length).fill('');
    this.keyindex = 0
    this.count = 0
    this.startTime= millis()
    this.state = "CONFIG"
    this.displayText = this.count
    
  }

  
  
}


```

S<img width="1762" height="638" alt="codigo 1" src="https://github.com/user-attachments/assets/5acf9c90-18f4-4e35-a795-22318a9f7e9a" />

a pesar de inicializar el canvas no se muestra en pantalla, se muestran los botones pero aún no tienen ninguna funcionalidad. Anteriormente se mostraba un texto que decia cuanto tiempo qudaba el cual se aumentaba sin control.


```js

    if (this.state === 'CONFIG') {
      if (keyIsPressed && key === 'A') {
        this.count = min(this.count + 1);
        this.displayText = this.count;
      }
      if (keyIsPressed && key === 'B') {
        this.count = max(10, this.count - 1); 
        this.displayText = this.count;
      }
```

Se supone que debería aumentar el tiempo del contador pero se esta sumando y no tiene limite. Ademas de que no existe una función was_pressed, por lo tanto siempre sumara mientras se mantega presionado el boton.

<img width="1430" height="508" alt="codigo 3" src="https://github.com/user-attachments/assets/ef6ba683-9cb6-4e8a-9ca6-4190540b30df" />


Llega hasta 60 y respeta el limite, pero no hace lo mismo con el 10, llega hasta negativos.
R// el problema era que ambos eran minimos, lo que causaba que el limite no se respetara.



```js
 if (this.state === 'ARMED')
      {
        this.displayText = 'HOLA'
        
      }
```

Aqui entra en armed porque muestra el mensaje hola

<img width="1298" height="460" alt="codigo 4" src="https://github.com/user-attachments/assets/01f5c2fc-2856-4aae-9540-e728c944fc2e" />


### Actividad 6

```js
let bombTask;

function setup() {
  createCanvas(200, 200);
  bombTask = new BombTask();
}

function draw() {
  background(220);
  bombTask.update();
  textSize(32);
  textAlign(CENTER, CENTER);
  text(bombTask.displayText, width / 2, height / 2);
}

class BombTask {
  constructor() {
    this.PASSWORD = ['A', 'B', 'A'];
    this.key = new Array(this.PASSWORD.length).fill('');
    this.keyindex = 0;
    this.count = 20;
    this.startTime = millis();
    this.state = 'CONFIG';
    this.displayText = this.count;
    this.lastKey = ''; 
  }

  update() {
    
    if (this.state === 'CONFIG') {
      if (keyIsPressed && key !== this.lastKey) {
        if (key === 'A') {
          this.count = min(this.count + 1, 60);
          this.displayText = this.count;
        }
        if (key === 'B') {
          this.count = max(10, this.count - 1);
          this.displayText = this.count;
        }
        if (key === 'S') {
          this.startTime = millis();
          this.state = 'ARMED';
        }
        this.lastKey = key;
      } else if (!keyIsPressed) {
        this.lastKey = '';
      }
    }

    // ARMED: ingresar contraseña, cuenta regresiva
    else if (this.state === 'ARMED') {
      if (keyIsPressed && key !== this.lastKey) {
        if (key === 'A' || key === 'B') {
          this.key[this.keyindex] = key;
          this.keyindex++;
        }

        if (this.keyindex === this.key.length) {
          let passIsOK = true;
          for (let i = 0; i < this.key.length; i++) {
            if (this.key[i] !== this.PASSWORD[i]) {
              passIsOK = false;
              break;
            }
          }

          if (passIsOK) {
            this.count = 20;
            this.displayText = this.count;
            this.keyindex = 0;
            this.state = 'CONFIG';
          } else {
            this.keyindex = 0;
          }
        }
        this.lastKey = key;
      } else if (!keyIsPressed) {
        this.lastKey = '';
      }

      // cuenta regresiva
      if (millis() - this.startTime > 1000) {
        this.startTime = millis();
        this.count -= 1;
        this.displayText = this.count;

        if (this.count === 0) {
          this.displayText = '💣';
          this.state = 'EXPLODED';
        }
      }
    }

    
    else if (this.state === 'EXPLODED') {
      if (keyIsPressed && key === 'R' && key !== this.lastKey) {
        this.count = 20;
        this.displayText = this.count;
        this.startTime = millis();
        this.state = 'CONFIG';
        this.lastKey = key;
      } else if (!keyIsPressed) {
        this.lastKey = '';
      }
    }
  }
}
```

### Actividad 7








