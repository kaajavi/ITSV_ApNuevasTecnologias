# Ejercicios: Git en Entornos de Equipo

Este conjunto de ejercicios está diseñado para simular el trabajo con Git en un entorno de equipo profesional. Practicarás flujos de trabajo colaborativos, resolverás conflictos, implementarás estándares de código y configurarás herramientas de calidad.

## Ejercicio 1: Establecer Convenciones y Estándares

### Objetivo
Configurar un repositorio con convenciones y estándares que faciliten la colaboración en equipo.

### Descripción
En este ejercicio, configurarás un repositorio con las mejores prácticas para trabajo en equipo, incluyendo estándares de mensajes de commit, hooks y archivos de configuración compartidos.

### Pasos

1. **Crear un repositorio**:
   ```bash
   mkdir proyecto-equipo
   cd proyecto-equipo
   git init
   ```

2. **Configurar Conventional Commits**:
   - Instala las herramientas necesarias:
   ```bash
   # Para proyectos Node.js
   npm init -y
   npm install --save-dev @commitlint/cli @commitlint/config-conventional
   npm install --save-dev husky
   ```

   - Crea un archivo de configuración para commitlint:
   ```bash
   echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
   ```

   - Configura husky para validar los mensajes de commit:
   ```bash
   npx husky install
   npx husky add .husky/commit-msg 'npx --no -- commitlint --edit "$1"'
   ```

3. **Crear archivos de configuración compartidos**:
   - Crea un archivo `.editorconfig`:
   ```
   root = true

   [*]
   charset = utf-8
   end_of_line = lf
   indent_style = space
   indent_size = 2
   insert_final_newline = true
   trim_trailing_whitespace = true

   [*.md]
   trim_trailing_whitespace = false
   ```

   - Crea un archivo `.gitattributes`:
   ```
   # Normalización de finales de línea
   * text=auto eol=lf

   # Archivos binarios
   *.png binary
   *.jpg binary
   *.pdf binary
   *.zip binary
   ```

   - Crea un archivo `.gitignore` completo:
   ```
   # Node.js
   node_modules/
   npm-debug.log
   
   # Archivos de entorno
   .env
   .env.local
   
   # Directorios de compilación
   dist/
   build/
   
   # Logs
   logs/
   *.log
   
   # Sistema operativo
   .DS_Store
   Thumbs.db
   
   # IDE y editores
   .idea/
   .vscode/
   *.sublime-*
   ```

4. **Configurar un hook de pre-commit personalizado**:
   - Crea un directorio para hooks compartidos:
   ```bash
   mkdir -p .githooks
   ```

   - Crea un hook de pre-commit básico:
   ```bash
   cat > .githooks/pre-commit << 'EOF'
   #!/bin/sh
   
   echo "Ejecutando verificaciones pre-commit..."
   
   # Verificar que no hay console.log en archivos JavaScript
   git diff --cached --name-only --diff-filter=ACM | grep "\.js$" | xargs grep -l "console.log" | while read file; do
     echo "Error: $file contiene console.log"
     exit 1
   done
   
   # Verificar formato correcto
   if command -v npx &> /dev/null; then
     npx prettier --check "*.js" || exit 1
   fi
   
   echo "Verificaciones pre-commit completadas con éxito"
   exit 0
   EOF
   ```

   - Haz el hook ejecutable:
   ```bash
   chmod +x .githooks/pre-commit
   ```

   - Configura Git para usar estos hooks:
   ```bash
   git config core.hooksPath .githooks
   ```

5. **Crear documentación de convenciones para el equipo**:
   - Crea un archivo `CONTRIBUTING.md`:
   ```markdown
   # Guía de Contribución

   ## Convenciones de Mensajes de Commit

   Utilizamos [Conventional Commits](https://www.conventionalcommits.org/) para los mensajes de commit:

   - `feat`: Nueva característica
   - `fix`: Corrección de error
   - `docs`: Cambios de documentación
   - `style`: Cambios de formato
   - `refactor`: Refactorización de código
   - `test`: Adición o corrección de pruebas
   - `chore`: Tareas de mantenimiento

   Ejemplos:
   ```
   feat(auth): implementa autenticación de dos factores
   fix(api): corrige error 500 en endpoint de usuarios
   docs: actualiza instrucciones de instalación
   ```

   ## Proceso de Revisión de Código

   1. Crea una rama desde `develop` con el prefijo adecuado:
      - `feature/` para nuevas características
      - `fix/` para correcciones
      - `refactor/` para refactorizaciones

   2. Realiza tus cambios siguiendo las guías de estilo
   
   3. Crea un Pull Request detallado y asigna revisores

   4. Aborda los comentarios de la revisión

   5. El merge se realizará una vez aprobado

   ## Guías de Estilo

   Seguimos las guías de estilo detalladas en los archivos de configuración:
   - `.editorconfig`
   - `.prettierrc`
   - `.eslintrc`
   ```

