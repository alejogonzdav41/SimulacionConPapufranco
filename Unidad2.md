# Proceso

La idea que tuve fue la de una cadena alimenticia, donde hay pasto, presa y depredador, por lo que le dí mi idea a gemini y me dió este primer resultado.

<img width="915" height="821" alt="image" src="https://github.com/user-attachments/assets/5f1a1c4a-b838-452a-a5af-5ae6637d7471" />

Como llegaba a un punto en el que se quedaba en equilibrio me asusté y puse un parametro para que los depredadores se coman a las presas, las presas al pasto y el pasto spawneaba cada cierto timepo.

<img width="913" height="810" alt="image" src="https://github.com/user-attachments/assets/ac3ecb24-05ab-4a33-bae5-0131c92db774" />

Como llegaba a un punto en el que se perdian totalmente las presas me asusté y volví a la primera versión del código, ahí tomé la desición de que en lugar de destruir, si pasan mucho tiempo los depredares con las presas, salgan expulsados.

<img width="913" height="828" alt="image" src="https://github.com/user-attachments/assets/566d8b83-5607-441e-b9bc-7b4ec35d0a48" />

Pero salió otro problema, si se acumulaban muchas presas la expulsión de los depredadores era minima, entonces hice que las presas también salieran expulsadas al tocar a los depredadores. 

<img width="917" height="817" alt="image" src="https://github.com/user-attachments/assets/59abc2e5-aac1-4037-ab1b-979884586142" />

<img width="912" height="830" alt="image" src="https://github.com/user-attachments/assets/199429ef-4fb8-4ccb-864a-151e332f57af" />

Y como ese caos no me gustó del todo entonces volví a la idea principal, ahí si hice muchos cambios visuales mientras que "refinaba" otras cositas para que cumpliera con lo pedido y conseguí el resultado que esperaba.
<img width="832" height="820" alt="image" src="https://github.com/user-attachments/assets/7a26f2f7-c77c-4ebe-ace0-ff3d10484ead" />

https://editor.p5js.org/alejogonzdav41/sketches/PAetnlaqh

