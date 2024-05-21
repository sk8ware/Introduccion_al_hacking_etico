
----
- TAG: #CONTROL #ATRIBUTOS #FICHEROS #LINUX #CHATTR #LSATTR
----
¿Es la primera vez que ves los comandos **Chattr** y **Lsattr**?, puedes indagar un poco más en el uso de estos en los siguientes enlaces que te comparto:

- Control de atributos de ficheros Linux: [Chattr y Lsattr](https://rm-rf.es/chattr-y-lsattr-visualizar-y-modificar-atributos-en-sistemas-de-ficheros-linux/#:~:text=El%20primer%20comando%2C%20lsattr%20permite,chmod%2C%20chown%2Csetfacl%E2%80%A6))
- Comandos Chattr y Lsattr en Linux: [https://programmerclick.com/article/5604675172/](https://programmerclick.com/article/5604675172/)

----
## Configuración y Uso de Permisos y Atributos de Archivos en Linux

### Eliminación de Directorios Protegidos

En la clase anterior, no mencioné que si intentamos borrar el directorio `pruebaspepito` sin ser `root`, no podremos hacerlo. Sin embargo, si nos convertimos en `root`, sí podremos eliminarlo.

### Copia de Archivos del Sistema

Si copiamos un archivo del sistema, como el archivo de hosts, al directorio `pruebaspepito`, lo hacemos con el siguiente comando:

```sh
cp /etc/hosts /home/sk8ware/Desktop/pruebaspepito
```

**Tip:** Algunos archivos del sistema, como `/etc/passwd-`, guardan copias debido a la información sensible que manejan.

### Comando `lsattr` para Ver Atributos de Archivos

Además del comando `ls` para listar archivos, tenemos `lsattr`, que muestra los atributos de los archivos. Al ejecutar `lsattr`, veremos un mensaje similar a:

```sh
--------------e------- ./prueba
```

### Uso del Comando `chattr` para Asignar Atributos

Como usuario `root`, podemos asignar un atributo especial a un archivo utilizando el comando `chattr`. Por ejemplo, para hacer un archivo inmutable (`+i`), usamos:

```sh
chattr +i -V /home/sk8ware/Desktop/pruebaspepito/prueba
```

El flag `-V` aplica un verbose que nos permite ver en detalle lo que está sucediendo.

### Protección de Archivos con Atributo Inmutable

Al aplicar el atributo inmutable, si intentamos borrar el archivo `prueba`, el sistema no lo permitirá:

```sh
rm /home/sk8ware/Desktop/pruebaspepito/prueba
```

Para eliminar un archivo con el atributo inmutable, primero debemos remover el atributo:

```sh
chattr -i -V /home/sk8ware/Desktop/pruebaspepito/prueba
```

Ahora, el archivo puede ser eliminado:

```sh
rm /home/sk8ware/Desktop/pruebaspepito/prueba
```

### Otras Flags Disponibles con `chattr`

El atributo `+i` es solo uno de los muchos atributos que podemos asignar a los archivos. Otros atributos incluyen:

- `a`: Solo permite añadir datos al archivo (append-only).
- `d`: El archivo no será respaldado por el comando `dump`.
- `e`: Archivo que tiene extents (extensiones).
- `j`: Archivo con datos de diario (journalled).
- `s`: Cuando el archivo se borra, sus bloques son sobrescritos.
- `u`: Cuando el archivo se borra, sus datos se guardan para poder recuperarlo más tarde.

### Resumen

El uso de comandos como `chattr` y `lsattr` permite una gestión avanzada de los archivos y directorios en sistemas Linux, protegiendo datos críticos y controlando estrictamente el acceso y modificación de archivos sensibles. La combinación de permisos tradicionales y atributos avanzados proporciona una capa adicional de seguridad y control.

---