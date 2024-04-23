
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