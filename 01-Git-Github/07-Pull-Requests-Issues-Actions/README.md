# Pull Requests, Issues y Actions

## Introducción

Una vez que comprendemos los fundamentos de Git y GitHub, es momento de explorar las herramientas que hacen que GitHub sea una plataforma de colaboración excepcional. Los Pull Requests, Issues y GitHub Actions son tres características fundamentales que transforman un simple repositorio de código en un entorno de trabajo colaborativo completo.

## Objetivos de Aprendizaje
- Dominar el flujo de trabajo colaborativo basado en Pull Requests
- Aprender a gestionar proyectos mediante Issues
- Comprender cómo automatizar tareas con GitHub Actions
- Implementar buenas prácticas para la colaboración en equipo

## Contenido

### Pull Requests: La Base de la Colaboración

Los Pull Requests (PRs) son el mecanismo principal para revisar código y colaborar en proyectos en GitHub.

#### ¿Qué es un Pull Request?

Un Pull Request es una propuesta de cambios que un colaborador quiere incorporar a un repositorio. Permite:

- Mostrar los cambios propuestos de forma clara
- Discutir y revisar el código línea por línea
- Solicitar cambios o aprobaciones
- Ejecutar verificaciones automáticas
- Mantener un registro completo de la conversación y decisiones

#### El Ciclo de Vida de un Pull Request

1. **Creación**: 
   - Desarrollar cambios en una rama separada
   - Enviar la rama a GitHub
   - Crear el PR a través de la interfaz de GitHub

   ```bash
   git checkout -b nueva-caracteristica
   # Realizar cambios y commits
   git push origin nueva-caracteristica
   # Luego crear el PR desde GitHub
   ```

2. **Revisión**:
   - Revisores examinan los cambios
   - Dejan comentarios, sugerencias y aprobaciones
   - Se hacen ajustes según sea necesario

3. **Integración**:
   - Una vez aprobado, el PR se puede fusionar (merge)
   - Opciones: merge estándar, squash, rebase
   - La rama se puede eliminar después de la fusión

4. **Cierre**:
   - PRs pueden cerrarse sin fusionar si se descartan los cambios

#### Anatomía de un Buen Pull Request

Un PR efectivo debe incluir:

1. **Título claro y descriptivo**
2. **Descripción detallada**:
   - Qué se implementó
   - Por qué se realizaron los cambios
   - Cómo se probó la funcionalidad
3. **Referencias a Issues** relacionados
4. **Capturas de pantalla** (para cambios visuales)
5. **Lista de comprobación** para revisores

#### Revisión de Código Efectiva

La revisión de código es una habilidad crucial:

- **Enfocarse primero en la arquitectura y diseño**, luego en detalles menores
- **Hacer preguntas en lugar de afirmaciones**: "¿Has considerado...?" en vez de "Deberías..."
- **Comentar tanto aspectos positivos como mejorables**
- **Ser específico en los comentarios**
- **Proponer soluciones** cuando sea posible

### Issues: Gestión de Tareas y Problemas

Los Issues son una forma flexible de rastrear ideas, mejoras, tareas o errores en proyectos de GitHub.

#### Tipos de Issues

Los Issues pueden representar:
- **Bugs**: Problemas en el código existente
- **Features**: Nuevas funcionalidades
- **Mejoras**: Optimizaciones de código o funcionalidades existentes
- **Documentación**: Necesidades de actualización o creación de documentación
- **Preguntas**: Dudas sobre el código o funcionamiento

#### Componentes de un Issue

Un Issue bien estructurado contiene:

1. **Título conciso pero descriptivo**
2. **Descripción detallada**:
   - Para bugs: pasos para reproducir, comportamiento esperado vs. actual
   - Para features: descripción de la funcionalidad, casos de uso
3. **Etiquetas** (bug, enhancement, documentation, etc.)
4. **Asignados**: Responsables de resolver el issue
5. **Milestone**: Agrupación de issues para una versión o sprint
6. **Referencias** a otros issues o PRs relacionados

#### Plantillas de Issues

GitHub permite crear plantillas para diferentes tipos de issues:

```markdown
---
name: Bug Report
about: Create a report to help us improve
---

## Descripción del Bug
Una descripción clara y concisa del bug.

## Pasos para Reproducir
1. Ir a '...'
2. Hacer clic en '....'
3. Desplazarse hasta '....'
4. Ver el error

## Comportamiento Esperado
Una descripción clara de lo que esperabas que ocurriera.

## Capturas de Pantalla
Si aplica, añade capturas para ayudar a explicar tu problema.

## Entorno
- Sistema Operativo: [ej. Windows 10]
- Navegador: [ej. Chrome 91]
- Versión: [ej. 1.2.3]
```

