
----
- Tag : #KITTY #FEH
----
Por aquí tienes el archivo ‘**color.ini**‘ para la Kitty:

- [Archivo color.ini](https://hack4u.io/wp-content/uploads/2022/09/color.ini_.txt)

Por aquí tienes el archivo de configuración ‘**kitty.conf**‘ para la Kitty:

- [Archivo kitty.conf](https://hack4u.io/wp-content/uploads/2022/09/kitty.conf_.txt)

Os compartimos a continuación el fondo de pantalla que utilizamos en esta clase:

- [Fondo de pantalla](https://wallpapercave.com/download/4k-ultra-hd-neon-mask-boy-wallpapers-wp7885623)

A continuación, vamos a definir cada uno de los conceptos que tocamos en esta clase:

- **Kitty:** Kitty es un emulador de terminal moderno para sistemas operativos basados en Unix, como Linux y macOS. Es especialmente conocido por su eficiencia y capacidad para manejar gráficos modernos como imágenes y emojis directamente en la terminal. Kitty es altamente personalizable y ofrece funcionalidades avanzadas como pestañas, división de ventanas, y transparencia, entre otros. Utiliza la aceleración por GPU para renderizar los textos, lo que lo hace particularmente rápido.
- **Hack Nerd Fonts:** Es una versión modificada de la fuente mono-espaciada Hack, que ha sido ampliada con una gran cantidad de iconos y símbolos adicionales, conocidos como “glyphs”. Estos incluyen íconos de populares herramientas de desarrollo y sistemas, lo que hace a esta fuente muy útil para desarrolladores y usuarios de terminales, ya que permite visualizar íconos específicos de herramientas directamente en la interfaz de la terminal.
- **Feh:** Feh es un visor de imágenes ligero y rápido para Linux que también puede ser utilizado para configurar fondos de pantalla en sistemas de escritorio. Es muy eficiente y funciona bien en entornos de escritorio ligeros o configuraciones minimalistas, ya que no depende de grandes librerías gráficas. Feh puede ser utilizado en scripts y configuraciones para cambiar automáticamente fondos de pantalla o para mostrar imágenes en presentaciones de diapositivas.

Estas herramientas son bastante populares en la comunidad de usuarios avanzados de Linux, especialmente aquellos que prefieren entornos altamente personalizables y eficientes.

----
# Empezamos con la personalización de la kitty y sus atajos 
- Primero vamos a configurar ciertos atajos en la siguiente ruta
```
cd ~/.config/sxhkd
nano sxhkdrc
```

- Añadimos la siguiente linea para poder abrir **Firefox** con las teclas 
```
# Firefox
super + shift + f
        firefox
```

- Para poder copiar y pegar de **Windows a Vmware** tiene que agregar la siguiete linea en **bspwmrc**
```
vmware-user-suid-wrapper &
```
Hacemos un Windows + Shift + R y volvemo intentar abrir Firefox

- Ahora procedemos a actualizar la **kitty**, para ello entramos en los releases en el siguiente repositorio
- https://github.com/kovidgoyal/kitty
- Descargar `Linux amd64 binary bundle`
- Removemos la kitty que tenemos en `cd /opt` (Preferible hacerlo en un gnome terminal)
- La eliminamos con `apt remove kitty` 
- Movemos el releases que descargamos a la ruta actual de /opt `mv /home/sk8ware/Downloads/kitty-0.34.1-x86_64.txz . `
- Descomprimimos el archivo con `7z x kitty-0.34.1-x86_64.txz`
- Creamos una Carpeta `Kitty` y movemos el archivo .txz detro de la carpeta y la ejecutamos con `tar -xf kitty-0.34.1-x86_64.txz`
- Entramos en la carpeta `Bin` y agregamos la nueva ruta `/opt/kitty/bin/kitty` debajo de Super + Return usando la configuración `nano /home/sk8ware/.config/sxhkd/sxhkdrc` 
- Actualizamos con Windows + Espacio para actualizar la kitty y volvemos a recargar
- Ahora nos diriguimos a la nueva ruta `cd ~/.config/kitty` y nos damos cuenta que se encuentra vacía, ahora creamos el siguiente archivo llamado `nano kitty.conf` y agregamos lo siguiente [Archivo kitty.conf](https://hack4u.io/wp-content/uploads/2022/09/kitty.conf_.txt)
- Adicional tambien creamos un archivo `nano color.ini` para dar una mejor estética de colores en el entorno de trabajo [Archivo color.ini](https://hack4u.io/wp-content/uploads/2022/09/color.ini_.txt), Guardamos y volvemos a iniciar la kitty.
- Ahora cuando abrimos nos pedira una miniconfiguración donde debemos poner `0` y nos mostrará una terminal muy simple en donde debemos irla configurando y probando todo, por ejemplo verificamos si tenemos instalado `imagemagick` y`feh` para el tratado de fotos, lo podemos probar con `kitty +kitten icat imagen.jpg` para ver imagenes en consola y `feh --bg-fill Fondo.jpg` para definir el fondo de pantalla
- Pero para que se quede la imagen como fondo de pantalla predeterminada hay que agregar el comando en el archivo `bspwmrc` 
```
# WALLPAPER
feh --bg-fill ~/Wallpaper/nothin.jpg
```
- Para que funcione las mismas configuraciones de usuario no privilegiado y root hay que arrastrar la configuración al direcctorio de root `cd /root/.config/kitty` en un principio debería estar vacía para copiar la configuración. 
```
cp /home/sk8ware/.config/kitty* . 
```
- De forma que ahora deberíamos tener la configuración **kitty.cof** y **color.ini** en root
- Ahora si lanzamos la kitty desde root debería estar aplicado la configuración 
```
/opt/kitty/bin/kitty
```
- Y listo con esto ya estaríamos avanzando demasiado ;)











```
cd /usr/local/share/fonts
```
