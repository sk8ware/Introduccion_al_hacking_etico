
----
- Tag: #POLYBAR #PICOM #ROFI
------
En esta clase, instalamos Polybar, Picom y Rofi, paquetes esenciales para personalizar tu entorno Bspwm, mejorando la interfaz y la usabilidad.

- **Polybar**: Es una barra de tareas altamente personalizable para sistemas de ventanas X. Polybar se destaca por su flexibilidad y capacidad para mostrar información variada como la fecha, la utilización del CPU, la memoria, y mucho más. Puedes configurar completamente su apariencia y los módulos que muestra, lo que la hace muy popular entre los usuarios que desean un escritorio minimalista y funcional.
- **Picom**: Es un compositor para el sistema de ventanas X, lo que significa que maneja cómo se muestran las ventanas y los efectos visuales en el escritorio, como sombras, transparencias y animaciones suaves. Picom ayuda a mejorar la estética general del escritorio y reduce el desgarro de la pantalla durante la reproducción de video y el movimiento de ventanas.
- **Rofi**: Es un lanzador de aplicaciones ligero y personalizable, que también puede servir como conmutador de ventanas y más. Rofi permite a los usuarios buscar y lanzar aplicaciones rápidamente, cambiar entre ventanas activas, o incluso ejecutar comandos personalizados. Su interfaz es altamente configurable, lo que permite a los usuarios adaptarla a sus necesidades específicas y estética del escritorio.

-----
# Intalación de la polybar

En nuestra terminal utilizamos el siguiente comando como usuarios root

```bash
apt install polybar
```

# Instalación de Picom

En esta instalación si necesitamos usar **Git Hub**, para poder confirar el difuminado, el sombreado, etc

En la siguiente **URL** pueden seguir los pasos de instalación segun su distribución.

Para debian:
```bash
apt install libconfig-dev libdbus-1-dev libegl-dev libev-dev libgl-dev libepoxy-dev libpcre2-dev libpixman-1-dev libx11-xcb-dev libxcb1-dev libxcb-composite0-dev libxcb-damage0-dev libxcb-glx0-dev libxcb-image0-dev libxcb-present-dev libxcb-randr0-dev libxcb-render0-dev libxcb-render-util0-dev libxcb-shape0-dev libxcb-util-dev libxcb-xfixes0-dev meson ninja-build uthash-dev -y
```

Ahora tenemos que salir y estar como usuario no privilegiado y vamos al directorio descargas:

Nos clonomanos el siguiente repositorio :

```bash
git clone https://github.com/yshui/picom.git
```

Y dentro de picom realizamos el build:

```bash
meson setup --buildtype=release build
ninja -C build
```

Si tienen problema con la instalacion de ninja intenten lo siguiente:
```bash
# Instalar Meson si es necesario
sudo apt install meson

# Configurar el proyecto
meson setup build

# Construir el proyecto
ninja -C build
```

Ahora el paso final para la instalación:

```bash
ninja -C build install
```

Y listo ;)  Con esto ya quedaria instalado definitivamente el picom

# Instalación de Rofi

Esto nos permitira desplegar las aplicaciones de una manera más estetica

```bash
sudo apt install rofi 
```

Para visualizar el rofi lo podemos hacer de esta manera 

```bash
rofi -show run
```

Para configurarlo a nuestro gusto para que se abra con `Windows + D`, para ello lo agregamos en la siguiente ruta: 

```bash
cd ~/.config/sxhkd/
```

Dentro de archivo 
```bash
nano sxhkdrc
```

Ingresamos la siguiente configuración:

```bash
# program launcher
super + d        
        /usr/bin/rofi -show run
```

Nos volvemos a logear de la siguiente manera:

```bash
kill -9 -1
```

Vamos a las dos barritas y seleccionamos la opción de **Bspwm** y nos logeamos con el mismo usuario y contraseña

Una vez dentro no se asusten si piensan que se quedo cargando o no aparece nada, es normal

Ahora pueden probar los atajos creados para ver si funcionan, como `Windows + Enter` etc

