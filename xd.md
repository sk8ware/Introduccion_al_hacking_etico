

## Touch y Redirecciones

Empezamos explicando un poco sobre los redireccionadores de la siguiente manera:

bash

`cd Desktop touch file.txt echo "probando" > file.txt`  

El comando `echo "probando" > file.txt` escribirá "probando" en `file.txt`. Sin embargo, si volvemos a utilizar el mismo comando, no se acumulará la información, sino que se sobrescribirá el contenido existente. Esto significa que siempre habrá un solo output cuando abramos el archivo `file.txt`.

Para poder realizar un _append_ (apilar) y evitar que se sobrescriba el archivo, solo debemos utilizar el doble mayor `>>`:

bash

`echo "nueva línea" >> file.txt`

Esto agregará "nueva línea" al final del archivo `file.txt` sin eliminar el contenido anterior.

## Nano

Con `nano` podemos crear y editar archivos, permitiendo agregar toda la información manualmente. Es un editor de texto sencillo pero poderoso, accesible desde la línea de comandos.

bash

`nano file.txt`

Dentro de `nano`, puedes escribir, editar y guardar el archivo.

## Vi

El editor `vi` también nos permite crear y editar archivos desde la línea de comandos. Aunque `vi` es más básico, se puede mejorar con **nvim** (Neovim), que es una versión extendida y más moderna de `vi`.

bash

`vi file.txt`

Para mejorar la experiencia, podemos usar:

bash

`nvim file.txt`

## Permisos de Archivos en Linux

Ahora que entendemos sobre la creación de archivos, es importante conocer los permisos que estos tienen. Para ver permisos en Linux, podemos utilizar el comando `ls -l`:

bash

`ls -l`

La estructura de permisos se muestra de la siguiente manera:

plaintext

`.rw-r--r--`

Estos permisos se distinguen en tres partes:

plaintext

`.rw- | r-- | r--`

Cada grupo de permisos se basa en tres atributos específicos `rwx`:

- `r` = Read (leer)
- `w` = Write (escribir)
- `x` = Execute (ejecutar)

plaintext

`|    rw-   |   r--   |   r--   |     sk8ware sk8ware | | propietario | grupos | otros | propietario grupo |`

El primer grupo de letras (rw-) corresponde al propietario del archivo, el segundo (r--) corresponde al grupo, y el tercero (r--) corresponde a otros usuarios.

Para identificar quién es el propietario o el grupo, podemos verlo en la parte derecha que sigue de los permisos. Siempre existen dos propietarios: el propietario que creó el archivo y el grupo al que pertenece. Por ejemplo, si hay otro usuario con el nombre "alumnos", este podría tener los mismos privilegios que el propietario, pero el primer usuario siempre tendrá los privilegios más altos.

### Ejemplo Práctico

Si listamos los permisos del archivo `/etc/passwd`:

bash

`ls -l /etc/passwd`

Veremos que el propietario y el grupo es `root`. Nosotros, como usuarios `sk8ware`, no podremos escribir en él. Intentar ejecutar:

bash

`echo "probando" > /etc/passwd`

nos devolverá un error, ya que no pertenecemos al grupo adecuado ni tenemos los permisos necesarios.

Otro ejemplo es listar los permisos del archivo `/etc/shadow`:

bash

`ls -l /etc/shadow`

Si intentamos ver su contenido con `cat`:

bash

`cat /etc/shadow`

Veremos las contraseñas del sistema de manera cifrada, pero solo si tenemos los permisos necesarios para acceder a dicho archivo.



