
---
- TAG: #ENUMERACIÓN #SCRIPTS #BASH
---
En esta clase, veremos cómo abusar del archivo **xmlrpc.php** para mediante la creación de un script de Bash aplicar fuerza bruta. El objetivo de este ejercicio será demostrar cómo los atacantes pueden utilizar este archivo existente en WordPress para intentar descubrir credenciales válidas y comprometer la seguridad del sitio web.

Para lograrlo, crearemos un script de Bash en el cual emplearemos la herramienta cURL para enviar solicitudes XML-RPC al archivo xmlrpc.php del sitio web WordPress. A través del método **wp.getUsersBlogs**, enviaremos una estructura XML que contendrá el nombre de usuario y la contraseña a probar.

En caso de que las credenciales no sean correctas, el servidor responderá con un mensaje de error que indica que las credenciales son incorrectas. Sin embargo, si las credenciales son válidas, la respuesta del servidor será diferente y no incluirá el mensaje de error.

De esta forma, podremos utilizar la respuesta del servidor para determinar cuándo hemos encontrado credenciales válidas y, de esta forma, tener acceso al sitio web de WordPress comprometido.

Cabe destacar que el método wp.getUsersBlogs **no es el único método existente**, ni mucho menos la única vulnerabilidad en xmlrpc.php. Existen otros métodos como **wp.getUsers**, **wp.getAuthors** o **wp.getComments**, entre otros, que también pueden ser utilizados por atacantes para realizar ataques de fuerza bruta y comprometer la seguridad del sitio web de WordPress.

Por lo tanto, es importante tener en cuenta que la seguridad de un sitio web de WordPress no solo depende de tener contraseñas seguras y actualizadas, sino también de estar atentos a posibles vulnerabilidades en el archivo xmlrpc.php y otras áreas del sitio web.

Comando con wpscan y creación de herramienta en bash:

`wpscan - -url <http://127.0.0.1:31337> -U sk8ware -P /usr/share/wordlists/rockyou.txt`

script en bash para realizar ataque de fuerza bruta para encontrar la contraseña del login en wordpress:

![[Pasted image 20240422005343.png]]