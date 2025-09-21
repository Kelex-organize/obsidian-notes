# Interval Scheduling
Descripción del problema

### Algoritmo
1. Ordenar todos los intervalos por su tiempo de finalización.
2. Inicializar ``A = vacio``
3. Recorrer los intervalos en orden
	- Si el inicio del intervalo actual `s_i <= ultimo_fin`, `agregar a A` y actualizar `ultimo_fin = f_i`.
	- En caso contrario, descártalo.
```
Interval-Scheduling(R)
	Ordenar R por f(i) creciente
	A = vacío 
	ultimo_fin = -∞
	for cada intervalo (s,f) en R en ese orden do
		if s >= ultimo_fin then
			agregar (s,f) a A
			ultimo_fin = f
return A
```
- Ordenamiento: $O(n \log n)$.
- Selección: $O(n)$.
- **Total:** $O(n \log n)$.
### Optimalidad
Explicacion con el algoritmo de exchange argument

### Ejemplo
Entrada: [(4,6), (1,3), (6,7), (2,5)]
1. Ordenamiento por fecha fin: [(1,3), (2,5), (4,6), (6,7)]
2. Selección greedy:
	- (1,3) → seleccionado.
	- (2,5) → descartado (solapa con (1,3)).
	- (4,6) → seleccionado.
	- (6,7) → seleccionado.
Salida: [(1,3), (4,6), (6,7)]

# Earliest-Deadline-First
Descripción del problema

### Algoritmo
1. Ordenar las tareas por si fecha límite creciente.
2. Ejecutarlas en orden.
	- Si el tiempo que se acumula al ejecutar las tareas es menor a la fecha límite de la tarea evaluada, no hay retraso
	- Si no se cumple, la tarea esta retrasada.
```
Earliest-Deadline-Fist(T)
	Ordenar T por fecha límite creciente
	tiempo = 0
	restrasos = 0
	for cada tarea t en T do
		tiempo = tiempo = t.ejecucion
		if tiempo > t.deadline then
			marcar t como retrasada
			retrasos = retrasos + 1
return secuencia, retrasos
```
- Ordenamiento: $O(n \log n)$.
- Ejecutar tareas: $O(n)$.
- **Total:** $O(n \log n)$.
### Optimalidad
Explicacion con el algoritmo de exchange argument

### Ejemplo
Entradas: [A(4,6), B(2,8), C(3,9), D(1,5)] (tiempo, fecha límite)
1. Ordenamiento por fecha límite: [D(1,5), A(4,6), B(2,8), C(3,9)]
2. Programamos en ese orden:
	- D: termina en tiempo 1 (antes de 5 ✅).
	- A: termina en tiempo 5 (antes de 6 ✅).
	- B: termina en tiempo 7 (antes de 8 ✅).
	- C: termina en tiempo 10 (después de 9 ❌ retrasada).
Salida: Solo una tarea retrasada C
Si se hubieran echo en otro orden (por ejemplo A, B, C, D), habría más tareas retrasadas.

# Algoritmo Dijkstra


### Algoritmo



```
Dijkstra(G, s, t)
	for cada nodo v en V do
		d[v] = ∞
		prev[v] = None
	d[s] = 0
	
	Q = todos los nodos (cola de prioridad con clave d[v])
	
	while Q no vacío do
		u = extraer nodo con menor d[u]
		if u == t then 
			break;
		for cada (u,v) en E do
			if d[u] + peso(u,v) < d[v] then
				d[v] = d[u] + peso(u,v)
				prev[v] = u
				actualizar prioridad de v en Q
```

### Optimalidad


### Ejemplo









