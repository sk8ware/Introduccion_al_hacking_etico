
----
- TAG: #ACTUALIZACIÓN #UPGRADE #UPGRADEO #SISTEMA 
-----
En caso de usar Arch Linux, para efectuar una actualización de todos los paquetes instalados, deberás ejecutar el siguiente comando:

- **sudo pacman -Syu**
----

Cuando queramos actualizar nuestro sistema, tenemos que realizar la función 
```
sudo apt update
```
En caso de que estemos como **root** solo 
```
apt update
```

Si sale que tenemos paquetes que tiene que ser actualizados realizamos la siguiente función 
```
sudo apt upgrade
```
Si estas en parrot mucho cuidado en realizar esta función ya que dañaria todo el sistema, para sistemas `parrot os` se realiza 
```
parrot-upgrade
```

Si al volver a realizar un `update` nos sale aun paquetes por actualizar simplemente realizamos un **reboot**
```
reboot
```
 