index.html
```
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Sabana Viva — Una contradicción en movimiento</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Zilla+Slab:wght@400;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap');
 
  :root{
    --bg-deep:#171b10;
    --bg-warm:#2e2818;
    --panel:#20220f;
    --line:#4a4326;
    --grass:#8ab84a;
    --zebra:#ece4cf;
    --croc:#54682f;
    --ember:#d98e3f;
    --blood:#c1442d;
    --ink:#ece4cf;
    --ink-dim:#a89f7f;
  }
 
  *{ box-sizing:border-box; }
 
  html,body{
    margin:0; padding:0; overflow:hidden;
    background: radial-gradient(ellipse at 30% 20%, var(--bg-warm), var(--bg-deep) 70%);
    font-family:'Zilla Slab', serif;
    color:var(--ink);
  }
 
  canvas{ display:block; }
 
  #panel{
    position:absolute; top:16px; left:16px;
    width:266px;
    max-height: calc(100vh - 32px);
    overflow-y:auto;
    background: linear-gradient(180deg, rgba(32,34,15,0.94), rgba(23,27,16,0.94));
    border:1px solid var(--line);
    border-left:3px solid var(--ember);
    border-radius:6px;
    padding:16px 16px 14px 16px;
    backdrop-filter: blur(6px);
    box-shadow: 0 8px 24px rgba(0,0,0,0.45);
    transition: transform 0.3s ease, opacity 0.3s ease;
  }
  #panel::-webkit-scrollbar{ width:6px; }
  #panel::-webkit-scrollbar-thumb{ background:var(--line); border-radius:3px; }

  /* Estado contraído del panel */
  #panel.collapsed {
    transform: translateX(calc(-100% - 30px));
    opacity: 0;
    pointer-events: none;
  }
 
  .panel-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
  }

  #toggleBtn {
    background: rgba(217,142,63,0.15);
    border: 1px solid var(--ember);
    color: var(--ember);
    border-radius: 4px;
    cursor: pointer;
    font-size: 14px;
    width: 26px;
    height: 26px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: background 0.15s ease;
  }
  #toggleBtn:hover { background: rgba(217,142,63,0.3); }

  /* Botón flotante para abrir el panel cuando está oculto */
  #openBtn {
    position: absolute;
    top: 16px;
    left: 16px;
    background: linear-gradient(180deg, rgba(32,34,15,0.94), rgba(23,27,16,0.94));
    border: 1px solid var(--line);
    border-left: 3px solid var(--ember);
    color: var(--ember);
    padding: 10px 14px;
    border-radius: 6px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 11.5px;
    font-weight: 700;
    cursor: pointer;
    backdrop-filter: blur(6px);
    box-shadow: 0 8px 24px rgba(0,0,0,0.45);
    display: none;
    z-index: 10;
    transition: background 0.15s ease;
  }
  #openBtn:hover { background: rgba(32,34,15,1); }
  #openBtn.visible { display: block; }
 
  #panel .eyebrow{
    font-family:'JetBrains Mono', monospace;
    font-size:10px;
    letter-spacing:0.16em;
    color:var(--ember);
    text-transform:uppercase;
    margin:0 0 2px 0;
  }
 
  #panel h1{
    font-size:19px;
    margin:0 0 12px 0;
    font-weight:700;
    letter-spacing:0.01em;
    border-bottom:1px solid var(--line);
    padding-bottom:10px;
  }
 
  .field{ margin-bottom:11px; }
 
  .field-head{
    display:flex;
    justify-content:space-between;
    align-items:baseline;
    margin-bottom:4px;
  }
 
  .field-label{
    font-size:11.5px;
    color:var(--ink-dim);
    text-transform:uppercase;
    letter-spacing:0.05em;
  }
 
  .field-value{
    font-family:'JetBrains Mono', monospace;
    font-size:13px;
    font-weight:700;
    color:var(--ink);
    background:rgba(0,0,0,0.3);
    padding:1px 7px;
    border-radius:3px;
    min-width:28px;
    text-align:center;
  }
 
  .swatch{ display:inline-block; width:9px; height:9px; border-radius:2px; margin-right:6px; vertical-align:1px; }
 
  input[type=range]{
    -webkit-appearance:none;
    width:100%;
    height:4px;
    border-radius:2px;
    background:var(--line);
    outline:none;
    margin:2px 0;
  }
  input[type=range]::-webkit-slider-thumb{
    -webkit-appearance:none;
    width:14px; height:14px;
    border-radius:50%;
    background:var(--ember);
    border:2px solid #1a1a10;
    cursor:pointer;
    margin-top:-5px;
  }
  input[type=range]::-moz-range-thumb{
    width:12px; height:12px; border-radius:50%;
    background:var(--ember); border:2px solid #1a1a10; cursor:pointer;
  }
  input[type=range]:disabled::-webkit-slider-thumb{ background:#6b6248; }
  input[type=range]::-webkit-slider-runnable-track{ height:4px; border-radius:2px; }
 
  #capacidad{
    font-family:'JetBrains Mono', monospace;
    font-size:10.5px;
    color:var(--ink-dim);
    margin:2px 0 12px 0;
    padding:6px 8px;
    background:rgba(0,0,0,0.25);
    border-radius:4px;
    border:1px dashed var(--line);
  }
  #capacidad b{ color:var(--ember); }
  #capacidad.full b{ color:var(--blood); }
 
  select{
    width:100%;
    background:rgba(0,0,0,0.3);
    color:var(--ink);
    border:1px solid var(--line);
    border-radius:4px;
    padding:6px 6px;
    font-family:'JetBrains Mono', monospace;
    font-size:12px;
  }
 
  .mode-note{
    font-size:11px;
    color:var(--ink-dim);
    line-height:1.35;
    margin-top:5px;
    font-style:italic;
  }
 
  .seed-row{ display:flex; gap:6px; }
  .seed-row input[type=text]{
    flex:1;
    background:rgba(0,0,0,0.3);
    border:1px solid var(--line);
    border-radius:4px;
    color:var(--ink);
    font-family:'JetBrains Mono', monospace;
    font-size:12px;
    padding:6px 8px;
    width:100%;
  }
  .seed-row button{
    background:rgba(217,142,63,0.15);
    border:1px solid var(--ember);
    color:var(--ember);
    border-radius:4px;
    cursor:pointer;
    font-size:13px;
    padding:0 10px;
  }
  .seed-row button:hover{ background:rgba(217,142,63,0.3); }
 
  #restart{
    width:100%;
    margin-top:10px;
    padding:9px 0;
    background:var(--ember);
    color:#1a1a10;
    border:none;
    border-radius:4px;
    font-family:'JetBrains Mono', monospace;
    font-weight:700;
    font-size:11.5px;
    letter-spacing:0.04em;
    text-transform:uppercase;
    cursor:pointer;
    transition: transform 0.08s ease, background 0.15s ease;
  }
  #restart:hover{ background:#e8a15c; }
  #restart:active{ transform:scale(0.97); }
 
  #census{
    margin-top:12px;
    padding-top:10px;
    border-top:1px solid var(--line);
    display:flex;
    justify-content:space-between;
    font-family:'JetBrains Mono', monospace;
    font-size:11px;
  }
  #census div{ text-align:center; }
  #census .n{ font-size:15px; font-weight:700; display:block; }
 
  hr.sep{ border:none; border-top:1px solid var(--line); margin:14px 0 12px 0; }
</style>
</head>
<body>

<button id="openBtn">⚙ Sabana Viva</button>
 
<div id="panel">
  <div class="panel-header">
    <div>
      <div class="eyebrow">Ecosistema · Censo de campo</div>
      <h1>Sabana Viva</h1>
    </div>
    <button id="toggleBtn" title="Ocultar panel">◀</button>
  </div>
 
  <div class="field">
    <div class="field-head">
      <span class="field-label">Capacidad del ecosistema (N)</span>
      <span class="field-value" id="valN">200</span>
    </div>
    <input type="range" id="sliderN" min="50" max="400" step="10" value="200">
  </div>
 
  <div id="capacidad">Asignado: <b id="asignado">0</b> / <span id="capMax">200</span> · Disponible: <b id="disponible">200</b></div>
 
  <div class="field">
    <div class="field-head">
      <span class="field-label"><span class="swatch" style="background:#8ab84a"></span>Pasto</span>
      <span class="field-value" id="valRecursos">120</span>
    </div>
    <input type="range" id="sliderRecursos" min="0" max="400" step="1" value="120">
  </div>
 
  <div class="field">
    <div class="field-head">
      <span class="field-label"><span class="swatch" style="background:#ece4cf"></span>Cebras</span>
      <span class="field-value" id="valPresas">70</span>
    </div>
    <input type="range" id="sliderPresas" min="0" max="400" step="1" value="70">
  </div>
 
  <div class="field">
    <div class="field-head">
      <span class="field-label"><span class="swatch" style="background:#c1442d"></span>Cocodrilos</span>
      <span class="field-value" id="valDepredadores">10</span>
    </div>
    <input type="range" id="sliderDepredadores" min="0" max="400" step="1" value="10">
  </div>
 
  <hr class="sep">
 
  <div class="field">
    <div class="field-head">
      <span class="field-label">Modo de comportamiento</span>
    </div>
    <select id="modo">
      <option value="equilibrio">Equilibrio salvaje</option>
      <option value="manada">Instinto de manada</option>
      <option value="individualismo">Ley del más fuerte</option>
    </select>
    <div class="mode-note" id="modoNota">La cooperación y la competencia se reparten el peso por igual.</div>
  </div>
 
  <div class="field">
    <div class="field-head">
      <span class="field-label">Semilla</span>
    </div>
    <div class="seed-row">
      <input type="text" id="seed" value="">
      <button id="dado" title="Semilla aleatoria">🎲</button>
    </div>
  </div>
 
  <button id="restart">Reiniciar simulación</button>
 
  <div id="census">
    <div><span class="n" id="cN" style="color:#8ab84a">0</span>pasto</div>
    <div><span class="n" id="cP" style="color:#ece4cf">0</span>cebras</div>
    <div><span class="n" id="cD" style="color:#c1442d">0</span>croc.</div>
  </div>
</div>
 
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.min.js"></script>
<script src="sketch.js"></script>
</body>
</html>
```

