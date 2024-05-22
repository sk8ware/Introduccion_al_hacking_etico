
----
-  TAG :  #BUSQUEDA #A-NIVEL-DE-SISTEMA
----
Aveces cuando compremetemos una maquina solemos revisar en que grupo pertenecemos con `id ` para intentar hacer busquedas a nivel de sistema de forma recursiva para detectar archivos o directorios que contengan ese grupo y varios permisos, por ejemplo si buscamos por `find / -name passwd ` pero como no estamos como root y posiblemente no tengamos acceso a varios directorios, asi que aplicamos un `2>/dev/null`
```
find / -name passwd 2>/dev/null 
```

De forma paralela podemos ejecutar `xargs ls -l` 
```
find / -name passwd 2>/dev/null | xargs ls -l
``` 

Recordemos que `xargs` nos permite ejecutar comandos en paralelo y podemos encontrar hasta archivos **suid** 

Para buscar archivos **SUID** desde la raiz 
```
find  / -perm -4000 2>/dev/null
```

Para buscar grupos por directorios 
```
find / -group sk8ware -type d 2>/dev/null
```

y si se usa la `f` de file en la parte de `-type` mostramos todos los archivos 

Ahora buscaremos a usarios que tengan capacidad de escritura 
```
find / -user root -writable 2>/dev/null
```

Y podremos ver todos los directorios con capacidad de escritura, si seleccionamos cualquiera y le hacemos un `ls -l ` veremos los tipos del directorio y ver que otros pueden escribir 

De igual manera con para los archivos ejecutables 
```
find / -user root -executable 2>/dev/null
```
 