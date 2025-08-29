---
description: Workflow for obtaining documentation of frameworks, libraries, languages and technologies
---

# Documentation Workflow

## Important Notes

- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis

Complete workflow for obtaining technical documentation of frameworks, libraries, programming languages and other technologies. This workflow helps find, access and use documentation efficiently.

# Documentation Workflow

Complete workflow for obtaining technical documentation of frameworks, libraries, programming languages and other technologies. This workflow helps find, access and use documentation efficiently.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete workflow within 8 steps maximum. If search takes longer than expected, use first available results.

**DECISION POINTS**: Make binary decisions quickly - use first relevant result found. Do not compare multiple options extensively.

**TERMINATION CONDITIONS**:
- If no documentation found after 3 search attempts: Provide best available alternative
- If user specifies specific technology: Focus search on that technology only
- If search commands fail: Use basic web search as fallback
- If results found: Stop and present documentation

## Steps

0. **LANGUAGE DETECTION**: Check for English keywords ("english", "documentation", "docs"). Default to Spanish.

1. **TECHNOLOGY IDENTIFICATION**:
   - Extract technology name from user input
   - Match against known categories: languages, frameworks, tools, databases
   - If unclear: Ask user for clarification and STOP
   - Set search scope to identified technology

2. **SOURCE PRIORITIZATION**:
   - Priority 1: Official documentation (docs.*domain*, developer.*domain*)
   - Priority 2: Reference sites (MDN, DevDocs, W3Schools)
   - Priority 3: GitHub repositories (README, docs/ folder)
   - Execute search in priority order

3. **SEARCH EXECUTION**:
   - Use MCP brave_web_search with specific queries:
     - `brave_web_search "${TECHNOLOGY} documentation site:docs.${DOMAIN}"`
     - `brave_web_search "${TECHNOLOGY} official docs"`
   - Limit to 3 search attempts maximum
   - If first search succeeds: Use results and proceed
   - If fails: Try alternative query and proceed

4. **CONTENT EXTRACTION**:
   - Extract key documentation sections: installation, usage, API reference
   - Prioritize practical examples and code snippets
   - Limit content to essential information only
   - If content too long: Summarize key points

5. **RESULT ORGANIZATION**:
   - Structure by categories: Getting Started, Basic Usage, Advanced Features
   - Include direct links to original documentation
   - Add practical examples where available
   - Remove redundant or outdated information

6. **DELIVERY PREPARATION**:
   - Format as clear, actionable documentation
   - Include installation instructions if relevant
   - Add troubleshooting section for common issues
   - Verify all links are accessible

7. **FINAL RESPONSE**:
   - Provide organized documentation summary
   - Include primary resource links
   - Suggest next steps or related documentation

**Language Support:**
- **Spanish**: DEFAULT - Buscar y explicar documentación en español para TODA entrada
- **English**: Si se especifica explícitamente "documentation in English" o se usan términos técnicos en inglés
- **Multilingual**: Buscar versiones en múltiples idiomas cuando sea posible

**Prerequisites:**
- Internet connection for online documentation access
- Appropriate permissions for accessing private repositories or documentation
- Text editor or IDE for viewing documentation files

## Fuentes de Documentación Principales

### Lenguajes de Programación

#### Python
```bash
# Documentación oficial
# https://docs.python.org/3/

# Instalar documentación offline
python -m pydoc -b  # Servidor local de documentación

# Documentación específica de módulos
python -c "import module_name; help(module_name)"

# PyPI y documentación de paquetes
pip show package_name  # Información básica
```

#### JavaScript/Node.js
```bash
# MDN Web Docs
# https://developer.mozilla.org/

# Node.js Documentation
# https://nodejs.org/docs/

# NPM Documentation
npm docs package_name  # Abre documentación en navegador
npm info package_name  # Información del paquete
```

#### Java
```bash
# Oracle Java Documentation
# https://docs.oracle.com/javase/

# Maven Documentation
# https://maven.apache.org/guides/

# Gradle Documentation
# https://docs.gradle.org/
```

### Frameworks Web

#### React
```bash
# Documentación oficial
# https://react.dev/

# Create React App docs
# https://create-react-app.dev/docs/

# Next.js
# https://nextjs.org/docs/
```

#### Angular
```bash
# Angular Documentation
# https://angular.io/docs/

# Angular CLI
ng help  # Comandos disponibles
ng doc component-name  # Abre documentación en navegador
```

#### Vue.js
```bash
# Vue.js Guide
# https://vuejs.org/guide/

# Nuxt.js
# https://nuxt.com/docs/
```

#### Django (Python)
```bash
# Django Documentation
# https://docs.djangoproject.com/

# Django Admin
python manage.py help  # Comandos disponibles
```

### Librerías y Herramientas

