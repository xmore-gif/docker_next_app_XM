# Docker Next App

Aplicación web desarrollada con Next.js y contenedorizada utilizando Docker para garantizar un entorno de desarrollo reproducible, aislado y portable.

## Tecnologías utilizadas

- Next.js 16.4.3
- React 19.3.0
- Node.js 20 Alpine
- Docker
- Docker Desktop
- TypeScript
- Tailwind CSS

## Estructura de Docker

El proyecto utiliza un Dockerfile multi-stage con tres etapas:

1. **deps:** instala las dependencias mediante `npm ci`.
2. **builder:** copia el proyecto y ejecuta `npm run build`.
3. **runner:** utiliza la aplicación compilada y ejecuta Next.js en modo producción.

Se utiliza `node:20-alpine` debido a que la versión de Next.js utilizada requiere Node.js 20.9.0 o superior.

## Construcción de la imagen

Desde la raíz del proyecto:

```bash
docker build -t docker-next-app .
```

## Ejecución del contenedor

```bash
docker run -d --name docker-next-app-container -p 3000:3000 docker-next-app
```

## Verificar el contenedor

```bash
docker ps
```

El contenedor debe aparecer ejecutándose y exponiendo el puerto:

```text
0.0.0.0:3000->3000/tcp
```

## Verificar la aplicación

Abrir en el navegador:

```text
http://localhost:3000
```

La aplicación Next.js debe mostrarse correctamente.

## Detener el contenedor

```bash
docker stop docker-next-app-container
```

## Eliminar el contenedor

```bash
docker rm docker-next-app-container
```

## .dockerignore

El proyecto incluye un archivo `.dockerignore` para excluir archivos y carpetas innecesarios del contexto de construcción, incluyendo:

- `node_modules`
- `.next`
- `.env`
- archivos temporales
- logs
- `.git`
- archivos de cobertura

Esto permite reducir el contexto enviado a Docker y mantener una construcción más limpia y eficiente.

## Resultado

La aplicación fue construida exitosamente mediante Docker y ejecutada dentro de un contenedor, siendo accesible desde el navegador mediante `http://localhost:3000`.