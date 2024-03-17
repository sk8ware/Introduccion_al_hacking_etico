
---
- Tag: #REMOTE #FILE #INCLUSION #RFI
----
La vulnerabilidad **Remote File Inclusion** (**RFI**) es una vulnerabilidad de seguridad en la que un atacante puede **incluir** **archivos remotos** en una aplicación web vulnerable. Esto puede permitir al atacante ejecutar código malicioso en el servidor web y comprometer el sistema.

En un ataque de RFI, el atacante utiliza una entrada del usuario, como una URL o un campo de formulario, para incluir un archivo remoto en la solicitud. Si la aplicación web no valida adecuadamente estas entradas, procesará la solicitud y devolverá el contenido del archivo remoto al atacante.

Un atacante puede utilizar esta vulnerabilidad para incluir archivos remotos maliciosos que contienen código malicioso, como virus o troyanos, o para ejecutar comandos en el servidor vulnerable. En algunos casos, el atacante puede dirigir la solicitud hacia un recurso PHP alojado en un servidor de su propiedad, lo que le brinda un mayor grado de control en el ataque.

A continuación, se proporciona el enlace al proyecto de Github correspondiente al laboratorio que estaremos desplegando para practicar esta vulnerabilidad:

- **DVWP**: [https://github.com/vavkamil/dvwp](https://github.com/vavkamil/dvwp)

Asimismo, se os comparte el enlace directo para la descarga del plugin ‘**Gwolle Guestbook**‘ de WordPress:

- **Gwolle Guestbook**: [https://es.wordpress.org/plugins/gwolle-gb/](https://es.wordpress.org/plugins/gwolle-gb/)
---
# Empezamos con el proyecto

- Empezamos desplegando el plugin para empezar a tener el entorno atacable e ingresamos a la carpeta dvwp 
```
git clone https://github.com/vavkamil/dvwp
```

- Y deplegamos con 
```
docker-compose up -d --build
```

- Desplegamos las vulneravilidades
```
docker-compose run --rm wp-cli install-wp
```
- Ingresamos por el puerto **localhosts:31337**
- Buscamos el exploit en nuestro sistema con `searchsploit gwolle`
- Buscamos el sploit por el internet con la versión que nos solicite
- Si no encontramos el archivo o encontramos el sploit en otra versión lo que haríamos es editar el link de descarga abriendo en una nueva pestaña
-https://downloads.wordpress.org/plugin/gwolle-gb.1.5.3.zip
 