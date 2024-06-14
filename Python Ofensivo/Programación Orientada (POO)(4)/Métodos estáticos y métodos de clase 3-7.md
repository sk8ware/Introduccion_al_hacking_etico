

----
- TAG:
----

Los métodos estáticos y los métodos de clase son dos herramientas poderosas en la programación orientada a objetos en Python, que ofrecen flexibilidad en cómo se puede acceder y utilizar la funcionalidad asociada con una clase.

**Métodos de Clase**

Se definen con el decorador ‘**@classmethod**‘, lo que les permite tomar la clase como primer argumento, generalmente nombrada ‘**cls**‘. Este acceso a la clase permite que los métodos de clase interactúen con la estructura de la clase en sí, como modificar atributos de clase que afectarán a todas las instancias. Se utilizan para tareas que requieren conocimiento del estado global de la clase, como la construcción de instancias de maneras específicas, también conocidos como métodos factory.

**Métodos Estáticos**

Se definen con el decorador ‘**@staticmethod**‘ y no reciben un argumento implícito de referencia a la clase o instancia. Son similares a las funciones regulares definidas dentro del cuerpo de una clase. Se utilizan para funciones que, aunque conceptualmente pertenecen a la clase debido a la relevancia temática, no necesitan acceder a ningún dato específico de la clase o instancia. Proporcionan una manera de encapsular la funcionalidad dentro de una clase, manteniendo la cohesión y la organización del código.

Ambos métodos contribuyen a un diseño de software más limpio y modular, permitiendo una clara separación entre la funcionalidad que opera con respecto a la clase en su totalidad y la funcionalidad que es independiente de las instancias de clase y de la clase misma. La elección entre utilizar un método de clase o un método estático a menudo depende del requisito específico de acceso o no a la clase o a sus instancias.

---
# Métodos estáticos

De manera de reforzar lo aprendido vamos a realizar otro ejercicio creando una simple calculadora

En este ejercicio no usaremos `self` ya que no estamos empleando objetos y por otro lado no son métodos de las instancias, son simplemente métodos estáticos que no juegan con objetos y unicamente operan con valores que correspondan a las variables de las clases o valores que le pasemos como argumentos

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

# Métodos de clase

Ahora lo veremos empleando la manera método de clase 

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


Uno que opere con variables de clases, todas las instancias u objetos creados pueden acceder o se comparte ese valor con todas las instancias

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


También tenemos la manera de crear la función `mostrar_estudiantes` para poder listar todos los estudiantes dentro de la lista 

```python
#!/usr/bin/python3

class Estudiantes:

	estudianres = []
	
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
			print(f"\n[!] Error: El estudiante {nobre} es menor de edad")

Estudiantes.crear_estudiante("Hackermate", 43)
Estudiantes.crear_estudiante("Sk8ware", 25)
Estudiantes.crear_estudiante("Xerosec", 12)
Estudiantes.crear_estudiante("Hackavis", 8)
Estudiantes.crear_estudiante("Lobotec", 1)

print("\n[i] Listando los estudiantes existentes:\n")

Estudiantes.mostrar_estudiantes()
```


