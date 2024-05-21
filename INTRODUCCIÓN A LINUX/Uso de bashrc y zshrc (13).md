
----
- TAG: #BASHRC #ZSHRC
-----
En mi caso yo opero con una ZSH, por tanto mi archivo de configuración corresponde al ‘~/.**zshrc**‘. Recuerda que en caso de usar una BASH tu archivo de configuración debería estar situado en ‘**~/.bashrc**‘

Por aquí te dejo algunos enlaces de interés por si quieres entender un poco mejor para qué sirven estos archivos:

- ¿Qué es Bashrc en Linux?: [https://www.compuhoy.com/que-es-bashrc-en-linux/](https://www.compuhoy.com/que-es-bashrc-en-linux/)
- ¿Por qué deberías usar ZSH?: [https://respontodo.com/que-es-zsh-y-por-que-deberia-usarlo-en-lugar-de-bash/](https://respontodo.com/que-es-zsh-y-por-que-deberia-usarlo-en-lugar-de-bash/)

Mi recomendación personal es que utilicéis ZSH en vez de BASH, desde que investiguéis un poco diferencias entre ambas entenderéis por qué merece la pena.

----
Empezamos listando directorios ocultos con 
```
ls -la
```

`a` = Permite mostrar directorios ocultos que empiecen con `.` 
`.` = Nos permite crear directorios ocultos

```zsh
mkdir .prueba
```

Buenos nosotros como utilizamos una `zsh` como tipo del `shell`, lo cual lo podemos ver con 
```
echo $SHELL
```

Asi que podemos econtrar nuestro archivo `.zshrc` en nuestra ruta personal de usuario
Vamos crear una función de ejemplo para que puedan integrar en su **.zshrc** y agregar las funciones que quieran, por ejemplo si queremos crear una función que nos muestre nuestra dirección ip privada podemos hacer lo siguiente:
```
hostname -I | awk '{print $1}'
```

Esta función nos permite filtrar solo por la primera dirección ip o tenemos otra forma de hacerlo con `cut`
```
hostname -I | cut -d ' ' -f 1
```
`-d` = Delimitador del espacio 
`' '` = Espacio entre las direcciones ip 
`-f` = Fead (campo)
`1` = Campo 1 

Ahora si queremos mostrar la dirección ip por consola con un mensaje lo podemos realizar de la siguiente manera
```zsh
echo "Tu dirección ip es: $(hostname -I | awk '{print $1}')"
```
Ya que si le agregamos el signo `$` antes del `()` podemos hacer que nos imprima esa cadena despues del `echo` 

Ahora para que puedan entender para que sirve el `.zshrc` nos podemos copiar el codigo de arriba
Y al final de todo podemos agregar la nueva función 
```bash
function vermiip(){
      echo "Tu dirección ip es: $(hostname -I | awk '{print $1}')"
}
```

Ahora si guardamos y volvemos a cargar veremos que si escribimos `vermiip` nos mostrara que si funciona al darnos la respuesta en la terminal 

Y ahora podemos hacer lo que se les de la gana creando funciones ;)
