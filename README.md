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
- [🧰 Tabla de comandos útiles](#-tabla-de-comandos-útiles)
- [📄 Instalación de Docker Compose (opcional)](#-instalación-de-docker-compose-opcional)
- [🛠️ Solución de problemas](#️-solución-de-problemas)
- [🌐 Recursos adicionales](#-recursos-adicionales)

---

## 🚀 Introducción

Esta guía enseña cómo instalar y usar **Docker** en **Debian** o **Ubuntu** de forma rápida y práctica.  
Docker permite crear, desplegar y gestionar aplicaciones mediante **contenedores**.

---

## 🔧 Instalación de Docker

### 1. Eliminar versiones antiguas
\`\`\`bash
sudo apt-get remove docker docker-engine docker.io containerd runc
\`\`\`

### 2. Actualizar repositorios
\`\`\`bash
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release
\`\`\`

### 3. Añadir la clave GPG oficial
\`\`\`bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
\`\`\`

### 4. Configurar el repositorio
\`\`\`bash
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu   $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
\`\`\`
> 💡 **Nota:** Si usas Debian, reemplaza \`ubuntu\` por \`debian\` en la URL.

### 5. Instalar Docker Engine
\`\`\`bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
\`\`\`

### 6. Verificar la instalación
\`\`\`bash
docker --version
\`\`\`

---

## 🏁 Primeros pasos

- **Comprobar estado de Docker:**
  \`\`\`bash
  sudo systemctl status docker
  \`\`\`

- **Iniciar Docker (si no está en ejecución):**
  \`\`\`bash
  sudo systemctl start docker
  \`\`\`

---

## 📦 Manejo de contenedores

### Acciones comunes:

- **Buscar una imagen:**
  \`\`\`bash
  docker search nginx
  \`\`\`

- **Descargar una imagen:**
  \`\`\`bash
  docker pull nginx
  \`\`\`

- **Ejecutar un contenedor:**
  \`\`\`bash
  docker run -d -p 8080:80 nginx
  \`\`\`

- **Listar contenedores en ejecución:**
  \`\`\`bash
  docker ps
  \`\`\`

- **Listar todos los contenedores (activos y detenidos):**
  \`\`\`bash
  docker ps -a
  \`\`\`

- **Detener un contenedor:**
  \`\`\`bash
  docker stop <ID o nombre>
  \`\`\`

- **Eliminar un contenedor:**
  \`\`\`bash
  docker rm <ID o nombre>
  \`\`\`

- **Ver logs de un contenedor:**
  \`\`\`bash
  docker logs <ID o nombre>
  \`\`\`

---

## 🧰 Tabla de comandos útiles

| Acción | Comando |
|:-------|:--------|
| Ver versión de Docker | \`docker --version\` |
| Ver imágenes disponibles | \`docker images\` |
| Eliminar una imagen | \`docker rmi <imagen>\` |
| Inspeccionar un contenedor | \`docker inspect <nombre>\` |
| Mostrar estadísticas de contenedores | \`docker stats\` |

---

## 📄 Instalación de Docker Compose (opcional)

### Instalar Docker Compose:
\`\`\`bash
sudo apt-get install docker-compose-plugin
\`\`\`

### Verificar instalación:
\`\`\`bash
docker compose version
\`\`\`

### Ejemplo básico de \`docker-compose.yml\`
\`\`\`yaml
version: "3.9"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
\`\`\`

Para levantar los servicios:
\`\`\`bash
docker compose up -d
\`\`\`

Para detenerlos:
\`\`\`bash
docker compose down
\`\`\`

---

## 🛠️ Solución de problemas

- **Docker no arranca**:
  \`\`\`bash
  sudo systemctl start docker
  \`\`\`

- **Problemas de permisos ("Permission denied"):**
  Añadir tu usuario al grupo \`docker\`:
  \`\`\`bash
  sudo usermod -aG docker $USER
  newgrp docker
  \`\`\`

- **Error "Cannot connect to the Docker daemon":**
  Verificar estado:
  \`\`\`bash
  sudo systemctl status docker
  \`\`\`

---

## 🌐 Recursos adicionales

- [📘 Documentación oficial de Docker](https://docs.docker.com/)
- [📖 Referencia de comandos CLI](https://docs.docker.com/engine/reference/commandline/docker/)
- [🎯 Docker para principiantes (guía interactiva)](https://docker-curriculum.com/)

---

> ✨ Autor: [Nando-Asir](https://github.com/Nando-Asir)  
> 🛡️ Licencia: MIT
