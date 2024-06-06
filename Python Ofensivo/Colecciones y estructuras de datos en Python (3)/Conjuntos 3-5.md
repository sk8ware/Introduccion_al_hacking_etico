
----
- TAG:
----

En esta clase, nos adentraremos en los conjuntos, conocidos en Python como ‘**sets**‘. Los conjuntos son una colección de elementos sin orden y sin elementos repetidos, inspirados en la teoría de conjuntos de las matemáticas. Son ideales para la gestión de colecciones de elementos únicos y operaciones que requieren eliminar duplicados o realizar comparaciones de conjuntos.

**Características de los Conjuntos**

- **Unicidad**: Los conjuntos automáticamente descartan elementos duplicados, lo que los hace perfectos para recolectar elementos únicos.
- **Desordenados**: A diferencia de las listas y las tuplas, los conjuntos no mantienen los elementos en ningún orden específico.
- **Mutabilidad**: Los elementos de un conjunto pueden ser agregados o eliminados, pero los elementos mismos deben ser inmutables (por ejemplo, no puedes tener un conjunto de listas, ya que las listas se pueden modificar).

**Operaciones con Conjuntos**

Exploraremos las operaciones básicas de conjuntos que Python facilita, como:

- **Adición y Eliminación**: Añadir elementos con ‘**add()**‘ y eliminar elementos con ‘**remove()**‘ o ‘**discard()**‘.
- **Operaciones de Conjuntos**: Realizar uniones, intersecciones, diferencias y diferencias simétricas utilizando métodos o operadores respectivos.
- **Pruebas de Pertenencia**: Comprobar rápidamente si un elemento es miembro de un conjunto.
- **Inmutabilidad Opcional**: Usar el tipo ‘**frozenset**‘ para crear conjuntos que no se pueden modificar después de su creación.

**Uso de Conjuntos en Python**

- **Eliminación de Duplicados**: Son útiles cuando necesitas asegurarte de que una colección no tenga elementos repetidos.
- **Relaciones entre Colecciones**: Facilitan la comprensión y el manejo de relaciones matemáticas entre colecciones, como subconjuntos y superconjuntos.
- **Rendimiento de Búsqueda**: Proporcionan una búsqueda de elementos más rápida que las listas o las tuplas, lo que es útil para grandes volúmenes de datos.

**Buenas Prácticas**

Discutiremos cuándo es beneficioso usar conjuntos en lugar de otras estructuras de datos y cómo su uso puede influir en la eficiencia del programa.

Al final de esta clase, tendrás una comprensión completa de los conjuntos en Python y cómo pueden ser utilizados para hacer tu código más eficiente y lógico, aprovechando sus propiedades únicas para manejar datos. Con este conocimiento, podrás implementar estructuras de datos complejas y operaciones que requieren lógica de conjuntos.

---
En este blog ya hemos visto las **Listas**, **Tuplas** y ahora veremos los **Conjuntos**(sets) y cada uno de ellos se emplean los diferentes signos `[]`, `()`, `{}`

Dentro de las llaves simplemente abrimos y escribimos nuestro conjunto, pero tomen en cuenta que aquí no se puede enumerar los espacios como lo hacíamos con las Listas y las Tuplas, por otro lado los conjuntos, los elementos tienen que ser únicos, no se pueden repetir elementos iguales ni tampoco los números.

```python
#!/usr/bin/python3

mi_conjunto = {1, 2, 3}

print(mi_conjunto)
```

A los conjuntos les podemos agregar nuevos elementos con `.add()`, pero no siempre se van agregar de manera ordenada ya que si empleamos el siguiente ejercicio se darán cuenta que al numero 8 lo manda al inicio

```python
#!/usr/bin/python3

mi_conjunto = {1, 2, 3}
mi_conjunto.add(8)

print(mi_conjunto)
```

Podemos agregar más elementos con `.update({})`

```python
#!/usr/bin/python3

mi_conjunto = {1, 2, 3}
mi_conjunto.update({4, 5, 6})

print(mi_conjunto)
```

Dentro de toda esta lista que hemos creado podemos eliminar algún elemento en especificó con `.remove()`

```python
#!/usr/bin/python3

mi_conjunto = {1, 2, 3}
mi_conjunto.add(8)

mi_conjunto.remove(3)

print(mi_conjunto)
```

Si deseamos imprimir código de una manera mas limpia podemos emplear la función `.discard()`, esto permitirá que cuando refleje algún tipo de error no nos muestre el stderr y cuando si exista elimine ese elemento 

```python
#!/usr/bin/python3

mi_conjunto = {1, 2, 3, 4, 5, 6}

mi_conjunto.discard(7)

print(mi_conjunto)
```

Adicional podemos crear intercepciones entre conjuntos con `.intersection` para mostrar todos los elementos repetidos dentro de nuestro conjunto

```python
#!/usr/bin/python3

mi_primer_conjunto = {1, 2, 3, 4, 5}
mi_segundo_conjunto = {3, 4, 5, 6, 7}

conjunto_final = mi_primer_conjunto.intersection(mi_segundo_conjunto)

print(conjutno_final)
```