sketch.js
```
let particles = [];
let currentSeed = 0;
 
// --- Parámetros físicos (motor de partículas tipo Clusters) ---
const beta = 15;
const friction = 0.92;
const forceFactor = 0.5;
 
const modes = {
  equilibrio: {
    label: "Equilibrio salvaje",
    note: "La cooperación y la competencia se reparten el peso por igual.",
    matrix: [
      [ 0.1,  0.0,  0.0],
      [ 0.3,  0.2, -1.0],
      [ 0.0,  1.0, -0.5]
    ],
    radii: [
      [50,  50,  50 ],
      [60,  60, 150 ],
      [50,  80,  60 ]
    ]
  },
  manada: {
    label: "Instinto de manada",
    note: "Las cebras se cohesionan con más fuerza y a mayor distancia: la cooperación domina y el grupo se vuelve el refugio frente al depredador.",
    matrix: [
      [ 0.1,  0.0,  0.0],
      [ 0.3,  0.6, -1.0],
      [ 0.0,  1.0, -0.5]
    ],
    radii: [
      [50,  50,  50 ],
      [60, 110, 150 ],
      [50,  80,  60 ]
    ]
  },
  individualismo: {
    label: "Ley del más fuerte",
    note: "Cada cebra se dispersa por su cuenta y el depredador caza más lejos y con más fuerza: la competencia individual domina y expone al grupo.",
    matrix: [
      [ 0.1,  0.0,  0.0],
      [ 0.3, -0.3, -1.4],
      [ 0.0,  1.4, -0.9]
    ],
    radii: [
      [50,  50,  50 ],
      [60,  45, 190 ],
      [50,  95,  60 ]
    ]
  }
};
 
let matrix = modes.equilibrio.matrix.map(row => row.slice());
let radii  = modes.equilibrio.radii.map(row => row.slice());
 
// --- Referencias a la interfaz ---
const els = {
  n: document.getElementById('sliderN'),
  recursos: document.getElementById('sliderRecursos'),
  presas: document.getElementById('sliderPresas'),
  depredadores: document.getElementById('sliderDepredadores'),
  restart: document.getElementById('restart'),
  toggleBtn: document.getElementById('toggleBtn'),
  openBtn: document.getElementById('openBtn'),
  panel: document.getElementById('panel'),
  valN: document.getElementById('valN'),
  valRecursos: document.getElementById('valRecursos'),
  valPresas: document.getElementById('valPresas'),
  valDepredadores: document.getElementById('valDepredadores'),
  capMax: document.getElementById('capMax'),
  asignado: document.getElementById('asignado'),
  disponible: document.getElementById('disponible'),
  capacidad: document.getElementById('capacidad'),
  modo: document.getElementById('modo'),
  modoNota: document.getElementById('modoNota'),
  seed: document.getElementById('seed'),
  dado: document.getElementById('dado'),
  cN: document.getElementById('cN'),
  cP: document.getElementById('cP'),
  cD: document.getElementById('cD')
};

// --- Control de Pestaña Ocultar/Mostrar UI ---
els.toggleBtn.addEventListener('click', () => {
  els.panel.classList.add('collapsed');
  els.openBtn.classList.add('visible');
});

els.openBtn.addEventListener('click', () => {
  els.panel.classList.remove('collapsed');
  els.openBtn.classList.remove('visible');
});
 
function getCounts(){
  return {
    n: parseInt(els.n.value),
    r: parseInt(els.recursos.value),
    p: parseInt(els.presas.value),
    d: parseInt(els.depredadores.value)
  };
}
 
function refreshBudgetLabels(){
  const { n, r, p, d } = getCounts();
  const asignado = r + p + d;
  els.capMax.textContent = n;
  els.asignado.textContent = asignado;
  els.disponible.textContent = n - asignado;
  els.capacidad.classList.toggle('full', asignado >= n);
}
 
function clampPopulationSlider(changedEl, otherEls){
  const n = parseInt(els.n.value);
  const others = otherEls.reduce((sum, el) => sum + parseInt(el.value), 0);
  const maxAllowed = Math.max(0, n - others);
  if (parseInt(changedEl.value) > maxAllowed){
    changedEl.value = maxAllowed;
  }
}
 
function onRecursosInput(){
  clampPopulationSlider(els.recursos, [els.presas, els.depredadores]);
  els.valRecursos.textContent = els.recursos.value;
  refreshBudgetLabels();
}
function onPresasInput(){
  clampPopulationSlider(els.presas, [els.recursos, els.depredadores]);
  els.valPresas.textContent = els.presas.value;
  refreshBudgetLabels();
}
function onDepredadoresInput(){
  clampPopulationSlider(els.depredadores, [els.recursos, els.presas]);
  els.valDepredadores.textContent = els.depredadores.value;
  refreshBudgetLabels();
}
 
function onNInput(){
  const n = parseInt(els.n.value);
  els.valN.textContent = n;
  let r = parseInt(els.recursos.value);
  let p = parseInt(els.presas.value);
  let d = parseInt(els.depredadores.value);
  let total = r + p + d;
  if (total > n && total > 0){
    const factor = n / total;
    r = Math.floor(r * factor);
    p = Math.floor(p * factor);
    d = Math.floor(d * factor);
    els.recursos.value = r;
    els.presas.value = p;
    els.depredadores.value = d;
    els.valRecursos.textContent = r;
    els.valPresas.textContent = p;
    els.valDepredadores.textContent = d;
  }
  refreshBudgetLabels();
}
 
els.recursos.addEventListener('input', onRecursosInput);
els.presas.addEventListener('input', onPresasInput);
els.depredadores.addEventListener('input', onDepredadoresInput);
els.n.addEventListener('input', onNInput);
els.restart.addEventListener('click', reiniciarSistema);
 
els.modo.addEventListener('change', () => {
  const m = modes[els.modo.value];
  for (let i = 0; i < 3; i++){
    for (let j = 0; j < 3; j++){
      matrix[i][j] = m.matrix[i][j];
      radii[i][j] = m.radii[i][j];
    }
  }
  els.modoNota.textContent = m.note;
});
 
function randomSeedValue(){
  return Math.floor(Math.random() * 1000000);
}
els.seed.value = randomSeedValue();
els.dado.addEventListener('click', () => {
  els.seed.value = randomSeedValue();
  reiniciarSistema();
});
 
function setup(){
  const cnv = createCanvas(windowWidth, windowHeight);
  cnv.style('position', 'fixed');
  cnv.style('top', '0');
  cnv.style('left', '0');
  cnv.style('z-index', '-1');
  colorMode(RGB);
  refreshBudgetLabels();
  reiniciarSistema();
}
 
function reiniciarSistema(){
  const seedVal = parseInt(els.seed.value) || 0;
  randomSeed(seedVal);
 
  particles = [];
  const { r: pRecursos, p: pPresas, d: pDepredadores } = getCounts();
 
  for (let i = 0; i < pRecursos; i++) particles.push(new Particle(random(width), random(height), 0));
  for (let i = 0; i < pPresas; i++) particles.push(new Particle(random(width), random(height), 1));
  for (let i = 0; i < pDepredadores; i++) particles.push(new Particle(random(width), random(height), 2));
 
  els.cN.textContent = pRecursos;
  els.cP.textContent = pPresas;
  els.cD.textContent = pDepredadores;
  refreshBudgetLabels();
}
 
function draw(){
  noStroke();
  fill(23, 27, 16, 60);
  rect(0, 0, width, height);
 
  for (let i = 0; i < particles.length; i++) particles[i].interact(particles);
  for (let i = 0; i < particles.length; i++){
    particles[i].update();
    particles[i].show();
  }
}
 
class Particle{
  constructor(x, y, t){
    this.x = x; this.y = y;
    this.vx = 0; this.vy = 0;
    this.type = t;
    this.heading = random(TWO_PI);
    this.phase = random(1000);
    this.legPhase = random(TWO_PI);
 
    if (this.type === 0){
      this.size = random(5, 8);
      const g = random(1);
      this.tint = lerpColor(color(120, 170, 60), color(190, 210, 90), g);
    } else if (this.type === 1){
      this.size = 11;
      this.tint = color(236, 228, 207);
    } else {
      this.size = 17;
      this.tint = color(84, 104, 47);
    }
  }
 
  interact(others){
    for (let i = 0; i < others.length; i++){
      const other = others[i];
      if (this === other) continue;
 
      let dx = other.x - this.x;
      let dy = other.y - this.y;
 
      if (dx > width / 2) dx -= width;
      if (dx < -width / 2) dx += width;
      if (dy > height / 2) dy -= height;
      if (dy < -height / 2) dy += height;
 
      const d = sqrt(dx * dx + dy * dy);
      const R = radii[this.type][other.type];
      const G = matrix[this.type][other.type];
 
      if (d > 0 && d < R){
        let F = 0;
        if (d < beta){
          F = (d / beta) - 1;
        } else {
          F = G * (1 - abs(2 * d - R - beta) / (R - beta));
        }
        const dirX = dx / d;
        const dirY = dy / d;
        this.vx += F * dirX * forceFactor;
        this.vy += F * dirY * forceFactor;
      }
    }
  }
 
  update(){
    this.vx *= friction;
    this.vy *= friction;
 
    const speed = sqrt(this.vx * this.vx + this.vy * this.vy);
    const maxSpeed = 8;
    if (speed > maxSpeed){
      this.vx = (this.vx / speed) * maxSpeed;
      this.vy = (this.vy / speed) * maxSpeed;
    }
 
    if (this.type !== 0 && speed > 0.15){
      const target = atan2(this.vy, this.vx);
      let diff = target - this.heading;
      while (diff > PI) diff -= TWO_PI;
      while (diff < -PI) diff += TWO_PI;
      this.heading += diff * 0.2;
    }
 
    this.x += this.vx;
    this.y += this.vy;
 
    if (this.x < 0) this.x += width;
    if (this.x >= width) this.x -= width;
    if (this.y < 0) this.y += height;
    if (this.y >= height) this.y -= height;
  }
 
  show(){
    if (this.type === 0) this.showGrass();
    else if (this.type === 1) this.showZebra();
    else this.showCroc();
  }
 
  showGrass(){
    push();
    translate(this.x, this.y);
    const sway = sin(frameCount * 0.04 + this.phase) * (this.size * 0.25);
    stroke(this.tint);
    strokeWeight(1.6);
    strokeCap(ROUND);
    noFill();
    line(0, 2, -this.size * 0.3 + sway * 0.3, -this.size + sway);
    line(0, 2, sway * 0.4, -this.size * 1.3 - 1);
    line(0, 2, this.size * 0.3 + sway * 0.3, -this.size + sway * 0.6);
    pop();
  }
 
  showZebra(){
    push();
    translate(this.x, this.y);
    rotate(this.heading);
 
    const L = this.size;
    const stride = sin(frameCount * 0.35 + this.legPhase);
 
    stroke(40, 38, 34);
    strokeWeight(1.6);
    line(-L * 0.35, L * 0.3, -L * 0.35 + stride * 2, L * 0.75);
    line(L * 0.15, L * 0.3, L * 0.15 - stride * 2, L * 0.75);
 
    noStroke();
    fill(this.tint);
    ellipse(0, 0, L * 2.1, L * 1.15);
 
    push();
    translate(L * 1.05, -L * 0.05);
    rotate(-0.35);
    fill(this.tint);
    ellipse(0, 0, L * 0.9, L * 0.55);
    pop();
 
    fill(30, 28, 24);
    triangle(L * 1.25, -L * 0.35, L * 1.05, -L * 0.55, L * 0.9, -L * 0.3);
 
    stroke(30, 28, 24);
    strokeWeight(1.8);
    for (let i = -1; i <= 3; i++){
      const sx = i * L * 0.38;
      line(sx, -L * 0.5, sx - L * 0.15, L * 0.5);
    }
 
    stroke(30, 28, 24);
    strokeWeight(2);
    line(L * 0.3, -L * 0.55, L * 0.85, -L * 0.35);
 
    stroke(30, 28, 24);
    strokeWeight(1.4);
    line(-L * 1.0, 0, -L * 1.3, L * 0.3 + stride);
 
    pop();
  }
 
  showCroc(){
    push();
    translate(this.x, this.y);
    rotate(this.heading);
 
    const L = this.size;
    const swim = sin(frameCount * 0.15 + this.phase) * 0.15;
 
    noStroke();
 
    fill(this.tint);
    push();
    rotate(swim * 1.5);
    triangle(-L * 1.0, 0, -L * 2.0, -L * 0.35, -L * 2.0, L * 0.35);
    pop();
 
    fill(this.tint);
    ellipse(0, 0, L * 2.0, L * 0.95);
 
    fill(60, 78, 34);
    for (let i = -1; i <= 1; i++){
      ellipse(i * L * 0.55, -L * 0.28, L * 0.35, L * 0.22);
    }
 
    fill(this.tint);
    beginShape();
    vertex(L * 0.9, -L * 0.3);
    vertex(L * 1.9, -L * 0.12);
    vertex(L * 1.9, L * 0.12);
    vertex(L * 0.9, L * 0.3);
    endShape(CLOSE);
 
    fill(230, 225, 205);
    for (let i = 0; i < 4; i++){
      const tx = L * 1.05 + i * L * 0.2;
      triangle(tx, -L * 0.14, tx + L * 0.09, -L * 0.14, tx + L * 0.045, -L * 0.02);
      triangle(tx, L * 0.14, tx + L * 0.09, L * 0.14, tx + L * 0.045, L * 0.02);
    }
 
    fill(200, 60, 40);
    ellipse(L * 0.75, -L * 0.32, L * 0.16);
    ellipse(L * 0.75, L * 0.32, L * 0.16);
    fill(10);
    ellipse(L * 0.78, -L * 0.32, L * 0.07);
    ellipse(L * 0.78, L * 0.32, L * 0.07);
 
    pop();
  }
}
 
function windowResized(){
  resizeCanvas(windowWidth, windowHeight);
}
```

