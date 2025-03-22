# Ejercicios: Flujo de Trabajo con Git

Este conjunto de ejercicios está diseñado para que practiques y domines los conceptos relacionados con el flujo de trabajo en Git. A través de estos ejercicios, aplicarás los comandos básicos, trabajarás con ramas, resolverás conflictos y explorarás herramientas avanzadas.

## Ejercicio 1: Comandos Básicos y Anatomía de un Proyecto

### Objetivo
Familiarizarte con los comandos diarios de Git y entender cómo se organizan los cambios a lo largo del tiempo.

### Descripción
En este ejercicio, crearás un pequeño proyecto y practicarás el ciclo básico de trabajo con Git: modificar, preparar y confirmar cambios. También aprenderás a visualizar y entender el historial de cambios.

### Pasos

1. Crea un nuevo directorio para el proyecto:
   ```bash
   mkdir mi-proyecto-git
   cd mi-proyecto-git
   ```

2. Inicializa un repositorio Git:
   ```bash
   git init
   ```

3. Crea un archivo README.md con el siguiente contenido:
   ```markdown
   # Mi Proyecto Git

   Este es un proyecto para practicar Git.
   ```

4. Añade y confirma este archivo:
   ```bash
   git add README.md
   git commit -m "Primer commit: Añade README"
   ```

5. Crea un archivo `index.html` con estructura básica HTML:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>Página de Prueba</title>
   </head>
   <body>
       <h1>Bienvenido a mi proyecto</h1>
   </body>
   </html>
   ```

6. Añade y confirma este archivo:
   ```bash
   git add index.html
   git commit -m "Añade página HTML básica"
   ```

7. Modifica el archivo `index.html` para añadir un párrafo:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>Página de Prueba</title>
   </head>
   <body>
       <h1>Bienvenido a mi proyecto</h1>
       <p>Esta es una página de prueba para Git.</p>
   </body>
   </html>
   ```

8. Visualiza los cambios antes de confirmarlos:
   ```bash
   git diff
   ```

9. Añade y confirma los cambios:
   ```bash
   git add index.html
   git commit -m "Añade párrafo explicativo"
   ```

10. Explora el historial de commits:
    ```bash
    git log
    git log --oneline
    git log --stat
    ```

11. Crea un archivo `styles.css` con contenido básico:
    ```css
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 20px;
        color: #333;
    }
    
    h1 {
        color: #0066cc;
    }
    ```

12. Modifica `index.html` para enlazar el CSS:
    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>Página de Prueba</title>
        <link rel="stylesheet" href="styles.css">
    </head>
    <body>
        <h1>Bienvenido a mi proyecto</h1>
        <p>Esta es una página de prueba para Git.</p>
    </body>
    </html>
    ```

13. Añade ambos cambios en un solo commit:
    ```bash
    git add index.html styles.css
    git commit -m "Añade estilos básicos"
    ```

14. Visualiza el log con un gráfico para ver la progresión lineal:
    ```bash
    git log --oneline --graph
    ```

### Preguntas de reflexión

1. ¿Qué información proporciona `git log` que resulta útil para entender la historia del proyecto?
2. ¿Por qué es importante hacer commits frecuentes y con mensajes descriptivos?
3. ¿Qué diferencias notas entre `git diff` y `git diff --staged`?

## Ejercicio 2: Trabajo con Ramas

### Objetivo
Aprender a crear y gestionar ramas para desarrollar funcionalidades en paralelo.

### Descripción
Practicarás el desarrollo de múltiples funcionalidades utilizando ramas independientes. Aprenderás a crear, fusionar y gestionar ramas.

### Pasos

1. Continúa con el repositorio del ejercicio anterior o crea uno nuevo.

2. Crea una nueva rama para desarrollar una nueva funcionalidad:
   ```bash
   git checkout -b feature/navbar
   ```

3. Modifica el archivo `index.html` para añadir una barra de navegación:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>Página de Prueba</title>
       <link rel="stylesheet" href="styles.css">
   </head>
   <body>
       <nav>
           <ul>
               <li><a href="#">Inicio</a></li>
               <li><a href="#">Acerca de</a></li>
               <li><a href="#">Contacto</a></li>
           </ul>
       </nav>
       <h1>Bienvenido a mi proyecto</h1>
       <p>Esta es una página de prueba para Git.</p>
   </body>
   </html>
   ```

