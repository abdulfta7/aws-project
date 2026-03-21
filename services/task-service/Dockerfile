FROM python:3.12-slim-bookworm

WORKDIR /app

# Create non-root user
RUN groupadd -r appuser && useradd -r -g appuser appuser

# Copy requirements first
COPY requirements.txt .

# Install only what's necessary (بدون upgrade)
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        gcc \
        default-libmysqlclient-dev \
        pkg-config && \
    pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt && \
    apt-get purge -y --auto-remove gcc pkg-config && \
    rm -rf /var/lib/apt/lists/* /root/.cache /tmp/*

# Copy application files
COPY app.py .

# Switch to non-root user
USER appuser

EXPOSE 8002
ENV PYTHONUNBUFFERED=1
CMD ["python", "-u", "app.py"]