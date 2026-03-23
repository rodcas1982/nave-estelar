# Configuración del Proyecto con Claude Code

Esta guía explica cómo trabajar con el proyecto **Nave Estelar** usando Claude Code en tu computadora.

---

## Requisitos Previos

- **Git** instalado
- **Claude Code** instalado (`npm install -g @anthropic-ai/claude-code`)
- Una cuenta en [Claude.ai](https://claude.ai) o una API key de Anthropic
- Un navegador moderno (Chrome, Firefox, Safari, Edge)

---

## 1. Instalación de Claude Code

```bash
# Instalar Claude Code globalmente via npm
npm install -g @anthropic-ai/claude-code

# Verificar la instalación
claude --version
```

Si no tienes npm, instala Node.js desde https://nodejs.org (versión 18 o superior).

---

## 2. Clonar el Repositorio

```bash
git clone https://github.com/rodcas1982/nave-estelar.git
cd nave-estelar
```

---

## 3. Iniciar Claude Code en el Proyecto

```bash
# Desde la carpeta del proyecto
claude
```

Claude Code leerá automáticamente el archivo `CLAUDE.md` en la raíz del proyecto para entender el contexto: tecnologías usadas, estructura de archivos, convenciones de commits y cómo ejecutar el juego.

---

## 4. Autenticación

La primera vez que ejecutes `claude`, se abrirá el flujo de autenticación:

```
? How would you like to authenticate?
> Login with Claude.ai (recommended)
  Enter API key
```

Selecciona **Login with Claude.ai** y sigue las instrucciones en el navegador, o ingresa tu API key de Anthropic directamente.

---

## 5. Ejecutar el Juego Localmente

El proyecto no requiere instalación de dependencias. Para ver el juego en el navegador:

```bash
# Opción simple — abrir directamente
open index.html          # macOS
xdg-open index.html      # Linux
start index.html         # Windows

# Opción recomendada — servidor local (evita restricciones CORS)
python3 -m http.server 8080
# Abrir en el navegador: http://localhost:8080
```

---

## 6. Flujo de Trabajo con Claude Code

Una vez dentro de la sesión interactiva de Claude Code, puedes hacer peticiones en lenguaje natural:

### Ejemplos de Comandos Útiles

```
# Pedir ayuda para entender el código
"Explícame cómo funciona el sistema de power-ups en index.html"

# Solicitar cambios
"Agrega un nuevo tipo de enemigo que sea más rápido"

# Depurar problemas
"El juego se congela al recoger el escudo, ayúdame a encontrar el bug"

# Revisar antes de hacer commit
"Revisa los cambios que hice y crea un commit descriptivo"
```

### Comandos de Slash Útiles

| Comando | Descripción |
|---------|-------------|
| `/help` | Ver todos los comandos disponibles |
| `/clear` | Limpiar el historial de la conversación |
| `/compact` | Resumir la conversación para liberar contexto |
| `/cost` | Ver el uso de tokens de la sesión actual |
| `/review` | Revisar los cambios pendientes |
| `/commit` | Crear un commit con mensaje generado automáticamente |

---

## 7. Estructura del Proyecto para Claude Code

El archivo `CLAUDE.md` en la raíz le indica a Claude Code:

- **Qué es el proyecto**: juego arcade HTML5 sin dependencias
- **Dónde está el código**: todo en `index.html`
- **Cómo ejecutarlo**: con un servidor local simple
- **Convenciones de commits**: formato con emojis
- **Dónde está el deploy**: GitHub Pages

Claude Code usa este contexto en cada sesión automáticamente.

---

## 8. Hacer Cambios y Publicar

```bash
# 1. Abrir Claude Code en el proyecto
cd nave-estelar
claude

# 2. Pedirle cambios a Claude (ejemplos)
"Mejora los efectos de explosión para que duren más tiempo"
"Agrega un contador de enemigos eliminados en la UI"

# 3. Claude modifica los archivos directamente
# Puedes revisar los cambios antes de aprobarlos

# 4. Crear el commit (Claude puede ayudarte)
"Crea un commit con los cambios que acabamos de hacer"

# 5. Publicar a GitHub Pages
git push origin main
# El juego se actualiza automáticamente en:
# https://rodcas1982.github.io/nave-estelar/
```

---

## 9. Modo No Interactivo (Automatización)

Claude Code también puede ejecutarse en modo no interactivo para tareas específicas:

```bash
# Ejecutar una tarea puntual sin sesión interactiva
claude -p "Revisa index.html y lista todos los power-ups disponibles"

# Imprimir resultado en formato texto plano
claude --output-format text -p "Resume los controles del juego"
```

---

## 10. Permisos y Seguridad

Claude Code pedirá confirmación antes de:

- Modificar archivos del proyecto
- Ejecutar comandos de terminal
- Hacer commits o push a Git

Puedes configurar permisos automáticos para comandos frecuentes en el archivo de configuración de Claude Code:

```bash
# Ver configuración actual
claude config list

# Permitir comandos específicos sin confirmación (ejemplo)
claude config set --global allowedTools "Bash(git add:*),Bash(git commit:*)"
```

---

## Recursos Adicionales

- [Documentación oficial de Claude Code](https://docs.anthropic.com/en/docs/claude-code)
- [GitHub del proyecto](https://github.com/rodcas1982/nave-estelar)
- [Juego en vivo](https://rodcas1982.github.io/nave-estelar/)
- [Reporte de problemas](https://github.com/rodcas1982/nave-estelar/issues)
