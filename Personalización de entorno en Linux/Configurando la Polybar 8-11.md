
----
- TAG: #CONFIGURANDO #POLYBAR 
-----
## Ahora empezaremos con la configuración de la polybar 
Dentro de nuestro directorio *.config* tenemos la ruta *polybar*, En esta ruta encontraremos dos archivos importantes el *launch.sh* y por otro lado el *current.ini* 

*launch.sh* .- Define los elementos o la barras que nosotros estamos cargando,  Si ponemos un # al principio de *top* por ejemplo podríamos quitar de la polybar la parte del wifi y sonido 

*current.ini* .- Es un archivo de configuración que se utiliza para definir cómo se muestra la información en la barra, como el contenido y el estilo de los módulos.
- Ingresamos al modulo *current.ini* y filtamos con `Ctrl + W` para buscar *log* y en el apartado de *width:2.5* modificamos el ancho del primer modulo de la parte izquierda donde se ubica el logo personal.
# Ejemplo del bar/log configurado:
```
[bar/log]
inherit = bar/main
width = 3%
height = 30
offset-x = 1%
offset-y = 15
bottom = false
foreground = ${color.white}
background = ${color.bg}
padding = 0
modules-center = my-text-label
wm-restack = bspwm
;override-redirect = true
```

- Si filtramos por *my-text-label* podemos cambiar el icono en la parte de *content*:
```
[module/my-text-label]
type = custom/text
content = %{T7}  (alien)
;interval = 1.0
;time = %k : %M
;date = %b %e
;format = <label1>
;format-foreground = ${color.white}
;label1 = aadasd
;label1-font = 7
```
Y si actualizamos nos daremos cuenta que no aparece porque esta contemplando un {T7} que no existe, para ello debemos crearlo de la siguiente manera
- Filtramos por *font-* y veremos algo asi:
```
font-0 = "Iosevka Nerd Font:size=13;3"
font-1 = "Iosevka Nerd Font:bold:size=24;2"
font-2 = "Iosevka Nerd Font:size=22;6"
font-3 = "Source Code Pro:size=10;3"
font-5 = "Helvetica Rounded:style=Bold:size=10.5;3"
font-4 = "Montserrat Medium:style=Medium:size=12;3"
font-6 = "Hurmit Nerd Font Mono:style=medium:pixelsize=17;3"
```
- En esta parte crearemos la septima font `font-7 = "Hack Nerd Font Mono:size=20;6"`, Refrescamos y ya estará resuelto el problema.
----
# Ahora configuraremos la parte de la dirección ip
Nos abrimos el archivo `launch.sh` y configuramos el nombre del apartado *secondary* y lo ponemos como *ethernet_bar* y este nombre debe contemplarse en el archivo `current.ini`

Guardamos e ingresamos a al *current.ini* y filtramos por *secondary* copiamos esta sección:
```
[bar/secondary]
inherit = bar/main
width = 8%
height = 30
offset-x = 4.3%
offset-y = 15
background = ${color.bg}
foreground = ${color.white}
bottom = false
padding = 1
;padding-top = 2 
module-margin-left = 0
module-margin-right = 0
;modules-left = date sep mpd
modules-center = date
wm-restack = bspwm
```

Y luego la pegamos en la parte de arriba, pero cambiando el nombre a [Ethernet_bar], ahora si actualizamos se va a reflejar la fecha pero solo hace falta cambiar el modulo si lo desea, esta vez la dejaremos ya que si me interesa ver la hora y fecha.

Pero para el ejemplo debemos configurar en la partde *modules-center* borrar el date y poner *ethernet_status*

Ahora filtramos por *module/date* y al final del apartado de module ingresamos el nuevo modulo de ethernet de la siguiente manera:
```
[module/Ethernet_status]
type = custom/script
interval = 2 
exec = ~/.config/scripts/ethernet_status
```

 - Para que funcione correctamente este es un script que debe ser creado en la ruta indicada con `touch ethernet_status.sh` y le otorgamos permisos de ejecución con `chmod +x ethernet_status` y luego lo editamos con `nano`:
 ```
 #!/bin/sh

echo "%{F#2495e7}ICONO %{F#ffffff}$(/usr/sbin/ifconfig ens33 | grep "inet " | awk '{print $2}')%{u-}"
 ```

 Y en la parte de *ICONO* colocamos el icono de ethernet a nuestro gusto, Luego de eso nos abrimos nuestro archivo `.zshrc` y agregamos *:/usr/games:`/usr/sbin`* 

 Hay que verificar que este correcta la ruta en el modulo *ethernet_status* en el *current.ini*
 `exec = ~/.config/bspwm/scripts/ethernet_status` 

-----
# Ahora agregaremos la parte de la VPN de HTB

Nos abrimos nuestro archivo *launch.sh* y debajo del modulo de *ethernet_bar* creamos la siguiente línea:

```
polybar vpn_bar -c ~/.config/polybar/current.ini & 
```

Ahora el modulo *vpn_bar* debe existir en *current.ini*, filtramos por *ethernet_bar* y copiamos todo el apartado con las configuraciones y justamente arriba para definir *vpn_bar*

Si guardamos y refrescamos se van a superponer encima de la ip y para poderle mover a la derecha debemos configurar el `offset-x = 14` y en *modules-center* poner el modulo  *vpn_status* 

Filtramos por *ethernet_status* en el apartado de modulos, para agregar lo siguiente:

```
[module/vpn_status]
type = custom/script
interval = 2 
exec = ~/.config/scripts/vpn_status
``` 

Nos dirigimos a nuestra carpeta `cd ~/.config/bspwm/scripts` y aqui crearemos el siguiente archivo *touch vpn_status* e ingresamos estos datos:

```
#!/bin/sh

IFACE=$(/usr/sbin/ifconfig | grep tun0 | awk '{print $1}' | tr -d ':')

if [ "$IFACE" = "tun0" ]; then

    echo "%{F#1bbf3e}ICONO %{F#ffffff}$(/usr/sbin/ifconfig tun0 | grep "inet " | awk '{print $2}')%{u-}"

else

    echo "%{F#1bbf3e}ICONO %{u-} Disconnected"

fi
``` 

Cambiamos el icono en *NerdFonts* por un cuadrado como el de *HTB*

Le otorgamos permisos de ejecución con *chmod +x vpn_status.sh* 

Y por ultimo terminamos configurando el botón de apagado en la ruta `cd ~/.config/polybar` y nos abrimos el *launch.sh* y vemos que se llama *primary* el botón de la derecha
Así que vamos al *current.ini* y filtramos por *primary* y en *background* cambiamos a *bg* el color.