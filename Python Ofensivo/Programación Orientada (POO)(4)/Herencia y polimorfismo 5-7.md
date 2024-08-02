
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

class Animal:  # Definición de una clase base llamada Animal
    def __init__(self, nombre):  # Constructor de la clase que inicializa el nombre del animal
        self.nombre = nombre  # Asigna el nombre pasado al crear el objeto a la variable de instancia

    def hablar(self):  # Método que debe ser implementado por las subclases
        raise NotImplementedError("Las subclases definidas deben implementar este método")  # Lanza un error si no se implementa en una subclase

class Gato(Animal):  # Definición de una clase llamada Gato que hereda de Animal
    def hablar(self):  # Implementación del método hablar para la clase Gato
        return f"{self.nombre} dice ¡Miau!"  # Devuelve un mensaje con el nombre del gato y "dice ¡Miau!"

class Perro(Animal):  # Definición de una clase llamada Perro que hereda de Animal
    def hablar(self):  # Implementación del método hablar para la clase Perro
        return f"{self.nombre} dice ¡Guau!"  # Devuelve un mensaje con el nombre del perro y "dice ¡Guau!"

gato = Gato("Mitis")  # Crea un nuevo objeto de la clase Gato con el nombre "Mitis"
perro = Perro("Negra")  # Crea un nuevo objeto de la clase Perro con el nombre "Negra"
gato_dos = Animal("Matrix")  # Crea un nuevo objeto de la clase Animal con el nombre "Matrix"

print(gato.hablar())  # Llama al método hablar del objeto gato y lo imprime
print(perro.hablar())  # Llama al método hablar del objeto perro y lo imprime
print(gato_dos.hablar())  # Llama al método hablar del objeto gato_dos y lo imprime (esto lanzará un error)

```

Tambien lo pudimos haberlo hecho de otra manera y es aqui cuando entra en juego el **Polimorfismo** 

- Fuera de las cases creamos una función llamada `hacer_hablar`
- Va a recibir un objeto esta funcón 
- Creamos los objetos :
	- `hacer_hablar(gato)`
	- `hacer_hablar(perro)`
- Hacemos un print dentro de la función donde desconoce el tipo de animal pero de manera dinamica llama al objeto de ese metodo correspondiente, gracias a ser subclases de las instancias que heredan de la "clase padre"(Animal), automaticamente al ingresar al método `hanlar` sabra que listar por consola 

```python
#!/usr/bin/python3  # Indica que se debe usar Python 3 para ejecutar este script

class Animal:  # Definición de una clase base llamada Animal
    def __init__(self, nombre):  # Constructor de la clase que inicializa el nombre del animal
        self.nombre = nombre  # Asigna el nombre pasado al crear el objeto a la variable de instancia

    def hablar(self):  # Método que debe ser implementado por las subclases
        raise NotImplementedError("Las subclases definidas deben implementar este método")  # Lanza un error si no se implementa en una subclase

class Gato(Animal):  # Definición de una clase llamada Gato que hereda de Animal
    def hablar(self):  # Implementación del método hablar para la clase Gato
        return f"¡Miau!"  # Devuelve "¡Miau!" cuando se llama a hablar

class Perro(Animal):  # Definición de una clase llamada Perro que hereda de Animal
    def hablar(self):  # Implementación del método hablar para la clase Perro
        return f"¡Guau!"  # Devuelve "¡Guau!" cuando se llama a hablar

def hacer_hablar(objeto):  # Definición de una función que toma un objeto como argumento
    print(f"{objeto.nombre} dice {objeto.hablar()}")  # Imprime el nombre del objeto y lo que dice

gato = Gato("Mitis")  # Crea un nuevo objeto de la clase Gato con el nombre "Mitis"
perro = Perro("Negra")  # Crea un nuevo objeto de la clase Perro con el nombre "Negra"

hacer_hablar(gato)  # Llama a la función hacer_hablar con el objeto gato
hacer_hablar(perro)  # Llama a la función hacer_hablar con el objeto perro

```