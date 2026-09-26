FROM python:3.8.12-bullseye

RUN apt-get update && \
    apt-get -y install nano && \
    pip install --upgrade pip && \
    pip install poetry==1.5.0

# postgresql client for execute psql command
RUN echo 'Acquire::Check-Valid-Until "false";' > /etc/apt/apt.conf.d/99no-check-valid && \
    echo "deb http://snapshot.debian.org/archive/debian/20260825T000000Z bullseye main" > /etc/apt/sources.list && \
    echo "deb http://snapshot.debian.org/archive/debian-security/20260825T000000Z bullseye-security main" >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get -y install postgresql-client

# backend for caching
RUN apt-get update && \
    apt-get -y install memcached libmemcached-tools systemd net-tools

# backend for tinymce spellcheck plugin
RUN apt-get -y install libenchant-2-dev aspell-ru aspell-en

COPY ./src/pyproject.toml ./src/poetry.lock /tmp/
WORKDIR /tmp
RUN poetry config virtualenvs.create false && \
    poetry install --no-dev --no-root --no-interaction

WORKDIR /app/src
