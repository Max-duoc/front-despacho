# Frontend Despachos — Innovatech Chile

Aplicación web desarrollada con React y Vite para la gestión de despachos de Innovatech Chile. Desplegada en contenedores Docker sobre AWS EC2.

## Tecnologías

- React 18
- Vite
- Tailwind CSS
- Nginx Alpine
- Docker + Docker Compose
- GitHub Actions (CI/CD)

## Estructura del proyecto
front_despacho/
├── .github/
│   └── workflows/
│       └── deploy.yml        # Pipeline CI/CD
├── Dockerfile                # Multi-stage build
├── docker-compose.yml        # Servicio frontend
├── nginx.conf                # Configuración Nginx
└── src/                      # Código fuente React

## Correr localmente con Docker

```bash
docker compose up --build
```

El frontend quedará disponible en `http://localhost`

## Variables de entorno

| Variable | Descripción |
|---|---|
| VITE_API_URL | URL del backend API |

## Pipeline CI/CD

El pipeline se activa automáticamente al hacer push a la rama `deploy`:

1. Construye la imagen Docker con multi-stage build
2. Compila el proyecto React con Vite
3. Sirve los archivos estáticos con Nginx Alpine
4. Publica la imagen en Docker Hub
5. Despliega automáticamente en la instancia EC2 pública

## Arquitectura de despliegue

- El Frontend corre en una instancia EC2 en subred pública
- Es el único servicio accesible desde Internet
- Se comunica con el Backend a través de la subred privada
- La comunicación está controlada por Security Groups de AWS
