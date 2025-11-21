# Guía Rápida: Desplegar Backend en Render

## Prerequisitos

- [ ] Código en GitHub
- [ ] Cuenta en Render
- [ ] `backend/requirements.txt` existe
- [ ] `backend/render.yaml` configurado

---

## Paso a Paso

### 1. Crear Web Service

1. Ve a [render.com](https://render.com)
2. **New +** → **Web Service**
3. Conecta tu repositorio de GitHub

### 2. Configuración Básica

| Campo | Valor |
|-------|-------|
| Name | `datadocs-api` |
| Region | Oregon (US West) |
| Branch | `main` |
| **Root Directory** | `backend` ⚠️ |
| Runtime | Python 3 |
| **Public Directory** | **(VACÍO)** ← No pongas nada |

> ⚠️ **Importante sobre Public Directory:**
> - Django maneja sus propios archivos estáticos internamente
> - Déjalo **completamente vacío** o Render puede tener problemas
> - `collectstatic` ya crea los archivos estáticos automáticamente

### 3. Build Settings

**Build Command:**
\`\`\`bash
pip install -r requirements.txt && python manage.py migrate && python manage.py collectstatic --noinput
\`\`\`

**Start Command:**
\`\`\`bash
gunicorn config.wsgi:application --bind 0.0.0.0:$PORT --workers 2
\`\`\`

### 4. Variables de Entorno

| Key | Value |
|-----|-------|
| `SECRET_KEY` | [Genera aquí](#generar-secret-key) |
| `DEBUG` | `False` |
| `ALLOWED_HOSTS` | `.onrender.com` |
| `CORS_ALLOWED_ORIGINS` | `https://tu-app.vercel.app` |

#### Generar SECRET_KEY

**Python:**
\`\`\`bash
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
\`\`\`

**Online:**
[djecrety.ir](https://djecrety.ir/)

### 5. Deploy

Click **"Create Web Service"**

Espera 5-10 minutos. Verás:
\`\`\`
Starting Gunicorn...
Listening at: http://0.0.0.0:10000
\`\`\`

Tu API estará en: `https://tu-api.onrender.com`

---

## Verificación

**Test API:**
\`\`\`bash
curl https://tu-api.onrender.com/api/modules/
\`\`\`

**Respuesta esperada:**
\`\`\`json
[{"id": 1, "title": "División de Datasets", ...}]
\`\`\`

---

## Solución de Problemas

**Build falla:**
- Verifica `requirements.txt` tiene todas las dependencias
- Revisa logs en Render Dashboard

**App no inicia:**
- Verifica `SECRET_KEY` está configurada
- Confirma `ALLOWED_HOSTS` incluye `.onrender.com`

**Error 500:**
- Ve a Logs en Dashboard
- Busca el traceback de Python

---

## Actualizar Deploy

\`\`\`bash
git add .
git commit -m "Update backend"
git push origin main
# Render auto-despliega
\`\`\`

---

Tu backend estará en: `https://tu-api.onrender.com`
