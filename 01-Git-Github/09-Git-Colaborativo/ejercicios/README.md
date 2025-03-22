# Ejercicios: Git como Herramienta Colaborativa

A continuación se presentan ejercicios prácticos que te ayudarán a dominar Git como herramienta para el trabajo en equipo.

## Ejercicio 1: Simulación de Flujo de Trabajo en Equipo

### Objetivo
Experimentar los flujos de trabajo de Git en un contexto de equipo simulado.

### Descripción
En este ejercicio, trabajarás con múltiples ramas y roles para simular el desarrollo colaborativo de una aplicación web simple.

### Pasos

1. **Preparación del repositorio**:
   ```bash
   # Crear un repositorio local
   mkdir equipo-colaborativo
   cd equipo-colaborativo
   git init
   
   # Crear estructura básica
   mkdir -p css js
   
   # Crear archivos iniciales
   echo "<!DOCTYPE html>
   <html>
   <head>
     <title>Proyecto Colaborativo</title>
     <link rel='stylesheet' href='css/styles.css'>
   </head>
   <body>
     <header>
       <h1>Proyecto del Equipo</h1>
     </header>
     <main>
       <div id='app'>
         <!-- Contenido de la aplicación -->
       </div>
     </main>
     <footer>
       <p>&copy; 2023 Equipo Colaborativo</p>
     </footer>
     <script src='js/app.js'></script>
   </body>
   </html>" > index.html
   
   echo "/* Estilos de la aplicación */
   body {
     font-family: Arial, sans-serif;
     margin: 0;
     padding: 0;
   }
   
   header, footer {
     background-color: #333;
     color: white;
     padding: 1rem;
     text-align: center;
   }
   
   main {
     padding: 2rem;
   }" > css/styles.css
   
   echo "// Código principal de la aplicación
   console.log('Aplicación inicializada');" > js/app.js
   
   # Commit inicial
   git add .
   git commit -m "feat: Estructura inicial del proyecto"
   
   # Crear rama de desarrollo
   git branch develop
   git checkout develop
   ```

2. **Simular trabajo en diferentes roles**:

   **Rol A: Desarrollador Frontend (Nueva característica)**
   ```bash
   # Crear rama para la característica
   git checkout -b feature/login-ui
   
   # Modificar archivos
   echo "/* Estilos de la aplicación */
   body {
     font-family: Arial, sans-serif;
     margin: 0;
     padding: 0;
   }
   
   header, footer {
     background-color: #333;
     color: white;
     padding: 1rem;
     text-align: center;
   }
   
   main {
     padding: 2rem;
   }
   
   /* Estilos para el formulario de login */
   .login-form {
     max-width: 400px;
     margin: 0 auto;
     padding: 2rem;
     border: 1px solid #ddd;
     border-radius: 5px;
   }
   
   .login-form input {
     display: block;
     width: 100%;
     margin-bottom: 1rem;
     padding: 0.5rem;
   }
   
   .login-form button {
     background-color: #4CAF50;
     color: white;
     padding: 0.5rem 1rem;
     border: none;
     cursor: pointer;
   }" > css/styles.css
   
   # Modificar HTML para añadir formulario
   sed -i '' 's/<div id='"'"'app'"'"'>/<div id='"'"'app'"'"'>\n        <form class="login-form">\n          <h2>Iniciar Sesión<\/h2>\n          <input type="email" placeholder="Email" required>\n          <input type="password" placeholder="Contraseña" required>\n          <button type="submit">Entrar<\/button>\n        <\/form>/' index.html
   
   # Commit los cambios
   git add .
   git commit -m "feat: añade interfaz de usuario para login"
   
   # Simular algunos commits adicionales
   echo "// Validación del formulario
   document.querySelector('.login-form').addEventListener('submit', function(e) {
     e.preventDefault();
     console.log('Formulario enviado');
   });" >> js/app.js
   git add js/app.js
   git commit -m "feat: añade validación básica del formulario"
   ```

   **Rol B: Desarrollador Backend (Otra característica)**
   ```bash
   # Volver a develop y crear otra rama
   git checkout develop
   git checkout -b feature/api-mock
   
   # Añadir archivo de API simulada
   mkdir -p js/api
   echo "// API Mock para simulación
   const api = {
     login: function(credentials) {
       return new Promise((resolve, reject) => {
         setTimeout(() => {
           if (credentials.email === 'usuario@ejemplo.com' && credentials.password === 'password123') {
             resolve({ success: true, user: { name: 'Usuario Demo' } });
           } else {
             reject({ success: false, message: 'Credenciales inválidas' });
           }
         }, 1000);
       });
     }
   };
   
   window.api = api;" > js/api/mock.js
   
   # Actualizar el HTML para incluir el nuevo script
   sed -i '' 's/<script src='"'"'js\/app.js'"'"'><\/script>/<script src='"'"'js\/api\/mock.js'"'"'><\/script>\n    <script src='"'"'js\/app.js'"'"'><\/script>/' index.html
   
   # Commit los cambios
   git add .
   git commit -m "feat: implementa mock de API para autenticación"
   ```

