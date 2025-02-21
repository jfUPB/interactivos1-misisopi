# Solución

![image](https://github.com/user-attachments/assets/f28a01d4-978d-4734-8133-5496242292a1)

### Descripción de la Lógica:

##### En el Modo de Configuración:

- Si se presiona el botón UP, el tiempo de la cuenta regresiva aumenta en 1 segundo, sin exceder los 60 segundos.
- Si se presiona el botón DOWN, el tiempo disminuye en 1 segundo, sin bajar de los 10 segundos.
- Al presionar el botón Touch, el sistema regresa a la configuración inicial sin iniciar la cuenta regresiva.
- Si se detecta un ARMED (shake), la bomba se arma y comienza la cuenta regresiva.
  
##### En el Modo Armado:

- El temporizador comienza a contar hacia atrás.
- El tiempo restante se muestra en la pantalla de LEDs.
- Si el tiempo llega a 0, el sistema activa el speaker para simular la explosión.
- La bomba se desactiva y regresa al Modo de Configuración.
- Cuando el temporizador llegue a cero, el sistema activará el speaker para simular la explosión y luego volverá automáticamente al Modo de Configuración.

![image](https://github.com/user-attachments/assets/df4952f0-f5b0-4990-8e4d-562383153a6b)


