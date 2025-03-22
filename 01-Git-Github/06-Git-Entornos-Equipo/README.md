# Git en Entornos de Equipo

## Introducción

El uso de Git en entornos colaborativos y profesionales requiere conocimientos y prácticas que van más allá del uso básico individual. En esta sección, exploraremos las mejores prácticas, herramientas y metodologías para utilizar Git efectivamente en equipos de desarrollo, abordando desafíos comunes y estableciendo flujos de trabajo productivos.

## Objetivos de Aprendizaje
- Comprender la importancia de establecer convenciones y estándares en equipos
- Dominar las estrategias de ramificación para el desarrollo colaborativo
- Implementar técnicas para asegurar la calidad del código
- Conocer metodologías para la integración y despliegue continuo con Git
- Resolver eficientemente conflictos y problemas comunes en entornos de equipo

## Contenido

### Convenciones y Estándares

#### Estándares de Mensajes de Commit

Los mensajes de commit consistentes mejoran la comunicación y la comprensión del historial del proyecto:

1. **Conventional Commits**: Un estándar popular que sigue este formato:
   ```
   <tipo>[ámbito opcional]: <descripción>
   
   [cuerpo opcional]
   
   [nota(s) al pie opcional(es)]
   ```

   Donde `tipo` puede ser:
   - `feat`: Nueva característica
   - `fix`: Corrección de error
   - `docs`: Cambios en documentación
   - `style`: Cambios de formato que no afectan el código
   - `refactor`: Refactorización de código
   - `test`: Adición o corrección de pruebas
   - `chore`: Tareas de mantenimiento

2. **Beneficios**:
   - Generación automática de changelogs
   - Determinar semánticamente las versiones
   - Comunicar la naturaleza de los cambios a colaboradores
   - Facilitar la navegación por el historial

3. **Herramientas**:
   - `commitlint`: Verifica que los mensajes sigan el estándar
   - `commitizen`: Asistente interactivo para crear mensajes

#### Configuración de Git a Nivel de Equipo

Establecer configuraciones consistentes mejora la colaboración:

1. **Archivos de configuración compartidos**:
   - `.gitattributes`: Define cómo Git maneja archivos específicos
   - `.gitignore`: Lista archivos que no deben ser versionados
   - `.gitconfig`: Configuraciones compartidas

2. **Ejemplo de `.gitattributes`**:
   ```
   # Auto detect text files and perform LF normalization
   * text=auto
   
   # Explicitly declare text files you want to always be normalized
   *.c text
   *.h text
   
   # Declare files that will always have CRLF line endings on checkout
   *.sln text eol=crlf
   
   # Denote all files that are binary and should not be modified
   *.png binary
   *.jpg binary
   ```

3. **Hooks compartidos**:
   - Crear directorio `.githooks/` en el repositorio
   - Configurar el equipo para usar estos hooks:
     ```bash
     git config core.hooksPath .githooks
     ```

### Estrategias de Ramificación para Equipos

#### GitFlow

Una metodología establecida para manejo de ramas:

1. **Ramas principales**:
   - `main` (o `master`): Código en producción
   - `develop`: Código de desarrollo integrado

2. **Ramas de soporte**:
   - `feature/*`: Para nuevas características
   - `release/*`: Preparación para liberaciones
   - `hotfix/*`: Correcciones urgentes
   - `bugfix/*`: Corrección de errores no urgentes

3. **Flujo básico**:
   - Las características se desarrollan en ramas `feature/`
   - Se integran a `develop`
   - Cuando se prepara un lanzamiento, se crea una rama `release/`
   - La rama `release/` permite correcciones finales y se fusiona a `main` y `develop`
   - Los problemas en producción se corrigen en ramas `hotfix/` y se fusionan a `main` y `develop`

4. **Comandos de GitFlow**:
   ```bash
   # Instalar gitflow (ejemplo en Ubuntu)
   apt-get install git-flow
   
   # Inicializar gitflow en un repositorio
   git flow init
   
   # Iniciar una nueva característica
   git flow feature start nueva-funcionalidad
   
   # Finalizar una característica
   git flow feature finish nueva-funcionalidad
   
   # Crear una versión
   git flow release start 1.0.0
   
   # Finalizar una versión
   git flow release finish 1.0.0
   ```

