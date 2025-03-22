# Versionado Semántico

## Introducción

El versionado semántico (SemVer) es un conjunto de reglas y requisitos que dictan cómo se asignan y se incrementan los números de versión en el software. Este sistema de versionado ofrece un método claro para comunicar cambios en el código, facilitando la gestión de dependencias y la compatibilidad entre diferentes piezas de software. En el desarrollo moderno, comprender y aplicar correctamente el versionado semántico es esencial para mantener proyectos estables y predecibles.

## Objetivos de Aprendizaje
- Comprender el concepto y la importancia del versionado semántico
- Dominar la estructura y significado de las versiones: Mayor, Menor, Parche
- Aprender a gestionar versiones en Git mediante tags
- Implementar releases en GitHub siguiendo prácticas profesionales

## Contenido

### Fundamentos del Versionado Semántico

#### ¿Qué es el Versionado Semántico?

El versionado semántico es una especificación para numerar las versiones de software que sigue el formato X.Y.Z, donde:

- **X** representa la versión **MAYOR** (MAJOR)
- **Y** representa la versión **MENOR** (MINOR)
- **Z** representa la versión de **PARCHE** (PATCH)

Cada uno de estos números tiene un significado específico y se incrementa según reglas concretas.

#### Reglas Básicas

1. Una vez que un software versionado ha sido liberado, los contenidos de esa versión NO DEBEN ser modificados. Cualquier modificación DEBE ser liberada como una nueva versión.

2. La versión **MAYOR** (X) se incrementa cuando se realizan cambios incompatibles en la API pública.

3. La versión **MENOR** (Y) se incrementa cuando se añade funcionalidad compatible con versiones anteriores.

4. La versión de **PARCHE** (Z) se incrementa cuando se implementan correcciones de errores compatibles con versiones anteriores.

5. Pueden incluirse etiquetas adicionales para metadata de pre-lanzamiento y metadata de compilación como extensiones al formato MAYOR.MENOR.PARCHE.

#### Ejemplos Prácticos

| Versión | Descripción |
|---------|-------------|
| 1.0.0   | Versión inicial estable |
| 1.0.1   | Corrección de errores |
| 1.1.0   | Nueva funcionalidad compatible |
| 2.0.0   | Cambio que rompe compatibilidad |
| 1.0.0-alpha | Versión alfa (pre-release) |
| 1.0.0-beta.1 | Versión beta 1 |

#### Etiquetas de Pre-lanzamiento

Las etiquetas de pre-lanzamiento indican que la versión no está lista para producción:

```
1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-beta < 1.0.0-beta.2 < 1.0.0-rc.1 < 1.0.0
```

Estas etiquetas son útiles para realizar pruebas progresivas antes de un lanzamiento estable.

### Versionado en el Desarrollo de Software

#### Beneficios del Versionado Semántico

1. **Comunicación clara**: Los desarrolladores entienden inmediatamente el impacto de una actualización.

2. **Gestión de dependencias**: Los sistemas de gestión de paquetes pueden trabajar de manera más eficiente.

3. **Compatibilidad**: Facilita determinar si una actualización es segura para un proyecto existente.

4. **Automatización**: Permite automatizar despliegues y actualizaciones basándose en reglas claras.

#### Implementación en Diferentes Lenguajes

El versionado semántico se aplica en diversos ecosistemas:

- **JavaScript/Node.js**: En `package.json`
  ```json
  {
    "name": "mi-paquete",
    "version": "1.2.3",
    "dependencies": {
      "otro-paquete": "^2.0.0"
    }
  }
  ```

- **Python**: En `setup.py` o `pyproject.toml`
  ```python
  setup(
      name="mi-paquete",
      version="1.2.3",
      install_requires=["otro-paquete>=2.0.0,<3.0.0"],
  )
  ```