#### Docker
```bash
# Docker Documentation
# https://docs.docker.com/

# Docker CLI
docker --help  # Comandos disponibles
docker command --help  # Ayuda específica
```

#### Kubernetes
```bash
# Kubernetes Documentation
# https://kubernetes.io/docs/

# kubectl
kubectl --help  # Comandos disponibles
kubectl explain resource.type  # Explicación de recursos
```

#### Git
```bash
# Git Documentation
# https://git-scm.com/docs/

# Ayuda local
git help  # Lista de comandos
git help command  # Ayuda específica
man git-command  # Manual pages
```

## Servicios en la Nube

### AWS
```bash
# AWS Documentation
# https://docs.aws.amazon.com/

# AWS CLI
aws --help  # Comandos disponibles
aws service help  # Documentación de servicio específico
```

### Google Cloud
```bash
# Google Cloud Documentation
# https://cloud.google.com/docs/

# gcloud CLI
gcloud --help  # Comandos disponibles
gcloud topic topic-name  # Documentación de temas específicos
```

### Azure
```bash
# Azure Documentation
# https://docs.microsoft.com/azure/

# Azure CLI
az --help  # Comandos disponibles
az find "search term"  # Buscar comandos
```

## Bases de Datos

### MongoDB
```bash
# MongoDB Documentation
# https://docs.mongodb.com/

# MongoDB Shell
mongosh --help  # Comandos disponibles
db.help()  # Ayuda de base de datos
```

### PostgreSQL
```bash
# PostgreSQL Documentation
# https://www.postgresql.org/docs/

# psql
psql --help  # Comandos disponibles
\?  # Ayuda dentro de psql
\help command  # Ayuda específica
```

## Herramientas de Desarrollo

### VS Code
```bash
# VS Code Documentation
# https://code.visualstudio.com/docs/

# Extensiones
# https://marketplace.visualstudio.com/
```

### IntelliJ IDEA
```bash
# IntelliJ Documentation
# https://www.jetbrains.com/idea/documentation/
```

## Estrategias de Búsqueda

### 1. Documentación Oficial Primero
- Siempre buscar en el sitio oficial del proyecto
- Verificar la versión específica que se está usando
- Buscar guías de migración entre versiones

### 2. Comunidades y Foros
- Stack Overflow para problemas específicos
- GitHub Issues para bugs y feature requests
- Reddit (r/programming, r/learnprogramming)
- Discord/Slack communities del proyecto

### 3. Cursos y Tutoriales
- freeCodeCamp, Codecademy
- YouTube channels especializados
- Egghead.io, Pluralsight
- Documentación con ejemplos prácticos

### 4. Blogs Técnicos
- Medium, Dev.to
- Blogs oficiales de empresas
- Personal blogs de maintainers
- Newsletters técnicas

## Comandos Útiles para Documentación

```bash
# Buscar documentación local
man command_name  # Manual pages en Linux/Unix
info command_name  # Info pages
tldr command_name  # Simplified man pages

# Buscar en paquetes
apt-cache search keyword  # Debian/Ubuntu
yum search keyword  # CentOS/RHEL
brew search keyword  # macOS

# Información de paquetes
pip show package_name  # Python
npm info package_name  # Node.js
gem info gem_name  # Ruby
```

## Mejores Prácticas

### Organización
- Crear bookmarks/carpetas por tecnología
- Mantener versiones de documentación offline
- Usar herramientas como DevDocs.io para acceso rápido
- Crear notas personales de comandos frecuentes

### Actualización
- Verificar fechas de última actualización
- Suscribirse a changelogs oficiales
- Seguir releases y anuncios importantes
- Mantener documentación actualizada

### Eficiencia
- Aprender atajos de teclado del IDE
- Usar extensiones para documentación integrada
- Crear snippets para consultas frecuentes
- Establecer flujos de trabajo consistentes

## Troubleshooting de Documentación

### Problemas Comunes
- **Documentación desactualizada**: Verificar fechas y versiones
- **Diferencias entre versiones**: Comparar changelogs
- **Documentación en inglés**: Usar traductores o buscar versiones en español
- **Ejemplos no funcionales**: Verificar sintaxis y dependencias

### Recursos Adicionales
- **DevDocs**: Documentación offline de múltiples tecnologías
- **Dash/Zeal**: Aplicaciones de documentación offline
- **ExplainShell**: Explicación de comandos de terminal
- **tldr**: Páginas de manual simplificadas

**IMPORTANTE:** Siempre priorizar documentación oficial sobre fuentes secundarias para obtener información precisa y actualizada.

**Idiomas Soportados:**
- **Español**: DEFAULT - Buscar y explicar documentación en español
- **English**: Si se especifica explícitamente "documentation in English"
- **Multilingual**: Buscar versiones en múltiples idiomas cuando sea posible