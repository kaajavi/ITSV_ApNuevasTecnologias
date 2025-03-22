# Filosofía de Git

## Introducción

Git surgió como una respuesta a las limitaciones de los sistemas de control de versiones anteriores, con una filosofía única que lo distingue fundamentalmente de sus predecesores. Entender estos principios básicos es clave para aprovechar al máximo esta herramienta y comprender por qué ha revolucionado el desarrollo de software.

## Objetivos de Aprendizaje
- Comprender el modelo conceptual detrás de Git
- Diferenciar entre el enfoque de snapshots y el de cambios incrementales
- Entender las ventajas del sistema distribuido frente al centralizado
- Familiarizarse con el modelo de datos interno de Git

## Contenido

### Snapshots vs. Cambios

#### El Enfoque de Cambios (Delta-based)

Los sistemas de control de versiones tradicionales como CVS y SVN utilizan un enfoque basado en cambios (deltas):

- Almacenan la versión inicial de un archivo y luego sólo las diferencias entre versiones
- Conceptualmente ven la información como un conjunto de archivos y los cambios realizados a cada archivo a lo largo del tiempo
- Para reconstruir una versión, deben aplicar todos los cambios incrementales desde el inicio

```
Archivo A (v1) -> +cambio1 -> +cambio2 -> +cambio3 -> Archivo A (v4)
```

**Ventajas:**
- Eficiente en espacio para archivos con pocos cambios
- Conceptualmente simple de entender

**Desventajas:**
- Recuperar versiones antiguas requiere reconstrucción desde el inicio
- Mayor complejidad para bifurcaciones (branches)

#### El Enfoque de Snapshots de Git

Git utiliza un enfoque totalmente diferente basado en snapshots (instantáneas):

- Cada vez que haces un commit, Git almacena una "fotografía" completa de todos los archivos en ese momento
- Para los archivos que no cambiaron, no almacena el archivo de nuevo, sino un enlace al archivo idéntico que ya tiene almacenado
- Conceptualmente, Git es como un mini sistema de archivos con herramientas poderosas construidas sobre él

```
Commit 1: [Snapshot de todos los archivos v1]
Commit 2: [Snapshot de todos los archivos v2]
```

**Ventajas:**
- Recuperación muy rápida de cualquier versión
- Operación offline completa
- Integridad garantizada a través de hashes (SHA-1)
- Más eficiente para ramificación y fusión

**Desventajas:**
- Mayor uso de espacio (mitigado con compresión)
- Conceptualmente más complejo al inicio

### Sistema Distribuido vs. Centralizado

#### Sistemas Centralizados

En sistemas como SVN:
- Existe un único repositorio "central" con la versión oficial
- Los desarrolladores obtienen (checkout) la versión actual
- Trabajan y luego envían (commit) sus cambios al servidor
- Requieren conexión a la red para la mayoría de operaciones
- Existe un único punto de fallo (el servidor central)

```
           Desarrollador 1
           /
Servidor Central -- Desarrollador 2
           \
           Desarrollador 3
```

#### Sistema Distribuido de Git

En Git:
- Cada desarrollador tiene una copia completa del repositorio con toda su historia
- Pueden trabajar, hacer commits, crear ramas y consultar la historia sin conexión
- Sincronización mediante "push" y "pull" cuando sea conveniente
- No hay un repositorio inherentemente "central" (aunque por convención se suele designar uno)
- Múltiples copias de seguridad distribuidas

```
Desarrollador 1 <--> Desarrollador 2 <--> Desarrollador 3
       ^                   ^                   ^
       |                   |                   |
       +------- Repositorio Compartido -------+
                (GitHub, GitLab, etc.)
```

**Ventajas:**
- Trabajo sin conexión
- Mayor velocidad para la mayoría de operaciones
- Respaldo natural (cada clon es un backup completo)
- Mayor flexibilidad en los flujos de trabajo
- Resistencia a fallos

