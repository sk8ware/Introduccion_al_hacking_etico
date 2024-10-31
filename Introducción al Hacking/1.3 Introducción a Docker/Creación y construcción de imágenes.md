
----
- TAG: #CONTRUCCIÓN #IMAGENES 
---
Para crear una imagen de Docker, es necesario tener un archivo **Dockerfile** que defina la configuración de la imagen. Una vez que se tiene el Dockerfile, se puede utilizar el comando “**docker build**” para construir la imagen. Este comando buscará el archivo ‘Dockerfile’ en el directorio actual y utilizará las instrucciones definidas en el mismo para construir la imagen.

Algunas de las instrucciones que vemos en esta clase son:

- **docker build**: es el comando que se utiliza para construir una imagen de Docker a partir de un Dockerfile.

La sintaxis básica es la siguiente:

➜ `docker build [opciones] ruta_al_Dockerfile`

El parámetro “**-t**” se utiliza para etiquetar la imagen con un nombre y una etiqueta. Por ejemplo, si se desea etiquetar la imagen con el nombre “**mi_imagen**” y la etiqueta “**v1**“, se puede usar la siguiente sintaxis:

➜ `docker build -t mi_imagen:v1 ruta_al_Dockerfile`

El punto (“**.**“) al final de la ruta al Dockerfile se utiliza para indicar al comando que busque el Dockerfile en el directorio actual. Si el Dockerfile no se encuentra en el directorio actual, se puede especificar la ruta completa al Dockerfile en su lugar. Por ejemplo, si el Dockerfile se encuentra en “**/home/usuario/proyecto/**“, se puede usar la siguiente sintaxis:

➜ `docker build -t mi_imagen:v1 /home/usuario/proyecto/` ( o puede ser .)

- **docker pull**: es el comando que se utiliza para descargar una imagen de Docker desde un registro de imágenes.

La sintaxis básica es la siguiente:

➜ `docker pull nombre_de_la_imagen:etiqueta`

Por ejemplo, si se desea descargar la imagen “ubuntu” con la etiqueta “latest”, se puede usar la siguiente sintaxis:

➜ `docker pull ubuntu:latest`

- **docker images**: es el comando que se utiliza para listar las imágenes de Docker que están disponibles en el sistema.

La sintaxis básica es la siguiente:

➜ `docker images [opciones]`

Durante la construcción de la imagen, Docker descargará y almacenará en caché las capas de la imagen que se han construido previamente, lo que hace que las compilaciones posteriores sean más rápidas.

En la siguiente clase, veremos cómo desplegar contenedores en base a las imágenes que previamente hayamos creado.