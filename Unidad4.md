# 🐉 Dragones en el cielo

https://alejogonzdav41.github.io/Unidad4Alejo/


## Arquetipos y Personalidades (Agentes)

El colectivo está compuesto por 8 dragones divididos en 4 arquetipos tímbricos y cromáticos:

| Arquetipo | Instrumento Inspirador | Onda Sintética | Frecuencia Base | Color Principal |
| :--- | :--- | :--- | :--- | :--- |
| **Brasa** | Cuerdas | Triángulo (`triangle`) | 146.83 Hz (D3) | `#ff7657` |
| **Niebla** | Flauta de aire | Senoidal (`sine`) | 220.00 Hz (A3) | `#8f9dff` |
| **Aurora** | Marimba | Triángulo (`triangle`) | 293.66 Hz (D4) | `#a7e66e` |
| **Éter** | "Pad" | Senoidal (`sine`) | 369.99 Hz (F#4) | `#d88cf5` |

---

## Arquitectura de Audio y Gráficos

1. **Síntesis Aditiva Modular (`p5.sound`):**
   * Cada dragón posee su propio oscilador (`p5.Oscillator`), un filtro de paso bajo (`p5.LowPass`) que suaviza los armónicos y una envolvente ADSR (`p5.Envelope`).
   * Las notas generadas responden a una **escala pentatónica armónica**, cuya frecuencia se recalcula dinámicamente según la fase $\theta_i$ y el nivel de sincronización global.
   * Panorama estéreo espacializado según la posición e identificador de cada agente.

2. **Renderizado Canvas Dinámico (`p5.js`):**
   * **Siluetas Vectoriales:** Cuerpo, alas en aleteo proporcional a $\sin(\theta_i)$, cola y cabeza proyectados dinámicamente.
   * **Interpolación de Movimiento:** Transición suave de posiciones desde un estado caótico basado en ruido pseudoaleatorio espacial hacia órbitas armónicas circulares mediante interpolación lineal (`p.lerp`).
   * **Estelas y Vectores:** Dibujo de estelas de movimiento que cambian de densidad según el parámetro de coherencia $R$.

---

## Interacción y Paneles del Laboratorio

* **Acoplamiento ($K$):** Ajusta la fuerza de influencia rítmica que ejerce cada dragón sobre sus compañeros.
* **Ritmo Natural ($\omega$):** Controla la velocidad rítmica base de la manada.
* **Diferencia de Ritmos ($\sigma$):** Introduce variaciones en las frecuencias individuales para dificultar o facilitar la sincronización.
* **Provocar Caos:** Rompe el acoplamiento y dispersa aleatoriamente la fase de todos los agentes.
* **Armonía Total:** Fuerza una fase compartida unificada, elevando el acoplamiento al máximo.
* **Interrupción Directa:** Al hacer clic sobre cualquier dragón en el lienzo, se desplaza su fase ($\Delta \theta$), separándolo temporalmente del grupo.

---

## Por lo que se pasó

Pues desde un principio pude aplicar bastante bien la idea que tenía, encontré problemas a la hora de conseguir unas visuales que me gustaran y que se parecieran a un dragón (peleando con la IA) pero igual siento que llegué a un buen punto. Y musicalmente hablando tambien hice varios cambios porque al principio la melodía que se generaba era por ondas y sonaba un "wuuuu" constante que no era tan agradable al oido, al final me basé en una canción que habia escuchado hace poco y me terminó gustando el resultado musical.

## Autoevaluación

## Autoevaluación (Escala 1.0 - 5.0)

| Criterio de Evaluación | Ponderación | Descripción del Cumplimiento | Nota |
| :--- | :---: | :--- | :---: |
| **Cumplimiento de Requisitos Mínimos** | 25% | Implementé los 8 agentes, 4 personalidades audiovisuales, control de $K$, perturbación de estado y la comunicación clara de los 3 estados del colectivo. | **4.0** |
| **Claridad de Variables del Modelo** | 25% | Explico claramente qué hace la fase ($\theta$), la frecuencia ($\omega$) y el acoplamiento ($K$) dentro del código y la escena. | **4.5** |
| **Explicación del Comportamiento Emergente** | 25% | Demuestro cómo el modelo de Kuramoto controla los shaders de partículas, la luz volumétrica y los búferes de audio. | **3.5** |
| **Demostración de Objetivos de Unidad** | 25% | El sistema funciona como un instrumento performativo interactivo real, donde la sincronía emerge de la física del modelo. | **5.0** |
| **NOTA FINAL** | **100%** | **Promedio ponderado de la evaluación** | **4.25** |
