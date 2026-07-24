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

Mi idea es crear un arte generativo relacionado al nombre de la feria, "Fotosintesis", relacionado con el mismo proceso que realizan las plantas para alimentarse y crecer, en un principio solo quería un semilla que se convirtiera en planta pero la idea fue cambiando hasta que se convirtió en lo que terminé haciendo mi proyecto: Una planta que cuando toca unas moleculas crece y al llegar al sol florece, la misma compite con otras dos y el proceso se repite.

Sinceramente el codigo fue generado por IA pero igual fue un reto interesante, primero intenté con chatgpt lo cual no fue muy útil pero fué el que me gastó más tiempo pero fué el que me ayudó a dislumbrar mi norte, luego pasé a gemini que me dió un resultado más acercado a lo que quería, es el siguiente:

<img width="432" height="760" alt="image" src="https://github.com/user-attachments/assets/82e8e78c-1e72-47f6-b5d4-af24810091ca" />

```
let molecules = [];
let plants = [];
let state = 0;
let bloomTimer = 0;
let sunPos;
let lastMouseTime = 0;
let winnerPlant = null;
let WIN_HEIGHT_THRESHOLD;

function setup() {
  calcularCanvas916();
  iniciarSistema();
}

function windowResized() {
  calcularCanvas916();
}

function calcularCanvas916() {
  let w = windowWidth;
  let h = windowHeight;
  if (w / h > 9 / 16) {
    w = h * (9 / 16);
  } else {
    h = w * (16 / 9);
  }
  createCanvas(w, h);
}

function iniciarSistema() {
  molecules = [];
  plants = [];
  state = 0;
  winnerPlant = null;
  sunPos = createVector(width / 2, height * 0.1); 
  WIN_HEIGHT_THRESHOLD = height * 0.85;

  let grassHeight = height * 0.08;
  for (let i = 1; i <= 3; i++) {
    plants.push(new Plant((width / 4) * i, height - grassHeight));
  }
}

function mouseMoved() {
  lastMouseTime = millis();
}

function draw() {
  background(15, 30, 60); 

  let isInteracting = (millis() - lastMouseTime < 500) && mouseX > 0 && mouseX < width && mouseY > 0 && mouseY < height;

  dibujarSol();
  
  if (state === 0) {
    if (frameCount % 4 === 0) {
      molecules.push(new Molecule(sunPos.x, sunPos.y));
    }

    let currentMaxAltura = 0;
    let potentialWinner = null;

    for (let p of plants) {
      p.grow();
      p.display();
      
      let alturaActual = height - p.head.y;
      if (alturaActual > currentMaxAltura) {
        currentMaxAltura = alturaActual;
        potentialWinner = p;
      }
    }

    for (let i = molecules.length - 1; i >= 0; i--) {
      let m = molecules[i];
      m.applyBehaviors(isInteracting);
      m.update(isInteracting);
      m.checkEdges();
      m.display();

      for (let p of plants) {
        if (dist(m.pos.x, m.pos.y, p.head.x, p.head.y) < width * 0.04) {
          p.boost += 45;
          molecules.splice(i, 1);
          break;
        }
      }
    }

    if (currentMaxAltura > WIN_HEIGHT_THRESHOLD) {
      state = 1;
      winnerPlant = potentialWinner;
    }
    
  } else if (state === 1) {
    for (let p of plants) {
      p.display();
    }

    winnerPlant.ascend(sunPos);
    
    if (winnerPlant.atSun) {
      state = 2; // Iniciar floración
      bloomTimer = millis();
    }
    
  } else if (state === 2) {
    for (let p of plants) {
      p.display();
    }

    winnerPlant.displayFlower();

    if (millis() - bloomTimer > 5000) {
      iniciarSistema();
    }
  }
  
  dibujarCesped();
}

function dibujarSol() {
  push();
  noStroke();
  fill(255, 240, 150, 60);
  circle(sunPos.x, sunPos.y, width * 0.35);
  fill(255, 230, 100, 120);
  circle(sunPos.x, sunPos.y, width * 0.22);
  fill(255, 255, 220);
  circle(sunPos.x, sunPos.y, width * 0.14);
  pop();
}

function dibujarCesped() {
  push();
  noStroke();
  let baseGrassY = height - (height * 0.08);

  fill(20, 80, 30);
  beginShape();
  vertex(0, height);
  vertex(0, baseGrassY);
  for (let x = 0; x <= width; x += 10) {
    let y = baseGrassY - noise(x * 0.02) * 15;
    vertex(x, y);
  }
  vertex(width, height);
  endShape(CLOSE);
  pop();
}

class Molecule {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.acc = createVector(0, 0);
    this.noiseOffset = random(1000);
  }

  applyBehaviors(isInteracting) {
    if (isInteracting) {
      let mouse = createVector(mouseX, mouseY);
      let attraction = p5.Vector.sub(mouse, this.pos);
      attraction.setMag(0.7);
      this.acc.add(attraction);
      if (random() < 0.06) {
        this.vel = p5.Vector.random2D().mult(random(18, 28));
      }
    } else {
      let angle = noise(this.pos.x * 0.01, this.pos.y * 0.01, this.noiseOffset) * TWO_PI * 1.5;
      let tendencyForce = p5.Vector.fromAngle(angle).mult(0.04);
      let gravity = createVector(0, 0.035); // Ligera caída
      
      this.acc.add(tendencyForce);
      this.acc.add(gravity);
      if (random() < 0.004) {
        this.vel = p5.Vector.random2D().mult(random(10, 18));
      }
    }
  }

  update(isInteracting) {
    this.vel.add(this.acc);

    let meanSpeed = isInteracting ? 7.0 : 2.8; 
    let speedLimit = abs(randomGaussian(meanSpeed, 1.2));
    
    this.vel.limit(speedLimit);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.noiseOffset += 0.025;
  }

  checkEdges() {
    if (this.pos.x < 0) { this.pos.x = 0; this.vel.x *= -1; }
    if (this.pos.x > width) { this.pos.x = width; this.vel.x *= -1; }
    if (this.pos.y < 0) { this.pos.y = 0; this.vel.y *= -1; }
    if (this.pos.y > height) { this.pos.y = height; this.vel.y *= -1; }
  }

  display() {
    push();
    noStroke();
    fill(220, 250, 255, 180);
    circle(this.pos.x, this.pos.y, width * 0.012);
    pop();
  }
}

class Plant {
  constructor(x, y) {
    this.head = createVector(x, y);
    this.segments = [this.head.copy()];
    this.boost = 0;
    this.xoff = random(1000);
    this.atSun = false;
    this.flowerColor = color(random(180, 255), random(100, 220), random(180, 255));
  }

  grow() {

    let growthRate = abs(randomGaussian(0.35, 0.1));
    
    if (this.boost > 0) {
      growthRate += 2.2; // Boost competitivo al alimentarse
      this.boost--;
    }

    let angle = -PI/2 + (noise(this.xoff) - 0.5) * 1.8;
    let step = p5.Vector.fromAngle(angle).mult(growthRate);
    
    this.head.add(step);

    this.segments.push(this.head.copy());
    this.xoff += 0.055;
  }

  ascend(target) {
    // SÓLO la cabeza estira hacia el sol, dejando la raíz quieta
    if (!this.atSun) {
      let dir = p5.Vector.sub(target, this.head);
      let distToSun = dir.mag();

      if (distToSun > 5) { 
        dir.setMag(5); // Velocidad de estiramiento de victoria
        this.head.add(dir);
        this.segments.push(this.head.copy());
      } else {
        this.atSun = true;
      }
    }
  }

  display() {
    push();
    stroke(100, 200, 100);
    strokeWeight(width * 0.015);
    noFill();

    beginShape();
    for (let v of this.segments) {
      vertex(v.x, v.y);
    }
    endShape();

    if (!this.atSun || state !== 2) {
        fill(140, 240, 140);
        noStroke();
        circle(this.head.x, this.head.y, width * 0.035);
    }
    pop();
  }

  displayFlower() {
    push();
    translate(this.head.x, this.head.y);
    noStroke();

    fill(this.flowerColor);
    let petalSize = width * 0.07;
    for (let i = 0; i < 8; i++) {
      rotate(PI / 4);
      ellipse(petalSize * 0.6, 0, petalSize, petalSize * 0.45);
    }

    fill(255, 215, 0);
    circle(0, 0, petalSize * 0.55);
    pop();
  }
}
```

