#  Docker en Acción: De Teoría a Repositorio - Informe Técnico
## David Santiago Beltran Pedraza
## Ficha: 3203084 - ADSO - CBA MOSQUERA

># Resumen conceptos claves en los dos videos

---

## Docker 

Docker es una de las herramientas más importantes hoy en día para el desarrollo y despliegue de aplicaciones. Nos permite ejecutar programas dentro de contenedores, que son entornos ligeros, portables y completamente configurables.  

Básicamente esta es una plataforma que nos permite empaquetar aplicaciones junto con sus dependencias dentro de contenedores y a diferencia de otras, mientras una máquina virtual incluye un sistema operativo completo, Docker utiliza el kernel del sistema anfitrión, lo que lo hace más rápido y liviano.  
Este utiliza herramientas como imagenes y contenedores en los cuales en el caso de la imagen es como una plantilla (read-only) y el contenedor es su instancia ejecutándose.  
## Ventajas Principales: 
Básicamente docker se caracteriza ya que es una máquina virtual que nos da portabilidad, velocidad, reproducibilidad y menor consumo de recursos.  

---

##  Uso de Docker

### 1. ¿Por qué usar Docker y cómo usarlo?
El aprender Docker es una habilidad muy necesaria y que nos da un gran ayuda para ejecutar todo lo que necesite una aplicación y además para asegurar que una aplicación funcione igual en cualquier equipo donde justamente gracias a que podemos descargar y hacer uso de diferentes códigos, bibliotecas y dependencias, lo que garantiza que funcionará de forma consistente en cualquier entorno evitando ese problema de las versiones en los programas, ya sea una computadora local o en la nube. Facilitando cosas como despliegues o pruebas de una app.

### 2. Teoría básica
Básicamente algunos de los conceptos que podemos ver en docker son:
- **Imagen:** plantilla que contiene el entorno de ejecución.  
- **Contenedor:** instancia de una imagen en ejecución.  
- **Capas:** cada instrucción del Dockerfile genera una capa, y el sistema las reutiliza para optimizar compilaciones.  
- **Registro:** repositorio de imágenes (como Docker Hub).  
- **Tag:** etiqueta de versión (`latest`, `1.0`, etc.).  
- **Redes y volúmenes:** permiten comunicación y persistencia de datos.  

### 3. Instalación
El proceso de instalación depende del sistema operativo. En Docker Desktop (Windows/Mac) se hace desde su interfaz oficial, y en Linux mediante el terminal.  
Después de instalar, se verifica con:
**docker --version**

### 4. Comandos de imágenes
En los videos y más que todo el primero se nos explica cómo  ver, descargar, construir, eliminar y otras funciones de las imágenes en el docker, dónde estos se aplican en un interprete de comandos y algunos de los que se usan por ejemplo son:
- **docker pull:** Descarga una imagen desde Docker Hub.
- **docker images:** Muestra las imágenes locales.
- **docker run:** Crea y ejecuta un contenedor nuevo.
- **docker ps:** Lista los contenedores en ejecución.
- **docker ps -a:** Lista todos los contenedores (activos e inactivos).
- **docker stop:** Detiene un contenedor.
- **docker start:** Inicia un contenedor detenido.
- **docker restart:** Reinicia un contenedor.
- **docker rm:** Elimina un contenedor.
- **docker rmi:** Elimina una imagen.
- **docker logs:** Muestra los registros de un contenedor.
- **docker exec -it:** Permite acceder a un contenedor en modo interactivo.
- **docker stats:** Muestra el consumo de recursos en tiempo real.


### 7. Docker Compose
Una parte muy importante del video. Se muestra cómo crear un archivo `docker-compose.yml` para levantar múltiples servicios a la vez (por ejemplo, una app y su base de datos).

Ejemplo:
```yaml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "5000:5000"
  db:
    image: mysql:8
    environment:
      - MYSQL_ROOT_PASSWORD=1234
```
Con un solo comando (`docker-compose up`) se levantan ambos contenedores coordinadamente.

### 8. Volúmenes
Aquí se enseña cómo mantener datos incluso si el contenedor se elimina. Es clave para bases de datos o archivos importantes.
```bash
docker volume create datos
docker run -v datos:/var/lib/mysql mysql
```
## 💭 Reflexiones personales

Aprender Docker me pareció una experiencia muy útil. Me permitió entender mejor cómo los desarrolladores despliegan software en entornos reales sin depender del sistema operativo o las librerías del equipo.  
Docker resuelve muchos problemas de compatibilidad y hace que el trabajo en equipo sea mucho más fluido.

Sus **ventajas** son claras: portabilidad, eficiencia, rapidez y consistencia.  
Los **desafíos**: aprender a usar bien volúmenes, redes y la gestión de imágenes para no ocupar demasiado espacio.  
En la práctica, se nota su utilidad en proyectos de backend, microservicios, bases de datos y pipelines de CI/CD.

---

## 🔗 Recursos adicionales consultados

- [Documentación oficial de Docker](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)

---

## 📤 Enlace al repositorio

Agrega aquí el enlace a tu repositorio una vez lo subas:  
`https://github.com/tuusuario/docker-informe`

---