# Practico 1 - Ejercicio 10
Dado $n \in \mathbb N$, consideremos la integral:
$$I_n = \int_0^1 \frac{x^n}{5 + x} dx$$

1. Verificar que $I_0 = log(6/5)$ y que, para todo $n ≥ 1$, se tiene $I_n ≥ 0$ y se cumple la relación
$$I_n + 5I_{n-1} = \frac{1}{n}$$

 **Solución:**
Para $n = 0$, la integral queda de la forma
$$I_0 = \int_0^1 \frac{x^0}{5 + x} dx = \int_0^1 \frac{1}{5 + x} = \left[\ln(5 + x)\right]^1_0 = \ln (6) - \ln (5) = \ln \left(\frac{6}{5}\right)$$

Para $n \ge 1$, la integral es de la forma
$$I_n = \int_0^1 \frac{x^n}{5 + x} dx$$

Rescribir la integral de manera que sea más sencillo resolverla
$$\frac{x^n}{5 + x} = \frac{x^{n - 1} \cdot x}{5 + x} = \frac{x^{n - 1} \cdot (x + 5 - 5)}{5 + x} = \frac{x^{n - 1} \cdot (x + 5) - 5x^{n-1}}{5 + x} = x^{n-1} - \frac{5x^{n-1}}{5 + x} \\ 
\quad \Rightarrow \quad I_n = \int_0^1 x^{n-1} - \frac{x^{n-1}}{5 + x} dx = \int_0^1x^{n-1} - 5\int_0^1\frac{x^{n-1}}{5 + x}$$

Observar que 
$$I_{n-1} = \int_0^1\frac{x^{n-1}}{5 + x}$$

Por lo que la integral se puede escribir de la siguiente manera
$$I_n = \int_0^1 x^{n-1} - 5I_{n-1} \quad \Rightarrow \quad I_n = \int_0^1 x^{n-1} - 5I_{n-1}$$

Resolviendo la integral que queda 
$$\int_0^1 x^{n-1} = \frac{1}{n}\left[ x^n\right]^1_0 = \frac{1}{n} (1-0) = \frac{1}{n} \quad \Rightarrow \quad I_n = \frac{1}{n} - 5 I_{n-1} \quad \Rightarrow \quad I_n + 5 I_{n-1}= \frac{1}{n} $$

Analizar el signo de $I_n$ para $n \ge 1$. El signo de $\frac{x^n}{5 + x}$ en el intervalo $[0,1]$:
- $x^n \ge 0$ para todo $n \ge 1$ en el intervalo $[0,1]$.
- $5+x \ge 0$ para todo $n \ge 1$ en el intervalo $[0,1]$.

Como la expresión es una división de dos valores positivos, se deduce que $\frac{x^n}{5 + x} \ge 0$ para todo $n \ge 1$. 
La integral de una función no negativa determina un crecimiento creciente, y como $I_0 = \ln (6/5) > 0$, podemos concluir que $I_n \ge 0$ para todo $n \ge 1$.

---
2. Escribir un programa de Octave que implemente la fórmula de recurrencia de la parte anterior y utilizarlo para calcular $I_{30}$. Analizar el resultado obtenido. ¿Es confiable? Justificar realizando un análisis de error hacia adelante.

**Solución:**
```octave
I = log(6/5);
for n = 1 : 30
	I = 1/n - 5.0*I;
end
disp(I) # -3.6669e+04
```

La salida obtenida es $I_30 = -3.6669e+04$ lo cual contradice lo demostrado en el punto anterior donde para todo $I_n \ge 0$ para todo $n \ge 0$, por lo que se concluye que el resultado no es confiable.

Al imprimir los valores de $I_n$ en cada paso se obtiene los siguientes valores:

| 1        | 2        | 3        | 4        | 5        | 6        | 7        | 8        | 9        | 10       |
| -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- |
| 0.088392 | 0.058039 | 0.043139 | 0.034306 | 0.028468 | 0.024325 | 0.021233 | 0.018837 | 0.016926 | 0.015368 |

| 11       | 12       | 13       | 14       | 15       | 16         | 17         | 18         | 19         |
| -------- | -------- | -------- | -------- | -------- | ---------- | ---------- | ---------- | ---------- |
| 0.014071 | 0.012977 | 0.012040 | 0.011229 | 0.010522 | 9.8903e-03 | 9.3719e-03 | 8.6960e-03 | 9.1515e-03 |

| 20         | 21       | 22        | 23     | 24      | 25     | 26      | 27     | 28      | 29     | 30          |
| ---------- | -------- | --------- | ------ | ------- | ------ | ------- | ------ | ------- | ------ | ----------- |
| 4.2426e-03 | 0.026406 | -0.086575 | 0.4764 | -2.3401 | 11.740 | -58.664 | 293.36 | -1466.7 | 7333.8 | -3.6669e+04 |






---
3. Como alternativa, se propone comenzar aproximando $I_{100} = 0$ y utilizar la fórmula de recurrencia hacia atrás. Computar $I_{30}$ de esta manera. Probar con otras aproximaciones iniciales para $I_{100}$, como por ejemplo $I_{100} = 0,1$, $I_{100} = 1$. Explicar qué ocurre y por qué.

**Solución:**

```octave
I = 0;
for n = 100:-1:30
    I = 1/5 * (1/n - I);
end
disp(I)
```













