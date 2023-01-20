# EjercicioOdoo

## Ps - servicios

Con el comando **ps** podemos ver todos los servicios activos incluido el propio comando.
Existen varias formas de ampliar dicha información como puede ser

```bash
 ps -aux
 ```
*Muestra todos los servicios, cuando se iniciaron,cuanto tiempo llevan activos ,el estado,el PID y el usuario que los inicio*

## netstat - conexiones que escuchan, esperan o establecidas
Este comando **netstat** permite ver todas las conexiones activas aunque, con ciertas modificaciones, podemos ver más información como puede ser:

```bash
 netstat -pt
 ```
 *Muestra todas las conexiones establecias con el nombre y PID incluido*
 
 ---
 
```bash
 netstat -putan
 ```
 *Muestra todas las conexiones establecidas y además las que están escuchando*
 
 ---
 
 También podemos buscar directamente el puerto y ver que conexiones están entrando, saliendo o esperando:
 ```bash
 netstat -putan | grep *puerto*
 ```
 
 ---

## service *nombreservicio* (start,stop)- Inicializar un servicio o pararlo 
El comando **service** inicia o para un servicio que nosotros le indiquemos.
Cabe destacar que dentro de un contenedor de Docker, el comando "service stop" no funciona. Es necesario usas docker-compose up y down o start y stop.

```bash
 service *nombre* (start o stop)
 ```
 
---

## ¿Que ocurre si en el ordenador local el puerto 5432 está ocupado?
Existe una pequeña probabilidad de que justo el puerto que uno quiera esté ocupado. Si se da el caso, el servicio que queramos iniciar no dejará de primera mano que arranque nada lo cual supone un problema.


Para ello disponemos de varias opciones para solucionarlo.
1. Parar el servicio que esté ocupando el susodicho puerto.
2. Puentear el puerto hacia otro.

---
## Docker-Compose
```
version: '3.1'
services:
  db:
    image: postgres:13
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=odoo
      - POSTGRES_USER=odoo
    ports:
      - "5430:5432"
    volumes:
      - dam22_odooklk:/var/lib/postgresql/data

 ```
En el Docker-Compose tenemos la parte de la base de datos. Se definen los datos del superusuario, la imagen y los puertos. Además añadimos un volumen personalizado.

```
odoo:
    image: odoo:14.0
    container_name: dam22_odooklk
    ports:
      - "8069:8069"
    depends_on:
      - db
volumes:
  dam22_odooklk:
```
La parte de la página de ventas contiene la imagen, el nombre del contenedor en cuestión, los puertos que va a usar y al final el volumen donde se va a guardar.

Además de todo lo normal y típico, tenemos un añadido nuevo, el "depends_on". Este sirve para que la aplicación no se ejecute en ningún caso antes de que la base de datos esté lanzada. Así nos aseguramos de que no falle por ningún lado ni haya fallos inesperados.


## Conectar la base de datos a pycharm

![Conexion](https://github.com/Ikero12/Imagenes/blob/main/Captura%20desde%202023-01-20%2012-21-40.png)


## Aplicación de Odoo funcionando

![Aplicacion](https://github.com/Ikero12/Imagenes/blob/main/Captura%20desde%202023-01-20%2012-25-54.png)





