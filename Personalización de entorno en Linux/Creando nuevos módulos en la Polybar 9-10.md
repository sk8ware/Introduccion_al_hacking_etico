
----
- TAG: #NUEVOS #MODULOS #POLYBAR 
-----
# Vamos a desplegar el modulo "Target" en la polybar

Este apartado nos permite visualizar en todo momento nuestra dirección ip para atacar con la función `settarget ip - Nombre de la maquina"` mandamos la información al *target*.

Nos dirigimos a `.config` a la carpeta de *polybar* e ingresamos a la configuración *launch.sh* 

Lo podemos ingresar antes del modulo *primary* 

```
polybar target_to_hack -c ~/.config/polybar/current.ini &
```

Ahora abrimos el archivo *current.ini* y filtramos por *secondary*, es lo mismo que hemos hecho, copiamos toda la configuración de *bar/secondary*, lo pegamos arriba y le cambiamos al nombre que hemos creado *target_to_hack*

```
[bar/target_to_hack]
inherit = bar/main
width = 18%
height = 30
offset-x = 72.45%
offset-y = 15
background = ${color.bg}
foreground = ${color.white}
bottom = false
padding = 1
;padding-top = 2
module-margin-left = 0
module-margin-right = 0
;modules-left = date sep mpd
modules-center = htb_target
wm-restack = bspwm 
```

Añadimos el nuevo modulo de la siguiente manera

```
[module/target_to_hack]
type = custom/script
interval = 2
exec = ~/.config/bspwm/scripts/htb_target.sh
```

En la ruta que *scripts* de *bspwm* creamos el archivo `touch htb_target.sh`, le damos permisos de ejecución con `chmod +x htb_target.sh` 

En el archivo `htb_target.sh` ingresamos el siguiente pastebin

```
#!/bin/bash

ip_address=$(/bin/cat /home/sk8ware/.config/bin/target | awk '{print $1}')

machine_name=$(/bin/cat /home/sk8ware/.config/bin/target | awk '{print $2}')

if [ $ip_address ] && [ $machine_name ]; then

    echo "%{F#e51d0b}ICONO %{F#ffffff}$ip_address%{u-} - $machine_name"

else

    echo "%{F#e51d0b}ICONO %{u-}%{F#ffffff} No target"

fi
```

Vale recalcar que hace falta cambiar *sk8ware* por su nombre de usuario en su maquina, adicional cambiar el icono a nuestro gusto

Si no tenemos directorio *bin* lo creamos rápidamente con `mkdir bin` en *~/.config* y creamos el archivo `touch target` 

## Ahora vamos a definir la función `settarget` y `cleartarget`

Hay que definir lo siguiente en la ruta `nano /home/sk8ware/.zshrc` 

Podemos definir `Settarget` en cualquier lugar con :

```
# Custom functions
---------------------------------------------------------
# Set Victim Target

function settarget(){

    ip_address=$1

    machine_name=$2

    echo "$ip_address $machine_name" > /home/s4vitar/.config/bin/target

}
```

Debajo de esta función colocamos la *Clear Target*

```
# Clear Victim Target

function cleartarget(){

    echo '' > /home/s4vitar/.config/bin/target

}
```

Ahora si enviamos un `settarget` deberiamos ver en el modulo la información enviada

## Para finalizar tocaremos el espacio de trabajo que se encuentra en `workspace.ini` 

En esta configuración podemos definir los colores y figuras que se muestran en el espacio de trabajo 

Filtramos por `occupied` y podemos ir configurando a nuestro gusto el espacio de trabajo

Y para finalizar utilizaremos la herramienta **FZF** que nos permite usar un buscador mucho mas eficiente y actual [Repositorio FZF](https://github.com/junegunn/fzf) 

```
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install
```

Este comando debemos hacerlo tanto como sk8ware como root

Ahora con *Ctrl + T* nos permite realizar acciones como `cat Ctrl + t` y buscar una ruta absoluta por ejemplo

Si escribimos una palabra incompleta como `who` y aplastamos `Ctrl + R` y ver funciones anteriores iniciadas con esas palabras

-----
### En caso de que presentemos algún problema podemos realizar el siguiente procedimiento

Se realiza un `pkill polybar` para matar el proceso de la polybar

Ejecutamos la `polybar` para poder ver el error que produce el conflicto en la polybar

Si revisamos el archivo y esta todo bien y refleja que existe después de un `file /home/sk8ware/.config/bin/target`
Nos muestra que si existe pero se encuentra vacío 

Si vamos al archivo *lauch.sh* y marcamos algunos plugins con # y recargamos para probar y verificamos que no es ninguno de esos 

Ahora probamos con el *current.ini* y revisamos alguna falla en palabras o modulos repetidos, por ejemplo desplegamos manualmente la siguiente linea y leemos el mensaje que nos indique:

```
polybar secondary -c ~/.config/polybar/current.ini 
```

Y nos indica que hemos duplicado *vpn_status*
