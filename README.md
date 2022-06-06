# **Docker compose with MySql and Wordpress**

## **Presentación:**

Actividad propuesta por @maximofernandezriera, profesor de la asignatura de Sistemas informáticos del curso DAW dual.

## **Enunciado:**

> Siguiendo el videotutorial propuesto de un creador de contenido  de habla hispana,que se está especializando en Docker, utilizando docker compose deberéis gestionar una configuración de wordpress y mysql. Para empezar debemos saber que con docker compose podemos manejar fácilmente las configuraciones de varios contenedores.
> 
> *Link:* https://www.youtube.com/watch?v=eoFxMaeB9H4

---


## **¿Qué es Docker Compose?**

*Compose* una herramienta para definir y ejecutar aplicaciones Docker de varios contenedores. Con Compose, utiliza un archivo YAML para configurar los servicios de su aplicación. Luego, con un solo comando, crea e inicia todos los servicios desde su configuración. Para obtener más información sobre todas las funciones de Compose, consulte la lista de funciones.

Y funciona en todos los entornos: producción, puesta en escena, desarrollo, pruebas, así como flujos de trabajo de CI.


---

## **Procedimiento:**

*Nota:* instalando `Docker Desktop` podemos disfrutar directamente de docker compose.

### 1. **Descargamos la imágen de mysql**

```docker
docker run -e MYSQL_ROOT_PASSWORD=12345 -d mysql:8.0.13

```

Al ser la primera vez, nos descargará la imagen de mysql desde DockerHub, en caso contrario directamente ejecutará la que ya tenemos instalada. 

![](resources/1mysql-image.png)


### 1. **Creamos el archivo `docker-compose.yml`**

En este archivo definiremos los servicios que componen nuestra aplicación para que puedan ejecutarse juntos en un entorno aislado. 

A continuación os muestro un ejemplo del archivo `.yml`  aplicado a esta actividad. También se puede encontrar una plantilla predefinida para wordpress en el DockerHub.

```dockerfile
version: '3.1'  #aquí se especifíca la versión del dockerCompose

services: # esta sección sirve para añadir las imágenes o otros servicios que vamos a usar 

  wordpress:
    image: wordpress
    restart: always
    ports:
      - 8080:80 # especificamos el puerto local que vamos a usar.
    environment: # configuración para wordpress. Fuente -> dockerHub
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: usuario
      WORDPRESS_DB_PASSWORD: constraseña
      WORDPRESS_DB_NAME: db

  db: #configuración para mysql. Fuente -> dockerHub
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: db
      MYSQL_USER: usuario
      MYSQL_PASSWORD: contraseña
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
```

### 2. **Ejecutamos el docker compose:**

Dentro de la carpeta del proyecto mediante el siguiente comando:
```powershell-interactive
docker-compose up
```




### 3. **Comprobación:**

Tras la correcta instalación, por último, visitamos al [localhost](http://localhost:8080/wp-admin/install.php) que hemos indicado en la configuración.
