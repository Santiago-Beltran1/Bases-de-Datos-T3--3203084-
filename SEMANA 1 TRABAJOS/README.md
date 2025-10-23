#  Docker en Acción: De Teoría a Repositorio - Informe Técnico
## David Santiago Beltran Pedraza
## Ficha: 3203084 - ADSO - CBA MOSQUERA

---

## Conceptos y todo lo aprendido (primer video):
## Docker 

Docker es una plataforma la cual nos permite ejecutar programas dentro de contenedores, que son entornos ligeros, portables y completamente configurables el cual busca el objetivo de ayudarnos a desarrollar y ejecutar nuestras aplicaciones.  

Básicamente esta es una plataforma que nos permite empaquetar aplicaciones junto con sus dependencias dentro de contenedores y a diferencia de otras, mientras que en una máquina virtual incluye un sistema operativo completo, Docker utiliza ese kernel del sistema anfitrión, lo que lo hace más rápido y liviano.  
Este utiliza herramientas como imagenes y contenedores en los cuales en el caso de la imagen es como una plantilla y el contenedor es su instancia ejecutándose.  

---

##  Uso de Docker

### ¿Por qué usar Docker y cómo usarlo?
Pues el aprender Docker es una habilidad muy necesaria y que nos da una gran ayuda para ejecutar todo lo que necesite una aplicación y además para asegurar que una aplicación funcione igual en cualquier equipo donde justamente gracias a que podemos descargar y hacer uso de diferentes códigos, bibliotecas y dependencias, lo que garantiza que funcionará de forma consistente en cualquier entorno evitando ese problema de las versiones en los programas, ya sea una computadora local o en la nube. Facilitando cosas como despliegues o pruebas de una app.

### Algunos Conceptos:
Básicamente algunos de los conceptos que podemos ver en docker son:
- **Imagen:** plantilla que contiene el entorno de ejecución.  
- **Contenedor:** instancia de una imagen en ejecución.  
- **Capas:** cada instrucción del Dockerfile genera una capa, y el sistema las reutiliza para optimizar compilaciones.  
- **Registro:** repositorio de imágenes (como Docker Hub).  
- **Tag:** etiqueta de versión (`latest`, `1.0`, etc.).  
- **Redes y volúmenes:** permiten comunicación y persistencia de datos.  

### Instalación
El proceso de instalación depende del sistema operativo. En Docker Desktop (Windows/Mac) se hace desde su interfaz oficial, y en Linux mediante el terminal.  
Después de instalar, ponemos el comando **wsl --install** para instalar la distribución de linux y de ahí ya podremos hacer uso de los comandos de Docker en el interprete.

También hay que recordar que para la creación de contenedores en la página de Docker Hub encontraremos todo ese repositorio con todas las plantillas o imágenes con las diferentes versiones de las que lleguemos a necesitar para la creación de nuestra aplicación la cual en el interprete se debera poner: **docker pull (más ese nombre de la imagen y la versión si se ha de necesitar o si no se instalará la más reciente)** y con el **comando docker images** podremos ver todas aquellas que se han descargado.

### Comandos de imágenes
En los videos y más que todo el primero se nos explica cómo  ver, descargar, construir, eliminar y otras funciones de las imágenes en el docker, donde estos se aplican en un interprete de comandos y algunos de los que se usan por ejemplo son:
- **docker create**: Crea un contenedor a partir de una imagen, pero no lo inicia. 
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

También al ejecutar el comando `docker run`, se pueden añadir diferentes opciones para personalizar la creación y ejecución del contenedor. Las que podemos ver en el video son:

- **--name**: Asigna un nombre al contenedor.  
- **-d**: Ejecuta el contenedor en modo detached (en segundo plano).  
- **-p**: Mapea los puertos del host con los del contenedor.  
- **-v**: Monta volúmenes (carpetas compartidas) entre el host y el contenedor.  
- **-e**: Define variables de entorno.  
- **--rm**: Elimina el contenedor automáticamente al detenerse.  

---

## Conceptos y todo lo aprendido (segundo video):

### Dockerfile y Docker Compose

Un Dockerfile es el archivo donde se define paso a paso cómo se construye una imagen de Docker. En este pues básicamente se indica qué base se usa, qué archivos se copian, qué dependencias se instalan y qué comando ejecuta el contenedor al iniciarse. Todo parte con la instrucción FROM, que selecciona una imagen base, por ejemplo una de Node.js, Python o algún otro. 
Luego se usa WORKDIR para establecer el directorio de trabajo dentro de la imagen, y COPY o ADD para copiar los archivos desde el proyecto local al interior de la imagen. La instrucción RUN ejecuta comandos durante la construcción, típicamente para instalar dependencias, y EXPOSE declara el puerto que la aplicación usará. Finalmente, con CMD o ENTRYPOINT se define el comando que corre al arrancar el contenedor, por ejemplo iniciar un servidor.

### Forma de hacerlo
Primero escribimos el Dockerfile en el directorio del proyecto, luego se construye la imagen con el comando docker build, asignándole un nombre y etiqueta, y después se ejecuta con docker run mapeando los puertos para poder acceder desde el host. 
También encontramos buenas prácticas como usar imágenes base livianas (por ejemplo Alpine), mantener el Dockerfile ordenado para aprovechar la caché de capas, incluir un archivo .dockerignore para no copiar archivos innecesarios y etiquetar correctamente las imágenes para un control de versiones claro.

