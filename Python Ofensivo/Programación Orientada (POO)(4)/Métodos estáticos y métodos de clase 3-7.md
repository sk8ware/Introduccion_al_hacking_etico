

----
- TAG: #Staticmethod #Classmethod
----

Los métodos estáticos y los métodos de clase son dos herramientas poderosas en la programación orientada a objetos en Python, que ofrecen flexibilidad en cómo se puede acceder y utilizar la funcionalidad asociada con una clase.

**Métodos de Clase**

Se definen con el decorador ‘**@classmethod**‘, lo que les permite tomar la clase como primer argumento, generalmente nombrada ‘**cls**‘. Este acceso a la clase permite que los métodos de clase interactúen con la estructura de la clase en sí, como modificar atributos de clase que afectarán a todas las instancias. Se utilizan para tareas que requieren conocimiento del estado global de la clase, como la construcción de instancias de maneras específicas, también conocidos como métodos factory.

**Métodos Estáticos**

Se definen con el decorador ‘**@staticmethod**‘ y no reciben un argumento implícito de referencia a la clase o instancia. Son similares a las funciones regulares definidas dentro del cuerpo de una clase. Se utilizan para funciones que, aunque conceptualmente pertenecen a la clase debido a la relevancia temática, no necesitan acceder a ningún dato específico de la clase o instancia. Proporcionan una manera de encapsular la funcionalidad dentro de una clase, manteniendo la cohesión y la organización del código.

Ambos métodos contribuyen a un diseño de software más limpio y modular, permitiendo una clara separación entre la funcionalidad que opera con respecto a la clase en su totalidad y la funcionalidad que es independiente de las instancias de clase y de la clase misma. La elección entre utilizar un método de clase o un método estático a menudo depende del requisito específico de acceso o no a la clase o a sus instancias.

---

>Para comprender mejor los conceptos de métodos estáticos y de clase en Python, vamos a analizar tres ejemplos adicionales: una calculadora simple utilizando métodos estáticos, una clase de automóviles utilizando métodos de clase, y una clase de estudiantes que emplea tanto métodos estáticos como de clase para gestionar la creación y listado de estudiantes mayores de edad.

### 1. Calculadora con Métodos Estáticos

Los métodos estáticos son útiles cuando no necesitamos acceder a ningún atributo de instancia o de clase. Solo realizan operaciones que no dependen del estado de un objeto en particular.

En este ejercicio no usaremos `self` ya que no estamos empleando objetos y por otro lado no son métodos de las instancias, son simplemente métodos estáticos que no juegan con objetos y únicamente operan con valores que correspondan a las variables de las clases o valores que le pasemos como argumentos

```python
#!/usr/bin/python3

class Calculadora:

	@staticmethod
	def suma(num1, num2):
		return num1 + num2

	@staticmethod
	def resta(num1, num2):
		return num1 - num2

	@staticmethod
	def multiplicacion(num1, num2):
		return num1 * num2

	@staticmethod
	def division(num1, num2):
		return num1 / num2 if num2 != 0 else "\n[!] Error: No se puede dividir un número entre cero\n"

print(Calculadora.suma(2, 8))
print(Calculadora.resta(8, 4))
print(Calculadora.multiplicacion(5, 10))
print(Calculadora.division(8,0))
```

Este código define una clase llamada `Calculadora` que contiene varios métodos estáticos para realizar operaciones aritméticas básicas. A continuación, te explico cada parte del código:


```python
#!/usr/bin/python3
```

Esta línea es una shebang que indica al sistema operativo que use el intérprete de Python 3 para ejecutar este script.

```python
class Calculadora:
```

Define una nueva clase llamada `Calculadora`.

```python
	@staticmethod     
	def suma(num1, num2):        
		return num1 + num2
```

Este es un método estático, marcado con el decorador `@staticmethod`, que toma dos números (`num1` y `num2`) como argumentos y retorna su suma.

```python
	@staticmethod     
	def resta(num1, num2):         
		return num1 - num2
```

Este es otro método estático que toma dos números como argumentos y retorna su resta (`num1` menos `num2`).

```python
	@staticmethod   
	def multiplicacion(num1, num2):         
		return num1 * num2
```

Este método estático toma dos números como argumentos y retorna su multiplicación.

```python
	@staticmethod     
	def division(num1, num2):        
		return num1 / num2 if num2 != 0 else "\n[!] Error: No se puede dividir un número entre cero\n"
```

Este método estático toma dos números como argumentos y retorna su división (`num1` dividido por `num2`). Si `num2` es 0, retorna un mensaje de error indicando que no se puede dividir por cero.

```python
print(Calculadora.suma(2, 8)) 
print(Calculadora.resta(8, 4)) 
print(Calculadora.multiplicacion(5, 10)) 
print(Calculadora.division(8, 0))
```

