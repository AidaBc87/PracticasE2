**Introducción completa** que cubre la configuración del entorno hasta la estructura de carpetas estándar de Django, todo usando **Visual Studio Code (VS Code)** como herramienta principal.

## 💻 Ejercicio: Configuración Completa del Proyecto y Estructura de Carpetas

Crearemos un proyecto llamado "Portfolio Digital" con una aplicación para mostrar "Proyectos".

-----

### Paso 1: Configuración Inicial en Visual Studio Code

1.  **Abrir una Carpeta:** En VS Code, ve a `Archivo` \> `Abrir Carpeta` y selecciona o crea una carpeta vacía (por ejemplo, `DjangoPortfolio`).

2.  **Abrir el Terminal Integrado:** Ve a `Terminal` \> `Nuevo Terminal`. Todos los comandos se ejecutarán aquí.

### Paso 2: Creación e Instalación del Entorno Virtual y Django

**Objetivo:** Aislar las dependencias del proyecto.

1.  **Creación del Entorno Virtual:**

    ```bash
    python -m venv .venv
    ```

    *(Esto crea una carpeta oculta `.venv` dentro de tu proyecto).*

2.  **Activación del Entorno Virtual:** (Verás `(.venv)` al inicio de la línea de comandos si fue exitoso).

      * **Windows (PowerShell):**
        ```bash
        .venv\Scripts\Activate
        ```
      * **macOS/Linux:**
        ```bash
        source .venv/bin/activate
        ```

3.  **Instalación del Framework Django:**

    ```bash
    pip install django
    ```

-----

### Paso 3: Creación del Proyecto y Ejecución

**Comandos Esenciales:** `startproject`, `startapp`, `runserver`.

1.  **Creación del Proyecto (Configuración Global):**

    ```bash
    django-admin startproject portfolio_project .
    ```

    > **Nota:** El punto (`.`) es crucial para crear el proyecto en la carpeta actual, evitando una anidación doble.

2.  **Creación de la Aplicación (Módulo Funcional):**

    ```bash
    python manage.py startapp projects
    ```

3.  **Ejecución del Servidor:**

    ```bash
    python manage.py runserver
    ```

    > **Verificación:** Abre `http://127.0.0.1:8000/` en tu navegador. Deberías ver la página de felicitación de Django.

-----

### Paso 4: Configuración del Proyecto (`settings.py` y `urls.py`)

1.  **Configurar la Aplicación (`settings.py`):**
    Abre `portfolio_project/settings.py` y registra la nueva aplicación.

    ```python
    # portfolio_project/settings.py
    INSTALLED_APPS = [
        # ...
        'projects.apps.ProjectsConfig', # Registra la aplicación
    ]
    ```

2.  **Configurar URLs Globales (`urls.py`):**
    Abre `portfolio_project/urls.py` e incluye las URLs de la aplicación `projects`.

    ```python
    # portfolio_project/urls.py
    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('', include('projects.urls')), # Incluir las URLs de la aplicación projects
    ]
    ```

-----

### Paso 5: Creación de la Aplicación y Lógica Principal

**Objetivo:** Crear una página de bienvenida simple.

1.  **Crear `projects/urls.py`:** Crea este archivo dentro de la carpeta `projects`.

    ```python
    # projects/urls.py
    from django.urls import path
    from . import views

    urlpatterns = [
        path('', views.home_view, name='home'),
    ]
    ```

2.  **Crear la Vista (`projects/views.py`):**

    ```python
    # projects/views.py
    from django.shortcuts import render

    def home_view(request):
        context = {'greeting': '¡Bienvenido a mi Portfolio Digital!'}
        return render(request, 'projects/home.html', context)
    ```

3.  **Crear Plantillas:** Crea la estructura `projects/templates/projects/` y el archivo `home.html` dentro de ella.

    ```html
    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <title>Inicio</title>
    </head>
    <body>
        <h1>{{ greeting }}</h1>
        <p>Esta es la página principal de la aplicación Proyectos.</p>
    </body>
    </html>
    ```

-----

### Paso 6: Configuración de Carpetas Estándar (Templates, Static, Media)

**Objetivo:** Preparar el proyecto para archivos HTML, CSS/JS/Imágenes estáticas y archivos subidos por usuarios.

1.  **Crear Carpetas Estándar en la Raíz:** En la carpeta raíz del proyecto (`portfolio_project`), crea:

      * `templates`
      * `static`
      * `media`

2.  **Configurar Directorios de Plantillas (`settings.py`):**
    Abre `portfolio_project/settings.py` y añade la carpeta `templates` global.

    ```python
    # portfolio_project/settings.py

    import os # Asegúrate de que esto está importado o usa pathlib

    # ... (al inicio, si usas pathlib)
    from pathlib import Path
    BASE_DIR = Path(__file__).resolve().parent.parent
    # ...

    TEMPLATES = [
        {
            # ...
            # Agregamos la carpeta global 'templates' en la raíz
            'DIRS': [BASE_DIR / 'templates'],
            # ...
        },
    ]
    ```

3.  **Configurar Archivos Estáticos y Media (`settings.py`):**
    Abre `portfolio_project/settings.py` y añade estas líneas al final del archivo para definir dónde buscar archivos estáticos (CSS, JS, imágenes del desarrollador) y archivos media (imágenes del usuario).

    ```python
    # portfolio_project/settings.py (al final del archivo)

    # Carpetas estáticas globales (CSS, JS, imágenes del proyecto)
    STATIC_URL = 'static/'
    STATICFILES_DIRS = [
        BASE_DIR / 'static',
    ]

    # Archivos subidos por los usuarios (fotos de perfil, documentos)
    MEDIA_URL = 'media/'
    MEDIA_ROOT = BASE_DIR / 'media'
    ```