Y finalmente le di unos toques finales con la ayuda de Claude le di un arreglo visula.

<img width="476" height="816" alt="image" src="https://github.com/user-attachments/assets/8d7f09a1-7cda-480b-b7af-b327abcbe067" />

```
let molecules = [];
let plants = [];
let stars = [];
let state = 0;
let bloomTimer = 0;
let sunPos;
let lastMouseTime = 0;
let winnerPlant = null;
let WIN_HEIGHT_THRESHOLD;

const FLOWER_PALETTE = [
  [255, 107, 157],
  [184, 146, 255],
  [255, 209, 102],
  [78, 205, 196],
  [255, 159, 67],
  [247, 127, 190]
];

function setup() {
  calcularCanvas916();
  crearEstrellas();
  iniciarSistema();
}

function windowResized() {
  calcularCanvas916();
}

function calcularCanvas916() {
  let w = windowWidth;
  let h = windowHeight;
  if (w / h > 9 / 16) {
    w = h * (9 / 16);
  } else {
    h = w * (16 / 9);
  }
  createCanvas(w, h);
}

function crearEstrellas() {
  stars = [];
  for (let i = 0; i < 60; i++) {
    stars.push({
      fx: random(1),
      fy: random(0.55),
      r: random(0.8, 2.2),
      phase: random(TWO_PI)
    });
  }
}

function randomFlowerColor() {
  let c = random(FLOWER_PALETTE);
  return color(c[0], c[1], c[2]);
}

function iniciarSistema() {
  molecules = [];
  plants = [];
  state = 0;
  winnerPlant = null;
  sunPos = createVector(width / 2, height * 0.1);
  WIN_HEIGHT_THRESHOLD = height * 0.85;

  let grassHeight = height * 0.08;
  for (let i = 1; i <= 3; i++) {
    plants.push(new Plant((width / 4) * i, height - grassHeight));
  }
}

function resetRonda() {
  for (let p of plants) {
    p.segments = [p.base.copy()];
    p.head = p.base.copy();
    p.boost = 0;
    p.atSun = false;
    p.flowerColor = randomFlowerColor();
  }
  molecules = [];
  winnerPlant = null;
  state = 0;
}

function iniciarRetorno() {
  for (let p of plants) {
    p.retreatStartLen = max(1, p.segments.length);
  }
  state = 3;
}

function mouseMoved() {
  lastMouseTime = millis();
}

function draw() {
  dibujarCielo();
  dibujarEstrellas();
  dibujarSol();

  let isInteracting = (millis() - lastMouseTime < 500) && mouseX > 0 && mouseX < width && mouseY > 0 && mouseY < height;

  if (frameCount % 4 === 0) {
    molecules.push(new Molecule(sunPos.x, sunPos.y));
  }
  for (let i = molecules.length - 1; i >= 0; i--) {
    let m = molecules[i];
    m.applyBehaviors(isInteracting);
    m.update(isInteracting);
    m.checkEdges();
    m.display();

    if (state === 0) {
      for (let p of plants) {
        if (dist(m.pos.x, m.pos.y, p.head.x, p.head.y) < width * 0.04) {
          p.boost += 45;
          molecules.splice(i, 1);
          break;
        }
      }
    }
  }

  if (state === 0) {
    let currentMaxAltura = 0;
    let potentialWinner = null;

    for (let p of plants) {
      p.grow();
      p.display();

      let alturaActual = height - p.head.y;
      if (alturaActual > currentMaxAltura) {
        currentMaxAltura = alturaActual;
        potentialWinner = p;
      }
    }

    if (currentMaxAltura > WIN_HEIGHT_THRESHOLD) {
      state = 1;
      winnerPlant = potentialWinner;
    }

  } else if (state === 1) {
    // === FASE 1: VICTORIA ===
    for (let p of plants) {
      p.display();
    }
    winnerPlant.ascend(sunPos);

    if (winnerPlant.atSun) {
      state = 2;
      bloomTimer = millis();
    }

  } else if (state === 2) {
    // === FASE 2: FLORACIÓN ===
    for (let p of plants) {
      p.display();
    }
    winnerPlant.displayFlower(1);

    if (millis() - bloomTimer > 5000) {
      iniciarRetorno();
    }

  } else if (state === 3) {
    let allDone = true;
    for (let p of plants) {
      let done = p.retreat();
      if (!done) allDone = false;
      p.display();

      if (p === winnerPlant) {
        let fraction = constrain(p.segments.length / p.retreatStartLen, 0, 1);
        if (fraction > 0.02) p.displayFlower(fraction);
      }
    }
    if (allDone) resetRonda();
  }

  dibujarCesped();
}

function dibujarCielo() {
  push();
  noStroke();
  let topC = color(8, 12, 34);
  let midC = color(36, 24, 66);
  let bottomC = color(84, 46, 82);
  let bandH = 4;
  for (let y = 0; y < height; y += bandH) {
    let t = y / height;
    let c = (t < 0.6) ? lerpColor(topC, midC, t / 0.6) : lerpColor(midC, bottomC, (t - 0.6) / 0.4);
    fill(c);
    rect(0, y, width, bandH + 1);
  }
  pop();
}

function dibujarEstrellas() {
  push();
  noStroke();
  for (let s of stars) {
    let a = map(sin(millis() * 0.0012 + s.phase), -1, 1, 40, 200);
    fill(255, 255, 255, a);
    circle(s.fx * width, s.fy * height, s.r);
  }
  pop();
}

function dibujarSol() {
  push();
  noStroke();
  let pulse = 1 + sin(millis() * 0.0018) * 0.05;
  fill(255, 240, 150, 55);
  circle(sunPos.x, sunPos.y, width * 0.35 * pulse);
  fill(255, 230, 100, 110);
  circle(sunPos.x, sunPos.y, width * 0.22 * pulse);
  fill(255, 255, 225);
  circle(sunPos.x, sunPos.y, width * 0.14);
  pop();
}

function dibujarCesped() {
  push();
  noStroke();
  let baseGrassY = height - (height * 0.08);

  fill(14, 55, 24);
  beginShape();
  vertex(0, height);
  vertex(0, baseGrassY + 8);
  for (let x = 0; x <= width; x += 10) {
    let y = baseGrassY + 8 - noise(x * 0.015 + 100) * 12;
    vertex(x, y);
  }
  vertex(width, height);
  endShape(CLOSE);

  fill(34, 108, 48);
  beginShape();
  vertex(0, height);
  vertex(0, baseGrassY);
  for (let x = 0; x <= width; x += 8) {
    let sway = sin(frameCount * 0.02 + x * 0.05) * 3;
    let y = baseGrassY - noise(x * 0.02) * 15 + sway;
    vertex(x, y);
  }
  vertex(width, height);
  endShape(CLOSE);
  pop();
}

class Molecule {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.acc = createVector(0, 0);
    this.noiseOffset = random(1000);
  }

  applyBehaviors(isInteracting) {
    if (isInteracting) {
      let mouse = createVector(mouseX, mouseY);
      let attraction = p5.Vector.sub(mouse, this.pos);
      attraction.setMag(0.7);
      this.acc.add(attraction);

      if (random() < 0.06) {
        this.vel = p5.Vector.random2D().mult(random(18, 28));
      }
    } else {
      let angle = noise(this.pos.x * 0.01, this.pos.y * 0.01, this.noiseOffset) * TWO_PI * 1.5;
      let tendencyForce = p5.Vector.fromAngle(angle).mult(0.04);
      let gravity = createVector(0, 0.035);

      this.acc.add(tendencyForce);
      this.acc.add(gravity);

      if (random() < 0.004) {
        this.vel = p5.Vector.random2D().mult(random(10, 18));
      }
    }
  }

  update(isInteracting) {
    this.vel.add(this.acc);
    let meanSpeed = isInteracting ? 7.0 : 2.8;
    let speedLimit = abs(randomGaussian(meanSpeed, 1.2));
    this.vel.limit(speedLimit);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.noiseOffset += 0.025;
  }

  checkEdges() {
    if (this.pos.x < 0) { this.pos.x = 0; this.vel.x *= -1; }
    if (this.pos.x > width) { this.pos.x = width; this.vel.x *= -1; }
    if (this.pos.y < 0) { this.pos.y = 0; this.vel.y *= -1; }
    if (this.pos.y > height) { this.pos.y = height; this.vel.y *= -1; }
  }

  display() {
    push();
    noStroke();
    drawingContext.shadowBlur = 8;
    drawingContext.shadowColor = 'rgba(180,230,255,0.8)';
    fill(220, 250, 255, 190);
    circle(this.pos.x, this.pos.y, width * 0.012);
    drawingContext.shadowBlur = 0;
    pop();
  }
}

class Plant {
  constructor(x, y) {
    this.base = createVector(x, y);
    this.head = createVector(x, y);
    this.segments = [this.head.copy()];
    this.boost = 0;
    this.xoff = random(1000);
    this.atSun = false;
    this.retreatStartLen = 1;
    this.flowerColor = randomFlowerColor();
  }

  grow() {
    let growthRate = abs(randomGaussian(0.35, 0.1));

    if (this.boost > 0) {
      growthRate += 2.2;
      this.boost--;
    }

    let angle = -PI / 2 + (noise(this.xoff) - 0.5) * 1.8;
    let step = p5.Vector.fromAngle(angle).mult(growthRate);

    this.head.add(step);
    this.segments.push(this.head.copy());
    this.xoff += 0.055;
  }

  ascend(target) {
    if (!this.atSun) {
      let dir = p5.Vector.sub(target, this.head);
      let distToSun = dir.mag();

      if (distToSun > 5) {
        dir.setMag(5);
        this.head.add(dir);
        this.segments.push(this.head.copy());
      } else {
        this.atSun = true;
      }
    }
  }

  retreat() {
    if (this.segments.length <= 1) {
      this.head = this.base.copy();
      return true;
    }
    let step = max(2, floor(this.segments.length * 0.07));
    let newLen = max(1, this.segments.length - step);
    this.segments.length = newLen;
    this.head = this.segments[this.segments.length - 1].copy();
    return this.segments.length <= 1;
  }

  display() {
    push();
    noFill();
    for (let i = 1; i < this.segments.length; i++) {
      let t = i / this.segments.length;
      let stemColor = lerpColor(color(35, 90, 45), color(140, 235, 140), t);
      stroke(stemColor);
      strokeWeight(width * 0.015 * (1 - 0.3 * t));
      line(this.segments[i - 1].x, this.segments[i - 1].y, this.segments[i].x, this.segments[i].y);
    }

    if (!this.atSun || state !== 2) {
      noStroke();
      drawingContext.shadowBlur = 14;
      drawingContext.shadowColor = 'rgba(160,255,170,0.65)';
      fill(150, 245, 150);
      circle(this.head.x, this.head.y, width * 0.035);
      drawingContext.shadowBlur = 0;
    }
    pop();
  }

  displayFlower(fraction = 1) {
    push();
    translate(this.head.x, this.head.y);
    let pulse = 1 + sin(millis() * 0.003) * 0.05;
    scale(fraction * pulse);
    noStroke();

    let alpha = 255 * fraction;
    drawingContext.shadowBlur = 25;
    drawingContext.shadowColor = `rgba(${red(this.flowerColor)},${green(this.flowerColor)},${blue(this.flowerColor)},0.8)`;

    fill(red(this.flowerColor), green(this.flowerColor), blue(this.flowerColor), alpha);
    let petalSize = width * 0.075;
    for (let i = 0; i < 8; i++) {
      rotate(PI / 4 + millis() * 0.00015);
      ellipse(petalSize * 0.6, 0, petalSize, petalSize * 0.45);
    }

    drawingContext.shadowBlur = 15;
    drawingContext.shadowColor = 'rgba(255,215,0,0.8)';
    fill(255, 215, 0, alpha);
    circle(0, 0, petalSize * 0.55);
    drawingContext.shadowBlur = 0;
    pop();
  }
}
```