3. **Integración de cambios**:

   **Merge de características a develop**
   ```bash
   # Integrar la característica de UI
   git checkout develop
   git merge --no-ff feature/login-ui -m "feat: integra interfaz de usuario de login"
   
   # Intentar integrar la API mock (generará conflicto)
   git merge --no-ff feature/api-mock
   
   # Resolver conflicto en index.html manualmente
   # Editar index.html para incluir ambos cambios
   
   # Completar el merge
   git add index.html
   git commit -m "feat: integra mock de API resolviendo conflictos"
   ```

4. **Preparar una release**:
   ```bash
   # Crear rama de release
   git checkout -b release/1.0.0
   
   # Hacer ajustes finales
   echo "/* Estilos de la aplicación */
   body {
     font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
     margin: 0;
     padding: 0;
     background-color: #f8f9fa;
   }
   
   /* Resto de estilos... */" > css/styles.css
   git add css/styles.css
   git commit -m "style: mejora apariencia para release"
   
   # Integrar a main y develop
   git checkout main
   git merge --no-ff release/1.0.0 -m "chore: release versión 1.0.0"
   git tag -a v1.0.0 -m "Primera versión estable"
   
   git checkout develop
   git merge --no-ff release/1.0.0 -m "chore: integra cambios de release 1.0.0"
   
   # Eliminar rama de release
   git branch -d release/1.0.0
   ```

5. **Simular una corrección urgente**:
   ```bash
   # Crear hotfix desde main
   git checkout main
   git checkout -b hotfix/1.0.1
   
   # Corregir un problema
   sed -i '' 's/console.log('"'"'Formulario enviado'"'"');/console.log('"'"'Formulario enviado'"'"');\n    // Mostrar mensaje de carga\n    alert('"'"'Iniciando sesión...'"'"');/' js/app.js
   
   git add js/app.js
   git commit -m "fix: añade indicador visual durante el login"
   
   # Integrar a main y develop
   git checkout main
   git merge --no-ff hotfix/1.0.1 -m "fix: corrige experiencia de usuario en login"
   git tag -a v1.0.1 -m "Corrección de experiencia de usuario"
   
   git checkout develop
   git merge --no-ff hotfix/1.0.1 -m "fix: integra corrección de experiencia de usuario"
   
   # Eliminar rama de hotfix
   git branch -d hotfix/1.0.1
   ```

### Análisis
- Observa el flujo de trabajo GitFlow en acción
- Comprende cómo se gestionan los conflictos en un entorno colaborativo
- Analiza el historial de commits para seguir el desarrollo de características

### Preguntas para reflexionar
1. ¿Qué ventajas y desventajas encuentras en el flujo de trabajo GitFlow?
2. ¿Cómo se podrían evitar los conflictos experimentados durante la integración?
3. ¿De qué manera los mensajes de commit ayudaron a entender la evolución del proyecto?

## Ejercicio 2: Revisión de Código y Buenas Prácticas

### Objetivo
Practicar la revisión de código y aplicar buenas prácticas en mensajes de commit.

### Descripción
En este ejercicio, mejorarás un proyecto existente aplicando buenas prácticas de commits y simulando un proceso de revisión de código.

### Pasos

1. **Preparación del repositorio**:
   ```bash
   # Clonar el repositorio del ejercicio anterior o crear uno nuevo
   git clone ./equipo-colaborativo revision-codigo
   cd revision-codigo
   
   # Crear una rama para mejoras
   git checkout -b mejoras/codigo-limpio
   ```

