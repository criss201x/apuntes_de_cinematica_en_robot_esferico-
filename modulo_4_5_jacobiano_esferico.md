# Módulo 4.5 — Cinemática diferencial y Jacobiano
> **Fuente:** MATLAB Aplicado a Robótica y Mecatrónica — Fernando Reyes Cortés (Cap. 4)

---

## El problema diferencial

La cinemática directa relaciona posiciones. El Jacobiano relaciona **velocidades**:

$$\dot{\mathbf{p}} = J \cdot \dot{\mathbf{q}}$$

donde:
- $\dot{\mathbf{p}} = (\dot{x}, \dot{y}, \dot{z})^T$ — velocidad cartesiana del efector
- $\dot{\mathbf{q}} = (\dot{\theta}_1, \dot{\theta}_2, \dot{d}_3)^T$ — velocidades articulares
- $J$ — matriz Jacobiana

---

## Construcción del Jacobiano

El Jacobiano es la matriz de derivadas parciales de la posición respecto a las variables articulares:

$$J = \begin{pmatrix} \frac{\partial x}{\partial \theta_1} & \frac{\partial x}{\partial \theta_2} & \frac{\partial x}{\partial d_3} \\ \frac{\partial y}{\partial \theta_1} & \frac{\partial y}{\partial \theta_2} & \frac{\partial y}{\partial d_3} \\ \frac{\partial z}{\partial \theta_1} & \frac{\partial z}{\partial \theta_2} & \frac{\partial z}{\partial d_3} \end{pmatrix}$$

---

## Jacobiano del robot esférico

Partiendo de $x = -d_3\sin\theta_1$, $y = d_3\cos\theta_1$, $z = d_1$:

**Columna 2 ($\theta_2$):** $\theta_2$ no aparece en ninguna ecuación de posición → columna de ceros.

**Fila 3 ($z$):** $z = d_1$ es constante → fila de ceros.

**Derivadas no nulas:**

$$\frac{\partial x}{\partial \theta_1} = -d_3\cos\theta_1 \qquad \frac{\partial y}{\partial \theta_1} = -d_3\sin\theta_1$$

$$\frac{\partial x}{\partial d_3} = -\sin\theta_1 \qquad \frac{\partial y}{\partial d_3} = \cos\theta_1$$

### Jacobiano completo

$$\boxed{J = \begin{pmatrix} -d_3\cos\theta_1 & 0 & -\sin\theta_1 \\ -d_3\sin\theta_1 & 0 & \cos\theta_1 \\ 0 & 0 & 0 \end{pmatrix}}$$

---

## Interpretación de las columnas

| Columna | Variable | Significado físico |
|---|---|---|
| 1 | $\dot{\theta}_1$ | Velocidad del efector al girar la base |
| 2 | $\dot{\theta}_2$ | Cero — $\theta_2$ no mueve el efector |
| 3 | $\dot{d}_3$ | Velocidad al extender el brazo — vector unitario $(-\sin\theta_1, \cos\theta_1)^T$ |

La tercera columna es un vector unitario: extender el brazo una unidad mueve el efector exactamente en la dirección en que apunta.

---

## Singularidades cinemáticas

Una singularidad ocurre cuando $\det(J) = 0$ — el robot pierde capacidad de moverse en alguna dirección cartesiana.

### Singularidad estructural del robot esférico

La tercera fila es siempre cero → $\det(J) = 0$ **para cualquier configuración**.

Este robot está en singularidad permanente en posición — no puede moverse verticalmente. Es una consecuencia directa de la geometría: los tres ejes se intersectan en un punto y el brazo vive en el plano horizontal.

### Tipos de singularidad

| Tipo | Causa | Efecto |
|---|---|---|
| Estructural | Geometría del robot — fila/columna siempre cero | Dirección permanentemente inaccesible |
| De frontera | Brazo completamente extendido o retraído | Pérdida de movilidad en el límite del espacio de trabajo |
| Interna | Configuración específica del robot | Pérdida temporal de una dirección |

---

## Resumen del capítulo 4

| Módulo | Pregunta que responde |
|---|---|
| 4.1 Clasificación | ¿Qué tipo de robot es y cuántos GDL tiene? |
| 4.2 D-H | ¿Cómo asigno marcos y construyo cada $T_{i-1,i}$? |
| 4.3 Cinemática directa | Dadas las articulaciones, ¿dónde está el efector? |
| 4.4 Cinemática inversa | Dado el punto deseado, ¿cuánto muevo cada articulación? |
| 4.5 Jacobiano | Dadas las velocidades articulares, ¿con qué velocidad se mueve el efector? |

---

*Fin del Capítulo 4*
