
----
-  TAG :  #BUSQUEDA #A-NIVEL-DE-SISTEMA #FIND #BUSQUEDADEARCHIVOS #GESTIONDEPERMISOS
----
# Búsqueda y Gestión de Archivos y Directorios en Linux

## Verificación de Grupos

A veces, cuando comprometemos una máquina, solemos revisar a qué grupo pertenecemos utilizando el comando `id`. Esto nos permite realizar búsquedas a nivel de sistema de forma recursiva para detectar archivos o directorios que contengan ese grupo y diversos permisos. Por ejemplo, si buscamos el archivo `passwd`:

```bash
find / -name passwd 2>/dev/null
```

El `2>/dev/null` se utiliza para redirigir los errores y evitar que se muestren en pantalla, lo cual es útil cuando no tenemos acceso a varios directorios debido a la falta de privilegios de root.

## Ejecución Paralela con xargs

Podemos ejecutar el comando `xargs ls -l` de forma paralela para listar los detalles de los archivos encontrados:

```bash
find / -name passwd 2>/dev/null | xargs ls -l
```

Recordemos que `xargs` nos permite ejecutar comandos en paralelo, lo que facilita la búsqueda de archivos importantes como archivos **SUID**.

## Búsqueda de Archivos SUID

Para buscar archivos **SUID** desde la raíz del sistema, utilizamos el siguiente comando:

```bash
find / -perm -4000 2>/dev/null
```

## Búsqueda por Grupo

Para buscar directorios específicos pertenecientes a un grupo determinado, por ejemplo, el grupo `sk8ware`, usamos:

```bash
find / -group sk8ware -type d 2>/dev/null
```

Si queremos mostrar todos los archivos en lugar de solo los directorios, cambiamos `-type d` por `-type f`:

```bash
find / -group sk8ware -type f 2>/dev/null
```

## Búsqueda de Archivos Escribibles

Para buscar archivos que pueden ser escritos por un usuario específico, como el usuario `root`, utilizamos:

```bash
find / -user root -writable 2>/dev/null
```

Esto nos mostrará todos los directorios con capacidad de escritura. Si seleccionamos cualquiera de ellos y ejecutamos un `ls -l`, veremos los permisos y qué otros usuarios pueden escribir en esos directorios.

## Búsqueda de Archivos Ejecutables

Para buscar archivos ejecutables pertenecientes al usuario `root`, utilizamos:

```bash
find / -user root -executable 2>/dev/null
```

Para buscar únicamente archivos ejecutables (no directorios):

```bash
find / -user root -executable -type f 2>/dev/null
```

Una vez que encontremos un archivo, podemos listar sus detalles con `ls -l` para ver quién más puede ejecutar el archivo.

## Búsqueda de Archivos por Nombre

Si deseamos buscar un archivo cuyo nombre no recordamos completamente, podemos usar comodines:

```bash
find / -name dex\* 2>/dev/null
```

O:

```bash
find / -name \*exdum\* 2>/dev/null
```

Para buscar archivos con una extensión específica, como `.sh`:

```bash
find / -name dex\*.sh 2>/dev/null
```

## Ayuda y Manual de find

Para ver todas las opciones disponibles del comando **find**, podemos usar:

```bash
find --help
```

O leer el manual completo:

```bash
man find
```

## Practica

Pon en práctica todos estos comandos para dominarlos y aprovechar al máximo sus funcionalidades.

# Script de s4vitar para crear una red wifi y robar credenciales

https://github.com/s4vitar/evilTrust/tree/master
