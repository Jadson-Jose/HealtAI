# Estágio de construção
FROM python:3.12-slim as builder

WORKDIR /app
COPY requirements/base.txt .
RUN pip install --user -r base.txt

# Estágio final
FROM python:3.12-slim

WORKDIR /app
ENV PYTHONPATH=/app
ENV PATH="/root/.local/bin:${PATH}"
ENV PYTHONUNBUFFERED=1
ENV PYTHONDONTWRITEBYTECODE=1

# Instala dependências de sistema necessárias
RUN apt-get update && apt-get install -y --no-install-recommends \
    libpq-dev \
    gcc \
    && rm -rf /var/lib/apt/lists/*

COPY --from=builder /root/.local /root/.local
COPY ./app /app/app

# Garante que o uvicorn use o worker padrão para Python 3.12
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000", "--workers", "4", "--loop", "uvloop", "--http", "httptools"]