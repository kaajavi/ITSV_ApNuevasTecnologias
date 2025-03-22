# Ejercicios: Pull Requests, Issues y Actions

A continuación se presentan ejercicios prácticos para dominar el uso de Pull Requests, Issues y GitHub Actions en entornos colaborativos.

## Ejercicio 1: Gestión Completa con Issues

### Objetivo
Aprender a utilizar el sistema de Issues de GitHub para planificar y seguir el progreso de un proyecto.

### Descripción
En este ejercicio crearás y gestionarás Issues para organizar el desarrollo de una aplicación web simple, utilizando etiquetas, milestones y proyectos.

### Pasos

1. **Configuración del repositorio**:
   ```bash
   # Crear un nuevo repositorio local
   mkdir gestion-proyecto
   cd gestion-proyecto
   git init
   echo "# Proyecto de Gestión de Tareas" > README.md
   git add README.md
   git commit -m "commit inicial"
   
   # Subir a GitHub
   # (Primero crea un repositorio vacío en GitHub)
   git remote add origin https://github.com/tu-usuario/gestion-proyecto.git
   git push -u origin main
   ```

2. **Crear plantillas de Issues**:
   - En GitHub, ve a tu repositorio
   - Navega a Settings > Options > Features
   - Marca "Issues" si no está activado
   - Crea el directorio `.github/ISSUE_TEMPLATE/` en tu repositorio
   - Crea dos plantillas:
   
   `bug_report.md`:
   ```markdown
   ---
   name: Reporte de Bug
   about: Crea un reporte para ayudarnos a mejorar
   title: "[BUG] "
   labels: bug
   assignees: ''
   ---
   
   ## Descripción del Bug
   Una descripción clara y concisa del bug.
   
   ## Pasos para Reproducir
   1. Ir a '...'
   2. Hacer clic en '....'
   3. Ver el error
   
   ## Comportamiento Esperado
   Una descripción de lo que esperabas que ocurriera.
   
   ## Capturas de Pantalla
   Si aplica, añade capturas para explicar tu problema.
   
   ## Contexto Adicional
   Cualquier otra información sobre el problema.
   ```
   
   `feature_request.md`:
   ```markdown
   ---
   name: Solicitud de Funcionalidad
   about: Sugiere una idea para el proyecto
   title: "[FEATURE] "
   labels: enhancement
   assignees: ''
   ---
   
   ## Problema Relacionado
   ¿Tu solicitud de funcionalidad está relacionada con un problema? Descríbelo.
   
   ## Solución Deseada
   Una descripción clara y concisa de lo que quieres que ocurra.
   
   ## Alternativas Consideradas
   Cualquier solución o característica alternativa que hayas considerado.
   
   ## Contexto Adicional
   Cualquier otra información o capturas sobre la solicitud de funcionalidad.
   ```

3. **Configurar etiquetas personalizadas**:
   - En GitHub, ve a Issues > Labels
   - Crea las siguientes etiquetas:
     - `frontend`: Para tareas relacionadas con la interfaz
     - `backend`: Para tareas relacionadas con la lógica del servidor
     - `documentation`: Para tareas de documentación
     - `high-priority`: Para tareas urgentes
     - `good first issue`: Para tareas adecuadas para principiantes

4. **Crear milestones**:
   - En GitHub, ve a Issues > Milestones
   - Crea dos milestones:
     - "MVP (Producto Mínimo Viable)" con fecha de vencimiento en 2 semanas
     - "Versión 1.0" con fecha de vencimiento en 4 semanas

5. **Crear un tablero de proyecto**:
   - En GitHub, ve a Projects
   - Crea un nuevo proyecto de tipo "Board" (Kanban)
   - Configura las columnas: "To Do", "In Progress", "Review", "Done"
   - Configura la automatización para mover issues automáticamente

6. **Crear y gestionar issues**:
   - Crea al menos 6 issues utilizando las plantillas:
     - 2 bugs
     - 4 funcionalidades
   - Asigna etiquetas apropiadas
   - Asigna issues a los milestones
   - Añade los issues al tablero de proyecto
   - Cierra 2 issues como completados
   - Cierra 1 issue como "won't fix" (no se implementará)

### Análisis
- Observa cómo la estructura de etiquetas y milestones ayuda a organizar el trabajo
- Evalúa la efectividad del tablero de proyecto para visualizar el progreso
- Reflexiona sobre cómo las plantillas mejoran la consistencia de la información

