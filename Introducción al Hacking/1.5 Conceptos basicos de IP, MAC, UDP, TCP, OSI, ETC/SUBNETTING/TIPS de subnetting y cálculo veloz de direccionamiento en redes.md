
--- 
- TAG : #TIPS #CALCULO-DE-RED
----
`10.18.51.23/23` IP y /23 corresponde a los 23 primeros bits de la mascara de red

00001010.00010010.00110011.00010111 (10.18.51.23) **En esta parte observamos la IP en binario y decimal**

- `echo “obase=2;10” | bc` **(este comando nos devuelve el decimal en binario en la terminal)**

11111111.11111111.11111110.00000000 (255.255. 254.0) **Mascara de red Network Mask**

- `echo “ibase=2;11111110” | bc`  
    (este comando nos devuelve el binario en decimal)

00001010.00010010.00110010.00000000 (10.18.50.0 Network ID)

- Para sacar el Network ID es necesario validar los valores que coincidan en 1 entre los binarios de la IP y Network Mask, si no coincide el valor es 0 pero si coinciden el valor es 1.

Si tenemos 23 bits de los 32 nos quedarian 9 hosts a la izquierda contando desde la derecha los bits

Cogemos la IP y la transformamos

00001010.00010010.00110011.11111111 (10.18.51.255 Broadcast Adress)

- IP CALCULATOR: [https://blog.jodies.de/ipcalc](https://blog.jodies.de/ipcalc)