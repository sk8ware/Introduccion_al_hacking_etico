

----
- Tag: #SERVER-SIDE #TEMPLATE #INJECTION #SSTI
----

El **Server-Side Template Injection** (**SSTI**) es una vulnerabilidad de seguridad en la que un atacante puede inyectar código malicioso en una **plantilla** de servidor.

Las plantillas de servidor son archivos que contienen código que se utiliza para generar **contenido dinámico** en una aplicación web. Los atacantes pueden aprovechar una vulnerabilidad de SSTI para inyectar código malicioso en una plantilla de servidor, lo que les permite ejecutar comandos en el servidor y obtener acceso no autorizado tanto a la aplicación web como a posibles datos sensibles.

Por ejemplo, imagina que una aplicación web utiliza plantillas de servidor para generar correos electrónicos personalizados. Un atacante podría aprovechar una vulnerabilidad de **SSTI** para inyectar código malicioso en la plantilla de correo electrónico, lo que permitiría al atacante ejecutar comandos en el servidor y obtener acceso no autorizado a los datos sensibles de la aplicación web.

En un caso práctico, los atacantes pueden detectar si una aplicación Flask está en uso, por ejemplo, utilizando herramientas como **WhatWeb**. Si un atacante detecta que una aplicación **Flask** está en uso, puede intentar explotar una vulnerabilidad de **SSTI**, ya que Flask utiliza el motor de plantillas **Jinja2**, que es vulnerable a este tipo de ataque.

Para los atacantes, detectar una aplicación Flask o Python puede ser un primer paso en el proceso de intentar explotar una vulnerabilidad de SSTI. Sin embargo, los atacantes también pueden intentar identificar vulnerabilidades de SSTI en otras aplicaciones web que utilicen diferentes frameworks de plantillas, como Django, Ruby on Rails, entre otros.

Para prevenir los ataques de SSTI, los desarrolladores de aplicaciones web deben validar y filtrar adecuadamente la entrada del usuario y utilizar herramientas y frameworks de plantillas seguros que implementen medidas de seguridad para prevenir la inyección de código malicioso.

---
# Iniciamos con la practica en nuestro entorno

- Desplegamos nuestro docker
```
docker run -p 8089:8089 -d filipkarc/ssti-flask-hacking-playground
```
 - Una vez desplegado la maquina entramos por el navegador por el puerto 8089
 - Si ingresamos un nombre en el espacio de usuario nos daremos cuenta que es inyectable de codigo en la parte de la URL
 - También podemos ánilizar el tipo de lenguajes que contiene la red con `whatwep localhost:8089`
 - Podemos realizar un intento de ingresar código en el **IMPUT** para ver si nos devuelve una respuesta valida en el **OUTPUT** como `{{7*7}}`
 - Buscamos nuestro payload en nuestro Recurso de github de **Payloads All The Things** 
 ejemplo de la inye


# Recursos 
- En este link podemos encontrar varios payloads para usar [Payloads All The Things](https://github.com/swisskyrepo/PayloadsAllTheThings)

