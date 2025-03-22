# Flujo de Trabajo con Git

## Introducción

El flujo de trabajo en Git se refiere a cómo utilizamos los diferentes comandos y funcionalidades para gestionar nuestro código a lo largo del tiempo. Dominar estos flujos de trabajo es fundamental para trabajar eficientemente tanto en proyectos personales como en equipos de desarrollo. En esta sección exploraremos los comandos básicos de Git, así como técnicas más avanzadas para gestionar el ciclo de vida del código.

## Objetivos de Aprendizaje
- Dominar los comandos básicos de Git para el trabajo diario
- Comprender y aplicar diferentes estrategias de ramificación
- Conocer técnicas para la fusión de código
- Aprender a gestionar cambios temporales con stash
- Explorar el historial de un repositorio de manera efectiva

## Contenido

### Comandos Básicos: Inicialización y Tracking

#### Inicialización de un Repositorio

Para comenzar a utilizar Git en un proyecto, necesitamos inicializar un repositorio:

```bash
# Inicializar un repositorio nuevo
git init

# Verificar el estado actual
git status
```

El comando `git init` crea un subdirectorio `.git` que contiene todos los metadatos necesarios para el repositorio.

#### Seguimiento de Archivos

Git clasifica los archivos en tu directorio de trabajo en tres estados principales:

1. **Modified (Modificado)**: Cambios que no han sido preparados para un commit
2. **Staged (Preparado)**: Cambios marcados para ser incluidos en el próximo commit
3. **Committed (Confirmado)**: Cambios que ya están almacenados en la base de datos local

Para mover archivos entre estos estados, utilizamos comandos como:

```bash
# Añadir un archivo específico al área de preparación
git add archivo.txt

# Añadir varios archivos
git add archivo1.txt archivo2.txt

# Añadir todos los archivos modificados
git add .

# Añadir todos los archivos con una extensión específica
git add *.js

# Añadir interactivamente (seleccionando partes específicas)
git add -p
```

#### Creación de Commits

Un commit en Git es una instantánea del estado de tu proyecto en un momento específico:

```bash
# Crear un commit básico
git commit -m "Mensaje descriptivo del commit"

# Añadir y hacer commit en un solo paso (solo para archivos tracked)
git commit -am "Mensaje del commit"

# Modificar el último commit
git commit --amend
```

**Buenas prácticas para mensajes de commit:**

1. **Usar formato imperativo**: "Añade función" en lugar de "Añadida función"
2. **Primera línea concisa**: Máximo 50 caracteres
3. **Descripción detallada**: Separada por una línea en blanco (opcional)
4. **Incluir contexto**: Por qué el cambio fue necesario, no solo qué cambió

Ejemplo de un buen mensaje de commit:
```
Añade validación de email en formulario de registro

- Implementa regex para validar formato de email
- Añade feedback visual para el usuario
- Previene envío de formulario con email inválido

Resuelve el issue #123
```

#### Visualización de Cambios

Para ver los cambios realizados entre diferentes estados:

```bash
# Ver cambios entre el directorio de trabajo y el área de preparación
git diff

# Ver cambios entre el área de preparación y el último commit
git diff --staged

# Ver cambios en un archivo específico
git diff archivo.txt

# Ver cambios entre dos commits
git diff commit1 commit2

# Ver cambios introducidos por un commit específico
git show commit_hash
```

### Branching: Trabajo con Ramas

Las ramas en Git son referencias móviles a commits, permitiendo desarrollo paralelo.

#### Gestión Básica de Ramas

```bash
# Listar todas las ramas
git branch

# Crear una nueva rama
git branch nueva-rama

# Cambiar a una rama existente
git checkout rama
# O en versiones más recientes de Git
git switch rama

# Crear y cambiar a una rama en un solo paso
git checkout -b nueva-rama
# O
git switch -c nueva-rama

# Renombrar una rama
git branch -m nombre-viejo nombre-nuevo

# Eliminar una rama (debe estar fusionada)
git branch -d rama-a-eliminar

# Eliminar una rama sin importar su estado (con cuidado)
git branch -D rama-a-eliminar
```

#### Estrategias de Ramificación

Existen varios modelos populares para gestionar ramas en proyectos:

