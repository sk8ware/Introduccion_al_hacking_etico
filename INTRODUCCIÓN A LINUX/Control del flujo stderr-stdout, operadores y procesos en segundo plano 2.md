

----
- TAG: #STEDERR #STDOUT #ASÍ ---> 2>/dev/null
----
Por aquí les dejo algunos recursos de apoyo para profundizar sobre el uso de redirectores en Bash:

-  Redirectores en Bash [Formato PDF]: [https://hack4u.io/wp-content/uploads/2022/05/bash-redirections-cheat-sheet.pdf](https://hack4u.io/wp-content/uploads/2022/05/bash-redirections-cheat-sheet.pdf)
    

Esta parte es fundamental, sobre todo de cara a las clases de scripting en Bash que tendremos más adelante, pues haremos mucho uso de estos.

----

; ---> Si hacemos un ` whoami ; ls ` podremos ejecutar dos comandos a la vez en el one liner
&& ---> (and) Esta función solo nos permite ejecutar solo si el primer comando nos devuelve como respuesta un código éxitoso ` whoami && ls ` 
|| ---> (or) Este comando nos permite ejecutar el segundo comando así el primero haya sido erroneo 
# **PARA VER EL ESTADO DE UN COMANDO**

```
cat /etc/hosts
```

```
echo $?
```

Siempre debemos enviar el comando que deseamos ver la respuesta y después el `echo $?` 

-----
# Stderr

Los erros se definen como **stderr** que se puede referenciar con el número `2` y decirle que le queremos redirigir `>` al `/dev/null` y esto hará que enviemos todos los errores al "agujero negro del sistema", esto evitará que veamos todos los errores por consola y solo nos muestre los resultados éxitosos

```
cat /etc/host 2>/dev/null
```
# Stdout 

Cuando por consola vemos una respuesta éxitosa y nos muestra toda la información eso es un **Stdout** 
En caso de que no queramos que el **Stdout** no se vea podemos realizar las dos siguientes opciones;

```
cat /etc/hosts > /dev/null
```

Pero si lo ejecutamos con información erronea nos muestra error ya que solo indica cuando fue ejecutado correctamente el comando

Si lo realizamos de la siguiente manera podemos eliminar los dos errores 
```
cat /etc/hosts > /dev/null 2>&1
```

Pero la mejor opción y la mas comoda es así;
```
cat /etc/hosts &>/dev/null
```

Así enviaremos el stderr y el stdout al **/dev/null** para no ver errores 

-----

Se preguntarán por que quisieramos eliminar los *stderr y los stdout* 
Cuando abrimos un aplicativo como wireshark en consola suele mostrar el *output* con información, suele pasar lo mismo cuando creamos un script y no queremos que refleje el **output**
Lo podemos poner en segundo plano para que no indique ese mensaje por consola 
```
wireshark &>/dev/null 
```

# PID

Para poderlo ejecutar en segundo plano seria de la siguiente manera:
```
wireshark &>/dev/null &
```

Nos mostrará un mensaje unico que sería el **PID** que es el número identificativo que hace referencia a un proceso que se este ejecutando en el sistema 
Cada proceso no pueden compartir el mismo **PID**

Ahora si queremos idependizar un proceso y que no dependa de consola lo podemos realizar de la siguiente manera
```
wireshark &>/dev/null & disown
```