2. **Mejora de código con buenos commits**:
   ```bash
   # Modificar estructura del proyecto
   mkdir -p src/{css,js,components}
   
   # Mover y reorganizar archivos
   mv css/styles.css src/css/
   mv js/app.js src/js/
   mv js/api/mock.js src/js/api.js
   
   # Actualizar referencias en index.html
   sed -i '' 's/css\/styles.css/src\/css\/styles.css/g' index.html
   sed -i '' 's/js\/api\/mock.js/src\/js\/api.js/g' index.html
   sed -i '' 's/js\/app.js/src\/js\/app.js/g' index.html
   
   # Commit con mensaje descriptivo
   git add .
   git commit -m "refactor(estructura): reorganiza archivos en patrón src

   - Mueve archivos CSS y JS a carpeta src
   - Renombra mock.js a api.js para mayor claridad
   - Actualiza referencias en index.html

   Este cambio facilita el mantenimiento y sigue estándares modernos de organización."
   ```

3. **Más mejoras con commits atómicos**:
   ```bash
   # Mejorar estilos
   echo "/**
    * Estilos principales de la aplicación
    * Versión: 1.1.0
    * Última actualización: $(date +"%Y-%m-%d")
    */

   :root {
     --color-primary: #4CAF50;
     --color-secondary: #333;
     --color-text: #212121;
     --color-background: #f8f9fa;
   }
   
   body {
     font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
     margin: 0;
     padding: 0;
     background-color: var(--color-background);
     color: var(--color-text);
   }
   
   header, footer {
     background-color: var(--color-secondary);
     color: white;
     padding: 1rem;
     text-align: center;
   }
   
   main {
     padding: 2rem;
     max-width: 1200px;
     margin: 0 auto;
   }
   
   /* Estilos para el formulario de login */
   .login-form {
     max-width: 400px;
     margin: 0 auto;
     padding: 2rem;
     border: 1px solid #ddd;
     border-radius: 5px;
     box-shadow: 0 2px 10px rgba(0,0,0,0.1);
   }
   
   .login-form input {
     display: block;
     width: 100%;
     margin-bottom: 1rem;
     padding: 0.5rem;
     border: 1px solid #ddd;
     border-radius: 4px;
   }
   
   .login-form button {
     background-color: var(--color-primary);
     color: white;
     padding: 0.5rem 1rem;
     border: none;
     border-radius: 4px;
     cursor: pointer;
     width: 100%;
   }
   
   .login-form button:hover {
     opacity: 0.9;
   }" > src/css/styles.css
   
   git add src/css/styles.css
   git commit -m "style: mejora diseño visual con variables CSS

   - Implementa sistema de variables para colores
   - Añade efectos hover y sombras
   - Mejora espaciado y márgenes
   
   Mejora la experiencia visual manteniendo consistencia de diseño."
   ```

   ```bash
   # Mejorar JavaScript
   echo "/**
    * API para autenticación de usuarios
    * Versión: 1.1.0
    */
   
   class AuthAPI {
     constructor() {
       this.endpoint = 'https://api.ejemplo.com/auth'; // Simulado
     }
   
     /**
      * Autentica a un usuario
      * @param {Object} credentials - Credenciales del usuario
      * @param {string} credentials.email - Email del usuario
      * @param {string} credentials.password - Contraseña del usuario
      * @returns {Promise} Promesa con resultado de autenticación
      */
     login(credentials) {
       console.log('Intentando autenticar con:', credentials.email);
       
       // SIMULACIÓN - En producción sería una llamada fetch real
       return new Promise((resolve, reject) => {
         setTimeout(() => {
           if (credentials.email === 'usuario@ejemplo.com' && credentials.password === 'password123') {
             resolve({ success: true, user: { name: 'Usuario Demo', role: 'user' } });
           } else {
             reject({ success: false, message: 'Credenciales inválidas' });
           }
         }, 1000);
       });
     }
   }
   
   // Exportar para uso global (en producción usar módulos ES)
   window.api = new AuthAPI();" > src/js/api.js
   
   git add src/js/api.js
   git commit -m "refactor(api): convierte API a clase con mejores prácticas

   - Usa clases ES6 para mejor organización 
   - Añade documentación JSDoc para métodos
   - Simula endpoint real para futura implementación
   
   Esta refactorización mejora la mantenibilidad y prepara el código para
   integración con backend real."
   ```

