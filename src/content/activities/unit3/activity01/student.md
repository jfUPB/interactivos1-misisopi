# Solución

```py
from microbit import *

class Semaforo:
    def __init__(self, rojo, amarillo, verde, columna):
        self.tiempos = [rojo, amarillo, verde]  # Duraciones de los estados
        self.estado = 0  # 0 = Rojo, 1 = Amarillo, 2 = Verde
        self.tiempo_restante = self.tiempos[self.estado]
        self.columna = columna  # Columna del semáforo en el display

    def update(self):
        self.tiempo_restante -= 1
        if self.tiempo_restante == 0:
            self.estado = (self.estado + 1) % 3  # Cambia de estado ciclicamente
            self.tiempo_restante = self.tiempos[self.estado]
        self.mostrar()
    
    def mostrar(self):
        colores = [9, 5, 1]  # Intensidades de LED para Rojo, Amarillo y Verde
        for fila in range(3):
            display.set_pixel(self.columna, fila, 0)  # Borra la columna actual
        display.set_pixel(self.columna, self.estado, colores[self.estado])  # Muestra el estado actual

# Crear los semáforos en diferentes columnas del display
semaforo1 = Semaforo(5, 2, 3, 0)
semaforo2 = Semaforo(3, 1, 2, 2)
semaforo3 = Semaforo(4, 3, 2, 4)

while True:
    semaforo1.update()
    semaforo2.update()
    semaforo3.update()
    sleep(1000)  # Espera 1 segundo por iteración
```
### Ventajas de usar una clase para representar un semáforo

El uso de una clase (`class`) en la implementación de los semáforos tiene varias ventajas clave:

1. **Modularidad y reutilización:**
   - Cada semáforo se define como una instancia de la clase `Semaforo`, lo que permite crear múltiples semáforos sin duplicar código.
   - Se puede reutilizar la clase en otros proyectos con facilidad.

2. **Facilidad de mantenimiento:**
   - Si se necesita cambiar la lógica del semáforo, solo se modifica la clase sin afectar otras partes del código.
   - La encapsulación de los atributos y métodos hace que el código sea más organizado y fácil de entender.

3. **Escalabilidad:**
   - Si se requiere agregar más semáforos, simplemente se crean nuevas instancias sin afectar la estructura principal del programa.

4. **Separación de responsabilidades:**
   - La clase maneja su propio comportamiento (cambio de estados, actualización de tiempos y visualización en el display).
   - El bucle principal solo se encarga de llamar a `update()` en cada semáforo.

### Máquinas de estado en programación
El programa utiliza el enfoque de **máquinas de estado finito (FSM - Finite State Machine)** para manejar el ciclo de los semáforos:

1. **Estados definidos:** Cada semáforo tiene tres estados (`rojo`, `amarillo`, `verde`).
2. **Transiciones controladas:** El semáforo cambia de estado después de un tiempo determinado.
3. **Ejecución en bucle:** Se actualizan los estados en cada iteración del bucle principal.

Este enfoque permite que cada semáforo funcione de manera independiente, garantizando que los tiempos de cada uno se manejen de forma concurrente y sincronizada sin interferencias.



