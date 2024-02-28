
----
- Tags: #LSE #PSPY #ENUMERACIÓN
----
## **En esta parte explicaremos sobre las herramientas de enumeración.**

> **LSE** (**Linux Smart Enumeration**): Es una herramienta de enumeración para sistemas Linux que permite a los atacantes obtener información detallada sobre la configuración del sistema, los servicios en ejecución y los permisos de archivo. LSE utiliza una variedad de comandos de Linux para recopilar información y presentarla en un formato fácil de entender. Al utilizar LSE, los atacantes pueden detectar posibles vulnerabilidades y encontrar información valiosa para futuros ataques.


> **Pspy**: Es una herramienta de enumeración de procesos que permite a los atacantes observar los procesos y comandos que se ejecutan en el sistema objetivo a intervalos regulares de tiempo. Pspy es una herramienta útil para la detección de malware y backdoors, así como para la identificación de procesos maliciosos que se ejecutan en segundo plano sin la interacción del usuario.

# ISNTALACIÓN Y USO DE LSE:

- Primero instalamos la herramienta con el repositorio de **GITHUB**:
```
wget https://raw.githubusercontent.com/diego-treitos/linux-smart-enumeration/master/lse.sh
```

- Damos permiso de escritura:
```
chmod +x lse.sh
```

- Ejecutamos la herramienta:
```
./lse.sh
```


### REPOSITORIOS QUE SE PUEDEN UTILIZAR PARA ENUMERACIÓN LSE:
- [LinEnum.sh](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS)
-  [LSE.SH](https://raw.githubusercontent.com/diego-treitos/linux-smart-enumeration/master/lse.sh)



# AHORA UTILIZAREMOS LA HERRAMIENTA PSPY PARA REALIZAR UN RECONOCIMIENTO DE TAREAS Y COMANDOS:

- Ingresamos al repositorio en **HITHUB** y en release descargar el archivo **PSPY64** y le otorgamos permisos de ejecución
```
chmod +x pspy64
```

- Luego ejecutamos 
```
./pspy64
```
**Este comando muestra tareas que se ejecuta en intervalos de tiempo por consola**

## También tenemos la opción de hacerlo manualmente

- Con el siguiente comando podemos verificar los procesos en ejecución de nuestro sistema
```
ps -eo command
```

- Lo cual podemos crear un script con este comando para realizarlo de manera manual
```nvim
nvim procmon.sh
```

```bin/bash
#!/bin/bash

function ctrl_c(){
  echo -e "\n\n[!] Saliendo...\n"
  tput cnorm; exit 1
}

# Ctrl+C
trap ctrl_c SIGINT

old_process=$(ps -eo user, command)

tput civis # Ocultar cursor

while true; do 
  new_process=$(ps -eo user,command)
  diff <(echo "$old_process") <(echo "$new_process") | grep -vE "command|kworker|procmon"
  old_process=$new-process
done
```

- Damos permisos de ejecución al archivo creado
```
chmod +x procmon.sh
```


- Ejecutamos el archivo creado
```
./procmon.sh
```


# HERRAMIENTA PARA VER SI UN BINARIO ES VULNERABLE:

- [GTFOBINS](https://gtfobins.github.io/)
- [HACKTRICKS](https://book.hacktricks.xyz/welcome/readme)