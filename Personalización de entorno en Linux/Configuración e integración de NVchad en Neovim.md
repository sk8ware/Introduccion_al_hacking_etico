
----
- TAG: #INSTALACIÓN #INTEGRACIÓN #NVCHAD #NEOVIM #NVIM 
-----
**Neovim**

Neovim es un editor de texto extensible basado en Vim, diseñado para mejorar la eficiencia en la edición de código y la experiencia del usuario. Se desarrolló como una bifurcación de Vim con el objetivo de modernizar el código base, introducir mejoras en la arquitectura y facilitar la contribución de la comunidad. Neovim añade características como una API mejorada para plugins y soporte integrado para ejecutar procesos de fondo asíncronos, lo que permite una experiencia más fluida y rica en características sin bloquear la interfaz del usuario mientras se ejecutan tareas complejas.

**NVChad**

NVChad es un framework de configuración para Neovim que ofrece una experiencia de usuario mejorada y una suite de características prediseñadas. Es conocido por su interfaz de usuario estéticamente agradable y por su enfoque en la simplicidad y la eficiencia. NVChad viene preconfigurado con una serie de plugins cuidadosamente seleccionados y configuraciones optimizadas que abordan tanto la funcionalidad como la visualización. Esto incluye soporte para temas de color, gestión de buffers mejorada, autocompletado inteligente, y mucho más, todo ello manteniendo un rendimiento rápido. NVChad está diseñado para ser fácil de instalar y configurar, ofreciendo a los usuarios una plataforma robusta sobre la cual pueden construir o adaptar según sus necesidades específicas.

Ambas herramientas están diseñadas para complementarse entre sí, donde Neovim proporciona el entorno base y NVChad aprovecha y amplía sus capacidades, facilitando una experiencia de usuario altamente personalizada y eficiente para programadores y editores de texto.

-----
# DESCARGANDO *NVCHAD* 
Primero empezamos verificando si no tenemos instaldo aun *neovim* en nuestro sistema
Luego seguimos los pasos de descarga del siguiente repositorio de *git hub* 
[Instalación Aquí](https://nvchad.com/docs/quickstart/install/)
Borramos la parte final del primer paso de la instalación el apartado de `&& nvim` 
Instalamos el *releases* de *nvim* del siguiente repositorio 
[NVIM RELEASES descargar nvim-linux64.tar.gz](https://github.com/neovim/neovim/releases/tag/v0.9.5)
Nos ingresamos a nuesta carpeta */opt* y creamos un carpeta que se llame *nvim* como usuario root, luego ingresamos
Luego movemos el archivo *.tar* ah la carpeta recien creada con `mv /home/sk8ware/Download/nvim-linux64.tar.gz . `
Lo descomprimimos con `tar -xf nvim-linux64.tar.gz` 
Nos dirigimos  a la carpeta e ingresamos a *bin* y encontraremos el archivo *nvim* 
Ahora copiamos la ruta ` /opt/nvim/nvim-linux64/bin ` y la pegamos al final del `PATH=` 
Guardamos y ahora abrimos una nueva ventana y abrimos *nvim*
De manera automática se instalara y nos mostrara la configuración, así que salimos haciendo ` Ctrl + :q! ` 
Revisamos en caso de que se encuentre con el signo `$` lo  puede borrar con la siguiente instrucción, 
Nos dirigimos a la configuración de *nvim* con  `cd ~/.config/nvim` y dentro de `init.lua` ponemos lo siguiente al inicio:
```
vim.opt.listchars = "tab:»·,trail:·"
```
Guardamos y salimos, volvemos revisar si ya no se encuentra el signo `$` 
Pero al momento parece estar actualizada, porque desde la instalación no apareció con ese problema, en caso que se presente ese error pues ya saben como solucionarlo :)
Ahora haremos *locate* pero en caso que no este instalado pueden hacer lo siguiente 
Hacemos un ` sudo apt install locate` , una vez instalado hacemos un `updatedb` y veremos que nos salen dos permisos denegados en las monturas indicadas, que tranquilamente se pueden desmontar 
Debemos logearnos como *root* y hacemos un ` umount ` con las rutas que nos indican tipo:
```
umount /run/user/1000/doc
```
Y de igual manera con la otra ruta, volvemos hacer un `updatedb` y ya no nos aparecera los errores 
Ahora podemos buscar archivos *.py* o los que desee, podemos visualizarlos con *nvim /usr/share/system-config-printer/debug.py* y ver perfectamente la sintaxis, pero cuando nos abrimos archivos *.lua* nos refleja un pequeño error en letras rojas en la parte inferior.
Lo que podemos hacer es hacer *esc + :* y escribir `MasonInstallAll` ponemos enter y se instalará lo necesario
Salimos con `esc` y `:q!`, volvemos abrir el mismo archivo y ya no aparecerá mas el error 