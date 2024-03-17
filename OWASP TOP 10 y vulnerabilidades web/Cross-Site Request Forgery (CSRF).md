
----
- Tag: #CROSS-SITE #REQUEST #FORGERY #CSRF 
----
>**AVISO (Actualización 11/05/2023)**: Si a la hora de hacer el ‘**docker-compose up -d**‘, os salta un error de tipo: “**networks.net-10.9.0.0 value Additional properties are not allowed (‘name’ was unexpected)**“, lo que tenéis que hacer es en el archivo ‘**docker-compose.yml**‘, borrar la línea número 41, la que pone “**name: net-10.9.0.0**“.

Con hacer esto, ya podréis desplegar el laboratorio sin ningún problema.

El **Cross-Site Request Forgery** (**CSRF**) es una vulnerabilidad de seguridad en la que un atacante **engaña** a un usuario legítimo para que realice una acción no deseada en un sitio web sin su conocimiento o consentimiento.

En un ataque CSRF, el atacante engaña a la víctima para que haga clic en un enlace malicioso o visite una página web maliciosa. Esta página maliciosa puede contener una solicitud HTTP que realiza una acción no deseada en el sitio web de la víctima.

Por ejemplo, imagina que un usuario ha iniciado sesión en su cuenta bancaria en línea y luego visita una página web maliciosa. La página maliciosa contiene un formulario que envía una solicitud HTTP al sitio web del banco para transferir fondos de la cuenta bancaria del usuario a la cuenta del atacante. Si el usuario hace clic en el botón de envío sin saber que está realizando una transferencia, el ataque CSRF habrá sido exitoso.

El ataque CSRF puede ser utilizado para realizar una amplia variedad de acciones no deseadas, incluyendo la transferencia de fondos, la modificación de la información de la cuenta, la eliminación de datos y mucho más.

Para prevenir los ataques CSRF, los desarrolladores de aplicaciones web deben implementar medidas de seguridad adecuadas, como la inclusión de tokens CSRF en los formularios y solicitudes HTTP. Estos tokens CSRF permiten que la aplicación web verifique que la solicitud proviene de un usuario legítimo y no de un atacante malintencionado (aunque cuidadín que también se pueden hacer cositas con esto).

Os compartimos a continuación el enlace al comprimido ZIP que utilizamos en esta clase para desplegar el laboratorio donde practicamos esta vulnerabilidad:

- **Lab Setup**: [https://seedsecuritylabs.org/Labs_20.04/Files/Web_CSRF_Elgg/Labsetup.zip](https://seedsecuritylabs.org/Labs_20.04/Files/Web_CSRF_Elgg/Labsetup.zip)
----
# Empezamos desplegando nuestro laboratorio 

- Descargamos el siguiente comprimido.
```
wget https://seedsecuritylabs.org/Labs_20.04/Files/Web_CSRF_Elgg/Labsetup.zip
```

- Lo descomprimimos con
```
unzip Labsetup.zip
```

- Ingresamos a la carpeta y deplegamos el docker 
```
docker-compose up -d 
```

- En este punto deberiamos realizar las siguientes modificaciones en la ruta **/etc/hosts** ya el laboratorio contiene una ip especifica para cada puerto.
```
10.9.0.5 www.seed-server.com
10.9.0.5 www.example32.com
10.9.105 www.attacker32.com
```
- En este caso solo nos enfocaremos en el dominio www.seed-server.com para realizar la práctica, eh ingresamos al dominio desde nuestro navegador.
- En este ejemplo usaremos solo dos usuarios y contraseñas que serian creados con nvim un archivo .txt
```
alice:seedalice
samy:seedsamy
```