### Matriz

| **Partícula que reacciona ↓ / Mirando a →** | **Pasto(0)** | **Cebra(1)** | **Cocodrilo(2)** |
| ------------------- | :-----------: | :---------------: | :--------: |
| **Pasto(0)**       |    **+0.1**   |      **0.0**      |   **0.0**  |
| **Cebra(1)**   |    **+0.3**   |      **+0.2**      |   **-0.1**  |
| **Cocodrilo(2)**          |    **0.0**   |      **+1.0**      |  **-0.5**  |

# Autoevluación  

| **Criterio**                                                                      | **Peso** |    **Valoración**    | **Aporte / Justificación**                                                                                                                                                                                         |
| --------------------------------------------------------------------------------- | :------: | :------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| La intención es clara y perceptible en el comportamiento.                         |    20%   |       **19/20**      | Siento que la tensión que quería mostrar (cooperación vs. vulnerabilidad) se nota a facilmente. Cuando uno ve la simulación, se entiende que las cebras están tratando de estar juntas y tranquilas, pero que se vuelven locas cuando alguno de los cocodrilos se acerca. Me bajé un poquito porque a veces las cebras se atascan un poquito en los bordes, pero la intención principal es clara. |
| Los tipos, cantidades, matriz y parámetros están justificados desde la intención. |    25%   |       **25/25**      | Me pongo los puntos completos porque los números puestos tienen su razón de ser así. Entendí por qué las cebras necesitaban ser el grupo mayoritario (para mostrar el efecto de manada) y cómo el +1.0 del depredador justifica los momentos de persecución. Todo tiene una razón de ser basada en la cadena alimenticia. |
| Comprendo y puedo modificar el funcionamiento técnico del sistema.                |    20%   |       **18/20**      | Logré modificar el código para que las figuras rotaran según su dirección y entendí cómo la fricción frena las partículas. Igual me bajé porque todavía me cuesta un poco la matemática pura detrás de cambiar la visión circular por un "cono de visión". |
| El sistema produce variaciones con una identidad reconocible.                     |    15%   |       **15/15**      | Gracias al botón de la semilla aleatoria, probé muchísimas veces y el sistema jamás se repite exactamente igual. Sin embargo, al ver la pantalla, se sabe de una que es la sabana viva por cómo se mueven las formas, los colores y las agrupaciones (que ciertamente es evidente por el estilo que tieen) por lo que la identidad es súper fuerte. |
| Experimenté, comparé, seleccioné y descarté con criterios claros.                 |    10%   |       **10/10**      | Me pongo la nota completa porque hice muchas variantes y regresé varias veces al resultado con el que me sentía más cómodo y de ahí fui por varios caminos. |
| Puedo distinguir y sustentar lo diseñado y lo emergente.                          |    10%   |       **10/10**       | Sé que yo diseñé las "físicas" del mundo (quién ve a quién, a qué distancia y qué fricción hay), pero que las figuras de "nubes" que forman las cebras o las rutas en zigzag son totalmente emergentes. |
| **Total**                                                                         | **100%** | **97/100 (4.85/5.0)** |  |

