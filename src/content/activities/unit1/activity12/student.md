# Solución 

#### Para el micro:bit python
```py
from microbit import *

# Diccionario con imágenes predefinidas
images = {
    '1': Image.HEART,
    '2': Image.HAPPY,
    '3': Image.SAD,
    '4': Image.SQUARE
}

while True:
    if uart.any():  # Si hay datos en el puerto serial
        data = uart.read(1).decode('utf-8')  # Leer el dato y decodificarlo
        if data in images:
            display.show(images[data])  # Mostrar la imagen correspondiente
```
#### Para el p5.js editor

```js
let port;
let connectBtn;

function setup() {
    createCanvas(400, 200);
    background(220);

    port = createSerial(); // Inicializar puerto serial

    // Botón para conectar el micro:bit
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(20, 150);
    connectBtn.mousePressed(connectBtnClick);

    // Botones para seleccionar imágenes
    let img1Btn = createButton('Imagen 1');
    img1Btn.position(20, 50);
    img1Btn.mousePressed(() => sendCommand('1'));

    let img2Btn = createButton('Imagen 2');
    img2Btn.position(100, 50);
    img2Btn.mousePressed(() => sendCommand('2'));

    let img3Btn = createButton('Imagen 3');
    img3Btn.position(180, 50);
    img3Btn.mousePressed(() => sendCommand('3'));

    let img4Btn = createButton('Imagen 4');
    img4Btn.position(260, 50);
    img4Btn.mousePressed(() => sendCommand('4'));
}

function sendCommand(command) {
    if (port.opened()) {
        port.write(command); // Enviar el número de la imagen al micro:bit
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200); // Conectar al micro:bit
    } else {
        port.close();
    }
}
```

### Interfaz en p5.js

- Se crean botones para seleccionar cada imagen.
- Cada botón envía un número ('1', '2', '3', '4') al micro:bit mediante serial.
- La función sendCommand(command) envía el dato cuando se presiona un botón.
  
### Recepción en micro:bit

- El micro:bit espera recibir datos del puerto serial.
- Cuando llega un número ('1', '2', '3', '4'), el programa busca la imagen en el diccionario images.
- La imagen correspondiente se muestra en la matriz LED del micro:bit.

#### Cambios experimentales en el micro:bit python

```py
from microbit import *

# Diccionario con imágenes predefinidas
images = {
    '1': Image.HEART,
    '2': Image.HAPPY,
    '3': Image.SAD,
    '4': Image.SQUARE
}

while True:
    if button_a.is_pressed():
        display.show(images['1']) # muestra la imagen 1 presionando el botón A
    if button_b.is_pressed():
        display.show(images['2']) # muestra la imagen 1 presionando el botón A
    if uart.any():  # Si hay datos en el puerto serial
        #data = uart.read(1).decode('utf-8')  // Leer el dato y decodificarlo, este se cita para experimentar
        data = uart.read(1) # lee el dato
        if data:
            data = data.decode('utf-8') # decodifica el dato
        if data in images: 
            display.show(images[str(data)])  # Mostrar la imagen correspondiente, pero la convierte de nuevo en cadena
```
