# Solución

```py
from microbit import *
import utime

# Variables globales
tiempo = 20  # Valor inicial del temporizador (segundos)
config_mode = True  # Estado inicial en modo configuración
desactivacion = ["A", "B", "A", "SHAKE"]  # Secuencia correcta
entrada_usuario = []  # Lista para registrar la secuencia de entrada

# Funciones
def aumentar_tiempo():
    global tiempo
    if config_mode and tiempo < 60:
        tiempo += 1
        display.show(str(tiempo))
        sleep(200)

def disminuir_tiempo():
    global tiempo
    if config_mode and tiempo > 10:
        tiempo -= 1
        display.show(str(tiempo))
        sleep(200)

def armar_bomba():
    global config_mode
    if config_mode:
        config_mode = False
        display.scroll("Armed")
        sleep(500)  # Pequeña pausa antes de iniciar cuenta
        cuenta_regresiva()

def resetear_bomba():
    global config_mode, tiempo, entrada_usuario
    config_mode = True
    tiempo = 20
    entrada_usuario = []
    display.scroll("Reset")
    display.show(str(tiempo))
    sleep(200)

def cuenta_regresiva():
    global tiempo
    while tiempo > 0:
        display.show(str(tiempo))
        sleep(1000)
        tiempo -= 1
        if verificar_desactivacion():
            return  # Si la secuencia es correcta, se reinicia la bomba
    explosion()

def explosion():
    display.show(Image.SKULL)
    for _ in range(5):
        pin0.write_digital(1)
        sleep(200)
        pin0.write_digital(0)
        sleep(200)

def registrar_entrada(evento):
    global entrada_usuario
    entrada_usuario.append(evento)
    if len(entrada_usuario) > len(desactivacion):
        entrada_usuario.pop(0)  # Mantener solo los últimos 4 eventos

def verificar_desactivacion():
    if entrada_usuario == desactivacion:
        display.scroll("Disarmed")
        resetear_bomba()
        return True
    return False

# Bucle principal
display.show(str(tiempo))
while True:
    if button_a.is_pressed():
        if config_mode:
            aumentar_tiempo()
        else:
            registrar_entrada("A")
            verificar_desactivacion()
    if button_b.is_pressed():
        if config_mode:
            disminuir_tiempo()
        else:
            registrar_entrada("B")
            verificar_desactivacion()
    if accelerometer.was_gesture("shake"):
        if config_mode:
            armar_bomba()
        else:
            registrar_entrada("SHAKE")
            verificar_desactivacion()
    if pin1.is_touched():
        resetear_bomba()
    sleep(100)
```
1. **Definir la secuencia correcta:** Se creó una lista desactivacion = ["A", "B", "A", "SHAKE"] que representa la secuencia que el usuario debe ingresar para desactivar la bomba.

2. **Registrar las entradas del usuario:** Cada vez que el usuario presiona el botón A, B o agita el micro:bit, se almacena el evento en la lista entrada_usuario.

3. **Mantener solo las últimas cuatro entradas:** Para asegurarnos de que el usuario ingrese la secuencia en el orden correcto, la lista entrada_usuario se mantiene con un máximo de cuatro elementos. Si se ingresa una nueva entrada, se elimina la más antigua.

4. **Verificar la secuencia:** Después de cada entrada del usuario, se compara entrada_usuario con desactivacion. Si coinciden, se muestra el mensaje "Disarmed" en la pantalla LED y la bomba se reinicia al modo de configuración.