#### GitHub Flow

Un flujo más simple orientado a despliegue continuo:

1. **Conceptos clave**:
   - Solo la rama `main` contiene código estable
   - Cualquier cambio requiere una rama nueva
   - Las ramas se crean a partir de `main`
   - Se realizan Pull Requests para revisar cambios
   - Una vez aprobados, se fusionan a `main`
   - Se despliega inmediatamente tras la fusión

2. **Ventajas**:
   - Simplicidad
   - Ideal para despliegue continuo
   - Reduce la complejidad de múltiples ramas
   - Enfocado en revisión de código

#### Trunk-Based Development

Una metodología centrada en integración continua:

1. **Principios**:
   - Todos trabajan principalmente en la rama principal (trunk)
   - Se crean ramas de corta duración para cambios
   - Integración frecuente a trunk (al menos diariamente)
   - Uso de feature flags para código incompleto

2. **Ventajas**:
   - Reduce problemas de integración
   - Favorece la integración continua
   - Simplifica el flujo de trabajo
   - Mejora la velocidad de entrega

3. **Desafíos**:
   - Requiere disciplina de equipo
   - Necesita buena cobertura de pruebas
   - Exige alta calidad de código

#### Comparación de Estrategias

| Estrategia | Complejidad | Casos de uso ideales | Tamaño de equipo |
|------------|-------------|----------------------|------------------|
| GitFlow | Alta | Proyectos con ciclos de lanzamiento definidos | Medianos a grandes |
| GitHub Flow | Media | Proyectos con despliegue continuo | Pequeños a medianos |
| Trunk-Based | Baja | Proyectos con alta automatización e integración continua | Cualquier tamaño |

### Control de Calidad del Código

#### Code Reviews

La revisión de código es fundamental para mantener la calidad:

1. **Prácticas recomendadas**:
   - Revisiones pequeñas y frecuentes
   - Enfocarse en la lógica, no solo en el estilo
   - Utilizar listas de verificación estandarizadas
   - Ser constructivo y respetuoso
   - Establecer estándares claros

2. **Herramientas de GitHub para revisiones**:
   - Revisión de Pull Requests
   - Comentarios en línea
   - Sugerencias de código
   - Revisiones requeridas para proteger ramas

3. **Proceso de revisión**:
   - El autor explica el propósito del cambio
   - Los revisores examinan el código
   - Se discuten alternativas
   - Se aprueban o solicitan cambios
   - El autor implementa los cambios sugeridos

#### Integración con Herramientas de Calidad

Git puede integrarse con diversas herramientas para asegurar la calidad:

1. **Linters y formatters**:
   - ESLint/Prettier (JavaScript)
   - Black/Flake8 (Python)
   - RuboCop (Ruby)
   - Configurados como pre-commit hooks

2. **Pruebas automatizadas**:
   - Configuración de CI/CD para ejecutar pruebas
   - Pruebas unitarias, integración, end-to-end
   - Cobertura de código integrada en PR

3. **Análisis estático de código**:
   - SonarQube
   - CodeClimate
   - Integración con Pull Requests

4. **Pre-commit hooks**:
   ```bash
   # Ejemplo de pre-commit hook para JavaScript
   #!/bin/sh
   
   FILES=$(git diff --cached --name-only --diff-filter=ACM | grep '\.js$')
   if [ -n "$FILES" ]; then
     echo "Ejecutando ESLint..."
     npx eslint $FILES
     if [ $? -ne 0 ]; then
       echo "ESLint encontró errores. Por favor corrígelos antes de hacer commit."
       exit 1
     fi
   fi
   ```

### CI/CD con Git

#### Integración Continua

La integración continua verifica automáticamente los cambios:

1. **Principios**:
   - Integración frecuente al tronco principal
   - Verificación automática de cada cambio
   - Retroalimentación rápida
   - Reparación inmediata de problemas

2. **Configuración con GitHub Actions**:
   ```yaml
   name: CI
   
   on:
     push:
       branches: [ main, develop ]
     pull_request:
       branches: [ main, develop ]
   
   jobs:
     build:
       runs-on: ubuntu-latest
       
       steps:
       - uses: actions/checkout@v3
       - name: Set up environment
         # Configuración del entorno
       - name: Install dependencies
         # Instalación de dependencias
       - name: Run tests
         # Ejecución de pruebas
       - name: Build
         # Proceso de compilación
   ```