### Modelo de Datos de Git

Git almacena su información como un grafo acíclico dirigido (DAG) de objetos, donde cada objeto está identificado por un hash SHA-1. Los principales tipos de objetos son:

#### 1. Blobs
- Contienen el contenido de un archivo
- No almacenan el nombre del archivo ni permisos, solo el contenido
- Un mismo blob puede ser referenciado por múltiples árboles

#### 2. Árboles (Trees)
- Representan un directorio
- Contienen punteros a blobs (archivos) u otros árboles (subdirectorios)
- Incluyen nombres de archivo, permisos y tipos de entrada

#### 3. Commits
- Representan un estado específico del proyecto
- Contienen:
  - Puntero al árbol (snapshot)
  - Información del autor y del committer
  - Mensaje de commit
  - Punteros a commit(s) padre(s)

#### 4. Referencias (Refs)
- Referencias a commits específicos (no son objetos inmutables)
- Ejemplos: ramas, etiquetas, HEAD
- Permiten dar nombres amigables a los hashes

#### Ejemplo de Relación entre Objetos:

```
                   +----------------+
                   | Commit         |
                   | Tree: a1b2c3   |
                   | Parent: d4e5f6 |
                   | Message: "..." |
                   +----------------+
                           |
                           v
                   +----------------+
                   | Tree a1b2c3    |
                   | foo.txt: g7h8i9|
                   | bar.txt: j0k1l2|
                   | src/: m3n4o5   |
                   +----------------+
                     /      |      \
                    /       |       \
        +---------+   +---------+    +---------+
        | Blob    |   | Blob    |    | Tree    |
        | g7h8i9  |   | j0k1l2  |    | m3n4o5  |
        | (foo.txt)|  | (bar.txt)|    | (src/) |
        +---------+   +---------+    +---------+
```

### Las Tres Áreas de Git

El flujo de trabajo en Git involucra tres áreas principales:

1. **Working Directory (Directorio de trabajo)**
   - Los archivos con los que estás trabajando activamente
   - La versión actual extraída del repositorio

2. **Staging Area (Área de preparación)**
   - También llamada "index"
   - Preparación de los cambios para el próximo commit
   - Permite seleccionar qué modificaciones incluir

3. **Repository (Repositorio)**
   - La base de datos de objetos de Git (.git)
   - Almacena la historia completa y los metadatos del proyecto

**Flujo básico:**
1. Modificas archivos en tu directorio de trabajo
2. Preparas (stage) los cambios con `git add`
3. Confirmas (commit) los cambios preparados con `git commit`

Esta arquitectura de tres áreas permite un flujo de trabajo muy flexible y granular.

## Conclusiones

La filosofía de Git se basa en varios principios fundamentales:

1. **Distribuido por diseño**: Facilita la colaboración sin dependencia de un servidor central
2. **Snapshots, no deltas**: Mayor rendimiento y flexibilidad
3. **Integridad**: Todo se identifica con hash SHA-1, garantizando consistencia
4. **Solo añadir**: Los objetos en Git son inmutables, solo se añaden nuevos
5. **Flexibilidad**: Diseñado para adaptarse a diferentes flujos de trabajo
6. **Operaciones locales**: La mayoría de las operaciones son rápidas y no requieren conexión

Entender estos conceptos fundamentales ayuda a trabajar con Git de manera más efectiva y aprovechar todo su potencial.

## Recursos Adicionales

- [Pro Git - Capítulo sobre los Fundamentos de Git](https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Fundamentos-de-Git)
- [Git from the Bottom Up](https://jwiegley.github.io/git-from-the-bottom-up/)
- [Git Internals - Git Objects](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects)

## Ejercicios

Para realizar los ejercicios prácticos, dirígete a la carpeta [ejercicios](./ejercicios/) donde encontrarás actividades que te ayudarán a comprender mejor la filosofía y estructura interna de Git. 