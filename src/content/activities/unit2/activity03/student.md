# Solución

### Dispositivos de entrada del micro:bit

- **Botón A:** Es un botón físico que permite recibir una entrada de usuario. Se utiliza para activar eventos o cambiar estados.

- **Botón B:** Similar al botón A, permite la interacción con el usuario. Se usa comúnmente para realizar una acción alternativa o como un control secundario.

- **Entrada de sensores:** Permite captar el movimiento y la orientación del micro:bit. Esto puede ser útil en juegos o sistemas que dependan del movimiento (como el acelerómetro).

- **Entrada de pines (P0, P1, P2):** Los pines de entrada pueden recibir señales de voltaje o ser usados para leer datos de otros dispositivos conectados al micro:bit.

### Salidas del micro:bit:

- **Pantalla LED (5x5):** El micro:bit tiene una pantalla LED de 5x5 píxeles que puede mostrar textos, números y patrones gráficos.

- **Buzzer o altavoz:** Se utiliza para emitir sonidos o tonos. Se conecta a uno de los pines (por ejemplo, P0) para generar alertas o efectos sonoros.

- **Pines de Salida (P0, P1, P2):** Los pines también pueden ser configurados para enviar señales de salida, como encender un LED externo o activar otros dispositivos.

- **Conexión Bluetooth:** Aunque no es una salida física directa, el micro:bit tiene la capacidad de enviar datos a través de Bluetooth a otros dispositivos.

### Funciones de micropython para entradas:

- button_a.is_pressed(): Detecta si el botón A está presionado.

```py
while True:
    if button_a.is_pressed():
        display.show('A')
```
- accelerometer.get_x(), get_y(), get_z(): Estos métodos leen los valores de aceleración en los ejes X, Y y Z, permitiendo detectar la orientación y el movimiento del micro:bit.

```py
while True:
    x = accelerometer.get_x()
    y = accelerometer.get_y()
    z = accelerometer.get_z()
    display.show(str(x))
```

- pin0.read_digital(): Lee una señal digital de un pin de entrada (por ejemplo, P0) y devuelve True si la señal es alta, o False si es baja.


```py
while True:
    if pin0.read_digital():
        display.show('1')
    else:
        display.show('0')
```

### Funciones de micropython para salidas:

- display.show(): Muestra un texto o una imagen en la pantalla LED del micro:bit.

```py
Copiar
from microbit import *
display.show("Hello")
```
- pin0.write_digital(): Envía una señal digital de salida a un pin específico. Por ejemplo, para encender un LED conectado al pin P0.

```py
pin0.write_digital(1)  # Enciende el LED
```
- music.play(): Utiliza el buzzer para reproducir sonidos. Permite emitir tonos a través del altavoz.

```py
import music
music.play(music.PYTHON)
```
