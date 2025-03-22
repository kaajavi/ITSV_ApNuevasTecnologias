# Ejercicios: GitHub y Colaboración

Este conjunto de ejercicios está diseñado para que practiques y domines las habilidades esenciales para colaborar en proyectos de desarrollo utilizando GitHub. A través de estos ejercicios, aprenderás a gestionar repositorios, trabajar con Pull Requests, manejar Issues y utilizar herramientas de automatización.

## Ejercicio 1: Configuración y Gestión de Repositorios

### Objetivo
Familiarizarte con la creación y configuración de repositorios en GitHub, y establecer las bases para una colaboración efectiva.

### Descripción
En este ejercicio, crearás un repositorio desde cero, lo configurarás adecuadamente y prepararás la documentación esencial para facilitar la colaboración.

### Pasos

1. **Crear y configurar un repositorio**:
   - Inicia sesión en GitHub y crea un nuevo repositorio público llamado "proyecto-colaborativo"
   - Añade una descripción breve: "Repositorio para practicar colaboración en GitHub"
   - Inicializa el repositorio con un archivo README
   - Añade un archivo .gitignore para el lenguaje de tu preferencia (ej. Python, JavaScript)
   - Selecciona una licencia (ej. MIT)

2. **Configurar el repositorio localmente**:
   ```bash
   # Clona el repositorio
   git clone https://github.com/tu-usuario/proyecto-colaborativo.git
   cd proyecto-colaborativo
   ```

3. **Crear estructura básica de archivos**:
   - Crea una carpeta `src/` para el código fuente
   - Crea una carpeta `docs/` para documentación
   - Dentro de `src/`, crea un archivo básico según el lenguaje elegido (ej. `main.py`, `index.js`)

4. **Mejorar la documentación**:
   - Edita el README.md para incluir:
     - Título y descripción del proyecto
     - Requisitos e instalación
     - Instrucciones de uso
     - Sección de "Cómo contribuir"
   
   - Crea un archivo CONTRIBUTING.md con guías para los contribuidores:
     - Proceso para crear issues
     - Proceso para enviar pull requests
     - Convenciones de código y commit
     - Proceso de revisión

5. **Añadir una plantilla para issues**:
   - Crea el directorio `.github/ISSUE_TEMPLATE/`
   - Añade un archivo `bug_report.md` con campos para:
     - Descripción del bug
     - Pasos para reproducirlo
     - Comportamiento esperado
     - Capturas de pantalla
     - Entorno (navegador, sistema operativo)

6. **Añadir una plantilla para pull requests**:
   - Crea el archivo `.github/pull_request_template.md` con campos para:
     - Descripción de los cambios
     - Tipo de cambio (feature, fix, etc.)
     - Issues relacionados
     - Checklist de tareas completadas

7. **Configurar protección de rama**:
   - En GitHub, ve a Settings > Branches
   - Añade una regla para proteger la rama `main`
   - Requiere revisiones de pull requests antes de hacer merge
   - Requiere que las pruebas pasen antes de hacer merge (si aplica)

8. **Subir todos los cambios**:
   ```bash
   git add .
   git commit -m "Configura estructura inicial del repositorio"
   git push origin main
   ```

### Preguntas de reflexión

1. ¿Por qué es importante tener documentación completa (README, CONTRIBUTING) en un proyecto colaborativo?
2. ¿Cómo ayudan las plantillas de issues y pull requests a mejorar la colaboración?
3. ¿Qué beneficios aporta la protección de ramas en un proyecto colaborativo?

## Ejercicio 2: Flujo de Trabajo con Pull Requests

### Objetivo
Dominar el proceso de creación, revisión y fusión de Pull Requests siguiendo el flujo de trabajo de GitHub.

### Descripción
En este ejercicio, simularás un flujo de trabajo colaborativo implementando nuevas características en ramas separadas y utilizando Pull Requests para incorporarlas al proyecto.

### Pasos

1. **Implementar una nueva característica**:
   ```bash
   # Crea una nueva rama
   git checkout -b feature/nueva-funcionalidad
   
   # Realiza cambios en el código (ejemplo con Python)
   # Añade un archivo src/funcionalidad.py con una función simple
   
   # Añade y comete los cambios
   git add src/funcionalidad.py
   git commit -m "Añade nueva funcionalidad"
   
   # Envía la rama al repositorio remoto
   git push -u origin feature/nueva-funcionalidad
   ```

