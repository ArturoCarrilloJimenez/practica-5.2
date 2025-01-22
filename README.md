# Despliegue de Wordpress con Docker Compose

## Instalación de Docker y Docker Compose

Para instalar Docker y Docker Compose en Ubuntu ejecutaremos los siguientes comandos:

⚠️** Nota:** Es importante tener en cuenta que estos comandos se han probado en una máquina virtual de AWS con Ubuntu 20.04.

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

