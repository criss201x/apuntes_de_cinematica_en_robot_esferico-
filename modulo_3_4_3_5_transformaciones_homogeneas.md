# Módulos 3.4 y 3.5 — Traslación y transformaciones homogéneas
> **Fuente:** MATLAB Aplicado a Robótica y Mecatrónica — Fernando Reyes Cortés (Cap. 3)

---

## 3.4 — El problema de la traslación

Una matriz de rotación $R$ de $3\times3$ solo puede rotar. Para describir la posición completa de un eslabón respecto a otro se necesita también trasladar:

$$\mathbf{p}_1 = R \cdot \mathbf{p}_2 + \mathbf{d}$$

donde $\mathbf{d} = (p_x, p_y, p_z)^T$ es el vector de traslación entre orígenes.

**Problema:** esta operación mezcla multiplicación matricial con suma vectorial. No se pueden encadenar varias transformaciones como un producto simple — se rompe la posibilidad de tratar cada eslabón como un solo bloque matemático.

---

## 3.5 — Transformación homogénea

### El truco algebraico

Se extiende el espacio de 3D a 4D agregando una coordenada artificial igual a 1:

$$\mathbf{p} = \begin{pmatrix} x \\ y \\ z \end{pmatrix} \longrightarrow \tilde{\mathbf{p}} = \begin{pmatrix} x \\ y \\ z \\ 1 \end{pmatrix}$$

Con esto, la operación $R\mathbf{p} + \mathbf{d}$ se convierte en una **sola multiplicación matricial**:

$$\begin{pmatrix} \mathbf{p}_1 \\ 1 \end{pmatrix} = \underbrace{\begin{pmatrix} R & \mathbf{d} \\ \mathbf{0}^T & 1 \end{pmatrix}}_{T \ (4\times4)} \begin{pmatrix} \mathbf{p}_2 \\ 1 \end{pmatrix}$$

### Estructura de la matriz $T$

$$T = \begin{pmatrix} r_{11} & r_{12} & r_{13} & d_x \\ r_{21} & r_{22} & r_{23} & d_y \\ r_{31} & r_{32} & r_{33} & d_z \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

| Bloque | Dimensión | Contenido |
|---|---|---|
| $R$ | $3\times3$ superior izquierda | Rotación pura |
| $\mathbf{d}$ | $3\times1$ superior derecha | Traslación |
| $\mathbf{0}^T$ | $1\times3$ inferior izquierda | Siempre ceros |
| $1$ | escalar inferior derecha | Siempre 1 |

### Por qué funciona para encadenar

La fila $(\mathbf{0}^T \quad 1)$ garantiza que el producto de dos matrices homogéneas produce otra matriz homogénea con la misma estructura. La cadena se cierra sobre sí misma:

$$T_{02} = T_{01} \cdot T_{12}$$

Generalizado para una cadena de $n$ eslabones:

$$T_{0n} = T_{01} \cdot T_{12} \cdots T_{n-1,n}$$

Esta es la expresión central de la **cinemática directa**.

### Inversa de una transformación homogénea

$$T^{-1} = \begin{pmatrix} R^T & -R^T\mathbf{d} \\ \mathbf{0}^T & 1 \end{pmatrix}$$

Se aprovecha que $R^{-1} = R^T$ — no se necesita invertir la matriz completa.

---

## Conexión con lo anterior

| Módulo | Aporte a $T$ |
|---|---|
| 3.1 Producto interno | Define ortogonalidad — propiedad de las columnas de $R$ |
| 3.2 Matrices de rotación | El bloque $R$ de $3\times3$ |
| 3.3 Rotación compuesta | El orden del producto $T_{01} \cdot T_{12} \cdots$ |
| 3.4 Traslación | El vector $\mathbf{d}$ y la motivación de la matriz $4\times4$ |
| **3.5 Homogénea** | **Unifica todo en una sola operación matricial** |

---

*Siguiente capítulo: **Cap. 4 — Cinemática directa con Denavit-Hartenberg***
