
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

```
cd /usr/local/share/fonts
```
