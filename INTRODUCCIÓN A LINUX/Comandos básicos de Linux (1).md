
-----
- TAG: #INTRODUCCIÓN #LINUX #COMANDOS #BASICOS
------
Les dejo por aquí algunas guías de interés para repasar comandos básicos de Linux:

-  Chuleta de comandos Linux: [https://ciberninjas.com/chuleta-comandos-linux/](https://ciberninjas.com/chuleta-comandos-linux/)

Esto que puede parecer una tontería para algunos… no lo es, ya que son comandos básicos fundamentales sobre los cuales acostumbraremos a maniobrar de cara al futuro. Jamás olvides tus orígenes.

Por aquí les dejo material de apoyo adicional para que puedan repasar y curiosear más comandos:

- Comandos básicos de Linux: [https://www.bonaval.com/kb/cheats-chuletas/comandos-basicos-linux](https://www.bonaval.com/kb/cheats-chuletas/comandos-basicos-linux)
- Guía en PDF de comandos básicos de Linux: [https://www.fing.edu.uy/inco/cursos/sistoper/recursosLaboratorio/tutorial0.pdf](https://www.fing.edu.uy/inco/cursos/sistoper/recursosLaboratorio/tutorial0.pdf)


------
Cuando nos abrimos una terminal nosotros somos alguien, si abrimos la consola y hacemos un `whoami` podríamos ver el tipo de usuario que somos, a su vez tambien podemos ver los nombres de usuarios `id` para asi ver los nombres importantes para poder escalar privilegios.

Escalar privigilegios es sencillamente pasar de un usuario no privilegiado a root, asi que ahora entienden por donde va la cosaa eh ;) por ejemplo en pentesting cuando dicen que han vulnerado una maquina, ahora toca rootearla, significa que tenemos que escalar los privilegios a root 

Todos los usuarios los podemos ver en la ruta 
```
/etc/group 
```

Si queremos contemplar algún binario desde consola deberiamos de observar nuestro `$PATH` para crear ese nuevo binero y agregarlo al final nuestra ruta absoluta, el orden siempre es de prioridad de izquierda a derecha

Hay ejemplos de hacking como **PATH hijacking** = Este tipo de ataque se aprovecha de la confianza del sistema en la variable PATH para encontrar y ejecutar programas, y puede ser especialmente efectivo en sistemas donde los usuarios no prestan atención a la configuración de sus variables de entorno.

Cuando queramos filtrar dentro de tanta data en consolta con la respuesta de **output** lo podemos hacer con ` grep `
```
/bin/cat /etc/group | grep  "floppy" -n
```

Para saber nuestra ruta podemos usar `pwd ` y en el directorio podemos ver el contenido del directorio actual con `ls` 

Para ver y listar los permisos avanzados de cada carpeta, documento o archivo lo podemos realizar con ` ls -l `
Estos archivos y configuraciones son muy importantes para que la puedan romper, asi que cuidado con estas configuraciones en enternos empresariales.

Con `cd ` podemos cambiar de directorio, significa **Change Directory**

Para ir a la raíz del sistema operativo tengo que dirigirme a ` cd / ` 

Para ver nuestra ruta y tipo de **SHELL** podemos verlo con ` echo $SHELL` 

Para ver los tipos de **SHELLS** ` cat /etc/shells ` y podemos migrar a cualquiera de esas shells simplemente aplastando `bash` en la terminal o el tipo de shell que queramos utilizar.