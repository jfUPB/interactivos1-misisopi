# Solución

### Código
```py
from microbit import *
import utime

class Pixel:
    def __init__(self,pixelX,pixelY,initState,interval):
        self.state = "Init"
        self.startTime = 0
        self.interval = interval
        self.pixelX = pixelX
        self.pixelY = pixelY
        self.pixelState = initState

    def update(self):

        if self.state == "Init":
            self.startTime = utime.ticks_ms()
            self.state = "WaitTimeout"
            display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

        elif self.state == "WaitTimeout":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                if self.pixelState == 9:
                    self.pixelState = 0
                else:
                    self.pixelState = 9
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

pixel1 = Pixel(0,0,0,1000)
pixel2 = Pixel(4,4,0,500)

while True:
    pixel1.update()
    pixel2.update()
```

### Análisis del código:

#### Clase Pixel:

La clase Pixel modela a un píxel en la pantalla del Micro:bit con las siguientes características:

#### Atributos:

- **state:** Representa el estado actual del píxel. Se inicializa con "Init", lo que indica que el píxel comienza en un estado de inicialización.
- **startTime:** Almacena el tiempo de inicio de un estado. Se usa para medir el intervalo de tiempo entre los cambios de estado.
- **interval:** El intervalo de tiempo en milisegundos entre los cambios de estado de encendido y apagado del píxel.
- **pixelX, pixelY:** Las coordenadas del píxel en la pantalla del Micro:bit.
- **pixelState:** El estado del píxel, que puede ser 0 (apagado) o 9 (encendido).
- **Método update():** Este es el principal encargado de cambiar el estado del píxel. En este método, se manejan los estados, eventos y acciones.

#### Estados:

Un estado representa una fase en la que el programa se encuentra en un momento dado. En este código se identifican dos estados principales dentro del método update():

**Estado "Init":**

- Es el estado inicial. El píxel comienza en este estado.
- **Acción:** Se registra el tiempo de inicio (self.startTime = utime.ticks_ms()) y el estado se cambia a "WaitTimeout". Además, se establece el valor del píxel en la pantalla con display.set_pixel(self.pixelX, self.pixelY, self.pixelState).

**Estado "WaitTimeout":**

En este estado, el programa espera a que haya transcurrido el intervalo de tiempo especificado para alternar el estado del píxel.

- **Evento:** La condición que desencadena el cambio de estado es el tiempo transcurrido. El programa compara el tiempo actual con self.startTime usando utime.ticks_diff(). Si el tiempo transcurrido es mayor que el intervalo (self.interval), se cambia el estado del píxel.
- **Acción:** Si el píxel está apagado (pixelState == 9), se cambia el estado a encendido (pixelState = 0). Si está encendido, se apaga (pixelState = 9). Luego, se actualiza el estado del píxel en la pantalla con display.set_pixel(self.pixelX, self.pixelY, self.pixelState).

#### Eventos:

Un evento es algo que ocurre en el programa y que puede cambiar su flujo de ejecución o su estado. En este programa, el evento es:

- **Tiempo de espera transcurrido:** El evento que provoca el cambio de estado es el tiempo que ha pasado desde el último cambio de estado. Cuando el tiempo transcurrido (utime.ticks_diff(utime.ticks_ms(), self.startTime)) supera el intervalo de espera (self.interval), el programa pasa del estado "WaitTimeout" al siguiente ciclo, lo que provoca la alternancia entre encendido y apagado del píxel.

#### Acciones:

Las acciones son las cosas que el programa hace en respuesta a un evento. En este caso:

**Acción cuando el estado es "Init":**

- Se guarda el tiempo de inicio (self.startTime = utime.ticks_ms()).
- Se establece el estado del píxel en la pantalla con display.set_pixel(self.pixelX, self.pixelY, self.pixelState).
- 

**Acción cuando el estado es "WaitTimeout":**

- Se evalúa si el tiempo ha transcurrido más de lo que se definió en el interval.
- Si es así, se alterna el estado del píxel entre apagado (0) y encendido (9).
- Luego, se actualiza el estado en la pantalla con display.set_pixel(self.pixelX, self.pixelY, self.pixelState).
- 
#### Cómo funciona el código:

- **Inicialización:** Dos objetos Pixel son creados: uno en la posición (0, 0) con un intervalo de 1000 ms (1 segundo), y otro en la posición (4, 4) con un intervalo de 500 ms (0.5 segundos).

- **Bucle principal:** El bucle while True ejecuta de manera continua el método update() de ambos píxeles. Esto hace que los píxeles alternen entre encendido y apagado a sus respectivos intervalos.

### ¿Puedes identificar algún estado? 

Sí, el código tiene dos estados claramente definidos:

- **"Init":** El estado inicial donde se inicia el temporizador y se muestra el estado inicial del píxel en la pantalla.
- **"WaitTimeout":** El estado de espera donde el programa mide el tiempo transcurrido y espera a que se alcance el intervalo antes de alternar el estado del píxel (encendido/apagado).

### ¿Puedes identificar algún evento?

El evento principal en este programa es el paso del tiempo. El evento que causa la transición entre estados es cuando el tiempo transcurrido (utime.ticks_diff()) excede el intervalo definido (self.interval).

### ¿Puedes identificar alguna acción?

Sí, las acciones que se ejecutan en respuesta al evento del paso del tiempo son:

- **En el estado "Init":** El tiempo se guarda y el píxel se muestra con su estado inicial.
- **En el estado "WaitTimeout":** Se alterna el estado del píxel entre encendido (9) y apagado (0), y se actualiza la pantalla del Micro:bit para reflejar este cambio.