- **Java/Maven**: En `pom.xml`
  ```xml
  <project>
      <version>1.2.3</version>
      <dependencies>
          <dependency>
              <groupId>com.example</groupId>
              <artifactId>otro-paquete</artifactId>
              <version>[2.0.0,3.0.0)</version>
          </dependency>
      </dependencies>
  </project>
  ```

#### Especificadores de Versión

En sistemas de gestión de paquetes, existen diferentes formas de especificar rangos de versiones compatibles:

- **Exacta**: `=1.2.3` - Solo la versión 1.2.3
- **Mayor o igual**: `>=1.2.3` - 1.2.3 o superior
- **Compatible con**: `^1.2.3` - Desde 1.2.3 hasta < 2.0.0
- **Aproximadamente igual**: `~1.2.3` - Desde 1.2.3 hasta < 1.3.0
- **Rango**: `>=1.2.3 <2.0.0` - Entre 1.2.3 y 2.0.0 (excluyendo 2.0.0)

### Tags en Git

Git proporciona el concepto de "tags" (etiquetas) que son perfectos para marcar versiones específicas en el historial de un repositorio.

#### Creación de Tags

```bash
# Crear un tag ligero
git tag v1.0.0

# Crear un tag anotado (recomendado para versiones)
git tag -a v1.0.0 -m "Versión 1.0.0 - Lanzamiento inicial estable"

# Crear un tag para un commit específico
git tag -a v1.0.1 -m "Corrección urgente" 9fceb02
```

#### Listado y Visualización de Tags

```bash
# Listar todos los tags
git tag

# Listar tags con un patrón
git tag -l "v1.0.*"

# Ver detalles de un tag específico
git show v1.0.0
```

#### Compartir Tags

Por defecto, los tags no se envían al repositorio remoto con `git push`. Debes enviarlos explícitamente:

```bash
# Enviar un tag específico
git push origin v1.0.0

# Enviar todos los tags
git push origin --tags
```

#### Checkout a Tags

Puedes hacer checkout a un tag específico para revisar el código en esa versión:

```bash
git checkout v1.0.0

# Para hacer cambios, debes crear una rama
git checkout -b version-1-fixes v1.0.0
```

#### Eliminar Tags

```bash
# Eliminar un tag local
git tag -d v1.0.0

# Eliminar un tag remoto
git push origin --delete v1.0.0
```

### Releases en GitHub

GitHub ofrece una interfaz dedicada para la gestión de releases, basada en los tags de Git pero con funcionalidades adicionales.

#### Creación de un Release

1. **Desde la interfaz web**:
   - Ve a tu repositorio en GitHub
   - Haz clic en "Releases"
   - Haz clic en "Draft a new release"
   - Selecciona un tag existente o crea uno nuevo
   - Completa el título y la descripción
   - Opcionalmente, añade archivos binarios
   - Marca como pre-release si corresponde
   - Publica el release

2. **Desde línea de comandos usando GitHub CLI**:
   ```bash
   # Instalar GitHub CLI si no la tienes
   # brew install gh (Mac) o apt install gh (Ubuntu)
   
   # Autenticarse
   gh auth login
   
   # Crear release
   gh release create v1.0.0 --title "Versión 1.0.0" --notes "Notas del release"
   
   # Crear pre-release
   gh release create v1.1.0-beta.1 --prerelease --title "Beta 1 de v1.1.0"
   ```

#### Estructura de Notas de Release

Un buen release debe tener notas detalladas, generalmente incluyendo:

1. **Resumen**: Breve descripción de lo que incluye la versión
2. **Nuevas características**: Listado de funcionalidades añadidas
3. **Correcciones**: Bugs solucionados
4. **Cambios incompatibles**: Si hay breaking changes
5. **Instrucciones de actualización**: Pasos para actualizar desde versiones anteriores
6. **Reconocimientos**: Agradecimientos a contribuyentes

