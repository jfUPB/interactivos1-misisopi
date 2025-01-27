## Mi solución a la actividad 

#### ¿Qué pasa cuando presionas el botón A y B?

Cuando presionas los botones A o B del micro:bit, este envía un mensaje **A** o **B** al programa en el computador a través de la conexión USB serial. En el entorno p5.js, este mensaje es recibido por el programa y se interpreta para cambiar el color del círculo en la pantalla. Si se presiona el botón A, el círculo se colorea de rojo; si se presiona el botón B, se colorea de amarillo. En este proceso:   

- El micro:bit detecta la presión de los botones usando button_a.is_pressed() o button_b.is_pressed().
- Envía el carácter correspondiente ("A" o "B") al puerto serial mediante uart.write().
- En el código de p5.js, el evento de recepción (port.read(1)) interpreta este mensaje y ajusta el colo  r del círculo según el dato recibido.
``` py
while True: 
    if button_a.is_pressed():
        uart.write('A')
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')
        sleep(500)
```

``` py
function draw() {

    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
        if(dataRx == 'A'){
            fill('red');
        }
        else if(dataRx == 'B'){
            fill('yellow');
        }
```
#### Sacude el micro:bit. ¿Qué pasa?

Cuando sacudes el micro:bit, este detecta el gesto de "shake" con su acelerómetro integrado. Esto provoca que el micro:bit envíe un mensaje ("C") al programa en el computador. En p5.js, al recibir "C", el círculo cambia de color a verde. Se logra cuando:

- El micro:bit usa accelerometer.was_gesture('shake') para identificar el gesto.
- Envía el carácter "C" al puerto serial usando uart.write().
- En p5.js, el dato "C" recibido por port.read(1) cambia el color del círculo a verde mediante un condicional.

``` py
 if accelerometer.was_gesture('shake'):
        uart.write('C')
        sleep(500)
```
 ``` py
else{
            fill('green');
        }
```

#### Presionar el botón Send Love. ¿Qué pasa?

Cuando presionas el botón "Send Love" en la interfaz de p5.js, el programa envía un mensaje ("h") al micro:bit a través del puerto serial. Al recibir este mensaje, el micro:bit muestra una animación en su pantalla: primero un corazón y luego una cara feliz. Se logra cuando:

- El botón "Send Love" ejecuta la función sendBtnClick() que usa port.write('h') para enviar el mensaje "h" al micro:bit.
- En el micro:bit, el código detecta el mensaje recibido mediante uart.read(1) y verifica si es "h".
- Si lo es, ejecuta las instrucciones para mostrar las imágenes de un corazón (Image.HEART) seguido de una cara feliz (Image.HAPPY) en la pantalla LED del micro:bit.

``` py
 if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('h'):
                display.show(Image.HEART)
                sleep(500)
                display.show(Image.HAPPY)
```
``` py
 let sendBtn = createButton('Send Love');
    sendBtn.position(220, 300);
    sendBtn.mousePressed(sendBtnClick);
    fill('white');
    ellipse(width / 2, height / 2, 100, 100);
```

``` py

function sendBtnClick() {
    port.write('h');
}

```
