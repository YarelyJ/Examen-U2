# Public Directory / Directorio Público

Este directorio contiene archivos estáticos que se sirven directamente desde la raíz de tu aplicación.

## Qué va en el directorio `public`:

### 1. Favicons e Iconos
- `favicon.ico` - Icono principal del navegador (16x16, 32x32, 48x48)
- `icon.svg` - Icono SVG moderno
- `apple-icon.png` - Icono para dispositivos Apple (180x180)
- `icon-192.png` - Icono PWA (192x192)
- `icon-512.png` - Icono PWA (512x512)

### 2. Imágenes y Assets
- `/images/` - Imágenes del sitio (logos, backgrounds, etc.)
- `/fonts/` - Fuentes personalizadas (si no usas Google Fonts)
- `/videos/` - Videos estáticos
- `/audio/` - Archivos de audio

### 3. Archivos de Configuración
- `robots.txt` - Instrucciones para crawlers de búsqueda
- `sitemap.xml` - Mapa del sitio para SEO
- `manifest.json` - Configuración de PWA (Progressive Web App)

### 4. Documentos Estáticos
- PDFs, documentos descargables
- Archivos de verificación (google-site-verification, etc.)

## Cómo usar archivos del public:

En tu código, refiérelos desde la raíz:

\`\`\`tsx
// Correcto
<img src="/images/logo.png" alt="Logo" />

// Incorrecto
<img src="/public/images/logo.png" alt="Logo" />
\`\`\`

## Archivos actuales en este proyecto:

- `favicon.ico` - Icono del navegador
- `icon.svg` - Icono vectorial
- `apple-icon.png` - Icono para iOS
- `robots.txt` - Configuración de SEO
- `manifest.json` - Configuración de PWA
