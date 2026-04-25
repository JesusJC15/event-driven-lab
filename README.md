# event-driven-lab

Laboratorio base para arquitectura dirigida por eventos con Spring Boot y Kafka.

## Estructura del proyecto

```text
event-driven-lab/
├── producer-service/         # Servicio Productor Spring Boot
│   ├── src/
│   ├── pom.xml
│   └── Dockerfile
├── consumer-service/         # Servicio Consumidor Spring Boot
│   ├── src/
│   ├── pom.xml
│   └── Dockerfile
├── .devcontainer/            # Configuración para Codespaces
│   └── devcontainer.json
├── docker-compose.yml        # Orquestación para Play with Docker
└── README.md                 # Instrucciones
```

## Requisitos

- Docker y Docker Compose
- Java 17 (si ejecutas sin contenedores)
- Maven 3.9+ (si ejecutas sin contenedores)

## Levantar el entorno con Docker

```bash
docker compose up --build
```

Servicios esperados:

- Kafka en `localhost:29092` (host)
- Producer service en `localhost:8080`
- Consumer service en `localhost:8081`

## Uso en Codespaces / Dev Container

Al abrir el repositorio en Dev Container se instala Java 17 y Docker-outside-of-docker.
Tambien se precargan dependencias Maven de ambos servicios en el `postCreateCommand`.

## Siguientes pasos sugeridos

- Agregar clase principal Spring Boot en ambos `src/`
- Crear endpoint en productor para publicar eventos
- Crear listener en consumidor para procesar eventos