6. **Realizar un commit inicial**:
   ```bash
   git add .
   git commit -m "chore: configuración inicial del repositorio"
   ```

7. **Probar el sistema de convenciones**:
   - Intenta hacer un commit que no siga las convenciones:
   ```bash
   echo "console.log('test')" > test.js
   git add test.js
   git commit -m "agregado archivo test"  # Debería fallar
   ```

   - Haz un commit que siga las convenciones:
   ```bash
   git commit -m "feat: agrega archivo de prueba"  # Debería funcionar
   ```

### Preguntas de reflexión

1. ¿Qué ventajas aporta el uso de estándares de mensajes de commit en un equipo?
2. ¿Cómo ayudan los hooks de Git a mantener la calidad del código?
3. ¿Qué otros archivos de configuración podrían ser útiles para un equipo de desarrollo específico?

## Ejercicio 2: Flujos de Trabajo con Ramas

### Objetivo
Practicar diferentes estrategias de ramificación utilizadas en entornos profesionales.

### Descripción
En este ejercicio, simularás el trabajo en un proyecto siguiendo diferentes estrategias de ramificación: GitFlow, GitHub Flow y Trunk-Based Development.

### Pasos

#### Parte 1: GitFlow

1. **Configura GitFlow en tu repositorio**:
   ```bash
   # Instalar git-flow (puedes omitir si ya lo tienes)
   # En sistemas basados en Debian/Ubuntu:
   # sudo apt-get install git-flow
   # En macOS:
   # brew install git-flow

   # Inicializar GitFlow con valores predeterminados
   git flow init -d
   ```

2. **Desarrollar una característica**:
   ```bash
   # Iniciar una nueva característica
   git flow feature start autenticacion
   
   # Crear un archivo para la característica
   echo "function login() { return 'user authenticated'; }" > autenticacion.js
   
   # Añadir y confirmar
   git add autenticacion.js
   git commit -m "feat: implementa función de login básica"
   
   # Añadir más funcionalidad
   echo "function logout() { return 'user logged out'; }" >> autenticacion.js
   git add autenticacion.js
   git commit -m "feat: implementa función de logout"
   
   # Finalizar la característica
   git flow feature finish autenticacion
   ```

3. **Preparar una versión**:
   ```bash
   # Iniciar una versión
   git flow release start 1.0.0
   
   # Crear un archivo de cambios
   echo "# Versión 1.0.0" > CHANGELOG.md
   echo "- Implementada funcionalidad de autenticación" >> CHANGELOG.md
   
   # Añadir y confirmar
   git add CHANGELOG.md
   git commit -m "docs: agrega changelog para versión 1.0.0"
   
   # Finalizar la versión
   git flow release finish 1.0.0
   ```

4. **Simular una corrección urgente**:
   ```bash
   # Iniciar un hotfix
   git flow hotfix start 1.0.1
   
   # Corregir un problema
   echo "function login() { return 'user authenticated successfully'; }" > autenticacion.js
   
   # Añadir y confirmar
   git add autenticacion.js
   git commit -m "fix: corrige mensaje de retorno en login"
   
   # Finalizar el hotfix
   git flow hotfix finish 1.0.1
   ```

#### Parte 2: GitHub Flow

1. **Resetear el repositorio para probar otro flujo**:
   ```bash
   # Crear nuevo directorio
   cd ..
   mkdir github-flow-demo
   cd github-flow-demo
   git init
   echo "# Proyecto Demo GitHub Flow" > README.md
   git add README.md
   git commit -m "chore: commit inicial"
   ```

2. **Desarrollar una característica con GitHub Flow**:
   ```bash
   # Crear una rama para la característica
   git checkout -b feature/login-component
   
   # Crear archivo de la característica
   echo "class LoginComponent { render() { return '<form>Login Form</form>'; } }" > login.js
   
   # Añadir y confirmar
   git add login.js
   git commit -m "feat: implementa componente de login"
   
   # Simular un Pull Request (en un entorno real sería mediante GitHub)
   git checkout main
   git merge --no-ff feature/login-component -m "Merge: Añade componente de login"
   ```

3. **Implementar otra característica simultáneamente**:
   ```bash
   # Crear una rama para otra característica
   git checkout -b feature/header-component
   
   # Crear archivo de la característica
   echo "class HeaderComponent { render() { return '<header>Site Header</header>'; } }" > header.js
   
   # Añadir y confirmar
   git add header.js
   git commit -m "feat: implementa componente de header"
   
   # Simular Pull Request
   git checkout main
   git merge --no-ff feature/header-component -m "Merge: Añade componente de header"
   ```

#### Parte 3: Trunk-Based Development

