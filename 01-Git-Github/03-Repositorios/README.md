# Repositorios en Git

## Introducción

Los repositorios son la unidad fundamental de organización en Git. Un repositorio Git contiene toda la historia del proyecto, incluyendo todos los archivos y directorios, así como los metadatos necesarios para administrar las diferentes versiones. En esta sección exploraremos la estructura y gestión de repositorios tanto locales como remotos.

## Objetivos de Aprendizaje
- Comprender la estructura de un repositorio Git
- Aprender a crear y configurar repositorios locales
- Dominar la interacción entre repositorios locales y remotos
- Configurar adecuadamente Git para un flujo de trabajo eficiente

## Contenido

### Estructura de un Repositorio Git

Un repositorio Git consta de dos partes principales:

1. **Directorio de trabajo:** Contiene los archivos que estás editando y con los que trabajas directamente.

2. **Directorio .git:** Contiene toda la base de datos y configuración del repositorio. Es la parte "mágica" donde Git administra versiones.

La estructura básica de un directorio `.git` incluye:

```
.git/
  ├── HEAD           # Referencia a la rama actual
  ├── config         # Configuración específica del repositorio
  ├── description    # Descripción del repositorio (usado por GitWeb)
  ├── hooks/         # Scripts que se ejecutan en eventos específicos
  ├── index          # El área de preparación (staging area)
  ├── objects/       # Base de datos de objetos (commits, trees, blobs)
  │   ├── info/
  │   └── pack/
  └── refs/          # Referencias (ramas, etiquetas)
      ├── heads/     # Ramas locales
      ├── remotes/   # Ramas remotas
      └── tags/      # Etiquetas
```

### Repositorios Locales

#### Creación de un Repositorio

Existen dos formas principales de iniciar un repositorio Git:

1. **Crear un repositorio nuevo:**
   ```bash
   mkdir mi-proyecto
   cd mi-proyecto
   git init
   ```
   Esto crea un directorio `.git` y prepara el repositorio para su uso.

2. **Clonar un repositorio existente:**
   ```bash
   git clone https://github.com/usuario/repositorio.git
   git clone git@github.com:usuario/repositorio.git  # Usando SSH
   git clone /ruta/local/a/otro/repositorio          # Desde una ruta local
   ```
   Al clonar obtienes una copia completa del historial del proyecto.

#### Creación de un Repositorio "Bare"

Un repositorio "bare" (desnudo) no tiene directorio de trabajo y está diseñado para ser un repositorio remoto compartido:

```bash
git init --bare mi-repo-compartido.git
```

Este tipo de repositorio se utiliza típicamente en servidores para compartir entre múltiples desarrolladores.

#### Configuración Básica de Git

Antes de empezar a trabajar con Git, es recomendable configurar algunos parámetros básicos:

1. **Configuración global (aplica a todos los repositorios del usuario):**
   ```bash
   git config --global user.name "Tu Nombre"
   git config --global user.email "tu.email@ejemplo.com"
   git config --global core.editor "nano"  # O tu editor preferido
   git config --global init.defaultBranch main  # Establecer nombre de rama por defecto
   ```

2. **Configuración local (específica de un repositorio):**
   ```bash
   cd mi-proyecto
   git config user.name "Nombre Diferente"
   git config user.email "otro.email@ejemplo.com"
   ```

3. **Ver la configuración actual:**
   ```bash
   git config --list
   git config user.name  # Ver un valor específico
   ```

#### Archivos de Configuración

La configuración de Git se almacena en diferentes archivos según su alcance:

- **`/etc/gitconfig`**: Configuración a nivel de sistema (todos los usuarios)
- **`~/.gitconfig`** o **`~/.config/git/config`**: Configuración global de usuario
- **`.git/config`**: Configuración específica del repositorio

#### Archivo .gitignore

El archivo `.gitignore` permite especificar archivos y directorios que Git debe ignorar:

```
# Ignorar archivos compilados
*.o
*.exe

# Ignorar directorios
/node_modules/
/dist/

# Ignorar archivos de configuración local
.env.local
```

Algunas buenas prácticas para `.gitignore`:
- Incluir archivos generados automáticamente
- Incluir dependencias que se pueden reconstruir
- Incluir archivos con información sensible o personalizada
- No ignorar archivos de configuración que deban ser compartidos

### Repositorios Remotos

#### Concepto y Propósito

Un repositorio remoto es una versión de tu proyecto alojada en internet o en una red. Permite:
- Colaboración entre múltiples desarrolladores
- Respaldo del código fuente
- Despliegue y distribución del software

#### Servicios Populares

- **GitHub**: La plataforma más grande, con funciones de redes sociales
- **GitLab**: Ofrece CI/CD integrado, puede ser self-hosted
- **Bitbucket**: Integrado con otros productos de Atlassian
- **Azure DevOps**: Solución integrada de Microsoft

#### Configuración de Repositorios Remotos

1. **Ver los remotos configurados:**
   ```bash
   git remote -v
   ```

2. **Añadir un remoto:**
   ```bash
   git remote add origin https://github.com/usuario/repo.git
   git remote add upstream https://github.com/original/repo.git  # Para forks
   ```

3. **Cambiar URL de un remoto:**
   ```bash
   git remote set-url origin git@github.com:usuario/repo.git
   ```

