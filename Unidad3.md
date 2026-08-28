# Bitácora del Instrumento Visual · LesAlpx

---

## 1. El Mapa del Sistema Pro

El proyecto está armado usando **Three.js** con WebGPU y TSL para tirar simulaciones masivas en la GPU sin que explote la PC:

* **El Estado:** Los datos viven en buffers paralelos en la GPU. `positionBuffer` y `velocityBuffer` guardan las coordenadas y vectores de las 131,072 partículas (`createSimulation.js`).
* **Las Fuerzas:** El cálculo se hace con funciones matemáticas y ruido procedimental. Trae Curl Noise y 5 estados controlados por el parámetro `modeState` (`createSimulation.js`).
* **La Integración:** Se actualiza por fotograma usando el tiempo (`dt`), sumando las fuerzas, aplicando fricción (`v.mul(0.93)`) para que no pegue saltos feos, y poniendo un límite de velocidad (`maxSpeed`) (`createSimulation.js`).
* **El Render:** Dibuja 131,072 instancias con `InstancedMesh` y sprites, cambiando el color dinámicamente según la velocidad (`createSimulation.js`).
* **Controles y Archivos:** 
  * `main.js`: El jefe supremo que orquesta todo.
  * `createSimulation.js`: El cerebro de la física en la GPU.
  * `parameters.js`: Las variables globales (`modeState`, `timeScale`, etc.).
  * `labPanel.js`: El panel flotante y el teclado (**Y, U, I, O, T**) para modificaciones en vivo.

---

## 2. Ficha de las Fuerzas

* **Las Ecuaciones:** 
  * *Estado 0 (Deriva Cósmica):* $F = \text{CurlNoise}(p) \times 1.5$. Mueve las partículas como polvo estelar.
  * *Estado 1 (Imán Cuántico):* $F = \text{dirToCenter} \times (\text{dist} \times 2.5) + \text{Vórtice}$. Una succión en espiral hacia el centro $(0,0,0)$.
  * *Estado 2 (Hiper-Explosión Supernova):* $F = \frac{\text{outward}}{\text{max}(dist, 0.1)} \times 15.0$. Repulsión masiva que manda todo a volar a los bordes.
  * *Estado 3 (Tormenta Geométrica):* $F = \sin(y) \cdot \cos(z) \cdot \sin(x) \times 6.0$. Ondas trigonométricas cruzadas.
  * *Estado 4 (Ciclón Extremo):* $F = \text{VórticeVertical} - (y \times 1.5)$. Giro estilo remolino.
* **Parámetros clave:** `params.modeState`, `params.uTurbulence`, `params.timeScale` y `params.maxSpeed`.
* **La Predicción:** Al pasar de la deriva al modo supernova (Estado 2), las partículas deben salir disparadas del centro al instante y ponerse fucsias por la velocidad.
* **Diseño:** Se usó fricción constante (`0.93`) para que los cambios de estado con el teclado no sean un reseteo brusco, sino una transición bien fluida.

---

## 3. El Registro de Pruebas

### Las cinco pruebas de ley
1. **Prueba de Inicialización:** Ver que la esfera de partículas nazca bien al arrancar (`reset`). *Resultado: Éxito total.* <img width="1919" height="1199" alt="image" src="https://github.com/user-attachments/assets/9141d6f3-f794-43c9-8e57-b31717ec4012" />

2. **Prueba de Límites:** Chequear que atraviesen los bordes y reaparezcan con el módulo. *Resultado: Flujo continuo.* <img width="1919" height="1199" alt="image" src="https://github.com/user-attachments/assets/705aafeb-3451-463e-8d5c-1432f08dd829" />

3. **Prueba de Turbulencia:** Mover el slider del ruido. *Resultado: Más dinamismo local.* <img width="1898" height="1066" alt="image" src="https://github.com/user-attachments/assets/b4872f5f-b043-4428-bc7b-81d0964b50fa" />

4. **Prueba de Color por Velocidad:** Validar que pasen de cian a fucsia. *Resultado: Retroalimentación visual adecuada.* <img width="1919" height="1199" alt="image" src="https://github.com/user-attachments/assets/1af8a654-0709-4d61-afdb-0881c64c9d50" />

