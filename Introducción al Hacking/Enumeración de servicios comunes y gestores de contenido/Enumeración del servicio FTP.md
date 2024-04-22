
----
- TAG: #ENUMERACIÓN #FTP
---
En esta clase, hablaremos sobre el protocolo de transferencia de archivos (**FTP**) y cómo aplicar reconocimiento sobre este para recopilar información.

FTP es un protocolo ampliamente utilizado para la **transferencia de archivos** en redes. La enumeración del servicio FTP implica recopilar información relevante, como la versión del servidor FTP, la configuración de permisos de archivos, los usuarios y las contraseñas (mediante ataques de fuerza bruta o guessing), entre otros.

A continuación, se os proporciona el enlace al primer proyecto que tocamos en esta clase:

- **Docker-FTP-Server**: [https://github.com/garethflowers/docker-ftp-server](https://github.com/garethflowers/docker-ftp-server)

Una de las herramientas que usamos en esta clase para el primer proyecto que nos descargamos es ‘**Hydra**‘. Hydra es una herramienta de pruebas de penetración de código abierto que se utiliza para realizar ataques de fuerza bruta contra sistemas y servicios protegidos por contraseña. La herramienta es altamente personalizable y admite una amplia gama de protocolos de red, como HTTP, FTP, SSH, Telnet, SMTP, entre otros.

El siguiente de los proyectos que utilizamos para desplegar el contenedor que permite la autenticación de usuarios invitados para FTP, es el proyecto ‘**docker-anon-ftp**‘ de ‘**metabrainz**‘. A continuación, se os proporciona el enlace al proyecto:

- **Docker-ANON-FTP**: [https://github.com/metabrainz/docker-anon-ftp](https://github.com/metabrainz/docker-anon-ftp)

Comandos utilizados para encontrar la contraseña:

```
docker run \\
	--detach \\
	--env FTP_PASS=123 \\
	--env FTP_USER=user \\
	--name my-ftp-server \\
	--publish 20-21:20-21/tcp \\
	--publish 40000-40009:40000-40009/tcp \\
	--volume /data:/home/user \\
	garethflowers/ftp-server
```

`ftp [localhost](<http://localhost>)` —————————————> para conectarse al contenedor de arriba

`ftp 127.0.0.1` también se puede usar

`nmap -sCV -p21 127.0.0.1` ———————> envia un script de reconocimiento al puerto 21

`cat /usr/share/wordlists/rockyou.txt | head -n 200 > passwords.txt` ———————————> Enviar las primeras 200 lineas como output al nuevo archivo `passwords.txt`

`hydra -l sk8ware -P passwords.txt [<ftp://127.0.0.1>](<ftp://127.0.0.1>) -t 15` ———————————> Para realizar el ataque por fuerza bruta con el archivo txt

`docker rm $(docker ps -a -q) - -force`

`docker rmi $(docker images -q)`

Comandos utilizados para encontrar el usuario:

`docker run -d -p 20-21:20-21 -p 65500-65515:65500-65515 -v /tmp:/var/ftp:ro metabrainz/docker-anon-ftp`

`nmap -sCV -p21 127.0.0.1`

`ftp 127.0.0.1`

usuario : anonymous

contraseña: Enter