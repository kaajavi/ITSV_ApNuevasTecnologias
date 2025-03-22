# Historia del Control de Versiones

## Introducción

El control de versiones es un sistema que registra los cambios realizados en un archivo o conjunto de archivos a lo largo del tiempo, permitiendo recuperar versiones específicas más adelante. En el desarrollo de software, es una herramienta indispensable que ha evolucionado significativamente en las últimas décadas.

## Objetivos de Aprendizaje
- Comprender la evolución histórica del control de versiones
- Identificar los problemas que cada sistema intentó resolver
- Reconocer las limitaciones de los sistemas anteriores a Git
- Entender el contexto que llevó a la creación de Git

## Contenido

### Desarrollo Manual y Primeros Sistemas

#### Método Manual

En los inicios de la programación, el control de versiones era completamente manual:
- Copias de archivos con nombres diferentes (`programa.c`, `programa_v2.c`, etc.)
- Archivos comprimidos con fechas (`codigo_20230315.zip`)
- Comentarios en el código indicando cambios

**Problemas:**
- Difícil coordinación entre desarrolladores
- Alta probabilidad de pérdida de información
- Imposible trabajar en paralelo efectivamente
- Dificultad para integrar cambios

#### SCCS (Source Code Control System)

- Desarrollado por Marc Rochkind en Bell Labs en 1972
- Primer sistema de control de versiones formal
- Almacenaba revisiones como conjuntos de deltas (diferencias)
- Bloqueaba archivos para edición ("check-out/check-in")
- Solo permitía uso local, en una única máquina

### Sistemas Centralizados

#### RCS (Revision Control System)

- Creado por Walter Tichy en 1982
- Mejora de SCCS con mejor rendimiento
- Operaba sobre archivos individuales
- Introdujo el concepto de ramificación (branches) limitada
- Seguía siendo local, sin soporte para red

#### CVS (Concurrent Versions System)

- Desarrollado por Dick Grune en 1986, mejorado por Brian Berliner en 1989
- Primer sistema popular de control de versiones en red
- Permitía a múltiples desarrolladores trabajar sobre los mismos archivos
- Operaba a nivel de archivo, no de proyecto completo
- Introdujo los comandos básicos que siguen usándose (checkout, commit, update)

**Características principales:**
- Repositorio central único
- No había confirmaciones atómicas (commits parciales posibles)
- Operaciones de red lentas
- Renombrar archivos era problemático
- No manejaba bien archivos binarios

#### Subversion (SVN)

- Lanzado por CollabNet en 2000
- Diseñado específicamente para superar las limitaciones de CVS
- Introdujo confirmaciones atómicas (todo o nada)
- Mejor manejo de binarios y metadatos
- Mejor manejo de ramas y etiquetas
- Soporte para mover y renombrar archivos

**Problemas de los sistemas centralizados:**
- Dependencia del servidor central
- Requiere conexión a la red para operaciones básicas
- Punto único de fallo
- Ramificación costosa y complicada
- Merges complejos y propensos a errores

### Sistemas Distribuidos

#### BitKeeper

- Desarrollado por BitMover Inc. en 2000
- Uno de los primeros sistemas de control de versiones distribuidos
- Utilizado por el kernel de Linux durante 2002-2005
- Cambió el modelo mental: cada desarrollador tiene una copia completa
- La controversia por su licencia llevó a la creación de Git

#### Git

- Creado por Linus Torvalds en 2005
- Desarrollado inicialmente para el kernel de Linux
- Diseñado para ser rápido, eficiente y totalmente distribuido
- Revolucionó el control de versiones con su modelo de datos basado en snapshots
- Se convirtió en el estándar de facto para control de versiones

**Otros sistemas distribuidos contemporáneos:**
- **Mercurial** (2005): Creado por Matt Mackall, como alternativa a BitKeeper
- **Bazaar** (2005): Desarrollado por Canonical, usado en Ubuntu
- **Fossil** (2007): Creado por D. Richard Hipp, autor de SQLite

## Línea de Tiempo

| Año  | Sistema | Tipo | Aporte Principal |
|------|---------|------|------------------|
| 1972 | SCCS    | Local | Primer sistema formal |
| 1982 | RCS     | Local | Mejor rendimiento, ramas limitadas |
| 1986/1989 | CVS | Centralizado | Trabajo en red, colaborativo |
| 2000 | SVN     | Centralizado | Commits atómicos, mejor manejo de binarios |
| 2000 | BitKeeper | Distribuido | Modelo distribuido usado por Linux |
| 2005 | Git     | Distribuido | Revoluciona velocidad y modelo de datos |
| 2005 | Mercurial | Distribuido | Alternativa más sencilla a Git |

## La Transición a Git

A partir de 2010, Git comenzó a ganar popularidad masiva por varias razones:
- Plataformas como GitHub (2008) y GitLab (2011) que facilitaron la colaboración
- Su modelo distribuido demostraba claras ventajas
- Mayor velocidad en operaciones diarias
- Mejor manejo de branches y merge
- El respaldo de grandes proyectos de código abierto

## Recursos Adicionales

- [Pro Git - "Getting Started"](https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git)
- [Evolution of Version Control System](https://medium.com/@hariomkumawat/evolution-of-version-control-system-56c8c7babc89)
- Video: [History of Version Control](https://www.youtube.com/watch?v=MyvyqdQ3OjU)

## Ejercicios

Para realizar los ejercicios prácticos, dirígete a la carpeta [ejercicios](./ejercicios/) donde encontrarás actividades que reforzarán tu comprensión sobre la historia del control de versiones. 