### Preguntas para reflexionar
1. ¿Cómo ayudan las plantillas de issues a mejorar la comunicación en un equipo?
2. ¿Qué ventajas tiene el uso de milestones para la planificación de versiones?
3. ¿Cómo contribuye un sistema de etiquetas bien diseñado a la eficiencia del equipo?

## Ejercicio 2: Workflow Colaborativo con Pull Requests

### Objetivo
Dominar el flujo de trabajo basado en Pull Requests para contribuir a un proyecto colaborativo.

### Descripción
En este ejercicio simularás un entorno colaborativo, donde diferentes miembros del equipo contribuyen a un proyecto a través de Pull Requests.

### Pasos

1. **Preparar el proyecto base**:
   ```bash
   # Crea un nuevo repositorio
   mkdir proyecto-colaborativo
   cd proyecto-colaborativo
   git init
   
   # Crear estructura básica
   mkdir -p src css js
   echo "<!DOCTYPE html>
   <html>
   <head>
     <title>Proyecto Colaborativo</title>
     <link rel='stylesheet' href='css/style.css'>
   </head>
   <body>
     <header>
       <h1>Mi Proyecto</h1>
     </header>
     <main id='content'>
       <!-- Contenido aquí -->
     </main>
     <footer>
       <p>&copy; 2023 Mi Proyecto</p>
     </footer>
     <script src='js/app.js'></script>
   </body>
   </html>" > index.html
   
   echo "/* Estilos principales */" > css/style.css
   echo "// Código JavaScript principal" > js/app.js
   
   # Commit inicial
   git add .
   git commit -m "Estructura inicial del proyecto"
   
   # Subir a GitHub
   # (Primero crea un repositorio vacío en GitHub)
   git remote add origin https://github.com/tu-usuario/proyecto-colaborativo.git
   git push -u origin main
   
   # Crear rama de desarrollo
   git checkout -b develop
   git push -u origin develop
   ```

2. **Configurar protección de ramas**:
   - En GitHub, ve a Settings > Branches
   - Añade una regla de protección para la rama `main`:
     - Requerir pull request antes de hacer merge
     - Requerir aprobación de al menos 1 revisor
     - Opcional: Requerir status checks

3. **Simular Desarrollador 1: Implementar header**:
   ```bash
   # Crear una rama feature
   git checkout develop
   git pull
   git checkout -b feature/header
   
   # Modificar archivos
   echo "header {
     background-color: #333;
     color: white;
     padding: 1rem;
     text-align: center;
   }
   
   nav {
     display: flex;
     justify-content: center;
     background-color: #444;
     padding: 0.5rem;
   }
   
   nav a {
     color: white;
     margin: 0 15px;
     text-decoration: none;
   }" >> css/style.css
   
   # Modificar HTML para añadir navegación
   sed -i '' 's/<header>/<header>\n    <nav>\n      <a href="#home">Home<\/a>\n      <a href="#about">About<\/a>\n      <a href="#contact">Contact<\/a>\n    <\/nav>/' index.html
   
   # Commit y push
   git add .
   git commit -m "Implementa diseño de header y navegación"
   git push -u origin feature/header
   ```

4. **Crear Pull Request para feature/header**:
   - En GitHub, navega a tu repositorio
   - Verás un mensaje sobre tu rama recién subida, haz clic en "Compare & pull request"
   - Completa el PR con:
     - Título: "Implementación de header y navegación"
     - Descripción detallada explicando los cambios
     - Asigna un revisor (puedes asignarte a ti mismo para este ejercicio)
   - Crea el PR

5. **Simular Desarrollador 2: Implementar footer**:
   ```bash
   # Crear una rama feature
   git checkout develop
   git pull
   git checkout -b feature/footer
   
   # Modificar archivos
   echo "footer {
     background-color: #333;
     color: white;
     padding: 1rem;
     text-align: center;
     margin-top: 2rem;
   }
   
   footer a {
     color: #9cf;
   }" >> css/style.css
   
   # Modificar HTML para mejorar el footer
   sed -i '' 's/<footer>/<footer>\n    <div class="footer-links">\n      <a href="terms.html">Terms<\/a> | \n      <a href="privacy.html">Privacy<\/a>\n    <\/div>/' index.html
   
   # Commit y push
   git add .
   git commit -m "Mejora el diseño del footer y añade enlaces"
   git push -u origin feature/footer
   ```

