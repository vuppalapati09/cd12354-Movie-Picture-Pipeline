FROM python:3.10-slim-bookworm

ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /

RUN useradd -u 1000 -m app

RUN apt-get update && \
    apt-get install -y \
    build-essential \
    libpcre3 \
    libpcre3-dev \
    libffi-dev \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir \
    flask \
    uwsgi \
    flask-cors \
    pytest

RUN mkdir -p /var/www/app && \
    mkdir -p /app

COPY . /app

CMD ["uwsgi", "--http", ":5000", "--master", "--enable-threads", "-s", "/var/www/app/app.sock", "--manage-script-name", "--mount", "/=app:app"]