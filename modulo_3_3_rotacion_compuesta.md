# Módulo 3.3 — Reglas de rotación compuesta
> **Fuente:** MATLAB Aplicado a Robótica y Mecatrónica — Fernando Reyes Cortés (Cap. 3)

---

## Principio fundamental

La multiplicación de matrices de rotación **no es conmutativa**:

$$R_z \cdot R_x \neq R_x \cdot R_z$$

El orden en que se aplican las rotaciones define completamente la postura final. Este es uno de los conceptos más críticos de la cinemática de robots.

---

## Composición de rotaciones

La rotación total de $n$ rotaciones aplicadas en secuencia es el producto matricial en orden de aplicación — **de derecha a izquierda**:

$$R_{total} = R_n \cdots R_2 \cdot R_1$$

$R_1$ se aplica primero, $R_n$ al final.

---

## Dos interpretaciones según el marco de referencia

| Interpretación | Marco | Orden de multiplicación |
|---|---|---|
| Ejes **fijos** (globales) | El marco no cambia | Pre-multiplicar: $R_{nuevo} = R_i \cdot R_{actual}$ |
| Ejes **locales** (del cuerpo) | El marco gira con el cuerpo | Post-multiplicar: $R_{nuevo} = R_{actual} \cdot R_i$ |

---

## Cadena cinemática

Para un robot con articulaciones $R_1, R_2, R_3$ sobre **ejes locales**:

$$R_{total} = R_1 \cdot R_2 \cdot R_3$$

Lectura: $R_1$ se aplica primero. El eje de $R_2$ ya no es el eje global — es el eje que quedó después de que $R_1$ transformó el sistema. Cada articulación hereda el marco de la anterior.

> En la convención D-H siempre se trabaja con ejes locales.

---

## Por qué el orden importa — intuición

Rota un libro 90° sobre Z (lo giras en la mesa) y luego 90° sobre X (lo inclinas hacia ti). Invierte el orden: primero 90° sobre X, luego 90° sobre Z. El resultado final es diferente — la orientación del libro no es la misma en ambos casos.

---

*Siguiente módulo: **3.4 — Transformaciones de traslación***
