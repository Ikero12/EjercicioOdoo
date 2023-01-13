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
