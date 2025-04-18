# Solución
```js
let port;
let connectBtn;
let xPos = 200; // Posición inicial del círculo

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial(); // Inicializar puerto serial

    // Botón para conectar el micro:bit
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 350);
    connectBtn.mousePressed(connectBtnClick);
}

function draw() {
    background(220);

    // Dibujar el círculo en la posición x actual
    fill('blue');
    ellipse(xPos, height / 2, 50, 50);

    // Verificar si hay datos disponibles en el puerto serial
    if (port.availableBytes() > 0) {
        let dataRx = port.read(1); // Leer un carácter desde el micro:bit

        // Mover el círculo según la entrada
        if (dataRx == 'A') {
            xPos -= 10; // Mueve a la izquierda
        } else if (dataRx == 'B') {
            xPos += 10; // Mueve a la derecha
        }

        // Limitar el movimiento dentro del canvas
        xPos = constrain(xPos, 25, width - 25);
    }

    // Actualizar el botón de conexión
    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    } else {
        connectBtn.html('Disconnect');
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200); // Conexión serial con el micro:bit
    } else {
        port.close();
    }
}
```

### 1. Detección de botones en el micro:bit

- Cuando se presiona el botón A, se envía el carácter 'A' por el puerto serial.
  
- Cuando se presiona el botón B, se envía el carácter 'B'.

### 2. Recepción de datos en p5.js

- En la función draw(), se revisa si hay datos disponibles en el puerto serial.

- Si se recibe 'A', la variable xPos disminuye en 10 unidades (moviendo el círculo a la izquierda).

- Si se recibe 'B', xPos aumenta en 10 unidades (moviendo el círculo a la derecha).

### 3. Limitación del movimiento

- Se usa constrain(xPos, 25, width - 25); para evitar que el círculo salga del canvas.
