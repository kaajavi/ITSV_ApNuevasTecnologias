# Ejercicios: Filosofía de Git

A continuación se presentan ejercicios prácticos para comprender mejor los conceptos fundamentales de la filosofía de Git.

## Ejercicio 1: Exploración de Objetos Git

### Objetivo
Entender cómo Git almacena la información internamente y visualizar el modelo de objetos que utiliza.

### Descripción
En este ejercicio explorarás la estructura interna de un repositorio Git, examinando los objetos (blobs, trees, commits) que conforman su base de datos.

### Pasos

1. Crea un nuevo repositorio:
   ```bash
   mkdir git-objetos
   cd git-objetos
   git init
   ```

2. Crea algunos archivos y añádelos:
   ```bash
   echo "Contenido del archivo 1" > archivo1.txt
   echo "Contenido del archivo 2" > archivo2.txt
   mkdir carpeta
   echo "Archivo dentro de carpeta" > carpeta/archivo3.txt
   
   git add .
   ```

3. Haz un commit:
   ```bash
   git commit -m "Primer commit para explorar objetos"
   ```

4. Explora los objetos creados:
   ```bash
   # Obtener el hash del último commit
   COMMIT_HASH=$(git rev-parse HEAD)
   echo "Hash del commit: $COMMIT_HASH"
   
   # Examinar el commit
   git cat-file -p $COMMIT_HASH
   
   # Obtener el hash del tree (desde la salida anterior)
   TREE_HASH=$(git cat-file -p $COMMIT_HASH | grep "tree" | cut -d " " -f 2)
   echo "Hash del tree: $TREE_HASH"
   
   # Examinar el tree
   git cat-file -p $TREE_HASH
   
   # Obtener el hash de un blob (desde la salida anterior)
   BLOB_HASH=$(git cat-file -p $TREE_HASH | grep "archivo1.txt" | cut -d " " -f 3)
   echo "Hash del blob: $BLOB_HASH"
   
   # Examinar el contenido del blob
   git cat-file -p $BLOB_HASH
   ```

5. Realiza un segundo commit y compara:
   ```bash
   echo "Contenido modificado" > archivo1.txt
   git add archivo1.txt
   git commit -m "Segundo commit para comparar objetos"
   
   # Obtener el hash del nuevo commit
   NEW_COMMIT=$(git rev-parse HEAD)
   git cat-file -p $NEW_COMMIT
   
   # Comparar trees
   NEW_TREE=$(git cat-file -p $NEW_COMMIT | grep "tree" | cut -d " " -f 2)
   git cat-file -p $NEW_TREE
   
   # Obtener el hash del nuevo blob para archivo1.txt
   NEW_BLOB=$(git cat-file -p $NEW_TREE | grep "archivo1.txt" | cut -d " " -f 3)
   
   # Verificar que es diferente del blob original
   echo "Hash del blob original: $BLOB_HASH"
   echo "Hash del nuevo blob: $NEW_BLOB"
   
   # Ver el contenido del nuevo blob
   git cat-file -p $NEW_BLOB
   ```

### Análisis
- Observa cómo cada commit apunta a un tree
- Nota cómo cada tree contiene referencias a blobs (archivos) y otros trees (subdirectorios)
- Verifica que al cambiar el contenido de un archivo, se crea un nuevo blob con un hash diferente
- Comprueba que los archivos no modificados mantienen el mismo hash

### Preguntas para reflexionar
1. ¿Por qué crees que Git utiliza hashes SHA-1 para identificar objetos?
2. ¿Qué ventajas ofrece el modelo de almacenamiento basado en contenido?
3. ¿Cómo garantiza Git la integridad de los datos?

## Ejercicio 2: Comparativa de Modelos de Control de Versiones

### Objetivo
Comprender las diferencias prácticas entre los modelos centralizado y distribuido.

### Descripción
En este ejercicio simularás el trabajo con repositorios centralizados y distribuidos, explorando sus ventajas y limitaciones.

### Parte A: Simulación de Sistema Centralizado

1. Crea un repositorio "central":
   ```bash
   mkdir repo-central
   cd repo-central
   git init
   echo "# Repositorio Central" > README.md
   git add README.md
   git commit -m "Commit inicial en repositorio central"
   cd ..
   ```

2. Configura dos clones que simulan desarrolladores:
   ```bash
   # Cliente 1
   git clone ./repo-central cliente1
   cd cliente1
   echo "Cambio del desarrollador 1" >> README.md
   git add README.md
   git commit -m "Cambio del desarrollador 1"
   git push origin main
   cd ..
   
   # Cliente 2
   git clone ./repo-central cliente2
   cd cliente2
   echo "Cambio del desarrollador 2" >> README.md
   git add README.md
   git commit -m "Cambio del desarrollador 2"
   # No hacemos push todavía
   cd ..
   ```

3. Simula un problema con el servidor central:
   ```bash
   # "Romper" el servidor central
   cd repo-central
   rm -rf .git/objects
   cd ..
   
   # Intentar push desde cliente 2
   cd cliente2
   git push origin main  # Fallará
   cd ..
   ```