1. **GitHub Flow**:
   - Rama principal `main` siempre desplegable
   - Ramas de características (feature branches) para nuevos desarrollos
   - Pull requests para revisión de código
   - Merge a `main` después de aprobación

2. **GitFlow**:
   - Dos ramas principales: `main` (producción) y `develop` (desarrollo)
   - Ramas de características (`feature/*`) desde `develop`
   - Ramas de lanzamiento (`release/*`) para preparar versiones
   - Ramas de corrección (`hotfix/*`) para arreglos urgentes en producción

3. **Trunk-Based Development**:
   - Desarrollo principalmente en `main` (trunk)
   - Ramas de corta duración
   - Integraciones frecuentes
   - Feature flags para funciones no completas

#### Ramas Remotas

Para trabajar con ramas en repositorios remotos:

```bash
# Ver ramas remotas
git branch -r

# Ver todas las ramas (locales y remotas)
git branch -a

# Crear una rama local que haga seguimiento a una rama remota
git checkout -b local-branch origin/remote-branch
# O más simplemente
git checkout --track origin/remote-branch

# Publicar una rama local en el remoto
git push -u origin rama-local

# Eliminar una rama remota
git push origin --delete rama-remota
```

### Fusión: Merge y Rebase

Hay dos estrategias principales para integrar cambios de una rama a otra:

#### Merge

Combina los cambios de una rama en otra, creando un commit de fusión:

```bash
# Primero, cambiar a la rama destino
git checkout main

# Fusionar otra rama en la actual
git merge rama-caracteristica

# Merge sin fast-forward (siempre crea commit de fusión)
git merge --no-ff rama-caracteristica

# Abortar un merge en caso de conflictos
git merge --abort
```

**Tipos de merge:**
- **Fast-forward**: Cuando no hay commits nuevos en la rama destino, simplemente avanza el puntero
- **Recursive**: Cuando ambas ramas tienen commits nuevos, crea un commit de fusión

#### Rebase

Reaplica los commits de una rama sobre otra, creando un historial lineal:

```bash
# Estando en la rama a rebasar
git rebase main

# Rebase interactivo (permite modificar commits)
git rebase -i HEAD~3  # Últimos 3 commits

# Continuar rebase después de resolver conflictos
git rebase --continue

# Abortar un rebase
git rebase --abort
```

**Cuándo usar merge vs rebase:**
- **Merge**: Para ramas de características que se fusionarán a ramas principales
- **Rebase**: Para mantener ramas de características actualizadas con la rama principal
- **Regla de oro**: No rebasar ramas que otros desarrolladores estén utilizando

#### Resolución de Conflictos

Los conflictos ocurren cuando Git no puede combinar automáticamente los cambios:

1. Git marca los archivos con conflictos
2. Edita manualmente los archivos para resolver los conflictos
3. Marca los conflictos como resueltos con `git add`
4. Completa la operación (merge o rebase)

```bash
# Herramientas visuales para resolución de conflictos
git mergetool

# Ver archivos con conflictos
git diff --name-only --diff-filter=U
```

### Gestión Temporal: Stash

El "stash" permite guardar temporalmente cambios que no estás listo para commitear:

```bash
# Guardar cambios actuales en el stash
git stash

# Guardar con un mensaje descriptivo
git stash save "Mensaje descriptivo"

# Listar todos los stashes
git stash list

# Aplicar el stash más reciente (manteniéndolo en la lista)
git stash apply

# Aplicar un stash específico
git stash apply stash@{2}

# Aplicar y eliminar el stash más reciente
git stash pop

# Eliminar el stash más reciente
git stash drop

# Eliminar un stash específico
git stash drop stash@{2}

# Crear una rama a partir de un stash
git stash branch nueva-rama stash@{0}
```

**Casos de uso comunes:**
- Necesitas cambiar rápidamente de tarea
- Quieres probar una idea pero no contaminar tu trabajo actual
- Pull de cambios remotos que podrían causar conflictos con cambios locales

### Exploración: Log, Diff, Show

#### Navegando por el Historial

Git proporciona herramientas poderosas para explorar la historia del proyecto:

