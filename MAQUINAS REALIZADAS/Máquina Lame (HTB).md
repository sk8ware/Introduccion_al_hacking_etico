
---
- TAG: #eJPT
----
![[Pasted image 20240618223305.png]]
# Hack The Box: Lame Writeup

## Introducción

En este writeup, documentaré el proceso completo para comprometer la máquina [Lame] en Hack The Box. La máquina está clasificada como [fácil] y fue lanzada el [14/03/2017] siendo una de las primeras maquinas de **HACK The Box**. Este writeup está destinado a fines educativos y pretende mostrar una metodología paso a paso para abordar y resolver máquinas en Hack The Box de manera efectiva.

## Preparativos

### Configuración del Entorno

Para comenzar, asegúrate de tener el entorno adecuado configurado. En este caso, usaré Kali Linux, una distribución de Linux diseñada para pruebas de penetración. Aquí están los pasos iniciales:

1. **Conexión a Hack The Box VPN**: Primero, debemos conectarnos a la red VPN de Hack The Box para acceder a la máquina objetivo. Descargamos el archivo de configuración de la VPN desde el sitio web de Hack The Box y lo ejecutamos con `openvpn`.
    
```sh
sudo openvpn htb.ovpn
````
    
2. **Reconocimiento Inicial**: Una vez conectados a la VPN, verificamos que tenemos conectividad con la máquina objetivo. Para este ejemplo, supongamos que la dirección IP de la máquina es `10.10.16.4`.
    
````zsh
ping -c 1 10.10.16.4
````


### Enumeración

#### Escaneo de Puertos

Comenzamos con un escaneo de puertos utilizando `nmap` para identificar los servicios que están ejecutándose en la máquina objetivo.

```sh
nmap -p- --open -sS --min-rate 500 -vvv -n -Pn 10.10.10.3 -oG allPorts
```

- **`nmap`**:
    
    - Es el comando principal para ejecutar `nmap`, una herramienta de código abierto utilizada para la exploración de red y auditorías de seguridad.
- **`-p-`**:
    
    - Escanea todos los 65535 puertos TCP. Por defecto, `nmap` escanea solo los 1000 puertos más comunes, pero esta opción asegura que todos los puertos sean escaneados.
- **`--open`**:
    
    - Muestra solo los puertos que están abiertos. Esto puede ayudar a filtrar el ruido de los puertos cerrados y filtrados, enfocándose solo en aquellos que están activos y escuchando.
- **`-sS`**:
    
    - Realiza un escaneo SYN, también conocido como "half-open" scan. Es más rápido y discreto que un escaneo TCP completo, ya que no establece una conexión completa (TCP handshake) con el puerto.
- **`--min-rate 500`**:
    
    - Establece una tasa mínima de paquetes por segundo que `nmap` debe enviar. En este caso, `500` paquetes por segundo. Esto acelera el escaneo, pero puede ser detectado por sistemas de detección de intrusos (IDS) o firewalls.
- **`-vvv`**:
    
    - Incrementa el nivel de verbosidad. `nmap` proporcionará mucha más información sobre el progreso del escaneo y los resultados, útil para diagnóstico y comprensión detallada.
- **`-n`**:
    
    - No resuelve nombres de dominio. Esto puede acelerar el escaneo al evitar la resolución DNS para cada dirección IP encontrada.
- **`-Pn`**:
    
    - Omite el host discovery. `nmap` normalmente envía pings para determinar si un host está activo antes de escanear los puertos. Esta opción asume que el host está activo y procede directamente al escaneo de puertos. Útil si el host no responde a pings ICMP pero tiene puertos abiertos.
- **`10.10.10.3`**:
    
    - Es la dirección IP del objetivo que se va a escanear.
- **`-oG allPorts`**:
    
    - Guarda los resultados en un archivo en formato "grepable" (`allPorts`). Este formato es fácil de analizar con herramientas de procesamiento de texto como `grep` o `awk`.

El resultado del escaneo debería darnos una lista de puertos abiertos y los servicios asociados.


### Ejemplo del Resultado Esperado

El comando anterior escaneará todos los puertos del host `10.10.10.3`, mostrando solo los puertos abiertos y ejecutando el escaneo de manera rápida y detallada. El resultado será guardado en un archivo llamado `allPorts` en un formato que es fácil de procesar posteriormente.

### Uso Típico

Este tipo de comando se usa comúnmente en escenarios donde se necesita una enumeración completa de puertos en un objetivo específico, especialmente en pruebas de penetración y auditorías de seguridad. La combinación de un escaneo rápido, detallado y enfocado solo en puertos abiertos proporciona una visión clara y eficiente del estado de los puertos del objetivo.

-----

Una vez tengamos el archivo grepeable, podemos utilizar la función [extractPorts] Para poder copiar la información relevante en la clipboard.

Ahora procedemos hacer un escaneo con **nmap** a los puertos detectados

```zhs
nmap -sCV -p21,22,139,445,3632 10.10.10.3 -oN targeted
```

Lo primero que veriamos es el sistema operativo, como vemos el puerto 21 podemos creer que es posible ingresar por el método **FTP**, Pero como usuario Anonymous nos podemos conectar ya que nos indica por la propia consola

Nos dirigimos a nuestra carpeta `Content` y realizamos el ftp a la dirección ip objetivo

```zsh
ftp 10.10.10.3
```

Una vez Logueados podemos tratar de buscar algo, pero no encontraremos ningún archivo de interes asi que continuamos

Tratamos de ver si tenemos poder de escritura haciendo 

```zsh
whoami > file
```

y en el `ftp` realizamos un 

```zsh
put file
```

Y efectivamente no tenemos poder de escritura, asi que nos diriguimos a de nuevo a nuestra carpeta `nmap`

Vemos la versión `vsftpd 2.3.4` en el puerto 21 y tratamos de buscar alguna vulneravilidad para poder aprovecharla

Nos dirigimos a nuestra carpeta `content` y buscamos la vulneravilidad con `searchsploit`

```bash
searchsploit vsftpd 2.3.4
```

veríamos algo asi :

![[Pasted image 20240618232522.png]]

Ahora para copiarnos el **exploit** ah nuestro directorio actual de trabajo de la siguiente manera:

```zsh
searchsploit -m unix/remote/49757.py
```
