# Módulos 4.1 y 4.2 — Clasificación de robots y convención Denavit-Hartenberg
> **Fuente:** MATLAB Aplicado a Robótica y Mecatrónica — Fernando Reyes Cortés (Cap. 4)

---

## 4.1 — Clasificación de robots industriales

### Tipos de articulaciones

| Símbolo | Tipo | Movimiento | Variable |
|---|---|---|---|
| R | Rotacional | Giro alrededor de un eje | $\theta_i$ |
| P | Prismática | Traslación a lo largo de un eje | $d_i$ |

### Grados de libertad (GDL)
Número de articulaciones = número de variables independientes = dimensión del espacio de juntas.

### Configuraciones canónicas

| Configuración | Notación | Espacio de trabajo |
|---|---|---|
| Cartesiana | PPP | Cúbico |
| Cilíndrica | RPP | Cilíndrico |
| Esférica | RRP | Esférico |
| SCARA | RRP | Cilíndrico acotado |
| Antropomórfica | RRR | Irregular (mayor alcance) |

---

## 4.2 — Convención Denavit-Hartenberg (D-H)

### El problema que resuelve
Dado un robot con $n$ articulaciones, D-H define un método sistemático para asignar marcos de referencia y construir cada matriz $T_{i-1,i}$ con exactamente **4 parámetros**.

### Los 4 parámetros D-H

| Parámetro | Símbolo | Qué describe |
|---|---|---|
| Longitud del eslabón | $a_i$ | Distancia entre ejes $z_{i-1}$ y $z_i$ a lo largo de $x_i$ |
| Desplazamiento | $d_i$ | Distancia a lo largo de $z_{i-1}$ hasta el origen del marco $i$ |
| Ángulo de torsión | $\alpha_i$ | Ángulo entre $z_{i-1}$ y $z_i$ alrededor de $x_i$ |
| Ángulo de articulación | $\theta_i$ | Ángulo de rotación alrededor de $z_{i-1}$ |

**Regla clave:**
- Articulación **R** → $\theta_i$ es la variable, $d_i$ constante
- Articulación **P** → $d_i$ es la variable, $\theta_i$ constante

### Matriz D-H general

$$T_{i-1,i} = \begin{pmatrix} \cos\theta_i & -\sin\theta_i\cos\alpha_i & \sin\theta_i\sin\alpha_i & a_i\cos\theta_i \\ \sin\theta_i & \cos\theta_i\cos\alpha_i & -\cos\theta_i\sin\alpha_i & a_i\sin\theta_i \\ 0 & \sin\alpha_i & \cos\alpha_i & d_i \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

- Bloque $3\times3$ superior izquierdo → rotación compuesta ($\theta_i$ y $\alpha_i$)
- Columna superior derecha → traslación ($a_i$ y $d_i$)

---

## Aplicación al robot esférico (RRP)

### Tabla D-H

| Eslabón | $a_i$ | $d_i$ | $\alpha_i$ | $\theta_i$ | Variable |
|---|---|---|---|---|---|
| 1 (R) | $0$ | $d_1$ | $90°$ | $\theta_1$ | $\theta_1$ |
| 2 (R) | $0$ | $0$ | $-90°$ | $\theta_2$ | $\theta_2$ |
| 3 (P) | $0$ | $d_3$ | $0°$ | $0$ | $d_3$ |

### Por qué $a_i = 0$ en todos los eslabones
Los ejes de las tres articulaciones se **intersectan en un punto común** — por eso no hay distancia entre ejes. Esta es la condición geométrica que genera el espacio de trabajo esférico.

### Por qué $\alpha_1 = 90°$
Sin la torsión de 90°, J1 y J2 girarían alrededor del mismo eje — se desperdiciaría un grado de libertad. El $\alpha_1 = 90°$ hace que J2 controle la elevación del brazo mientras J1 controla el giro horizontal.

### Matrices individuales

$$T_{01} = \begin{pmatrix} \cos\theta_1 & 0 & \sin\theta_1 & 0 \\ \sin\theta_1 & 0 & -\cos\theta_1 & 0 \\ 0 & 1 & 0 & d_1 \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

$$T_{12} = \begin{pmatrix} \cos\theta_2 & 0 & -\sin\theta_2 & 0 \\ \sin\theta_2 & 0 & \cos\theta_2 & 0 \\ 0 & -1 & 0 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

$$T_{23} = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & d_3 \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

$T_{23}$ tiene el bloque de rotación igual a la identidad — la articulación prismática no rota, solo traslada a lo largo de $z_2$.

### Cinemática directa
$$T_{03} = T_{01}(\theta_1) \cdot T_{12}(\theta_2) \cdot T_{23}(d_3)$$

---

*Siguiente módulo: **4.3 — Cinemática directa: obtención de $T_{03}$***
