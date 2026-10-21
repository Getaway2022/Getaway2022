<div align="center">

# Nexo Store

Tienda full-stack con Next.js, Spring Boot y PostgreSQL. Incluye catálogo, carrito, favoritos, pedidos y panel administrativo.

<img src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white" alt="Next.js"/>
<img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript"/>
<img src="https://img.shields.io/badge/Spring%20Boot-Java%2017-6DB33F?style=for-the-badge&logo=springboot&logoColor=white" alt="Spring Boot, Java 17"/>
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL"/>
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker"/>

<br/><br/>

<a href="https://nexo-store-roan.vercel.app"><img src="https://img.shields.io/badge/Ver%20tienda-nexo--store--roan.vercel.app-000000?style=for-the-badge&logo=vercel&logoColor=white" alt="Ver tienda"/></a>

</div>

---

## Aplicación desplegada

- Tienda: [https://nexo-store-roan.vercel.app](https://nexo-store-roan.vercel.app)
- API: [https://nexo-store-gfqu.onrender.com/api](https://nexo-store-gfqu.onrender.com/api)
- Panel administrativo: [https://nexo-store-roan.vercel.app/admin/login](https://nexo-store-roan.vercel.app/admin/login)

El frontend Next.js está desplegado en Vercel. El backend Spring Boot está en Render (Docker, plan gratuito) y la base de datos PostgreSQL en Neon. Las credenciales administrativas se configuran como variables privadas en Render y no deben almacenarse en el repositorio.

> El backend está en el plan gratuito de Render: si estuvo inactivo, la primera carga puede tardar unos 50 segundos.

## Funcionalidades

- Catálogo de productos tecnológicos y gaming (teclados, mouse, memorias, monitores y accesorios).
- Carrito de compras y favoritos.
- Pedidos.
- Panel administrativo: gestión de productos y pedidos.
- Carga inicial de 64 productos de demostración.
- Verificaciones automáticas (lint, build y pruebas) con GitHub Actions en cada push y pull request.

## Tecnologías

| Capa | Tecnologías | Despliegue |
|---|---|---|
| Frontend | Next.js, TypeScript | Vercel |
| Backend | Java 17, Spring Boot | Render |
| Datos | PostgreSQL | Neon |
| Infraestructura | Docker Compose, GitHub Actions | |

## Capturas

<!--
Sube tus capturas reales a docs/ y descomenta este bloque:

<p align="center">
  <img src="docs/catalogo.png" width="48%" alt="Catálogo"/>
  <img src="docs/carrito.png" width="48%" alt="Carrito de compras"/>
</p>
<p align="center">
  <img src="docs/admin-productos.png" width="48%" alt="Gestión de productos"/>
  <img src="docs/admin-pedidos.png" width="48%" alt="Gestión de pedidos"/>
</p>
-->

## Variables de producción

Vercel requiere esta variable de tipo `Config`:

```env
NEXT_PUBLIC_API_URL=https://nexo-store-gfqu.onrender.com/api
```

El servicio del backend en Render requiere:

```env
SPRING_PROFILES_ACTIVE=prod
SPRING_DATASOURCE_URL=jdbc:postgresql://<host-de-neon>/<base_de_datos>?sslmode=require
SPRING_DATASOURCE_USERNAME=<usuario-de-neon>
SPRING_DATASOURCE_PASSWORD=<contraseña-de-neon>
APP_JWT_SECRET=<secreto-aleatorio-de-al-menos-64-caracteres>
APP_ADMIN_EMAIL=<correo-del-administrador>
APP_ADMIN_PASSWORD=<contraseña-segura>
APP_CORS_ALLOWED_ORIGINS=https://nexo-store-roan.vercel.app
```

La conexión a Neon usa SSL (`sslmode=require`); no publiques la cadena de conexión. `NEXT_PUBLIC_API_URL` debe terminar en `/api`. Después de modificar una variable `NEXT_PUBLIC_*`, es necesario volver a desplegar el frontend porque su valor se incorpora durante la compilación.

## Desarrollo local

Requisitos: Node.js 22 y Java 17.

```powershell
Copy-Item frontend/.env.example frontend/.env.local
cd frontend
npm.cmd ci
npm.cmd run dev
```

En otra terminal:

```powershell
cd backend
mvn spring-boot:run
```

Frontend: `http://localhost:3000`. API: `http://localhost:8080/api`.

## Producción con Docker

1. Copia `.env.example` como `.env`.
2. Sustituye todos los valores de ejemplo por secretos aleatorios y el dominio real.
3. No confirmes `.env` en Git.
4. Ejecuta `docker compose up -d --build`.
5. Comprueba `docker compose ps` y `curl http://localhost/api/health`.

La base de datos no está expuesta a Internet. Los datos persisten en el volumen `postgres_data`.

## Catálogo

La primera ejecución sobre una base vacía carga 64 productos de demostración. Después se administran desde `/admin/products`; no se deben editar directamente en PostgreSQL ni en Oracle Cloud.

El cargador inicial no modifica una base que ya contiene productos.

## Verificación

```powershell
cd frontend
npm.cmd run lint
npm.cmd run build

cd ../backend
mvn test
```

GitHub Actions repite estas comprobaciones en cada push y pull request.

## Documentación

- [Despliegue en Oracle Cloud](docs/oracle-cloud-deploy.md)
- [Contrato del backend](frontend/BACKEND_CONTRACT.md)
- [Créditos de imágenes](frontend/CREDITS.md)

## Autor

**Andrés Junior Gamio Patricio** · Estudiante de Ingeniería de Sistemas, UNMSM

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/andres-junior-gamio-patricio-206267430/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/Getaway2022)
