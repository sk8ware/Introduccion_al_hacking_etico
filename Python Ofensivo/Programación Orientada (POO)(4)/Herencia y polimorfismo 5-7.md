
---
- TAG: #Herencia #Polimorfismo
----

La herencia y el polimorfismo son conceptos fundamentales en la programación orientada a objetos que permiten la creación de una estructura de clases flexible y reutilizable.

**Herencia**

Es un principio de la POO que permite a una clase heredar atributos y métodos de otra clase, conocida como su clase base o superclase. La herencia facilita la reutilización de código y la creación de una jerarquía de clases. Las subclases heredan las características de la superclase, lo que permite que se especialicen o modifiquen comportamientos existentes.

----
Para explicarlo de mejor manera vamos con la practica con unos pequeños ejemplos
1. Creamos un archivo nvim `exercise.py`
2. Creamos un ejemplo de clase utilizando la clase `Animal`

```python
#!/usr/bin/python3  # Indica que se debe usar Python 3 para ejecutar este script

class Animal:  # Definición de una clase llamada Animal
    def __init__(self, nombre):  # Constructor de la clase que inicializa el nombre del animal
        self.nombre = nombre  # Asigna el nombre pasado al crear el objeto a la variable de instancia

    def hablar(self):  # Método que hace que el animal "hable"
        print(f"{self.nombre} dice ¡Miau!")  # Imprime el nombre del animal seguido de "dice ¡Miau!"

gato = Animal("Mitis")  # Crea un nuevo objeto de la clase Animal con el nombre "Mitis"
gato.hablar()  # Llama al método hablar del objeto gato


```
3. Creamos el concepto de la herencia, solemos utilizar `pass` para definir o entender que se debe crear las subclases

O podemos utilizar `raise` para permitir salir un mensaje al momento que nos aparezca un error y el desarrollador pueda entender el error

```python
#!/usr/bin/python3 

class Animal: 
	def __init__(self, nombre): 
		self.nombre = nombre 
	def hablar(self): 
		 raise NotImplementedError("Las subclases definidas deben implementar este método")

class Gato(Animal):
	def hablar(self):
		return f"{self.nombre} dice ¡Miau!"

class Perro(Animal):
	def hablar(self):
		return f"{self.nombre} dice ¡Guau!"

gato = Gato("Mitis") 
perro = Perro("Negra")
gato_dos = Animal("Matrix")

print(gato.hablar())
print(perro.hablar())
print(gato_dos.hablar())
```