6. **Crear Pull Request para feature/footer**:
   - Crea un PR de manera similar al anterior
   - Dirígelo a la rama `develop`

7. **Revisión y aprobación de PRs**:
   - Revisa ambos PRs
   - Deja comentarios constructivos
   - Solicita cambios si es necesario
   - Finalmente, aprueba y fusiona ambos PRs en `develop`

8. **Crear PR para fusionar develop en main**:
   - Crea un PR para fusionar todos los cambios de `develop` a `main`
   - Revisa todos los cambios acumulados
   - Aprueba y fusiona

### Análisis
- Observa cómo los Pull Requests facilitan la revisión de código
- Evalúa la utilidad de las ramas protegidas para mantener la calidad
- Comprueba cómo las discusiones en los PRs mejoran el código final

### Preguntas para reflexionar
1. ¿Qué ventajas tiene revisar el código a través de Pull Requests frente a hacer commits directos?
2. ¿Cómo contribuye la protección de ramas a la estabilidad del proyecto?
3. ¿Qué estrategias de ramificación serían adecuadas para diferentes tamaños de equipos?

## Ejercicio 3: Automatización con GitHub Actions

### Objetivo
Implementar flujos de trabajo automatizados utilizando GitHub Actions para mejorar la calidad del código y la productividad.

### Descripción
En este ejercicio configurarás diferentes workflows de GitHub Actions para automatizar tareas comunes como linting, pruebas y despliegue de un sitio web simple.

### Pasos

1. **Preparar un proyecto web sencillo**:
   ```bash
   # Crear un nuevo repositorio
   mkdir actions-demo
   cd actions-demo
   git init
   
   # Crear estructura del proyecto
   echo "<!DOCTYPE html>
   <html>
   <head>
     <title>GitHub Actions Demo</title>
     <link rel='stylesheet' href='styles.css'>
   </head>
   <body>
     <h1>GitHub Actions Demo</h1>
     <p>Esta página demostrará el uso de GitHub Actions para CI/CD.</p>
     <script src='script.js'></script>
   </body>
   </html>" > index.html
   
   echo "body {
     font-family: Arial, sans-serif;
     max-width: 800px;
     margin: 0 auto;
     padding: 2rem;
   }" > styles.css
   
   echo "console.log('GitHub Actions funcionando correctamente');" > script.js
   
   # Añadir archivos para linting
   echo '{
     "parserOptions": {
       "ecmaVersion": 2021
     },
     "rules": {
       "semi": ["error", "always"],
       "quotes": ["error", "single"]
     }
   }' > .eslintrc.json
   
   echo '*.log
   node_modules/
   .DS_Store' > .gitignore
   
   # Inicializar npm y añadir dependencias
   npm init -y
   npm install --save-dev eslint
   
   # Modificar package.json para añadir scripts
   sed -i '' 's/"scripts": {/"scripts": {\n    "lint": "eslint *.js",\n    "test": "echo \\"Tests passed\\" && exit 0",/' package.json
   
   # Commit inicial
   git add .
   git commit -m "Configuración inicial del proyecto"
   
   # Subir a GitHub
   # (Primero crea un repositorio vacío en GitHub)
   git remote add origin https://github.com/tu-usuario/actions-demo.git
   git push -u origin main
   ```

2. **Configurar un workflow para linting**:
   - Crea el directorio para workflows:
   ```bash
   mkdir -p .github/workflows
   ```
   
   - Crea un archivo para el workflow de linting:
   ```bash
   echo 'name: Lint Code

   on:
     push:
       branches: [ main ]
     pull_request:
       branches: [ main ]
   
   jobs:
     lint:
       runs-on: ubuntu-latest
       
       steps:
       - uses: actions/checkout@v3
       
       - name: Set up Node.js
         uses: actions/setup-node@v3
         with:
           node-version: "16"
           
       - name: Install dependencies
         run: npm install
         
       - name: Run ESLint
         run: npm run lint
   ' > .github/workflows/lint.yml
   
   # Commit y push
   git add .github/workflows/lint.yml
   git commit -m "Añade workflow de GitHub Actions para linting"
   git push
   ```

