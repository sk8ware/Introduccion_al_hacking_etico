
---
- TAG: #CONFIGURANDO #ZSH #POWERLEVEL10K 
----
Les compartimos por aquí el código correspondiente al sistema de autocompletado moderno que vemos en el minuto 27:33, el cual podéis introducir en vuestro archivo ‘**.zshrc**‘:

- [https://pastebin.com/H87J3nMj](https://pastebin.com/H87J3nMj)

**ZSH (Z Shell)**

ZSH, o Z Shell, es un intérprete de comandos para sistemas Unix, que se utiliza como una alternativa avanzada al tradicional shell Bash. Ofrece muchas mejoras en términos de características, plugins, y temas, lo que lo hace muy popular entre los usuarios avanzados y desarrolladores.

Algunas de las características más notables de ZSH incluyen:

- **Autocompletado**: ZSH proporciona un sistema de autocompletado potente y versátil que puede predecir comandos basados en el contexto, incluyendo opciones y parámetros.
- **Corrección de errores**: Ofrece sugerencias de corrección cuando se escribe un comando erróneamente.
- **Gestión de scripts**: ZSH es compatible con todos los scripts de Bourne Shell y Bash, y añade sus propias mejoras en la programación de scripts.
- **Personalización**: Se puede personalizar profundamente mediante temas y configuraciones que pueden cambiar su apariencia y comportamiento.

**Powerlevel10k**

Powerlevel10k es un tema para ZSH diseñado para ser visualmente atractivo y altamente informativo. Está diseñado para ser una versión más rápida y personalizable del popular tema Powerlevel9k.

Algunas de las características que lo hacen destacar incluyen:

- **Velocidad**: Es significativamente más rápido que otros temas para ZSH, lo que reduce el tiempo de inicio del terminal y la latencia al escribir comandos.
- **Personalizable**: Viene con un asistente de configuración que guía a los usuarios a través del proceso de configuración, permitiendo personalizar el prompt dependiendo de las preferencias del usuario.
- **Información contextual**: Muestra información útil en el prompt según el contexto, como el estado del repositorio git, el usuario actual, el tiempo de ejecución de comandos, y mucho más.
- **Iconos y fuentes**: Utiliza fuentes de Nerd Fonts para mostrar iconos y otros elementos gráficos que hacen que la información sea fácil de leer y visualmente atractiva.

Juntos, ZSH y Powerlevel10k ofrecen una experiencia de terminal rica y eficiente, mejorando tanto la funcionalidad como la apariencia del entorno de línea de comandos. Estas herramientas son particularmente populares entre los desarrolladores y los entusiastas de la personalización de sistemas Unix/Linux.

----
- Primero nos loguemos como usuarios root, a continuación instalamos los siguientes paquetes
```
apt install zsh-autocomplete zsh-autosuggestions zsh-syntax-highlighting
```

- Si relizamos la siguiente linea nos mostrará los plugins que hemos descargado
```
ls -l /usr/share | grep zsh
```
Los plugins que se muestran son los que debemos agregar como source para que nos aplique el plugin y lo podamos utilizar.

- Para que **root** también trabaje con una *zsh* debemos realizar el siguiente comando
```
usermod --shell /usr/bin/zsh root 
```
- De igual manera para para el usuario *sk8ware*
```
usermod --shell /usr/bin/zsh sk8ware
```
- Con `cat /etc/passwd | grep -E "^sk8ware|^root"` podemos ver que tanto el usuario *root* como *sk8ware* manejan un terminal con una *zsh*. 
----
Ahora como el usuario *sk8ware* nos clonamos la siguiente linea de la *POWERLEVEL10K*

```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

- En  la configuración `nano /.zshrc` configuramos la ruta a: `source /home/sk8ware/powerlevel10k/powerlevel10k.zsh-theme` ya que la ruta absoluta de root que indica no existe

Ahora solo escribimos **zsh** en la terminal como usuario no privilegiado para empezar con la instalación de la **powerlevel10k**

- Una vez tengamos desplegado nuestra *powerlevel10k* quitamos el visto que nos sale mano derecha, para ello debemos editar la configuración en `nano .p10k.zsh` y comentamos todos los *plugins* con *#* para que no aparezca ningún icono en la parte derecha y evitar que se relentice la terminal, guardamos y listo.

- Si desea se puede agregar como extras en la parte de la izquierda los siguientes comando para verlos en la powerlevel10k

```
context
command_execution_time
status
```
---
Ahora para vamos a configurar la *POWERLEVEL10K*  para el usuario *ROOT*

- Realizamos el mismo proceso para el usuario *root* , nos copiamos el repositorio de la *powerlevel10k*
```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

 - Aplastamos nuevamente `zsh` en la terminal para configurar la *powerlevel10k*
 - Nos vamos al directorio  `cd /root` y configuramos el `nano .p10k.zsh`
 - Nuevamente comentamos todos los plugins con `#` y agregamos los siguientes plugins en la parte izquierda:
```
context
command_execution_time
status
```

 - Si queremos modificar la parte donde nos indica el nombre del usuario **root** lo podemos cambiar por un símbolo a nuestra preferencia, en `nano .p10k.zsh`
 - Nos copiamos el símbolo que hayamos escogido y lo pegamos en la parte de *root_template*
 - En la parte de *DIR_ANCHOR* se puede poner en *false* para eliminar la negrilla en las letras que indican el usuario a la izquierda.

- Ahora vamos a tocar un poco la *zsh* para poder centralizar todo en un archivo, tanto para root como para sk8ware, para que la configuración de la *zsh* se ejecute en ambas con :
```
cd /root
ln -s -f /home/sk8ware/.zshrc .zshrc
```

- para verificarlo podemos hacer un `ls -la` y veremos que ahora se conectan a través de un link mutuo
- Ingresamos a la carpeta de *zsh-autocomplete* y realizamos el siguiente comando :
```
chown root:root /usr/share/zsh/site-functions/_bspc
source  /usr/share/zsh-autosuggestions/zsh-autosuggestions.zsh
```

- Para no hacer siempre esta instrucción lo ingresmos en nuestra consifiguración *.zshrc* como sk8ware
```
# Plugins
source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
#source /usr/share/zsh-autocomplete/zsh-autocomplete.plugin.zsh
source /usr/share/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/share/zsh-sudo/sudo.plugin.zsh
```

O así : 

```
# ZSH Autosuggestions Plugin 
if  [ -f /usr/share/zsh-autosuggestions/zsh-autosuggestions.zsh ]; then
     source /usr/share/zsh-autosuggestions/zsh-autosuggestions.zsh
fi 

# ZSH Syntax Highlighting
if [ -f /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh ]; then
	source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
fi
```  

- Ahora podemos agregar la **funcion esc + esc** desde el siguente link de hit hub:
  https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/sudo/sudo.plugin.zsh
  Nos decargamos el raw desde nuestra terminal con: 
  Nos logueamos como *root* y luego entramos a la carpeta `cd /usr/share` y creamos la carpeta `mkdir zsh.sudo`, dentro de la nueva carpeta descargamos el *raw*
```
wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/plugins/sudo/sudo.plugin.zsh
```
- Agreamos el nuevo plugin en *nano .zshrc*
```
# ZSH Sudo Plugin
if [ -f /usr/share/zsh-sudo/sudo.plugin.zsh ]; then
	source /usr/share/zsh-sudo/sudo.plugin.zsh
fi
```

----
### Ahora vamos a configurar un poco el *History*
- En el mismo archivo `.zsh` agregamos la siguiente linea
```
# History
HISTFILE=~/.zsh_history
HISTSIZE=1000
SAVEHIST=1000
setopt histignorealldups sharehistory
```

- Para eliminar el historial del historico hay que realizar 
```
echo '' > ~/.zsh_history
``` 

- Para completar palabras incompletas como *whomi* a *whoami* con `TAB` 
- [En este pastebin](https://pastebin.com/H87J3nMj) encontraremos la configuración para agregar a nuestra `.zsh` 