# Módulo 3.2 — Matrices de rotación
> **Fuente:** MATLAB Aplicado a Robótica y Mecatrónica — Fernando Reyes Cortés (Cap. 3)

---

## Idea constructiva

Las columnas de una matriz de rotación son los **destinos de cada eje coordenado** después de la rotación. Si rotas 90° alrededor de Z:

- Eje X → $(0, 1, 0)$
- Eje Y → $(-1, 0, 0)$
- Eje Z → $(0, 0, 1)$ — no se mueve, es el eje de rotación

$$R_z(90°) = \begin{pmatrix} 0 & -1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix}$$

---

## Matrices de rotación generales

$$R_x(\theta) = \begin{pmatrix} 1 & 0 & 0 \\ 0 & \cos\theta & -\sin\theta \\ 0 & \sin\theta & \cos\theta \end{pmatrix}$$

$$R_y(\theta) = \begin{pmatrix} \cos\theta & 0 & \sin\theta \\ 0 & 1 & 0 \\ -\sin\theta & 0 & \cos\theta \end{pmatrix}$$

$$R_z(\theta) = \begin{pmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{pmatrix}$$

**Patrón:** la fila y columna del eje de rotación tienen 1 en la diagonal y 0 en el resto.

---

## Por qué $R_y$ tiene el signo invertido

El orden cíclico dextrógiro es $X \to Y \to Z \to X$:

- $R_z$: plano $X \to Y$ — orden natural
- $R_x$: plano $Y \to Z$ — orden natural
- $R_y$: plano $Z \to X$ — orden **invertido** respecto a $X \to Z$

Mantener la regla de la mano derecha consistente obliga a voltear el signo negativo en $R_y$.

---

## Propiedades fundamentales — grupo $SO(3)$

Las matrices de rotación pertenecen al grupo especial ortogonal $SO(3)$, definido por:

### 1. Ortogonalidad

$$R \cdot R^T = I \implies R^{-1} = R^T$$

Invertir una rotación es simplemente **transponerla** — geométricamente es el viaje de regreso. Computacionalmente muy eficiente.

### 2. Determinante unitario

$$\det(R) = +1$$

Derivación: de $R \cdot R^T = I$ se sigue $\det(R)^2 = 1$, por tanto $\det(R) = \pm 1$. El $+1$ distingue rotaciones puras de reflexiones — en robótica siempre $+1$.

---

## Regla de la mano derecha

Para determinar el sentido positivo de rotación alrededor de un eje: apuntar el pulgar derecho en la dirección positiva del eje — los dedos indican el sentido positivo de rotación.

Ejemplo: $R_x(90°)$ sobre $\mathbf{v} = (0,1,0)$: el pulgar apunta en $+X$, los dedos van de $Y$ hacia $Z$, entonces el vector termina en $(0, 0, 1)$.

---

## Resumen de propiedades

| Propiedad | Expresión |
|-----------|-----------|
| Inversa = transpuesta | $R^{-1} = R^T$ |
| Determinante | $\det(R) = +1$ |
| Columnas ortonormales | cada columna es unitaria y ortogonal a las demás |
| Conserva longitudes | $\|R\mathbf{v}\| = \|\mathbf{v}\|$ |

---

*Siguiente módulo: **3.3 — Reglas de rotación compuesta***
