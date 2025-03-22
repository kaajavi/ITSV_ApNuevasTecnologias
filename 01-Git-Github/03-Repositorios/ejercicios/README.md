# Ejercicios: Repositorios en Git

Los siguientes ejercicios te ayudarán a practicar y comprender mejor la creación, configuración y sincronización de repositorios en Git.

## Ejercicio 1: Configuración Inicial de Git

### Objetivo
Configurar correctamente Git en tu computadora para garantizar que tus contribuciones sean correctamente identificadas.

### Descripción
En este ejercicio configurarás las opciones básicas de Git y personalizarás algunas opciones adicionales.

### Pasos

1. Configura tu identidad en Git:
   ```bash
   git config --global user.name "Tu Nombre Completo"
   git config --global user.email "tu.email@ejemplo.com"
   ```

2. Configura el editor predeterminado (elige uno):
   ```bash
   # Para Visual Studio Code
   git config --global core.editor "code --wait"
   
   # Para Sublime Text
   git config --global core.editor "subl -n -w"
   
   # Para Vim
   git config --global core.editor "vim"
   
   # Para Notepad++ (Windows)
   git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
   ```

3. Configura el nombre de la rama principal predeterminada:
   ```bash
   git config --global init.defaultBranch main
   ```

4. Configura algunas opciones útiles:
   ```bash
   # Colorear la salida de Git
   git config --global color.ui auto
   
   # Configurar la estrategia de pull (merge o rebase)
   git config --global pull.rebase false  # Merge (default)
   # O
   git config --global pull.rebase true   # Rebase
   
   # Configurar el push para que coincida con la rama actual
   git config --global push.default current
   ```

5. Verifica tu configuración:
   ```bash
   git config --list
   ```

6. Crear un alias útil:
   ```bash
   git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
   
   # Prueba tu nuevo alias
   mkdir test-repo && cd test-repo
   git init
   touch README.md
   git add README.md
   git commit -m "Commit inicial"
   git lg
   ```

### Preguntas para reflexionar
1. ¿Por qué es importante configurar correctamente la identidad en Git?
2. ¿Cuál es la diferencia entre la configuración `--global` y la configuración a nivel de repositorio?
3. ¿Qué ventajas tiene personalizar Git con alias?

## Ejercicio 2: Creación y Gestión de Repositorios Locales

### Objetivo
Aprender a crear y organizar repositorios Git para diferentes tipos de proyectos.

### Descripción
En este ejercicio crearás diferentes tipos de repositorios locales y experimentarás con su estructura interna.

### Parte A: Creación de un Repositorio desde Cero

1. Crea un nuevo repositorio para un proyecto:
   ```bash
   mkdir mi-proyecto
   cd mi-proyecto
   git init
   ```

2. Examina la estructura del directorio `.git`:
   ```bash
   ls -la .git
   ```

3. Crea algunos archivos y haz el primer commit:
   ```bash
   echo "# Mi Proyecto" > README.md
   echo "console.log('Hola mundo');" > index.js
   echo "node_modules/" > .gitignore
   
   git add .
   git commit -m "Commit inicial: estructura básica"
   ```

4. Examina el historial y los objetos creados:
   ```bash
   git log
   
   # Obtén el hash del commit
   COMMIT_HASH=$(git log --format="%H" -n 1)
   
   # Examina el contenido del commit
   git cat-file -p $COMMIT_HASH
   ```

### Parte B: Creación de un Repositorio Bare

1. Crea un repositorio "bare" que servirá como repositorio central:
   ```bash
   cd ..
   git init --bare repositorio-central.git
   ```

2. Examina su estructura:
   ```bash
   ls -la repositorio-central.git
   ```

3. Configura el repositorio anterior para usar este repositorio bare como remoto:
   ```bash
   cd mi-proyecto
   git remote add origin ../repositorio-central.git
   git push -u origin main
   ```

4. Crea un clon de trabajo del repositorio bare:
   ```bash
   cd ..
   git clone repositorio-central.git clon-trabajo
   cd clon-trabajo
   
   # Verifica que tienes el mismo contenido
   ls -la
   git log
   ```

### Parte C: Experimentación con .gitignore

1. Crea un archivo que debería ser ignorado:
   ```bash
   # En el directorio mi-proyecto
   cd ../mi-proyecto
   mkdir node_modules
   echo "contenido de prueba" > node_modules/test.js
   
   # Verifica que Git lo ignora
   git status
   ```

2. Crea un archivo `.gitignore` más completo:
   ```bash
   cat > .gitignore << EOF
   # Dependencias
   node_modules/
   
   # Archivos de construcción
   dist/
   build/
   
   # Logs
   logs/
   *.log
   
   # Archivos de entorno
   .env
   .env.local
   
   # Archivos del sistema operativo
   .DS_Store
   Thumbs.db
   EOF
   
   git add .gitignore
   git commit -m "Actualizado .gitignore con reglas detalladas"
   git push origin main
   ```

