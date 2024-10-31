
----
- TAG : #NMAP #ESCANEO #FUNCIONES 
----

**Nmap (Network Mapper)** es una herramienta de escaneo de redes ampliamente utilizada para descubrir dispositivos y servicios en una red, así como para evaluar la seguridad de los sistemas informáticos. 

Aquí tienes una lista más completa de las funciones y opciones de Nmap:

1. **Escaneo de puertos**:
    - `-p <puertos>`: Especifica los puertos que se deben escanear.
    - `-F`: Escanea solo los puertos más comunes (100 puertos).
    - `-p-`: Escanea todos los puertos (0-65535).
2. **Escaneo de hosts**:
    - `-sL`: Lista de hosts sin escanear (no realiza escaneo, solo muestra los hosts).
    - `-sn`: Escaneo de hosts vivos (sin escanear puertos).
3. **Tipos de escaneo**:
    - `-sS`: Escaneo de tipo SYN.
    - `-sT`: Escaneo de tipo TCP Connect.
    - `-sU`: Escaneo de tipo UDP.
    - `-sA`: Escaneo de tipo ACK.
    - `-sF`: Escaneo de tipo FIN.
    - `-sN`: Escaneo de tipo NULL.
    - `-sX`: Escaneo de tipo Xmas Tree.
4. **Detección de sistemas operativos**:
    - `-O`: Intenta determinar el sistema operativo de los hosts.
    - `--osscan-limit`: Limita el número de host a los que se les realiza la detección de SO.
    - `--osscan-guess`: Adivina el sistema operativo de los hosts basándose en la detección.
5. **Escaneo de versiones de servicios**:
    - `-sV`: Intenta determinar las versiones de los servicios que se ejecutan en los puertos abiertos.
    - `--version-intensity <intensidad>`: Controla la intensidad del escaneo de versiones.
6. **Scripts NSE (Nmap Scripting Engine)**:
    - `--script <script>`: Ejecuta un script específico de NSE.
    - `--script-help <script>`: Muestra la ayuda de un script específico de NSE.
    - `--script-args <args>`: Proporciona argumentos adicionales para los scripts de NSE.
7. **Opciones de salida**:
    - `-oN <archivo>`: Guarda la salida en formato normal en un archivo.
    - `-oX <archivo>`: Guarda la salida en formato XML en un archivo.
    - `-oG <archivo>`: Guarda la salida en formato greppable en un archivo.
    - `-oA <prefijo>`: Guarda la salida en todos los formatos con un prefijo específico.
8. **Opciones de rendimiento**:
    - `-T <velocidad>`: Establece el nivel de velocidad/tiempo (0-5).
    - `--min-parallelism <número>`: Establece el número mínimo de tareas paralelas.
    - `--max-parallelism <número>`: Establece el número máximo de tareas paralelas.
9. **Otros**:
    - `-v`: Aumenta el nivel de verbosidad.
    - `-h`, `--help`: Muestra la ayuda y la lista de opciones.
    - `--open`: Muestra solo los puertos que están abiertos.
    - `--traceroute`: Realiza un trazado de ruta hacia el objetivo.
    - `-iL <archivo>`: Lee las direcciones IP o los rangos de direcciones desde un archivo.