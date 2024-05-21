

----
- TAG: #OCTAL #NOTACIÓN #PERMISOS 
--------
>Te dejo a continuación algunos enlaces de interés para que puedas reforzar lo aprendido:

- Permisos del sistema de archivos GNU/Linux: [https://blog.alcancelibre.org/staticpages/index.php/permisos-sistema-de-archivos](https://blog.alcancelibre.org/staticpages/index.php/permisos-sistema-de-archivos)
-----

## Asignación de Permisos: Notación Octal

### Creación de Directorio y Propietario

Primero, creamos un directorio llamado `testing` y asignamos el propietario y grupo como **root**.

### Notación Octal de Permisos

La notación octal es una forma eficiente y común de representar los permisos en sistemas Unix/Linux. Cada permiso se puede representar mediante un número binario y luego convertirlo a su equivalente decimal.

#### Conversión de Permisos Simbólicos a Binarios y Decimales

Cada letra en los permisos representa un `1`, y cada espacio vacío representa un `0`. Aquí se muestra cómo transformar esto de binario a decimal:

| Simbólico | Binario | Decimal |
| --------- | ------- | ------- |
| rwx       | 111     | 7       |
| r-x       | 101     | 5       |
| r-x       | 101     | 5       |

Para convertir de binario a decimal, recordemos que se cuenta de derecha a izquierda, comenzando desde `2^0`. Por ejemplo, para `101`:

- 20=120=1 (posición 1, desde la derecha)
- 22=422=4 (posición 3, desde la derecha)

Sumamos estas posiciones: 1+4=51+4=5.

Haciendo esto para cada conjunto de permisos, obtenemos:

- `rwx` = 7
- `r-x` = 5
- `r-x` = 5

Esto nos da el número octal `755`.

### Asignación de Permisos con `chmod`

Para asignar estos permisos, usamos el comando `chmod`:

```sh
chmod 755 testing
```

Esto cambiará los permisos del directorio `testing` a `rwxr-xr-x`.

### Ejemplo de Cambio de Permisos

Si queremos modificar los permisos a `r-xr---w-`, calculamos el número octal de la misma manera:

| Simbólico | Binario | Decimal |
| --------- | ------- | ------- |
| r-x       | 101     | 5       |
| r--       | 100     | 4       |
| --w       | 010     | 2       |

Esto da como resultado el número octal `542`. Para aplicarlo, usamos:

```sh
chmod 542 testing
```

### Truco para Calcular Permisos

Un truco útil para recordar los valores es usar los números `421`, que corresponden a los permisos `rwx`.

| Simbólico | Binario | Decimal |
| --------- | ------- | ------- |
| rwx       | 111     | 7       |
| r-x       | 101     | 5       |
| --x       | 001     | 1       |

Por ejemplo, para `rwxr-xr-x`:

| Simbólico | Suma de Valores |
| --------- | --------------- |
| rwx       | 4 + 2 + 1 = 7   |
| r-x       | 4 + 0 + 1 = 5   |
| r-x       | 4 + 0 + 1 = 5   |

Esto nos da `755` de nuevo.

---