1. **Resetear el repositorio para probar otro flujo**:
   ```bash
   # Crear nuevo directorio
   cd ..
   mkdir trunk-based-demo
   cd trunk-based-demo
   git init
   echo "# Proyecto Demo Trunk-Based Development" > README.md
   git add README.md
   git commit -m "chore: commit inicial"
   ```

2. **Implementar características con ramas de corta duración**:
   ```bash
   # Crear una rama para una implementación pequeña
   git checkout -b feature/add-button
   
   # Crear cambios
   echo "function Button() { return '<button>Click me</button>'; }" > button.js
   
   # Añadir y confirmar
   git add button.js
   git commit -m "feat: implementa componente de botón básico"
   
   # Integrar a trunk (main) rápidamente
   git checkout main
   git merge feature/add-button
   git branch -d feature/add-button
   ```

3. **Usar feature flags para código incompleto**:
   ```bash
   # Trabajar directamente en main para cambios pequeños
   echo "const FEATURES = { newHeader: false, darkMode: true };" > feature-flags.js
   git add feature-flags.js
   git commit -m "feat: agrega sistema de feature flags"
   
   # Implementar característica protegida por feature flag
   echo "function NewHeader() { if (!FEATURES.newHeader) return null; return '<header>New Design</header>'; }" > new-header.js
   git add new-header.js
   git commit -m "feat: implementa nuevo header tras feature flag"
   ```

### Preguntas de reflexión

1. ¿Qué estrategia de ramificación te parece más adecuada para diferentes tipos de proyectos?
2. ¿Cómo afectan las diferentes estrategias a la velocidad de desarrollo y a la estabilidad?
3. ¿Qué desafíos podrían surgir al implementar cada uno de estos flujos de trabajo en un equipo real?

## Ejercicio 3: Gestión de Calidad y Conflictos

### Objetivo
Implementar herramientas de calidad de código y practicar la resolución de conflictos en un entorno colaborativo.

### Descripción
En este ejercicio, configurarás herramientas de calidad y simularás situaciones de conflicto que ocurren habitualmente en equipos de desarrollo.

### Pasos

1. **Crear un repositorio para el ejercicio**:
   ```bash
   mkdir calidad-codigo
   cd calidad-codigo
   git init
   ```

2. **Configurar herramientas de calidad de código**:
   - Para JavaScript:
   ```bash
   # Inicializar proyecto
   npm init -y
   
   # Instalar ESLint y Prettier
   npm install --save-dev eslint prettier eslint-config-prettier
   
   # Configurar ESLint
   npx eslint --init
   # Responde a las preguntas según tus preferencias
   
   # Crear configuración de Prettier
   echo '{
     "semi": true,
     "singleQuote": true,
     "tabWidth": 2,
     "trailingComma": "es5"
   }' > .prettierrc
   ```

   - Para Python:
   ```bash
   # Crear entorno virtual
   python -m venv venv
   source venv/bin/activate  # En Windows: venv\Scripts\activate
   
   # Instalar herramientas
   pip install flake8 black pytest
   
   # Configurar flake8
   echo '[flake8]
   max-line-length = 88
   extend-ignore = E203
   exclude = venv/*,build/*
   ' > .flake8
   ```

3. **Configurar un pre-commit hook para verificar calidad**:
   ```bash
   mkdir -p .githooks
   
   # Para JavaScript
   cat > .githooks/pre-commit << 'EOF'
   #!/bin/sh
   FILES=$(git diff --cached --name-only --diff-filter=ACM | grep '\.js$')
   if [ -n "$FILES" ]; then
     echo "Verificando con ESLint y Prettier..."
     npx eslint $FILES || exit 1
     npx prettier --check $FILES || exit 1
   fi
   exit 0
   EOF
   
   # Para Python
   cat > .githooks/pre-commit << 'EOF'
   #!/bin/sh
   FILES=$(git diff --cached --name-only --diff-filter=ACM | grep '\.py$')
   if [ -n "$FILES" ]; then
     echo "Verificando con flake8 y black..."
     venv/bin/flake8 $FILES || exit 1
     venv/bin/black --check $FILES || exit 1
   fi
   exit 0
   EOF
   
   chmod +x .githooks/pre-commit
   git config core.hooksPath .githooks
   ```

4. **Crear código inicial**:
   - Para JavaScript:
   ```bash
   echo "function calcularTotal(items) {
     let total = 0;
     for (let i = 0; i < items.length; i++) {
       total += items[i].precio;
     }
     return total;
   }
   
   module.exports = { calcularTotal };" > utils.js
   
   git add utils.js
   git commit -m "feat: agrega función para calcular total"
   ```

   - Para Python:
   ```bash
   echo "def calcular_total(items):
       total = 0
       for item in items:
           total += item['precio']
       return total" > utils.py
   
   git add utils.py
   git commit -m "feat: agrega función para calcular total"
   ```

