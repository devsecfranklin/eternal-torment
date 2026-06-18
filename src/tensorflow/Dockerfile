# syntax=docker/dockerfile:1.25
FROM nvcr.io/nvidia/l4t-tensorflow:r32.6.1-tf2.5-py3

LABEL maintainer="franklin <smoooth.y62wj@passmail.net>"
LABEL org.opencontainers.image.source="https://github.com/pale-shadow/eternal-torment"

ENV DEBIAN_FRONTEND=noninteractive \
    PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1

RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
    --mount=type=cache,target=/var/lib/apt,sharing=locked \
    apt-get update && apt-get install -y --no-install-recommends \
    python3-pip \
    python3-dev \
    build-essential \
    libhdf5-serial-dev \
    hdf5-tools \
    libhdf5-dev \
    zlib1g-dev \
    zip \
    libjpeg8-dev \
    liblapack-dev \
    libblas-dev \
    gfortran \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt .

RUN --mount=type=cache,target=/root/.cache/pip \
    python3 -m pip install --upgrade pip setuptools wheel && \
    python3 -m pip install -r requirements.txt

COPY . .

RUN useradd -m appuser && chown -R appuser /app
USER appuser

CMD ["python3", "main.py"]
