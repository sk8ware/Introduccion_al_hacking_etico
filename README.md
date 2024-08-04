
# README

Este repositorio contiene una serie de recursos y guías relacionadas con Linux, hacking ético, y desarrollo de habilidades ofensivas en Python.

# N°1 Introducción a Linux

En esta sección se cubren diversos aspectos relacionados con el sistema operativo Linux.

---
- N°1 Actualización y Upgradeo del sistema
- N°2 Asignación de permisos
- N°3 Búsquedas a nivel de sistema
- N°4 Comandos básicos de Linux
- N°5 Control de atributos de ficheros en Linux – Chattr y Lsattr
- N°6 Control del flujo stderr-stdout, operadores y procesos en segundo plano
- N°7 Cuestionario
- N°8 Descriptores de archivo
- N°9 Estructura de directorios del sistema
- N°10 Lectura e interpretación de permisos
- N°11 Notación octal de permisos
- N°12 Permisos especiales – SUID y SGID
- N°13 Permisos especiales – Sticky Bit
- N°14 Privilegios especiales – Capacidades
- N°15 Sistemas operativos para pentesting
- N°16 Uso de bashrc y zshrc
- N°17 Uso y manejo con Tmux
----
# N°2 Personalización del entorno en Linux

En esta sección aprenderán a configurar su entorno como un verdadero hacker

---
- N°1 Instalación y configuración de Bspwm y Sxhkd
- N°2 Instalación de Polybar, Picom y Rofi
- N°3 Configurando las fuentes, la Kitty e instalación de Feh
- N°4 Despliegue de la Polybar
- N°5 Configurando los bordeados, las sombras y los difuminados con Picom
- N°6 Configurando la ZSH e instalando Powerlevel10k
- N°7 Instalación de Batcat y Lsd
- N°8 Configurando la Polybar
- N°9 Creando nuevos módulos en la Polybar
- N°10 Configuración e integración de NVchad en Neovim
- N°11 Repaso final por todos los atajos definidos
----
# N°3 Introducción al Hacking

Esta sección cubre fundamentos y técnicas relacionadas con el hacking ético.

---

- ## N°1 Conceptos básicos de IP, MAC, UDP, TCP, OSI, etc.
- N°2 SUBNETTING
	- N°2.1 Subnetting – CIDRs y cálculo total de hosts
	- N°2.2 Subnetting – Interpretación de los rangos de red que el cliente nos ofrece para auditar	
	- N°2.3 Subnetting – Máscaras de subred, tipos de clase e interpretación de prefijos de red
	- N°2.4 Subnetting – Qué es y cómo se interpreta una máscara de red
	- N°2.5 Subnetting – Redes extrañas y casos particulares
	- N°2.6 TIPS de subnetting y cálculo veloz de direccionamiento en redes
    - N°2.7 Direcciones IP (IPv4 e IPv6)
- N°3 Direcciones MAC (OUI y NIC)
- N°4 El modelo OSI – En qué consiste y cómo se estructura la actividad de red en capas
- N°5 Protocolos comunes (UDP, TCP) y el famoso Three-Way Handshake
---
- ## N°6 Conceptos básicos de enumeración y explotación
	- N°6.1 Enumeración del sistema
	- N°6.2 Introducción a BurpSuite
	- N°6.3 Introducción a la explotación de vulnerabilidades
	- N°6.4 Reverse Shells, Bind Shells y Forward Shells
	- N°6.5 Tipos de explotación (Manuales y Automatizadas)
	- N°6.6 Tipos de payloads (Staged y Non-Staged)
----
- ## N°7 Enumeración de servicios comunes y gestores de contenido
- N°7.1 Enumeración de gestores de contenido CMS
	- N°7.1.1 Drupal
	- N°7.1.2 Joomla
	- N°7.1.3 Magento
	- N°7.1.4 WordPress
