
------
- Tag: #BSPWM #SXHKD
-----

Lo primero que haremos es dirigirnos a la carpeta descargas 

Una vez dentro hacemos un `sudo apt update`, para luego instalar las siguientes dependencias

```bash
- **apt install build-essential git vim xcb libxcb-util0-dev libxcb-ewmh-dev libxcb-randr0-dev libxcb-icccm4-dev libxcb-keysyms1-dev libxcb-xinerama0-dev libasound2-dev libxcb-xtest0-dev libxcb-shape0-dev**
```

Lo siguiente seria descargar **bspwm** 

```bash
sudo apt install bspwm
```

O sino directo con las librerias:
```bash
git clone https://github.com/baskerville/bspwm.git
git clone https://github.com/baskerville/sxhkd.git
```

Nos dirigimos a la carpeta de bspwm y sxhkd y realiamos lo siguiente

```bash
make
sudo make install
```

Seguido de eso se cambiara de ruta a `/usr/local/bin/bspwm`


Ahora nos toca crear los siguiente archivos `bspwmrc` y `sxhkdrc`

```bash
mkdir ~/.config/{bspwm,sxhkd}
```

En el directorio **Examples** de cada archivo existe el archivo `bspwmrc` y `sxhkdrc`, si le realizamos un `ls -l` veremos que los archivos tiene permisos de ejecución
 - `bspwmrc` - Es para agregarle nuestras utilidades cuando se cargue el entorno
 - `sxhkdrc` - Es para configurar nuestros atajos de teclado 

Copiamos estos archivos en la siguientes rutas:

```bash
cp bspwmrc ~/.config/bspwm
cp sxhkdrc ~/.config/sxhkd
```



# Configuración de la sxhkd


Hay que tomar en cuenta que cuando queramos confirar algo de este archivo la tecla **Windows** esta representada por la palabra **Super**.
Y el **Return** seria la tecla **Enter**
Debemos estar logeados como **ROOT**

1. Para Abrir la terminal con `Super + Return`
```bash
# terminal emulator
super + Return
        /usr/bin/kitty
```

- La configuramos para usar una kitty como terminal asignando la ruta absoluta de la kitty.
- Tenerla instalada o hacerlo con `sudo apt install kitty`, cuando se la instala de esta manera por lo general siempre suele venir desactualizad, pero ya lo actualizaremos mas adelante

2. Salir de la terminal con `Super + Q`
```bash
# close and kill 
super + {_,shift + }q
        bspc node -{c,k}
```

3. Para recargar el `bspwm`
```bash
# quit/restart bspwm
super + shift + {q,r}
        bspc {quit,wm -r}
```

4. Para movernos por flechas
```bash
# focus the node in the given direction
super + {_,shift + }{Left,Down,Up,Right}
        bspc node -{f,s} {west,south,north,east}
```

5. Para configurar el tamaño de la ventana que vayamos abrir debemos hacer en los **preselectores**
```bash
# preselect the direction
super + ctrl + alt + {Left,Down,Up,Right}
        bspc node -p {west,south,north,east}
```

6. para la cancelar la preseleccion de una ventana
```bash
# cancel the preselection for the focused node
super + ctrl + alt + space
        bspc node -p cancel
```

7. Eliminamos estos dos apartados
```bash
# expand a window by moving one of its side outward
super + alt + {h,j,k,l}
        bspc node -z {left -20 0,bottom 0 20,top 0 -20,right 20 0}

# contract a window by moving one of its side inward
super + alt + shift + {h,j,k,l}
        bspc node -z {right -20 0,top 0 20,bottom 0 -20,left 20 0}

```

8. Para mover la ventana flotante de la terminal 
```bash
# move a floating window    
super + shift + {Left,Down,Up,Right}
        bspc node -v {-20 0,0 20,0 -20,20 0}
```

9. Para ajustar el tamaño de la ventana con las flechas
```bash
# Custom Resize
super + shift + {Left,Down,Up,Right}
    /home/kali/.config/bspwm/scripts/bspwm_resize{west,south,north,east}
```

Guardamos las configuraciones con `Ctrl + s` y salimos.

10. Creamos el archivo `Resize` como usuarios no privilegiados.
```bash
cd /home/kali/.config/bspwm/
mkdir scripts
cd !$
touch bspwm_resize
chmod +x bspwm_resize
nano bspwm_resize
```

En el archivo `bspwm_resize` debemos guardar lo siguiente:
```bash
#!/usr/bin/env dash

if bspc query -N -n focused.floating > /dev/null; then
	step=20
else
	step=100
fi

case "$1" in
	west) dir=right; falldir=left; x="-$step"; y=0;;
	east) dir=right; falldir=left; x="$step"; y=0;;
	north) dir=top; falldir=bottom; x=0; y="-$step";;
	south) dir=top; falldir=bottom; x=0; y="$step";;
esac

bspc node -z "$dir" "$x" "$y" || bspc node -z "$falldir" "$x" "$y"
```

-----


**Bspwm (Binary Space Partitioning Window Manager)**

Bspwm es un gestor de ventanas que utiliza la técnica de partición binaria del espacio para organizar las ventanas en el escritorio. Es conocido por su simplicidad y eficiencia, ya que se configura y se controla exclusivamente a través de scripts y comandos en la terminal. Bspwm no maneja teclados ni otros dispositivos de entrada por sí mismo, sino que delega esta tarea a otras herramientas, lo que permite una mayor personalización y flexibilidad.

Cada ventana se organiza automáticamente de manera que ocupe un área divisoria del espacio disponible en el escritorio, optimizando el uso del espacio y facilitando la navegación entre diferentes aplicaciones y documentos abiertos.

**  
Sxhkd (Simple X Hotkey Daemon)**

Sxhkd es un demonio de teclas de acceso rápido para sistemas X Window. Funciona en conjunto con gestores de ventanas como Bspwm y permite a los usuarios asignar acciones a combinaciones de teclas y botones del mouse. Su configuración se realiza a través de un archivo de texto plano, donde el usuario define las combinaciones de teclas y las acciones correspondientes que se deben ejecutar. Sxhkd es altamente configurable y ligero, diseñado para ser rápido y eficiente en el manejo de eventos de entrada, lo que lo hace ideal para entornos donde los recursos del sistema son limitados o cuando se busca una experiencia de usuario altamente personalizable y controlada.

Ambos programas son muy populares en la comunidad de entusiastas de Linux que prefieren un entorno de escritorio altamente personalizable y orientado al uso de teclado.