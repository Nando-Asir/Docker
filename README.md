🐳 Docker - Guía Completa
Este repositorio contiene una guía completa para instalar, configurar y utilizar Docker en sistemas basados en Debian y Ubuntu. Docker es una plataforma de contenedores que permite empaquetar aplicaciones y sus dependencias en entornos aislados, facilitando su despliegue y ejecución en diferentes sistemas.

📋 Tabla de Contenidos
Instalación
En Debian
En Ubuntu
Uso Básico
Manejo de Contenedores
Tabla de Comandos Útiles
Consejos y Buenas Prácticas
Recursos Adicionales
Instalación
En Debian
Para instalar Docker en Debian, sigue estos pasos:

Actualizar el sistema :
bash


1
sudo apt update && sudo apt upgrade -y
Instalar dependencias necesarias :
bash


1
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
Agregar la clave GPG oficial de Docker :
bash


1
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
Agregar el repositorio de Docker :
bash


1
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
Actualizar los índices de paquetes e instalar Docker :
bash


1
2
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
Verificar la instalación :
bash


1
sudo docker --version
(Opcional) Agregar tu usuario al grupo docker :
bash


1
sudo usermod -aG docker $USER
Luego, reinicia tu sesión para aplicar los cambios.
En Ubuntu
Para instalar Docker en Ubuntu, sigue estos pasos:

Actualizar el sistema :
bash


1
sudo apt update && sudo apt upgrade -y
Instalar dependencias necesarias :
bash


1
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
Agregar la clave GPG oficial de Docker :
bash


1
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
Agregar el repositorio de Docker :
bash


1
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
Actualizar los índices de paquetes e instalar Docker :
bash


1
2
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
Verificar la instalación :
bash


1
sudo docker --version
(Opcional) Agregar tu usuario al grupo docker :
bash


1
sudo usermod -aG docker $USER
Luego, reinicia tu sesión para aplicar los cambios.
Uso Básico
Descargar una imagen desde Docker Hub :
bash


1
docker pull <nombre-de-la-imagen>
Ejecutar un contenedor :
bash


1
docker run <nombre-de-la-imagen>
Ejecutar un contenedor en segundo plano (detached mode) :
bash


1
docker run -d <nombre-de-la-imagen>
Listar contenedores en ejecución :
bash


1
docker ps
Listar todos los contenedores (incluidos los detenidos) :
bash


1
docker ps -a
Detener un contenedor :
bash


1
docker stop <id-o-nombre-del-contenedor>
Eliminar un contenedor :
bash


1
docker rm <id-o-nombre-del-contenedor>
Eliminar una imagen :
bash


1
docker rmi <id-o-nombre-de-la-imagen>
Manejo de Contenedores
Crear una red personalizada
bash


1
docker network create <nombre-de-la-red>
Conectar un contenedor a una red específica
bash


1
docker run --network=<nombre-de-la-red> <nombre-de-la-imagen>
Inspeccionar un contenedor
bash


1
docker inspect <id-o-nombre-del-contenedor>
Ver los logs de un contenedor
bash


1
docker logs <id-o-nombre-del-contenedor>
Ejecutar un comando dentro de un contenedor en ejecución
bash


1
docker exec -it <id-o-nombre-del-contenedor> <comando>
Tabla de Comandos Útiles
docker pull <imagen>
Descarga una imagen desde Docker Hub.
docker run <imagen>
Crea y ejecuta un contenedor a partir de una imagen.
docker ps
Lista los contenedores en ejecución.
docker ps -a
Lista todos los contenedores (incluidos detenidos).
docker stop <contenedor>
Detiene un contenedor en ejecución.
docker rm <contenedor>
Elimina un contenedor.
docker rmi <imagen>
Elimina una imagen.
docker images
Lista las imágenes disponibles localmente.
docker exec -it <contenedor> bash
Accede al shell de un contenedor en ejecución.
docker logs <contenedor>
Muestra los logs de un contenedor.
docker network create <red>
Crea una red personalizada.
docker inspect <contenedor>
Muestra información detallada de un contenedor.

Consejos y Buenas Prácticas
Usa nombres descriptivos para tus contenedores : Esto facilita su identificación.
bash


1
docker run --name mi-aplicacion <imagen>
Limpia recursos innecesarios : Elimina contenedores e imágenes no utilizados para liberar espacio.
bash


1
docker system prune -a
Usa Docker Compose para aplicaciones multi-contenedor : Facilita la gestión de servicios interdependientes.
yaml


1
2
3
4
5
6
⌄
⌄
⌄
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
Monta volúmenes para persistir datos : Evita perder datos cuando un contenedor se detenga o elimine.
bash


1
docker run -v /ruta/local:/ruta/contenedor <imagen>
Recursos Adicionales
Docker Documentation
Docker Hub
Docker Compose
Best Practices for Writing Dockerfiles
Si tienes alguna pregunta o sugerencia, no dudes en abrir un issue en este repositorio. ¡Gracias por usar Docker! 🐳
