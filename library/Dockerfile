# `python-base` sets up all our shared environment variables
FROM python:3.8.1-slim as python-base

# python
ENV PYTHONUNBUFFERED=1 \
    # prevents python creating .pyc files
    PYTHONDONTWRITEBYTECODE=1 \
    \
    # pip
    PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=on \
    PIP_DEFAULT_TIMEOUT=100

# Install dependencies
RUN apt-get update \
    && apt-get install --no-install-recommends -y \
        # dependencies for building Python packages
        build-essential \
        # dependencies for PostgreSQL
        libpq-dev gcc \
    && pip install --upgrade pip \
    && pip install django psycopg2-binary djangorestframework \
    && pip install psycopg2 \
    && apt-get -y install libpq-dev gcc \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Set the working directory
WORKDIR /app

# Copy the project files to the working directory
COPY . /app/

# Expose the port Django will run on
EXPOSE 8000

# Run the Django development server
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]