**Nota:** 4.85


# Presentación

### Mi intención en una frase:
Quiero explorar la tensión constante entre buscar refugio en el grupo (cooperación) y el pánico de huir para salvarse (competencia y vulnerabilidad).

### Una relación central de la matriz y el comportamiento esperado:
La relación más importante de mi matriz es la asimetría entre las cebras y los cocodrilos. El cocodrilo tiene una atracción fuerte de +1.0 hacia la cebra, y la cebra tiene una repulsión de -1.0 (o más, dependiendo del modo) hacia el cocodrilo; además, las cebras se atraen entre sí con +0.2. Al programar esto, yo esperaba ver un contraste súper claro: momentos de mucha calma donde las cebras se juntan a comer pasto (comportamiento de manada), interrumpidos bruscamente por explosiones de caos donde rompen el grupo para huir apenas entra un depredador en su radio de visión.

### Comparación de un resultado seleccionado con un descarte:
En las siguientes imagenes se puede observar como se ve finalmente el proyecto ya con todo, pero en el codigo descartado (quitando de lado lo visual), podemos ver el frenetismo de todo comparado al final.

<img width="822" height="817" alt="image" src="https://github.com/user-attachments/assets/0fcdbc54-bb4b-4255-bc7d-bb1e11efbe3b" />

<img width="910" height="812" alt="image" src="https://github.com/user-attachments/assets/84ff0534-989d-49e0-ad7a-afa8e2483f53" />

### Qué parte fue diseñada y qué parte emergió:
Lo que yo diseñé fueron únicamente las reglas invisibles: los radios de visión, la fricción del suelo, la velocidad máxima y quién se siente atraído o repelido por quién. Lo que surgió fue el comportamiento de los animales y el pasto al ser "liberados"cumpliendo obviamente con las reglas que les impuse.

### Una decisión técnica que cambiaría y por qué:
Si volviera a hacer el proyecto, cambiaría la forma en que ven las partículas. Ahorita calculan la distancia usando un radio circular (360 grados), lo que significa que un cocodrilo o una cebra tiene "ojos en la nuca" y reacciona a cosas que tiene detrás. Técnicamente cambiaría eso para implementar un "cono de visión" (digamos, de 120 grados hacia el frente usando vectores). Lo haría porque haría el sistema mucho más realista y permitiría comportamientos emergentes nuevos, como que el depredador pueda acercarse con sigilo por la espalda de la presa sin que esta se dé cuenta hasta que se voltea.

