FROM python:3.10-slim

WORKDIR /app

# Copiar requirements y instalar dependencias
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copiar código
COPY backend.py .
COPY brain_tumor_cnn.tflite .
COPY static/ static/

# Crear directorio de uploads
RUN mkdir -p static/uploads

# Exponer puerto
EXPOSE 8000

# Comando para iniciar
CMD ["gunicorn", "--workers", "4", "--worker-class", "sync", "--timeout", "60", "--bind", "0.0.0.0:8000", "backend:app"]