3. En el otro clon, actualiza y verifica el nuevo `.gitignore`:
   ```bash
   cd ../clon-trabajo
   git pull
   cat .gitignore
   
   # Prueba las reglas
   touch .env
   mkdir logs
   echo "mensaje" > logs/error.log
   git status
   ```

### Preguntas para reflexionar
1. ¿Cuál es la diferencia entre un repositorio regular y uno "bare"?
2. ¿En qué situaciones usarías un repositorio bare?
3. ¿Por qué es importante tener un buen archivo `.gitignore` desde el inicio del proyecto?

## Ejercicio 3: Trabajo con Repositorios Remotos

### Objetivo
Aprender a trabajar con repositorios remotos en plataformas como GitHub, GitLab o Bitbucket.

### Descripción
En este ejercicio crearás un repositorio en GitHub, lo conectarás con tu repositorio local, y practicarás las operaciones de sincronización.

### Requisitos previos
- Una cuenta en GitHub, GitLab o Bitbucket
- Git instalado y configurado en tu computadora

### Pasos

1. Crea un repositorio en GitHub:
   - Ve a GitHub.com y accede a tu cuenta
   - Haz clic en el botón "+" y selecciona "New repository"
   - Nombra el repositorio "practica-git-remoto"
   - No inicialices el repositorio con ningún archivo
   - Haz clic en "Create repository"

2. Conecta tu repositorio local con el remoto:
   ```bash
   # Si estás continuando del ejercicio anterior, crea un nuevo directorio
   mkdir practica-remoto
   cd practica-remoto
   git init
   
   # Crea un archivo README.md
   echo "# Práctica de Repositorios Remotos" > README.md
   git add README.md
   git commit -m "Commit inicial"
   
   # Conecta al repositorio remoto (sustituye USER por tu nombre de usuario)
   git remote add origin https://github.com/USER/practica-git-remoto.git
   
   # Sube los cambios
   git push -u origin main
   ```

3. Configura la autenticación (si no lo has hecho antes):
   - Para HTTPS: Git te pedirá tu nombre de usuario y contraseña (o token)
   - Para SSH: Sigue las instrucciones de configuración de claves SSH en la documentación de GitHub

4. Haz cambios en GitHub:
   - Ve a tu repositorio en GitHub
   - Haz clic en el archivo README.md
   - Haz clic en el ícono de edición (lápiz)
   - Añade una línea: "Cambio realizado directamente en GitHub"
   - Haz commit con un mensaje descriptivo

5. Sincroniza los cambios:
   ```bash
   # Descarga los cambios del remoto
   git fetch origin
   
   # Examina las diferencias
   git diff origin/main
   
   # Incorpora los cambios
   git pull origin main
   
   # Verifica el contenido actualizado
   cat README.md
   git log --oneline
   ```

6. Realiza cambios locales y súbelos:
   ```bash
   echo "## Sección Local" >> README.md
   echo "Este cambio fue realizado localmente" >> README.md
   
   git add README.md
   git commit -m "Añadida sección local al README"
   git push origin main
   ```

7. Trabaja con múltiples remotos (simulando una contribución a un proyecto open source):
   ```bash
   # Crea un "fork" simulado
   cd ..
   mkdir proyecto-upstream
   cd proyecto-upstream
   git init
   echo "# Proyecto Original" > README.md
   git add README.md
   git commit -m "Commit inicial del proyecto upstream"
   
   # Crea un clon que simule tu fork
   cd ..
   git clone ./proyecto-upstream mi-fork
   cd mi-fork
   
   # Añade el "upstream" como remoto adicional
   git remote add upstream ../proyecto-upstream
   git remote -v
   
   # Realiza cambios en tu fork
   echo "Contribución desde mi fork" >> README.md
   git add README.md
   git commit -m "Añadida contribución"
   git push origin main
   
   # Simula cambios en el upstream
   cd ../proyecto-upstream
   echo "## Actualizaciones del equipo principal" >> README.md
   git add README.md
   git commit -m "Actualización del equipo principal"
   
   # Sincroniza tu fork con el upstream
   cd ../mi-fork
   git fetch upstream
   git merge upstream/main
   git push origin main
   ```

### Preguntas para reflexionar
1. ¿Cuál es la diferencia entre `git fetch` y `git pull`?
2. ¿Por qué es útil tener múltiples remotos en un repositorio?
3. ¿Qué ventajas ofrece el modelo de fork+pull request en proyectos de código abierto?