4. **Eliminar un remoto:**
   ```bash
   git remote remove nombre-remoto
   ```

#### Protocolos de Acceso

Git soporta varios protocolos para acceder a repositorios remotos:

1. **HTTPS**:
   - Ejemplo: `https://github.com/usuario/repo.git`
   - Ventajas: Fácil de configurar, funciona a través de firewalls
   - Desventajas: Puede requerir autenticación repetida

2. **SSH**:
   - Ejemplo: `git@github.com:usuario/repo.git`
   - Ventajas: Seguro, permite autenticación sin contraseña con claves
   - Desventajas: Requiere configuración de claves SSH

3. **Git**:
   - Ejemplo: `git://github.com/usuario/repo.git`
   - Ventajas: Más rápido, sin autenticación
   - Desventajas: No encriptado, generalmente solo lectura

4. **Local**:
   - Ejemplo: `/ruta/a/repositorio` o `file:///ruta/a/repositorio`
   - Ventajas: No requiere red, muy rápido
   - Desventajas: Solo disponible localmente

#### Configuración de SSH para GitHub/GitLab

Usar SSH facilita la autenticación sin necesidad de introducir credenciales:

1. **Generar una clave SSH:**
   ```bash
   ssh-keygen -t ed25519 -C "tu.email@ejemplo.com"
   # O si no soporta ed25519:
   ssh-keygen -t rsa -b 4096 -C "tu.email@ejemplo.com"
   ```

2. **Añadir la clave al agente SSH:**
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   ```

3. **Copiar la clave pública:**
   ```bash
   cat ~/.ssh/id_ed25519.pub
   # Copiar el contenido
   ```

4. **Añadir la clave a tu cuenta de GitHub/GitLab**:
   - Ve a Configuración > Claves SSH
   - Pega tu clave pública

5. **Probar la conexión:**
   ```bash
   ssh -T git@github.com
   ```

### Clonación y Sincronización

#### Clonación de Repositorios

```bash
# Clonar y mantener el mismo nombre
git clone https://github.com/usuario/repo.git

# Clonar a un directorio específico
git clone https://github.com/usuario/repo.git mi-directorio

# Clonar una rama específica
git clone -b nombre-rama https://github.com/usuario/repo.git

# Clonar de forma superficial (solo el commit más reciente)
git clone --depth 1 https://github.com/usuario/repo.git
```

#### Sincronización con Repositorios Remotos

1. **Descargar cambios sin integrarlos:**
   ```bash
   git fetch origin
   git fetch --all  # Todos los remotos
   ```

2. **Descargar e integrar cambios (fetch + merge):**
   ```bash
   git pull origin main
   git pull  # Rama actual desde el remoto predeterminado
   ```

3. **Pull con rebase en lugar de merge:**
   ```bash
   git pull --rebase origin main
   ```

4. **Subir cambios locales al remoto:**
   ```bash
   git push origin main
   git push  # Rama actual al remoto predeterminado
   
   # Forzar push (usar con precaución)
   git push -f origin main
   ```

5. **Configurar tracking de rama:**
   ```bash
   # Al crear una rama
   git checkout -b feature origin/feature
   
   # Para una rama existente
   git branch --set-upstream-to=origin/feature feature
   ```

### Gestión de Múltiples Remotos

#### Escenarios comunes

1. **Contribuir a un proyecto open source (fork workflow):**
   ```bash
   # Después de hacer fork en GitHub/GitLab
   git clone https://github.com/tu-usuario/proyecto.git
   cd proyecto
   git remote add upstream https://github.com/proyecto-original/proyecto.git
   
   # Mantener tu fork actualizado
   git fetch upstream
   git checkout main
   git merge upstream/main
   git push origin main
   ```

2. **Trabajar con múltiples entornos:**
   ```bash
   git remote add production git@servidor-produccion:proyecto.git
   git remote add staging git@servidor-staging:proyecto.git
   
   git push production main
   git push staging feature-branch
   ```

## Buenas Prácticas

1. **Configuración consistente**: Mantén la misma configuración de usuario en todos tus proyectos para mantener coherencia en el historial de commits.

2. **Organización de repositorios**: 
   - Un repositorio por proyecto lógico
   - Evitar repositorios demasiado grandes
   - Considerar el uso de submódulos o monorepos según el caso

3. **Política de ramas**:
   - Mantener main/master siempre en estado funcional
   - Usar ramas para características, correcciones y versiones
   - Establecer convenciones de nomenclatura

4. **Seguridad**:
   - No almacenar credenciales en el código
   - Utilizar .gitignore para archivos sensibles
   - Configurar correctamente los permisos en repositorios compartidos

## Ejercicios

Para realizar los ejercicios prácticos, dirígete a la carpeta [ejercicios](./ejercicios/) donde encontrarás actividades para practicar la creación y gestión de repositorios Git.

## Recursos Adicionales

- [Pro Git: Capítulo sobre Repositorios Git](https://git-scm.com/book/es/v2/Fundamentos-de-Git-Trabajando-con-Remotos)
- [Documentación Oficial de GitHub sobre Conexión SSH](https://docs.github.com/es/authentication/connecting-to-github-with-ssh)
- [Guía de Gitignore](https://www.atlassian.com/git/tutorials/saving-changes/gitignore) 