2. **Crear un Pull Request**:
   - Ve a GitHub y navega a tu repositorio
   - Deberías ver un mensaje sugiriendo crear un Pull Request para tu rama recién subida
   - Haz clic en "Compare & pull request"
   - Completa la plantilla de PR con información detallada
   - Asígnate a ti mismo como revisor (en un proyecto real serían otros colaboradores)
   - Crea el Pull Request

3. **Revisar el código**:
   - En la página del Pull Request, ve a la pestaña "Files changed"
   - Añade comentarios a líneas específicas simulando una revisión:
     - Sugiere mejoras en el código
     - Haz preguntas sobre la implementación
     - Señala posibles problemas

4. **Responder a la revisión**:
   - Vuelve a tu entorno local y realiza cambios basados en la revisión
   ```bash
   # Realiza los cambios necesarios
   
   # Añade y comete los cambios
   git add src/funcionalidad.py
   git commit -m "Mejora la implementación según revisión"
   
   # Envía los cambios
   git push origin feature/nueva-funcionalidad
   ```

5. **Fusionar el Pull Request**:
   - Vuelve a GitHub y al Pull Request
   - Verifica que los cambios se hayan actualizado
   - Aprueba la revisión (como si fueras otro revisor)
   - Fusiona el Pull Request usando el método "squash and merge"
   - Escribe un mensaje de commit descriptivo para el squash

6. **Sincronizar el repositorio local**:
   ```bash
   git checkout main
   git pull origin main
   ```

7. **Crear un segundo Pull Request con conflictos**:
   ```bash
   # Crea otra rama
   git checkout -b feature/otra-funcionalidad
   
   # Modifica el mismo archivo que modificaste anteriormente
   # (esto generará un conflicto potencial)
   
   # Añade y comete los cambios
   git add src/funcionalidad.py
   git commit -m "Añade otra funcionalidad"
   
   # Envía la rama
   git push -u origin feature/otra-funcionalidad
   ```

8. **Resolver conflictos en el Pull Request**:
   - Crea un nuevo Pull Request en GitHub
   - Observa que GitHub indica que hay conflictos
   - Puedes resolver los conflictos directamente en GitHub o localmente:
   
   Para resolverlos localmente:
   ```bash
   git checkout main
   git pull origin main
   git checkout feature/otra-funcionalidad
   git merge main
   # Resuelve los conflictos en tu editor
   git add .
   git commit -m "Resuelve conflictos con main"
   git push origin feature/otra-funcionalidad
   ```

9. **Finalizar el segundo Pull Request**:
   - Una vez resueltos los conflictos, el PR debería estar listo para fusionar
   - Fusiona usando el método "create a merge commit"
   - Observa la diferencia en el historial de commits en comparación con el squash

### Preguntas de reflexión

1. ¿Cuáles son las ventajas de desarrollar en ramas separadas y usar Pull Requests?
2. Compara los diferentes métodos de fusión (merge, squash, rebase). ¿Cuándo usarías cada uno?
3. ¿Qué estrategias puedes implementar para minimizar conflictos en el desarrollo colaborativo?

## Ejercicio 3: Gestión de Issues y Proyectos

### Objetivo
Aprender a utilizar el sistema de Issues de GitHub para rastrear tareas, bugs y mejoras, y organizar el trabajo utilizando Proyectos.

### Descripción
En este ejercicio, configurarás un sistema de seguimiento de tareas para tu proyecto utilizando Issues de GitHub y los organizarás con un tablero de Proyecto.

### Pasos

1. **Crear etiquetas personalizadas**:
   - En tu repositorio, ve a Issues > Labels
   - Crea las siguientes etiquetas:
     - `bug` (rojo): Problemas que necesitan ser corregidos
     - `enhancement` (azul): Nuevas características o mejoras
     - `documentation` (verde): Mejoras en la documentación
     - `good first issue` (verde claro): Buenas tareas para nuevos contribuidores
     - `priority-high` (naranja): Issues que requieren atención inmediata

2. **Crear hitos (milestones)**:
   - Ve a Issues > Milestones
   - Crea un hito llamado "Versión 1.0" con una fecha de vencimiento de dos semanas
   - Añade una descripción de los objetivos para esta versión

