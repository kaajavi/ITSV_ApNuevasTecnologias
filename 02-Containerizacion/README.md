# Unidad 2: Conteinerización - Docker y Docker Compose

## Descripción
Esta unidad aborda la tecnología de contenedores, centrada en Docker como herramienta principal. Los estudiantes comprenderán cómo los contenedores revolucionaron el desarrollo y despliegue de aplicaciones, facilitando entornos reproducibles y consistentes. Se explorarán tanto los conceptos fundamentales como las implementaciones avanzadas con Docker Compose.

## Objetivos
- Entender los problemas que soluciona la conteinerización
- Comprender la arquitectura y funcionamiento de Docker
- Crear y gestionar imágenes y contenedores Docker
- Desarrollar aplicaciones multi-contenedor con Docker Compose
- Aplicar buenas prácticas en la conteinerización de aplicaciones

## Contenidos

### [1. Problemas del Despliegue Tradicional](01-Problemas-Despliegue-Tradicional/README.md)
- El infierno de las dependencias
- "En mi máquina funciona"
- Consistencia entre entornos
- Desafíos del escalado horizontal

### [2. Virtualización vs. Conteinerización](02-Virtualizacion-vs-Containerizacion/README.md)
- Máquinas virtuales: beneficios y limitaciones
- Diferencias técnicas y conceptuales
- Ventajas de los contenedores
- Casos de uso ideales para cada tecnología

### [3. Arquitectura de Docker](03-Arquitectura-Docker/README.md)
- Cliente y servidor (daemon)
- Docker Engine
- Arquitectura de capas
- Runtime de contenedores

### [4. Imágenes, Contenedores, Volúmenes y Redes](04-Imagenes-Contenedores-Volumenes-Redes/README.md)
- Imágenes: construcción y gestión
- Contenedores: ciclo de vida y operaciones
- Volúmenes: persistencia de datos
- Redes: comunicación entre contenedores

### [5. Dockerfile y Mejores Prácticas](05-Dockerfile-Buenas-Practicas/README.md)
- Sintaxis y comandos
- Construcción de imágenes eficientes
- Multi-stage builds
- Seguridad y optimización

### [6. DockerHub y Registries](06-DockerHub-Registries/README.md)
- Repositorios públicos y privados
- Publicación de imágenes
- Registros privados
- Automatización de builds

### [7. Docker Compose y Definición de Servicios](07-Docker-Compose/README.md)
- Formato YAML
- Definición de servicios
- Redes y volúmenes en Compose
- Entornos de desarrollo con Compose

### [8. Casos de Uso Reales](08-Casos-Uso-Reales/README.md)
- Contenedores en producción
- Patrones comunes
- Integración con CI/CD
- Orquestación: introducción a Kubernetes

## Proyectos Prácticos
- Conteinerización de aplicación simple
- Desarrollo de entorno multi-contenedor
- Implementación de pipeline con Docker
- Despliegue en plataforma basada en contenedores
