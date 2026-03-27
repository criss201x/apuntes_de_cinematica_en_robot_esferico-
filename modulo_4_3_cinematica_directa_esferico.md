# Módulo 4.3 — Cinemática directa: obtención de $T_{03}$
> **Fuente:** MATLAB Aplicado a Robótica y Mecatrónica — Fernando Reyes Cortés (Cap. 4)

---

## Objetivo

Obtener una sola matriz $T_{03}$ que exprese la posición y orientación del efector en función de las tres variables articulares $\theta_1$, $\theta_2$ y $d_3$.

$$T_{03} = T_{01}(\theta_1) \cdot T_{12}(\theta_2) \cdot T_{23}(d_3)$$

---

## Notación compacta

$$c_i = \cos\theta_i \qquad s_i = \sin\theta_i$$

---

## Paso 1 — $T_{02} = T_{01} \cdot T_{12}$

### Regla de composición de traslaciones

$$\mathbf{d}_{02} = \mathbf{d}_{01} + R_{01} \cdot \mathbf{d}_{12}$$

- $\mathbf{d}_{01}$: lleva del origen al marco 1
- $R_{01} \cdot \mathbf{d}_{12}$: traslación del eslabón 2 rotada por la orientación del eslabón 1

Como $\mathbf{d}_{12} = (0,0,0)^T$, la traslación de $T_{02}$ es simplemente $(0, 0, d_1)^T$.

### Resultado

$$T_{02} = \begin{pmatrix} c_1 c_2 & -c_1 s_2 & -s_1 & 0 \\ s_1 c_2 & -s_1 s_2 & c_1 & 0 \\ -s_2 & -c_2 & 0 & d_1 \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

---

## Paso 2 — $T_{03} = T_{02} \cdot T_{23}$

$T_{23}$ solo traslada a lo largo de $z_2$ una distancia $d_3$. La tercera columna de $R_{02}$ es $(-s_1, \ c_1, \ 0)^T$, entonces:

$$\mathbf{d}_{03} = \begin{pmatrix} 0 \\ 0 \\ d_1 \end{pmatrix} + d_3 \begin{pmatrix} -s_1 \\ c_1 \\ 0 \end{pmatrix} = \begin{pmatrix} -d_3 s_1 \\ d_3 c_1 \\ d_1 \end{pmatrix}$$

### Resultado final

$$\boxed{T_{03} = \begin{pmatrix} c_1 c_2 & -c_1 s_2 & -s_1 & -d_3 s_1 \\ s_1 c_2 & -s_1 s_2 & c_1 & d_3 c_1 \\ -s_2 & -c_2 & 0 & d_1 \\ 0 & 0 & 0 & 1 \end{pmatrix}}$$

---

## Posición del efector final

La columna de traslación de $T_{03}$ da la posición cartesiana del efector:

$$\mathbf{p} = \begin{pmatrix} x \\ y \\ z \end{pmatrix} = \begin{pmatrix} -d_3 \sin\theta_1 \\ d_3 \cos\theta_1 \\ d_1 \end{pmatrix}$$

---

## Interpretación geométrica

| Variable | Controla | Tipo de efecto |
|---|---|---|
| $\theta_1$ | Giro horizontal del brazo | Posición: $x$ e $y$ |
| $d_3$ | Extensión del brazo | Posición: radio en $xy$ |
| $\theta_2$ | Orientación del efector | Solo orientación — no posición |

### Por qué $\theta_2$ no afecta la posición

El eje $z_2$ (dirección de extensión del brazo) está contenido en el plano $XY$ — siempre apunta al horizonte. $\theta_2$ rota el efector pero no desplaza su origen. Con $d_3$ fijo, el efector solo puede trazar un **círculo horizontal** de radio $d_3$ a altura $d_1$.

$\theta_2$ aparece en el bloque de rotación de $T_{03}$ pero no en la columna de traslación — es un grado de libertad de **orientación pura**.

---

## Espacio de trabajo

Con $d_{3,min} \leq d_3 \leq d_{3,max}$ y $\theta_1 \in [0°, 360°)$, el efector puede alcanzar cualquier punto de una **corona circular** a altura $z = d_1$.

---

*Siguiente módulo: **4.4 — Cinemática inversa***
