
------
- Tag: #BSPWM #SXHKD
-----
**Bspwm (Binary Space Partitioning Window Manager)**

Bspwm es un gestor de ventanas que utiliza la técnica de partición binaria del espacio para organizar las ventanas en el escritorio. Es conocido por su simplicidad y eficiencia, ya que se configura y se controla exclusivamente a través de scripts y comandos en la terminal. Bspwm no maneja teclados ni otros dispositivos de entrada por sí mismo, sino que delega esta tarea a otras herramientas, lo que permite una mayor personalización y flexibilidad.

Cada ventana se organiza automáticamente de manera que ocupe un área divisoria del espacio disponible en el escritorio, optimizando el uso del espacio y facilitando la navegación entre diferentes aplicaciones y documentos abiertos.

  
**Sxhkd (Simple X Hotkey Daemon)**

Sxhkd es un demonio de teclas de acceso rápido para sistemas X Window. Funciona en conjunto con gestores de ventanas como Bspwm y permite a los usuarios asignar acciones a combinaciones de teclas y botones del mouse. Su configuración se realiza a través de un archivo de texto plano, donde el usuario define las combinaciones de teclas y las acciones correspondientes que se deben ejecutar. Sxhkd es altamente configurable y ligero, diseñado para ser rápido y eficiente en el manejo de eventos de entrada, lo que lo hace ideal para entornos donde los recursos del sistema son limitados o cuando se busca una experiencia de usuario altamente personalizable y controlada.

Ambos programas son muy populares en la comunidad de entusiastas de Linux que prefieren un entorno de escritorio altamente personalizable y orientado al uso de teclado.

En resumen, primeramente ejecutaremos el siguiente comando:

```
apt install build-essential git vim xcb libxcb-util0-dev libxcb-ewmh-dev libxcb-randr0-dev libxcb-icccm4-dev libxcb-keysyms1-dev libxcb-xinerama0-dev libasound2-dev libxcb-xtest0-dev libxcb-shape0-dev
```

Posteriormente, aplicaremos una actualización del sistema con el comando ‘**apt update**‘. Acto seguido, tenéis que dirigiros a la carpeta de descargas de vuestro equipo y descargar los proyectos ‘**bswpm**‘ y ‘**sxhkd**‘ con los siguientes comandos:

- git clone https://github.com/baskerville/bspwm.git
- git clone https://github.com/baskerville/sxhkd.git

Para instalar cada uno de estos, lo que debéis hacer es meteros en ambos directorios por separado y ejecutar los comandos ‘**make**‘ y ‘**sudo make install**‘.

- Como los archivos **bspwmrc** y **sxhkdrc** no existen los creamos en 
```
mkdir ~/.config/{bspwm,sxhkd}
```

- Luego copiamos los archivos **bspwmrc** y **sxhkdrc** 
  ---> cp bspwmrc ~/.config/bspwm
  ---> cp sxhkdrc ~/.config/sxhkd

- En la configuración **sxhkd** ya podemos ir modificando a nuestro gusto 
```
nano .config/sxhkd/sxhkdrc
```
Podemos ir modificando la parte de inicialización de la Kitty, ingrensando la ruta de la kitty en *#Terminal emulator*

Instalamos la terminal kitty donde vamos a estar operando y para ello debemos instalarlo

```
sudo apt install kitty
```
- Después de instalar debemos actualizarla a su ultima versión ya que por defecto se instala desactualizadamente
- Ingresamos al siguiente link para ver la última actualización de la kitty en **releases** [Actualizar kitty Aquí](https://github.com/kovidgoyal/kitty)


- Podemos empezar a configurar ciertas cosas como el **sxhkd** y el **bspwm** a nuestro gusto 
- Se cambia Windows + q , Windows + shift + (q,r) , Windows + Shift + x (ilocker)
- En **focus** cambiamos las letras por las flechas:
# focus the node in the given direction
super + {_,shift + }{Left,Down,Up,Right}
        bspc node -{f,s} {west,south,north,east}

- De igual manera con los pre selectores
# preselect the direction
super + ctrl + alt + {Left,Down,Up,Right}
        bspc node -p {west,south,north,east}

- Con la Pre cancelación 
# cancel the preselection for the focused node
super + ctrl + alt + space
        bspc node -p cancel


A continuación tenéis el enlace al archivo de configuración ‘**bspwm_resize**‘ que usamos al final de esta clase en caso de que hayan creado un script personalizado para el move/resize:

- [Archivo bspwm_resize](https://hack4u.io/wp-content/uploads/2022/09/bspwm_resize.txt)

