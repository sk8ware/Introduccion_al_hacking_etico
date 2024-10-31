
---- 
- TAG: #FUZZING #ENUMERACIÓN #ARCHIVOS #WEB 
----

En esta clase, hacemos uso de las herramientas **Wfuzz** y **Gobuster** para aplicar **Fuzzing**. Esta técnica se utiliza para descubrir rutas y recursos ocultos en un servidor web mediante ataques de fuerza bruta. El objetivo es encontrar recursos ocultos que podrían ser utilizados por atacantes malintencionados para obtener acceso no autorizado al servidor.

**Wfuzz** es una herramienta de descubrimiento de contenido y una herramienta de inyección de datos. Básicamente, se utiliza para automatizar los procesos de prueba de vulnerabilidades en aplicaciones web.

Permite realizar ataques de fuerza bruta en parámetros y directorios de una aplicación web para identificar recursos existentes. Una de las **ventajas** de Wfuzz es que es altamente personalizable y se puede ajustar a diferentes necesidades de pruebas. Algunas de las **desventajas** de Wfuzz incluyen la necesidad de comprender la sintaxis de sus comandos y que puede ser más lenta en comparación con otras herramientas de descubrimiento de contenido.

Por otro lado, **Gobuster** es una herramienta de descubrimiento de contenido que también se utiliza para buscar archivos y directorios ocultos en una aplicación web. Al igual que Wfuzz, Gobuster se basa en ataques de fuerza bruta para encontrar archivos y directorios ocultos. Una de las principales **ventajas** de Gobuster es su velocidad, ya que es conocida por ser una de las herramientas de descubrimiento de contenido más rápidas. También es fácil de usar y su sintaxis es simple. Sin embargo, una **desventaja** de Gobuster es que puede no ser tan personalizable como Wfuzz.

En resumen, tanto Wfuzz como Gobuster son herramientas útiles para pruebas de vulnerabilidades en aplicaciones web, pero tienen diferencias en su enfoque y características. La elección de una u otra dependerá de tus necesidades y preferencias personales.

A continuación, te proporcionamos el enlace a estas herramientas:

- **Wfuzz**: [https://github.com/xmendez/wfuzz](https://github.com/xmendez/wfuzz)
- **Gobuster**: [https://github.com/OJ/gobuster](https://github.com/OJ/gobuster)

**Comandos utilizados:**

- gobuster dir -u [https://miwifi.com/](https://miwifi.com/) -w /kali/home/SecLists/Discovery/Web-Content/directory-2.3-medium.txt -t 200 —add-slash -b 403,404 Este comando enlista rutas o directorios de paginas web con gobuster (si no hay permiso de por medio puede llegar a ser ilegal)
- gobuster dir -u [https://miwifi.com/](https://miwifi.com/) -w /kali/home/SecLists/Discovery/Web-Content/directory-2.3-medium.txt -t 50 -x html -s 200 -b ‘ ‘ Este comando muestra directorios y filtra por hmtl
- wfuzz -c —hc=404 -t 200 -w /kali/home/SecLists/Discovery/Web-Content/directory-2.3-medium.txt [https://miwifi.com/FUZZ/](https://miwifi.com/FUZZ/) El parametro —hc=404 elimina la respuesta 404 Este comando indica los directorios con wfuzz