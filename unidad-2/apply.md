# Unidad 2


## 🛠 Fase: Apply


### Codigo 

```py
# Imports go at the top
from microbit import *
import utime
import speech

STATE_INIT = 0
STATE_Armed = 1
STATE_Blow = 2

ARMED_INTERVAL = 20000

current_state = STATE_INIT
start_time=20000

while True:
    if current_state == STATE_INIT:
        if button_a.was_pressed():
            start_time +=1000

            
            mensaje = "Start time is " + str(start_time) #feedback de tiempo
            speech.say(mensaje)

            
            
           
            
           

    if button_b.was_pressed():
        start_time-=1000
        print(start_time)
        

```
