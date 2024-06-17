# Despliegue de una Aplicación de Votación en Kubernetes

Este archivo README proporciona una guía paso a paso para desplegar una aplicación de votación en un clúster de Kubernetes. Se incluyen explicaciones detalladas de los archivos de configuración y los comandos necesarios para crear y eliminar los recursos en Kubernetes.

## Contenido

1. [Archivos de Configuración](#archivos-de-configuración)
    - [db-deployment.yaml](#db-deploymentyaml)
    - [db-service.yaml](#db-serviceyaml)
    - [redis-deployment.yaml](#redis-deploymentyaml)
    - [redis-service.yaml](#redis-serviceyaml)
    - [result-deployment.yaml](#result-deploymentyaml)
    - [result-service.yaml](#result-serviceyaml)
    - [vote-deployment.yaml](#vote-deploymentyaml)
    - [vote-service.yaml](#vote-serviceyaml)
    - [worker-deployment.yaml](#worker-deploymentyaml)
2. [Pasos para Desplegar la Aplicación](#pasos-para-desplegar-la-aplicación)
3. [Comandos Útiles para Verificación](#comandos-útiles-para-verificación)
4. [Eliminación de los Recursos](#eliminación-de-los-recursos)

## Archivos de Configuración

### db-deployment.yaml
Define un Deployment para la base de datos PostgreSQL. Especifica la cantidad de réplicas del contenedor, la imagen del contenedor y las variables de entorno necesarias, como la contraseña de la base de datos.

### db-service.yaml
Define un Service para la base de datos PostgreSQL, permitiendo que otros componentes de la aplicación se comuniquen con ella. Establece el puerto y utiliza un selector para vincular el servicio con el Deployment de la base de datos.

### redis-deployment.yaml
Define un Deployment para el almacén de datos en memoria Redis. Especifica la imagen del contenedor y el puerto en el que Redis estará disponible.

### redis-service.yaml
Define un Service para Redis, permitiendo que otros componentes de la aplicación se comuniquen con él. Establece el puerto y utiliza un selector para vincular el servicio con el Deployment de Redis.

### result-deployment.yaml
Define un Deployment para el componente de resultados de la aplicación, que mostrará los resultados de las votaciones. Especifica la imagen del contenedor y el puerto en el que la aplicación estará disponible.

### result-service.yaml
Define un Service para el componente de resultados, permitiendo acceder a la aplicación de resultados desde fuera del clúster. Establece el puerto y utiliza un selector para vincular el servicio con el Deployment de resultados. Además, utiliza el tipo NodePort para hacer que el servicio esté disponible en un puerto específico en cada nodo del clúster.

### vote-deployment.yaml
Define un Deployment para el componente de votación de la aplicación, que permitirá a los usuarios emitir sus votos. Especifica la imagen del contenedor y el puerto en el que la aplicación estará disponible.

### vote-service.yaml
Define un Service para el componente de votación, permitiendo acceder a la aplicación de votación desde fuera del clúster. Establece el puerto y utiliza un selector para vincular el servicio con el Deployment de votación. Al igual que el servicio de resultados, utiliza el tipo NodePort para hacer que el servicio esté disponible en un puerto específico en cada nodo del clúster.

### worker-deployment.yaml
Define un Deployment para el componente worker de la aplicación, que procesa los votos y actualiza los resultados en la base de datos. Especifica la imagen del contenedor y las configuraciones necesarias para que el worker funcione correctamente.

## Pasos para Desplegar la Aplicación

1. Asegúrate de que tienes `kubectl` instalado y configurado para interactuar con tu clúster de Kubernetes.
2. Navega al directorio que contiene los archivos de configuración YAML (por ejemplo, `k8s-specifications`).
3. Ejecuta el siguiente comando para crear los deployments y servicios en tu clúster:

    ```bash
    kubectl create -f k8s-specifications/
    ```

    Este comando aplicará todos los archivos YAML en el directorio especificado, creando los recursos necesarios en tu clúster de Kubernetes.

4. Una vez desplegados los recursos, usa el siguiente comando para hacer un port-forward y acceder a las aplicaciones desde tu máquina local:

    - Para la aplicación de votación en el puerto 31000:
    
        ```bash
        kubectl port-forward svc/vote 31000:5000
        ```

    - Para la aplicación de resultados en el puerto 31001:
    
        ```bash
        kubectl port-forward svc/result 31001:5001
        ```

## Comandos Útiles para Verificación

Para verificar que los pods están corriendo correctamente, puedes usar el siguiente comando:

```bash
kubectl get pods
```

Este comando mostrará una lista de todos los pods en el clúster, su estado actual y otra información relevante.

Para verificar los servicios desplegados, usa:

```bash
kubectl get svc
```

Este comando mostrará una lista de todos los servicios en el clúster, sus tipos y los puertos en los que están expuestos.

## Eliminación de los Recursos

Para eliminar los recursos creados (deployments y servicios), ejecuta el siguiente comando:

```bash
kubectl delete -f k8s-specifications/
```

Este comando eliminará todos los recursos especificados en los archivos YAML en el directorio indicado, limpiando el clúster de Kubernetes de los componentes de la aplicación de votación.
