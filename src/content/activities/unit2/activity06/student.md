# Solución

```py
# Mostrar un corazón
display.show(Image.HEART)
sleep(1000)  # Mantener la imagen durante 1 segundo

# Mostrar texto "Hola"
display.scroll("Hola")
sleep(1000)  # Esperar 1 segundo antes de cambiar a la siguiente imagen

# Mostrar una carita feliz
display.show(Image.HAPPY)
sleep(1000)  # Mantener la imagen durante 1 segundo

# Mostrar texto "Fin"
display.scroll("Fin")
```

### Explicación del funcionamiento:

#### 1. Mostrar una imagen de corazón (Image.HEART):

display.show(Image.HEART) utiliza una de las imágenes predefinidas en la librería de MicroPython para la pantalla LED. El corazón es una de las imágenes disponibles y se muestra en la pantalla.
La función sleep(1000) hace que la imagen se mantenga visible durante 1 segundo antes de cambiar a la siguiente.

#### 2. Mostrar texto "Hola":

display.scroll("Hola") hace que el texto "Hola" se desplace de derecha a izquierda en la pantalla del micro:bit. Esta función se utiliza para mostrar cadenas de texto de forma dinámica.
Después de mostrar el texto, se espera un segundo con sleep(1000) antes de cambiar a la siguiente imagen.

#### 3. Mostrar una carita feliz (Image.HAPPY):

display.show(Image.HAPPY) muestra una imagen de una carita feliz en la pantalla LED del micro:bit. Esta es otra de las imágenes predefinidas disponibles en MicroPython.
Al igual que antes, la imagen se mantiene visible durante 1 segundo con sleep(1000).

#### 4. Mostrar texto "Fin":

Al igual que con el texto "Hola", display.scroll("Fin") hará que el texto "Fin" se desplace de derecha a izquierda en la pantalla del micro:bit.

#### Resumen de las imágenes y textos:
- Imagen 1: Corazón (Image.HEART)
- Texto 1: "Hola" (desplazado)
- Imagen 2: Carita feliz (Image.HAPPY)
- Texto 2: "Fin" (desplazado)