3. **Crear issues**:
   - Crea al menos 5 issues diferentes:
     - Un bug reportado
     - Dos mejoras de características
     - Una mejora de documentación
     - Una tarea de refactorización
   - Asigna etiquetas apropiadas a cada issue
   - Asigna todos los issues al hito "Versión 1.0"
   - Asígnate cada issue a ti mismo

4. **Configurar un proyecto de tipo tablero Kanban**:
   - Ve a tu perfil > Projects > New project
   - Selecciona la plantilla "Board"
   - Nombra el proyecto "Desarrollo Versión 1.0"
   - Conecta el proyecto a tu repositorio

5. **Configurar columnas y automatización**:
   - Configura las columnas: "Todo", "In Progress", "Review" y "Done"
   - Configura la automatización:
     - Los nuevos issues se añaden a "Todo"
     - Los PRs se mueven a "In Progress"
     - Los PRs aprobados se mueven a "Review"
     - Los issues cerrados y PRs fusionados se mueven a "Done"

6. **Añadir issues al proyecto**:
   - Añade todos los issues que creaste al proyecto
   - Organízalos en las columnas correspondientes

7. **Cerrar un issue mediante un commit**:
   - Selecciona uno de los issues (preferiblemente una tarea sencilla)
   - Crea una rama para resolverlo:
   ```bash
   git checkout -b fix/issue-numero
   
   # Haz los cambios necesarios para resolver el issue
   
   # Añade y comete los cambios, incluyendo el número del issue en el mensaje
   git add .
   git commit -m "Resuelve problema de X. Closes #1"
   
   # Envía los cambios
   git push -u origin fix/issue-numero
   ```
   
   - Crea un Pull Request y fusiona los cambios
   - Observa que el issue se cierra automáticamente cuando se fusiona el PR

8. **Añadir una nota al proyecto**:
   - En tu tablero de proyecto, añade una nota en la columna "Todo"
   - Escribe "Ideas para la próxima versión" y añade algunas ideas

9. **Crear vistas diferentes**:
   - Configura una vista adicional de tipo "Table"
   - Personaliza las columnas para mostrar título, etiquetas, asignados y estado

### Preguntas de reflexión

1. ¿Cómo ayuda un sistema organizado de issues y etiquetas a gestionar un proyecto?
2. ¿De qué manera los proyectos de GitHub mejoran la visibilidad del progreso?
3. ¿Qué ventajas tiene cerrar issues automáticamente mediante mensajes de commit?

## Ejercicio 4: GitHub Actions y Automatización

### Objetivo
Implementar flujos de trabajo automatizados utilizando GitHub Actions para mejorar la calidad del código y automatizar tareas repetitivas.

### Descripción
En este ejercicio, configurarás varios flujos de trabajo de GitHub Actions para automatizar verificaciones de código, pruebas y documentación.

### Pasos

1. **Configurar un flujo de trabajo básico de CI**:
   - Crea el directorio `.github/workflows/`
   - Crea un archivo `ci.yml` con el siguiente contenido (ajústalo según tu lenguaje):

   Para Python:
   ```yaml
   name: CI

   on:
     push:
       branches: [ main ]
     pull_request:
       branches: [ main ]

   jobs:
     test:
       runs-on: ubuntu-latest
       steps:
       - uses: actions/checkout@v3
       - name: Set up Python
         uses: actions/setup-python@v4
         with:
           python-version: '3.x'
       - name: Install dependencies
         run: |
           python -m pip install --upgrade pip
           if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
           pip install pytest flake8
       - name: Lint with flake8
         run: |
           flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
       - name: Test with pytest
         run: |
           pytest
   ```

   Para JavaScript (Node.js):
   ```yaml
   name: CI

   on:
     push:
       branches: [ main ]
     pull_request:
       branches: [ main ]

   jobs:
     test:
       runs-on: ubuntu-latest
       steps:
       - uses: actions/checkout@v3
       - name: Use Node.js
         uses: actions/setup-node@v3
         with:
           node-version: '16.x'
       - name: Install dependencies
         run: npm ci
       - name: Run linting
         run: npm run lint
       - name: Run tests
         run: npm test
   ```

2. **Preparar el código para CI**:
   - Si elegiste Python:
     - Crea un archivo `requirements.txt` con las dependencias
     - Añade algunos tests simples usando pytest
   - Si elegiste JavaScript:
     - Asegúrate de tener package.json con scripts para lint y test
     - Añade algunos tests simples usando Jest u otro framework

