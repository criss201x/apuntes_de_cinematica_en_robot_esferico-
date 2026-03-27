# Módulo 4.4 — Cinemática inversa
> **Fuente:** MATLAB Aplicado a Robótica y Mecatrónica — Fernando Reyes Cortés (Cap. 4)

---

## El problema inverso

Dado un punto deseado $(x, y, z)$ en el espacio cartesiano, encontrar las variables articulares $(\theta_1, \theta_2, d_3)$ que llevan el efector a ese punto.

Es la operación inversa a la cinemática directa:

$$\text{Directa: } (\theta_1, \theta_2, d_3) \longrightarrow (x, y, z)$$
$$\text{Inversa: } (x, y, z) \longrightarrow (\theta_1, \theta_2, d_3)$$

---

## Sistema de ecuaciones

De la cinemática directa del robot esférico:

$$x = -d_3 \sin\theta_1 \qquad y = d_3 \cos\theta_1 \qquad z = d_1$$

---

## Restricción estructural

$z = d_1$ es un parámetro fijo del robot — la altura del efector no es controlable. Si se pide $z \neq d_1$, la solución no existe. Es una restricción del espacio de trabajo, no un problema matemático.

---

## Solución para $d_3$

Elevando al cuadrado y sumando ambas ecuaciones:

$$x^2 + y^2 = d_3^2\sin^2\theta_1 + d_3^2\cos^2\theta_1 = d_3^2$$

$$\boxed{d_3 = \sqrt{x^2 + y^2}}$$

Interpretación geométrica: $d_3$ es la norma del vector $(x, y)$ — el radio en el plano horizontal.

---

## Solución para $\theta_1$

Dividiendo las ecuaciones para eliminar $d_3$:

$$\frac{x}{y} = -\tan\theta_1$$

$$\boxed{\theta_1 = \text{atan2}(-x, \ y)}$$

Se usa $\text{atan2}$ (no $\arctan$) para preservar el cuadrante correcto. $\arctan$ solo devuelve valores en $(-90°, 90°)$ — perdería el signo de $x$ e $y$ por separado.

---

## Solución para $\theta_2$

$$\boxed{\theta_2 = \text{libre}}$$

$\theta_2$ no participa en la posición del efector — es un grado de libertad de orientación pura. Se asigna según la orientación deseada del efector.

---

## Solución completa

$$\theta_1 = \text{atan2}(-x, \ y) \qquad d_3 = \sqrt{x^2 + y^2} \qquad \theta_2 = \text{libre}$$

---

## Unicidad de la solución

El sistema tiene estructura de coordenadas polares — dado un punto $(x,y)$, el radio $d_3$ es único por definición de norma y el ángulo $\theta_1$ es único en $(-180°, 180°]$.

No hay soluciones múltiples porque no existe una segunda forma de expresar un punto en coordenadas polares con $d_3 > 0$. Contrasta con el robot antropomórfico RRR donde la cadena puede doblarse como "codo arriba" o "codo abajo" para el mismo punto — eso genera dos soluciones válidas.

---

## Comparación directa vs. inversa

| Aspecto | Cinemática directa | Cinemática inversa |
|---|---|---|
| Entrada | Variables articulares | Posición cartesiana |
| Salida | Posición cartesiana | Variables articulares |
| Unicidad | Siempre única | Puede tener 0, 1 o N soluciones |
| Complejidad | Álgebra directa | Requiere despejar — puede ser no lineal |

---

*Siguiente módulo: **4.5 — Cinemática diferencial y Jacobiano***