Algo interesante es que también se pueden crear uniones con `.union()` y organizar todos los elementos del conjunto

```python
#!/usr/bin/python3

mi_primer_conjunto = {1, 2, 3, 4, 5}
mi_segundo_conjunto = {2, 9, 1, 8, 15}

conjunto_final = mi_primer_conjunto.union(mi_segundo_conjunto)

print(conjutno_final)
```

Al momento de imprimir veremos que esta organizado, pero no siempre hay confiar ya que como les había explicado en los **Conjuntos** no esta creado para organizar de manera automática, es probable que mas adelante con otros ejercicios si que muestre ese error.

Con los conjuntos también podemos identificar si un conjunto es un subconjunto de otro conjunto y se los estaré explicando de la siguiente manera con `.issubset()`:

```python
#!/usr/bin/python3

primer_conjunto = {1, 2, 3}
segundo_conjunto = {1, 2, 3, 4, 5}

print(primer_conjunto.issubset(segundo_conjunto))
```

Aquí nos mostraría es que es **True** ya que todos los elementos del primer conjunto existen en el segundo conjunto, si faltara tan solo un elemento saldría **False**, no importa el orden  siempre y cuando existan en el conjunto

Esto pasa de igual manera con los nombres.

¿Para qué nos puede servir los conjuntos ?

Crearemos una lista con números para poderlo imprimir con la función `set()` imprimir un conjunto sin las repeticiones de la lista

```python
#!/usr/bin/python

mi_lista = [1, 5, 4, 6, 5, 1, 2, 3, 8, 12, 14, 12, 1, 1]

no_repeat = set(mi_lista)
print(no_repeat)
```

Si lo deseamos convertir a una lista simplemente lo colocamos el `list()` antes de `set()`
```python
#!/usr/bin/python

mi_lista = [1, 5, 4, 6, 5, 1, 2, 3, 8, 12, 14, 12, 1, 1]

no_repeat = list(set(mi_lista))
print(no_repeat)
```

Estos ejercicios nos benefician para la búsqueda de un conjunto pues es mas eficiente que buscarlo en una lista 
Para ello podemos convertir una lista en un conjunto para poder buscar información en ella por ejemplo si existe el número `1234`

Lo aplicamos de la siguiente manera para saber si este valor existe no mostrara un valor booleano con el valor **True en caso de existir** y **False en caso de no existir**

```python
#!/usr/bin/python3

mi_conjunto = set(range(10000))

print(1234 in mi_conjunto)
```

Y para operar con conjuntos es mucho más practico como les mostraré a continuación:

Imaginen si desean saber que usuario están en ambas plataformas

```python
#!/usr/bin/python3

usuarios_facebook = {"Ana", "Sk8ware", "Hackermate", "Lobotec"}
usuarios_X = {"Hackermate", "Sk8ware", "Manolo", "Chichico"}

ambas_plataformas = usuarios_facebook.intersection(usuarios_X)

print(ambas_plataformas)
```

Si deseamos imprimir todos los usuarios de ambas plataformas utilizamos la función `.union()` para que no se repitan y se muestren en un solo conjutno

```python
#!/usr/bin/python3

usuarios_facebook = {"Ana", "Sk8ware", "Hackermate", "Lobotec"}
usuarios_X = {"Hackermate", "Sk8ware", "Manolo", "Chichico"}

ambas_plataformas = usuarios_facebook.intersection(usuarios_X)
todos_los_usuarios = usuarios_facebook.union(usuarios_X)

print(todos_los_usuarios)
```

Cuando lo imprimos en la mayoria de los casos suele imprimir en desorden cada vez que lo imprimimos, cuidado con el orden 

Tenemos una caracteristica o utilidad que esta interesante que es `.difference()`
Para que nos muestre las diferncias entre plataformas, es decir los que no estan repetidos

```python
#!/usr/bin/python3

usuarios_facebook = {"Ana", "Sk8ware", "Hackermate", "Lobotec"}
usuarios_X = {"Hackermate", "Sk8ware", "Manolo", "Chichico"}

ambas_plataformas = usuarios_facebook.intersection(usuarios_X)
todos_los_usuarios = usuarios_facebook.union(usuarios_X)
diferencias_entre_plataformas = usuarios_facebook.difference(usuarios_X)

print(todos_los_usuarios)
```

Nos mostrará la diferencia únicamente de la lista de Facebook contra la de usuarios X, si desean lo pueden invertir de la siguiente manera para obtener el mismo resultado con Usuarios X

```python
#!/usr/bin/python3

usuarios_facebook = {"Ana", "Sk8ware", "Hackermate", "Lobotec"}
usuarios_X = {"Hackermate", "Sk8ware", "Manolo", "Chichico"}

ambas_plataformas = usuarios_facebook.intersection(usuarios_X)
todos_los_usuarios = usuarios_facebook.union(usuarios_X)
diferencias_entre_plataformas = usuarios_X.difference(usuarios_facebook)

print(difencias_entre_plataformas)
```

De esta manera pueden listar elementos que no se repitan con la lista de comparación de facebook. 
