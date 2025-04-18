# Solución

### Código

```py
from microbit import *
Import uart

# Inicializar UART para comunicación serial
uart.init(baudrate=115200)

# Variables globales para eventos
evento_ocurrido = False
evento_tipo = ''

def tareaEventos():
    global evento_ocurrido, evento_tipo
    
    # Leer botones del micro:bit
    if button_a.was_pressed():
        evento_ocurrido = True
        evento_tipo = 'A'
    elif button_b.was_pressed():
        evento_ocurrido = True
        evento_tipo = 'B'
    elif accelerometer.was_gesture('shake'):
        evento_ocurrido = True
        evento_tipo = 'S'
    elif pin_logo.is_touched():
        evento_ocurrido = True
        evento_tipo = 'T'
    
    # Leer datos desde el puerto serial
    if uart.any():
        mensaje = uart.read()
        if mensaje:
            mensaje = mensaje.decode().strip()
            if mensaje in ['A', 'B', 'S', 'T']:
                evento_ocurrido = True
                evento_tipo = mensaje

def tareaBomba():
    global evento_ocurrido, evento_tipo
    
    if evento_ocurrido:
        if evento_tipo == 'A':
            display.show("A")
            # Aquí iría la lógica para activar la bomba con botón A
        elif evento_tipo == 'B':
            display.show("B")
            # Aquí iría la lógica para activar la bomba con botón B
        elif evento_tipo == 'S':
            display.show("S")
            # Aquí iría la lógica para activar la bomba con shake
        elif evento_tipo == 'T':
            display.show("T")
            # Aquí iría la lógica para activar la bomba con touch
        
        # Consumir el evento
        evento_ocurrido = False
        sleep(500)
        evento_tipo = ''
    else:
        display.clear()

while True:
    tareaEventos()
    tareaBomba()
```

### Explicación

1. Inicialización del puerto serial:

- Se configura UART con una velocidad de 115200 baudios para recibir datos seriales.

2. Manejo de eventos (tareaEventos):

- Verifica si se ha presionado un botón físico en el micro:bit (A, B, shake o touch).
- Si se recibe un mensaje válido por el puerto serial, se almacena en la variable evento_tipo.
- Se establece evento_ocurrido = True cuando un evento es detectado.

3. Máquina de estados de la bomba (tareaBomba):

- Si hay un evento pendiente (evento_ocurrido = True), se muestra en el display y se ejecuta la acción correspondiente.
- Después de procesar el evento, se resetean las variables (evento_ocurrido = False y evento_tipo = ''), asegurando que el evento sea consumido correctamente.
  
4. Bucle principal (while True):

- Llama a tareaEventos() para capturar eventos.
- Llama a tareaBomba() para procesar los eventos capturados.
- Se usa sleep(100) para evitar que el código se ejecute demasiado rápido y mejorar eficiencia.