5. **Prueba del Modo Performance:** Ocultar el panel con la `P`. *Resultado: Pantalla limpia a más de 60 FPS.* <img width="1919" height="1199" alt="image" src="https://github.com/user-attachments/assets/7cf5aad3-f78d-4a54-98cb-64699bf4d8e8" />


### La prueba de fuego (Combinación central)
* **Qué se hizo:** Una secuencia rítmica dándole a las teclas (**Y** $\rightarrow$ **U** $\rightarrow$ **I** $\rightarrow$ **T**) simulando los drops de *LesAlpx*.
* **Hipótesis:** El sistema iba a aguantar la acumulación de energía sin congelarse.
* **Resultado:** Todo bien. Las ecuaciones mutaron en el siguiente ciclo de la GPU sin crashear el navegador y la tecla `T` salvó la patria al no chocar con la `P` (esto pasó por un prompt que se envió a la IA).

---

## 4. El Score Visual

* **Tramo 1 (Intro tranqui):** **Estado 0 [Y] (Deriva Cósmica)**. Para ambientar de chill mientras arranca la pista. <img width="1919" height="1199" alt="image" src="https://github.com/user-attachments/assets/045b3be7-4ac5-442d-a52b-b8c1fec9f893" />

* **Tramo 2 (La tensión):** **Estado 1 [U] (Imán Cuántico)**. Un remolino para concentrar la mirada al centro. <img width="1919" height="1199" alt="image" src="https://github.com/user-attachments/assets/b6705087-8bda-4e1c-9065-91a4d994742e" />

* **Tramo 3 (El Drop / Clímax):** **Estado 2 [I] (Hiper-Explosión Supernova)**. El golpazo visual que revienta la pantalla. <img width="1408" height="938" alt="image" src="https://github.com/user-attachments/assets/22578215-0a65-4e64-a6d9-0cf46c2937f1" />

* **Tramo 4 (El cierre épico):** **Estado 3 [O] o Estado 4 [T] (Tormenta / Ciclón)**. Texturas y giros salvajes para la recta final de *LesAlpx*. <img width="1124" height="667" alt="image" src="https://github.com/user-attachments/assets/3bc23a42-d380-4881-83a6-51b55fcca721" />
<img width="1804" height="973" alt="image" src="https://github.com/user-attachments/assets/bf9ef249-32f2-4794-86fc-ab495125ec1d" />


---

## 5. La Bitácora de la IA

* **Lo que se pidió:** Arreglar los bugs de `parameters.js`, meter estados dinámicos en la GPU y acomodar las letras del teclado (`Y, U, I, O, T`) liberando la `P`.
* **Cambios aceptados:** Estructuras condicionales en TSL, nuevos uniformes y el listener de eventos en `labPanel.js`.
* **Correcciones hechas:** Ajuste de la fuerza de las explosiones para que las partículas no se perdieran en el infinito, y validación de que los inputs de texto no activaran comandos por error.
* **Lo que se rechazó:** Usar los números del 1 al 5 porque el script original de `main.js` los usaba para hacer un `reset` brusco que arruinaba las transiciones.

---

## 6. Autoevaluación Ponderada (Nota: 80/100)

| Criterio | Peso | Qué pide la profe | Valoración (0-100) | Justificación papu |
| :--- | :---: | :--- | :---: | :--- |
| **Trazabilidad y comprensión** | 25 | Explicar estado, fuerzas, render y archivos. | 80 | Todo documentado en el mapa del sistema. |
| **Verificación del algoritmo** | 25 | Aislar fuerzas, predecir y modificar parámetros. | 80 | Se hizo en la ficha de fuerzas y pruebas. |
| **Diseño de fuerzas e intención** | 20 | Comportamiento emergente y no pre-dibujado. | 80 | Respaldado por el score visual y el Curl Noise. |
| **Instrumento y score** | 15 | Conducir en vivo sin automatización rara. | 80 | Control total con las teclas personalizadas. |
| **Criterio frente a la IA** | 10 | Registrar hallazgos y descartes con la IA. | 85 | Bien documentado el cambio de números a letras. |
| **Entrega técnica** | 5 | URL y bitácora al 100. | 85 | Estructura completa y lista para entregar. |
| **Total Puntos** | **100** | *Suma final* | **81 / 100** | **Nota final de 80/100 (4)** |



https://alejogonzdav41.github.io/Unidad3Simulacion-nombrederechosdeautorMiguelValencia-/
