# Practico 1 - Ejercicio 10
Dado $n \in \mathbb N$, consideremos la integral:
$$I_n = \int_0^1 \frac{x^n}{5 + x} dx$$

1. Verificar que $I_0 = \log(6/5)$ y que, para todo $n ≥ 1$, se tiene $I_n ≥ 0$ y se cumple la relación
$$I_n + 5I_{n-1} = \frac{1}{n}$$

 **Solución:**
Para $n = 0$, la integral queda de la forma
$$I_0 = \int_0^1 \frac{x^0}{5 + x} dx = \int_0^1 \frac{1}{5 + x} = \left[\log(5 + x)\right]^1_0 = \log (6) - \log (5) = \log \left(\frac{6}{5}\right)$$

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
I # -3.6669e+04
```

La salida obtenida es $I_30 = -3.6669e+04$ lo cual contradice lo demostrado en el punto anterior donde $I_n \ge 0$ para todo $n \ge 0$, por lo que se concluye que el resultado no es confiable. 
Además se observa en la recurrencia que es una resta de valores menores a $1$, por lo que obtener un resultado con un exponente $+4$ significa que un calculo fallo y disparo el resultado. 

Si se analiza el error hacia adelante del problema tenemos que 
$$y_0 = 1/n, \quad f(y_o,I_{n-1}) = y_0 - 5 I_{n-1}$$

La expresión $y_0 = \frac{1}{n}$ esta bien condicionada ya que $k_{y_0}(n) = 1$.

Para ver como se propaga el error de $I_{n-1}$ a lo largo de las operaciones, se estudia el numero de condición de la función según $I_{n-1}$
$$k_f(I_{n-1}) = \left| \frac{(f'(I_{n-1}) \cdot I_{n-1})}{f(I_{n-1})} \right| = \left| \frac{(-5) I_{n-1}}{1/n - 5 I_{n-1}} \right| = \frac{5 I_{n-1}}{I_n}$$

Al calcular el error relativo inevitable que se produce al computar se obtiene que
$$|\varepsilon_f| \le \frac{\varepsilon_M}{2} + \frac{5 I_{n-1}}{I_{n}} |\varepsilon_{I_{n-1}}|$$

Se puede observar que la expresión utilizada para encontrar $I_{30}$ esta mal condicionada ya que $k_f > 1$, y a medida que se avanza en la recurrencia el error va aumentando con un factor mayor que $5$ ($I_{n-1} / I_n > 0$). A su vez, se arrastra el error de operaciones anteriores a través de $|\varepsilon_{I_{n-1}}|$ por lo que error arrastrado aumenta exponencialmente con $n$.

Por lo que en un punto de la recurrencia, el error arrastrado fue tan grande que provoco que los valores se dispararan afectando al valor de $I_{30}$.

---
3. Como alternativa, se propone comenzar aproximando $I_{100} = 0$ y utilizar la fórmula de recurrencia hacia atrás. Computar $I_{30}$ de esta manera. Probar con otras aproximaciones iniciales para $I_{100}$, como por ejemplo $I_{100} = 0,1$, $I_{100} = 1$. Explicar qué ocurre y por qué.

**Solución:**

```octave
I = 0;
for n = 100:-1:30
    I = 1/5 * (1/n - I);
end
I # 5.5857e-03

I = 0.1;
for n = 100:-1:30
    I = 1/5 * (1/n - I);
end
I # 5.5857e-03

I = 1;
for n = 100:-1:30
    I = 1/5 * (1/n - I);
end
I # 5.5857e-03
```

En este caso la función implementada en el problema es 
$$I_{n-1} = \frac{1}{5} \left( \frac{1}{n} - I_n \right)$$
Si se realiza el mismo estudio que se realizo en el punto anterior llegamos a la expresión
$$k_f(I_{n-1}) = \left| \frac{(f'(I_{n-1}) \cdot I_{n-1})}{f(I_{n-1})} \right| = \left| \frac{(-1/5) I_{n-1}}{1/5 \cdot (1/n - I_{n-1})} \right| = \frac{I_{n}}{5I_{n-1}}$$

Por lo que el error inevitable al computar la expresión queda de la forma
$$|\varepsilon_f| \le \frac{\varepsilon_M}{2} + \frac{I_{n}}{5 I_{n-1}} |\varepsilon_{I_{n-1}}|$$

Se puede observar que en este caso $k_f < 1$, por lo que la expresión esta bien condicionada, no solo eso sino que el error disminuye con un factor mayor que 5 ($\frac{I_{n}}{5 I_{n-1}} < 1$).
El comportamiento de que independientemente de si $I_{100} = 0$ o $I_{100}$ = 0.1 o $I_{100} = 1$ de el mismo resultado se debe a lo mencionado anteriormente, como $k_f < 1$ a medida que avanza la recurrencia el error se va amortiguando hasta que llega un punto que no afecta al resultado de $I_{30}$.

