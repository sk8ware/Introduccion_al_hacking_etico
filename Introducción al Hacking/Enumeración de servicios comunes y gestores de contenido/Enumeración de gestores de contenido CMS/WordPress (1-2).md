
---
- TAG: #ENUMERACIÓN #CMS #WORDPRESS
----
En esta clase estaremos enseñando técnicas de enumeración para el gestor de contenido (**CMS**) **WordPress**. Un gestor de contenido es una herramienta que permite la creación, gestión y publicación de contenidos digitales en la web, como por ejemplo páginas web, blogs, tiendas en línea, entre otros.

WordPress es un CMS de código abierto muy popular que fue lanzado en 2003. Es utilizado por millones de sitios web en todo el mundo y se destaca por su facilidad de uso y flexibilidad. Con WordPress, los usuarios pueden crear y personalizar sitios web sin necesidad de conocimientos de programación avanzados. Además, cuenta con una amplia variedad de plantillas y plugins que permiten añadir funcionalidades adicionales al sitio.

El proyecto que utilizamos en esta clase para enumerar un WordPress es el siguiente:

- **DVWP**: [https://github.com/vavkamil/dvwp](https://github.com/vavkamil/dvwp)

Una de las herramientas que utilizamos en esta clase para enumerar este gestor de contenido es **Wpscan**. Wpscan es una herramienta de código abierto que se utiliza para escanear sitios web en busca de vulnerabilidades de seguridad en WordPress.

Con Wpscan, podemos realizar una enumeración completa del sitio web y obtener información detallada sobre la instalación de WordPress, como la versión utilizada, los plugins y temas instalados y los usuarios registrados en el sitio. También nos permite realizar pruebas de fuerza bruta para descubrir contraseñas débiles y vulnerabilidades conocidas en plugins y temas.

Wpscan es una herramienta muy útil para los administradores de sitios web que desean mejorar la seguridad de su sitio WordPress, ya que permite identificar y corregir vulnerabilidades antes de que sean explotadas por atacantes malintencionados. Además, es una herramienta fácil de usar y muy efectiva para identificar posibles debilidades de seguridad en nuestro sitio web.

El uso de esta herramienta es bastante sencillo, a continuación se indica la sintaxis básica:

➜ `wpscan --url <https://example.com`>

Si deseas enumerar usuarios o plugins vulnerables en WordPress utilizando la herramienta wpscan, puedes añadir los siguientes parámetros a la línea de comandos:

**➜** `wpscan --url <https://example.com> --enumerate u`

En caso de querer enumerar plugins existentes los cuales sean vulnerables, puedes añadir el siguiente parámetro a la línea de comandos:

➜ `wpscan --url <https://example.com> --enumerate vp`

Asimismo, otro de los recursos que contemplamos en esta clase es el archivo **xmlrpc.php**. Este archivo es una característica de WordPress que permite la comunicación entre el sitio web y aplicaciones externas utilizando el protocolo **XML-RPC**.

El archivo xmlrpc.php es utilizado por muchos plugins y aplicaciones móviles de WordPress para interactuar con el sitio web y realizar diversas tareas, como publicar contenido, actualizar el sitio y obtener información.

Sin embargo, este archivo también puede ser abusado por atacantes malintencionados para aplicar **fuerza bruta** y descubrir **credenciales válidas** de los usuarios del sitio. Esto se debe a que xmlrpc.php permite a los atacantes realizar un número ilimitado de solicitudes de inicio de sesión sin ser bloqueados, lo que hace que la ejecución de un ataque de fuerza bruta sea relativamente sencilla.

En la siguiente clase estaremos desarrollando un script en Bash desde cero para realizar este tipo de ataques.

Comandos utilizados en la clase:

`docker volume rm $(docker volume ls -q)` ——————> Para eliminar por completos los volumenes