# Django Postgres FastAPI Tutorial

This content was generated using a Large Language Model called **wizardlm2**. If you try it out, let me know how it went!

## Prompt

I'm searching for an excellent tutorial that shows me how to build a FastAPI Django website with Postgresql. Any recommendations?

## wizardlm2 Response

Creating a FastAPI-Django hybrid application with PostgreSQL as the database involves integrating FastAPI as an API backend with Django, which can be used for handling web views and managing database migrations, among other things. Here's a step-by-step guide to help you set up such a system:

### Prerequisites

- Python 3.6+
- Docker (optional but recommended)
- PostgreSQL
- `pip` for package installation

### Step 1: Initialize Your Project

Start by creating a new Django project and a Django app if you haven't already:

```bash
django-admin startproject myproject
cd myproject
python manage.py startapp myapp
```

### Step 2: Set Up PostgreSQL

Configure your PostgreSQL database in `myproject/settings.py` and create a new database for your project. You can use environment variables to keep 
sensitive information like database credentials secure.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydatabase',
        'USER': 'myuser',
        'PASSWORD': 'mypassword',
        'HOST': 'localhost',  # Or the address of your PostgreSQL server
        'PORT': '5432',
    }
}
```

### Step 3: Create and Apply Migrations

Create migrations for your models in Django and apply them to set up the database schema.

```bash
python manage.py makemigrations myapp
python manage.py migrate
```

### Step 4: Install FastAPI and Uvicorn

Install FastAPI and Uvicorn, which will serve your API endpoints.

```bash
pip install fastapi uvicorn
```

### Step 5: Create FastAPI Application

Create a new file for your FastAPI application, e.g., `api_app.py`, and define your FastAPI endpoints there.

```python
from fastapi import FastAPI, HTTPException
app = FastAPI()

@app.get("/items/{item_id}")
def read_item(item_id: int, q: Optional[str] = None):
    if item_id == 10:
        raise HTTPException(status_code=418, detail="I'm a teapot")
    return {"item_id": item_id}
```

### Step 6: Integrate FastAPI with Django

You can integrate FastAPI within a Django app by using the `django-starlette` package or by creating a Django view that delegates requests to the 
FastAPI application. Here's an example using `django-starlette`:

```bash
pip install django-starlette
```

In your Django project, set up the application in `settings.py` and add it to `INSTALLED_APPS`.

Then, in your Django view, you can use `django-starlette` to include FastAPI:

```python
from starlette.applications import StarletteApp
from django.http import HttpResponseBadRequest
from django.urls import path
from django.utils.deprecation import MiddlewareWrapper

# Load your FastAPI app (api_app.py)
from myproject.myapp import api_app

class DjangoStarletteMiddleware(MiddlewareWrapper):
    def __init__(self, get_response):
        super().__init__(get_response)
        self.starlette_app = StarletteApp(api_app)  # or your FastAPI app

    def __call__(self, environment):
        # Add the starlette WSGI environment to the request
        environment['wsgi.url_scheme'] = 'auto'
        return super().__call__(environment)

# Include the middleware in your project's URL configuration
middleware = [DjangoStarletteMiddleware()]
```

Add the middleware to your Django project's `urls.py`:

```python
from django.core.asgi import hooked
from django.urls import path, include

# Include all Django URLs here (optional)
# from django.urls import path, include
# urlpatterns = [
#     path('admin/', admin.site.urls),
#     path('api/', include('myapp.urls')),  # if you're using Django's `include` for API endpoints
# ]

# Include FastAPI URLs here
hooked("django:startup", lambda: app.mount("/api", api_app))

urlpatterns = [
    path('admin/', admin.site.urls),
    # Your other Django views go here
]
```

### Step 7: Run the Application

You can now run your FastAPI endpoints by visiting `http://localhost:8000/api/items/{item_id}`.

To run the entire Django project (including both Django and FastAPI), you can use the following command:

```bash
gunicorn myproject.wsgi:application --bind 0.0.0.0:8000
```

Or, if you're using Docker, you can define services for both Django and PostgreSQL in your `docker-compose.yml` file and run them together.

### Step 8: Test Your Application

Write tests for both your Django views and FastAPI endpoints to ensure everything is working as expected.

### Tutorials and Resources

- The [official FastAPI documentation](https://fastapi.tiangolo.com/advanced-use-cases/) has sections on integrating with Django.
- The `django-starlette` GitHub repository has examples of integration: [GitHub - 
django-starlette](https://github.com/encode/django-rest-framework#integration-with-fastapi).
- The Django REST framework (DRF) also provides a way to integrate FastAPI, although it's more complex than using `django-starlette`. You can find 
information on this in the [DRF documentation](https://www.django-rest-framework.org/).

### Additional Tips

- Use Docker for easier deployment and environment consistency.
- Consider using `django-extensions` for managing large projects (e.g., `shell_plus` for a better interactive shell with access to both Django and 
FastAPI contexts).
- Ensure that you manage your database migrations carefully, keeping in mind that Django and FastAPI might use the database concurrently.

By following these steps and utilizing the resources provided, you should be able to build a robust FastAPI-Django application with PostgreSQL as its 
backend. Remember to keep your dependencies up to date and test thoroughly before deploying your application to production.
