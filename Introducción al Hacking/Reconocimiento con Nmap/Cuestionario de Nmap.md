
**1. ¿Qué parámetro de gobuster se utiliza para especificar la URL o el dominio objetivo para la búsqueda?**

`-u`

Este parámetro permite a los usuarios especificar la URL o el dominio que se va a escanear para buscar archivos y directorios ocultos en la aplicación web.

**2.¿Cuál es el modo de escaneo más rápido en Nmap?**

Escaneo de puertos TCP SYN

El escaneo de puertos TCP SYN es el modo más rápido de escaneo en Nmap porque aprovecha el handshake de tres pasos de TCP para determinar si el puerto está abierto o cerrado, sin establecer completamente la conexión.

**3. ¿Qué parámetro de wfuzz se utiliza para realizar una petición con un método HTTP personalizado, como PUT o DELETE?**

`-X`

Este parámetro permite a los usuarios especificar un método HTTP personalizado para usar en las solicitudes, en lugar del método HTTP estándar GET

**4. ¿Qué parámetro se utiliza en Nmap para escanear puertos UDP?**

`-sU`

Este parámetro indica a Nmap que realice un escaneo de puertos UDP en lugar de un escaneo de puertos TCP, ya que por defecto Nmap realiza un escaneo de puertos TCP.

**5. ¿Qué formas válidas existen con nmap de indicar que queremos escanear todo el rango total de puertos?**

`-p-`

Esta es la forma acotada de indicarle a nmap que queremos abarcar todo el rango total de puertos existentes para nuestro escaneo.

**6. ¿Qué técnica de escaneo de Nmap se utiliza para enviar paquetes TCP con banderas TCP URG y PUSH activadas para detectar hosts o puertos que estén protegidos por firewalls que bloquean paquetes SYN?**

`XMAS scan`

Esta técnica utiliza un paquete TCP con las banderas URG, PUSH y FIN activadas para enviar al puerto de destino y analizar la respuesta. Si el puerto está cerrado, se recibirá una respuesta RST. Si el puerto está abierto, no se recibirá ninguna respuesta y se puede inferir que el puerto está abierto.

**7. ¿Qué técnica de escaneo de Nmap se utiliza para detectar sistemas operativos en una red?**

`OS Fingerprinting`

Esta técnica se basa en el análisis de las respuestas del protocolo TCP/IP durante el escaneo y el envío de paquetes, para determinar la identidad del sistema operativo en el host de destino.

**8. ¿Qué parámetro de wfuzz se utiliza para especificar una lista de palabras para realizar un ataque de fuerza bruta?**

`-w`

Este parámetro permite a los usuarios especificar una lista de palabras para probar diferentes combinaciones de nombres de usuario, contraseñas y otros parámetros en un ataque de fuerza bruta.

**9. ¿En qué lenguaje se pueden escribir scripts personalizados para nmap?**

`Lua`

Lua es el lenguaje de programación en el que se pueden escribir scripts personalizados para Nmap. Lua es un lenguaje de scripting eficiente y ligero que se integra perfectamente con Nmap y proporciona una gran flexibilidad y control para personalizar los escaneos y la salida de Nmap.

### 10. Rellena el espacio con el parámetro correcto de la herramienta Wfuzz (con guiones incluidos)

`--hh`

**11. ¿Qué técnica alternativa se puede utilizar para enumerar puertos en lugar del escaneo de puertos TCP/UDP?**

Enumeración de puertos usando descriptores de archivo

La enumeración de puertos mediante descriptores de archivo /dev/tcp es una técnica alternativa de escaneo de puertos que manipula descriptores de archivo en sistemas operativos tipo Unix para acceder a puertos remotos y determinar si están abiertos o cerrados.

**12. ¿Qué parámetro de Nmap se utiliza para realizar un escaneo rápido sin realizar una resolución DNS inversa?**

`-n`

Este parámetro evita que Nmap realice una resolución DNS inversa en las direcciones IP que se están escaneando, lo que puede acelerar el escaneo y evitar posibles retrasos en la resolución DNS inversa.

**13. ¿Qué técnica de escaneo de Nmap se utiliza para omitir el escaneo de puertos cerrados y enfocarse solo en los puertos abiertos?**

ACK scan

Esta técnica envía paquetes TCP ACK a los puertos que se están investigando y analiza las respuestas para determinar si los puertos están abiertos, cerrados o filtrados por un firewall.

**14. ¿Qué parámetro de Nmap me sirve para controlar el temporizado y el rendimiento del escaneo?**

`-T`

Este parámetro permite al usuario especificar el perfil de temporización del escaneo, que controla la velocidad y la agresividad del escaneo. Los perfiles de temporización incluyen opciones como "-T0" (modo sigiloso, más lento y menos intrusivo), "-T3" (modo normal, equilibrado entre velocidad y precisión) y "-T5" (modo agresivo, más rápido y menos preciso).

**15. ¿Qué cabecera debo usar con Wfuzz si deseo enumerar subdominios mediante un ataque de fuerza bruta sobre un dominio dado?**

`Host`

Al incluir la cabecera "Host" en la solicitud, se puede especificar el subdominio que se está atacando. Por ejemplo, el comando "wfuzz -H 'Host: [FUZZ.example.com](http://fuzz.example.com/)' [](http://example.com/)[http://example.com](http://example.com)" enviará solicitudes HTTP a la URL "[](http://example.com/)[http://example.com](http://example.com)" utilizando diferentes subdominios especificados en el diccionario proporcionado.

**17. ¿Cuál es la técnica de escaneo de Nmap que utiliza paquetes ICMP Echo Request en lugar de TCP o UDP?**

`ICMP scan`

Esta técnica utiliza paquetes ICMP para determinar la disponibilidad de hosts y puede ser útil en situaciones donde el tráfico de TCP o UDP es bloqueado o filtrado.

**18. Rellena el espacio con el parámetro correcto de la herramienta Wfuzz (con guiones incluidos)**

Si quiero con Wfuzz mostrar aquellas respuestas que tengan un número de palabras dado, tendré que usar el parámetro `—sc`

**19.¿Qué parámetro de wfuzz se utiliza para especificar el código de estado HTTP para considerar una respuesta como válida durante un ataque de fuerza bruta?**

`—sc`

Este parámetro permite a los usuarios especificar uno o varios códigos de estado HTTP para considerar una respuesta como válida durante un ataque de fuerza bruta.

**20. ¿Qué parámetro se utiliza en Nmap para ocultar la dirección IP de origen de los paquetes enviados durante el escaneo?**

`-D`

Este parámetro permite a Nmap enviar paquetes desde direcciones IP falsas o aleatorias, lo que puede ayudar a ocultar la dirección IP real del escáner y evitar la detección por parte de los sistemas de seguridad.

**21. Rellena el campo con la respuesta correcta**

64

22. ¿Qué parámetro de Nmap se utiliza para especificar un rango de puertos a escanear?

`-P`

Este parámetro permite a los usuarios especificar un rango de puertos a escanear, lo que puede ayudar a acelerar el escaneo y enfocarse en los puertos de interés.

**23. ¿Qué comando me permitiría desde gobuster aplicar un reconocimiento de subdominios?**

`vhost`

Esta opción es utilizada para realizar un ataque de fuerza bruta contra el servidor web, buscando subdominios o virtual hosts.

**24. Rellena el campo con la respuesta correcta**

128