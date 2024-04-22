
----
- TAG: #ENUMERACIÓN #CMS #TIENDAS-EN-LINEA #ESCALABLES #NIKE #COCA-COLA
-----
En esta clase, veremos cómo enumerar el gestor de contenido **Magento**. Magento es una plataforma de comercio electrónico de código abierto, que se utiliza para construir tiendas en línea de alta calidad y escalables. Es una de las plataformas más populares para el comercio electrónico y es utilizado por grandes marcas como Nike, Coca-Cola y Ford.

Sin embargo, con la popularidad de Magento también ha surgido la preocupación por la seguridad. Una de las herramientas que veremos en esta clase es **Magescan**, una herramienta de escaneo de vulnerabilidades específica para Magento.

Magescan puede detectar vulnerabilidades comunes en Magento, incluyendo problemas con permisos de archivos, errores de configuración y vulnerabilidades conocidas en extensiones populares de Magento.

A continuación se proporciona el enlace directo al proyecto en Github:

- **Magescan**: [https://github.com/steverobbins/magescan](https://github.com/steverobbins/magescan)

Su sintaxis y modo de uso es bastante sencillo, a continuación se comparte un ejemplo:

➜ `php magescan.phar scan:all <https://example.com`>

Donde “**magescan.pha**r” es el archivo ejecutable de la herramienta “**Magescan**“, “**scan:all**” es el comando específico de Magescan que indica que se realizará un escaneo exhaustivo de todas las vulnerabilidades conocidas en el sitio web objetivo y “**[https://example.com](https://example.com)**” es la URL del sitio web objetivo que se escaneará en busca de vulnerabilidades.

Asimismo, se comparte el enlace al laboratorio que estaremos desplegando en Docker para configurar el Magento vulnerable:

- **Magento 2.2 SQL Injection**: [https://github.com/vulhub/vulhub/tree/master/magento/2.2-sqli](https://github.com/vulhub/vulhub/tree/master/magento/2.2-sqli)

Una de las técnicas que explotaremos sobre este gestor de contenidos es la famosa **SQL Injection**. Esta vulnerabilidad se produce cuando los datos de entrada no son debidamente validados y se pueden insertar comandos SQL maliciosos en la consulta a la base de datos.

Un ataque de inyección SQL exitoso puede permitir al atacante obtener información confidencial, como credenciales de usuario o datos de pago, o incluso ejecutar comandos en la base de datos del sitio web.

En el caso del Magento que estaremos desplegando, explotaremos una inyección SQL con el objetivo de obtener una cookie de sesión, la cual podremos posteriormente utilizar para llevar a cabo un ataque de “**Cookie Hijacking**“. Este tipo de ataque nos permitirá como atacantes asumir la identidad del usuario legítimo y acceder a las funciones del usuario, que en este caso será administrador.

Comandos utilizados:

1. Crear entorno vulnerable de Magento
2. Copiar el raw del github en la terminal wget [https://github.com/ambionics/magento-exploits/blob/master/magento-sqli.py](https://github.com/ambionics/magento-exploits/blob/master/magento-sqli.py)
3. Iniciar sesión para poder copiar el cookie de inicio de sesión
4. abrir inspeccionar para buscar el redes y en cookies copiar el **Value** de **admin**
5. En la terminal `python3 [magento-sqli.py](<http://magento-sqli.py>) <http://localhost:8080/`> para obtener la cookie de inicio de sesión por la terminal con ataque de fuerza bruta con [`magento-sqli.py`](http://magento-sqli.py)
6. Abrir el navegador de burpsuite y descargar la extensión de **cookie management tool**
7. abrir el navegador en burpsuite y abrir la extensión para guardar la cookie de inicio de sesión y actualizar la pagina para ingresar

TIPS:

- Ayudarnos con la libreria de github **Vulhub** ya que tiene varias gestores, aplicativos para hacer varias cosillas.