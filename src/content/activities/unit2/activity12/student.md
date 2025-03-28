# Solución

### Código

```py

from microbit import *
import utime

# Variables globales
tiempo = 20  # Valor inicial del temporizador (segundos)
config_mode = True  # Estado inicial en modo configuración

# Funciones
def aumentar_tiempo():
    global tiempo
    if config_mode and tiempo < 60:
        tiempo += 1
        display.show(str(tiempo))

def disminuir_tiempo():
    global tiempo
    if config_mode and tiempo > 10:
        tiempo -= 1
        display.show(str(tiempo))

def armar_bomba():
    global config_mode
    if config_mode:
        config_mode = False
        display.scroll("Armed")
        cuenta_regresiva()

def resetear_bomba():
    global config_mode, tiempo
    config_mode = True
    tiempo = 20
    display.scroll("Reset")
    display.show(str(tiempo))

def cuenta_regresiva():
    global tiempo
    while tiempo > 0:
        display.show(str(tiempo))
        sleep(1000)
        tiempo -= 1
    explosion()

def explosion():
    display.show(Image.SKULL)
    for _ in range(5):
        pin0.write_digital(1)
        sleep(200)
        pin0.write_digital(0)
        sleep(200)

# Bucle principal
display.show(str(tiempo))
while True:
    if button_a.is_pressed():
        aumentar_tiempo()
        sleep(200)
    if button_b.is_pressed():
        disminuir_tiempo()
        sleep(200)
    if accelerometer.was_gesture("shake"):
        armar_bomba()
    if pin1.is_touched():
        resetear_bomba()
    sleep(100)
```
### Link de funcionamiento de bomba temporizada

https://youtu.be/wqSlkT4iDwA?si=epTz2vautGO_kaIE
