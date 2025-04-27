# 🐳 Docker - Guía Completa de Instalación y Uso

[![Docker](https://img.shields.io/badge/docker-ready-blue?logo=docker)](https://www.docker.com/)
[![Ubuntu Compatible](https://img.shields.io/badge/ubuntu-20.04%2B-orange?logo=ubuntu)](https://ubuntu.com/)
[![Debian Compatible](https://img.shields.io/badge/debian-11%2B-red?logo=debian)](https://www.debian.org/)
[![License: MIT](https://img.shields.io/badge/license-MIT-green)](LICENSE)

---

## 📚 Índice
- [🚀 Introducción](#-introducción)
- [🔧 Instalación de Docker](#-instalación-de-docker)
- [🏁 Primeros pasos](#-primeros-pasos)
- [📦 Manejo de contenedores](#-manejo-de-contenedores)
- [🧰 Tabla de comandos útiles](#-tabla-de-comandos-útiles)
- [📄 Instalación de Docker Compose (opcional)](#-instalación-de-docker-compose-opcional)
- [🛠️ Solución de problemas (Troubleshooting)](#️-solución-de-problemas-troubleshooting)
- [🌐 Recursos adicionales](#-recursos-adicionales)

---

## 🚀 Introducción
Esta guía te enseña cómo instalar y utilizar **Docker** en **Debian** o **Ubuntu** de forma práctica y rápida.  
Docker permite construir, desplegar y gestionar aplicaciones de manera aislada usando **contenedores**.

---

## 🔧 Instalación de Docker

### 1. Eliminar versiones antiguas
```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
2. Actualizar repositorios
bash
Copiar
Editar
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release
3. Añadir la clave GPG oficial
bash
Copiar
Editar
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
4. Configurar el repositorio
bash
Copiar
Editar
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
💡 Nota: Si usas Debian, reemplaza ubuntu por debian en el enlace del repositorio.

5. Instalar Docker Engine
bash
Copiar
Editar
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
6. Verificar instalación
bash
Copiar
Editar
docker --version
🏁 Primeros pasos
Comprobar que Docker está corriendo:

bash
Copiar
Editar
sudo systemctl status docker
Iniciar Docker (si es necesario):

bash
Copiar
Editar
sudo systemctl start docker
📦 Manejo de contenedores

Acción	Comando
Buscar imágenes	docker search nginx
Descargar imagen	docker pull nginx
Ejecutar un contenedor	docker run -d -p 8080:80 nginx
Listar contenedores en ejecución	docker ps
Listar todos los contenedores	docker ps -a
Detener un contenedor	docker stop <nombre o ID>
Eliminar un contenedor	docker rm <nombre o ID>
Ver logs de un contenedor	docker logs <nombre o ID>
🧠 Tip: Usa docker ps -a para ver contenedores detenidos también.

🧰 Tabla de comandos útiles

Acción rápida	Comando
Ver versión de Docker	docker --version
Ver imágenes disponibles	docker images
Eliminar una imagen	docker rmi <imagen>
Inspeccionar un contenedor	docker inspect <nombre>
Mostrar estadísticas	docker stats
📄 Instalación de Docker Compose (opcional)
Docker Compose permite definir y correr aplicaciones multicontenedor mediante un archivo YAML.

Instalar Docker Compose
bash
Copiar
Editar
sudo apt-get install docker-compose-plugin
Verificar instalación
bash
Copiar
Editar
docker compose version
Ejemplo básico de docker-compose.yml
yaml
Copiar
Editar
version: "3.9"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
Para iniciar los servicios:

bash
Copiar
Editar
docker compose up -d
Para detenerlos:

bash
Copiar
Editar
docker compose down
🛠️ Solución de problemas (Troubleshooting)
Docker no inicia:

bash
Copiar
Editar
sudo systemctl start docker
Error: permission denied (sin sudo): Agrega tu usuario al grupo docker:

bash
Copiar
Editar
sudo usermod -aG docker $USER
newgrp docker
Error "Cannot connect to the Docker daemon": Asegúrate de que Docker esté en ejecución:

bash
Copiar
Editar
sudo systemctl status docker
🌐 Recursos adicionales
📚 Documentación oficial de Docker

📖 Referencias de comandos CLI

🎓 Docker para principiantes - Guía interactiva

✨ Autor: Nando-Asir
🛡️ Licencia: MIT
