
----
- Tags: #LOCAL #FILE #INCLUSION #LFI
----
La vulnerabilidad **Local File Inclusion** (**LFI**) es una vulnerabilidad de seguridad informática que se produce cuando una aplicación web **no valida adecuadamente** las entradas de usuario, permitiendo a un atacante **acceder a archivos locales** en el servidor web.

En muchos casos, los atacantes aprovechan la vulnerabilidad de LFI al abusar de parámetros de entrada en la aplicación web. Los parámetros de entrada son datos que los usuarios ingresan en la aplicación web, como las URL o los campos de formulario. Los atacantes pueden manipular los parámetros de entrada para incluir rutas de archivo local en la solicitud, lo que puede permitirles acceder a archivos en el servidor web. Esta técnica se conoce como “**Path Traversal**” y se utiliza comúnmente en ataques de LFI.

En el ataque de Path Traversal, el atacante utiliza caracteres especiales y caracteres de escape en los parámetros de entrada para navegar a través de los directorios del servidor web y acceder a archivos en ubicaciones sensibles del sistema.

Por ejemplo, el atacante podría incluir “**../**” en el parámetro de entrada para navegar hacia arriba en la estructura del directorio y acceder a archivos en ubicaciones sensibles del sistema.

Para prevenir los ataques LFI, es importante que los desarrolladores de aplicaciones web validen y filtren adecuadamente la entrada del usuario, limitando el acceso a los recursos del sistema y asegurándose de que los archivos sólo se puedan incluir desde ubicaciones permitidas. Además, las empresas deben implementar medidas de seguridad adecuadas, como el cifrado de archivos y la limitación del acceso de usuarios no autorizados a los recursos del sistema.

A continuación, se os proporciona el enlace directo a la herramienta que utilizamos al final de esta clase para abusar de los ‘**Filter Chains**‘ y conseguir así ejecución remota de comandos:

- **PHP Filter Chain Generator**: [https://github.com/synacktiv/php_filter_chain_generator](https://github.com/synacktiv/php_filter_chain_generator)
----
# Empezamos con el ejercicio
- Creamo un script sencillo .php en nuestro directorio /var/www/html
```
<?php
  $filename = $_GET['filename'];
  include($filename);
?>
```
-  Luego ingresamos a nuestro navegador e ingresamos **localhost/index.php?filename=test** y esto nos mostrara el contenido del archivo oa su vez podemos filtrar información por directorios como /etc/passwd y Ctrl+U para verlo de mejor manera

- Uno podria decir que de la siguiente manera uno podria sanitizar el codigo
```
<?php
  $filename = $_GET['filename'];
  include("/var/www/html/" . $filename); // /var/www/html//etc/passwd
?>
```
- Pero no es así por que al momento que ingresamos ./../../../ después del = (Igual) con el directorio que deseamos ver la información
  **localhost/index.php?filename=../../../../../etc/passwd**

- Para evitar este acceso se suele utilizar la siguiente línea de código 
```
<?php
  $filename = $_GET['filename'];
  $filename = str_replace("../", "", $filename);
  include("/var/www/html/" . $filename); // /var/www/html//etc/passwd
?>
```
