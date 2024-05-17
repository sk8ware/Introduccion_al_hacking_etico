

1.- ### 1. ¿Cuál sería la expresión a establecer para una tarea Cron que quiero que se ejecute al tercer minuto de cada hora?

3 * * * *
2. ### ¿Qué conseguimos con la operatoria 3>&1 1>&2 2>&3?
Conseguimos intercambiar stderr con stdout y stdout con stderr

3. ### ¿Qué vías válidas tendríamos para filtrar por la tercera línea de este script?
2,3y4

4. ### ¿Qué estaré mostrando por consola con este comando?
Estaré mostrando el contenido de la variable de entorno

5. ### Si quiero asignar el permiso 676 en octal a un directorio, ¿cómo quedarán representados los permisos finales para este directorio?
rw-rwxrw-

6. ### ¿Con qué comando puedo crear un enlace?
ln

7. ### ¿Es posible que 2 archivos o más posean la misma ruta absoluta?
No

8. ### ¿Cuál sería la expresión a establecer para una tarea Cron que quiero que se ejecute cada minuto, cada 2 horas? 
```
* */2 * * *
```

9. ### En consola, ¿cómo podemos autocompletar?
Con TAB

10. ### ¿Dónde se guardan los archivos de configuración del sistema?
```
/etc
```

11. ### ¿De qué forma puedo indicar que quiero ejecutar una tarea cron a las 02:10 AM, cada 2 días de la semana?
```markdown
10 2 */2 * *
```

12. ### ¿Qué se estará mostrando por consola una vez ejecutado el último comando?
ip6-allnodes

13. ### ¿Con qué comando puedo cambiar el propietario de un archivo?
Chown

14. ### ¿Cuál sería la expresión a establecer para una tarea Cron que quiero que se ejecute cada minuto, en el día 10 del mes, cada 2 meses?
```markdown
* * 10 */2 *
```

15. ### ¿Si quiero ocultar el stderr de un comando, cómo lo podría hacer?
Metiéndole un 2>/dev/null al final

16. ### ¿De qué forma puedo mostrar sólo las 3 últimas líneas de este archivo concreto?
cat /etc/hosts | tail -n 3

17. ### . ¿Cuál sería la expresión a establecer para una tarea Cron que quiero que se ejecute al tercer minuto de cada hora?
```
3 * * * *
```

18. ### ¿Cómo puedo mostrar por consola únicamente la versión de kernel que tengo?
uname -r

19. ### ¿Qué comando puedo emplear para conocer el nombre de la máquina en la que estoy conectado?
hostname

20. ### ¿Cómo puedo indicar en una misma línea que el stderr del último comando a ejecutar se introduzca en el archivo 'file' y el stdout en el archivo ‘file_two’?
![[Pasted image 20240517143844.png]]
```
2>&1 >&8 1>&7
```

21. ### ¿Qué significa ./?
Representa el directorio actual

22. ### ¿Qué comando puedo utilizar para ver las variables de entorno de mi sesión?
env

23. ### ¿Qué conseguiremos con este comando?
*touch file.{sumary,report,results}*

24. ### ¿Con qué comando podemos matar un proceso?
```bash
kill
```

25. ### ¿Con qué comando puedo saber en qué directorio me sitúo?
pwd

26. ### ¿De qué forma puedo indicar que quiero ejecutar una tarea cron a las 02:10 AM, cada 2 días de la semana?
```markdown
10 2 */2 * *
```

27. ### ¿Cómo puedo indicar que quiero ejecutar una tarea Cron cada minuto, en el primer día del mes sólo para el mes de Febrero y los días Miércoles?
```bash
* * 1 2 3
```

28. ### ¿Qué se mostrará por consola una vez se ejecute el siguiente comando?
*whoam && echo test || echo test2 *

El comando devolverá un error y mostrará la cadena test2

29. ### ¿Qué expresión tendré que introducir a continuación para cambiar todas las palabras donde ponga ‘root’ por ‘user’ haciendo uso del comando ‘sed’?
*cat /etc/passwd | head -n 1 |*
```
sed ' s/root/user/g'
```

30. ### ¿Existen físicamente todos los dispositivos que hay en '/dev'?
No

31. ### Empareja cada permiso con su representación octal correspondiente
1. **r--r-xr--** - **454**
2. **----w---x** - **021**
3. **r-x-w-r-x** - **525**
4. **-w-r-x-w-** - **252**
5. **rwsr--r-x** - **4745**
6. **rwSr--r-x** - **4645**