## Ejercicio 4: Creación de un Proyecto Colaborativo

### Objetivo
Practicar el flujo de trabajo colaborativo usando Git y GitHub con múltiples colaboradores.

### Descripción
En este ejercicio, trabajarás en equipo para crear un pequeño sitio web, usando GitHub como plataforma de colaboración.

### Pasos

1. El "propietario" del proyecto:
   - Crea un nuevo repositorio en GitHub llamado "sitio-colaborativo"
   - Inicialízalo con un README.md
   - Añade un archivo index.html básico:
     ```html
     <!DOCTYPE html>
     <html>
     <head>
         <title>Sitio Colaborativo</title>
         <link rel="stylesheet" href="styles.css">
     </head>
     <body>
         <header>
             <h1>Bienvenido a nuestro sitio colaborativo</h1>
         </header>
         <main>
             <p>Este sitio está siendo desarrollado colaborativamente usando Git y GitHub.</p>
         </main>
         <footer>
             <p>Curso de Git y GitHub - 2023</p>
         </footer>
     </body>
     </html>
     ```
   - Añade un archivo styles.css vacío
   - Invita a 1-3 compañeros de clase como colaboradores en la configuración del repositorio

2. Cada "colaborador":
   - Acepta la invitación
   - Clona el repositorio:
     ```bash
     git clone https://github.com/OWNER/sitio-colaborativo.git
     cd sitio-colaborativo
     ```
   - Crea una rama para su tarea:
     ```bash
     # Colaborador 1: Diseño del encabezado
     git checkout -b header-design
     
     # Colaborador 2: Contenido principal
     git checkout -b main-content
     
     # Colaborador 3: Diseño del pie de página
     git checkout -b footer-design
     ```

3. Cada colaborador trabaja en su parte:

   **Colaborador 1 (Encabezado)**:
   ```css
   /* En styles.css */
   header {
       background-color: #2c3e50;
       color: white;
       padding: 20px;
       text-align: center;
   }
   ```

   **Colaborador 2 (Contenido Principal)**:
   ```html
   <!-- Modificando main en index.html -->
   <main>
       <p>Este sitio está siendo desarrollado colaborativamente usando Git y GitHub.</p>
       <section>
           <h2>Acerca del proyecto</h2>
           <p>Este proyecto demuestra cómo trabajar de manera efectiva en equipo usando Git.</p>
       </section>
       <section>
           <h2>Tecnologías utilizadas</h2>
           <ul>
               <li>HTML5</li>
               <li>CSS3</li>
               <li>Git</li>
               <li>GitHub</li>
           </ul>
       </section>
   </main>
   ```

   **Colaborador 3 (Pie de página)**:
   ```css
   /* En styles.css */
   footer {
       background-color: #34495e;
       color: white;
       padding: 10px;
       text-align: center;
       position: fixed;
       bottom: 0;
       width: 100%;
   }
   ```

4. Cada colaborador añade sus cambios, hace commit y push:
   ```bash
   git add .
   git commit -m "Añadido diseño de [mi parte]"
   git push origin [mi-rama]
   ```

5. Cada colaborador crea un Pull Request (PR) en GitHub:
   - Ve al repositorio en GitHub
   - Haz clic en "Pull requests" > "New pull request"
   - Selecciona tu rama como "compare" y main como "base"
   - Haz clic en "Create pull request"
   - Añade un título y descripción adecuados

6. El propietario revisa y fusiona los PR:
   - Revisa cada PR
   - Si hay conflictos, trabaja con el colaborador para resolverlos
   - Merge cada PR una vez aprobado

7. Todos los colaboradores actualizan su copia local:
   ```bash
   git checkout main
   git pull origin main
   ```

8. Opcional: Añade una función final en equipo:
   - Crea una rama para una nueva función (por ejemplo, un menú de navegación)
   - Implementa la función entre todos
   - Crea un PR final

### Análisis del ejercicio
- Reflexiona sobre la experiencia de trabajar con un flujo de ramas y PR
- Identifica qué funcionó bien y qué podría mejorarse
- Discute cómo resolver conflictos de manera efectiva

## Entrega

Para completar estos ejercicios, debes:

1. Crear un repositorio en GitHub con el nombre "practicas-git-[tunombre]"
2. Documentar cada ejercicio en carpetas separadas con capturas de pantalla y explicaciones
3. Incluir un archivo README.md en la raíz con un resumen de lo aprendido
4. Compartir el enlace al repositorio con tu instructor

## Recursos adicionales

- [GitHub Learning Lab](https://lab.github.com/)
- [Try Git Interactive Tutorial](https://try.github.io/)
- [Generador de archivos .gitignore](https://www.toptal.com/developers/gitignore) 