3. **Crear un flujo de trabajo para GitHub Pages**:
   - Crea un archivo `.github/workflows/pages.yml`:
   
   ```yaml
   name: Deploy to GitHub Pages

   on:
     push:
       branches: [ main ]
     workflow_dispatch:

   jobs:
     deploy:
       runs-on: ubuntu-latest
       steps:
       - uses: actions/checkout@v3
       - name: Set up dependencies
         run: |
           # Instala las dependencias necesarias para generar la documentación
           # (esto variará según tu lenguaje y herramientas)
       - name: Generate documentation
         run: |
           # Comandos para generar la documentación
           # Por ejemplo: mkdocs build, sphinx-build, etc.
           # Como ejemplo simple, podemos mover los archivos de docs/ a un directorio de salida
           mkdir -p build
           cp -r docs/* build/
       - name: Deploy to GitHub Pages
         uses: JamesIves/github-pages-deploy-action@v4
         with:
           folder: build
   ```

4. **Añadir documentación de ejemplo**:
   - En la carpeta `docs/`, añade algunos archivos markdown:
     - `index.md`: Página principal
     - `usage.md`: Instrucciones de uso
     - `api.md`: Documentación de API (si aplica)

5. **Configurar GitHub Pages**:
   - Ve a Settings > Pages
   - Configura como fuente la rama `gh-pages` (que será creada por el Action)

6. **Crear un flujo de trabajo para automatizar etiquetas en PRs**:
   - Crea un archivo `.github/workflows/labeler.yml`:
   
   ```yaml
   name: "Pull Request Labeler"
   
   on:
     pull_request:
       types: [opened, synchronize]
   
   jobs:
     label:
       runs-on: ubuntu-latest
       steps:
       - uses: actions/labeler@v4
         with:
           repo-token: "${{ secrets.GITHUB_TOKEN }}"
   ```

7. **Configurar reglas para el etiquetado automático**:
   - Crea un archivo `.github/labeler.yml`:
   
   ```yaml
   documentation:
     - docs/**/*
     - '**/*.md'
   
   source:
     - src/**/*
   
   tests:
     - tests/**/*
     - '**/*.test.js'
     - '**/*_test.py'
   
   dependencies:
     - package.json
     - requirements.txt
   ```

8. **Probar los flujos de trabajo**:
   - Realiza cambios en diferentes partes del repositorio
   - Crea PRs y observa cómo se aplican las etiquetas automáticamente
   - Verifica que las pruebas de CI se ejecuten correctamente
   - Comprueba que la documentación se publique en GitHub Pages

9. **Crear un informe de estado**:
   - Añade badges al README.md que muestren el estado de tus flujos de trabajo:
   
   ```markdown
   ![CI](https://github.com/tu-usuario/proyecto-colaborativo/actions/workflows/ci.yml/badge.svg)
   ![Pages](https://github.com/tu-usuario/proyecto-colaborativo/actions/workflows/pages.yml/badge.svg)
   ```

### Preguntas de reflexión

1. ¿De qué manera GitHub Actions mejora la calidad del código y la colaboración?
2. ¿Qué otras automatizaciones podrías implementar en un proyecto real?
3. ¿Cómo afecta la Integración Continua al proceso de desarrollo?

## Entrega de la Práctica

Para completar estos ejercicios, deberás:

1. Compartir los enlaces a los repositorios que creaste
2. Incluir capturas de pantalla de:
   - Pull Requests creados y fusionados
   - Issues gestionados en el tablero del proyecto
   - Flujos de trabajo de GitHub Actions en ejecución
3. Escribir un breve informe (máximo 2 páginas) respondiendo a las preguntas de reflexión
4. Opcionalmente, crear un video breve demostrando el flujo de trabajo que implementaste

## Recursos Adicionales

- [GitHub Skills](https://skills.github.com/): Cursos interactivos oficiales
- [GitHub Actions Marketplace](https://github.com/marketplace?type=actions): Acciones predefinidas para distintas tareas
- [GitHub CLI](https://cli.github.com/): Herramienta de línea de comandos para GitHub
- [GitHub Docs: GitHub Projects](https://docs.github.com/es/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects)
- [GitHub Docs: GitHub Actions](https://docs.github.com/es/actions) 