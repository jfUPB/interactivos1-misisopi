# Solución
```js
let estadoActual = "rojo";  // Estado inicial del semáforo
let tiempoInicio = 0;       // Tiempo de inicio
let duracionRojo = 3000;    // Duración del rojo en milisegundos (3 segundos)
let duracionAmarillo = 1000; // Duración del amarillo en milisegundos (1 segundo)
let duracionVerde = 2000;   // Duración del verde en milisegundos (2 segundos)

function setup() {
  createCanvas(400, 400);  // Creamos una ventana de 400x400 píxeles
  tiempoInicio = millis();  // Guardamos el tiempo inicial
}

function draw() {
  background(0);  // Limpiamos el fondo en cada frame
  
  // Dependiendo del estado actual, dibujamos el semáforo
  if (estadoActual === "rojo") {
    mostrarSemaforo("rojo");
    if (millis() - tiempoInicio > duracionRojo) {
      estadoActual = "amarillo";
      tiempoInicio = millis();  // Reiniciamos el tiempo al cambiar de estado
    }
  } else if (estadoActual === "amarillo") {
    mostrarSemaforo("amarillo");
    if (millis() - tiempoInicio > duracionAmarillo) {
      estadoActual = "verde";
      tiempoInicio = millis();  // Reiniciamos el tiempo al cambiar de estado
    }
  } else if (estadoActual === "verde") {
    mostrarSemaforo("verde");
    if (millis() - tiempoInicio > duracionVerde) {
      estadoActual = "rojo";
      tiempoInicio = millis();  // Reiniciamos el tiempo al cambiar de estado
    }
  }
}

// Función que dibuja el semáforo con el color correspondiente
function mostrarSemaforo(estado) {
  let x = width / 2; // Posición X central
  let y = height / 3; // Posición Y central para el primer círculo

  // Dibujamos los tres círculos del semáforo
  fill(255); // Blanco para el borde de los círculos
  ellipse(x, y, 100, 100);         // Círculo para el rojo
  ellipse(x, y + 120, 100, 100);   // Círculo para el amarillo
  ellipse(x, y + 240, 100, 100);   // Círculo para el verde

  // Colocamos los colores dentro de cada círculo
  if (estado === "rojo") {
    fill(255, 0, 0);  // Rojo
    ellipse(x, y, 100, 100);  // Círculo rojo
  } else if (estado === "amarillo") {
    fill(255, 255, 0); // Amarillo
    ellipse(x, y + 120, 100, 100);  // Círculo amarillo
  } else if (estado === "verde") {
    fill(0, 255, 0);   // Verde
    ellipse(x, y + 240, 100, 100);  // Círculo verde
  }
}
```

|      Estado      |    Evento       | acción          |
|------------------|-----------------|-----------------|
|    Rojo   | Tiempo transcurrido > duración de Rojo (3 segundo) | Mostrar el semáforo con el círculo rojo iluminado. Cambiar a Amarillo después de 3 segundos.|
|  Amarillo |	Tiempo transcurrido > duración de Amarillo (1 segundo)|Mostrar el semáforo con el círculo amarillo iluminado. Cambiar a Verde después de 1 segundo.|
|   Verde   | Tiempo transcurrido > duración de Verde (2 segundos) | Mostrar el semáforo con el círculo verde iluminado. Cambiar a Rojo después de 2 segundos. |

### Estados:

Un estado es una situación particular en la que se encuentra el semáforo en un momento dado, dependiendo de la fase del ciclo del semáforo. Los tres estados que hemos definido son:

- **Rojo:** El semáforo está en rojo y los vehículos deben detenerse.
- **Amarillo:** El semáforo está en amarillo, lo que indica que los vehículos deben prepararse para detenerse o para avanzar.
- **Verde:** El semáforo está en verde y los vehículos pueden avanzar.

### Eventos:

Un evento es una condición o suceso que evalúa el programa y que puede hacer que el sistema cambie de estado o realice una acción. En este caso, el evento principal que se evalúa es el tiempo transcurrido, el cual determina cuándo se debe cambiar de estado.

- **Evento en el estado Rojo:** Cuando ha pasado el tiempo de duración del rojo (por ejemplo, 3 segundos), el semáforo cambia al estado amarillo.
- **Evento en el estado Amarillo:** Cuando ha pasado el tiempo de duración del amarillo (por ejemplo, 1 segundo), el semáforo cambia al estado verde.
- **Evento en el estado Verde:** Cuando ha pasado el tiempo de duración del verde (por ejemplo, 2 segundos), el semáforo cambia al estado rojo.

### Acciones:

Las acciones son las actividades que el programa realiza cuando ocurre un evento en un estado. En este caso, las acciones están relacionadas con:

- Mostrar el color correspondiente en la pantalla del semáforo (rojo, amarillo o verde).
- Cambiar el estado después de que haya pasado el tiempo adecuado en cada color.
