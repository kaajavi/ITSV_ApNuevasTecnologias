# Ejercicios: Versionado Semántico

A continuación se presentan ejercicios prácticos para aplicar los conceptos de versionado semántico en proyectos de software.

## Ejercicio 1: Implementación de Versionado Semántico

### Objetivo
Aplicar correctamente el versionado semántico en un proyecto y comprender cómo evoluciona con los cambios.

### Descripción
Crearás un pequeño proyecto y lo irás modificando, asignando versiones según las reglas de SemVer.

### Pasos

1. **Crear un proyecto simple**:
   ```bash
   mkdir mi-biblioteca
   cd mi-biblioteca
   git init
   
   # Crear estructura básica (JavaScript)
   mkdir src
   touch README.md
   
   # Crear archivo principal
   echo 'function sumar(a, b) {
     return a + b;
   }
   
   function restar(a, b) {
     return a - b;
   }
   
   module.exports = {
     sumar,
     restar
   };' > src/matematicas.js
   
   # Crear archivo package.json
   echo '{
     "name": "mi-biblioteca-matematica",
     "version": "0.1.0",
     "description": "Biblioteca simple de funciones matemáticas",
     "main": "src/matematicas.js",
     "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1"
     },
     "keywords": ["matematicas", "biblioteca"],
     "author": "Tu Nombre",
     "license": "MIT"
   }' > package.json
   
   # Commit inicial
   git add .
   git commit -m "feat: Implementación inicial de la biblioteca"
   ```

2. **Etiquetar primera versión**:
   ```bash
   # Primer tag (versión alfa)
   git tag -a v0.1.0 -m "Versión inicial de desarrollo"
   ```

3. **Corregir un bug (incremento de PATCH)**:
   ```bash
   # Modificar el archivo
   echo 'function sumar(a, b) {
     return Number(a) + Number(b); // Asegura que a y b son números
   }
   
   function restar(a, b) {
     return a - b;
   }
   
   module.exports = {
     sumar,
     restar
   };' > src/matematicas.js
   
   # Actualizar versión en package.json (0.1.1)
   sed -i '' 's/"version": "0.1.0"/"version": "0.1.1"/' package.json
   
   # Commit y tag
   git add .
   git commit -m "fix: Asegura que los parámetros de sumar sean tratados como números"
   git tag -a v0.1.1 -m "Corrección de bug en función sumar"
   ```

4. **Añadir nueva funcionalidad (incremento de MINOR)**:
   ```bash
   # Modificar el archivo añadiendo nuevas funciones
   echo 'function sumar(a, b) {
     return Number(a) + Number(b);
   }
   
   function restar(a, b) {
     return a - b;
   }
   
   function multiplicar(a, b) {
     return a * b;
   }
   
   function dividir(a, b) {
     if (b === 0) throw new Error("No se puede dividir por cero");
     return a / b;
   }
   
   module.exports = {
     sumar,
     restar,
     multiplicar,
     dividir
   };' > src/matematicas.js
   
   # Actualizar versión en package.json (0.2.0)
   sed -i '' 's/"version": "0.1.1"/"version": "0.2.0"/' package.json
   
   # Commit y tag
   git add .
   git commit -m "feat: Añade funciones de multiplicar y dividir"
   git tag -a v0.2.0 -m "Añadidas nuevas funcionalidades: multiplicar y dividir"
   ```

5. **Primera versión estable**:
   ```bash
   # Actualizar versión en package.json (1.0.0)
   sed -i '' 's/"version": "0.2.0"/"version": "1.0.0"/' package.json
   
   # Commit y tag
   git add .
   git commit -m "chore: Prepara lanzamiento de versión 1.0.0"
   git tag -a v1.0.0 -m "Primera versión estable"
   ```

6. **Cambio que rompe compatibilidad (incremento de MAJOR)**:
   ```bash
   # Modificar interfaz de las funciones
   echo 'function calcular(operacion, a, b) {
     switch(operacion) {
       case "sumar":
         return Number(a) + Number(b);
       case "restar":
         return a - b;
       case "multiplicar":
         return a * b;
       case "dividir":
         if (b === 0) throw new Error("No se puede dividir por cero");
         return a / b;
       default:
         throw new Error("Operación no reconocida");
     }
   }
   
   // Ya no exportamos las funciones individuales
   module.exports = {
     calcular
   };' > src/matematicas.js
   
   # Actualizar versión en package.json (2.0.0)
   sed -i '' 's/"version": "1.0.0"/"version": "2.0.0"/' package.json
   
   # Commit y tag
   git add .
   git commit -m "feat!: Cambia interfaz a función única calcular"
   git tag -a v2.0.0 -m "Cambio de API: Unifica funciones en método calcular"
   ```

7. **Ver historial de versiones**:
   ```bash
   git tag -l
   git log --oneline --decorate
   ```

### Análisis
- Observa cómo cada cambio afecta al número de versión según su tipo
- Identifica cómo el versionado semántico comunica claramente el impacto de los cambios
- Analiza la claridad que aportan los tags a la historia del proyecto

### Preguntas para reflexionar
1. ¿Cómo ayudaría el versionado semántico a los usuarios de tu biblioteca?
2. ¿En qué casos podrías justificar un incremento de versión MAYOR?
3. ¿Qué información adicional debería incluirse en las notas de cada versión?

## Ejercicio 2: Gestión de Releases en GitHub

