# Use Python 3.11 slim image
FROM python:3.11-slim

# Set working directory
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    postgresql-client \
    libpq-dev \
    gcc \
    python3-dev \
    bash \
    dos2unix \
    && rm -rf /var/lib/apt/lists/*

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Copy and install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the entire application code
COPY . .

# Fix shell script formatting and permissions
RUN dos2unix migrate.sh && chmod +x migrate.sh

# Expose the app port
EXPOSE 8000

# Run app with Gunicorn
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "run:app"]

