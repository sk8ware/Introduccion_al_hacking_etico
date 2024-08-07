
----
- TAG: #ASIGNACIÓN #PERMISOS 
----
> ¿Necesitas indagar un poco más en esta temática?, te dejo por aquí algunos recursos de interés:

- Asignación de permisos: [https://www.ionos.es/digitalguide/servidores/know-how/asignacion-de-permisos-de-acceso-con-chmod/](https://www.ionos.es/digitalguide/servidores/know-how/asignacion-de-permisos-de-acceso-con-chmod/)
- Propietarios y permisos: [https://atareao.es/tutorial/terminal/propietarios-y-permisos/](https://atareao.es/tutorial/terminal/propietarios-y-permisos/)

>Te comparto por aquí algunos enlaces de interés por si quieres investigar más acerca de permisos en Linux:

- Gestión de usuarios, grupos y permisos en Linux: [https://computernewage.com/2016/05/22/gestionar-usuarios-y-permisos-en-linux/](https://computernewage.com/2016/05/22/gestionar-usuarios-y-permisos-en-linux/)
- Gestión de usuarios y grupos en Linux: [https://atareao.es/como/gestion-de-usuarios-y-grupos-en-linux/](https://atareao.es/como/gestion-de-usuarios-y-grupos-en-linux/)
----
## Configurando los permisos del grupo "otros"

Empezamos convirtiéndonos en root e ingresamos al usuario:

```bash
cd /home/sk8ware/Desktop
```


En este punto, creamos un directorio:

```bash
mkdir prueba
```

Luego, migramos de usuario utilizando el comando `su` para cambiar a nuestro usuario `sk8ware`. Si hacemos un `ls -l`, veremos que el directorio que creamos tiene como propietario y grupo a `root`. Si intentamos crear algún archivo o directorio dentro del directorio **prueba**, no nos lo permitirá. Para permitir esto, cambiamos los permisos del grupo "otros" para que tengan poder de escritura de la siguiente manera:

```bash
chmod o+w prueba/
```

Ahora, cuando hagamos un `ls -l`, veremos que el directorio **prueba** tiene permisos de escritura para el grupo "otros", lo que se reflejará en la tercera parte de los permisos:

```plaintext
drwxr-xrwx
```

Si no queremos que "otros" tengan privilegios de escritura, podemos revertir el cambio:

```bash
chmod o-w prueba/
```

## Configurando los permisos del grupo "grupos"

Si queremos que los grupos puedan crear contenido, utilizamos la herramienta `chgrp` para cambiar el grupo propietario del directorio:

```bash
chgrp sk8ware prueba
```

Luego, asignamos permisos de escritura al grupo con:

```bash
chmod g+w prueba/
```

Si deseamos modificar los permisos en serie en una sola línea para ajustarlos a nuestras necesidades, podemos hacerlo de la siguiente manera. Supongamos que queremos cambiar los permisos de `rwxrwxr-x` a `rw--w-rw-`:

```bash
chmod u-x,g-rx,o+w,o-x prueba/
```

## Creación y configuración de usuarios

Como usuarios `root`, vamos a jugar un poco con la creación de usuarios, algo fundamental e importante. En la ruta `/home` encontramos nuestro usuario `root`. Aquí crearemos el usuario `pepe` y configuraremos su directorio personal de trabajo, además del tipo de shell que queremos que utilice con `-s`, y el directorio personal con `-d`:

```bash
useradd pepe -s /bin/bash -d /home/pepe
```

Si hacemos un `grep` al archivo `/etc/passwd` para buscar a `pepe`, veremos la información en línea:

```bash
grep pepe /etc/passwd
```

Para asignarle una contraseña, utilizamos el comando:

```bash
passwd pepe
```

El problema es que el usuario `pepe` tiene como propietario y grupo a **root**. Queremos que sea dueño de su directorio tanto a nivel de propietario como de grupo. Podemos utilizar `chown` para cambiar el propietario y `chgrp` para cambiar el grupo, o hacerlo todo en un solo comando:

```bash
chown pepe:pepe /home/pepe
```

Ahora podremos loguearnos como `pepe` con su respectiva bash. Vamos a jugar un poco con el tema de grupo "Alumnos". Para crear el grupo, lo hacemos de la siguiente manera:

```bash
groupadd Alumnos
```

Si revisamos el archivo `/etc/group`, veremos que no tiene un usuario asignado. Lo podemos asignar de la siguiente manera:

```bash
usermod -a -G Alumnos pepe
```

Si volvemos a listar el archivo `/etc/group`, observaremos que ya tiene un usuario asignado. Además, si nos logueamos como **pepe** y ejecutamos `id`, veremos que el grupo _Alumnos_ pertenece al identificador de `pepe`.

Si nos dirigimos al escritorio de **sk8ware** como el usuario **root** y creamos el directorio `prueba`:

```bash
mkdir prueba
```

Veremos que otros pueden atravesar el directorio. Si queremos que otras personas no atraviesen directorios, podemos hacer lo siguiente:

```bash
chmod o-rx prueba
```

Ahora, si salimos de **root** y vamos al escritorio `Desktop` y tratamos de entrar al directorio `prueba`, nos saldrá un mensaje de "permiso denegado".

También podríamos asignar el grupo **Alumnos** al directorio **prueba** y hacer que el grupo **Alumnos** pueda leer, escribir y atravesar. Para ello, asignamos:

```bash
chown :Alumnos prueba chmod g+rwx prueba
```

Si ingresamos como el usuario **pepe** y nos dirigimos al directorio **prueba** y creamos un archivo con `touch`, veremos que nos deja hacerlo:

```bash
touch prueba/archivo_nuevo.txt
```

----
### Eliminación del usuario 

Para eliminar un usuario que fue creado con `useradd` en Linux, puedes usar el comando `userdel`. Este comando permite eliminar el usuario y, opcionalmente, su directorio de inicio y otros archivos asociados. Aquí te dejo los pasos detallados:

### Eliminar un Usuario sin Eliminar su Directorio de Inicio

Si deseas eliminar un usuario pero conservar su directorio de inicio y otros archivos, utiliza el siguiente comando:

```bash
sudo userdel pepe
```

### Eliminar un Usuario y su Directorio de Inicio

Si deseas eliminar un usuario junto con su directorio de inicio y otros archivos asociados, utiliza el comando con la opción `-r`:

```bash
sudo userdel -r pepe
```

---
## Elimininación de grupos 

**Eliminar el Grupo**:

1. Utiliza el comando `groupdel` seguido del nombre del grupo que deseas eliminar. En este caso, el grupo se llama `Alumnos`:
    
```bash
sudo groupdel Alumnos
```

2. **Verificar la Eliminación**:
    
    - Puedes verificar que el grupo ha sido eliminado revisando el archivo `/etc/group`:
        
        ```bash
        cat /etc/group | grep Alumnos
        ```
        
    
- Si el grupo no aparece en el listado, ha sido eliminado correctamente.