Estas líneas llaman a cada uno de los métodos estáticos definidos en la clase `Calculadora` y imprimen los resultados:

1. `Calculadora.suma(2, 8)` suma 2 y 8, retornando 10.
2. `Calculadora.resta(8, 4)` resta 4 de 8, retornando 4.
3. `Calculadora.multiplicacion(5, 10)` multiplica 5 por 10, retornando 50.
4. `Calculadora.division(8, 0)` intenta dividir 8 por 0, pero dado que no se puede dividir por cero, retorna un mensaje de error.

Cuando ejecutas este código, el resultado será:

```yaml
10 
4 
50  

[!] Error: No se puede dividir un número entre cero
```

Esto muestra los resultados de las operaciones aritméticas y el manejo de la división por cero con un mensaje de error.

### 2. Clase de Automóviles con Métodos de Clase

Los métodos de clase son útiles cuando necesitamos acceder o modificar el estado de la clase, es decir, operar sobre atributos que son compartidos por todas las instancias de la clase.

con la función `cls` tenemos acceso a información de la clase, para realizar una propia llamada a la clase `Automovil` donde le pase marca y el modelo
Utilizamos `self` ya que estamos tratando con un objeto en especifico, asi que para ello debemos saber que tipo de objeto es 
La función `cls` información de la clase como primer argumento

```python
#!/usr/bin/python

class Automovil:

	def __init__(self, marca, modelo):
		self.marca = marca
		self.modelo = modelo

	@classmethod
	def deportivos(cls, marca):
		
		return cls(marca, "Deportivo")
		
	@classmethod
	def sean(cls, marca):
		return cls(marca, "Sean")
		
	def __str__(self):
		return f"La marca {self.marca} es un modelo {self.modelo}"

deportivo = print(Automovil.deportivos("Ferrari")) # Automovil("Ferrari", "Deportivo")
sean = print(Automovil.sean("Toyota")) # Automovil("Toyota", "Sean")
```

Este código define una clase llamada `Automovil` que incluye métodos para crear instancias de automóviles con modelos específicos. A continuación, te explico cada parte del código:

```python
#!/usr/bin/python
```

Esta línea es una shebang que indica al sistema operativo que use el intérprete de Python para ejecutar este script.

```python
class Automovil:
```

Define una nueva clase llamada `Automovil`.

```python
	def __init__(self, marca, modelo):         
		self.marca = marca         
		self.modelo = modelo
```

Este es el método constructor `__init__`. Se ejecuta automáticamente cuando se crea una nueva instancia de `Automovil`. Inicializa los atributos del automóvil:

- `marca`: la marca del automóvil.
- `modelo`: el modelo del automóvil.

```python
	@classmethod     
	def deportivos(cls, marca):         
		return cls(marca, "Deportivo")
```

Este es un método de clase, marcado con el decorador `@classmethod`. Crea y retorna una nueva instancia de `Automovil` con la marca especificada y el modelo "Deportivo".

```python
	@classmethod     
	def sean(cls, marca):         
		return cls(marca, "Sean")
```

Este es otro método de clase que crea y retorna una nueva instancia de `Automovil` con la marca especificada y el modelo "Sean".

```python
	def __str__(self):         
		return f"La marca {self.marca} es un modelo {self.modelo}"
```

Este es un método especial `__str__` que se llama cuando se intenta convertir la instancia del objeto en una cadena de texto (por ejemplo, cuando se usa `print`). Retorna una cadena que describe la marca y el modelo del automóvil.

```python
deportivo = print(Automovil.deportivos("Ferrari")) # Automovil("Ferrari", "Deportivo") 
sean = print(Automovil.sean("Toyota")) # Automovil("Toyota", "Sean")
```

Estas líneas crean instancias de `Automovil` usando los métodos de clase `deportivos` y `sean`, y luego imprimen los resultados:

1. `Automovil.deportivos("Ferrari")` crea una instancia de `Automovil` con la marca "Ferrari" y el modelo "Deportivo".
2. `Automovil.sean("Toyota")` crea una instancia de `Automovil` con la marca "Toyota" y el modelo "Sean".

Las instancias se imprimen inmediatamente, llamando al método `__str__` de cada instancia, lo cual genera las siguientes salidas:

```zsh
La marca Ferrari es un modelo Deportivo 
La marca Toyota es un modelo Sean
```

Esto indica que los métodos de clase han creado correctamente las instancias de `Automovil` y que el método `__str__` ha sido llamado para proporcionar una representación en cadena de estas instancias.


### 3. Clase de Estudiantes con Métodos Estáticos y de Clase

Este ejemplo muestra cómo usar tanto métodos estáticos como de clase para gestionar la creación de estudiantes y listar los que son mayores de edad.

