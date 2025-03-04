
# Despliegue de la Aplicación de Votación

Esta aplicación de votación utiliza Python, Node.js, .NET, Redis para la mensajería y Postgres para el almacenamiento.

## Estructura del Proyecto

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

5 directories, 22 files
```

## Descripción de Carpetas y Archivos

- `docker-compose.yml`: Define cómo se ejecutan los servicios de la aplicación utilizando Docker Compose.
  
### healthchecks

Contiene scripts de comprobación de salud para los servicios de PostgreSQL y Redis.

- `postgres.sh`: Script de comprobación de salud para PostgreSQL.
- `redis.sh`: Script de comprobación de salud para Redis.

### result

Contiene los archivos relacionados con el servicio de resultados.

- `Dockerfile`: Archivo Dockerfile para la construcción de la imagen del servicio de resultados.
- `docker-compose.test.yml`: Archivo de configuración de Docker Compose para las pruebas del servicio de resultados.
- `package-lock.json`: Archivo de bloqueo de dependencias de npm para el servicio de resultados.
- `package.json`: Archivo de configuración de npm para el servicio de resultados.
- `server.js`: Archivo principal del servidor del servicio de resultados.
  
#### result/tests

Contiene archivos relacionados con las pruebas del servicio de resultados.

- `Dockerfile`: Archivo Dockerfile para la construcción de la imagen de las pruebas del servicio de resultados.
- `render.js`: Script de renderización para las pruebas del servicio de resultados.
- `tests.sh`: Script de pruebas para el servicio de resultados.

#### result/views

Contiene vistas HTML y archivos estáticos del servicio de resultados.

### seed-data

Contiene archivos relacionados con los datos iniciales de la aplicación.

- `Dockerfile`: Archivo Dockerfile para la construcción de la imagen de datos de inicio.
- `generate-votes.sh`: Script para generar votos en la base de datos.
- `make-data.py`: Script para generar datos en la base de datos.

### vote

Contiene los archivos relacionados con el servicio de votación.

- `Dockerfile`: Archivo Dockerfile para la construcción de la imagen del servicio de votación.
- `app.py`: Archivo principal de la aplicación del servicio de votación.
- `requirements.txt`: Archivo de requisitos de Python para el servicio de votación.

#### vote/static

Contiene archivos estáticos para el servicio de votación.

#### vote/templates

Contiene plantillas HTML para el servicio de votación.

### worker

Contiene los archivos relacionados con el servicio de trabajador.

- `Dockerfile`: Archivo Dockerfile para la construcción de la imagen del servicio de trabajador.
- `Program.cs`: Archivo principal del programa del servicio de trabajador.
- `Worker.csproj`: Archivo de proyecto del servicio de trabajador.

## Instrucciones para el Despliegue


### Pasos para Desplegar

1. **Desplegar la Aplicación**

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