#### Despliegue Continuo

El despliegue continuo automatiza la entrega de software:

1. **Principios**:
   - Automatización completa del despliegue
   - Despliegue frecuente a producción
   - Cambios pequeños e incrementales
   - Capacidad de rollback

2. **Flujo de trabajo típico**:
   - El código se fusiona a la rama principal
   - Se ejecutan pruebas automáticas
   - Se construyen artefactos
   - Se despliega a entorno de staging
   - Se ejecutan pruebas adicionales
   - Se despliega a producción

3. **Configuración con GitHub Actions**:
   ```yaml
   name: Deploy to Production
   
   on:
     push:
       branches: [ main ]
   
   jobs:
     deploy:
       runs-on: ubuntu-latest
       
       steps:
       - uses: actions/checkout@v3
       - name: Build
         # Construir la aplicación
       - name: Deploy to staging
         # Desplegar a staging
       - name: Run integration tests
         # Ejecutar pruebas en staging
       - name: Deploy to production
         # Desplegar a producción
   ```

### Resolución de Problemas Comunes

#### Manejo de Conflictos

Los conflictos de fusión son inevitables en equipos:

1. **Prevención**:
   - Integración frecuente
   - Comunicación clara sobre áreas de trabajo
   - Cambios pequeños y enfocados
   - Estructura de código modular

2. **Procedimiento de resolución**:
   - Identificar archivos en conflicto: `git status`
   - Entender la causa del conflicto
   - Resolver manualmente editando los archivos
   - Marcar como resueltos: `git add <archivo>`
   - Completar la fusión: `git commit`

3. **Herramientas**:
   - Herramientas visuales: `git mergetool`
   - IDEs modernos con resolución integrada
   - Servicios de revisión de código

#### Reescritura de Historia Compartida

La reescritura de historia en ramas compartidas puede causar problemas:

1. **Regla general**: No reescribir historia que ya ha sido compartida

2. **Situaciones para evitar**:
   - `git rebase` en ramas publicadas
   - `git commit --amend` en commits publicados
   - `git push --force` (excepto en casos muy específicos)

3. **Alternativas seguras**:
   - Crear commits de corrección
   - Documentar los problemas
   - Uso de `git revert` para deshacer cambios

4. **Excepciones controladas**:
   - Pull Requests con regla de "rebase y actualizar"
   - Uso de `git push --force-with-lease` como precaución

#### Recuperación de Errores

Git ofrece varias formas de recuperación:

1. **RefLog: tu red de seguridad**:
   ```bash
   # Ver el reflog
   git reflog
   
   # Recuperar estado perdido
   git checkout HEAD@{2}
   
   # Crear una rama desde un estado anterior
   git branch recuperacion HEAD@{2}
   ```

2. **Recuperación de cambios perdidos**:
   ```bash
   # Ver commits "perdidos"
   git fsck --lost-found
   
   # Examinar contenido de blob perdido
   git show <hash>
   
   # Recuperar archivo eliminado del último commit
   git checkout HEAD^ -- ruta/al/archivo
   ```

3. **Revertir cambios incorrectos**:
   ```bash
   # Revertir un commit específico
   git revert <hash-commit>
   
   # Revertir un rango de commits
   git revert <hash-inicial>..<hash-final>
   ```

### Optimización y Rendimiento

#### Repositorios Grandes

Los proyectos grandes pueden presentar desafíos de rendimiento:

1. **Git LFS (Large File Storage)**:
   - Maneja archivos grandes eficientemente
   - Almacena punteros en lugar de contenido
   - Ideal para binarios, imágenes, videos

   ```bash
   # Instalar Git LFS
   git lfs install
   
   # Configurar extensiones para trackear
   git lfs track "*.psd"
   git lfs track "*.zip"
   
   # Verificar configuración
   git lfs status
   ```

2. **Shallow Clones**:
   - Clonan solo el historial reciente
   ```bash
   git clone --depth=1 https://github.com/usuario/repo.git
   ```

3. **Partial Clones**:
   - Filtran ciertos objetos durante el clonado
   ```bash
   git clone --filter=blob:none https://github.com/usuario/repo.git
   ```

