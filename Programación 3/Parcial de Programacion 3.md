# Ejercicio 1

1. Definición de problema de emparejamiento estable:
**Solución:**
Consideramos un conjunto $M = \{m_1, m_2, ... , m_n\}$ y un conjunto $W = \{w_1, w_2, ... , w_n\}$. Un emparejamiento $S$ es un subconjunto del producto cartesiano $M \times W$, con la propiedad de que cada miembro de $M$ y cada miembro $W$ aparece como máximo un par en $S$. Un emparejamiento $S$ es perfecto si cada miembro de $M$ y cada miembro de $W$ aparece exactamente un par de $S$.

Cada $m \in M$ ordena a todos los elementos de $W$, y decimos que m prefiere a $w$ sobre $w'$ si $m$ ordena a $w$ en una posición más alta que a $w'$ en sus lista de preferencias. Análogamente, cada $w \in W$ ordena a todos los elementos de $M$.

El problema de emparejamiento estable se define como encontrar un emparejamiento perfecto entre $W$ y $M$ que no tenga inestabilidades. Una inestabilidad se define como un par $(m, w')$ tal que $(m, w)$ y $(m', w')$ se encuentran en $S$, pero m prefiere a $w'$ antes que a $w$, y $w'$ prefiere a m antes que a $m'$.

2. Diseñe un algoritmo que, dado un grafo dirigido $G$ y uno de sus nodos $s$, determine la componente fuertemente conexa que contiene a $s$. El algoritmo debe de ejecutarse en tiempo $O(m + n)$, donde $n$ es la cantidad de nodos y $m$ la cantidad de aristas del grafo. Puede asumir que tiene disponible una implementación de $DFS$ que retorna el conjunto de nodos alcanzables desde un nodo dado.
**Solución:**
```
Componente-Conexa(G, s)
	alanzables := DFS(G,s)
	Sea G^t el grafo transpuesto de G
	alcanzablesEnTranspuesto := DFS(D,s)
	componente := alcanzables union alcanzableEnTranspuesto
	
	return componente
```

3. Supongamos que en el algoritmo para el problema Particionamiento de intervalos que se ve en el curso se sustituye el criterio de ordenamiento y se eligen los intervalos en orden creciente de su tiempo de finalización. Muestre un contraejemplo en el que puede haber una ejecución del algoritmo en la que no se obtiene el resultado óptimo. Justifique por que no es óptimo.
**Solución:**
Intervalos (1,3), (4,6), (2,6). Se puede resolver con dos etiquetas. Pero puede haber una ejecución que asigne una etiqueta a (1,3), otra distancia (4,6) y entonces deja sin asignar (2,6).

4. Sea $G = (V,E)$ un grafo no dirigido en el que cada arista $e$ tiene asociado un costo $c_e$ mayor que cero, y supongamos que todos los costos de las aristas son distintos. Sea $S$ un subconjunto de $V$ no vacío y distinto de $V$, y sea $e = (v,w)$, con $v \in S$, $w \in V - S$ la arista de menor costo entre todas las que un extremo en $S$ y otro en $V - S$. Demuestre que c bada árbol de cubrimiento de costo mínimo de $G$ contiene la arista $e$.
**Solución:**
En esencia, supongamos para llegar a una contradicción que $T$ es un $MST$ que no contiene $(v,w)$. Por ser conexo, tiene que haber un camino, $P$, en $T$ que conecte $v$ con $w$. Como $v$ está en $S$ y $w \in V - S$ el camino $P$ debe incluir una arista $(v',w')$, con $v' \in S$ y $w'  \in V - S$. El grafo $(T \ (v', w')) \un (w,v)$ es conexo y tiene $n - 1$ aristas por lo que es un árbol de cubrimiento. Pero, por la hipótesis del costo de $(u,v)$, el costo de este árbol es menor que el de $T$, lo que contradice que $T$ sea de costo mínimo.

5. En el grafo de la figura indique en que orden elige las aristas los algoritmos de Prim y de Kruskal. Considere que el inicio es el vértice $1$ cuando corresponda.
![[Pasted image 20250919203008.png]]
**Solución:**