32. ### ¿Se almacenará así el stderr del comando indicado entre paréntesis en el archivo 'file'?
Verdadero

33. ### ¿Cuál sería la expresión a establecer para una tarea Cron que quiero que se ejecute cada minuto, sólo los Sábados?
```
* * * * 6
```

34. ### ¿Cómo hago para copiar ‘archivo1' a ‘archivo2’ que está en el directorio ‘/home/usuario/’?
```
cp archivo1 /home/usuario/archivo2
```

35. ### 5. ¿Qué pasará cuando ejecute el último comando?
![[pruebalinux1.png]]
La ejecución causará un error, dado que el descriptor de archivo indicado ha sido cerrado

36. ### ¿Cuál sería la expresión a establecer para una tarea Cron que quiero que se ejecute cada 3 minutos?
```
*/3 * * * *
```

37. ### ¿Cómo podría declarar en una línea un array que reúna las siguientes especificaciones en un script de Bash?
![[pruebalinux.png]]
elementos=(a b c d e)

38. ### ¿Cuál sería la expresión a establecer para una tarea Cron que quiero que se ejecute cada minuto, en el día 10 del mes, cada 2 meses?
```
* * 10 */2 *
```

39. ### ¿Qué conseguimos con la operatoria 3>&1 1>&2 2>&3?
Conseguimos intercambiar stderr con stdout y stdout con stderr


40. ### ¿Cuál sería la expresión a establecer para una tarea Cron que quiero que se ejecute cada minuto, sólo los Sábados?
```markdown
* * * * 6
```

41. ### Si quiero asignar el permiso 123 en octal a un fichero, ¿cómo quedarán representados los permisos finales para este fichero?
```
--x-w--wx
```

42. ### Estoy perdido en el árbol de directorios, ¿cómo puedo volver a mi HOME?
```
cd
```

43. Esto puedo hacerlo incorporando un  al final de mi instrucción.
```
&
```

44. ### ¿Con qué comando puedo traer un proceso en segundo plano al primer plano?
```
fg
```

45. ### ¿Cada cuánto se estaría ejecutando esta tarea?
![[Pasted image 20240517104905.png]]
```
Cada minuto, cada 2 días
```

46. ### ¿De qué forma puedo iterar sobre las líneas de un archivo tras aplicar un cat sobre este e incorporar un pipe al final de la misma línea? (Consideremos almacenar el valor de cada línea por cada iteración en una variable con nombre ‘value’)
```
| while IFS= read -r value; do echo "$value"; done
```

47. ### ¿Qué formas correctas tendríamos en Bash para aplicar una suma entre dos números?

2+5

2+5 | bash

(2+5) | bash

echo (2+5)

- [-] echo 2+5 | bc

- [-] echo "2+5" | bc

echo $(2+5) | bc

 - [-] echo $((2+5)) | bc
 
- [-] echo $((2+5))

48. ### ¿Cómo hago para saber el tiempo que tarda en ejecutarse un comando?
```
time ls -l
```

49. ### . ¿Es el Kernel el núcleo del sistema operativo?
```
verdader
```

50.  ### ¿Qué se va a almacenar en el archivo 'file' tras ejecutar el comando indicado?
![[Pasted image 20240517140830.png]]
(whoami 3>&1 1>&2 2>&3) > file 
```
Salida del stdout al archivo file
```

51. ### ¿Qué conseguimos con la operatoria 3>&1 1>&2 2>&3?
```
Conseguimos intercambiar stderr con stdout y stdout con stderr
```

52. ### ¿Cuál es la representación en octal del siguiente permiso?
![[Pasted image 20240517141548.png]]
.--x-----x
```
101
```

53. ### ¿Qué se almacenará en el archivo file?
![[Pasted image 20240517142857.png]]
excec 3<> file 
whoam 2>&3

- [-] Los errores del comando ejecutado  
- [-] El stderr

54. ### ¿Qué se estará almacenando en el archivo file tras la ejecución del último comando?
![[Pasted image 20240517144006.png]]
exec 3<> file
exec 4>&3
whoami 2>&1 >&4

```
2.- El stderr del comando 'whoami'
```

55. ### ¿En qué directorios se guardan generalmente los programas?