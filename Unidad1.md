# Unidad 1

## Aleatoriedad

Usamos la aleatoriedad para que siempre consigamos resultados distintos y asi evitemos la monotonía

Hoy he aprendido bastante, la actitud de un diseñador dgenerativo debe ser la de un explorador.

<img width="1919" height="940" alt="image" src="https://github.com/user-attachments/assets/e790bb7f-f577-4619-bca8-008354a23e32" />

<img width="1919" height="893" alt="image" src="https://github.com/user-attachments/assets/894db4f7-9b1c-41d1-9abb-a42539c25cd0" />

Puro campanazo de Gauss

### Actividad 3

***En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios***
* La distribución uniforme quiere decir que hay uniformidad en la probabilidad de todo, osea que le probabilidad es la misma para todos. Mientras que la no uniforme tiene "cierta preferencia" o da prioridad a otros numeros en el rango a gusto de aquel que lo modifica.

Mi compañero Miguel Valencia me ha ayudado mucho, me enseñó como dirigir el patrón a la derecha.

***Modifica el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha.***

```
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(900, 500);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    quad(this.x, this.y, this.y, this.y, this.x, this.x, this.y, this.x);
  }

  step() {
    let choice = floor(randomGaussian(0, 3));
    if (choice < 0)
    {
      choice = 0;
    }
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}

```
### Actividad 4

<img width="1856" height="656" alt="image" src="https://github.com/user-attachments/assets/faac0c1a-7cd6-4c79-bd71-61ddeffca6dc" />

```
function setup() {
  createCanvas(1000, 1000);
}

function draw() {
  background(220);
}

function draw() {
  //{!1} A normal distribution with mean 320 and standard deviation 60
  let x = randomGaussian(320, 200);
  noStroke();
  fill(20, 5);
  square(x, 20, 100);
}
```

### Actividad 5

<img width="885" height="748" alt="image" src="https://github.com/user-attachments/assets/40a4ef8f-80d9-4ebb-91ce-a0326bd7debe" />

```
let x;
let y;

function setup() {
  createCanvas(1000, 1000);
  background(220);

  x = width / 2;
  y = height / 2;

  rectMode(CENTER);
}

function draw() {

  let paso;

  if (random(1) < 0.95) {
    paso = randomGaussian(0, 5);
  }

  else {
    paso = randomGaussian(0, 120);
  }

  let angulo = random(TWO_PI);

  x += cos(angulo) * paso;
  y += sin(angulo) * paso;

  x = constrain(x, 0, width);
  y = constrain(y, 0, height);

  fill(random(255), random(255), random(255), 120);
  noStroke();

  square(x, y, 12);
}
```

Usé la técnica de Lévy Flight porque permite que el punto haga la mayoría de sus movimientos cortos y, en pocas ocasiones, realice un salto mucho más grande. Esto hace que el recorrido sea más natural y menos repetitivo. Esperaba que el punto recorriera diferentes partes del lienzo sin quedarse siempre en el mismo lugar.

### Actividad 6

<img width="900" height="790" alt="image" src="https://github.com/user-attachments/assets/401b40e0-d940-4bf7-8767-a480fb53e6c7" />

```
let tx = 0;
let ty = 1000;
let tc = 2000;

function setup() {
  createCanvas(1000, 1000);
  background(15);
  rectMode(CENTER);
  noStroke();
}

function draw() {

  let x = noise(tx) * width;
  let y = noise(ty) * height;

  let r = noise(tc) * 255;
  let g = noise(tc + 100) * 255;
  let b = noise(tc + 200) * 255;

  fill(r, g, b, 80);

  square(x, y, 30);

  tx += 0.01;
  ty += 0.01;
  tc += 0.02;
}
```

Decidí representar el ruido Perlin con un cuadrado que cambia de posición y de color de forma suave. A diferencia de usar números completamente aleatorios, el ruido Perlin hace que los cambios sean continuos, por lo que el movimiento se ve más natural y agradable. Esperaba que el cuadrado recorriera el lienzo sin hacer movimientos bruscos y que los colores cambiaran poco a poco.

### Actividad 07
**Reto de diseño: Navegar la incertidumbre**

En un primer momento habia pensado en dos ideas: Un volcan que erupciona y tiene una poblacion abajo con la que se podía interactuar y unas olas del mar que estaban dispersas pero que al tocarlas bajaban todas. Luego de hablar con Juanferfranco me dí cuenta de cual era el proposito real: no acoplar el entorno a aquello que me parece cómodo o me gusta, si no brindar un producto o una solución a una necesidad.
Con eso en mente decidí investigar sobre algunas ferias de ciencia que podría haber en la ciudad y encontré "Fotosíntesis" un festival de arte, ciencia y tecnologías que se acoplaba a la idea de "feria de ciencia y creatividad" por lo que ofrece.
