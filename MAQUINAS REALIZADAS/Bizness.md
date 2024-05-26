
----
- TAG: #OSCP #STYLE #MAQUINA #HTB #eWPT
----
Hola chicos, hoy vamos estar hackeando la siguiente maquina de Hack The Box 

Empezamos Conectandonos a la vpn de htb y enviando el target objetivo que vamos a comprometer

Creamos nuestra carpeta `Bizness` y a continuación hacemos nuestro `mkt` que automaticamente nos crea los archivos necesarios para la auditoria, **nmap, scripts, exploits, content.**

Por si desean esta utilidad de `mkt` es la siguiente:
```
mkt () {
	mkdir {nmap,content,exploits,scripts}
}
```

---
Ingresamos en nuestra carpeta de scaner nmap para realizar un `ping` para ver si tenemos respuesta de la maquina
```
ping -c 1 10.10.11.252 
```

 Si tenemos un paquete enviado y un paquete recivido significa que si tenemos conexión a ella, si el `TTL` que nos muestra tiene proximidad con `64`, Significa que estamos ante una maquina `Linux` 
 Si le hacemos un `-R` al final del todo podemos ver por donde pasa nuestra ip ya que la conexión no es directa
 ```
 ping -c 1 10.10.11.252 -R
 ```

Tenemos una utilidad para poder identificar el sistema operativo con el siguiente scipt:
```
whichSystem.py 10.10.11.252
```

Script en python3:
```
#!/usr/bin/python3
#coding: utf-8

import re, sys, subprocess

# python3 wichSystem.py 10.10.10.188 

if len(sys.argv) != 2:
    print("\n[!] Uso: python3 " + sys.argv[0] + " <direccion-ip>\n")
    sys.exit(1)

def get_ttl(ip_address):

    proc = subprocess.Popen(["/usr/bin/ping -c 1 %s" % ip_address, ""], stdout=subprocess.PIPE, shell=True)
    (out,err) = proc.communicate()

    out = out.split()
    out = out[12].decode('utf-8')

    ttl_value = re.findall(r"\d{1,3}", out)[0]

    return ttl_value

def get_os(ttl):

    ttl = int(ttl)

    if ttl >= 0 and ttl <= 64:
        return "Linux"
    elif ttl >= 65 and ttl <= 128:
        return "Windows"
    else:
        return "Not Found"

if __name__ == '__main__':

    ip_address = sys.argv[1]

    ttl = get_ttl(ip_address)

    os_name = get_os(ttl)
    print("\n\t%s (ttl -> %s): %s" % (ip_address, ttl, os_name))
```

Ahora con la ayuda de `nmap` escanearemos tos los puertos con `-p-` unicamente por los puertos abiertos `--open` con un `stelf scan` con `-sS` que nos permite realizar un scaneo mas sigilozo, al igual que muy rapido , a continuación de un `--min-rate 5000` para indicar a tramitar paquetes menores a 5000 por segundo, le aplicamos un triple verbose para ver por consola lo que tramita `-vvv `, `-n` para que no nos aplique resolución `dns` y si no queremos que nos descubra hosts ataves del protoco de resolución de direcciones usamos un `-Pn` y a continución nuestra dirección ip objetivo.
Lo exportamos a un documento grepeable con `-oG allPorts` 
```
nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 10.10.11.252 -oG allPorts
```

Si revisamos nuestro archivo `allPorts` veremos toda la información solicitada
```
cat allPorts
```

Pero si le hacemos un `extractPorts` con nuestra utilidad, que si desean se las dejo a continuación del ejemplo:
```
extractPorts allPorts
```

- Utilidad `extractPorts` 
```
extractPorts () {
	ports="$(cat $1 | grep -oP '\d{1,5}/open' | awk '{print $1}' FS='/' | xargs | tr ' ' ',')" 
	ip_address="$(cat $1 | grep -oP '\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}' | sort -u | head -n 1)" 
	echo -e "\n[*] Extracting information...\n" > extractPorts.tmp
	echo -e "\t[*] IP Address: $ip_address" >> extractPorts.tmp
	echo -e "\t[*] Open ports: $ports\n" >> extractPorts.tmp
	echo $ports | tr -d '\n' | xclip -sel clip
	echo -e "[*] Ports copied to clipboard\n" >> extractPorts.tmp
	bat extractPorts.tmp
	rm extractPorts.tmp
}
```