4. Analiza la situación:
   - Los cambios del cliente 1 están en el servidor pero se perdieron al "dañarse"
   - Los cambios del cliente 2 están solo en su copia local
   - No hay manera de recuperar la información sin backups externos

### Parte B: Sistema Distribuido (Git)

1. Recuperación gracias al modelo distribuido:
   ```bash
   # Recrear el repositorio central a partir del cliente 1
   cd cliente1
   git remote remove origin
   cd ..
   
   # Configurar cliente2 para usar cliente1 como remoto
   cd cliente2
   git remote remove origin
   git remote add origin ../cliente1
   git push origin main  # Puede causar conflicto, resolverlo si es necesario
   cd ..
   
   # Configurar un nuevo "central" desde cliente1
   mkdir nuevo-central
   cd nuevo-central
   git init --bare
   cd ..
   
   cd cliente1
   git remote add origin ../nuevo-central
   git push origin main
   cd ..
   
   cd cliente2
   git remote remove origin
   git remote add origin ../nuevo-central
   git push origin main
   cd ..
   ```

2. Analiza la situación:
   - A pesar de perder el repositorio central, se pudo recuperar toda la información
   - Cada clon tenía una copia completa de la historia
   - Se pudo establecer un nuevo repositorio "central" sin pérdida de datos

### Preguntas para reflexionar
1. ¿Qué ventajas tiene el modelo distribuido en términos de resistencia a fallos?
2. ¿Cómo impacta la arquitectura de Git en la colaboración cuando hay problemas de conectividad?
3. ¿Por qué el modelo distribuido permite flujos de trabajo más flexibles?

## Ejercicio 3: Visualización del Espacio de Trabajo

### Objetivo
Entender el funcionamiento de las tres áreas de Git (directorio de trabajo, área de preparación y repositorio).

### Descripción
Este ejercicio te permitirá visualizar cómo los cambios se mueven entre las tres áreas de Git y cómo esto afecta el estado del proyecto.

### Pasos

1. Crea un nuevo repositorio:
   ```bash
   mkdir tres-areas
   cd tres-areas
   git init
   ```

2. Crea algunos archivos iniciales:
   ```bash
   echo "Archivo 1 - Versión 1" > archivo1.txt
   echo "Archivo 2 - Versión 1" > archivo2.txt
   echo "Archivo 3 - Versión 1" > archivo3.txt
   
   # Comprueba el estado
   git status
   ```

3. Añade algunos archivos al área de preparación:
   ```bash
   git add archivo1.txt archivo2.txt
   
   # Observa estado mixto
   git status
   ```

4. Realiza un commit:
   ```bash
   git commit -m "Añado los dos primeros archivos"
   
   # Observa que archivo3.txt sigue sin seguimiento
   git status
   ```

5. Modifica archivos en diferentes áreas:
   ```bash
   # Modifica un archivo ya commiteado
   echo "Archivo 1 - Versión 2" > archivo1.txt
   
   # Añade un archivo al área de preparación
   git add archivo3.txt
   
   # Modifica un archivo ya añadido al área de preparación
   echo "Archivo 3 - Versión 2" > archivo3.txt
   
   # Comprueba el estado - Deberías ver cambios en las tres áreas
   git status
   ```

6. Explora las diferencias entre áreas:
   ```bash
   # Diferencias entre directorio de trabajo y área de preparación
   git diff
   
   # Diferencias entre área de preparación y último commit
   git diff --staged
   
   # Diferencias entre directorio de trabajo y último commit
   git diff HEAD
   ```

7. Experimenta con git add parcial:
   ```bash
   echo -e "Línea 1\nLínea 2\nLínea 3\nLínea 4" > multilinea.txt
   git add multilinea.txt
   git commit -m "Añado archivo multilínea"
   
   # Modifica varias líneas
   echo -e "Línea 1\nLínea 2 modificada\nLínea 3\nLínea 4 modificada" > multilinea.txt
   
   # Añade solo algunas líneas
   git add -p multilinea.txt
   # Cuando te pregunte, selecciona 'y' para el primer hunk y 'n' para el segundo
   
   # Comprueba el estado
   git status
   git diff
   git diff --staged
   ```

### Análisis

- Observa cómo Git mantiene claramente separadas las tres áreas
- Comprende cómo el área de preparación permite seleccionar qué cambios incluir en cada commit
- Reconoce las diferencias entre los comandos `git diff`, `git diff --staged` y `git diff HEAD`

### Preguntas para reflexionar

1. ¿Qué ventajas ofrece el área de preparación (staging area) de Git?
2. ¿Cómo contribuye la arquitectura de tres áreas a la organización de commits lógicos?
3. ¿Por qué es útil poder añadir cambios por hunks (partes) en lugar de archivos completos?

## Entrega

Para completar esta práctica, debes:

1. Crear un repositorio en GitHub para estos ejercicios
2. Subir los scripts y comandos utilizados
3. Incluir capturas de pantalla mostrando el resultado de los comandos clave
4. Añadir un archivo REFLEXIONES.md con tus respuestas a las preguntas planteadas
5. Explicar en tus propias palabras cómo estas experiencias te ayudaron a entender mejor la filosofía de Git 