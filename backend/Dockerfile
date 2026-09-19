# Gunakan base image Python 3.11 yang ringan
FROM python:3.11-slim

# Set working directory di dalam container
WORKDIR /app

# Install dependencies sistem yang diperlukan untuk build package Python
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Copy file requirements.txt terlebih dahulu (agar memanfaatkannya sebagai layer cache Docker)
COPY requirements.txt .

# Upgrade pip dan install semua package Python
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

# Copy seluruh source code backend ke dalam container
COPY . .

# Pastikan struktur folder uploads ada di dalam container
RUN mkdir -p /app/uploads/covers /app/uploads/ebooks

# Expose port yang digunakan FastAPI
EXPOSE 8001

# Jalankan Uvicorn server
CMD ["uvicorn", "server:app", "--host", "0.0.0.0", "--port", "8001", "--workers", "1"]