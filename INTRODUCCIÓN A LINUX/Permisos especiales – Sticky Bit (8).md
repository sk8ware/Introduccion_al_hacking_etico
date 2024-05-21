
----
- TAG: #PERMISOS #ESPECIALES #STICKY #BIT 
----
>¿Quieres entender mejor el Sticky Bit?, puedes profundizar en los siguientes enlaces de interés que te comparto:

- ¿Qué es el Sticky Bit y cómo configurarlo?: [https://keepcoding.io/blog/que-es-el-sticky-bit-y-como-configurarlo/](https://keepcoding.io/blog/que-es-el-sticky-bit-y-como-configurarlo/)
- El bit Sticky | Tutorial de GNU/Linux: [https://www.fpgenred.es/GNU-Linux/el_bit_sticky.html](https://www.fpgenred.es/GNU-Linux/el_bit_sticky.html)

¡Ánimo que lo estás haciendo muy bien!, recuerda que la mejor forma de aprender es poniendo en práctica todo lo que vayas aprendiendo.

----

En este momento nos encontramos como usuario `sk8ware` y nos dirigimos a nuestro escritorio `Desktop` y como usuario `root` nos creamos un directorio `pruebaspepito` y le cambiamos de grupos 
```
chown pepe:pepe pruebaspepito/
```


Y ahora le cambiamos los permisos para se pueda escribir en grupos y otros, lo podemos hacer de dos maneras 
```
chmod g+w,o+w pruebaspepito/
```

O de la manera que les habia enseñado con 
```
chmod 777 pruebaspepito/
```

Nos logeamos como `pepe` al directorio `pruebas pepito` y creamos un archivo `echo hola probando` y lo metemos en `> file.txt` 
Y ahora salimos y desde nuestro escritorio `sk8ware` podemos darnos cuenta que el archivo fue creado en nuestra maquina y vemos que en los permisos despues del `ls -l` no tenemos permisos de alterar el archivo, pero el directorio `pruebas pepito` si tiene todos los permisos para otros, asi que si hacemos un `rm file.txt` se eliminara dado a que el permiso que le precede si tiene permiso que se manipule archivos 

Para evitar que nos suceda esto podemos logearnos de nuevo como `pepe` y regresar a la ruta donde podamos ver el directorio `pruebas pepito` y le aplicamos el `Sticky Bit` de la siguiente manera 
```
chmod +t pruebaspepito/ 
```

Ahora lo que consegimos con esto 