Ejemplo:
```markdown
# Release v2.0.0

## 🚀 Nuevas Características

- Implementado sistema de autenticación con OAuth
- Añadido soporte para múltiples idiomas
- Nueva interfaz de usuario con Material Design

## 🐛 Correcciones

- Solucionado error al cargar imágenes grandes (#123)
- Corregido problema de rendimiento en búsquedas complejas (#145)
- Arreglados varios typos en la documentación

## ⚠️ Cambios Incompatibles

- La API de autenticación ha cambiado completamente
- El formato de configuración de idiomas es ahora JSON en lugar de YAML

## 📝 Instrucciones de Actualización

1. Actualiza tus llamadas a la API de autenticación
2. Convierte tus archivos de idiomas a formato JSON
3. Ejecuta el script de migración incluido

## 👏 Reconocimientos

Gracias a @usuario1, @usuario2 y @usuario3 por sus contribuciones a este release.
```

#### Automatización de Releases

Puedes automatizar la creación de releases usando GitHub Actions:

```yaml
name: Create Release

on:
  push:
    tags:
      - 'v*'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
        
      - name: Build project
        run: |
          # Comandos para construir el proyecto
          npm install
          npm run build
          
      - name: Create Release
        id: create_release
        uses: actions/create-release@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          tag_name: ${{ github.ref }}
          release_name: Release ${{ github.ref }}
          draft: false
          prerelease: false
          
      - name: Upload Release Asset
        uses: actions/upload-release-asset@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          upload_url: ${{ steps.create_release.outputs.upload_url }}
          asset_path: ./dist/mi-app.zip
          asset_name: mi-app.zip
          asset_content_type: application/zip
```

### Gestión de Changelog

Un fichero CHANGELOG.md es una práctica recomendada para documentar los cambios entre versiones.

#### Formato Estándar

```markdown
# Changelog

Todos los cambios notables a este proyecto serán documentados en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/),
y este proyecto adhiere a [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [No publicado]

### Añadido
- Nueva funcionalidad X

## [1.1.0] - 2023-10-15

### Añadido
- Funcionalidad Y
- Soporte para Z

### Cambiado
- Refactorización de la clase A

### Corregido
- Bug en el módulo B (#123)

## [1.0.0] - 2023-09-01

### Añadido
- Lanzamiento inicial
```

#### Automatización de Changelog

Existen herramientas para generar automáticamente el changelog basándose en los mensajes de commit:

```bash
# Instalar standard-version para Node.js
npm install --save-dev standard-version

# Añadir script en package.json
# "release": "standard-version"

# Generar nueva versión y changelog
npm run release
```

Esto funciona especialmente bien cuando se utilizan mensajes de commit convencionales (Conventional Commits).

### Buenas Prácticas

1. **Sigue rigurosamente las reglas de SemVer**: No incrementes la versión MAYOR por cambios menores.

2. **Documenta todos los cambios públicos**: Los usuarios deben poder entender qué ha cambiado entre versiones.

3. **Prueba exhaustivamente antes de cada release**: Especialmente importante para versiones estables.

4. **Utiliza pre-releases para pruebas**: Versiones alpha, beta y RC para obtener feedback antes de una versión estable.

5. **Automatiza el proceso**: Usa CI/CD para asegurar la consistencia en cada release.

6. **Mantén múltiples líneas de versiones cuando sea necesario**: Da soporte a versiones anteriores para permitir actualizaciones graduales.

7. **Comunica claramente los breaking changes**: Deben ser evidentes en la documentación y en el número de versión.

## Ejercicios

Para practicar estos conceptos, dirígete a la carpeta [ejercicios](./ejercicios/) donde encontrarás actividades para implementar versionado semántico en proyectos reales.

## Recursos Adicionales

- [Especificación oficial de Semantic Versioning](https://semver.org/spec/v2.0.0.html)
- [Keep a Changelog](https://keepachangelog.com/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Git Tagging Docs](https://git-scm.com/book/en/v2/Git-Basics-Tagging)
- [GitHub Releases Documentation](https://docs.github.com/es/repositories/releasing-projects-on-github/about-releases) 