Esto hará que se nos copie en la clipboard y le podamos hacer un escaneo a los puertos con nmap 
```
nmap -sC -p22,80,443,44459
```

`-sC` significa el tipo de script que deseamos enviar al puerto solicitado
Recuerden que nmap contiene muchos scripts escritos en lua buscando con `locate .nse`
Como me interesa encontrar la version y el servicio podemos usar `-sV` o conpactarle con `sCV` 
Y para finalizar indicamos la dirección ip y nos guardamos como archivo nmap con `oN targeted`
```
nmap -sCV -p22,80,443,44459 10.10.11.252 -oN targeted
```

Ahora podemos revisar el archivo en estilo java 
```
cat targeted -l java 
```

Podemos observar información importante como la que hay en el puerto 22 y buscar por la pagina `launchpad` para ver a los que nos estamos enfrentando, asi que nos damos cuenta que estamos enfrentando un ubuntu `bullseye` 

En el puerto 80 vemos que hay un redireccionamiento a una pagina `https://bizness.htb/` 

Pero si le hacemos un `ping` a https://bizness.htb/ no va a saber que es asi que le agregamos en nuestra lista de hosts
```
nvim /etc/hosts
```

la siguiente dirección 
```
10.10.11.252 bizness.htb
```

Adicional le podemos aplicar un `whatweb` para identificar las tecnologias por detras  
```
whatweb http://bizness.htb
```

Recuerden que el certificado ssl lo podemos ver de la siguiente manera
```
openssl s_client -connect bizness.htb:443
```
Viene bien aveces revisar el certificado por que en ocaciones en comant name se puede observar subdominios o correos, etc

Si nos dirigimos al final y vemosenel apartado de `powered by BootstrapMade` y tratamos de buscar un sploit y vemos un archivo importante en `git hub` y vemos que nos da un autentication bypass, de primera nos hace pensar que tiene un panel de logeo 
Ahora realizaremos el siguiente comando con `wfuzz` para encontrar directorios o archivos
```
wfuzz -c --hc=404,302 -t 200 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt https://bizness.htb/FUZZ
```

Usando fuerza bruta para encontrar los direcctorios de la pagina web encontramos un archivo `/control` y si lo buscamos como directorio en la pagina web nos va a reflejar que no existe, asi que volvemos a usar el comando de arriba pero ahora con el directorio `/control`
```
wfuzz -c --hc=404,302 -t 200 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt https://bizness.htb/control/FUZZ
```

Ocultamos todos que contengan mas de 1596 palabras con --hw=1596
```
wfuzz -c --hc=404,302 --hw=1596 -t 200 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt https://bizness.htb/control/FUZZ
```

Y podemos encontrar la pagina de `login` asi que ingresamos a la pagina `https://bizness.htb/control/login` 
Nos mostrara una pagina de logeo con usuario y constraseña asi que de primeras buscamos usuario y contraseñas default de `ofbiz` y vemos que no nos permite, la han cambiado de un principio 

Empezamos a buscar exploit para `ofbiz` que encontramos de `CVE-2023-51467` La vulneravilidad permite al atacante omitir el paso de autenticación haciendo un `Server-Side Request Forgery (SSRF)` y `Pre-auth RCE` con la vulneravilidad `CVE-2023-49070` 

Dejo el primer repositorio que les va a servir de mucho :
- [Apache-OFBiz-Authentication-Bypass](https://github.com/jakabakos/Apache-OFBiz-Authentication-Bypass)
En la carpeta (xdetection.py) de github podemos ver un poco sobre el detector en python 
Nos dirigimos a nuestra carpeta `content` y nos clonamos el repositorio 
```
git clone https://github.com/jakabakos/Apache-OFBiz-Authentication-Bypass/
```

Y usamos la siguiente herramienta para saber si es vulnerable o no 
```
python3 xdetection.py --url https://bizness.htb
```
