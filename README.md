
# Despliegue de la aplicación de Votación

Esta aplicación de votación utiliza Python, Node.js, .NET, Redis para la mensajería y Postgres para el almacenamiento. En este Readme se proporciona una guía detallada sobre cómo configurar y ejecutar la aplicación en Docker.

## Estructura del proyecto

El proyecto tiene la siguiente estructura:

```
.
|-- docker-compose.yml
|-- healthchecks
|   |-- postgres.sh
|   `-- redis.sh
|-- result
|   |-- Dockerfile
|   |-- docker-compose.test.yml
|   |-- package-lock.json
|   |-- package.json
|   |-- server.js
|   |-- tests
|   |   |-- Dockerfile
|   |   |-- render.js
|   |   `-- tests.sh
|   `-- views
|       |-- angular.min.js
|       |-- app.js
|       |-- index.html
|       |-- socket.io.js
|       `-- stylesheets
|           `-- style.css
|-- seed-data
|   |-- Dockerfile
|   |-- generate-votes.sh
|   `-- make-data.py
|-- vote
|   |-- Dockerfile
|   |-- app.py
|   |-- requirements.txt
|   |-- static
|   |   `-- stylesheets
|   |       `-- style.css
|   `-- templates
|       `-- index.html
`-- worker
    |-- Dockerfile
    |-- Program.cs
    `-- Worker.csproj

11 directories, 27 files
```

## Descripción de archivos

- `docker-compose.yml`: Archivo de configuración de Docker Compose que define cómo se ejecutan los servicios de la aplicación.
- `healthchecks/postgres.sh`: Script de comprobación de salud para PostgreSQL.
- `healthchecks/redis.sh`: Script de comprobación de salud para Redis.
- `result/Dockerfile`: Archivo Dockerfile para la construcción de la imagen del servicio de resultados.
- `result/docker-compose.test.yml`: Archivo de configuración de Docker Compose para las pruebas del servicio de resultados.
- `result/package-lock.json`: Archivo de bloqueo de dependencias de npm para el servicio de resultados.
- `result/package.json`: Archivo de configuración de npm para el servicio de resultados.
- `result/server.js`: Archivo principal del servidor del servicio de resultados.
- `result/tests/Dockerfile`: Archivo Dockerfile para la construcción de la imagen de las pruebas del servicio de resultados.
- `result/tests/render.js`: Script de renderización para las pruebas del servicio de resultados.
- `result/tests/tests.sh`: Script de pruebas para el servicio de resultados.
- `result/views`: Directorio que contiene las vistas HTML y archivos estáticos del servicio de resultados.
- `seed-data/Dockerfile`: Archivo Dockerfile para la construcción de la imagen de datos de inicio.
- `seed-data/generate-votes.sh`: Script para generar votos en la base de datos.
- `seed-data/make-data.py`: Script para generar datos en la base de datos.
- `vote/Dockerfile`: Archivo Dockerfile para la construcción de la imagen del servicio de votación.
- `vote/app.py`: Archivo principal de la aplicación del servicio de votación.
- `vote/requirements.txt`: Archivo de requisitos de Python para el servicio de votación.
- `vote/static`: Directorio que contiene archivos estáticos para el servicio de votación.
- `vote/templates`: Directorio que contiene plantillas HTML para el servicio de votación.
- `worker/Dockerfile`: Archivo Dockerfile para la construcción de la imagen del servicio de trabajador.
- `worker/Program.cs`: Archivo principal del programa del servicio de trabajador.
- `worker/Worker.csproj`: Archivo de proyecto del servicio de trabajador.

## Empezando

Sigue estos pasos para desplegar la aplicación de votación en tu entorno local.

### Prerrequisitos

- Docker Desktop para Mac o Windows. Docker Compose se instalará automáticamente. En Linux, asegúrate de tener la última versión de Compose.
- Asegúrate de que `docker-compose` está instalado y funcionando en tu sistema.

### Pasos para desplegar

1. **Clonar el Repositorio**

   Clona este repositorio en tu máquina local:

   ```bash
   git clone <URL_DEL_REPOSITORIO>
   ```

2. **Desplegar la Aplicación**

   En el directorio raíz del proyecto, ejecuta el siguiente comando para construir y ejecutar la aplicación:

   ```bash
   docker compose up
   ```

   Este comando creará y ejecutará los servicios definidos en el archivo `docker-compose.yml`. El servicio de votación estará disponible en `http://localhost:5000`, y los resultados en `http://localhost:5001`.

   Alternativamente, si deseas ejecutarlo en un Docker Swarm, primero asegúrate de tener un enjambre. Si no lo tienes, ejecuta:

   ```bash
   docker swarm init
   ```

   Una vez que tengas tu enjambre, en el directorio raíz del proyecto, ejecuta:

   ```bash
   docker stack deploy --compose-file docker-stack.yml vote
   ```

   Esto desplegará la aplicación en tu enjambre de Docker.

---

Con estos pasos, deberías poder desplegar fácilmente la aplicación de votación en tu entorno local. ¡Disfruta de tu experiencia de votación!
