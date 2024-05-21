
----
- TAG: #PERMISOS #ESPECIALES #STICKY #BIT 
----
>¿Quieres entender mejor el Sticky Bit?, puedes profundizar en los siguientes enlaces de interés que te comparto:

- ¿Qué es el Sticky Bit y cómo configurarlo?: [https://keepcoding.io/blog/que-es-el-sticky-bit-y-como-configurarlo/](https://keepcoding.io/blog/que-es-el-sticky-bit-y-como-configurarlo/)
- El bit Sticky | Tutorial de GNU/Linux: [https://www.fpgenred.es/GNU-Linux/el_bit_sticky.html](https://www.fpgenred.es/GNU-Linux/el_bit_sticky.html)

¡Ánimo que lo estás haciendo muy bien!, recuerda que la mejor forma de aprender es poniendo en práctica todo lo que vayas aprendiendo.

----

## Uso del Sticky Bit para Proteger Archivos en Directorios Compartidos

En este momento, nos encontramos como el usuario `sk8ware`. Nos dirigimos a nuestro escritorio `Desktop` y, como usuario `root`, creamos un directorio `pruebaspepito` y cambiamos su propietario y grupo a `pepe`.

### Creación y Configuración de Directorio

Primero, creamos el directorio y cambiamos el propietario y grupo:

```sh
mkdir /home/sk8ware/Desktop/pruebaspepito chown pepe:pepe /home/sk8ware/Desktop/pruebaspepito/
```

### Modificación de Permisos

Cambiamos los permisos para que el grupo y otros puedan escribir en el directorio. Esto se puede hacer de dos maneras:

1. Utilizando opciones específicas:
    
```sh
chmod g+w,o+w /home/sk8ware/Desktop/pruebaspepito/`
```

2. Asignando permisos completos (lectura, escritura y ejecución para todos):
    
```sh 
chmod 777 /home/sk8ware/Desktop/pruebaspepito/`
```    

### Creación y Manipulación de Archivos

Nos logueamos como `pepe`, navegamos al directorio `pruebaspepito`, y creamos un archivo:

```sh
su pepe cd /home/sk8ware/Desktop/pruebaspepito echo "hola probando" > file.txt
```

Luego, salimos de la sesión de `pepe` y volvemos a nuestro usuario `sk8ware`. Verificamos los permisos del archivo creado:

```sh
ls -l /home/sk8ware/Desktop/pruebaspepito
```

Notamos que, aunque `sk8ware` no tiene permisos de alterar el archivo, el directorio `pruebaspepito` tiene permisos completos para otros. Por lo tanto, podemos eliminar el archivo:

```sh
rm /home/sk8ware/Desktop/pruebaspepito/file.txt
```

### Protección con Sticky Bit

Para evitar que los archivos creados por un usuario sean eliminados por otros usuarios que tienen permisos de escritura en el directorio, usamos el `Sticky Bit`. Esto garantiza que solo el propietario del archivo (o el root) pueda eliminar o renombrar los archivos en el directorio.

#### Aplicación del Sticky Bit

Nos logueamos de nuevo como `pepe` y aplicamos el `Sticky Bit` al directorio `pruebaspepito`:

```sh
su pepe cd /home/sk8ware/Desktop 
chmod +t pruebaspepito/
```

Verificamos los permisos del directorio para asegurarnos de que el `Sticky Bit` se ha aplicado correctamente:

```sh
ls -ld /home/sk8ware/Desktop/pruebaspepito
```

El permiso del directorio debería mostrarse como `drwxrwxrwt`, donde la `t` al final indica que el `Sticky Bit` está activado.

### Efecto del Sticky Bit

Ahora, si creamos de nuevo un archivo en el directorio `pruebaspepito` y tratamos de eliminarlo desde el usuario `sk8ware`, veremos que no se permite la eliminación:

1. Crear el archivo como `pepe`:
    
```sh
su pepe 
cd /home/sk8ware/Desktop/pruebaspepito 
echo "nuevo archivo" > file.txt`
```    
2. Intentar eliminarlo como `sk8ware`:
    
```sh
su sk8ware rm /home/sk8ware/Desktop/pruebaspepito/file.txt`
```    

El sistema no permitirá la eliminación, mostrando un mensaje de "Operación no permitida".

### Resumen del Sticky Bit

El `Sticky Bit` es una herramienta esencial para proteger archivos en directorios compartidos, evitando que usuarios no propietarios eliminen o renombren archivos que no les pertenecen. Es especialmente útil en directorios como `/tmp`, donde múltiples usuarios tienen permisos de escritura.