
----
- TAG: #INSTALACIÓN #BATCAT #CAT #BAT #LSD
-----
# **Batcat**

Batcat es la versión distribuida en Debian y Ubuntu del programa **bat**, una herramienta de línea de comandos que sirve como una versión mejorada del clásico comando **cat** de Unix. Batcat ofrece resaltado de sintaxis para una gran variedad de lenguajes de programación y formatos de archivo, facilitando la lectura y comprensión del código directamente en la terminal. Además, integra funcionalidades como la integración con git para mostrar diferencias en el código, numeración de líneas, y la capacidad de previsualizar el contenido de archivos en formato paginado.

Esta herramienta es especialmente útil para desarrolladores y personas que trabajan frecuentemente con código fuente o scripts, ya que mejora significativamente la legibilidad y la eficiencia al explorar o revisar archivos en la terminal.

# **Lsd**

Lsd (abreviatura de LSDeluxe) es un reemplazo moderno para el tradicional comando **ls** de Unix, diseñado para mejorar la visualización de los archivos en la terminal. Lsd ofrece un resaltado de colores basado en el tipo de archivo y permisos, además de utilizar iconos para cada tipo de archivo, lo que hace que la navegación y comprensión de la estructura de directorios sea mucho más intuitiva y visualmente agradable. Al igual que bat, lsd soporta fuentes de Nerd Fonts para mostrar iconos, y puede ser completamente personalizado mediante un archivo de configuración para adaptarse a las preferencias del usuario.

Lsd también soporta características como el árbol de directorios directamente en la lista de archivos, lo cual es útil para obtener una visión rápida de la jerarquía de directorios sin necesidad de comandos adicionales. Su funcionalidad y estética mejorada lo hacen popular entre los usuarios que desean una experiencia más rica y eficiente en la línea de comandos.

-----
## Empezamos descargando #BATCAT Y #LSD 
- [Repositorio de batcat](https://github.com/sharkdp/bat)
- [Repositorio de LSD](https://github.com/lsd-rs/lsd)
----
- Empezamos descargando los archivos, pero antes de ello debemos loguearnos como *root*
```
dpkg -i bat_0.24.0_amd64.deb
dpkg -i lsd_1.1.2_amd64.deb
```
Con esto ya tendríamos instalado bat como lsd, pero ahora vamos a configurar para que nuestro *bat* se convierta en *cat* y el *lsd* en nuestro *ls*, pero antes de ello vamos a configurar que el *lsd* no se vea como negrilla las leras

- Hacemos un `echo $LS_COLORS` y veremos el valor de esa variable, con lo cual trataremos de quitarle el puno y coma en todos los números, Para ello debemo agregarle `| sed 's/=01;/=/g'` Para que nos la quite en toda la respuesta.
```
echo $LS_COLORS | sed 's/=01;/=/g'
```
- Ahora si hacemos el siguiente comando exportaremos el nuevo valor a la variable 
```
export  $LS_COLORS="nueva variable"
```
- Debemos contemplar este nuevo resulado en nuestoarchivo `nano .zshrc` lo podemos colocar al final de todo.
- Hacemos un `echo $PATH` como *sk8ware* y copiamos la ruta para agregarle debajo del *export $LS_COLORS*
```
export PATH="ruta absoluta"
```
-----
### Ahora configuraremos un poco la zsh para cambiar el bat por el cat
- Podemos ponerlo de 2 maneras la configuración 
```
# Custom Aliases

alias ll='lsd -lh --group-dirs=first'
alias la='lsd -a --group-dirs=first'
alias l='lsd --group-dirs=first'
alias lla='lsd -lha --group-dirs=first'
alias ls='lsd --group-dirs=first'
alias cat='/bin/batcat --paging=never'
alias catn='cat'
alias catnp='batcat'

[ -f ~/.fzf.zsh ] && source ~/.fzf.zsh
```
o este suele ser mas completo y actualizado 
```
# Custom Aliases

# -----------------------------------------------

# bat

alias cat='bat'

alias catn='bat --style=plain'

alias catnp='bat --style=plain --paging=never'

# ls

alias ll='lsd -lh --group-dirs=first'

alias la='lsd -a --group-dirs=first'

alias l='lsd --group-dirs=first'

alias lla='lsd -lha --group-dirs=first'

alias ls='lsd --group-dirs=first'
```
----
# Solución a error cuando se trata de abrir burpsuite 
- Si tratamos de abrir *burpsuite* por lo general suele salir un mensaje de error, para ello hay un recurso en donde nos explican paso a paso como solucionarlo:
[Procedimiento para arreglar el inconveniente con Burpsuite](https://medium.com/@neat_mahogany_porcupine_191/burpsuite-no-longer-launches-after-parrot-upgrade-d1c6b17cb70d)

- También suele reflejar otro error al momeno de abrir *burpsuite* y es que la proporción de la imagen suele estar reducida.
1. Como usuario no privilegiado nos abrimos nuestro archivo `.zshrc` y agregamos la siguiente línea 
```
# Fix The Java Problem 
export _JAVA_AWT_WM_NONREPARENTING=1  
```
2. Nos abrimos nuestro archivo `nano /home/sk8ware/.config/bspwm/bspwmrc` y al abajo de todo le colocamos la siguiente instrucción
```
wmname LG3D & 
```
  3. Volvernos a loguear con *Windows + Shift + Q* y veremos que nos funciona normal el burpsuite pero cuando lo abrimos desde el rofi va a presentar el mismo problema, para ello debemos irnos a la ruta `cd /usr/bin` hacemos un `echo $PATH`, nos logueamos como *root* y creamos un archivo `touch burpsuite-launcher` 
  4. Otorgamos permisos de ejecución con `chmod burpsuite-launcher` y abrimos el archivo con `nano` 
  ```
  #!/bin/bash
  export _JAVA_AWT_WM_NONREPARENTING=1
  wmname LG3D &
  /usr/bin/burpsuite
  ```
  5. Guardamos y ahora lo volvemos abrir desde el *rofi*