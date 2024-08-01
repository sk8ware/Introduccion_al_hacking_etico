
----
- TAG:
-----
El uso de self es uno de los aspectos más fundamentales y a la vez confusos para quienes se adentran en la Programación Orientada a Objetos (POO) en Python. Este identificador es crucial para entender cómo Python maneja los métodos y atributos dentro de sus clases y objetos.

**Definición de ‘self’**

A nivel conceptual, ‘**self**‘ es una referencia al objeto actual dentro de la clase. Es el primer parámetro que se pasa a cualquier método de una clase en Python. A través de self, un método puede acceder y manipular los atributos del objeto y llamar a otros métodos dentro del mismo objeto.

**Uso de ‘self’**

Cuando se crea una nueva instancia de una clase, Python pasa automáticamente la instancia recién creada como el primer argumento al método ‘**__init__**‘ y a otros métodos definidos en la clase que tienen self como su primer parámetro. Esto es lo que permite que un método opere con datos específicos del objeto y no con datos de la clase en general o de otras instancias de la clase.

**Importancia de ‘self’**

El concepto de self es importante en la POO ya que asegura que los métodos y atributos se apliquen al objeto correcto. Sin self, no podríamos diferenciar entre las operaciones y datos de diferentes instancias de una clase.

En esta clase, nos enfocaremos en comprender a fondo cómo y por qué self es usado en Python, explorando su papel en la interacción con las instancias de la clase. Desarrollaremos una comprensión clara de cómo self permite que las clases en Python sean intuitivas y eficientes, manteniendo un estado consistente a través de las operaciones del objeto. Este conocimiento es esencial para trabajar con clases y objetos de manera efectiva y aprovechar la potencia de la POO.

---

Vamos a praticar con un ejercicio empleando una clase para explicar de mejor manera el uso de `self`

Esta plantilla puede contener tanto métodos como atributos, recuerden que la clase no es un objeto, es cuando instanciamos la clase que creamos un objeto eso seria la instancia de la clase, esta clase tendria sus metodos y atributos que hayamos definido en la clase 

Se empieza creando un constructor `def __init__()`

Cuando creamos una instancia de la clase, al hacer esto le estaríamos pasando unos valores para poder crear este objeto, sus propiedades y atributos serían `("Anthony", 25)`

```bash
#!/usr/bin/python3

class Persona:
	def __init__()

anthony = Persona("Anthony", 25)
```

Como estamos creando este objeto debemos irlo construyendo, que seria primero el método especial que es el constructor `def __init__()`, asi que le agregamos un `self` que hace referencia a `anthony`

Ya que cuando creamos el objeto `anthony` los atributos `("Anthony", 25)` se vincula de alguna manera al objeto `anthony`

En el siguiente ejemplo se hara referencia `self` al objeto `anthony` donde nombre valdra a Anthony y edad a 25

```bash
#!/usr/bin/python3

class Persona:
	def __init__(self, nombre, edad): #Persona.__init__(anthony, nombre, edad)
		self.anthony = nombre # anthony.nombre = "Anthony"
		self.edad = edad # anthony.edad = 28

anthony = Persona("Anthony", 25)
```

Si trataramos de imprimir dicha función, veremos que no funcionará por que no le hemos indicado lo que queremos que nos muestre, para ello debemos agregarle una definición con `def`

```bash
#!/usr/bin/python3

class Persona:
	def __init__(self, nombre, edad): #Persona.__init__(anthony, nombre, edad)
		self.nombre = nombre # anthony.nombre = "Anthony"
		self.edad = edad # anthony.edad = 28

	def presentacion(def): # Persona.presentacion(anthony)
		print(f"Hola soy {self.nombre} y tengo {self.edad} años") #anthony.nombre #anthony.edad

anthony = Persona("Anthony", 25)
anthony.presetacion()
```

Para imprimir el nombre o hacer referencia a el, debemos agregarle el `marcelo.presentacion()` al final del def presemtacion

Agregando el `print` que nos permitira ver por consola el texto agregando el `{self.nombre}` y `{self.edad}`