Uno que opere con variables de clases, todas las instancias u objetos creados pueden acceder o se compartir ese valor con todas las instancias

Vamos a crear una clases que se llame estudiantes, creamos una lista internamente 

Incomporamos nuevos elementos a una lista con `.append`, pero solo queremos incorporar `nuevos alumnos` que sean igual o mayores a 18 años 

Jugamos primeramente con un método de clase, que se llame crear_estudiante donde verifiquemos si es mayor de edad, podríamos jugar con igualdad ahi o podríamos jugar estatic method para considerar si es mayor o no, lo cual lo definimos por arriba y definimos lo siguiente

Ahora listaremos todos los menores de edad en el siguiente ejemplo:

```python
#!/usr/bin/python3

class Estudiantes:

	estudiantes = []
	
	def __init__(self, nombre, edad):
		self.nombre = nombre
		self.edad = edad
		
		Estudiantes.estudiantes.append(self)
		
	@staticmethod
	def es_mayor_de_edad(edad):
		return edad >= 18
		
	@classmethod
	def crear_estudiante(cls, nombre, edad):
		if cls.es_mayor_de_edad(edad):
			return cls(nombre, edad)
		else:
			print(f"\n[!] Error: El estudiante {nombre} es menor de edad\n")

Estudiantes.crear_estudiante("hackermate", 43)
Estudiantes.crear_estudiante("sk8ware", 25)
Estudiantes.crear_estudiante("Xerosec", 12)
Estudiantes.crear_estudiante("Hackavis", 8)
```

Este código define una clase llamada `Estudiantes` que gestiona una lista de estudiantes y proporciona métodos para crear instancias de estudiantes con validación de edad. A continuación, explico cada parte del código:

```python
#!/usr/bin/python3
```

Esta línea es una shebang que indica al sistema operativo que use el intérprete de Python 3 para ejecutar este script.

```python
class Estudiantes:     
	estudiantes = []
```

Define una clase `Estudiantes` con una variable de clase `estudiantes` que es una lista vacía al inicio.

```python
	def __init__(self, nombre, edad):         
		self.nombre = nombre         
		self.edad = edad         
		Estudiantes.estudiantes.append(self)
```

El método `__init__` es el constructor de la clase. Se ejecuta automáticamente cuando se crea una nueva instancia de `Estudiantes`. Inicializa los atributos `nombre` y `edad` del estudiante y luego agrega el objeto estudiante actual (`self`) a la lista `estudiantes` de la clase.

```python
	@staticmethod     
	def es_mayor_de_edad(edad):         
		return edad >= 18
```

Este es un método estático `es_mayor_de_edad` que toma un parámetro `edad` y verifica si es mayor o igual a 18. Retorna `True` si es mayor de edad y `False` si no lo es.

```python
	@classmethod     
	def crear_estudiante(cls, nombre, edad):         
		if cls.es_mayor_de_edad(edad):             
			return cls(nombre, edad)         
		else:             
			print(f"\n[!] Error: El estudiante {nombre} es menor de edad\n")
```

Este es un método de clase `crear_estudiante` que crea una nueva instancia de `Estudiantes` con el nombre y edad proporcionados, si el estudiante es mayor de edad según el método estático `es_mayor_de_edad`. Si el estudiante es menor de edad, imprime un mensaje de error.

```python
Estudiantes.crear_estudiante("hackermate", 43) 
Estudiantes.crear_estudiante("sk8ware", 25) 
Estudiantes.crear_estudiante("Xerosec", 12) 
Estudiantes.crear_estudiante("Hackavis", 8)
```

Estas líneas crean varios estudiantes utilizando el método `crear_estudiante` y pasan el nombre y la edad como argumentos. Aquí están los resultados esperados para cada llamada:

1. `"hackermate", 43`: Crea un estudiante llamado "hackermate" con 43 años de edad. Como es mayor de edad, se crea correctamente.
2. `"sk8ware", 25`: Crea un estudiante llamado "sk8ware" con 25 años de edad. Como es mayor de edad, se crea correctamente.
3. `"Xerosec", 12`: Intenta crear un estudiante llamado "Xerosec" con 12 años de edad. Como es menor de edad, imprime un mensaje de error.
4. `"Hackavis", 8`: Intenta crear un estudiante llamado "Hackavis" con 8 años de edad. Como es menor de edad, imprime un mensaje de error.

Por lo tanto, la salida esperada de este código sería:

```yaml
[!] Error: El estudiante Xerosec es menor de edad  

[!] Error: El estudiante Hackavis es menor de edad
```

Los estudiantes "hackermate" y "sk8ware" serían agregados a la lista `estudiantes` de la clase `Estudiantes`, mientras que los otros dos no, debido a la validación de edad.

----

También tenemos la manera de crear la función `mostrar_estudiantes` para poder listar todos los estudiantes dentro de la lista 

