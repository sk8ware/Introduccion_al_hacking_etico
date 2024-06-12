
----
- TAG: 
----
La Programación Orientada a Objetos (POO) es un paradigma de programación que utiliza objetos y clases en su enfoque central. Es una manera de estructurar y organizar el código que refleja cómo los desarrolladores piensan sobre el mundo real y las entidades dentro de él.

**Clases**

Las clases son los fundamentos de la POO. Actúan como plantillas para la creación de objetos y definen atributos y comportamientos que los objetos creados a partir de ellas tendrán. En Python, una clase se define con la palabra clave ‘**class**‘ y proporciona la estructura inicial para todo objeto que se derive de ella.

**Instancias de Clase y Objetos**

Un objeto es una instancia de una clase. Cada vez que se crea un objeto, se está creando una instancia que tiene su propio espacio de memoria y conjunto de valores para los atributos definidos por su clase. Los objetos encapsulan datos y funciones juntos en una entidad discreta.

**Métodos de Clase**

Los métodos de clase son funciones que se definen dentro de una clase y solo pueden ser llamados por las instancias de esa clase. Estos métodos son el mecanismo principal para interactuar con los objetos, permitiéndoles realizar operaciones o acciones, modificar su estado o incluso interactuar con otros objetos.

En esta clase, te proporcionaremos las herramientas y el entendimiento necesario para comenzar a diseñar y desarrollar tus propias clases y a crear instancias de esas clases en objetos funcionales. Aprenderemos cómo los métodos de clase operan y cómo puedes utilizarlos para dar vida al comportamiento de tus objetos en Python. Este conocimiento será esencial a medida que continúes aprendiendo y aplicando los principios de la POO en proyectos más complejos.

---
# Clases y objetos (1/2)

Ahora iremos con la parte practica creando un archivo `.py`
Y crearemos una clase que se llame animal y luego aplicaremos un método que no permite realizar una función interna de la maquina 
Hay un constructor cuando creamos un objeto, este objeto suele ser una instancia de la clase, suele haber el constructor para que se inicialice a través de unos atributos 

```python
#!/usr/bin/python3

class Persona:

	def __init__(self, nombre, edad): # Persona.__init__(anthony, nombre, edad)
	
		self.nombre = nombre
		self.edad = edad 
		
	def saludo(self): # Persona.saludo(anthony)
		
		return f"Hola, soy {self.nombre} y tengo {self.edad} años"
	
anthony = Persona("Anthony", 25)
print(anthony.saludo())
```

### Explicación Resumida

1. **Shebang**:
    
```python
#!/usr/bin/python3
```   
Indica que se use el intérprete de Python 3.
    
2. **Definición de la Clase `Persona`**:
    
 ```python
 class Persona:
 ```
    
3. **Método Constructor `__init__`**:
```pyhton
def __init__(self, nombre, edad):    
    self.nombre = nombre   
	self.edad = edad
```
    
- Inicializa los atributos `nombre` y `edad` al crear una instancia.

4. **Método `saludo`**:
    
  ```python
  def saludo(self):    
   return f"Hola, soy {self.nombre} y tengo {self.edad} años"
  ```
    
- Retorna un saludo con el nombre y la edad de la persona.

5. **Creación de la Instancia y Llamada al Método**:
```pyhton
   anthony = Persona("Anthony", 25) print(anthony.saludo())
```
    
- Crea una instancia `anthony` con nombre "Anthony" y edad 25.
- Imprime: "Hola, soy Anthony y tengo 25 años".

# Creando otro objeto 

Si deseamos crear otro objeto simplemente le agregamos un `silvia = Persona("Silvia", 48)` asi creamos una instancia de la clase, asi que esto pasa al constructor y entiende el parametro **nombre y edad**
Imprimimos en consola el resultado con `print(silvia.saludo())`

```python
#!/usr/bin/python3

class Persona:

	def __init__(self, nombre, edad): # Persona.__init__(anthony, nombre, edad)
	
		self.nombre = nombre
		self.edad = edad 
		
	def saludo(self): # Persona.saludo(anthony)
		
		return f"Hola, soy {self.nombre} y tengo {self.edad} años"
	
anthony = Persona("Anthony", 25)
silvia = Persona("Silvia", 48)

print(anthony.saludo())
print(silvia.saludo())
```

Ahora mostraremos otro ejercicio, con objetos totalmente independientes que tienen sus atributos definidos y sus propiedades, a los cuales podemos ingresar gracias a los métodos que hemos declarado , no hace falta poner un `return` también se puede usar la función `print`

```python
#!/usr/bin/python3

class Animal:

	def __init__(self, nombre, animal): # Animal.__init__(gato, nombre, animal)
	
		self.nombre = nombre
		self.animal = animal
		
	def descripcion(self): # Persona.saludo(anthony)
		
		print(f"{self.nombre} es un {self.animal}")
	
gato = Animal("Tijuana", "Gato")
perro = Animal("Pancho", "Perro")

gato.descripcion()
perro.descripcion()
```


# Ejercicio cuenta bancaria

Crearemos una clase **cuenta bancaria** e indicaremos unos valores que nosotros indiquemos para un cliente, donde el cliente es el objeto 

```python
#!/usr/bin/python3

class CuentaBancaria:

	def __init__(self, cuenta, nombre, dinero=0):
		self.cuenta = cuenta
		self.nombre = nombre
		self.dinero = dinero

	def depositar_dinero(self, dinero): # CuentaBancaria.depositar_dinero(manolo)
		self.dinero += dinero 
		
		return f"\n[+] Se han depositado {dinero} dolares, actualmente el balance de la cuenta es de {self.dinero} dolares"

manolo = CuentaBancaria("187263", "Manolo Vieira", 1000)
print(manolo.depositar_dinero(500))
```