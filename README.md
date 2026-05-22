# Proyecto DevOps - Tienda Perritos

## Descripción del Proyecto

Este proyecto consiste en el despliegue de una aplicación web multicapa utilizando contenedores Docker y servicios AWS bajo un enfoque DevOps.

La aplicación está dividida en tres capas:

- Frontend
- Backend
- Base de Datos

Cada componente fue desplegado en instancias EC2 separadas, permitiendo una arquitectura distribuida y escalable.

---

# Arquitectura del Proyecto

## Tecnologías Utilizadas

| Componente | Tecnología |
|---|---|
| Frontend | React + Nginx |
| Backend | Node.js + Express |
| Base de Datos | MySQL 8 |
| Contenedores | Docker |
| Cloud | AWS |
| CI/CD | GitHub Actions |
| Registro de imágenes | Amazon ECR |

---

# Arquitectura AWS

## Servicios Utilizados

- Amazon EC2
- Amazon VPC
- Security Groups
- AWS Systems Manager (SSM)
- Amazon ECR
- GitHub Actions
- Docker

---

# Arquitectura de Red

## VPC

```txt
10.0.0.0/16
```

## Subredes

| Subred | Tipo |
|---|---|
| Frontend | Pública |
| Backend | Privada |
| Database | Privada |

---

# Seguridad

## Security Groups

### Frontend
- HTTP 80 desde Internet
- Comunicación con Backend

### Backend
- Puerto 3001 desde Frontend

### Database
- Puerto 3306 desde Backend

---

# Conexión mediante Session Manager

Las instancias EC2 fueron administradas utilizando AWS Systems Manager Session Manager, evitando el uso de llaves SSH.

---

# Dockerización

## Frontend

### Build

```bash
docker build -t tienda-frontend .
```

### Run

```bash
docker run -d --name tienda-frontend -p 80:80 tienda-frontend
```

---

## Backend

### Variables de entorno

```env
DB_HOST=
DB_USER=
DB_PASSWORD=
DB_NAME=
DB_PORT=3306
```

### Build

```bash
docker build -t tienda-backend .
```

### Run

```bash
docker run -d --name tienda-backend -p 3001:3001 tienda-backend
```

---

## Base de Datos

### Run

```bash
docker run -d \
--name tienda-db \
-e MYSQL_ROOT_PASSWORD=root \
-e MYSQL_DATABASE=tienda_perritos \
-p 3306:3306 mysql:8
```

---

# Integración Continua y Despliegue Continuo (CI/CD)

Se implementaron pipelines separados en GitHub Actions para:

- Frontend
- Backend
- Database

## Funcionalidades del Pipeline

- Build automático de imágenes Docker
- Push automático a Amazon ECR
- Despliegue automático en EC2

---

# Amazon ECR

Las imágenes Docker fueron publicadas en repositorios ECR separados para:

- Frontend
- Backend
- Database

---

# GitHub Actions

## Secrets utilizados

```txt
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_SESSION_TOKEN
AWS_REGION

ECR_REPO_URL_FRONTEND
ECR_REPO_URL_BACKEND
ECR_REPO_URL_DB

EC2_FRONTEND_INSTANCE_ID
EC2_BACKEND_INSTANCE_ID
EC2_DB_INSTANCE_ID
```

---

# Validaciones Realizadas

## Frontend

Acceso desde navegador:

```txt
http://IP_PUBLICA
```

---

## Backend

Health Check:

```txt
/api/health
```

---

## Base de Datos

Verificación de conexión exitosa entre Backend y MySQL.

---

# Comandos de Verificación

## Ver contenedores activos

```bash
docker ps
```

## Ver logs

```bash
docker logs tienda-frontend
docker logs tienda-backend
docker logs tienda-db
```

---

---

# Resultado Final

Se logró desplegar exitosamente una aplicación multicapa en AWS utilizando Docker, automatizando el proceso de integración y despliegue mediante GitHub Actions y Amazon ECR.

El proyecto permitió aplicar conceptos de:

- Arquitectura multicapa
- Dockerización
- Infraestructura Cloud
- CI/CD
- Automatización DevOps
- Redes y Seguridad AWS

---

# Integrantes

- Juan Cortés
- Camila Hernández

