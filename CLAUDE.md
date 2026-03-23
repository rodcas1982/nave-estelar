# Nave Estelar - Guía para Claude Code

## Descripción del Proyecto

**Nave Estelar** es un juego arcade de naves espaciales construido completamente con tecnologías web estándar (HTML5, JavaScript Vanilla, CSS3). No tiene dependencias externas ni sistema de build — todo el juego vive en un único archivo `index.html`.

## Estructura del Proyecto

```
nave-estelar/
├── index.html              # Juego completo (HTML + CSS + JS en un solo archivo)
├── index.html.backup.v*    # Backups de versiones anteriores
├── README.md               # README del repositorio
├── CLAUDE.md               # Este archivo — contexto para Claude Code
├── spaceship_generated.png # Imagen de la nave
├── assets/                 # Recursos visuales del juego
│   ├── background_space.png
│   ├── enemy_ship.png
│   ├── explosion.png
│   ├── logo.png
│   ├── powerup_*.png
│   └── PROJECT_CHARTER.md
└── docs/                   # Documentación adicional
    └── SETUP_CLAUDE_CODE.md
```

## Tecnologías

- **HTML5 Canvas** — Motor de renderizado del juego
- **JavaScript Vanilla** — Lógica del juego (sin frameworks)
- **CSS3** — Estilos y animaciones de UI
- **GitHub Pages** — Deploy automático desde rama `main`

## Cómo Ejecutar el Juego Localmente

```bash
# Opción 1: Abrir directamente en el navegador
open index.html

# Opción 2: Servidor local simple (recomendado para evitar CORS)
python3 -m http.server 8080
# Luego abrir: http://localhost:8080
```

## Convenciones de Commits

Este proyecto usa mensajes de commit con emojis descriptivos:

- `🎨` — Cambios visuales / assets
- `🚀` — Nueva versión o feature importante
- `🐛` — Bug fix
- `♻️` — Refactor

## Deploy

El juego se despliega automáticamente a GitHub Pages al hacer push a `main`:

```
https://rodcas1982.github.io/nave-estelar/
```

## Contexto Importante para Modificaciones

- Todo el código del juego está en `index.html` — buscar secciones con comentarios `/* --- SECCIÓN --- */`
- Las funciones principales del game loop: `update()`, `draw()`, `gameLoop()`
- Los backups `index.html.backup.v*` son referencias de versiones estables anteriores
- Los assets en `assets/` son imágenes PNG usadas como sprites
