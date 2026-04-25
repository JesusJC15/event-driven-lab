# event-driven-lab

Laboratorio base para arquitectura dirigida por eventos con Spring Boot y RabbitMQ.

## Estructura del proyecto

```text
event-driven-lab/
├── producer-service/         # Servicio productor Spring Boot
│   ├── src/
│   ├── pom.xml
│   └── Dockerfile
├── consumer-service/         # Servicio consumidor Spring Boot
│   ├── src/
│   ├── pom.xml
│   └── Dockerfile
├── docker-compose.yml        # Orquestación con RabbitMQ + producer + consumer
└── README.md                 # Instrucciones
```

## Requisitos

- Docker y Docker Compose
- Java 17 y Maven 3.9+ (solo si ejecutas sin contenedores)

## Levantar el entorno local con Docker Compose

Puedes usar cualquiera de estas variantes, según tu instalación:

```bash
docker compose up -d
```

o

```bash
docker-compose up -d
```

Verifica el estado:

```bash
docker compose ps
```

## Servicios expuestos

- Producer API: http://localhost:8080
- RabbitMQ AMQP: localhost:5672
- RabbitMQ Management UI: http://localhost:15672 (guest/guest)

## Probar flujo de eventos

1) Enviar mensaje desde el productor:

```bash
curl -X POST "http://localhost:8080/api/messages/send?message=HolaDesdeCompose"
```

Respuesta esperada:

```text
Mensaje 'HolaDesdeCompose' enviado!
```

2) Ver logs del consumidor:

```bash
docker compose logs consumer
```

Debes ver trazas similares a:

```text
Mensaje recibido: 'HolaDesdeCompose'
>>> Mensaje Procesado: HolaDesdeCompose
```

Nota: Usa el nombre de servicio consumer (no consumer-service) para logs con Compose.

## Opcion A: Ejecutar en Killercoda

1) Abre Ubuntu Playground en Killercoda e inicia sesion.
2) Clona el repositorio:

```bash
git clone https://github.com/<tu-usuario>/event-driven-lab.git
cd event-driven-lab
```

3) Verifica tu variante de Compose:

```bash
docker-compose --version
```

o

```bash
docker compose version
```

4) Levanta servicios:

```bash
docker-compose up -d
```

Si tu entorno usa plugin V2, usa docker compose up -d.

5) Espera aproximadamente 30 segundos y valida:

```bash
docker-compose ps
```

6) Envia evento:

```bash
curl -X POST "http://localhost:8080/api/messages/send?message=HolaDesdeKillercoda"
```

7) Verifica procesamiento:

```bash
docker-compose logs consumer
```

8) Publica puertos en el menu Traffic / Port de Killercoda:

- 8080 para Producer API
- 15672 para RabbitMQ Management UI

En RabbitMQ UI usa guest/guest y revisa la cola messages.queue.

## Nota sobre error 405 en navegador

Si abres /api/messages/send directamente en el navegador veras 405 Method Not Allowed. Es esperado porque el endpoint acepta solo POST.

Usa curl o una herramienta HTTP (por ejemplo Hoppscotch) con metodo POST.