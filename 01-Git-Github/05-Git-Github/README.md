# GitHub y Colaboración

## Introducción

GitHub es una plataforma basada en la nube que amplía las capacidades de Git, permitiendo la colaboración entre desarrolladores a nivel global. Se ha convertido en el estándar de facto para el desarrollo colaborativo de software, alojando millones de repositorios tanto públicos como privados. En esta sección, aprenderemos a trabajar con GitHub y dominar las técnicas de colaboración que son fundamentales para el desarrollo de software moderno.

## Objetivos de Aprendizaje
- Comprender qué es GitHub y sus principales características
- Dominar el flujo de trabajo de GitHub para colaboración
- Utilizar Pull Requests para revisar y contribuir código
- Gestionar problemas (issues) y proyectos
- Configurar y utilizar GitHub Actions para CI/CD básico
- Aprender buenas prácticas para la colaboración en proyectos

## Contenido

### ¿Qué es GitHub?

GitHub es una plataforma de alojamiento de código que proporciona:

1. **Alojamiento de repositorios Git**: Almacenamiento en la nube para tus repositorios.
2. **Interfaz web**: Para gestionar y visualizar tus repositorios.
3. **Herramientas de colaboración**: Pull requests, issues, proyectos, wikis, etc.
4. **Integración y despliegue continuos**: A través de GitHub Actions.
5. **Visibilidad y descubrimiento**: Facilita encontrar proyectos y contribuir a ellos.

GitHub no es sólo un servicio de alojamiento; es un ecosistema completo que fomenta prácticas de desarrollo colaborativo y abierto.

#### Alternativas a GitHub

Aunque GitHub es la plataforma más popular, existen alternativas como:

- **GitLab**: Ofrece CI/CD integrado y puede hospedarse en servidores propios.
- **Bitbucket**: De Atlassian, con integración cercana con Jira y otras herramientas de Atlassian.
- **Gitea/Gogs**: Alternativas ligeras y de código abierto, autoalojadas.

### Configuración de GitHub

#### Creación de una cuenta

Para empezar a usar GitHub:

