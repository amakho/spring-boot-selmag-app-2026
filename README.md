# Spring Projects (2026)

Simple microservices project based on Spring Boot.  

## Profiles

- **standalone** – run services without Eureka and Config Server  
- **cloud** – run with Eureka  
- **cloudconfig** – run with Eureka + Config Server  
- **gateway** – services behind API Gateway  
- **native / git** – Config Server config source

## Required Services

### Keycloak – Auth Server

```bash
docker run --name selmag-keycloak -p 8082:8080 \
-e KEYCLOAK_ADMIN=admin \
-e KEYCLOAK_ADMIN_PASSWORD=admin \
quay.io/keycloak/keycloak:23.0.7 start-dev
```

### PostgreSQL – Catalogue DB

```bash
docker run --name catalogue-db -p 5432:5432 \
-e POSTGRES_USER=catalogue \
-e POSTGRES_PASSWORD=catalogue \
-e POSTGRES_DB=catalogue postgres:16
```

### MongoDB – Feedback DB

```bash
docker run --name feedback-db -p 27017:27017 mongo:7
```

## Monitoring Stack

### Victoria Metrics

```bash
docker run --name selmag-metrics -p 8428:8428 \
victoriametrics/victoria-metrics:v1.93.12
```

### Grafana

```bash
docker run --name selmag-grafana -p 3000:3000 \
grafana/grafana:10.2.4
```

### Loki

```bash
docker run --name selmag-loki -p 3100:3100 \
grafana/loki:2.9.4
```

### Tempo

```bash
docker run --name selmag-tracing -p 3200:3200 \
grafana/tempo:2.3.1
```

## How to run locally

1. Start required Docker services  
2. Choose Spring profile  
3. Run applications with:

```bash
mvn spring-boot:run -Dspring-boot.run.profiles=standalone
```

## Notes

- `172.17.0.1` – default Docker host IP  
- If your Docker uses another address, update configs
- All services use local environment by default