```python
#!/usr/bin/python3

class Estudiantes:

    estudiantes = []

    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad 
        
        Estudiantes.estudiantes.append(self)
        
    @staticmethod
    def es_mayor_de_edad(edad):
        return edad >= 18 
        
    @classmethod
    def crear_estudiante(cls, nombre, edad):
        if cls.es_mayor_de_edad(edad):
            return cls(nombre, edad)
        else:
            print(f"\n[!] Error: El estudiante {nombre} es menor de edad")
    
    @staticmethod
    def mostrar_estudiantes():
        for i, estudiante in enumerate(Estudiantes.estudiantes):
            print(f"\t[+] Estudiante número [{i+1}]: {estudiante.nombre}")
            

Estudiantes.crear_estudiante("Hackermate", 43)
Estudiantes.crear_estudiante("Sk8ware", 25)
Estudiantes.crear_estudiante("Xerosec", 12)
Estudiantes.crear_estudiante("Hackavis", 8)
Estudiantes.crear_estudiante("Lobotec", 1)

print("\n[i] Listando los estudiantes existentes:\n")

Estudiantes.mostrar_estudiantes()

```

El código define la clase `Estudiantes`, que gestiona una lista de estudiantes y ofrece métodos para crear estudiantes, verificar si son mayores de edad, y mostrar la lista de estudiantes creados. A continuación, explicaré cada parte del código y luego mostraré la salida esperada:

```python
#!/usr/bin/python3
```

La línea de shebang indica al sistema operativo que debe usar el intérprete de Python 3 para ejecutar este script.

```python
class Estudiantes:     
	estudiantes = []
```

Define una clase `Estudiantes` con una variable de clase `estudiantes` que es una lista vacía al inicio.

```python
	def __init__(self, nombre, edad):         
		self.nombre = nombre         
		self.edad = edad          
		Estudiantes.estudiantes.append(self)
	```

El método `__init__` es el constructor de la clase. Se ejecuta automáticamente cuando se crea una nueva instancia de `Estudiantes`. Inicializa los atributos `nombre` y `edad` del estudiante y luego agrega el objeto estudiante actual (`self`) a la lista `estudiantes` de la clase.

```python
	@staticmethod     
	def es_mayor_de_edad(edad):         
		return edad >= 18
```

Este es un método estático `es_mayor_de_edad` que toma un parámetro `edad` y verifica si es mayor o igual a 18. Retorna `True` si es mayor de edad y `False` si no lo es.

```python
	@classmethod     
	def crear_estudiante(cls, nombre, edad):         
		if cls.es_mayor_de_edad(edad):             
			return cls(nombre, edad)         
		else:             
			print(f"\n[!] Error: El estudiante {nombre} es menor de edad")
	```

Este es un método de clase `crear_estudiante` que crea una nueva instancia de `Estudiantes` con el nombre y edad proporcionados, si el estudiante es mayor de edad según el método estático `es_mayor_de_edad`. Si el estudiante es menor de edad, imprime un mensaje de error.

```python
	@staticmethod     
	def mostrar_estudiantes():         
		for i, estudiante in enumerate(Estudiantes.estudiantes):             
		print(f"\t[+] Estudiante número [{i+1}]: {estudiante.nombre}")
```

Este es un método estático `mostrar_estudiantes` que recorre la lista de estudiantes y muestra el nombre de cada estudiante junto con un índice numerado.

```python
Estudiantes.crear_estudiante("Hackermate", 43) 
Estudiantes.crear_estudiante("Sk8ware", 25) 
Estudiantes.crear_estudiante("Xerosec", 12) 
Estudiantes.crear_estudiante("Hackavis", 8) 
Estudiantes.crear_estudiante("Lobotec", 1)
```

Estas líneas crean varios estudiantes utilizando el método `crear_estudiante` y pasan el nombre y la edad como argumentos.

```python
print("\n[i] Listando los estudiantes existentes:\n") 
Estudiantes.mostrar_estudiantes()
```

Finalmente, estas líneas imprimen un encabezado y luego llaman al método estático `mostrar_estudiantes` para listar y mostrar todos los estudiantes creados.

La salida esperada de este código será:

```less
[!] Error: El estudiante Xerosec es menor de edad 
[!] Error: El estudiante Hackavis es menor de edad  

[i] Listando los estudiantes existentes:      

	[+] Estudiante número [1]: Hackermate     
	[+] Estudiante número [2]: Sk8ware     
	[+] Estudiante número [3]: Lobotec
```

Explicación de la salida:

- Se intenta crear estudiantes con las edades 12, 8, y 1, lo que resulta en mensajes de error porque son menores de edad.
- Luego se lista solo los estudiantes válidos (mayores de edad) que fueron agregados correctamente a la lista `estudiantes` de la clase `Estudiantes`.