-----

### Paso 7: Modelos, Admin y Migraciones

**Objetivo:** Introducir los archivos clave para la base de datos y la administración.

1.  **Definir un Modelo (`projects/models.py`):** Un modelo es una clase que representa una tabla en la base de datos.

    ```python
    # projects/models.py
    from django.db import models

    class Project(models.Model):
        title = models.CharField(max_length=100)
        description = models.TextField()
        technology = models.CharField(max_length=50)
        created_at = models.DateTimeField(auto_now_add=True)

        def __str__(self):
            return self.title
    ```

2.  **Crear la Interfaz de Administración (`projects/admin.py`):** Esto hace que el modelo sea accesible en el panel de administración de Django.

    ```python
    # projects/admin.py
    from django.contrib import admin
    from .models import Project

    admin.site.register(Project)
    ```

3.  **Comandos de Base de Datos:**

      * **Crear migraciones (tablas):** Le dice a Django cómo cambiar la base de datos para que coincida con el modelo.

        ```bash
        python manage.py makemigrations
        ```

      * **Aplicar migraciones:** Ejecuta los cambios en la base de datos.

        ```bash
        python manage.py migrate
        ```

      * **Crear Superusuario (para acceder al Admin):**

        ```bash
        python manage.py createsuperuser
        # Sigue las instrucciones en el terminal (username, email, password)
        ```

    > **Verificación:** Ejecuta `python manage.py runserver` y ve a `http://127.0.0.1:8000/admin/`. Inicia sesión y deberías ver la sección **Projects** donde puedes agregar nuevos proyectos.

-----

### Resumen de Comandos Esenciales

| Comando | Función |
| :--- | :--- |
| `python -m venv .venv` | Crea el entorno virtual. |
| `source .venv/bin/activate` | Activa el entorno virtual. |
| `pip install django` | Instala Django. |
| `django-admin startproject` | Crea la estructura base del proyecto. |
| `python manage.py startapp` | Crea una aplicación. |
| `python manage.py runserver` | Ejecuta el servidor de desarrollo. |
| `python manage.py makemigrations` | Prepara los cambios del modelo. |
| `python manage.py migrate` | Aplica los cambios a la base de datos. |
| `python manage.py createsuperuser` | Crea un usuario administrador. |

-----

Integrar un archivo **CSS** en la carpeta **`static`** es un paso crucial para darle estilo a tu sitio de Django. Aquí te muestro cómo hacerlo con tu proyecto "Portfolio Digital" para darle un estilo básico a `home.html`.

## 🎨 Integración de Archivos Estáticos (CSS)

### Paso 1: Crear el Archivo CSS

1.  Asegúrate de que la carpeta **`static`** existe en la raíz de tu proyecto.

2.  Dentro de la carpeta **`static`**, crea una subcarpeta con el mismo nombre que tu aplicación para organizar tus archivos (es una buena práctica): **`static/projects/`**.

3.  Dentro de `static/projects/`, crea el archivo **`style.css`**.

    ```
    portfolio_project/
    ├── static/
    │   └── projects/
    │       └── style.css  <-- Archivo a crear
    └── ...
    ```

4.  Abre **`static/projects/style.css`** y añade un estilo simple:

    ```css
    /* static/projects/style.css */
    body {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        background-color: #f4f4f9;
        color: #333;
        margin: 40px;
    }

    h1 {
        color: #007bff; /* Azul */
        border-bottom: 2px solid #ccc;
        padding-bottom: 10px;
    }

    p {
        line-height: 1.6;
    }
    ```

-----

### Paso 2: Cargar y Usar el Archivo Estático en la Plantilla

Para que Django pueda encontrar y servir el archivo CSS, debes hacer dos cosas en tu plantilla `home.html`:

1.  **Cargar la etiqueta `static`:** Usar la etiqueta `{% load static %}` al comienzo del archivo HTML.
2.  **Referenciar el CSS:** Usar la etiqueta `{% static 'path/to/file.css' %}` dentro del enlace `<link>`.

Abre **`projects/templates/projects/home.html`** y modifícalo:

```html
{% load static %} <!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Inicio</title>
    <link rel="stylesheet" href="{% static 'projects/style.css' %}">
</head>
<body>
    <h1>{{ greeting }}</h1>
    <p>Esta es la página principal de la aplicación Proyectos. ¡Ahora con estilo!</p>
</body>
</html>
```

-----

### Paso 3: Probar el Resultado

1.  Asegúrate de que tu servidor de desarrollo esté ejecutándose:
    ```bash
    python manage.py runserver
    ```
2.  Ve a `http://127.0.0.1:8000/` en tu navegador.

Deberías ver la página con el fondo gris claro, el texto en gris oscuro y el título **azul**, confirmando que Django encontró y sirvió tu archivo **`style.css`** desde la carpeta **`static`**.

-----

Este proceso es el estándar de Django: la etiqueta `{% load static %}` le dice a Django que busque archivos estáticos en todas las carpetas que definiste en `settings.py`, y la etiqueta `{% static '...' %}` genera la URL correcta para ese archivo.
