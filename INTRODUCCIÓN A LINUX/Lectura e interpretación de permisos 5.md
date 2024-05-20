


-----
- TAG: #LECTURA #INTERPRETACIÓN #PERMISOS
-----
Te dejo por aquí algunos materiales de apoyo por si quieres indagar más en los permisos de Linux:

- Permisos y derechos en Linux: [https://blog.desdelinux.net/permisos-y-derechos-en-linux/?msclkid=22f8cb88ba8111ecb5d8a3db91f066ab](https://blog.desdelinux.net/permisos-y-derechos-en-linux/?msclkid=22f8cb88ba8111ecb5d8a3db91f066ab)
- Permisos básicos en Linux: [https://www.profesionalreview.com/2017/01/28/permisos-basicos-linux-ubuntu-chmod/](https://www.profesionalreview.com/2017/01/28/permisos-basicos-linux-ubuntu-chmod/)
-----
## Touch y redirectores

Empezamos explicando un poco sobre los redirectores de la siguiente manera 
```
cd Desktop
touch file.txt
echo "probando" > file.txt  
```

Pero si volvemos a utilizar el mismo comando no nos va a permitir acumular la información, es decir abra un solo output cuando abramos el archivo `file`, para poder realizar un *apent* (apilar) y que no nos sobre escriba el archivo, solo debemos utilizar doble mayor `>>` 

## Nano 

Con nano podremos crear archivos en donde podremos agregar toda la información manualmente

## Vi

De inicio con vi tambien lo podemos crear hasta poderlo mejorar con **nvim** 

-----
Ahora que entendemos sobre la creación de archivos para ver los permisos que estos tienen 
Para ver permisos en linux lo podemos realizar de la siguiente manera  con `ls -l`
Y la estructura de permisos se estable de la siguiente manera 
### .rw-r--r--

Pero ah estos permisos siempre hay que distingirlos en tres partes

### .rw-|r--|r--

Todo se basa en 3 palabras en especifico `rwx` 
# R = Read
# W = Write 

# X = Executable

 |        rw-      |    r--     |    r--  |     sk8ware sk8ware | 
 
 | propietario | grupos | otros |    sk8ware sk8ware  |

Y para darnos cuenta quien es propietario o de grupo lo podemos ver en la parte derecha que sigue de los permisos, para ello siempre existe dos propietarios, el propietario quien fue quien creo el archivo y la parte de grupos, por ejemplo si existe otro usuario con nombre "alumnos" este podría tener los mismos privilegios el propietario, pero siempre con privilegio es el primer usuario 