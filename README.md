
# README

Este repositorio contiene una serie de recursos y guías relacionadas con Linux, hacking ético, y desarrollo de habilidades ofensivas en Python.

# Introducción a Linux

En esta sección se cubren diversos aspectos relacionados con el sistema operativo Linux.

---
- Actualización y Upgradeo del sistema
- Asignación de permisos
- Búsquedas a nivel de sistema
- Comandos básicos de Linux
- Control de atributos de ficheros en Linux – Chattr y Lsattr
- Control del flujo stderr-stdout, operadores y procesos en segundo plano
- Cuestionario
- Descriptores de archivo
- Estructura de directorios del sistema
- Lectura e interpretación de permisos
- Notación octal de permisos
- Permisos especiales – SUID y SGID
- Permisos especiales – Sticky Bit
- Privilegios especiales – Capacidades
- Sistemas operativos para pentesting
- Uso de bashrc y zshrc
- Uso y manejo con Tmux
----
# Personalización del entorno en Linux

En esta sección aprenderán a configurar su entorno como un verdadero hacker

---
- Instalación y configuración de Bspwm y Sxhkd
- Instalación de Polybar, Picom y Rofi
- Configurando las fuentes, la Kitty e instalación de Feh
- Despliegue de la Polybar
- Configurando los bordeados, las sombras y los difuminados con Picom
- Configurando la ZSH e instalando Powerlevel10k
- Instalación de Batcat y Lsd
- Configurando la Polybar
- Creando nuevos módulos en la Polybar
- Configuración e integración de NVchad en Neovim
- Repaso final por todos los atajos definidos
----
# Introducción al Hacking

Esta sección cubre fundamentos y técnicas relacionadas con el hacking ético.

---

- ## Conceptos básicos de IP, MAC, UDP, TCP, OSI, etc.
- SUBNETTING
	- Subnetting – CIDRs y cálculo total de hosts
	- Subnetting – Interpretación de los rangos de red que el cliente nos ofrece para auditar	
	- Subnetting – Máscaras de subred, tipos de clase e interpretación de prefijos de red
	- Subnetting – Qué es y cómo se interpreta una máscara de red
	- Subnetting – Redes extrañas y casos particulares
	- TIPS de subnetting y cálculo veloz de direccionamiento en redes
    - Direcciones IP (IPv4 e IPv6)
- Direcciones MAC (OUI y NIC)
- El modelo OSI – En qué consiste y cómo se estructura la actividad de red en capas
- Protocolos comunes (UDP, TCP) y el famoso Three-Way Handshake
---
- ## Conceptos básicos de enumeración y explotación
	- Enumeración del sistema
	- Introducción a BurpSuite
	- Introducción a la explotación de vulnerabilidades
	- Reverse Shells, Bind Shells y Forward Shells
	- Tipos de explotación (Manuales y Automatizadas)
	- Tipos de payloads (Staged y Non-Staged)
----
- ## Enumeración de servicios comunes y gestores de contenido
- Enumeración de gestores de contenido CMS
	- Drupal
	- Joomla
	- Magento
	- WordPress
- Enumeración del servicio FTP
- Enumeración del servicio HTTP y HTTPS
- Enumeración del servicio SMB
- Enumeración del servicio SSH
----
- ## Introducción a Docker
	- Carga de instrucciones en Docker y desplegando nuestro primer contenedor
	- Comandos comunes para la gestión de contenedores
	- Creación y construcción de imágenes
	- DOCKER
	- Definiendo la estructura básica de Dockerfile
	- Despliegue de máquinas vulnerables con Docker-Compose
	- Instalación de Docker en Linux
	- Port Forwarding en Docker y uso de monturas
----
- ## OWASP TOP 10 y vulnerabilidades web
	- Cross-Site Request Forgery (CSRF)
	- Cross-Site Scripting (XSS)
	- Local File Inclusion (LFI)
	- Log Poisoning (LFI - RCE)
	- Remote File Inclusion (RFI)
	- SQL Injection (SQLI)
	- Server-Side Request Forgery (SSRF)
	- Server-Side Template Injection (SSTI)
	- XML External Entity Injection (XXE)
-----
- ## Reconocimiento
	- Alternativas para la enumeración de puertos usando descriptores de archivo
	- Creación de tus propios scripts en Lua para nmap
	- Credenciales y brechas de seguridad
	- Cuestionario de Nmap
	- Descubrimiento de correos electrónicos
	- Descubrimiento de equipos en la red local (ARP e ICMP) y Tips
	- Enumeración de subdominios
	- Fuzzing y enumeración de archivos en un servidor web
	- Google Dorks - Google Hacking (Los 18 Dorks más usados)
	- Identificación de las tecnologías en una página web
	- Identificación y verificación externa de la versión del sistema operativo
	- Reconocimiento de imágenes
	- Scaneo con nmap y sus funciones
	- Técnicas de evasión de Firewalls (MTU, Data Length, Source Port, Decoy, etc.)
	- Uso de scripts y categorías en nmap para aplicar reconocimiento
	- Validación del objetivo (Fijando un target en HackerOne)
----

# Maquinas

Maquinas realizadas en **Hack The Box**

---
- Builder - **medium difficulty**
- Bizness - **medium difficulty**
- Hospital - **easy difficulty**
----

# Python Ofensivo

Domina Python **desde cero** y crea tu propio arsenal de herramientas ofensivas para enfrentarte a los retos más complejos en ciberseguridad

---
- ## Introducción a Python
	- Historia y filosofía de Python
	- Características y ventajas de Python
	- Diferencias entre Python2, Python3, PIP2 y PIP3
- ## Conceptos básicos de Python
	- El intérprete de Python 
	- Shebang y convenios en Python
	- Variables y tipos de datos
	- Operadores básicos en Python
	- Formato de cadenas
	- Control de flujo (Condicionales y Bucles)
	- Funciones y ámbito de las variables
	- Funciones lambda anónimas
	- Manejo de errores y excepciones
- ## Colecciones y estructuras de datos en Python
	- Listas
	- Tuplas
	- Conjuntos
	- Diccionarios
	- Proyecto videojuegos

gobuster dir -u http://1.2.3.4/ -w /usr/share/wordlist/dirbuster/
