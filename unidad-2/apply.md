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
            start_time -= 10000
            speech.say('Low' + str(start_time // 1000) + 'seconds')
            print(start_time)
        if accelerometer.was_gesture('shake'):
            music.play(music.JUMP_DOWN)
            current_state = STATE_Armed  
            ticks = utime.ticks_ms()
            
    if current_state == STATE_Armed:
       
        display.scroll(str(start_time // 1000))  
       
        if utime.ticks_diff(utime.ticks_ms(), ticks) > start_time:                
                       
            speech.say('Explosion comfirmed')
            current_state = STATE_Blow  
        
            
            

    if current_state == STATE_Blow:
        
        display.show(Image('00900:'
                               '09990:'
                               '90009:'
                               '90009:'
                               '09990'))
        if pin_logo.is_touched():
            
            display.show(Image.MEH)
            current_state = STATE_INIT
            start_time = 20000
            set_volume(190)
            music.play(music.FUNERAL)
        

```

### Vectores de prueba
- 1.) Se inicializa el codigo, este debe pasar a el estado INIT, donde se vera la cara feliz.

- <img width="635" height="380" alt="estado init" src="https://github.com/user-attachments/assets/45ec45f9-41ec-4a22-8ae5-9f3a377c4d09" />
- 2.) En el estado init los botones "a" y "b" deben aumentar o disminuir el tiempo en 10 segundos, ademas de no sobrepasar los 60 segundos o ser menor que 10 segundos, ademas el alta voz comunica la variación en el tiempo. Para el acelerometro este reproduce el audio asignado y pasa al estado armado.
<img width="567" height="536" alt="variacion en el tiempo" src="https://github.com/user-attachments/assets/d3b118b7-a681-4dda-9ee0-2b1c32043cec" />
- 3.) En el estado Armed los leds deben mostrar el tiempo asginado a la bomba, es decir, si son 20 segundos debe mostrar el 20 y si son 10 deben mostrar el número 10 y ese es el tiempo que debe de transcurrir. En este estado la los botones "a" y "b" no modifican ni alteran el conteo regresivo y el boton touch no reinicia esta fase. Al terminar el contador se reproduce el mensaje de "explosion confirmada" y se pasa al estado de explosión.
- 4.) En el estado de explosión se debe visulizar en los leds la "explosión" dentro de este estado los botones "a" y "b" no modifican el esatdo Explosión y al presionarse el botón touch, se visualiza la cara "Meh", se reproduce la musica y se pasa al estado init.






