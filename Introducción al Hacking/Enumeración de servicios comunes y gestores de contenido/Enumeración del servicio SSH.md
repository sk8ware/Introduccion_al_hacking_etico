
----
- TAG: #ENUMERACIÓN #SSH 
----
En esta clase, exploraremos el protocolo **SSH** (**Secure Shell**) y cómo realizar reconocimiento para recopilar información sobre los sistemas que ejecutan este servicio.

SSH es un protocolo de administración remota que permite a los usuarios **controlar** y **modificar** sus servidores remotos a través de Internet mediante un mecanismo de **autenticación seguro**. Como una alternativa más segura al protocolo **Telnet**, que transmite información sin cifrar, SSH utiliza **técnicas criptográficas** para garantizar que todas las comunicaciones hacia y desde el servidor remoto estén cifradas.

SSH proporciona un mecanismo para autenticar un usuario remoto, transferir entradas desde el cliente al host y retransmitir la salida de vuelta al cliente. Esto es especialmente útil para administrar sistemas remotos de manera segura y eficiente, sin tener que estar físicamente presentes en el sitio.

A continuación, se os proporciona el enlace directo a la web donde copiamos todo el comando de ‘docker’ para desplegar nuestro contenedor:

- **Docker Hub OpenSSH-Server**: [https://hub.docker.com/r/linuxserver/openssh-server](https://hub.docker.com/r/linuxserver/openssh-server)

Cabe destacar que a través de la versión de SSH, también podemos identificar el codename de la distribución que se está ejecutando en el sistema.

Por ejemplo, si la versión del servidor SSH es “**OpenSSH 8.2p1 Ubuntu 4ubuntu0.5**“, podemos determinar que el sistema está ejecutando una distribución de Ubuntu. El número de versión “**4ubuntu0.5**” se refiere a la revisión específica del paquete de SSH en esa distribución de Ubuntu. A partir de esto, podemos identificar el **codename** de la distribución de Ubuntu, que en este caso sería “**Focal**” para Ubuntu 20.04.

Todas estas búsquedas las aplicamos sobre el siguiente dominio:

- **Launchpad**: [https://launchpad.net/ubuntu](https://launchpad.net/ubuntu)

Comandos vistos en esta clase:

docker run -d \ --name=openssh-server \ --hostname=sk8ware \ -e PUID=1000 \ -e PGID=1000 \ -e TZ=Etc/UTC \ -e PASSWORD_ACCESS=true \ -e USER_PASSWORD=louise \ -e USER_NAME=sk8ware \ -p 2222:2222 \ -v /path/to/appdata/config:/config \ --restart unless-stopped \ [lscr.io/linuxserver/openssh-server:latest](http://lscr.io/linuxserver/openssh-server:latest)

`docker ps`

`ssh sk8ware@127.0.0.1 -p 2222`

`hydra -l sk8ware -P /usr/share/wordlists/rockyou.txt ssh://127.0.0.1 -s 2222 -t 15`