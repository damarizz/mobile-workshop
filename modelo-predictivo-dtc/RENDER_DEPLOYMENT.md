# 🚀 Deploy en Render - Guía de Solución

## ✅ Problemas Resueltos

### 1. **Error de Compatibilidad de Dependencias**
- **Problema**: `contourpy==1.3.3` requiere Python 3.11+
- **Solución**: 
  - Actualizado `requirements.txt` con versiones compatibles con Python 3.10+
  - Cambiado Dockerfile a Python 3.11 para mejor soporte
  - Removidas versiones conflictivas

### 2. **Dependencias Faltantes para TensorFlow**
- **Agregado**: Librerías del sistema requeridas en Dockerfile (`libsm6`, `libxext6`, `libxrender-dev`)
- **Agregado**: Health check en el Dockerfile

### 3. **Optimizaciones de Producción**
- Workers reducidos de 4 a 2 (plan free de Render tiene límites)
- Logs habilitados para debugging en Render
- PYTHONUNBUFFERED=1 para ver logs en tiempo real

## 📋 Próximos Pasos

### 1. Push a GitHub
```bash
git add -A
git commit -m "fix: actualizar requirements.txt y Dockerfile para Render"
git push origin main
```

### 2. En Render.com:
1. Ve a https://dashboard.render.com
2. Click en "New+" → "Web Service"
3. Conecta tu repositorio `mobile-workshop`
4. Configura:
   - **Name**: `brain-tumor-backend`
   - **Runtime**: `Docker` (para más control)
   - **Build Command**: (dejar en blanco, usa Dockerfile)
   - **Start Command**: (dejar en blanco, usa Dockerfile)
   - **Root Directory**: `modelo-predictivo-dtc`
   - **Plan**: Free

### 3. Verifica el Deploy
Una vez deployado:
```bash
curl https://tu-backend.onrender.com/
# Deberías ver: {"status": "ok", "message": "Brain Tumor API is running"}
```

## 🔧 Archivos Modificados

- ✅ `requirements.txt` - Versiones compatibles
- ✅ `Dockerfile` - Python 3.11, optimizaciones
- ✅ `render.yaml` - Configuración actualizada
- ✅ `.dockerignore` - Archivos a ignorar en build
- ✅ `backend.py` - Endpoint de salud agregado

## 📱 Configurar Flutter para el Backend

En tu app Flutter, actualiza la URL:

```dart
// En tu servicio o configuración
const String API_URL = 'https://brain-tumor-backend.onrender.com';

// Ejemplo de llamada:
final response = await http.post(
  Uri.parse('$API_URL/api/clasificar'),
  headers: {'Content-Type': 'multipart/form-data'},
  body: formData,
);
```

## ⚠️ Notas Importantes

- El plan **Free de Render** puede hibernar después de 15 minutos sin uso
- Los uploads se perderán cuando se redeploy (usa base de datos o storage en producción)
- Para producción, considera upgrade a plan pagado

¿Necesitas ayuda con algo más?