#### Organización con Tableros de Proyectos

Los tableros de proyectos en GitHub permiten:
- **Visualizar** issues en formato Kanban
- **Automatizar** el movimiento de tarjetas
- **Priorizar** tareas
- **Filtrar** por diversos criterios
- **Realizar seguimiento** del progreso

### GitHub Actions: Automatización de Flujos de Trabajo

GitHub Actions permite automatizar tareas y procesos directamente en el repositorio.

#### Conceptos Fundamentales

1. **Workflow**: Proceso automatizado configurado en un repositorio
2. **Job**: Conjunto de pasos que se ejecutan en un runner
3. **Step**: Tarea individual dentro de un job
4. **Action**: Instrucción reutilizable que realiza una tarea específica
5. **Runner**: Servidor que ejecuta los workflows
6. **Event**: Actividad que desencadena un workflow

#### Estructura de un Workflow

Los workflows se definen en archivos YAML en el directorio `.github/workflows/`:

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '16'
        
    - name: Install dependencies
      run: npm install
      
    - name: Run tests
      run: npm test
```

#### Casos de Uso Comunes

GitHub Actions puede emplearse para:

1. **Integración Continua (CI)**:
   - Ejecutar tests automáticamente en cada push
   - Verificar estilo de código (linting)
   - Analizar calidad del código

2. **Despliegue Continuo (CD)**:
   - Publicar sitios web
   - Desplegar a entornos de staging o producción
   - Generar y publicar documentación

3. **Automatización de tareas**:
   - Etiquetar PRs automáticamente
   - Cerrar issues inactivos
   - Enviar notificaciones

4. **Publicación de paquetes**:
   - Publicar en npm, PyPI, Docker Hub, etc.
   - Generar releases automáticamente

#### Creación de un Action Personalizada

Puedes crear tus propias actions para reutilizar lógica:

1. **Actions compuestas**: Combinan múltiples pasos en un solo archivo YAML
2. **Actions de Docker**: Utilizan un contenedor Docker
3. **Actions de JavaScript**: Escritas en JavaScript o TypeScript

### Integrando Pull Requests, Issues y Actions

Estas tres características trabajan juntas para crear un flujo de trabajo completo:

1. **Se crea un Issue** para una nueva funcionalidad
2. **Se implementa la funcionalidad** en una rama separada
3. **Se crea un Pull Request** referenciando el issue
4. **GitHub Actions ejecuta tests** automáticamente en el PR
5. **El equipo revisa el código** y solicita cambios si es necesario
6. **Se aprueba el PR** y se fusiona con la rama principal
7. **El Issue se cierra automáticamente** al fusionar el PR
8. **GitHub Actions despliega** la nueva versión

### Buenas Prácticas

1. **Pull Requests**:
   - Mantenerlos pequeños y enfocados
   - Describir claramente el propósito
   - Responder a los comentarios de revisión de manera oportuna
   - Asegurarse de que pasan todas las verificaciones automáticas

2. **Issues**:
   - Ser específico y proporcionar toda la información necesaria
   - Usar plantillas para mantener consistencia
   - Mantener actualizado el estado
   - Cerrar issues resueltos o duplicados

3. **GitHub Actions**:
   - Mantener los workflows simples y modulares
   - Reutilizar actions existentes cuando sea posible
   - Establecer secretos para información sensible
   - Optimizar para reducir tiempo de ejecución

## Ejercicios

Para poner en práctica estos conceptos, dirígete a la carpeta [ejercicios](./ejercicios/) donde encontrarás actividades que te ayudarán a dominar el uso de Pull Requests, Issues y GitHub Actions.

## Recursos Adicionales

- [GitHub Docs: Pull Requests](https://docs.github.com/es/pull-requests)
- [GitHub Docs: Issues](https://docs.github.com/es/issues)
- [GitHub Docs: Actions](https://docs.github.com/es/actions)
- [GitHub Learning Lab: Introduction to GitHub Actions](https://lab.github.com/githubtraining/github-actions:-hello-world)
- [GitHub Learning Lab: Managing Merge Conflicts](https://lab.github.com/githubtraining/managing-merge-conflicts) 