```bash
# Ver historial básico
git log

# Visualización compacta
git log --oneline

# Ver historial con gráfico
git log --graph --oneline --all

# Ver cambios introducidos por cada commit
git log -p

# Ver estadísticas resumidas
git log --stat

# Buscar commits por mensaje
git log --grep="bugfix"

# Buscar commits por autor
git log --author="Nombre"

# Buscar commits que afectan a un archivo/directorio
git log -- ruta/al/archivo

# Limitar cantidad de commits
git log -n 5

# Filtrar por fecha
git log --since="2023-01-01" --until="2023-12-31"
```

#### Inspección Detallada

Para analizar cambios específicos:

```bash
# Ver detalles completos de un commit
git show commit_hash

# Ver archivos modificados en un commit
git show --name-only commit_hash

# Ver cómo era un archivo en un commit específico
git show commit_hash:ruta/al/archivo

# Ver cómo era un archivo en un momento específico
git show HEAD~3:ruta/al/archivo  # 3 commits atrás
```

#### Búsqueda avanzada

Para encontrar cuando y cómo se introdujo un cambio:

```bash
# Encontrar el commit que introdujo un cambio específico
git blame archivo.txt

# Mostrar quién modificó cada línea y en qué commit
git blame -L 10,20 archivo.txt  # Solo líneas 10-20

# Buscar el commit que introdujo o eliminó una cadena específica
git log -S "cadena a buscar"

# Búsqueda por expresión regular
git log -G "patron[0-9]+"
```

#### Git Bisect

Para encontrar el commit que introdujo un bug mediante búsqueda binaria:

```bash
# Iniciar búsqueda
git bisect start

# Marcar el estado actual como malo
git bisect bad

# Marcar un commit anterior conocido como bueno
git bisect good commit_hash

# Git seleccionará commits intermedios para probar
# Después de cada prueba, marcar como bueno o malo
git bisect good  # O
git bisect bad

# Cuando se encuentra el commit problemático, finalizar
git bisect reset
```

### Buenas Prácticas en el Flujo de Trabajo

1. **Commits atómicos**: Cada commit debe representar un cambio lógico único
2. **Commits frecuentes**: No esperes a tener grandes cambios
3. **Pull antes de push**: Sincroniza con el repositorio remoto antes de subir cambios
4. **Ramas para características**: Desarrolla nuevas funciones en ramas dedicadas
5. **Mensajes descriptivos**: Facilita entender qué y por qué se hizo un cambio
6. **Revisión de código**: Utiliza pull requests o revisiones para mejorar la calidad
7. **Pruebas antes de merge**: Asegúrate de que todo funciona correctamente antes de fusionar

## Flujos de Trabajo Avanzados

### Reescritura de la Historia

Git permite modificar el historial de commits, pero debe usarse con precaución:

```bash
# Modificar el último commit
git commit --amend

# Reescribir múltiples commits
git rebase -i HEAD~5

# Opciones en rebase interactivo:
# pick: mantener el commit como está
# reword: cambiar el mensaje del commit
# edit: modificar el contenido del commit
# squash: fusionar con el commit anterior
# fixup: fusionar sin preservar el mensaje
# drop: eliminar el commit
```

**¡IMPORTANTE!** No reescribas la historia de ramas compartidas con otros desarrolladores.

### Cherry-Pick

Seleccionar y aplicar commits específicos:

```bash
# Aplicar un commit específico a la rama actual
git cherry-pick commit_hash

# Aplicar múltiples commits
git cherry-pick commit1 commit2 commit3

# Cherry-pick sin hacer commit automático
git cherry-pick -n commit_hash
```

### Reflog: Tu Red de Seguridad

Git mantiene un registro de todos los movimientos de HEAD:

```bash
# Ver el reflog
git reflog

# Recuperar un estado anterior
git checkout HEAD@{2}  # 2 movimientos atrás en reflog
```

El reflog es especialmente útil para recuperarse de operaciones destructivas como rebase o reset.

## Ejercicios

Para realizar los ejercicios prácticos, dirígete a la carpeta [ejercicios](./ejercicios/) donde encontrarás actividades que te ayudarán a dominar el flujo de trabajo con Git.

## Recursos Adicionales

- [Pro Git: Capítulo sobre Branching](https://git-scm.com/book/es/v2/Ramificaciones-en-Git-¿Qué-es-una-rama%3F)
- [Atlassian Git Tutorial: Flujos de Trabajo](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [Git Flow Cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/)
- [Visualizing Git Concepts](https://onlywei.github.io/explain-git-with-d3/) 