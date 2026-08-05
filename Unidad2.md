# Proceso

<img width="915" height="821" alt="image" src="https://github.com/user-attachments/assets/5f1a1c4a-b838-452a-a5af-5ae6637d7471" />

<img width="913" height="810" alt="image" src="https://github.com/user-attachments/assets/ac3ecb24-05ab-4a33-bae5-0131c92db774" />

<img width="913" height="828" alt="image" src="https://github.com/user-attachments/assets/566d8b83-5607-441e-b9bc-7b4ec35d0a48" />

<img width="917" height="817" alt="image" src="https://github.com/user-attachments/assets/59abc2e5-aac1-4037-ab1b-979884586142" />

<img width="912" height="830" alt="image" src="https://github.com/user-attachments/assets/199429ef-4fb8-4ccb-864a-151e332f57af" />

<img width="832" height="820" alt="image" src="https://github.com/user-attachments/assets/7a26f2f7-c77c-4ebe-ace0-ff3d10484ead" />










# Autoevluación  

| **Criterio**                                                                      | **Peso** |    **Valoración**    | **Aporte / Justificación**                                                                                                                                                                                         |
| --------------------------------------------------------------------------------- | :------: | :------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| La intención es clara y perceptible en el comportamiento.                         |    20%   |       **0/20**      |                       |
| Los tipos, cantidades, matriz y parámetros están justificados desde la intención. |    25%   |       **0/25**      | |
| Comprendo y puedo modificar el funcionamiento técnico del sistema.                |    20%   |       **0/20**      |             |
| El sistema produce variaciones con una identidad reconocible.                     |    15%   |       **0/15**      |                                                                |
| Experimenté, comparé, seleccioné y descarté con criterios claros.                 |    10%   |       **0/10**      |                                   |
| Puedo distinguir y sustentar lo diseñado y lo emergente.                          |    10%   |       **0/10**       |                                 |
| **Total**                                                                         | **100%** | **0/100 (0/5.0)** |                              |

**Nota:** 0


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

