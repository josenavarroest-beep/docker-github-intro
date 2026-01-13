# Introducción a GitHub y Docker

Información del Proyecto

**Autor**: José Navarro  
**Fecha**: Enero 2026  
**Objetivo**: Comprender el rol de GitHub en el desarrollo colaborativo y su relación con Docker para la gestión de aplicaciones contenerizadas.

 ¿Qué es GitHub?

GitHub es una plataforma de desarrollo colaborativo basada en **Git**, el sistema de control de versiones distribuido. Permite a desarrolladores de todo el mundo:

- **Almacenar código** en repositorios en la nube
- **Colaborar** en proyectos mediante pull requests y revisiones de código
- **Rastrear cambios** y versiones del código a lo largo del tiempo
- **Gestionar proyectos** con issues, project boards y wikis
- **Automatizar workflows** mediante GitHub Actions (CI/CD)

 Ventajas de GitHub

 Control de versiones robusto  
 Colaboración en tiempo real  
 Integración con múltiples herramientas de desarrollo  
 Comunidad global de desarrolladores  
 Hosting gratuito para proyectos open source  
 Documentación integrada (README, wikis)  

¿Qué es Docker?

Docker es una plataforma de **virtualización por contenedores** que permite empaquetar aplicaciones y sus dependencias en unidades estandarizadas llamadas **contenedores**.

Conceptos Clave de Docker

- **Contenedor**: Entorno aislado y ligero que contiene todo lo necesario para ejecutar una aplicación
- **Imagen**: Plantilla inmutable que define el contenedor
- **Dockerfile**: Archivo de texto con instrucciones para construir una imagen
- **Docker Hub**: Registro público de imágenes Docker (similar a GitHub para contenedores)

Beneficios de Docker

**Portabilidad**: "Funciona en mi máquina" ya no es un problema  
**Consistencia**: Mismo entorno en desarrollo, pruebas y producción  
**Eficiencia**: Contenedores más ligeros que máquinas virtuales  
**Escalabilidad**: Fácil replicación y orquestación  
**Aislamiento**: Aplicaciones independientes sin conflictos de dependencias  

---

Relación entre GitHub y Docker

GitHub y Docker son herramientas complementarias en el desarrollo moderno de software:

1. Versionado de Configuraciones

GitHub almacena `Dockerfiles` y archivos de configuración (`docker-compose.yml`), permitiendo:
- Rastrear cambios en la configuración de contenedores
- Colaborar en la definición de entornos
- Mantener un historial de modificaciones

2. CI/CD Automatizado

GitHub Actions puede:
- Construir imágenes Docker automáticamente
- Ejecutar pruebas en contenedores
- Publicar imágenes en Docker Hub o GitHub Container Registry
- Desplegar aplicaciones contenerizadas

**Ejemplo de workflow**:
```yaml
name: Docker Build and Push

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Build Docker image
        run: docker build -t mi-app:latest .
      - name: Push to Docker Hub
        run: docker push mi-app:latest
```

 3. Documentación y Colaboración

- **README.md** documenta cómo usar imágenes Docker del proyecto
- **Issues** reportan problemas en contenedores
- **Pull Requests** proponen mejoras en Dockerfiles

 4. GitHub Container Registry (ghcr.io)

GitHub ofrece su propio registro de contenedores integrado:
- Almacena imágenes Docker privadas o públicas
- Se integra con permisos de repositorio
- Permite distribuir contenedores junto al código

5. Entornos de Desarrollo Reproducibles

Con `Dockerfile` en GitHub:
- Cualquier colaborador puede recrear el entorno exacto
- Se eliminan las diferencias "funciona en mi máquina"
- Onboarding más rápido de nuevos desarrolladores

---

Workflow Típico: GitHub + Docker

```
1. Desarrollador escribe código
   ↓
2. Crea/Actualiza Dockerfile
   ↓
3. Commit y push a GitHub
   ↓
4. GitHub Actions ejecuta:
   - Construcción de imagen Docker
   - Tests en contenedor
   - Push a registro (Docker Hub/ghcr.io)
   ↓
5. Deployment automático en servidores
```

---

Ejemplo Práctico

Estructura de Proyecto

```
mi-proyecto/
├── README.md
├── Dockerfile
├── docker-compose.yml
├── .github/
│   └── workflows/
│       └── docker-build.yml
└── src/
    └── app.py
```

Dockerfile de Ejemplo

```dockerfile
# Imagen base
FROM python:3.11-slim

# Directorio de trabajo
WORKDIR /app

# Copiar dependencias
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copiar código
COPY src/ .

# Exponer puerto
EXPOSE 8000

# Comando de inicio
CMD ["python", "app.py"]
``` Docker Compose

```yaml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "8000:8000"
    volumes:
      - ./src:/app
    environment:
      - DEBUG=True

Conceptos Aprendidos

 GitHub
-  Control de versiones distribuido
-  Trabajo colaborativo mediante branches y PRs
-  Automatización con GitHub Actions
-  Almacenamiento de código y configuraciones
  
-  Virtualización por contenedores
-  Portabilidad de aplicaciones
-  Gestión de dependencias
-  Consistencia entre entornos

 Integración GitHub-Docker
-  Versionado de Dockerfiles
-  CI/CD para imágenes de contenedores
-  GitHub Container Registry
-  Entornos de desarrollo reproducibles

Recursos Adicionales

GitHub
- [Documentación oficial de GitHub](https://docs.github.com)
- [GitHub Actions](https://github.com/features/actions)
- [GitHub Container Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry)

Docker
- [Documentación oficial de Docker](https://docs.docker.com)
- [Docker Hub](https://hub.docker.com)
- [Docker Compose](https://docs.docker.com/compose)
- [Best practices para Dockerfiles](https://docs.docker.com/develop/dev-best-practices)

Tutoriales
- [GitHub Learning Lab](https://lab.github.com)
- [Docker Getting Started](https://docs.docker.com/get-started)

Conclusión

GitHub y Docker son herramientas fundamentales en el desarrollo moderno de software. Mientras GitHub gestiona el código fuente y facilita la colaboración, Docker asegura que las aplicaciones se ejecuten consistentemente en cualquier entorno. Su integración permite workflows automatizados que van desde el desarrollo hasta el despliegue en producción.

Contacto

**Nombre**: José Navarro  
**Email**: rolando.n562@gmail.com  
**GitHub**: [@josenavarroest-beep](https://github.com/josenavarroest-beep)

Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo `LICENSE` para más detalles.
