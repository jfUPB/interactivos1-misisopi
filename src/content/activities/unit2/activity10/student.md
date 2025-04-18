# Solución

### Explicación de Concurrencia en el Programa

El programa implementa una máquina de estados finitos en el micro:bit para gestionar la secuencia de imágenes y la respuesta a la pulsación del botón A. La concurrencia en este contexto se maneja mediante la verificación de eventos en un bucle infinito, permitiendo que el programa haga lo siguiente de manera simultánea:

- **Cambio de imágenes basado en el tiempo:** Cada estado tiene un tiempo de duración predefinido, tras el cual transiciona automáticamente al siguiente estado.

- **Interrupción inmediata en respuesta al botón A:** Si el botón A se presiona en cualquier momento, el programa interrumpe la secuencia de estados y transiciona inmediatamente según las reglas establecidas.

- **Evita bloqueos:** La verificación de tiempos y eventos ocurre en cada iteración del bucle sin detenerse, permitiendo que ambas tareas (temporización y respuesta a eventos) se manejen concurrentemente.

Esto permite una interfaz reactiva en la que el usuario puede influir en la secuencia de imágenes en cualquier momento sin esperar que termine un ciclo completo.

### Vectores de Prueba

Para validar el correcto funcionamiento del programa, se han definido los siguientes vectores de prueba:

**Vector de Prueba 1:** Secuencia Normal de Estados

- **Condiciones Iniciales:** El micro:bit está en STATE_HAPPY.

- **Eventos Generados:** Se deja correr el tiempo sin presionar botones.

- **Resultados Esperados:**

1. STATE_HAPPY dura 1.5 segundos, luego cambia a STATE_SMILE.

2. STATE_SMILE dura 1 segundo, luego cambia a STATE_SAD.

3. STATE_SAD dura 2 segundos, luego regresa a STATE_HAPPY.

- **Resultados Obtenidos:** Coinciden con lo esperado. (Prueba pasada)

**Vector de Prueba 2:** Interrupción en STATE_HAPPY

- **Condiciones Iniciales:** El micro:bit está en STATE_HAPPY.

- **Eventos Generados:** Se presiona el botón A.

- **Resultados Esperados:**

1. STATE_HAPPY se interrumpe inmediatamente y cambia a STATE_SAD.

2. STATE_SAD sigue su curso normal por 2 segundos antes de cambiar.

- **Resultados Obtenidos:** Coinciden con lo esperado. (Prueba pasada)

**Vector de Prueba 3:** Interrupción en STATE_SAD

- **Condiciones Iniciales:** El micro:bit está en STATE_SAD.

- **Eventos Generados:** Se presiona el botón A.

- **Resultados Esperados:**

1. STATE_SAD se interrumpe inmediatamente y cambia a STATE_SMILE.

2. STATE_SMILE sigue su curso normal por 1 segundo antes de cambiar.

- **Resultados Obtenidos:** Coinciden con lo esperado. (Prueba pasada)

### Conclusión

El programa implementa correctamente una máquina de estados para gestionar la secuencia de imágenes y responder a eventos del usuario de manera concurrente. Los tres vectores de prueba demuestran que la lógica de transiciones funciona correctamente y que el programa es reactivo a la interacción del usuario sin interrumpir la secuencia de estados de manera inesperada. Esto garantiza una experiencia fluida y predecible en el micro:bit.