1. Visita [github.com](https://github.com/) y crea una cuenta
2. Elige un plan (el plan gratuito ofrece repositorios públicos ilimitados)
3. Verifica tu dirección de correo electrónico

#### Configuración de la autenticación

GitHub soporta múltiples métodos de autenticación:

1. **HTTPS con token de acceso personal**:
   ```bash
   # Configurar credenciales para no tener que ingresar usuario/token cada vez
   git config --global credential.helper store
   # O para cache temporal
   git config --global credential.helper cache
   ```

2. **SSH**:
   ```bash
   # Generar clave SSH si no tienes una
   ssh-keygen -t ed25519 -C "tu_email@ejemplo.com"
   
   # Iniciar el agente SSH
   eval "$(ssh-agent -s)"
   
   # Añadir tu clave privada al agente
   ssh-add ~/.ssh/id_ed25519
   
   # Copiar la clave pública para añadirla a GitHub
   cat ~/.ssh/id_ed25519.pub
   ```
   
   Luego, añade esta clave en GitHub: Settings > SSH and GPG keys > New SSH key

#### Perfil de GitHub

Tu perfil de GitHub es tu carta de presentación:

- **Completa tu biografía**: Un pequeño resumen sobre ti y tus habilidades
- **Añade foto de perfil**: Preferiblemente una foto profesional
- **Crea un README de perfil**: Un repositorio especial con tu nombre de usuario que se muestra en tu perfil
- **Pinned repositories**: Destaca tus mejores proyectos

### Flujo de Trabajo con GitHub

GitHub promueve un flujo de trabajo específico, conocido como "GitHub Flow":

1. **Crear una rama**: Para cada nueva característica o corrección
2. **Realizar cambios**: Hacer commits en esa rama
3. **Crear un Pull Request**: Para solicitar que los cambios se integren
4. **Revisar código**: Discusión y posibles ajustes
5. **Merge**: Integración de los cambios en la rama principal

#### Operaciones Básicas

Trabajar con repositorios remotos en GitHub:

```bash
# Clonar un repositorio
git clone https://github.com/usuario/repositorio.git

# Ver repositorios remotos
git remote -v

# Añadir un remoto
git remote add origin https://github.com/usuario/repositorio.git

# Cambiar URL del remoto
git remote set-url origin https://github.com/usuario/nuevo-repo.git

# Subir cambios
git push origin main

# Traer cambios
git pull origin main
```

#### Sincronización con Forks

Un "fork" es una copia personal de un repositorio ajeno:

```bash
# Añadir el repositorio original como remoto
git remote add upstream https://github.com/propietario-original/repo.git

# Verificar remotos
git remote -v

# Traer cambios del repositorio original
git fetch upstream

# Fusionar cambios a tu rama principal local
git checkout main
git merge upstream/main

# Empujar a tu fork
git push origin main
```

### Pull Requests

Los Pull Requests (PRs) son el mecanismo principal para colaborar en GitHub.

#### Creación de un Pull Request

1. **Desde la interfaz web**:
   - Navega a tu repositorio
   - Cambia a la rama que contiene tus cambios
   - Haz clic en "Contribute" y luego "Open pull request"
   - Completa la descripción y crea el PR

2. **Desde la línea de comandos (con la CLI de GitHub)**:
   ```bash
   # Instalar GitHub CLI si no la tienes
   # Mac: brew install gh
   # Windows: scoop install gh
   # Linux: apt install gh
   
   # Autenticarse
   gh auth login
   
   # Crear PR
   gh pr create --base main --head tu-rama
   ```

#### Anatomía de un Pull Request

Un PR efectivo debe incluir:

- **Título claro**: Breve descripción de lo que hace
- **Descripción detallada**: Qué, por qué y cómo se implementaron los cambios
- **Referencias a issues**: Usando #número-de-issue
- **Capturas de pantalla** (si aplica): Especialmente para cambios visuales
- **Pasos para probar**: Cómo verificar que los cambios funcionan

#### Revisión de código

La revisión es fundamental para la calidad del código:

- **Comentarios**: Sugiere mejoras o pide aclaraciones
- **Aprobación**: Indica que los cambios están listos para integrar
- **Solicitud de cambios**: Indica que se necesitan modificaciones
- **Conversaciones**: Discusiones sobre implementaciones específicas

#### Fusionando un Pull Request

Existen tres estrategias para fusionar un PR:

1. **Merge commit**: Crea un commit adicional que une las historias
   ```bash
   gh pr merge --merge
   ```

2. **Squash and merge**: Combina todos los commits en uno solo
   ```bash
   gh pr merge --squash
   ```

3. **Rebase and merge**: Aplica los commits individuales en la rama destino
   ```bash
   gh pr merge --rebase
   ```

### Issues y Proyectos

#### Gestión de Issues

Los issues son la forma de rastrear tareas, mejoras y bugs:

- **Creación de issues**: Con título, descripción, etiquetas, asignados
- **Plantillas de issues**: Para estandarizar la información requerida
- **Etiquetas (labels)**: Categorizan los issues (bug, enhancement, etc.)
- **Hitos (milestones)**: Agrupan issues relacionados con una fecha objetivo
- **Asignados (assignees)**: Responsables de resolver el issue

```bash
# Crear un issue desde la CLI
gh issue create --title "Título del issue" --body "Descripción detallada"

# Listar issues
gh issue list

# Ver un issue específico
gh issue view 123
```

#### Tableros de Proyectos

GitHub Projects permite organizar el trabajo:

- **Vistas**: Kanban (tablero), tabla, calendario
- **Automatización**: Mover issues basado en su estado
- **Campos personalizados**: Prioridad, estimación, etc.
- **Relación con issues y PRs**: Vinculación automática

### GitHub Actions

GitHub Actions permite automatizar flujos de trabajo directamente en GitHub.

#### Conceptos Básicos

- **Workflows**: Procesos automatizados configurados en el repositorio
- **Eventos**: Desencadenantes que inician workflows (push, PR, etc.)
- **Jobs**: Conjunto de pasos que se ejecutan en una máquina virtual
- **Actions**: Bloques de código reutilizables para tareas comunes
- **Runners**: Servidores que ejecutan los jobs

#### Configuración de un Workflow Simple

Los workflows se definen en archivos YAML en el directorio `.github/workflows/`:

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '16'
        
    - name: Install dependencies
      run: npm install
      
    - name: Run tests
      run: npm test
```

#### Casos de Uso Comunes

GitHub Actions puede utilizarse para:

1. **Pruebas automáticas**: Ejecutar tests en cada push o PR
2. **Linting y verificación de estilo**: Asegurar consistencia en el código
3. **Construcción y despliegue**: Compilar y publicar automáticamente
4. **Publicación de paquetes**: Actualizar npm, PyPI, Docker Hub, etc.
5. **Notificaciones**: Integrar con Slack, email u otros servicios

### Características Adicionales de GitHub

#### GitHub Pages

Alojamiento gratuito de sitios web estáticos desde tus repositorios:

1. Configuración básica:
   - Crea un repositorio nombrado `username.github.io`
   - Añade contenido HTML/CSS/JS
   - Tu sitio estará disponible en `https://username.github.io`

2. Para proyectos individuales:
   - Habilita GitHub Pages en la configuración del repositorio
   - Elige la rama y carpeta fuente
   - El sitio estará en `https://username.github.io/repository`

#### GitHub Discussions

Foros integrados para preguntas, ideas y conversaciones:

- **Categorías**: Preguntas, ideas, anuncios, etc.
- **Formato**: Soporte para markdown, código, imágenes
- **Reacciones y votos**: Para identificar contenido valioso
- **Marcar como respuesta**: Para preguntas resueltas

#### GitHub Wikis

Documentación colaborativa para tu proyecto:

- **Páginas vinculadas**: Sistema completo de documentación
- **Formato Markdown**: Fácil de escribir y leer
- **Historial de cambios**: Control de versiones para la documentación
- **Permisos**: Configurable para permitir ediciones de colaboradores

### Buenas Prácticas para la Colaboración

#### Documentación del Proyecto

Un proyecto bien documentado es más accesible para nuevos colaboradores:

1. **README.md**: Descripción del proyecto, instalación, uso básico
2. **CONTRIBUTING.md**: Guía para contribuidores
3. **CODE_OF_CONDUCT.md**: Normas de comportamiento
4. **CHANGELOG.md**: Historial de cambios
5. **LICENSE**: Licencia del proyecto

#### Estrategias de Ramificación

Elige una estrategia de ramificación adecuada:

1. **GitHub Flow**: Simple, adecuado para despliegue continuo
2. **GitFlow**: Más estructurado, con ramas de desarrollo, características y versiones
3. **Trunk-Based Development**: Enfocado en integración continua con la rama principal

#### Comunicación Efectiva

La comunicación clara es esencial:

1. **Mensajes de commit descriptivos**: Explica qué y por qué
2. **Descripciones detalladas en PRs e issues**: Proporciona contexto
3. **Código autodocumentado**: Nombres claros de variables y funciones
4. **Comentarios donde sea necesario**: Explica el "por qué", no el "qué"

#### Revisión de Código Constructiva

Al revisar código de otros:

1. **Sé respetuoso**: Critica el código, no a la persona
2. **Sé específico**: "Esta variable podría llamarse X para mayor claridad"
3. **Explica el razonamiento**: No solo digas qué cambiar, sino por qué
4. **Sugiere alternativas**: Ofrece soluciones, no solo críticas

## Ejercicios

Para poner en práctica estos conceptos, dirígete a la carpeta [ejercicios](./ejercicios/) donde encontrarás actividades que te ayudarán a dominar GitHub y la colaboración en equipos de desarrollo.

## Recursos Adicionales

- [GitHub Docs](https://docs.github.com/es): Documentación oficial de GitHub
- [GitHub Skills](https://skills.github.com/): Cursos interactivos oficiales
- [GitHub Guides](https://guides.github.com/): Guías oficiales sobre características específicas
- [Pro Git Book: GitHub Chapter](https://git-scm.com/book/en/v2/GitHub-Account-Setup-and-Configuration)
- [GitHub CLI Manual](https://cli.github.com/manual/): Documentación de la herramienta de línea de comandos 