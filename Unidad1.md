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