#### Monorepos

Los monorepos (repositorios que contienen múltiples proyectos) requieren consideraciones especiales:

1. **Ventajas**:
   - Visibilidad completa del código
   - Refactorización global más fácil
   - Dependencias compartidas simplificadas
   - CI/CD unificado

2. **Desafíos**:
   - Tamaño y rendimiento
   - Granularidad de permisos
   - Complejidad de CI/CD

3. **Herramientas**:
   - Google's Bazel
   - Nx
   - Lerna (para JavaScript)
   - Optimizaciones específicas de Git

### Herramientas de Colaboración Avanzada

#### Herramientas de Revisión de Código

Existen diversas plataformas especializadas:

1. **Características comunes**:
   - Comentarios en línea
   - Discusiones enhebradas
   - Revisiones formales
   - Integración con CI/CD

2. **Plataformas populares**:
   - GitHub Pull Requests
   - GitLab Merge Requests
   - Gerrit
   - Crucible
   - Reviewable

#### Integración con Gestión de Proyectos

Git puede integrarse con herramientas de gestión:

1. **Integración con issue trackers**:
   - Jira
   - Trello
   - Asana
   - GitHub Issues
   - GitLab Issues

2. **Automatizaciones comunes**:
   - Cierre automático de issues mediante commits
   - Transiciones de estados por actividad de PR
   - Asignación de trabajo basada en ramas
   - Reportes de actividad y progreso

#### Análisis del Repositorio

El análisis de patrones ayuda a mejorar procesos:

1. **Métricas útiles**:
   - Frecuencia de commit
   - Tamaño de commits
   - Tiempo de integración
   - Tasa de errores por commit
   - Distribución de trabajo

2. **Herramientas**:
   - Git Insights
   - GitPrime
   - Code Climate Velocity
   - GitHub Insights
   - GitStats

### Seguridad

#### Firma de Commits

La firma criptográfica verifica la autenticidad:

1. **Configuración de GPG**:
   ```bash
   # Generar clave GPG
   gpg --full-generate-key
   
   # Listar claves
   gpg --list-secret-keys --keyid-format LONG
   
   # Configurar Git para usar la clave
   git config --global user.signingkey <ID-DE-CLAVE>
   
   # Habilitar firma por defecto
   git config --global commit.gpgsign true
   ```

2. **Firma de commits**:
   ```bash
   # Firmar un commit
   git commit -S -m "Mensaje del commit firmado"
   
   # Verificar firmas
   git log --show-signature
   ```

3. **Configuración en plataformas**:
   - Añadir clave pública a GitHub/GitLab
   - Habilitar verificación de firmas
   - Requerir commits firmados en ramas protegidas

#### Control de Acceso

La gestión de permisos es crucial:

1. **Niveles típicos de permisos**:
   - Lectura: Clonar y ver código
   - Escritura: Push a ciertas ramas
   - Administración: Configurar repositorio

2. **Estrategias comunes**:
   - Protección de ramas principales
   - Revisiones obligatorias
   - Permisos granulares por directorio (GitLab)
   - CODEOWNERS para áreas específicas

3. **Ejemplo de CODEOWNERS**:
   ```
   # Propietarios predeterminados para todo el repositorio
   *       @equipo-principal
   
   # Propietarios de la documentación
   /docs/  @equipo-documentacion
   
   # Propietarios del backend
   /src/api/  @equipo-backend
   
   # Propietarios del frontend
   /src/ui/  @equipo-frontend
   ```

## Ejercicios

Para poner en práctica estos conceptos, dirígete a la carpeta [ejercicios](./ejercicios/) donde encontrarás actividades diseñadas para trabajar con Git en entornos de equipo.

## Recursos Adicionales

- [Pro Git: Capítulo Sobre Ramificación](https://git-scm.com/book/es/v2/Ramificaciones-en-Git-Flujos-de-Trabajo-Ramificados)
- [Conventional Commits](https://www.conventionalcommits.org/es/v1.0.0/)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Documentación de GitFlow](https://nvie.com/posts/a-successful-git-branching-model/)
- [Trunk Based Development](https://trunkbaseddevelopment.com/)
- [Git Hooks](https://git-scm.com/docs/githooks)
- [Git LFS](https://git-lfs.github.com/) 