4. **Simular proceso de revisión de código**:
   ```bash
   # Crear un Pull Request (simulado en local)
   git checkout develop
   git checkout -b revision/mejoras-codigo
   git merge --no-ff mejoras/codigo-limpio -m "merge: integra mejoras de código para revisión"
   
   # Simular comentarios de revisión
   echo "/**
    * Comentarios de la revisión de código:
    * 
    * 1. Excelente trabajo en la refactorización a clases ES6
    * 2. Buena separación de responsabilidades
    * 3. Sugerencia: Considera usar módulos ES para imports/exports
    * 4. Pregunta: ¿Has considerado añadir manejo de errores?
    * 5. Aprobado con pequeñas sugerencias
    */
   " > revision-comments.md
   
   git add revision-comments.md
   git commit -m "docs: añade comentarios de revisión de código"
   ```

5. **Implementar cambios sugeridos en la revisión**:
   ```bash
   # Mejorar el código basado en comentarios
   echo "/**
    * Módulo principal de la aplicación
    * Versión: 1.1.0 
    */
   
   // Manejar el envío del formulario de login
   document.addEventListener('DOMContentLoaded', () => {
     const loginForm = document.querySelector('.login-form');
     const emailInput = loginForm.querySelector('input[type=\"email\"]');
     const passwordInput = loginForm.querySelector('input[type=\"password\"]');
     const submitButton = loginForm.querySelector('button[type=\"submit\"]');
     
     loginForm.addEventListener('submit', async function(e) {
       e.preventDefault();
       submitButton.disabled = true;
       submitButton.textContent = 'Iniciando sesión...';
       
       try {
         const credentials = {
           email: emailInput.value,
           password: passwordInput.value
         };
         
         const response = await window.api.login(credentials);
         alert(`Bienvenido, ${response.user.name}!`);
         // Redirigir o actualizar UI
       } catch (error) {
         alert(`Error: ${error.message || 'No se pudo iniciar sesión'}`);
         console.error('Error de autenticación:', error);
       } finally {
         submitButton.disabled = false;
         submitButton.textContent = 'Entrar';
       }
     });
   });" > src/js/app.js
   
   git add src/js/app.js
   git commit -m "feat: implementa manejo de errores y mejora UX

   - Añade manejo de excepciones con try/catch
   - Deshabilita botón durante la autenticación
   - Restaura el estado del botón al finalizar
   - Muestra mensajes adecuados al usuario
   
   Implementado según sugerencias de la revisión de código."
   ```

6. **Integrar los cambios revisados**:
   ```bash
   git checkout develop
   git merge --no-ff revision/mejoras-codigo -m "feat: integra mejoras de código con revisión

   - Reorganiza estructura del proyecto
   - Mejora sistema de estilos con variables CSS
   - Refactoriza API con clases ES6
   - Implementa mejor manejo de errores
   
   Closes #42"
   ```

### Análisis
- Observa cómo los mensajes de commit bien estructurados documentan el proyecto
- Analiza la efectividad del proceso de revisión para mejorar el código
- Evalúa cómo las buenas prácticas facilitan la comprensión del código

### Preguntas para reflexionar
1. ¿De qué manera los mensajes de commit detallados facilitan el entendimiento de la evolución del código?
2. ¿Cómo contribuye el proceso de revisión a la calidad del producto final?
3. ¿Qué ventajas aporta seguir convenciones como Conventional Commits?

## Entrega de la Práctica

Para completar estos ejercicios, deberás:

1. Crear un repositorio en GitHub con todo el historial de commits
2. Documentar en un archivo INFORME.md:
   - Capturas del historial de commits (`git log --graph --oneline --all`)
   - Capturas de la resolución de conflictos
   - Respuestas a las preguntas de reflexión
   - Conclusiones personales sobre el trabajo colaborativo con Git

## Recursos Adicionales

- [Atlassian: Comparing Git Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [Conventional Commits Specification](https://www.conventionalcommits.org/)
- [GitHub Flow Guide](https://guides.github.com/introduction/flow/)
- [Effective Code Reviews](https://www.evoketechnologies.com/blog/code-review-checklist-perform-effective-code-reviews/) 