### Objetivo
Aprender a crear y gestionar releases en GitHub siguiendo las convenciones de versionado semántico.

### Descripción
Utilizarás GitHub para publicar releases formales de un proyecto, incluyendo notas de lanzamiento detalladas y archivos adjuntos.

### Pasos

1. **Crear repositorio en GitHub**:
   - Crea un nuevo repositorio en GitHub
   - Sube tu proyecto local del ejercicio anterior:
   ```bash
   git remote add origin https://github.com/tu-usuario/mi-biblioteca.git
   git push -u origin main
   git push --tags
   ```

2. **Crear release para v1.0.0**:
   - Ve a la sección "Releases" en GitHub
   - Haz clic en "Draft a new release"
   - Selecciona el tag v1.0.0
   - Añade un título: "Primera versión estable"
   - Escribe notas de lanzamiento detalladas:
   ```markdown
   # Lanzamiento de versión estable 1.0.0
   
   Esta es la primera versión estable de nuestra biblioteca matemática.
   
   ## Funcionalidades
   
   - Operación sumar
   - Operación restar
   - Operación multiplicar
   - Operación dividir
   
   ## Instrucciones de instalación
   
   ```npm install mi-biblioteca-matematica```
   
   ## Ejemplo de uso
   
   ```javascript
   const mat = require('mi-biblioteca-matematica');
   console.log(mat.sumar(5, 3)); // 8
   ```
   ```
   - Publica el release

3. **Crear una pre-release para beta**:
   - Crea una nueva funcionalidad en una rama
   ```bash
   git checkout -b feature/potencia
   
   # Añadir función de potencia
   echo 'function sumar(a, b) {
     return Number(a) + Number(b);
   }
   
   function restar(a, b) {
     return a - b;
   }
   
   function multiplicar(a, b) {
     return a * b;
   }
   
   function dividir(a, b) {
     if (b === 0) throw new Error("No se puede dividir por cero");
     return a / b;
   }
   
   function potencia(base, exponente) {
     return Math.pow(base, exponente);
   }
   
   module.exports = {
     sumar,
     restar,
     multiplicar,
     dividir,
     potencia
   };' > src/matematicas.js
   
   # Actualizar versión en package.json (1.1.0-beta.1)
   sed -i '' 's/"version": "1.0.0"/"version": "1.1.0-beta.1"/' package.json
   
   # Commit y tag
   git add .
   git commit -m "feat: Añade función de potencia"
   git tag -a v1.1.0-beta.1 -m "Versión beta con función de potencia"
   git push origin feature/potencia --tags
   ```
   
   - Crea un release en GitHub para v1.1.0-beta.1
   - Marca la casilla "This is a pre-release"
   - Añade notas indicando que es una versión beta para pruebas

4. **Crear release final v1.1.0**:
   - Fusiona la rama con main
   ```bash
   git checkout main
   git merge feature/potencia
   sed -i '' 's/"version": "1.1.0-beta.1"/"version": "1.1.0"/' package.json
   git add .
   git commit -m "chore: Actualiza versión a 1.1.0"
   git tag -a v1.1.0 -m "Versión 1.1.0 con función de potencia"
   git push origin main --tags
   ```
   
   - Crea un release en GitHub para v1.1.0
   - Incluye notas de lanzamiento completas

5. **Crear un changelog**:
   - Crea un archivo CHANGELOG.md en tu repositorio
   ```markdown
   # Changelog
   
   Todos los cambios notables en este proyecto serán documentados en este archivo.
   
   ## [1.1.0] - YYYY-MM-DD
   
   ### Añadido
   - Función de potencia para calcular una base elevada a un exponente
   
   ## [1.0.0] - YYYY-MM-DD
   
   ### Añadido
   - Función sumar
   - Función restar
   - Función multiplicar
   - Función dividir
   
   ## [0.2.0] - YYYY-MM-DD
   
   ### Añadido
   - Funciones multiplicar y dividir
   
   ## [0.1.1] - YYYY-MM-DD
   
   ### Corregido
   - Bug en función sumar que no convertía strings a números
   
   ## [0.1.0] - YYYY-MM-DD
   
   ### Añadido
   - Versión inicial con funciones sumar y restar
   ```
   
   - Actualiza el changelog en cada nueva versión
   - Commit y push de los cambios

### Análisis
- Analiza cómo las releases en GitHub proporcionan un historial claro de cambios
- Observa la diferencia entre releases estables y pre-releases
- Evalúa la utilidad del changelog para usuarios y desarrolladores

### Preguntas para reflexionar
1. ¿Qué ventajas ofrecen las pre-releases frente a publicar directamente versiones estables?
2. ¿Cómo influye un buen sistema de versionado en la adopción de tu software?
3. ¿Qué información adicional podrías incluir en las notas de release para diferentes audiencias?

## Entrega de la Práctica

Para completar estos ejercicios, deberás:

1. Crear un repositorio público en GitHub con todos los commits, tags y releases
2. Incluir un archivo README.md con:
   - Explicación del proyecto
   - Documentación de las diferentes versiones
   - Justificación de las decisiones de versionado
3. Mantener un CHANGELOG.md actualizado con todos los cambios
4. Compartir el enlace al repositorio y a las releases creadas

## Recursos Adicionales

- [Calculadora online de SemVer](https://semver.npmjs.com/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [GitHub CLI Documentation](https://cli.github.com/manual/gh_release)
- [npm semver calculator](https://semver.npmjs.com/) 