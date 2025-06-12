FROM python:3.9-slim

WORKDIR /app

# Install system dependencies needed for development tools
RUN apt-get update && apt-get install -y \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements first to leverage Docker cache
COPY requirements.txt .
RUN pip install  --no-cache-dir -r requirements.txt

# Copy the rest of the application
COPY . .

ENV PYTHONUNBUFFERED=1
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONPATH=/app
ENV REDIS_HOST=redis
ENV MONGODB_URL=mongodb://mongodb:27017
ENV NSQ_HOST=nsqd
ENV NSQ_PORT=4150
ENV NSQ_TOPIC=gold_price
ENV NSQ_LOOKUPD_HTTP_ADDRESS=nsqlookupd:4161

RUN pip install --no-cache-dir watchfiles

CMD ["python", "main.py"]
