
----
- Tag: #POLYBAR #PICOM #ROFI
------
En esta clase, instalamos Polybar, Picom y Rofi, paquetes esenciales para personalizar tu entorno Bspwm, mejorando la interfaz y la usabilidad.

- **Polybar**: Es una barra de tareas altamente personalizable para sistemas de ventanas X. Polybar se destaca por su flexibilidad y capacidad para mostrar información variada como la fecha, la utilización del CPU, la memoria, y mucho más. Puedes configurar completamente su apariencia y los módulos que muestra, lo que la hace muy popular entre los usuarios que desean un escritorio minimalista y funcional.
- **Picom**: Es un compositor para el sistema de ventanas X, lo que significa que maneja cómo se muestran las ventanas y los efectos visuales en el escritorio, como sombras, transparencias y animaciones suaves. Picom ayuda a mejorar la estética general del escritorio y reduce el desgarro de la pantalla durante la reproducción de video y el movimiento de ventanas.
- **Rofi**: Es un lanzador de aplicaciones ligero y personalizable, que también puede servir como conmutador de ventanas y más. Rofi permite a los usuarios buscar y lanzar aplicaciones rápidamente, cambiar entre ventanas activas, o incluso ejecutar comandos personalizados. Su interfaz es altamente configurable, lo que permite a los usuarios adaptarla a sus necesidades específicas y estética del escritorio.
----
# Podemos copiar los paquetes necesarios en :
- [Picom](https://github.com/yshui/picom)
- Copiamos los paquetes
```
sudo apt install libconfig-dev libdbus-1-dev libegl-dev libev-dev libgl-dev libepoxy-dev libpcre2-dev libpixman-1-dev libx11-xcb-dev libxcb1-dev libxcb-composite0-dev libxcb-damage0-dev libxcb-dpms0-dev libxcb-glx0-dev libxcb-image0-dev libxcb-present-dev libxcb-randr0-dev libxcb-render0-dev libxcb-render-util0-dev libxcb-shape0-dev libxcb-util-dev libxcb-xfixes0-dev libxext-dev meson ninja-build uthash-dev -y
```

- Hacer un ``sudo apt update`` 
- Nos instalamos el repositorio en /Descargas `git clone https://github.com/yshui/picom)` 
- Dentro la carpeta de **picom** realizamos la instalación 
```
meson setup --buildtype=release build
ninja -C build
```

### To install
```
ninja -C build install
```

# Rofi

- Instalamos rofi
```
sudo apt install rofi
```

- Ahora debemos colocarlo con la función Windows + D
```
nano ~/.config/sxhkd/sxhkdrc
```
# program launcher
super + d
        rofi -show run

# Ahora salimos al login para escoger bspwm
- Una vez dentro veremos todo negro ya que aún no hemos instalado la polybar, fondo de pantalla etc
- Probamos que todas las funciones esta correctamente configuradas
