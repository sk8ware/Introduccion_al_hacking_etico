
----
- TAG: #BASHRC #ZSHRC
-----
En mi caso yo opero con una ZSH, por tanto mi archivo de configuración corresponde al ‘~/.**zshrc**‘. Recuerda que en caso de usar una BASH tu archivo de configuración debería estar situado en ‘**~/.bashrc**‘

Por aquí te dejo algunos enlaces de interés por si quieres entender un poco mejor para qué sirven estos archivos:

- ¿Qué es Bashrc en Linux?: [https://www.compuhoy.com/que-es-bashrc-en-linux/](https://www.compuhoy.com/que-es-bashrc-en-linux/)
- ¿Por qué deberías usar ZSH?: [https://respontodo.com/que-es-zsh-y-por-que-deberia-usarlo-en-lugar-de-bash/](https://respontodo.com/que-es-zsh-y-por-que-deberia-usarlo-en-lugar-de-bash/)

Mi recomendación personal es que utilicéis ZSH en vez de BASH, desde que investiguéis un poco diferencias entre ambas entenderéis por qué merece la pena.

----
# Trabajando con Directorios Ocultos y Configuraciones en Zsh

## Listado de Directorios Ocultos

Para listar los directorios ocultos, utilizamos el siguiente comando:

```sh
ls -la
```

- `-a`: Permite mostrar directorios ocultos que empiecen con `.`.
- `.`: Nos permite crear directorios ocultos.

Para crear un directorio oculto, usamos:

```zsh
mkdir .prueba
```

## Identificación del Tipo de Shell

Como estamos utilizando `zsh` como tipo de shell, podemos verificarlo con:

```sh
echo $SHELL
```

## Archivo de Configuración `.zshrc`

Podemos encontrar nuestro archivo `.zshrc` en la ruta personal de usuario. Vamos a crear una función de ejemplo para integrarla en nuestro `.zshrc` y agregar las funciones que queramos.

### Creación de una Función para Mostrar la Dirección IP Privada

Si queremos crear una función que nos muestre nuestra dirección IP privada, podemos hacer lo siguiente:

```sh
hostname -I | awk '{print $1}'
```

Esta función nos permite filtrar solo la primera dirección IP. También podemos hacerlo usando `cut`:

```sh
hostname -I | cut -d ' ' -f 1
```

- `-d`: Delimitador del espacio.
- `' '`: Espacio entre las direcciones IP.
- `-f`: Field (campo).
- `1`: Campo 1.

### Mostrar la Dirección IP con un Mensaje

Para mostrar la dirección IP en la consola con un mensaje, podemos realizarlo de la siguiente manera:

```zsh
echo "Tu dirección IP es: $(hostname -I | awk '{print $1}')"
```

Si agregamos el signo `$` antes de los paréntesis `()`, podemos hacer que se imprima esa cadena después del `echo`.

## Integración de la Función en `.zshrc`

Para que puedan entender para qué sirve el archivo `.zshrc`, podemos copiar el código anterior. Al final de todo, agregamos la nueva función:

```bash
function vermiip(){      
       echo "Tu dirección IP es: $(hostname -I | awk '{print $1}')" 
}
```

## Cargar y Probar la Nueva Función

Guardamos el archivo y recargamos la configuración. Si escribimos `vermiip` en la terminal, nos mostrará la dirección IP, confirmando que la función funciona correctamente.

```sh
source ~/.zshrc
```

Ahora pueden crear las funciones que deseen y personalizar su entorno de trabajo.