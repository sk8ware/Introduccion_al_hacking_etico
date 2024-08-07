
---
- TAG: #CAPABILITIES #PRIVILEGIOS #ESPECIALES 
- ----
>Te recomiendo el siguiente recurso en caso de que quieras investigar un poco más acerca de las Capabilities:

- ¿Qué son las Linux Capabilities?: [http://www.etl.it.uc3m.es/Linux_Capabilities](http://www.etl.it.uc3m.es/Linux_Capabilities)
---
### ¿Qué son las Capabilities?

En Linux, las "capabilities" (capacidades) son una forma de dividir los privilegios del superusuario (root) en partes más pequeñas que pueden ser asignadas a procesos individuales. Esto permite que los programas puedan realizar ciertas operaciones privilegiadas sin necesidad de tener acceso completo como root, mejorando así la seguridad del sistema.

### Ejemplo Práctico con Python

Si empezamos viendo los permisos de `python3.11`, observamos que no tiene permisos _suid_, pero pertenece al grupo de **root**. Si intentamos usar un intérprete de Python y nos tratamos de loguear como root, no podremos hacerlo. Para ello, debemos asignarle unos permisos específicos para que pueda usar la siguiente función:

```bash
which python3.11 | xargs ls -l
```

```python
import os os.setuid(0)
```

### Listar las Capabilities del Sistema

Tenemos una herramienta en consola que nos permite listar las capabilities del sistema:

```bash
getcap -r / 2>/dev/null
```

Este comando nos mostrará un listado de todas las capabilities de nuestro sistema. Aquí es donde deberíamos agregarle a `python3.11` la capacidad necesaria para que podamos tener acceso al usuario **root** desde el intérprete de Python.

### Asignar Capabilities

Para ello, debemos loguearnos como **root** y ejecutar el siguiente comando:

```bash
setcap cap_setuid+ep /usr/bin/python3.11
```

Podemos verificar que la capacidad se ha asignado correctamente con:

```bash
getcap /usr/bin/python3.11
```

### Quitar Capabilities

Cabe recalcar que existen muchos tipos de capabilities. Para quitar una capability, debemos usar el siguiente comando:

```bash
setcap -r /usr/bin/python3.11
```

Luego, verificamos que ya no tenga la capability con:

```bash
getcap /usr/bin/python3.11
```

---

### Recursos Adicionales

> Tenemos el siguiente recurso para buscar las **capabilities** de algunos binarios en la siguiente página:
> 
> - [GTFOBins](https://gtfobins.github.io/)