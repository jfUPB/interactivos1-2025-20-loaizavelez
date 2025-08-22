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
      if (keyIsPressed && key === 'T' && key !== this.lastKey) {
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
```py
from microbit import *
import utime

display.clear()


class Event:
    def __init__(self):
        self.value = 0

    def set(self, _val):
        self.value = _val

    def clear(self):
        self.value = 0

    def read(self):
        return self.value


class SerialTask:
    def __init__(self):
        uart.init(baudrate=115200)

    def update(self):
        if uart.any():
            data = uart.read(1)
            if data:
                if data[0] == ord('A'):
                    event.set('A')
                elif data[0] == ord('B'):
                    event.set('B')
                elif data[0] == ord('S'):
                    event.set('S')
                elif data[0] == ord('T'):
                    event.set('T')


class ButtonTask:
    def __init__(self):
        pass

    def update(self):
        if button_a.was_pressed():
            event.set('A')
        elif button_b.was_pressed():
            event.set('B')
        elif accelerometer.was_gesture('shake'):
            event.set('S')
        elif pin_logo.is_touched():
            event.set('T')


class BombTask:
    def __init__(self):
        self.PASSWORD = ['A', 'B', 'A']
        self.key = [''] * len(self.PASSWORD)
        self.keyindex = 0
        self.count = 20
        self.startTime = utime.ticks_ms()
        self.state = 'CONFIG'
        display.clear()
        display.show(self.count, wait=False)

    def update(self):
     
        if self.state == 'CONFIG':
            if event.read() == 'A':
                event.clear()
                self.count = min(self.count + 1, 60)
                display.show(self.count, wait=False)

            elif event.read() == 'B':
                event.clear()
                self.count = max(10, self.count - 1)
                display.show(self.count, wait=False)

            elif event.read() == 'S':
                event.clear()
                self.startTime = utime.ticks_ms()
                self.state = 'ARMED'

      
        elif self.state == 'ARMED':
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > 1000:
                self.startTime = utime.ticks_ms()
                self.count -= 1
                display.show(self.count, wait=False)
                if self.count == 0:
                    display.show(Image.SKULL)
                    self.state = 'EXPLODED'

            if event.read() == 'A':
                event.clear()
                if self.keyindex < len(self.key):
                    self.key[self.keyindex] = 'A'
                    self.keyindex += 1

            elif event.read() == 'B':
                event.clear()
                if self.keyindex < len(self.key):
                    self.key[self.keyindex] = 'B'
                    self.keyindex += 1

            if self.keyindex == len(self.key):
                passIsOK = True
                for i in range(len(self.key)):
                    if self.key[i] != self.PASSWORD[i]:
                        passIsOK = False
                        break
                if passIsOK:
                    self.count = 20
                    display.show(self.count, wait=False)
                    self.keyindex = 0
                    self.state = 'CONFIG'
                else:
                    self.keyindex = 0

      
        elif self.state == 'EXPLODED':
            if event.read() == 'T':
                event.clear()
                self.count = 20
                display.show(self.count, wait=False)
                self.startTime = utime.ticks_ms()
                self.state = 'CONFIG'


event = Event()
bombTask = BombTask()
serialTask = SerialTask()
buttonTask = ButtonTask()


while True:
    serialTask.update()
    buttonTask.update()
    bombTask.update()
```
biblioteca

```html
<script src="https://unpkg.com/@gohai/p5.webserial@^1/libraries/p5.webserial.js"></script>
```








