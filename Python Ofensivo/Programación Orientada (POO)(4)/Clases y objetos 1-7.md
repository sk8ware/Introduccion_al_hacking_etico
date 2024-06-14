
----
- TAG: #Python #POO #Clases #Objetos
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

Ahora iremos con la parte práctica, creando un archivo `.py` y desarrollando una clase llamada `Persona`. Luego, aplicaremos un método que nos permite realizar una función interna de la clase.

Cuando creamos un objeto, este objeto es una instancia de la clase. El constructor se utiliza para inicializar los atributos del objeto.

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

Si deseamos crear otro objeto, simplemente agregamos un `silvia = Persona("Silvia", 48)`. Así, creamos una instancia de la clase y el constructor entiende los parámetros **nombre y edad**. Imprimimos en consola el resultado con `print(silvia.saludo())`.

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

Creamos una clase llamada `Persona` y muestra cómo se crean instancias de esta clase y cómo se utilizan sus métodos. A continuación, te explico cada parte del código:

```python
#!/usr/bin/python3
```

Esta línea es una shebang que indica al sistema operativo que use el intérprete de Python 3 para ejecutar este script.

```python
class Persona:
```

Define una nueva clase llamada `Persona`.

```python
	def __init__(self, nombre, edad): # Persona.__init__(anthony, nombre, edad)         
		self.nombre = nombre         
		self.edad = edad
```

Este es el método constructor `__init__`. Se ejecuta automáticamente cuando se crea una nueva instancia de `Persona`. Inicializa los atributos de la persona:

- `nombre`: el nombre de la persona.
- `edad`: la edad de la persona.

```python
def saludo(self): # Persona.saludo(anthony)         
	return f"Hola, soy {self.nombre} y tengo {self.edad} años"
```

Este método, `saludo`, retorna un saludo en forma de cadena de texto que incluye el nombre y la edad de la persona.

```python
anthony = Persona("Anthony", 25) 
silvia = Persona("Silvia", 48)  

print(anthony.saludo()) 
print(silvia.saludo())
```

Finalmente, se crean dos instancias de la clase `Persona`:

- `anthony`, con el nombre "Anthony" y la edad 25.
- `silvia`, con el nombre "Silvia" y la edad 48.

Luego, se llaman al método `saludo` para cada instancia y se imprimen los resultados.

Cuando ejecutas este código, el resultado será:

```zsh
Hola, soy Anthony y tengo 25 años 
Hola, soy Silvia y tengo 48 años
```

Esto indica que el método `saludo` se ha llamado correctamente en ambas instancias, produciendo un mensaje de saludo con el nombre y la edad de cada persona.

---
# Objetos Independientes

Ahora mostraremos otro ejercicio con objetos independientes que tienen sus atributos y propiedades definidos. Podemos acceder a estos atributos gracias a los métodos declarados. No hace falta usar `return`; también se puede usar la función `print`.

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

Este código define una clase llamada `Animal` que representa a un animal y tiene métodos para describirlo. A continuación, te explico cada parte del código:


```python
#!/usr/bin/python3
```

Esta línea es una shebang que indica al sistema operativo que use el intérprete de Python 3 para ejecutar este script.

```python
class Animal:
```

Define una nueva clase llamada `Animal`.

```python
	def __init__(self, nombre, animal): # Animal.__init__(gato, nombre, animal)   
	      self.nombre = nombre         
	      self.animal = animal
```

Este es el método constructor `__init__`. Se ejecuta automáticamente cuando se crea una nueva instancia de `Animal`. Inicializa los atributos del animal:

- `nombre`: el nombre del animal.
- `animal`: el tipo de animal.

```python
	def descripcion(self): # Animal.descripcion(gato)       
	  print(f"{self.nombre} es un {self.animal}")
```

Este método, `descripcion`, imprime una descripción en la forma de una cadena de texto que incluye el nombre y el tipo de animal.

```python
gato = Animal("Tijuana", "Gato") 
perro = Animal("Pancho", "Perro")  

gato.descripcion()
perro.descripcion()
```

Finalmente, se crean dos instancias de la clase `Animal`:

- `gato`, con el nombre "Tijuana" y el tipo "Gato".
- `perro`, con el nombre "Pancho" y el tipo "Perro".

Luego, se llaman al método `descripcion` para cada instancia, lo cual imprime la descripción de cada animal.

Cuando ejecutas este código, el resultado será:

```zhs
Tijuana es un Gato 
Pancho es un Perro
```

Esto indica que el método `descripcion` se ha llamado correctamente en ambas instancias, produciendo un mensaje descriptivo con el nombre y el tipo de cada animal.

---
# Ejercicio cuenta bancaria

Crearemos una clase **CuentaBancaria** e indicaremos unos valores para un cliente, donde el cliente es el objeto.

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

Este código es un ejemplo de programación orientada a objetos en Python. Define una clase llamada `CuentaBancaria` que representa una cuenta bancaria y tiene métodos para gestionar el dinero en la cuenta. A continuación, te explico cada parte del código:


```python
#!/usr/bin/python3
```

Esta línea es una shebang que indica al sistema operativo que use el intérprete de Python 3 para ejecutar este script.

```python
class CuentaBancaria:
```

Define una nueva clase llamada `CuentaBancaria`.

```python
	def __init__(self, cuenta, nombre, dinero=0):         
		self.cuenta = cuenta        
		self.nombre = nombre      
		self.dinero = dinero
```

Este es el método constructor `__init__`. Se ejecuta automáticamente cuando se crea una nueva instancia de `CuentaBancaria`. Inicializa los atributos de la cuenta bancaria:

- `cuenta`: el número de cuenta.
- `nombre`: el nombre del titular de la cuenta.
- `dinero`: el saldo inicial de la cuenta (por defecto es 0).

```python
	def depositar_dinero(self, dinero):         
		self.dinero += dinero         
		return f"\n[+] Se han depositado {dinero} dolares, actualmente el balance de la cuenta es de {self.dinero} dolares"
```

Este método, `depositar_dinero`, permite añadir dinero a la cuenta bancaria. Toma un parámetro `dinero` que representa la cantidad de dinero a depositar y lo añade al saldo actual (`self.dinero`). Luego, retorna un mensaje con el monto depositado y el nuevo balance.

```python
manolo = CuentaBancaria("187263", "Manolo Vieira", 1000) 
print(manolo.depositar_dinero(500))
```

Finalmente, se crea una instancia de `CuentaBancaria` llamada `manolo` con el número de cuenta "187263", el nombre "Manolo Vieira" y un saldo inicial de 1000 dólares. Luego, se llama al método `depositar_dinero` para depositar 500 dólares en la cuenta de Manolo y se imprime el mensaje retornado por este método.

Cuando ejecutas este código, el resultado será:

```css
[+] Se han depositado 500 dolares, actualmente el balance de la cuenta es de 1500 dolares
```

Esto indica que se han añadido 500 dólares al saldo inicial de 1000 dólares, resultando en un nuevo balance de 1500 dólares.


