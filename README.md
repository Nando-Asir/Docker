# 🐳 Docker - Guía Completa de Instalación y Uso

![Docker](https://img.shields.io/badge/docker-ready-blue?logo=docker)
![Ubuntu Compatible](https://img.shields.io/badge/ubuntu-20.04%2B-orange?logo=ubuntu)
![Debian Compatible](https://img.shields.io/badge/debian-11%2B-red?logo=debian)
![License: MIT](https://img.shields.io/badge/license-MIT-green)

---

## 📚 Índice
- [🚀 Introducción](#-introducción)
- [🔧 Instalación de Docker](#-instalación-de-docker)
- [🏁 Primeros pasos](#-primeros-pasos)
- [📦 Manejo de contenedores](#-manejo-de-contenedores)
- [🛠️ Volúmenes y Redes](#-volúmenes-y-redes)
- [🔨 Construcción de Imágenes](#-construcción-de-imágenes)
- [🔨 Docker Compose](#-docker-compose)
- [🔨 Terminal y Comandos Rápidos](#-terminal-y-comandos-rápidos)
- [🔨 Mantenimiento y Limpieza](#-mantenimiento-y-limpieza)
- [🌐 Recursos adicionales](#-recursos-adicionales)

---

## 🚀 Introducción

Esta guía enseña cómo instalar y usar **Docker** en **Debian** o **Ubuntu** de forma sencilla. Docker permite empaquetar aplicaciones y sus dependencias dentro de **contenedores ligeros**.

---

## 🔧 Instalación de Docker

### 1. Eliminar versiones antiguas
```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```

### 2. Actualizar repositorios
```bash
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release
```

### 3. Añadir clave GPG oficial
```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

### 4. Configurar el repositorio
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
> 💡 **Nota:** Si usas Debian, reemplaza `ubuntu` por `debian` en la URL.

### 5. Instalar Docker
```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### 6. Verificar instalación
```bash
docker --version
docker compose version
```

---

## 🏁 Primeros pasos

- **Estado de Docker:**
  ```bash
  sudo systemctl status docker
  ```

- **Iniciar Docker:**
  ```bash
  sudo systemctl start docker
  ```

- **Habilitar al arranque:**
  ```bash
  sudo systemctl enable docker
  ```

- **Usar Docker sin sudo:**
  ```bash
  sudo usermod -aG docker $USER
  newgrp docker
  ```

---

## 📦 Manejo de contenedores

### Comandos básicos:

| Acción | Comando |
|:-------|:--------|
| Buscar imagen | `docker search <nombre ID>` |
| Descargar imagen | `docker pull <nombre ID>` |
| Ver imágenes descargadas | `docker images` |
| Ejecutar contenedor | `docker run -d -p 8080:80 <nombre ID>` |
| Ejecutar con comando | `docker run -it <nombre ID> /bin/bash` |
| Crear un contenedor y muestra una carpeta con-w | `docker run -it -w <carpeta> <nombre ID> <comando>` |
| Listar contenedores activos | `docker ps` |
| Listar todos los contenedores | `docker ps -a` |
| Detener un contenedor | `docker stop <nombre ID>` |
| Reiniciar contenedor | `docker restart <nombre ID>` |
| Eliminar contenedor | `docker rm <nombre ID>` |
| Eliminar imagen | `docker rmi <imagen>` |
| Ver logs de contenedor | `docker logs <nombre ID>` |
| Inspeccionar contenedor | `docker inspect <nombre ID>` |

### Ejemplo: correr un servidor Nginx
```bash
docker run -d --name webserver -p 8080:80 nginx
```

---

## 🛠️ Volúmenes y Redes

### Volúmenes:
- Crear volumen:
  ```bash
  docker volume create datos_app
  ```
- Listar volúmenes:
  ```bash
  docker volume ls
  ```
- Usar volumen en contenedor:
  ```bash
  docker run -d -v datos_app:/app/data nginx
  ```

### Redes:
- Crear red personalizada:
  ```bash
  docker network create mi_red
  ```
- Ejecutar contenedor en una red:
  ```bash
  docker run -d --network mi_red nginx
  ```
- Listar redes:
  ```bash
  docker network ls
  ```

---

## 🔨 Construcción de Imágenes

- Crear un `Dockerfile`:

```Dockerfile
FROM ubuntu:latest
RUN apt-get update && apt-get install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

- Construir imagen personalizada:
```bash
docker build -t mi-nginx .
```

- Ejecutar imagen creada:
```bash
docker run -d -p 8080:80 mi-nginx
```

---

## 🔨 Docker Compose

- Ejemplo básico `docker-compose.yml`:

```yaml
version: "3.9"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

- Levantar servicios:
```bash
docker compose up -d
```

- Apagar servicios:
```bash
docker compose down
```

---

## 🔨 Terminal y Comandos Rápidos

| Acción | Comando |
|:--------|:--------|
| Crear y levantar contenedor en segundo plano | `docker run -d --name miapp alpine sleep 3600` |
| Ver detalles de un contenedor | `docker inspect miapp` |
| Obtener IP de un contenedor | `docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' miapp` |
| Ejecutar terminal interactiva | `docker exec -it miapp sh` |
| Crear imagen desde contenedor | `docker commit miapp miapp_backup` |
| Crear red bridge personalizada | `docker network create --driver bridge midockerred` |
| Conectar contenedor a otra red | `docker network connect midockerred miapp` |
| Desconectar contenedor de red | `docker network disconnect bridge miapp` |
| Crear volumen persistente | `docker volume create volumen_app` |
| Montar volumen en run | `docker run -d -v volumen_app:/datos nginx` |

---

## 🔨 Mantenimiento y Limpieza

| Acción | Comando |
|:--------|:--------|
| Ver espacio usado | `docker system df` |
| Eliminar contenedores parados | `docker container prune` |
| Eliminar imágenes no usadas | `docker image prune` |
| Eliminar todo lo no usado | `docker system prune -a` |

**Ejemplo para liberar espacio:**
```bash
docker system prune -a --volumes
```

---

## 🌐 Recursos adicionales

- [📘 Documentación oficial Docker](https://docs.docker.com/)
- [🔗 Comandos Docker CLI](https://docs.docker.com/engine/reference/commandline/docker/)
- [🔍 Guía interactiva de Docker para principiantes](https://docker-curriculum.com/)

---

> ✨ Autor: [Nando-Asir](https://github.com/Nando-Asir)  
> 🛡️ Licencia: MIT

---