3. **Provocar un error de linting para probar el workflow**:
   ```bash
   # Crear una rama para el cambio
   git checkout -b fix/lint-error
   
   # Modificar el archivo JS con un error de estilo
   echo 'console.log("Este código tiene comillas dobles y sin punto y coma")' > script.js
   
   # Commit y push
   git add script.js
   git commit -m "Añade código con error de estilo"
   git push -u origin fix/lint-error
   ```
   
   - Crea un Pull Request para esta rama
   - Observa cómo falla la verificación de linting
   - Corrige el error:
   
   ```bash
   echo 'console.log(\'Este código tiene comillas simples y punto y coma\');' > script.js
   git add script.js
   git commit -m "Corrige errores de estilo"
   git push
   ```
   
   - Observa cómo ahora pasa la verificación
   - Aprueba y fusiona el PR

4. **Configurar un workflow para desplegar a GitHub Pages**:
   ```bash
   echo 'name: Deploy to GitHub Pages

   on:
     push:
       branches: [ main ]
   
   jobs:
     deploy:
       runs-on: ubuntu-latest
       
       steps:
       - uses: actions/checkout@v3
       
       - name: Deploy
         uses: JamesIves/github-pages-deploy-action@v4
         with:
           branch: gh-pages
           folder: .
   ' > .github/workflows/deploy.yml
   
   # Commit y push
   git add .github/workflows/deploy.yml
   git commit -m "Añade workflow para desplegar a GitHub Pages"
   git push
   ```
   
   - Activa GitHub Pages en tu repositorio:
     - Ve a Settings > Pages
     - Selecciona la rama `gh-pages` como origen
   
   - Haz un cambio en el sitio para probar el despliegue:
   ```bash
   git checkout main
   echo "<p>Actualizado automáticamente con GitHub Actions</p>" >> index.html
   git add index.html
   git commit -m "Actualiza contenido del sitio"
   git push
   ```
   
   - Observa el workflow en acción y verifica que el sitio se actualiza

5. **Crear un workflow personalizado para notificaciones**:
   ```bash
   echo 'name: Notificación de Issues

   on:
     issues:
       types: [opened, closed, reopened]
   
   jobs:
     notify:
       runs-on: ubuntu-latest
       
       steps:
       - name: Registrar actividad de issues
         run: |
           echo "Se ha ${{ github.event.action }} un issue:"
           echo "Título: ${{ github.event.issue.title }}"
           echo "Por usuario: ${{ github.event.issue.user.login }}"
           echo "URL: ${{ github.event.issue.html_url }}"
   ' > .github/workflows/issue-notification.yml
   
   # Commit y push
   git add .github/workflows/issue-notification.yml
   git commit -m "Añade workflow para notificaciones de issues"
   git push
   ```
   
   - Crea un nuevo issue en el repositorio para probar el workflow
   - Verifica la ejecución del workflow en la pestaña "Actions"

### Análisis
- Observa cómo los workflows automatizan tareas repetitivas
- Evalúa el impacto en la calidad del código y el tiempo ahorrado
- Considera otras automatizaciones que podrían ser útiles

### Preguntas para reflexionar
1. ¿Qué otras tareas en tu proceso de desarrollo podrían automatizarse con GitHub Actions?
2. ¿Cómo afecta la integración continua a la calidad general del proyecto?
3. ¿Qué ventajas tiene la automatización del despliegue frente al despliegue manual?

## Entrega de la Práctica

Para completar estos ejercicios, deberás:

1. Crear los repositorios mencionados en GitHub
2. Implementar todos los pasos descritos
3. Documentar tu proceso con capturas de pantalla que muestren:
   - Los Issues creados y gestionados
   - Los Pull Requests y sus revisiones
   - Las ejecuciones de GitHub Actions
4. Crear un informe que incluya:
   - Respuestas a las preguntas de reflexión
   - Desafíos que encontraste durante el proceso
   - Cómo resolverías los problemas encontrados

## Recursos Adicionales

- [GitHub Skills: Introducción a GitHub](https://github.com/skills/introduction-to-github)
- [GitHub Skills: Revisar Pull Requests](https://github.com/skills/review-pull-requests)
- [GitHub Learning Lab: Gestión de Merge Conflicts](https://lab.github.com/githubtraining/managing-merge-conflicts)
- [GitHub Docs: Creando workflows de GitHub Actions](https://docs.github.com/es/actions/quickstart) 