- N°7.2 Enumeración del servicio FTP
- N°7.3 Enumeración del servicio HTTP y HTTPS
- N°7.4 Enumeración del servicio SMB
- N°7.5 Enumeración del servicio SSH
----
- ## N°8 Introducción a Docker
	- N°8.1 Carga de instrucciones en Docker y desplegando nuestro primer contenedor
	- N°8.2 Comandos comunes para la gestión de contenedores
	- N°8.3 Creación y construcción de imágenes
	- N°8.4 DOCKER
	- N°8.5 Definiendo la estructura básica de Dockerfile
	- N°8.6 Despliegue de máquinas vulnerables con Docker-Compose
	- N°8.7 Instalación de Docker en Linux
	- N°8.8 Port Forwarding en Docker y uso de monturas
----
- ## N°9 OWASP TOP 10 y vulnerabilidades web
	- N°9.1 Cross-Site Request Forgery (CSRF)
	- N°9.2 Cross-Site Scripting (XSS)
	- N°9.3 Local File Inclusion (LFI)
	- N°9.4 Log Poisoning (LFI - RCE)
	- N°9.5 Remote File Inclusion (RFI)
	- N°9.6 SQL Injection (SQLI)
	- N°9.7 Server-Side Request Forgery (SSRF)
	- N°9.8 Server-Side Template Injection (SSTI)
	- N°9.9 XML External Entity Injection (XXE)
-----
- ## N°10 Reconocimiento
	- N°10.1 Alternativas para la enumeración de puertos usando descriptores de archivo
	- N°10.2 Creación de tus propios scripts en Lua para nmap
	- N°10.3 Credenciales y brechas de seguridad
	- N°10.4 Cuestionario de Nmap
	- N°10.5 Descubrimiento de correos electrónicos
	- N°10.6 Descubrimiento de equipos en la red local (ARP e ICMP) y Tips
	- N°10.7 Enumeración de subdominios
	- N°10.8 Fuzzing y enumeración de archivos en un servidor web
	- N°10.9 Google Dorks - Google Hacking (Los 18 Dorks más usados)
	- N°10.10 Identificación de las tecnologías en una página web
	- N°10.11 Identificación y verificación externa de la versión del sistema operativo
	- N°10.12 Reconocimiento de imágenes
	- N°10.13 Scaneo con nmap y sus funciones
	- N°10.14 Técnicas de evasión de Firewalls (MTU, Data Length, Source Port, Decoy, etc.)
	- N°10.15 Uso de scripts y categorías en nmap para aplicar reconocimiento
	- N°10.16 Validación del objetivo (Fijando un target en HackerOne)
----

# N°4 Python Ofensivo

Domina Python **desde cero** y crea tu propio arsenal de herramientas ofensivas para enfrentarte a los retos más complejos en ciberseguridad

---
- ## N°1 Introducción a Python
	- N°1.1 Historia y filosofía de Python
	- N°1.2 Características y ventajas de Python
	- N°1.3 Diferencias entre Python2, Python3, PIP2 y PIP3
- ## N°2 Conceptos básicos de Python
	- N°2.1 El intérprete de Python 
	- N°2.2 Shebang y convenios en Python
	- N°2.3 Variables y tipos de datos
	- N°2.4 Operadores básicos en Python
	- N°2.5 Formato de cadenas
	- N°2.6 Control de flujo (Condicionales y Bucles)
	- N°2.7 Funciones y ámbito de las variables
	- N°2.8 Funciones lambda anónimas
	- N°2.9 Manejo de errores y excepciones
- ## N°3 Colecciones y estructuras de datos en Python
	- N°3.1 Listas
	- N°3.2 Tuplas
	- N°3.3 Conjuntos
	- N°3.4 Diccionarios
	- N°3.5 Proyecto videojuegos

---
# N°5 Maquinas

Maquinas realizadas en **Hack The Box**

---
- N°1 Builder - **medium difficulty**
- N°2 Bizness - **medium difficulty**
- N°3 Hospital - **easy difficulty**
----

hola 