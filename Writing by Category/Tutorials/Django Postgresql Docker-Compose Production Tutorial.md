# Django Postgresql Docker-Compose Production Tutorial

## Query

Familiarize yourself with the documentation at https://docs.djangoproject.com/en/5.0/ and then provide a tutorial for building a Django Postgresql website using docker-compose to host the application on a production Debian server. Format your output as a Markdown document.

## llama3 Response

### Django, PostgreSQL, Docker-Compose, and Debian: A Tutorial for Building a Production-ready Website

=====================================================

### Step 1: Install Required Packages (Local Development Environment)

Before we start building our application, let's ensure we have the necessary packages installed:

```bash
sudo apt-get update
sudo apt-get install -y python3 python3-pip python3-dev build-essential libpq5 libpq-dev
```

### Step 2: Create a New Django Project

Create a new Django project using the following command:

```bash
django-admin startproject mysite
cd mysite/

```

### Step 3: Configure Django Settings and Database

In `mysite/settings.py`, set your database settings to use PostgreSQL:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydatabase',
        'USER': 'mypostgresuser',
        'PASSWORD': 'mypassword',
        'HOST': 'localhost',
        'PORT': '',  # Set to empty string for default
    }
}
```

### Step 4: Create Models and Run Migrations

Create a new Django app:

```bash
python manage.py startapp mysite/mysite

```

Define your models in `mysite/mysite/models.py`:

```python
from django.db import models

class MyModel(models.Model):
    name = models.CharField(max_length=255)
    description = models.TextField()
```

Run the following command to create the database tables for our models:

```bash
python manage.py makemigrations mysite
python manage.py migrate
```

### Step 5: Create a Docker-Compose File

Create a new file named `docker-compose.yml` with the following content:

```yaml
version: '3'
services:
  db:
    image: postgres
    environment:
      - POSTGRES_USER=mypostgresuser
      - POSTGRES_PASSWORD=mypassword
      - POSTGRES_DB=mydatabase

  app:
    build: .
    command: python manage.py runserver
    ports:
      - "8000"
    depends_on:
      - db
```

### Step 6: Build and Run the Docker-Compose Environment

Run the following commands to build and start our Docker containers:

```bash
docker-compose up -d
```

### Step 7: Configure the Production Server (Debian)

On your production Debian server, install Docker and create a new directory for your application:

```bash
sudo apt-get install docker.io
mkdir /var/www/mysite
```

Move your `docker-compose.yml` file to this directory and run the following command to start the containers:

```bash
cd /var/www/mysite
docker-compose up -d
```

### Step 8: Configure Systemd Service

Create a new systemd service file at `/etc/systemd/system/mysite.service` with the following content:

```ini
[Unit]
Description=mymysite
After=network.target

[Service]
User=myuser
Exec=/usr/bin/docker-compose up -d
Restart=always

[Install]
WantedBy=multi-user
```

Reload systemd and start the service:

```bash
sudo systemctl daemon-reload
sudo systemctl enable mysite
sudo systemctl start mysite
```

That's it! You now have a production-ready Django application using PostgreSQL, Docker-Compose, and Debian.
