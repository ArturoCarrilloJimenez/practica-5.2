# Despliegue de Wordpress con Docker Compose

En esta práctica desplegaremos un servicio de Wordpress con Docker Compose, utilizando un servicio de MySQL, PhpMyAdmin y https-portal para proteger los servicios con SSL.

## Indice

1. [Instalación de Docker y Docker Compose](#instalación-de-docker-y-docker-compose)
2. [Despliegue de Wordpress](#despliegue-de-wordpress)


## Instalación de Docker y Docker Compose

Para instalar Docker y Docker Compose en Ubuntu ejecutaremos los siguientes comandos:

1. Actualizamos el sistema

```bash
sudo apt update
```

2. Instalamos Docker y Docker Compose

```bash
sudo apt install docker.io docker-compose -y
```

3. Añadimos el usuario al grupo de Docker para poder ejecutar comandos sin necesidad de ser root

```bash
sudo usermod -aG docker ubuntu
```

4. Cerramos la sesión y volvemos a iniciarla para que los cambios surtan efecto

```bash
newgrp docker
```

De esta forma ya tendremos instalado Docker y Docker Compose en nuestro sistema para poder desplegar Wordpress a continuación.

## Despliegue de Wordpress

Para el despliegue de Wordpress con Docker Compose, crearemos un archivo `docker-compose.yml` con el siguiente servicios:

### Servicio de MySQL

Para el servicio de MySQL, utilizaremos la imagen oficial de MySQL y configuraremos las variables de entorno para el usuario, contraseña y base de datos.

```yaml
environment:
  - MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_PASSWORD}
  - MYSQL_DATABASE=${MYSQL_DATABASE}
  - MYSQL_USER=${MYSQL_USER}
  - MYSQL_PASSWORD=${MYSQL_PASSWORD}
```

### Servicio de Wordpress

Para el servicio de Wordpress, utilizaremos la imagen de bitnami/wordpress y configuraremos las variables de entorno para la base de datos, usuario y contraseña.

```yaml
environment:
  - WORDPRESS_USERNAME=${WORDPRESS_USERNAME}
  - WORDPRESS_PASSWORD=${WORDPRESS_PASSWORD}
  - WORDPRESS_EMAIL=${WORDPRESS_EMAIL}
  - WORDPRESS_BLOG_NAME=${WORDPRESS_BLOG_NAME}
  - WORDPRESS_DATABASE_HOST=${MYSQL_HOST}
  - WORDPRESS_DATABASE_NAME=${MYSQL_DATABASE}
  - WORDPRESS_DATABASE_USER=${MYSQL_USER}
  - WORDPRESS_DATABASE_PASSWORD=${MYSQL_PASSWORD}
```

### Servicio de PhpMyAdmin

Para el servicio de PhpMyAdmin, utilizaremos la imagen oficial de PhpMyAdmin y lo configuraremos para poder conctar con distintos servicios de MySQL.

```yaml
environment:
  - PMA_ARBITRARY=1
```

### Servicio de https-portal

Para el servicio de https-portal, utilizaremos la imagen de steveltn/https-portal y configuraremos los dominios que queremos proteger con SSL.

Con este servicio, podremos proteger los servicios de Wordpress y PhpMyAdmin para que tengas un certificado y puedan ser accedidos por HTTPS.

````yaml
environment:
      DOMAINS: "${DOMAIN} -> http://wordpress:8080"
      STAGE: "production"
````

### Resultado

![wordpress](./Captura%20de%20pantalla%202025-01-27%20195419.png)