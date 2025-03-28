# Solución

```py
from microbit import *
import music

# Sonido 1: Nota de 440 Hz (La4)
def sonido1():
    music.pitch(440, 500)  # 440 Hz durante 500 ms

# Sonido 2: Nota de 880 Hz (La5)
def sonido2():
    music.pitch(880, 500)  # 880 Hz durante 500 ms

while True:
    if button_a.is_pressed():  # Si se presiona el botón A
        sonido1()  # Reproduce el sonido 1
        display.show("A")  # Muestra "A" en la pantalla
    elif button_b.is_pressed():  # Si se presiona el botón B
        sonido2()  # Reproduce el sonido 2
        display.show("B")  # Muestra "B" en la pantalla
    else:
        display.clear()  # Limpia la pantalla
```
### Descripción del código:

#### Funciones de sonido:

- **sonido1():** Utiliza la función music.pitch() para generar una frecuencia de 440 Hz durante 500 milisegundos. La frecuencia de 440 Hz corresponde a la nota La4 (A4).
- **sonido2():** Similar al primero, pero genera una frecuencia de 880 Hz (nota La5, A5).

#### Bucle principal:

- Si se presiona el botón A, se llama a la función sonido1() para generar un sonido de 440 Hz y muestra la letra "A" en la pantalla del Micro:bit.
- Si se presiona el botón B, se llama a la función sonido2() para generar un sonido de 880 Hz y muestra la letra "B".
- Si no se presionan los botones, la pantalla se limpia.
### Explicación del proceso:

- El Micro:bit tiene la capacidad de generar tonos mediante la función music.pitch(). Esta función permite especificar la frecuencia del sonido (en Hz) y la duración (en milisegundos).

- Usamos los botones A y B del Micro:bit para interactuar con el código. Dependiendo del botón presionado, se genera un sonido diferente, lo que permite experimentar con dos frecuencias distintas.

- La pantalla del Micro:bit se utiliza para mostrar qué botón ha sido presionado, proporcionando retroalimentación visual al usuario.
