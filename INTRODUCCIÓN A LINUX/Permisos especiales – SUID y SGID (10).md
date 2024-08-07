
----
- TAG: #PERMISOS #ESPECIALES #SUID #SGID 
-----

>Puedes indagar más en el uso de permisos SUID/SGID en los siguientes enlaces que te proporciono:

- Permisos SGID, SUID y Sticky Bit: [Permisos SGID, SUID y Sticky Bit](https://deephacking.tech/permisos-sgid-suid-y-sticky-bit-linux/#:~:text=Permiso%20SGID,-El%20permiso%20SGID&text=Si%20se%20establece%20en%20un,perteneciente%2C%20el%20grupo%20del%20directorio.)
- Permisos especiales en Linux: [Permisos especiales en Linux – Sticky Bit, SUID y SGID](https://www.ochobitshacenunbyte.com/2019/06/17/permisos-especiales-en-linux-sticky-bit-suid-y-sgid/)
- Los bits SUID, SGID y Sticky: [Los bits SUID, SGID y Sticky](https://www.ibiblio.org/pub/linux/docs/LuCaS/Manuales-LuCAS/SEGUNIX/unixsec-2.1-html/node56.html)
-----
### SUID

Al abrir nuestra consola y convertirnos en **root**, podemos considerar un **binario** como `python3.11`. Al ejecutar `which python3.11`, obtenemos su ruta absoluta. En lugar de copiar manualmente esta ruta, podemos utilizar `xargs` para concatenar el comando y evitar trabajo adicional:

```bash
which python3.11 | xargs ls -l
```

Luego, podemos otorgar permisos **SUID** al binario:

```bash
chmod u+s /usr/bin/python3.11
```

#### Significado de `u+s`

- **`u`**: Significa "user" (usuario), refiriéndose al propietario del archivo.
- **`+s`**: Indica que estamos estableciendo el bit SUID en el archivo.

Al listar de nuevo el binario con `ls -l`, veremos que ahora contiene una `s` en el grupo de propietarios, lo cual conlleva ciertos riesgos de seguridad.

#### Riesgos del SUID

1. **Escalada de Privilegios:** Si un programa con SUID tiene vulnerabilidades, un usuario malintencionado puede explotarlas para obtener privilegios de root, permitiéndoles realizar cualquier acción en el sistema.
    
2. **Ejecución de Código No Autorizado:** Un atacante puede usar un programa SUID vulnerable para ejecutar su propio código malicioso con permisos elevados, comprometiendo la seguridad del sistema.
    
3. **Acceso No Autorizado a Recursos:** Programas SUID pueden permitir el acceso no autorizado a archivos y recursos que normalmente estarían protegidos.
    

### Vulnerabilidad en `/usr/bin/pkexec`

`/usr/bin/pkexec` es una utilidad del paquete `polkit` que permite a un usuario ejecutar programas como otro usuario, típicamente root. En enero de 2022, se descubrió una vulnerabilidad crítica en `pkexec` (identificada como CVE-2021-4034) que permitió a los atacantes escalar sus privilegios a root en sistemas afectados.

#### Resumen de la Vulnerabilidad

1. **Descripción:** La vulnerabilidad en `pkexec` permitía a un usuario no privilegiado ejecutar código arbitrario como root debido a un error de manejo en los argumentos del programa.
    
2. **Explotación:** Al explotar esta vulnerabilidad, un atacante podía ejecutar comandos con privilegios de root sin necesidad de autenticación, comprometiendo completamente el sistema afectado.
    
3. **Impacto:** La explotación de esta vulnerabilidad permitió a los atacantes tener control total sobre el sistema, pudiendo instalar programas, modificar archivos, y crear nuevas cuentas con privilegios elevados.
    
4. **Mitigación:** Una vez descubierta, los desarrolladores de `polkit` lanzaron rápidamente parches para corregir la vulnerabilidad. Los administradores de sistemas fueron instados a actualizar sus paquetes de `polkit` inmediatamente para proteger sus sistemas.

/// Para identificar otros archivos con permisos SUID en el sistema, podemos utilizar el siguiente comando:

```typescript
find / -type f -perm -4000 2>/dev/null
```

Al ejecutarlo, veremos que el binario `python3.11` ahora tiene el permiso SUID (`s`). Si nos logueamos como otro usuario, como `sk8ware`, y ejecutamos el binario `python3.11`, lo estaríamos utilizando de manera privilegiada, ya que el binario posee el permiso SUID y está asociado al grupo **root**.

Desde el intérprete de Python, podemos realizar acciones privilegiadas, como importar la biblioteca `os` y utilizar `setuid` para cambiar nuestro identificador de usuario a `0`, que es el identificador de **root**. Si no se produce ningún error, significa que se nos ha permitido el acceso, y cualquier comando que ejecutemos, como `whoami`, se realizará con privilegios de **root**:

```python
import os   
os.setuid(0)  
os.system("whoami")  
os.system("id")  
os.system("bash")
```

----

### SGID

El concepto de SGID es similar al SUID, pero se aplica a nivel de grupo. Los archivos con permisos SGID ejecutan con los permisos del grupo al que pertenecen. Para encontrar estos archivos en el sistema, utilizamos:

```typescript
find / -type f -perm -2000 2>/dev/null
```

Podemos otorgar permisos SGID a un grupo utilizando:

```bash
chmod g+s /usr/bin/python3.11
```

O en notación octal `2775`:

```bash
chmod 2755 /usr/bin/python3.11
```

Para eliminar el permiso SGID, utilizamos:

```bash
chmod u-s /usr/bin/python3.11
```

y

```bash
chmod g-s /usr/bin/python3.11
```
