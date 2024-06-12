
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

	def __init__(self, nombre, edad): # Persona.__init__(marcelo, nombre, edad)
	
		self.nombre = nombre
		self.edad = edad 
		
	def saludo(self): # Persona.saludo(anthony)
		
		return f"Hola, soy {self.nombre} y tengo {self.edad} años"
	
marcelo = Persona("Marcelo", 28)
print(marcelo.saludo())
```