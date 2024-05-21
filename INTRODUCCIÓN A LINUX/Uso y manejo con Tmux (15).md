
----
- TAG: #MANEJO #TMUX 
----
>Para tener todos los atajos y comandos de Tmux centralizados, hemos creado la siguiente guía la cual esperamos que le puedas sacar provecho:

- Guía de atajos y comandos de Tmux: [https://hack4u.io/wp-content/uploads/2022/05/Tmux-Cheat-Sheet.pdf](https://hack4u.io/wp-content/uploads/2022/05/Tmux-Cheat-Sheet.pdf)
-----
# Uso de tmux: Guía Básica

## Instalación de tmux

Para empezar, debemos asegurarnos de tener instalada la aplicación tmux en nuestro sistema. Si no la tienen, pueden instalarla fácilmente con:

```bash
sudo apt install tmux
```

O buscarla con:

```bash
apt search tmux
```

Si surge un error al abrir tmux por primera vez, pueden solucionarlo ejecutando:

```bash
touch ~/.hushlogin
```

## Personalización de tmux con Oh My Tmux

Por lo general, tmux viene con un diseño predeterminado que podemos modificar utilizando [Oh My Tmux](https://github.com/gpakosz/.tmux). Este repositorio de GitHub proporciona instrucciones claras para usuarios tanto regulares como root.

En caso de que la configuración no se aplique a un usuario no privilegiado, pueden usar:

```bash
tmux kill-server
```

y luego repetir los pasos indicados en el repositorio de GitHub.

## Comandos Básicos de tmux

### Crear y Manejar Sesiones

El número que aparece a la izquierda es el número de sesión, que por defecto es `0`. Para crear una nueva sesión con un nombre específico, pueden usar:

```bash
tmux new -s Academia
```

Si ya están dentro de tmux, pueden crear una nueva sesión con:

```css
Ctrl + b (sueltas) + Shift + 4
```

### Renombrar Ventanas

Una vez dentro de tmux, pueden renombrar la ventana actual con:

```css
Ctrl + b (sueltas) + ,
```

### Crear y Navegar Entre Ventanas

Para crear una nueva ventana, usen:

```css
Ctrl + b (sueltas) + c
```

Luego, pueden renombrar la ventana usando el mismo comando para renombrar.

Para moverse entre ventanas:

```css
Ctrl + b (sueltas) + 1
```

Activen el control de mouse en tmux con:

```css
Ctrl + b (sueltas) + m
```

### Dividir la Pantalla

Para abrir una ventana debajo y poder maniobrar en doble pantalla:

```css
Ctrl + b (sueltas) + Shift + 2
```

Para dividirla de forma lateral:

```css
Ctrl + b (sueltas) + Shift + 5
```

Para maniobrar entre ventanas:

```css
Ctrl + b (sueltas) + o
```
o con las flechas de dirección.

### Cerrar Ventanas

Para cerrar una ventana, pueden usar:

```bash
exit
```

o:

```css
Ctrl + b (sueltas) + x
```

### Ajustar el Tamaño de las Ventanas

Para ajustar el tamaño de las ventanas, salgan al modo mouse con:

```css
Ctrl + b (sueltas) + m
```

O mantengan presionado `Ctrl` mientras usan las teclas de dirección.

## Copiar y Pegar en tmux

Para copiar y pegar texto de manera eficiente en tmux:

1. Para copiar:
    
    - Hagan `cat /etc/hosts`
    - Copien con `Ctrl + Shift + c`
    - Peguen con `Ctrl + Shift + v`
2. Alternativamente, usen:
    
    - `Ctrl + b (sueltas) + Shift + [`
    - Naveguen por las líneas para seleccionar lo que desean copiar con `Ctrl + espacio`
    - Copien al portapapeles con `Alt + w`
3. Para pegar:
    
    - `Ctrl + b (sueltas) + Shift + ]`

## Uso de tmux con Procesos en Segundo Plano

tmux es especialmente útil para manejar varios procesos en segundo plano. Para hacer un detach y cerrar la ventana:

```css
Ctrl + b (sueltas) + d
```

Para ver las sesiones abiertas:

```bash
tmux list-sessions
```

Para reconectarse a una sesión:

```bash
tmux attach
```

(si solo hay una sesión) o:

```bash
tmux attach -t Academia
```

(si es una sesión específica).

Para migrar entre sesiones si tienen más de dos:

```css
Ctrl + b (sueltas) + w
```
