
----
- TAG: #FUZZING #ENUMERACIÓN #WEB 
----

En esta clase, veremos cómo se pueden utilizar diferentes parámetros de **Wfuzz** para ajustar el alcance y la profundidad de nuestro reconocimiento en aplicaciones web. Algunos de los parámetros que cubriremos incluyen el parámetro ‘**–sl**‘, para filtrar por un número de líneas determinado, el parámetro ‘**–hl**‘ para ocultar un número de líneas determinado y por último el parámetro ‘**-z**‘ para indicar el tipo de dato que queremos usar de cara al reconocimiento que nos interese aplicar, abarcando opciones como diccionarios, listas y rangos numéricos.

Adicionalmente, otra de las herramientas que examinamos en esta clase, perfecta para la enumeración de recursos disponibles en una plataforma en línea, es **BurpSuite**. BurpSuite es una plataforma que integra características especializadas para realizar pruebas de penetración en aplicaciones web. Una de sus particularidades es la función de **análisis de páginas en línea**, empleada para identificar y enumerar los recursos accesibles en una página web.

BurpSuite cuenta con dos versiones: una **versión gratuita** (**BurpSuite Community Edition**) y una **versión de pago** (**BurpSuite Pofessional**).

### BurpSuite Community Edition

Es la **versión gratuita** de esta plataforma, viene incluida por defecto en el sistema operativo. Su función principal es desempeñar el papel de **proxy HTTP** para la aplicación, facilitando la realización de pruebas de penetración.

Un **proxy HTTP** es un filtro de contenido de alto rendimiento, ampliamente usado en el hacking con el fin de interceptar el tráfico de red. Esto permite analizar, modificar, aceptar o rechazar todas las solicitudes y respuestas de la aplicación que se esté auditando.

Algunas de las ventajas que la versión gratuita ofrecen son:

- **Gratuidad**: La versión Community Edition es gratuita, lo que la convierte en una opción accesible para principiantes y profesionales con presupuestos limitados.
- **Herramientas básicas**: Incluye las herramientas esenciales para realizar pruebas de penetración en aplicaciones web, como el Proxy, el Repeater y el Sequencer.
- **Intercepción y modificación de tráfico**: Permite interceptar y modificar las solicitudes y respuestas HTTP/HTTPS, facilitando la identificación de vulnerabilidades y la exploración de posibles ataques.
- **Facilidad de uso**: La interfaz de usuario de la Community Edition es intuitiva y fácil de utilizar, lo que facilita su adopción por parte de usuarios con diversos niveles de experiencia.
- **Aprendizaje y familiarización**: La versión gratuita permite a los usuarios aprender y familiarizarse con las funcionalidades y técnicas de pruebas de penetración antes de dar el salto a la versión Professional.
- **Comunidad de usuarios**: La versión Community Edition cuenta con una amplia comunidad de usuarios que comparten sus conocimientos y experiencias en foros y blogs, lo que puede ser de gran ayuda para resolver problemas y aprender nuevas técnicas.

A pesar de que la Community Edition no ofrece todas las funcionalidades y ventajas de la versión Professional, sigue siendo una opción valiosa para aquellos que buscan comenzar en el ámbito de las pruebas de penetración o que necesitan realizar análisis de seguridad básicos sin incurrir en costos adicionales.

### BurpSuite Proffesional

BurpSuite Proffessional es la **versión de pago** desarrollada por la empresa **PortSwigger**. Incluye, además del proxy HTTP, algunas herramientas de pentesting web como:

- **Escáner de seguridad automatizado**: Permite identificar vulnerabilidades en aplicaciones web de manera rápida y eficiente, lo que ahorra tiempo y esfuerzo.
- **Integración con otras herramientas**: Puede integrarse con otras soluciones de seguridad y entornos de desarrollo para mejorar la eficacia de las pruebas.
- **Extensibilidad**: A través de su API, BurpSuite Professional permite a los usuarios crear y añadir extensiones personalizadas para adaptarse a necesidades específicas.
- **Actualizaciones frecuentes**: La versión profesional recibe actualizaciones periódicas que incluyen nuevas funcionalidades y mejoras de rendimiento.
- **Soporte técnico**: Los usuarios de BurpSuite Professional tienen acceso a un soporte técnico de calidad para resolver dudas y problemas.
- **Informes personalizables**: La herramienta permite generar informes detallados y personalizados sobre las pruebas de penetración y los resultados obtenidos.
- **Interfaz de usuario intuitiva**: La interfaz de BurpSuite Professional es fácil de utilizar y permite a los profesionales de seguridad trabajar de manera eficiente.
- **Herramientas avanzadas**: Incluye funcionalidades avanzadas, como el módulo de intrusión, el rastreador de vulnerabilidades y el generador de payloads, que facilitan la identificación y explotación de vulnerabilidades en aplicaciones web.

En conclusión, tanto la Community Edition como la versión Professional de BurpSuite ofrecen un conjunto de herramientas útiles y eficientes para realizar pruebas de penetración en aplicaciones web. Sin embargo, la versión Professional brinda ventajas adicionales.

La elección entre ambas versiones dependerá del alcance y las necesidades específicas del proyecto o de la empresa. Si se requiere un conjunto básico de herramientas para pruebas de seguridad ocasionales, la Community Edition podría ser suficiente. No obstante, si se busca una solución más completa y personalizable, con soporte técnico y herramientas avanzadas para un enfoque profesional y exhaustivo, la versión Professional sería la opción más adecuada.

**Comandos utilizados:**

- wfuzz -c —hc=404,403 -t 200 -w /kali/home/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt [https://miwifi.com/FUZZ.html](https://miwifi.com/FUZZ.html) Este comando sirve para buscar directorios por `hmtl, txt`
- wfuzz -c —hc=404,403 -t 200 -w /kali/home/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -z list,html-txt-php [https://miwifi.com/FUZZ.FUZ2Z](https://miwifi.com/FUZZ.FUZ2Z) Este comando sirve para enlistar mas de un lenguaje, ahora vemos que mostrara por consola `html, txt, php`
- wfuzz -c —hw=6515 -t 200 -z range,1-20000 ‘[https://mi.com/shop/buy/detail?product_id=FUZZ’](https://mi.com/shop/buy/detail?product_id=FUZZ%E2%80%99) Este comando indica todos los productos de una ruta
- ffuf -c -t 200 -w /kali/home/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -u [https://miwifi.com/FUZZ/](https://miwifi.com/FUZZ/) —mc=200 Este comando permite utilizar la herramienta de git hub **ffuf** para mostrar codigos de estado y directorios de modo pasivo.
- burpsuite &> /dev/null & disown permite la intercepción y modificación de tráfico HTTP/HTTPS