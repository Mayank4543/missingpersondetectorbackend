FROM python:3.11-slim

WORKDIR /app

# Prevent python buffering
ENV PYTHONUNBUFFERED=1

# Install system dependencies for OpenCV
RUN apt-get update && apt-get install -y \
    libglib2.0-0 \
    libsm6 \
    libxext6 \
    libxrender-dev \
    libgomp1 \
    libgstreamer1.0-0 \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements
COPY requirements.txt .

# Install python dependencies
RUN pip install --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

# Copy project files
COPY . .

# Create upload folders
RUN mkdir -p uploads/persons uploads/videos uploads/frames

# Cloud Run uses this port
ENV PORT=8080
EXPOSE 8080

# Start FastAPI
CMD ["sh", "-c", "uvicorn main:app --host 0.0.0.0 --port $PORT"]