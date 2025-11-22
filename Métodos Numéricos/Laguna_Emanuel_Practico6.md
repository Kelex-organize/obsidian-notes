# Practico 6 - Ejercicio 2
Dada una función $f$ con una singularidad (integrable) en un punto $x_0$, de la que se conoce de qué forma $f(x) \rightarrow \infty$ cuando $x \rightarrow x_0$, una forma de obtener una regla de cuadratura adaptada, que utilice más nodos cerca de $x_0$, es realizando un cambio de variable adecuado.

1. Sea $f(x) = \frac{e^x}{\sqrt{x}}$. Se quiere estimar
$$I = \int_0^1 f(x)dx \approx 2,9253$$
Como $f(x) \rightarrow \infty$ con $x \rightarrow 0^+$, usar una regla de trapecio compuesta como en el Ejercicio 1 para estimar $I$ arrojaría infinito como resultado. Sin embargo, también vale que 
$$\int_0^{10^{-10}}f(x)dx \approx 2 \cdot10^{-5}$$
Por lo tanto, se podría aplicar una regla de cuadratura en el intervalo $[10^{-10}, 1]$ para obtener una aproximación de $I$ correcta hasta el quinto dígito. Usar el comando `trapecio(f, 1e-10, 1, n)` para estimar $I$ usando $n = {10^2, 10^3, 10^4, 10^5, 10^6}$. ¿Qué tan precisos son los resultados obtenidos?


2. Realizar la sustitución $t = sqrt x$ en (1) para expresar $I$ con la integral de otra función, que llamaremos $g(t)$. Observar que $g \in C([0, 1])$. Correr `trapecio(g, 0, 1, n)` con los mismos valores de n que en la parte anterior y comparar los resultados obtenidos.

3. Obtener cotas para el error de cuadratura para los enfoques de las partes anteriores. Para entender por qué el enfoque de la parte (b) produce mejores resultados que el de la parte a, notar cómo cambian los nodos equiespaciados 
$$0 = t_1 \le \dots \le t_n = 1$$
con el cambio de variables realizado.
