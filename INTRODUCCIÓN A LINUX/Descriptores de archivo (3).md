
----
- TAG:  #DESCRIPTORES #ARCHIVOS 
----
Por aquí les dejo algunos recursos de apoyo para profundizar sobre el uso de descriptores de archivo en Bash:

-  Redirectores en Bash [Formato PDF]: [https://hack4u.io/wp-content/uploads/2022/05/bash-redirections-cheat-sheet.pdf](https://hack4u.io/wp-content/uploads/2022/05/bash-redirections-cheat-sheet.pdf)

Esta parte es fundamental, sobre todo de cara a las clases de scripting en Bash que tendremos más adelante, pues haremos mucho uso de estos.

----
Podemos crear un descriptor de archivo de la siguiente manera identificado con el numero `3` 
```
exec 3 <> file 
``` 

Nos crea un archivo vacio con poder de lectura y escritura, si solo queremos lectura solo utilizariamos el menor `< ` y para poder escribir le podemos usar el `>` 

Ahora si realizamos la siguiente función nos enviara nuestro output al archivo ` file ` 
```
whoami >&3
```

Si realizamos la misma función con otros comandos, todos los output se derigiran al archivo **file** 

Ahora si queremos terminar el descriptor de archivo creado con la siguiente función 
```
exec  3>&- 
```

Pero esto no significa que el contenido se haya borrado, si quisieramos enviar nuevos outputs al archivo file la terminal nos mostraría un error ya que ese archivo no existe

Ahora imaginemos que queremos copiar la información entre descriptores de archivo, seria de la siguiente manera
```
exec 5>&3
```

Con el archivo `5` ahora tendremos posibilidad de guardar la información en el descriptor de archivo `3` , ahora por ejemplo si nos abrimos el archivo
```
cat data
```
Veremos que se guardo correctamente la información, con esto podriamos obtener copias y cerrar la que no necesitemos

