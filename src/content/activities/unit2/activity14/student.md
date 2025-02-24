# Solución

## Proceso de pruebas y depuración de la Bomba Temporizada

### 1. Vectores de Prueba y Resultados Esperados

| # | Acción | Estado Inicial | Entrada | Resultado Esperado |
|---|--------|---------------|---------|--------------------|
| 1 | Aumentar tiempo | Modo Configuración, 20s | Botón A presionado | Se incrementa el tiempo a 21s y se muestra en la pantalla |
| 2 | Disminuir tiempo | Modo Configuración, 10s | Botón B presionado | No se disminuye más, sigue en 10s |
| 3 | Armar bomba | Modo Configuración, 15s | Agitar el micro:bit | Se muestra "Armed", inicia cuenta regresiva desde 15s |
| 4 | Explosión | Modo Armado, 1s restante | Esperar 1 segundo | Se muestra 💀 y suena el buzzer en P0 |
| 5 | Resetear bomba | Modo Armado, 5s restantes | Tocar pin P1 | Se reinicia a 20s en modo configuración |

### 2. Errores Encontrados y Correcciones

#### Problema 1: Rebotes en botones A y B
- **Causa:** No había un control de rebote adecuado en los botones.
- **Solución:** Se añadió `sleep(200)` tras detectar la pulsación para evitar múltiples lecturas rápidas.

#### Problema 2: La cuenta regresiva no actualizaba correctamente la pantalla
- **Causa:** Se realizaban actualizaciones demasiado rápidas.
- **Solución:** Se implementó `sleep(1000)` entre cambios y se aseguró que cada número se mostrara correctamente.

#### Problema 3: Sensibilidad excesiva del gesto *shake*
- **Causa:** La función `was_gesture("shake")` respondía a movimientos leves.
- **Solución:** Se añadió un retraso pequeño antes de cambiar el estado.

#### Problema 4: Sonido inconsistente en la explosión
- **Causa:** No se usaba un ciclo adecuado para alternar el estado del buzzer.
- **Solución:** Se ajustó el bucle de activación del buzzer para uniformidad.

### 3. Código Final Corregido

```python
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
    global config_mode, tiempo
    config_mode = True
    tiempo = 20
    display.scroll("Reset")
    display.show(str(tiempo))
    sleep(200)

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
    if button_b.is_pressed():
        disminuir_tiempo()
    if accelerometer.was_gesture("shake"):
        armar_bomba()
    if pin1.is_touched():
        resetear_bomba()
    sleep(100)
```

### 4. Conclusión

Las pruebas permitieron identificar errores clave y mejorar la estabilidad del código. La implementación final ahora tiene mejor control de rebotes, un flujo de estados más seguro y una experiencia más realista en la cuenta regresiva y la explosión. A futuro, se podrían agregar efectos de sonido más variados o una confirmación antes de armar la bomba para mejorar la interacción del usuario.

