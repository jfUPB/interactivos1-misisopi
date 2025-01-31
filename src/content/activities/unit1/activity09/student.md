# Solución

```js
function setup() {
  createCanvas(600, 600);
  noLoop(); // Para que el patrón se genere una sola vez
}

function draw() {
  background(0);
  noFill();
  
  let cols = 20; // Número de columnas
  let rows = 20; // Número de filas
  let spacing = width / cols; // Espaciado entre las líneas
  
  for (let y = 0; y < height; y += spacing) {
    for (let x = 0; x < width; x += spacing) {
      let size = random(10, 40); // Tamaño aleatorio de cada figura
      let angle = noise(x * 0.01, y * 0.01) * TWO_PI; // Variación con ruido
      let offsetX = cos(angle) * size;
      let offsetY = sin(angle) * size;
      
      stroke(random(100, 255), random(100, 255), random(255)); // Color aleatorio
      strokeWeight(random(1, 4));
      ellipse(x + offsetX, y + offsetY, size, size);
    }
  }
}
```
### Funciones utilizadas:

- random(min, max): Genera valores aleatorios para el tamaño de las figuras y el color.
  
- sin() y cos(): Se usan para modificar la posición de los elementos con un ángulo aleatorio basado en noise(), creando variaciones suaves.
  
- noise(x, y): Genera valores aleatorios pero con continuidad, evitando cambios bruscos en los patrones.
  
- stroke(r, g, b): Aplica colores aleatorios en cada figura.
  
- noLoop(): Evita que draw() se ejecute continuamente, manteniendo el mismo patrón hasta que se recargue la página.

### Modificación de parámetros:

- Aumentando cols y rows se obtienen patrones más densos.
  
- Variando strokeWeight() los contornos pueden ser más delgados o gruesos.
  
- Ajustando la escala de noise() se pueden generar patrones más caóticos o suaves.
  
- Modificando size, las figuras pueden ser más grandes o pequeñas según la estética deseada.

  
