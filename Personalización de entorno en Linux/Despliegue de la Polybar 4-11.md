
----
- Tag: #POLYBAR #DESPLIEGUE 
-----
**Polybar** es una herramienta muy utilizada en la personalización de entornos de escritorio en sistemas Linux, especialmente en aquellos que emplean gestores de ventanas livianos o “tiling window managers” como **i3**, **bspwm**, y otros. Es una barra de estado que se destaca por ser altamente configurable y modular.

Polybar permite a los usuarios crear barras de estado que se adaptan precisamente a sus necesidades y estética del escritorio. Puedes configurar elementos como módulos de reloj, indicadores de batería, controles de volumen, monitores de sistema (como CPU, memoria, etc.), espacios de trabajo y muchos otros. Cada módulo en la barra puede ser personalizado en términos de funcionalidad y apariencia.

La configuración de Polybar se realiza a través de archivos de texto plano, lo que proporciona una gran flexibilidad. Los usuarios pueden escribir sus propios módulos usando scripts en diferentes lenguajes de programación o adaptar módulos existentes para personalizar su experiencia. Además, Polybar es capaz de lanzar y mostrar notificaciones o resultados de comandos específicos, lo que lo hace una herramienta extremadamente potente para aquellos que desean tener un control total sobre la información que se muestra en su entorno de escritorio.

En la siguiente clase, trabajaremos en las esquinas, el sombreado y los difuminados.

-----
- Nos dirigimos a nuestra carpeta donde tengamos picom (Descargas), y copiamos el siguiente repositorio
```
git clone https://github.com/VaughnValle/blue-sky
```

- Entramos a la carpeta **blue-sky** y luego a **/polybar** 
- Copiamos el contenido de la carpeta *polybar* de forma recursiva `cp -r * ~/.config/polybar`
- Ahora podemos ejecutar `echo '~/.config/polybar/./launch.sh &' >> ~/.config/bspwm/bspwmrc` pero antes de eso debemos guardarlo en nuestro archivo **bspwmrc**
- Ahora nos logueamos como usuario root y copiamos el archivo de configuración `cp fonts/* /usr/share/fonts/truetype/` 
- Ahora vamos actualizar y sincronizar la cache de fuentes con `fc-cache -v` y damos enter.
- Hacemos Windows + Shift + R para recargar y que nos aparezca la polybar
- 