# Guía Rápida: Desplegar Frontend en Vercel

## Método 1: Desde v0 (Más Fácil)

1. Click en **"Publish"** en v0.app
2. v0 automáticamente despliega a Vercel
3. Obtén tu URL: `https://tu-app.vercel.app`

**Configurar Variables:**
- Ve a tu proyecto en Vercel
- Settings → Environment Variables
- Agrega: `NEXT_PUBLIC_API_URL=https://tu-backend.onrender.com`
- Redeploy

---

## Método 2: Desde Vercel Dashboard

### Paso 1: Preparar Código

\`\`\`bash
# Asegúrate de que está en GitHub
git add .
git commit -m "Ready for Vercel"
git push origin main
\`\`\`

### Paso 2: Importar en Vercel

1. Ve a [vercel.com](https://vercel.com)
2. Click **"Add New..."** → **"Project"**
3. Selecciona tu repositorio
4. Configura:
   - Framework: **Next.js**
   - **Root Directory: `frontend`** ← ⚠️ **MUY IMPORTANTE**
   - Build Command: `npm run build`
   - Output Directory: `.next`

### Paso 3: Variables de Entorno ⚠️ REQUERIDO

**Debes agregar esta variable ANTES del primer deploy:**

1. En la pantalla de configuración, scroll hasta **Environment Variables**
2. Agrega:
   \`\`\`
   Name: NEXT_PUBLIC_API_URL
   Value: https://tu-backend.onrender.com
   \`\`\`
3. Aplica a: **Production, Preview, Development** (todas)

**Si ya desplegaste sin la variable:**

1. Ve a tu proyecto en Vercel
2. Settings → Environment Variables
3. Click **"Add New"**
4. Nombre: `NEXT_PUBLIC_API_URL`
5. Valor: `https://tu-backend.onrender.com` (URL de tu backend en Render)
6. Guarda y luego **Redeploy** desde Deployments → tres puntos → Redeploy

### Paso 4: Deploy

Click **"Deploy"** y espera 2-3 minutos.

---

## Solución: "Variable NEXT_PUBLIC_API_URL references Secret that does not exist"

Este error ocurre cuando Vercel no encuentra la variable de entorno. **Solución:**

1. Ve a tu proyecto en Vercel Dashboard
2. Click en **Settings** (arriba)
3. Click en **Environment Variables** (menú lateral)
4. Click **"Add New"**
5. Completa:
   - **Key:** `NEXT_PUBLIC_API_URL`
   - **Value:** `https://tu-backend.onrender.com`
   - **Environments:** Marca Production, Preview y Development
6. Click **"Save"**
7. Ve a **Deployments** tab
8. En el último deployment, click en los tres puntos (...)
9. Click **"Redeploy"**
10. Espera 2-3 minutos

**IMPORTANTE:** Reemplaza `https://tu-backend.onrender.com` con la URL real que Render te dio para tu backend Django.

---

## Verificación

### Test 1: App Carga
\`\`\`
https://tu-app.vercel.app
\`\`\`

### Test 2: Sin Errores CORS
- F12 → Console
- No debe haber errores rojos

### Test 3: Datos del Backend
- Debería mostrar módulos de Data Science
- Con gráficos interactivos

---

## Solución Rápida de Problemas

**Error: "No Next.js version detected"**
\`\`\`bash
# Verifica Root Directory en Vercel
# Settings → General → Root Directory: frontend
# Redeploy después de cambiar
\`\`\`

**No muestra datos:**
\`\`\`bash
# Verifica variable de entorno
# En Vercel Settings → Environment Variables
# Debe existir: NEXT_PUBLIC_API_URL
# Luego redeploy
\`\`\`

**Error CORS:**
\`\`\`bash
# En Render, actualiza CORS_ALLOWED_ORIGINS
# Incluye tu URL de Vercel exacta
# Espera 2-3 min a que redesplegue
\`\`\`

---

## Comandos Útiles

**Ver logs:**
\`\`\`bash
npm i -g vercel
vercel logs
\`\`\`

**Despliegue local preview:**
\`\`\`bash
vercel dev
\`\`\`

---

Tu frontend estará en: `https://tu-app.vercel.app`
