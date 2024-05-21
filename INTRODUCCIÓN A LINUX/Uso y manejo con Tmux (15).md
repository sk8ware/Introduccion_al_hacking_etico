
----
- TAG: #MANEJO #TMUX 
----
>Para tener todos los atajos y comandos de Tmux centralizados, hemos creado la siguiente guía la cual esperamos que le puedas sacar provecho:

- Guía de atajos y comandos de Tmux: [https://hack4u.io/wp-content/uploads/2022/05/Tmux-Cheat-Sheet.pdf](https://hack4u.io/wp-content/uploads/2022/05/Tmux-Cheat-Sheet.pdf)
-----
De primera solemos tener instalada la aplicación de tmux en nuestro sistema, pero si no lo tienen lo pueden hacer facilmente con `apt install tmux`  o buscarlo con `apt search tmux` 

Si sale un error al abrir el tmux por primera vez pueden realizar 
```
touch ~/.hushlogin
```

Por lo general siempre viene con un diseño predeterminado lo cual lo podemos modificar con [oh my tmux](https://github.com/gpakosz/.tmux)  en un repositorio de `git hub` y seguimos las instrucciones que nos indica tanto como sk8ware y root
(En caso de que no se aplique la configuración en usuario no provilegiado use `tmux kill-server` y volver a realizar los pasos de `git hub` )

El primer numero que indica a la izquierda es numero de sesión que muestra por defecto el `0` con `tmux new -s Academia` o si ya te encuentras adentro de **tmux** puedes hacer un `Ctrl + b (sueltas) + Shift + 4` 
Una vez instala y dentro de `tmux` podemos ejecutar `Ctrl + b (sueltas) + ,` para renombrar la pagina actual 
Para crear una nueva ventana sería, `Ctrl + b (sueltas) + c` y la puede volver a renombrar
Para moverte por ventanas es `Ctrl + b (sueltas) + 1` para ir a la ventana 1
Para realizarlo con el teclado sería `Ctrl + m (sueltas) + mouse` puedes activar el control de mouse en tmux
Para abrir una ventana debajo y poder maniobrar en doble pantalla seria con `Ctrl + b (sueltas) + Shift + 2` o de forma lateral con `Ctrl + b (sueltas) + Shift + 5 ` 
Para maniobrar en ambas ventanas podemos utilizar `Ctrl + b (sueltas) + O ` o con las flechas para arriba y abajo
Si queremos abrirnos una tercera ventana seria de igual manera con `Ctrl + b (sueltas) + Shift + 2` y para maniobrar de igual manera con `Ctrl + b (sueltas) + O `
Para cerrar la ventana se puede utilizar `exit` o `Ctrl + b (sueltas) + x ` 
Para ajustar el `size` podemos salir al modo mouse con `Ctrl + m (sueltas) + mouse` o `Ctrl + b + (tener aplastado el Ctrl y mover con las teclas)`

Algo para tomar en cuenta es que si hacemos un `cat /etc/hosts` y hace un `Ctrl + Shift + c` para copiar y `Ctrl + Shift + v` para pegar, hay otra manera para poderlo hacer `Ctrl + b (sueltas) + shift + [ ` nos movemos por la lineas para copiar la que deseemos y selecionar lo que queremos copiar con `Ctrl + espacio ` y para poder copiar el la clipboard podemos hacer `Alt + W ` 
Para pegarlo podemos hacer un `Ctrl + b (sueltas) + shift + ] ` 

Viene bueno utilizar **tmux** cuando realizamos varios procesos en segundo plano con `Ctrl + b (sueltas) + D` hace un detachet y cerramos la ventana y podemos ver la sesiones abiertas en tmux con la siguiente función `tmux list-sessions`
Para conectarnos a esta sesión podemos hacer un `tmux attach` si solo es una, si es una en especifico puede ser con `tmux attach -t Academia`
Para migrar de sesion en caso de que tengamos mas de 2 podemos hacer `Ctrl + b (sueltas) + W` 