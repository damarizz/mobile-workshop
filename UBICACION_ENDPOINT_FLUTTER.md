# 📍 Ubicación del Endpoint Local en Flutter

## 🔍 Archivo donde está el endpoint:

```
📂 proyectoflutter01/
  📂 lib/
    📂 services/
      📄 api_service.dart  ← 🔴 AQUÍ ESTÁ
```

---

## 📝 Código Actual (LÍNEA 8):

```dart
class ApiService {
  // ⚠️ Asegúrate de que Flask esté corriendo en este puerto
  static const String _baseUrl = 'http://localhost:5000';  // 🔴 AQUÍ
  
  /// Envía la imagen como bytes (Uint8List) — compatible con Flutter Web.
  /// No usa dart:io ni File.
  static Future<ResultadoModel> clasificar({
    required Uint8List bytes,
    required String nombreArchivo,
  }) async {
    final uri = Uri.parse('$_baseUrl/api/clasificar');
    
    // ... resto del código
  }
}
```

---

## 🎯 Lo que Necesitas Cambiar:

**De:**
```dart
static const String _baseUrl = 'http://localhost:5000';
```

**A:**
```dart
static const String _baseUrl = 'https://brain-tumor-backend.onrender.com';
```

---

## 📍 Ruta Completa del Archivo:

```
/home/damaris/dev/mobile-workshop/modelo-predictivo-dtc/proyectoflutter01/lib/services/api_service.dart
```

**Línea:** 8

---

## 📚 Cómo se usa este endpoint:

El archivo `api_service.dart` tiene un método `clasificar()` que:

1. ✅ Toma una imagen (como bytes)
2. ✅ La envía a `_baseUrl/api/clasificar` 
3. ✅ Espera respuesta JSON con predicción
4. ✅ Retorna un objeto `ResultadoModel`

**Se llama desde:**
- `clasificacion_controller.dart` (el controlador de lógica)
- Que es usado en las vistas para enviar la imagen al backend

---

## 🔄 Flujo Completo:

```
Vista (views/) 
  ↓
Controlador (controllers/clasificacion_controller.dart)
  ↓
Servicio (services/api_service.dart) ← 🔴 AQUÍ ESTÁ EL ENDPOINT
  ↓
Backend en Render (https://brain-tumor-backend.onrender.com/api/clasificar)
```

¿Necesitas que edite este archivo o necesitas más información?
