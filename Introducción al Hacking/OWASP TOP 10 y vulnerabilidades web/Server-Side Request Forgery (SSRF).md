
---
- Tags: #SERVER #SIDE #REQUEST #FORGERY #SSRF
---

El **Server-Side Request Forgery** (**SSRF**) es una vulnerabilidad de seguridad en la que un atacante puede forzar a un servidor web para que realice solicitudes HTTP en su nombre.

En un ataque de SSRF, el atacante utiliza una entrada del usuario, como una URL o un campo de formulario, para enviar una solicitud HTTP a un servidor web. El atacante manipula la solicitud para que se dirija a un servidor vulnerable o a una red interna a la que el servidor web tiene acceso.

El ataque de SSRF puede permitir al atacante acceder a información confidencial, como contraseñas, claves de API y otros datos sensibles, y también puede llegar a permitir al atacante (en función del escenario) ejecutar comandos en el servidor web o en otros servidores en la red interna.

Una de las **diferencias** clave entre el **SSRF** y el **CSRF** es que el SSRF se ejecuta en el servidor web en lugar del navegador del usuario. El atacante **no necesita engañar a un usuario legítimo** para hacer clic en un enlace malicioso, ya que puede enviar la solicitud HTTP directamente al servidor web desde una fuente externa.

Para prevenir los ataques de SSRF, es importante que los desarrolladores de aplicaciones web validen y filtren adecuadamente la entrada del usuario y limiten el acceso del servidor web a los recursos de la red interna. Además, los servidores web deben ser configurados para limitar el acceso a los recursos sensibles y restringir el acceso de los usuarios no autorizados.

En esta clase, estaremos utilizando **Docker** para crear **redes personalizadas** en las que podremos simular un escenario de **red interna**. En esta red interna, intentaremos a través del SSRF apuntar a un recurso existente que no es accesible externamente, lo que nos permitirá explorar y comprender mejor la explotación de esta vulnerabilidad.

Para crear una nueva red en Docker, podemos utilizar el siguiente comando:

➜ `docker network create --subnet=<subnet> <nombre_de_red>`

Donde:

- **subnet**: es la dirección IP de la subred de la red que estamos creando. Es importante tener en cuenta que esta dirección IP debe ser única y no debe entrar en conflicto con otras redes o subredes existentes en nuestro sistema.
- **nombre_de_red**: es el nombre que le damos a la red que estamos creando.

Además de los campos mencionados anteriormente, también podemos utilizar la opción ‘**–driver**‘ en el comando ‘docker network create’ para especificar el controlador de red que deseamos utilizar.

Por ejemplo, si queremos crear una red de tipo “**bridge**“, podemos utilizar el siguiente comando:

➜ `docker network create --subnet=<subnet> --driver=bridge <nombre_de_red>`

En este caso, estamos utilizando la opción ‘**–driver=bridge**‘ para indicar que deseamos crear una red de tipo “**bridge**“. La opción –driver nos permite especificar el controlador de red que deseamos utilizar, que puede ser “**bridge**“, “**overlay**“, “**macvlan**“, “**ipvlan**” u otro controlador compatible con Docker.

---