Después de entender cómo funciona ese contenedor individual pasamos al Docker Compose, que sirve para ir creando múltiples contenedores al mismo tiempo. En lugar de iniciar cada servicio con comandos separados, Compose permite definir todo en un único archivo llamado docker-compose.yml, escrito en formato YAML. Allí especifícamos los servicios o aplicaciones, las imágenes que usarán, los puertos que se abrirán, los volúmenes que se montarán y las dependencias entre ellos. Por ejemplo, una aplicación web puede depender de una base de datos, y esa relación se expresa con depends_on.

### Funcionamiento del compose

En el archivo se listan los servicios, por ejemplo uno llamado “app” que se construye con el Dockerfile local (usando la clave build) y otro servicio “db” que usa directamente una imagen preexistente (con la clave image). Los puertos se declaran con ports, indicando el mapeo entre el host y el contenedor, y los volúmenes permiten mantener persistencia o reflejar los cambios del código local dentro del contenedor, esto siendo muy útil para el mismo desarrollo. Con un solo comando docker-compose up se levantan todos los servicios juntos y se conectan automáticamente dentro de una red interna creada por Docker.

## Volúmenes y ambientes en Docker (Explicado más que todo en el primer video)

En el video se explica que los volúmenes son la forma en que Docker maneja los datos que deben persistir, incluso cuando un contenedor se elimina. Por defecto, todo lo que está dentro de un contenedor desaparece al detenerlo, así que los volúmenes sirven para mantener la información fuera de ese ciclo de vida efímero. Lo más común es usarlos para cosas como bases de datos, logs o archivos que querés conservar entre ejecuciones.

Ayudan a montar el código de el proyecto directamente dentro del contenedor. De esa forma, cada vez que se guardan cambios en la máquina, se reflejan automáticamente en el contenedor sin tener que reconstruir la imagen. En producción, en cambio, no se suele montar el código local, sino que se trabaja con la imagen ya construida y volúmenes solo para los datos que deben persistir.

El video también habla de los ambientes o entornos, que básicamente son las diferentes configuraciones según el contexto en el que se este trabajando: desarrollo, pruebas o producción. En Docker esto se maneja principalmente con variables de entorno y con pequeños ajustes en los volúmenes o en cómo se construye la imagen. Por ejemplo, en desarrollo se pueden definir variables que habiliten el modo debug o montar el código local, mientras que en producción esas variables cambian y los volúmenes se usan solo para persistencia de datos reales.

---

## Reflexiones personales

### Ventajas, Desafíos y Usos Prácticos: 

- Pienso que la principal ventaja de Docker es que hace que todo sea más fácil cuando se desarrolla una aplicación, por ejemplo lo que se nos explicaba en los videos donde surgen problemas porque no funciona igual en todos los equipos pero con Docker eso no es así. El hecho de que los contenedores que la aplicación ejecuta justamente gracias a esta plataforma se puedan correr igual sin importar el sistema operativo o la máquina donde este,  evita esa pérdida de tiempo. Siendo justamente muy rápido y fluido gracias a los mismos contenedores y el repositorio con el que cuenta en Docker-Hub donde pues básicamente esta la gran mayoría de códigos o bibliotecas para trabajar en el desarrollo de alguna aplicación.

- Por mi parte uno de los desafíos que encontré fue entender como se construye correctamente un Dockerfile. Básicamente para hacer buen uso de un Dockerfile o un compose hay que entender el orden y las buenas prácticas de este mismo y aunque es tema de tiempo y entreno es algo que almenos a mi se me dificulta en estos momentos. Básicamente no es solo aprenderse o copiar código sino que saber ordenarlo y aplicarlo.

- Y en el caso de usos prácticos los usos más prácticos de Docker está para mi en que nos deja tener ese control sobre los versiones o esos entornos, imágenes etc. Si un compañero necesita probar algo, solo debe ejecutar un comando y tendrá el mismo entorno que uno, al igual que nos ayuda en la simplificación del desarrollo de una aplicación y además de que nos permite unir varias herramientas en un mismo espacio, como en nuestro caso pues el tema de bases de datos donde podemos incluir y trabajar con varias al tiempo de manera muy eficaz.

---

## Ejemplo práctico de algún concepto de Docker:

### Ejemplo en la creación de un contenedor

**docker run -d --name mi-postgres -p 5432:5432 -e POSTGRES_USER=admin -e POSTGRES_PASSWORD=1234 -e POSTGRES_DB=midb postgres**

Aquí pues básicamente encontramos un ejemplo de como se aplicarian esos comandos de los que se hablo anteriormente al ejecutar un contenedor.

### Otro Ejemplo
Aquí se puede ver cómo crear un archivo `docker-compose.yml` para levantar múltiples servicios a la vez (por ejemplo, una app más la base de datos).

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




---

## Recursos adicionales consultados

- [Documentación oficial de Docker](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- Estos se usaron también al momento de averiguar comandos en la creación de contenedores o cómo se instalan images, en dónde se encuentran los mismos también.
