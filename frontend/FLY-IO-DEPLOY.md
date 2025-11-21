# 🚀 Guía de Despliegue en Fly.io

## Frontend Next.js en Fly.io

### Prerequisitos

1. **Instalar Fly CLI**
\`\`\`bash
# macOS/Linux
curl -L https://fly.io/install.sh | sh

# Windows (PowerShell)
iwr https://fly.io/install.ps1 -useb | iex
\`\`\`

2. **Login en Fly.io**
\`\`\`bash
flyctl auth login
\`\`\`

---

## 📦 Paso 1: Configurar el Proyecto

### 1.1 Navegar a la carpeta frontend
\`\`\`bash
cd frontend
\`\`\`

### 1.2 Verificar archivos creados
- ✅ `Dockerfile` - Configuración de contenedor
- ✅ `fly.toml` - Configuración de Fly.io
- ✅ `.dockerignore` - Archivos a ignorar
- ✅ `next.config.js` - Con `output: 'standalone'`

---

## 🛠️ Paso 2: Crear la Aplicación en Fly.io

### 2.1 Inicializar (si no existe)
\`\`\`bash
flyctl launch --no-deploy
\`\`\`

**Responde las preguntas:**
- App name: `exaxistone2` (o el nombre que prefieras)
- Region: Elige la más cercana a tus usuarios
- Postgresql: No
- Redis: No

### 2.2 Si ya existe la app
El archivo `fly.toml` ya tiene configurado `app = 'exaxistone2'`

---

## 🔐 Paso 3: Configurar Variables de Entorno

### 3.1 Agregar la URL del backend
\`\`\`bash
flyctl secrets set NEXT_PUBLIC_API_URL=https://tu-backend.onrender.com
\`\`\`

**Importante:** Reemplaza `tu-backend.onrender.com` con la URL real de tu backend Django en Render.

### 3.2 Verificar secrets
\`\`\`bash
flyctl secrets list
\`\`\`

---

## 🚀 Paso 4: Desplegar

### 4.1 Desplegar la aplicación
\`\`\`bash
flyctl deploy
\`\`\`

Este comando:
- Construye la imagen Docker con npm (NO pnpm)
- Sube la imagen a Fly.io
- Despliega la aplicación
- Toma aproximadamente 3-5 minutos

### 4.2 Verificar estado
\`\`\`bash
flyctl status
\`\`\`

### 4.3 Ver logs en tiempo real
\`\`\`bash
flyctl logs
\`\`\`

---

## 🌐 Paso 5: Abrir la Aplicación

\`\`\`bash
flyctl open
\`\`\`

Tu aplicación estará disponible en:
`https://exaxistone2.fly.dev`

---

## ⚙️ Configuración Importante

### Memoria y CPU
El `fly.toml` está configurado con:
- **Memoria:** 1GB
- **CPU:** 1 core compartido
- **Auto-scaling:** Se apaga cuando no hay tráfico

### Puerto
- **Puerto interno:** 8080 (configurado en fly.toml)
- **Puerto externo:** 443 (HTTPS automático)

---

## 🔧 Comandos Útiles

### Ver información de la app
\`\`\`bash
flyctl info
\`\`\`

### Escalar la app
\`\`\`bash
# Aumentar memoria
flyctl scale memory 2048

# Aumentar instancias
flyctl scale count 2
\`\`\`

### SSH a la máquina
\`\`\`bash
flyctl ssh console
\`\`\`

### Ver métricas
\`\`\`bash
flyctl dashboard
\`\`\`

### Redeploy rápido
\`\`\`bash
flyctl deploy --remote-only
\`\`\`

---

## 🐛 Troubleshooting

### Error: "pnpm no encontrado"
✅ **Solucionado** - El Dockerfile usa `npm` en lugar de `pnpm`

### Error: "Failed to build"
\`\`\`bash
# Limpiar caché y volver a intentar
flyctl deploy --no-cache
\`\`\`

### Error: "Health checks failing"
Verifica los logs:
\`\`\`bash
flyctl logs
\`\`\`

Asegúrate de que:
- El puerto 8080 esté configurado correctamente
- `NEXT_PUBLIC_API_URL` esté configurado
- El backend esté funcionando

### Error: "Out of memory"
Aumenta la memoria:
\`\`\`bash
flyctl scale memory 2048
\`\`\`

### La app no carga datos del backend
1. Verifica la variable de entorno:
\`\`\`bash
flyctl secrets list
\`\`\`

2. Asegúrate de que el backend permita CORS desde tu dominio Fly.io
3. Verifica que la URL del backend esté correcta

---

## 🔄 Actualizar Después de Cambios

Cada vez que hagas cambios en el código:

\`\`\`bash
cd frontend
flyctl deploy
\`\`\`

Fly.io automáticamente:
- Detecta cambios
- Reconstruye la imagen
- Despliega la nueva versión
- Hace zero-downtime deployment

---

## 💰 Costos

**Free Tier incluye:**
- 3 máquinas compartidas 256MB
- 160GB de transferencia

**Tu configuración (1GB RAM):**
- ~$5-10 USD/mes si está corriendo 24/7
- ~$0-2 USD/mes con auto-scaling (se apaga sin tráfico)

---

## 📊 Monitoreo

### Dashboard web
\`\`\`bash
flyctl dashboard
\`\`\`

### Métricas de rendimiento
\`\`\`bash
flyctl status
flyctl logs
\`\`\`

---

## ✅ Checklist de Despliegue

- [ ] Fly CLI instalado y autenticado
- [ ] Backend Django desplegado en Render (obtener URL)
- [ ] Variable `NEXT_PUBLIC_API_URL` configurada en Fly.io
- [ ] `flyctl deploy` ejecutado exitosamente
- [ ] App accesible en `https://exaxistone2.fly.dev`
- [ ] Datos del backend cargando correctamente
- [ ] CORS configurado en el backend para permitir Fly.io

---

## 🆘 Soporte

Si encuentras problemas:

1. **Logs detallados:**
\`\`\`bash
flyctl logs --app exaxistone2
\`\`\`

2. **Estado de la app:**
\`\`\`bash
flyctl status --app exaxistone2
\`\`\`

3. **Documentación oficial:**
- https://fly.io/docs/languages-and-frameworks/nextjs/
- https://fly.io/docs/reference/configuration/

4. **Foro de Fly.io:**
- https://community.fly.io/
