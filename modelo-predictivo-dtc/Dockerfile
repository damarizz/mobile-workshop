FROM python:3.13

WORKDIR /app

# Instalar dependencias del sistema necesarias para TensorFlow
RUN apt-get update && apt-get install -y --no-install-recommends \
    libsm6 \
    libxext6 \
    libxrender-dev \
    && rm -rf /var/lib/apt/lists/*

# Copiar requirements y instalar dependencias Python
COPY requirements.txt .
RUN pip install --no-cache-dir --upgrade pip setuptools && \
    pip install --no-cache-dir -r requirements.txt

# Copiar código
COPY backend.py .
COPY brain_tumor_cnn.tflite .
COPY static/ static/

# Crear directorio de uploads
RUN mkdir -p static/uploads

# Health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
    CMD python -c "import requests; requests.get('http://localhost:8000/')"

# Exponer puerto
EXPOSE 8000

# Comando para iniciar
CMD ["gunicorn", "--workers", "2", "--worker-class", "sync", "--timeout", "60", "--bind", "0.0.0.0:8000", "--access-logfile", "-", "--error-logfile", "-", "backend:app"]
