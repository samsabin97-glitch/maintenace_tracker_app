# Initialize first
FROM python:3.12-slim-bookworm AS builder
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/ 

#setting up the environment
ENV PYTHONDONTWERITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# build container
ENV UV_LINK_MODE=copy

WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc python3-dev default-libmysqlclient-dev \
    build-essential pkg-config libpango-1.0-0 libpangoft2-1.0-0 \
    curl \
    git \
    libpq-dev \
    libssl-dev \
    libffi-dev \
    libxml2-dev \
    libxslt1-dev \
    zlib1g-dev \
    wget \
    vim \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

COPY . . 
# build venv
RUN uv venv && uv sync && uv lock

COPY --from=builder /app /app
ENV PATH="/app/.venv/bin:$PATH"

ENTRYPOINT []
# final container
# FROM python:3.12-slim-bookworm 
# COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/