4. Actualiza el archivo `styles.css` para estilizar la barra de navegación:
   ```css
   body {
       font-family: Arial, sans-serif;
       margin: 0;
       padding: 20px;
       color: #333;
   }
   
   h1 {
       color: #0066cc;
   }
   
   nav {
       background-color: #333;
       padding: 10px;
   }
   
   nav ul {
       list-style-type: none;
       margin: 0;
       padding: 0;
       display: flex;
   }
   
   nav li {
       margin-right: 20px;
   }
   
   nav a {
       color: white;
       text-decoration: none;
   }
   
   nav a:hover {
       text-decoration: underline;
   }
   ```

5. Añade y confirma tus cambios:
   ```bash
   git add index.html styles.css
   git commit -m "Añade barra de navegación"
   ```

6. Vuelve a la rama principal:
   ```bash
   git checkout main
   ```

7. Crea otra rama para desarrollar una funcionalidad diferente:
   ```bash
   git checkout -b feature/footer
   ```

8. Modifica `index.html` para añadir un pie de página:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>Página de Prueba</title>
       <link rel="stylesheet" href="styles.css">
   </head>
   <body>
       <h1>Bienvenido a mi proyecto</h1>
       <p>Esta es una página de prueba para Git.</p>
       <footer>
           <p>&copy; 2023 Mi Proyecto Git. Todos los derechos reservados.</p>
       </footer>
   </body>
   </html>
   ```

9. Actualiza `styles.css` para el pie de página:
   ```css
   body {
       font-family: Arial, sans-serif;
       margin: 0;
       padding: 20px;
       color: #333;
   }
   
   h1 {
       color: #0066cc;
   }
   
   footer {
       margin-top: 20px;
       padding: 10px;
       background-color: #f5f5f5;
       border-top: 1px solid #ddd;
       text-align: center;
       font-size: 0.8em;
   }
   ```

10. Añade y confirma los cambios:
    ```bash
    git add index.html styles.css
    git commit -m "Añade pie de página"
    ```

11. Vuelve a la rama principal:
    ```bash
    git checkout main
    ```

12. Fusiona la rama de la barra de navegación:
    ```bash
    git merge feature/navbar
    ```

13. Fusiona la rama del pie de página (esto debería generar un conflicto):
    ```bash
    git merge feature/footer
    ```

14. Resuelve el conflicto manualmente editando los archivos en conflicto:
    - Abre los archivos marcados como conflictivos
    - Busca los marcadores de conflicto (`<<<<<<<`, `=======`, `>>>>>>>`)
    - Edita para incluir tanto la barra de navegación como el pie de página
    - Guarda los archivos

15. Una vez resuelto el conflicto, marca los archivos como resueltos y completa la fusión:
    ```bash
    git add index.html styles.css
    git commit -m "Fusiona navbar y footer resolviendo conflictos"
    ```

16. Visualiza el historial con gráfico para ver cómo se han integrado las ramas:
    ```bash
    git log --oneline --graph --all
    ```

### Preguntas de reflexión

1. ¿Cuáles son las ventajas de desarrollar funcionalidades en ramas separadas?
2. ¿Por qué se produjeron conflictos al fusionar la segunda rama?
3. ¿Qué estrategias podrías implementar para minimizar conflictos en un equipo?

## Ejercicio 3: Estrategias de Fusión: Merge vs Rebase

### Objetivo
Comprender las diferencias entre merge y rebase, y cuándo usar cada estrategia.

### Descripción
En este ejercicio, experimentarás con diferentes estrategias de fusión para integrar cambios entre ramas. Aprenderás las ventajas y desventajas de cada enfoque.

### Pasos

1. Continúa con el repositorio del ejercicio anterior o crea uno nuevo.

2. Asegúrate de estar en la rama principal:
   ```bash
   git checkout main
   ```

3. Crea una rama para experimentar con merge:
   ```bash
   git checkout -b feature/contacto
   ```

4. Crea un archivo `contacto.html` con el siguiente contenido:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>Contacto - Mi Proyecto</title>
       <link rel="stylesheet" href="styles.css">
   </head>
   <body>
       <nav>
           <ul>
               <li><a href="index.html">Inicio</a></li>
               <li><a href="#">Acerca de</a></li>
               <li><a href="contacto.html">Contacto</a></li>
           </ul>
       </nav>
       <h1>Contacto</h1>
       <form>
           <div>
               <label for="nombre">Nombre:</label>
               <input type="text" id="nombre" name="nombre">
           </div>
           <div>
               <label for="email">Email:</label>
               <input type="email" id="email" name="email">
           </div>
           <div>
               <label for="mensaje">Mensaje:</label>
               <textarea id="mensaje" name="mensaje"></textarea>
           </div>
           <button type="submit">Enviar</button>
       </form>
       <footer>
           <p>&copy; 2023 Mi Proyecto Git. Todos los derechos reservados.</p>
       </footer>
   </body>
   </html>
   ```

