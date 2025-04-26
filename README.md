# 🐳 Docker - Guía Completa

Este repositorio contiene una guía completa para instalar, configurar y utilizar Docker en sistemas basados en Debian y Ubuntu. Docker es una plataforma de contenedores que permite empaquetar aplicaciones y sus dependencias en entornos aislados, facilitando su despliegue y ejecución en diferentes sistemas.

## 📋 Tabla de Contenidos

1. [Instalación](#instalación)
   - [En Debian](#en-debian)
   - [En Ubuntu](#en-ubuntu)
2. [Uso Básico](#uso-básico)
3. [Manejo de Contenedores](#manejo-de-contenedores)
4. [Tabla de Comandos Útiles](#tabla-de-comandos-útiles)
5. [Consejos y Buenas Prácticas](#consejos-y-buenas-prácticas)
6. [Recursos Adicionales](#recursos-adicionales)

---

## Instalación

### En Debian

Para instalar Docker en Debian, sigue estos pasos:

1. **Actualizar el sistema**:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. **Instalar dependencias necesarias**:
   ```bash
   sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
   ```

3. **Agregar la clave GPG oficial de Docker**:
   ```bash
   curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```

4. **Agregar el repositorio de Docker**:
   ```bash
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

5. **Actualizar los índices de paquetes e instalar Docker**:
   ```bash
   sudo apt update
   sudo apt install -y docker-ce docker-ce-cli containerd.io
   ```

6. **Verificar la instalación**:
   ```bash
   sudo docker --version
   ```

7. **(Opcional) Agregar tu usuario al grupo docker**:
   ```bash
   sudo usermod -aG docker $USER
   ```
   Luego, reinicia tu sesión para aplicar los cambios.

### En Ubuntu

Para instalar Docker en Ubuntu, sigue estos pasos:

1. **Actualizar el sistema**:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. **Instalar dependencias necesarias**:
   ```bash
   sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
   ```

3. **Agregar la clave GPG oficial de Docker**:
   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```

4. **Agregar el repositorio de Docker**:
   ```bash
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

5. **Actualizar los índices de paquetes e instalar Docker**:
   ```bash
   sudo apt update
   sudo apt install -y docker-ce docker-ce-cli containerd.io
   ```

6. **Verificar la instalación**:
   ```bash
   sudo docker --version
   ```

7. **(Opcional) Agregar tu usuario al grupo docker**:
   ```bash
   sudo usermod -aG docker $USER
   ```
   Luego, reinicia tu sesión para aplicar los cambios.

## Uso Básico

- **Descargar una imagen desde Docker Hub**:
  ```bash
  docker pull <nombre-de-la-imagen>
  ```

- **Ejecutar un contenedor**:
  ```bash
  docker run <nombre-de-la-imagen>
  ```

- **Ejecutar un contenedor en segundo plano (detached mode)**:
  ```bash
  docker run -d <nombre-de-la-imagen>
  ```

- **Listar contenedores en ejecución**:
  ```bash
  docker ps
  ```

- **Listar todos los contenedores (incluidos los detenidos)**:
  ```bash
  docker ps -a
  ```

- **Detener un contenedor**:
  ```bash
  docker stop <id-o-nombre-del-contenedor>
  ```

- **Eliminar un contenedor**:
  ```bash
  docker rm <id-o-nombre-del-contenedor>
  ```

- **Eliminar una imagen**:
  ```bash
  docker rmi <id-o-nombre-de-la-imagen>
  ```

## Manejo de Contenedores

- **Crear una red personalizada**:
  ```bash
  docker network create <nombre-de-la-red>
  ```

- **Conectar un contenedor a una red específica**:
  ```bash
  docker run --network=<nombre-de-la-red> <nombre-de-la-imagen>
  ```

- **Inspeccionar un contenedor**:
  ```bash
  docker inspect <id-o-nombre-del-contenedor>
  ```

- **Ver los logs de un contenedor**:
  ```bash
  docker logs <id-o-nombre-del-contenedor>
  ```

- **Ejecutar un comando dentro de un contenedor en ejecución**:
  ```bash
  docker exec -it <id-o-nombre-del-contenedor> <comando>
  ```

## Tabla de Comandos Útiles

| Comando | Descripción |
|---------|-------------|
| `docker pull <imagen>` | Descarga una imagen desde Docker Hub. |
| `docker run <imagen>` | Crea y ejecuta un contenedor a partir de una imagen. |
| `docker ps` | Lista los contenedores en ejecución. |
| `docker ps -a` | Lista todos los contenedores (incluidos detenidos). |
| `docker stop <contenedor>` | Detiene un contenedor en ejecución. |
| `docker rm <contenedor>` | Elimina un contenedor. |
| `docker rmi <imagen>` | Elimina una imagen. |
| `docker images` | Lista las imágenes disponibles localmente. |
| `docker exec -it <contenedor> bash` | Accede al shell de un contenedor en ejecución. |
| `docker logs <contenedor>` | Muestra los logs de un contenedor. |
| `docker network create <red>` | Crea una red personalizada. |
| `docker inspect <contenedor>` | Muestra información detallada de un contenedor. |

## Consejos y Buenas Prácticas

- **Usa nombres descriptivos para tus contenedores**: Esto facilita su identificación.
  ```bash
  docker run --name mi-aplicacion <imagen>
  ```

- **Limpia recursos innecesarios**: Elimina contenedores e imágenes no utilizados para liberar espacio.
  ```bash
  docker system prune -a
  ```

- **Usa Docker Compose para aplicaciones multi-contenedor**: Facilita la gestión de servicios interdependientes.
  ```yaml
  version: '3'
  services:
    web:
      image: nginx
      ports:
        - "80:80"
  ```

- **Monta volúmenes para persistir datos**: Evita perder datos cuando un contenedor se detenga o elimine.
  ```bash
  docker run -v /ruta/local:/ruta/contenedor <imagen>
  ```

## Recursos Adicionales

- [Docker Documentation](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Best Practices for Writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

Si tienes alguna pregunta o sugerencia, no dudes en abrir un issue en este repositorio. ¡Gracias por usar Docker! 🐳
