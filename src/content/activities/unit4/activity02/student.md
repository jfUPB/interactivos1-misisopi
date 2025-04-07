# Solución

Este sketch genera un conjunto de líneas onduladas y paralelas que fluyen de manera suave y orgánica sobre el lienzo. Las líneas son curvas que se crean punto a punto con algo de aleatoriedad, pero dentro de un control que las mantiene suaves. Este tipo de técnica es común en el arte generativo para crear patrones naturales o que recuerdan estructuras orgánicas.

---

## Explicación del código por partes

```js
let lines = [];
let noiseScale = 0.005;
let stepSize = 2;
```

**lines:** un arreglo para almacenar las líneas.

**noiseScale:** escala para el ruido Perlin (valores bajos = más suave).

**stepSize:** espacio entre puntos en la dirección horizontal (X).
