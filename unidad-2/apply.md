# Unidad 2


## 🛠 Fase: Apply


### Codigo 

```py
# Imports go at the top
from microbit import *
import utime
import speech
import music

STATE_INIT = 0
STATE_Armed = 1
STATE_Blow = 2
bomb_image = Image(
    '00900:'
    '09990:'
    '90009:'
    '90009:'
    '09990'
)


current_state = STATE_INIT
start_time = 20000 
ticks = 0

while True:
    if current_state == STATE_INIT:
        display.show(Image.HAPPY)
        if button_a.was_pressed() and start_time < 60000:
            start_time += 10000
            speech.say('Plus' + str(start_time // 1000) + 'seconds')
            print(start_time)
        if button_b.was_pressed() and start_time > 10000:
            start_time -= 1000
            speech.say('Low' + str(start_time // 1000) + 'seconds')
            print(start_time)
        if accelerometer.was_gesture('shake'):
            music.play(music.JUMP_DOWN)
            current_state = STATE_Armed  
            ticks = utime.ticks_ms()
            
    if current_state == STATE_Armed:
        display.show(Image.SKULL)
        if utime.ticks_diff(utime.ticks_ms(), ticks) > start_time:
            
            music.pitch(880, 200)
            music.pitch(440, 200)
            current_state = STATE_Blow  
            display.show(bomb_image)
            

    if current_state == STATE_Blow:
        if pin_logo.is_touched():
            current_state = STATE_INIT
            start_time = 20000
            music.play(music.FUNERAL)
        

```