5. Añade y confirma el archivo:
   ```bash
   git add contacto.html
   git commit -m "Añade página de contacto"
   ```

6. Vuelve a la rama principal y realiza un cambio:
   ```bash
   git checkout main
   ```

7. Actualiza el archivo `README.md`:
   ```markdown
   # Mi Proyecto Git

   Este es un proyecto para practicar Git.

   ## Páginas
   - Inicio
   - Contacto (próximamente)
   ```

8. Añade y confirma los cambios:
   ```bash
   git add README.md
   git commit -m "Actualiza README con las páginas del sitio"
   ```

9. Fusiona la rama feature/contacto usando merge normal:
   ```bash
   git merge feature/contacto
   ```

10. Observa el historial con el commit de fusión:
    ```bash
    git log --oneline --graph --all
    ```

11. Ahora vamos a probar rebase. Crea una nueva rama:
    ```bash
    git checkout -b feature/about
    ```

12. Crea un archivo `about.html`:
    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>Acerca de - Mi Proyecto</title>
        <link rel="stylesheet" href="styles.css">
    </head>
    <body>
        <nav>
            <ul>
                <li><a href="index.html">Inicio</a></li>
                <li><a href="about.html">Acerca de</a></li>
                <li><a href="contacto.html">Contacto</a></li>
            </ul>
        </nav>
        <h1>Acerca de</h1>
        <p>Este es un proyecto de prueba para aprender Git.</p>
        <footer>
            <p>&copy; 2023 Mi Proyecto Git. Todos los derechos reservados.</p>
        </footer>
    </body>
    </html>
    ```

13. Añade y confirma el archivo:
    ```bash
    git add about.html
    git commit -m "Añade página Acerca de"
    ```

14. Vuelve a la rama principal y haz otro cambio:
    ```bash
    git checkout main
    ```

15. Actualiza el README.md nuevamente:
    ```markdown
    # Mi Proyecto Git

    Este es un proyecto para practicar Git.

    ## Páginas
    - Inicio
    - Contacto
    - Acerca de (próximamente)
    ```

16. Añade y confirma los cambios:
    ```bash
    git add README.md
    git commit -m "Actualiza README con página Acerca de"
    ```

17. Vuelve a la rama feature/about:
    ```bash
    git checkout feature/about
    ```

18. En lugar de fusionar con merge, usa rebase:
    ```bash
    git rebase main
    ```

19. Vuelve a la rama principal y realiza un merge fast-forward:
    ```bash
    git checkout main
    git merge feature/about
    ```

20. Observa el historial y compara con el resultado anterior de merge:
    ```bash
    git log --oneline --graph --all
    ```

### Preguntas de reflexión

1. ¿Qué diferencias observas en el historial entre los cambios integrados con merge y los integrados con rebase?
2. ¿Cuáles son las ventajas y desventajas de cada enfoque?
3. ¿En qué situaciones preferirías usar merge y en cuáles rebase?

## Ejercicio 4: Gestión Avanzada

### Objetivo
Familiarizarte con herramientas avanzadas como stash, cherry-pick y rebase interactivo.

### Descripción
En este ejercicio, practicarás técnicas avanzadas para gestionar el código y el historial de tu repositorio.

### Pasos

#### Parte 1: Stash

1. Asegúrate de estar en la rama principal:
   ```bash
   git checkout main
   ```

2. Comienza a modificar el archivo `index.html` añadiendo un nuevo elemento:
   ```html
   <!-- Añade después del párrafo existente -->
   <div class="featured">
       <h2>Funcionalidades destacadas</h2>
       <ul>
           <li>Característica 1</li>
           <li>Característica 2</li>
       </ul>
   </div>
   ```

3. No hagas commit todavía. Imagina que necesitas cambiar urgentemente a otra tarea. Guarda tus cambios con stash:
   ```bash
   git stash save "Añadiendo sección de características destacadas"
   ```

4. Verifica que tu directorio de trabajo está limpio:
   ```bash
   git status
   ```

5. Crea una rama para solucionar un bug urgente:
   ```bash
   git checkout -b hotfix/navbar-link
   ```

6. Corrige un problema en `index.html`:
   ```bash
   # Abre index.html y asegúrate que el enlace "Acerca de" apunte al archivo correcto:
   # Cambia <li><a href="#">Acerca de</a></li> a:
   # <li><a href="about.html">Acerca de</a></li>
   ```

7. Añade y confirma la corrección:
   ```bash
   git add index.html
   git commit -m "Corrige enlace roto en la barra de navegación"
   ```

8. Vuelve a la rama principal y aplica la corrección:
   ```bash
   git checkout main
   git merge hotfix/navbar-link
   ```

9. Recupera tus cambios guardados en stash:
   ```bash
   git stash list
   git stash apply stash@{0}
   ```

10. Añade y confirma estos cambios:
    ```bash
    git add index.html
    git commit -m "Añade sección de características destacadas"
    ```

#### Parte 2: Cherry-pick

1. Crea una rama para experimentar:
   ```bash
   git checkout -b feature/experimento
   ```

2. Realiza varios commits:
   ```bash
   # Modifica README.md añadiendo una sección de instalación
   # Añade y confirma
   git add README.md
   git commit -m "Añade instrucciones de instalación"
   
   # Crea un archivo javascript.js con funcionalidad básica
   # Añade y confirma
   git add javascript.js
   git commit -m "Añade funcionalidad JavaScript básica"
   
   # Modifica index.html para incluir el script
   # Añade y confirma
   git add index.html
   git commit -m "Enlaza archivo JavaScript"
   ```

3. Vuelve a la rama principal:
   ```bash
   git checkout main
   ```

4. Supongamos que solo quieres el commit de las instrucciones de instalación. Identifica su hash:
   ```bash
   git log feature/experimento --oneline
   ```

5. Aplica solo ese commit específico a main:
   ```bash
   git cherry-pick <hash-del-commit-de-instalacion>
   ```

#### Parte 3: Rebase Interactivo

1. Crea una rama para practicar:
   ```bash
   git checkout -b feature/rebase-practica
   ```

2. Haz varios commits pequeños:
   ```bash
   # Commit 1: Añade un archivo nuevo
   echo "# Documentación" > docs.md
   git add docs.md
   git commit -m "Inicia documentación"
   
   # Commit 2: Añade más contenido
   echo -e "\n## Instalación\n\nInstrucciones de instalación..." >> docs.md
   git add docs.md
   git commit -m "Añade sección de instalación"
   
   # Commit 3: Corrige un error de ortografía
   # Edita el archivo para corregir algún error y confirma
   git add docs.md
   git commit -m "Corrige error de ortografía"
   
   # Commit 4: Añade más contenido
   echo -e "\n## Uso\n\nCómo usar la aplicación..." >> docs.md
   git add docs.md
   git commit -m "Añade sección de uso"
   ```

3. Usa rebase interactivo para limpiar y reorganizar estos commits:
   ```bash
   git rebase -i HEAD~4
   ```

4. En el editor que se abre:
   - Combina el commit de corrección ortográfica con el anterior usando `squash` o `fixup`
   - Reordena los commits si es necesario
   - Cambia el mensaje de algún commit usando `reword`
   - Guarda y cierra el editor

5. Observa el historial resultante:
   ```bash
   git log --oneline
   ```

### Preguntas de reflexión

1. ¿En qué situaciones el comando `stash` resulta útil en un flujo de trabajo real?
2. ¿Cuáles son los casos de uso apropiados para `cherry-pick`?
3. ¿Qué ventajas ofrece el rebase interactivo para mantener un historial de commits limpio?
4. ¿Qué precauciones deberías tomar al reescribir la historia con comandos como rebase?

## Entrega de la Práctica

Para completar estos ejercicios, deberás:

1. Crear un repositorio en GitHub para tus ejercicios
2. Subir el código resultante de cada ejercicio
3. Incluir capturas de pantalla de momentos clave (como la resolución de conflictos o el resultado de rebase)
4. Crear un archivo `REFLEXIONES.md` con tus respuestas a las preguntas de reflexión

El objetivo principal es que experimentes con los diferentes comandos y flujos de trabajo, entendiendo cómo y cuándo aplicar cada técnica.

## Recursos Adicionales

- [Atlassian Git Tutorial: Usando Ramas](https://www.atlassian.com/git/tutorials/using-branches)
- [Atlassian Git Tutorial: Reescribiendo la Historia](https://www.atlassian.com/git/tutorials/rewriting-history)
- [Visualizing Git: Herramienta Interactiva](https://git-school.github.io/visualizing-git/)
- [Learn Git Branching: Juego Interactivo](https://learngitbranching.js.org/) 