En el codigo se ve que se cumplen:

Normalidad: Para esto metí un randomGaussian (Campanazo de Gauss). Lo usé para controlar qué tan rápido crecen las plantas (growthRate) y para el límite de velocidad de las moléculas (speedLimit). Básicamente, asegura que la mayoría del tiempo se comporten de forma "normal" o en el promedio.

Tendencia: Aquí usé el ruido Perlin (noise(this.xoff)). Eso es lo que hace que los tallos no crezcan rectos aburridos, sino que se vayan curvando orgánicamente. También crea como un campo de "viento" que empuja las moléculas cuando nadie toca nada.

Excepción: Le puse una probabilidad súper bajita (tipo 0.004) de que una molécula de la nada pegue un salto a toda velocidad (entre 10 y 18).

Influencia: Cuando uno mueve el mouse, no es solo que las bolitas sigan al cursor y ya. Lo que en verdad pasa es que se "hackean" las matemáticas del código: la probabilidad de que den esos saltos locos sube de 0.4% a 6%, y el promedio de la velocidad de las moléculas pasa de 2.8 a 7.0. Por este medio se nota la interacción del usuario.

Con esto veo que cumple pero la parte de Probabilidad no me termina de convencer, pero diría que se ve antes de inicar y en los segundos antes de que se repita el ciclo.

### Criterio

Encargo completo: interpreto los cinco momentos dentro de un mismo sistema visual. Cumple.

Simulación con intención: utilizo al menos tres conceptos de la unidad para comunicar las ideas del encargo. Cumple.

Interacción significativa: la interacción modifica el comportamiento o las probabilidades del sistema, que también funciona sin intervención. Cumple.

Prototipo funcional: la experiencia puede ejecutarse y recorrerse completa sin errores que impidan comprenderla. Cumple.

Proceso documentado: la bitácora evidencia avances, decisiones, dificultades, soluciones, uso de IA y enlace al prototipo. Cumple.

Nota: 5.0
