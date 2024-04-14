
---
# Resolución de la maquina **BUILDER**
---

- Empezamos creando nuestras carpetas que contengan nuestros registros de nmap, scripts, exploits, content.
```
mkt
```

- Ingresamos a nuestra carpeta de nmap y realizamos un ping y escaneo a la red.
```
ping -c 10.10.11.10
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