5. **Simular desarrollo colaborativo con conflictos**:
   - Crea dos ramas para simular dos desarrolladores:
   ```bash
   # Desarrollador 1
   git checkout -b dev1/mejora-utils
   
   # Para JavaScript
   echo "function calcularTotal(items) {
     return items.reduce((total, item) => total + item.precio, 0);
   }
   
   function calcularImpuestos(total, tasa = 0.21) {
     return total * tasa;
   }
   
   module.exports = { calcularTotal, calcularImpuestos };" > utils.js
   
   # Para Python
   echo "def calcular_total(items):
       return sum(item['precio'] for item in items)
       
   def calcular_impuestos(total, tasa=0.21):
       return total * tasa" > utils.py
   
   git add utils.js || git add utils.py
   git commit -m "refactor: optimiza cálculo y agrega función de impuestos"
   ```

   ```bash
   # Vuelve a main
   git checkout main
   
   # Desarrollador 2
   git checkout -b dev2/descuentos
   
   # Para JavaScript
   echo "function calcularTotal(items) {
     let total = 0;
     for (let i = 0; i < items.length; i++) {
       total += items[i].precio;
     }
     return total;
   }
   
   function aplicarDescuento(total, porcentaje) {
     return total - (total * porcentaje / 100);
   }
   
   module.exports = { calcularTotal, aplicarDescuento };" > utils.js
   
   # Para Python
   echo "def calcular_total(items):
       total = 0
       for item in items:
           total += item['precio']
       return total
       
   def aplicar_descuento(total, porcentaje):
       return total - (total * porcentaje / 100)" > utils.py
   
   git add utils.js || git add utils.py
   git commit -m "feat: agrega función para aplicar descuentos"
   ```

6. **Resolver conflictos mediante merge**:
   ```bash
   # Integra la primera rama
   git checkout main
   git merge dev1/mejora-utils
   
   # Intenta integrar la segunda rama (generará conflicto)
   git merge dev2/descuentos
   
   # Verás un mensaje de conflicto. Edita el archivo para combinar ambos cambios:
   # Para JavaScript:
   echo "function calcularTotal(items) {
     return items.reduce((total, item) => total + item.precio, 0);
   }
   
   function calcularImpuestos(total, tasa = 0.21) {
     return total * tasa;
   }
   
   function aplicarDescuento(total, porcentaje) {
     return total - (total * porcentaje / 100);
   }
   
   module.exports = { calcularTotal, calcularImpuestos, aplicarDescuento };" > utils.js
   
   # Para Python:
   echo "def calcular_total(items):
       return sum(item['precio'] for item in items)
       
   def calcular_impuestos(total, tasa=0.21):
       return total * tasa
       
   def aplicar_descuento(total, porcentaje):
       return total - (total * porcentaje / 100)" > utils.py
   
   # Marca como resuelto y completa el merge
   git add utils.js || git add utils.py
   git commit -m "merge: integra funciones de impuestos y descuentos"
   ```

7. **Probar la prevención de errores**:
   - Intenta hacer un commit con código que no cumple los estándares:
   ```bash
   # Para JavaScript
   echo "function badCode() { console.log('Este código no debería pasar el linter'); var x = 10 }" >> utils.js
   
   # Para Python
   echo "def bad_code():    print('Este código no debería pasar el linter'); x = 10" >> utils.py
   
   git add utils.js || git add utils.py
   git commit -m "feat: agrega función mal formateada"
   # Debería fallar el hook de pre-commit
   ```

### Preguntas de reflexión

1. ¿Cómo ayudan las herramientas de calidad a prevenir conflictos?
2. ¿Qué estrategias son eficaces para manejar conflictos en equipos grandes?
3. ¿Cuál es el equilibrio adecuado entre automatización y flexibilidad en las reglas de código?

## Entrega de la Práctica

Para completar estos ejercicios, deberás:

1. Crear un repositorio en GitHub con tus ejercicios
2. Incluir capturas de pantalla o logs que muestren:
   - La configuración de convenciones y estándares
   - Los diferentes flujos de trabajo con ramas
   - La resolución de conflictos
3. Añadir un archivo REFLEXIONES.md con tus respuestas a las preguntas planteadas
4. Incluir una breve descripción de qué enfoque consideras más adecuado para diferentes tipos de proyectos

## Recursos Adicionales

- [Conventional Commits](https://www.conventionalcommits.org/)
- [Git Flow Cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/)
- [Documentación de ESLint](https://eslint.org/docs/user-guide/getting-started)
- [Documentación de Prettier](https://prettier.io/docs/en/index.html)
- [Documentación de GitHub Flow](https://guides.github.com/introduction/flow/)
- [Trunk Based Development](https://trunkbaseddevelopment.com/) 