Crear un proyecto desde cero que se enfoque en la **cadena solicitud-respuesta**, la creación de **múltiples vistas**, y el uso de **plantillas estáticas y dinámicas**.
Aquí tienes una práctica paso a paso para crear un **Sitio Web de Perfiles Simple**.
-----
## Activar Scripts en Windows
Ejecutar como administrador el PowerShell
Escribir el comando: Set-ExecutionPolicy RemoteSigned y presiona Enter
Luego Escribir: S y presiona Enter
Escribe: exit y presiona Enter
-----
## 💻 Práctica: Múltiples Vistas y Plantillas en Django

El objetivo es tener un sitio con una **Página de Inicio** y una **Página "Acerca de"**, usando plantillas y vistas separadas.

### 1\. Preparación y Creación Inicial

Si ya tienes tu entorno virtual de la práctica anterior, ¡úsalo\! Si no, sigue estos pasos:

1.  **Crea una Carpeta** llamada `perfiles_django` y ábrela en VS Code.

2.  **Activa tu entorno virtual** (`venv`).

3.  **Instala Django** (si es necesario): `pip install django`

4.  **Crea el Proyecto Principal** (`mi_sitio`):

    ```bash
    django-admin startproject mi_sitio .
    ```

5.  **Crea la Aplicación** (`principal`):

    ```bash
    python manage.py startapp principal
    ```

6.  **Registra la Aplicación:** Abre **`mi_sitio/settings.py`** y añade `'principal'` a la lista `INSTALLED_APPS`.

    ```python
    # mi_sitio/settings.py
    INSTALLED_APPS = [
        # ...
        'principal',  # <-- Añade esto
    ]
    ```

-----

### 2\. Definición de las Vistas (`principal/views.py`)

Las vistas son funciones de Python que reciben una solicitud (`request`) y devuelven una respuesta (generalmente renderizando una plantilla). Vamos a crear dos.

1.  **Abre `principal/views.py`** y define las funciones:

    ```python
    # principal/views.py

    from django.shortcuts import render
    from django.http import HttpResponse

    # Vista 1: Página de Inicio
    def inicio(request):
        # Datos dinámicos (Contexto) que se enviarán a la plantilla
        contexto = {
            'nombre_sitio': 'Mi Sitio de Perfiles',
            'es_alumno': True,
        }
        # Renderiza la plantilla principal/inicio.html
        return render(request, 'principal/inicio.html', contexto)

    # Vista 2: Página "Acerca de"
    def acerca_de(request):
        # Datos simples
        contexto = {
            'version': '1.0',
        }
        # Renderiza la plantilla principal/acerca_de.html
        return render(request, 'principal/acerca_de.html', contexto)
    ```

-----

### 3\. Configuración de las URLs (Rutas)

Necesitamos dos archivos `urls.py`: uno en la aplicación y uno en el proyecto.

1.  **Crea el Archivo de Rutas de la App (`principal/urls.py`):**
    *Crea un nuevo archivo* llamado **`urls.py`** dentro de la carpeta `principal/`.

    ```python
    # principal/urls.py

    from django.urls import path
    from . import views

    app_name = 'principal' # Opcional, pero buena práctica para referenciar rutas
    urlpatterns = [
        # La ruta vacía '' se mapea a la función views.inicio
        path('', views.inicio, name='inicio'), 
        # La ruta 'acerca/' se mapea a la función views.acerca_de
        path('acerca/', views.acerca_de, name='acerca'), 
    ]
    ```

2.  **Incluye las Rutas de la App en el Proyecto (`mi_sitio/urls.py`):**
    Abre el archivo principal **`mi_sitio/urls.py`** y dirige todo el tráfico raíz a tu aplicación.

    ```python
    # mi_sitio/urls.py

    from django.contrib import admin
    from django.urls import include, path # Asegúrate de importar 'include'

    urlpatterns = [
        path('', include('principal.urls')), # <-- Todo lo que venga de la raíz va a la app principal
        path('admin/', admin.site.urls),
    ]
    ```

-----

### 4\. Creación de las Plantillas (Templates)

Las plantillas son los archivos HTML que Django renderiza.

1.  **Crea la Estructura de Plantillas:**
    Dentro de la carpeta `principal/`, crea una subcarpeta llamada **`templates`**.
    Dentro de **`templates`**, crea otra subcarpeta llamada **`principal`**.

    La estructura debe ser: `principal/templates/principal/`

2.  **Crea la Plantilla Base (`principal/templates/base.html`):**
    Esta plantilla define el *esqueleto* de todo el sitio, incluyendo la navegación. Esto introduce el concepto de **Herencia de Plantillas** (`{% block %}`).
    *Crea este archivo en la carpeta* `principal/templates/` (no dentro de `principal/templates/principal/`).

    ```html
    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <title>{% block title %}Mi Sitio Django{% endblock %}</title>
    </head>
    <body>
        <nav>
            <a href="{% url 'principal:inicio' %}">Inicio</a> | 
            <a href="{% url 'principal:acerca' %}">Acerca de</a>
        </nav>
        <hr>

        <div id="content">
            {% block content %}
            {% endblock %}
        </div>

        <hr>
        <footer>
            <p>&copy; 2024 Proyecto de Bachillerato</p>
        </footer>
    </body>
    </html>
    ```

3.  **Crea la Plantilla de Inicio (`principal/templates/principal/inicio.html`):**
    Esta hereda de `base.html` y usa las variables del contexto (`contexto`) que enviamos desde la vista.

    ```html
    {% extends "base.html" %} 

    {% block title %}Inicio - {{ nombre_sitio }}{% endblock %}

    {% block content %}
        <h2>Bienvenido a {{ nombre_sitio }}</h2>

        {% if es_alumno %}
            <p>Este es un proyecto básico de Django para alumnos de tercer semestre.</p>
        {% else %}
            <p>Este es un sitio web de prueba.</p>
        {% endif %}

        <p>Aprende más sobre este proyecto y su versión.</p>
    {% endblock %}
    ```

4.  **Crea la Plantilla Acerca de (`principal/templates/principal/acerca_de.html`):**

    ```html
    {% extends "base.html" %}

    {% block title %}Acerca de{% endblock %}

    {% block content %}
        <h2>Acerca de Nuestro Proyecto</h2>
        <p>
            Esta página demuestra el uso de múltiples vistas y plantillas en una aplicación Django.
        </p>
        <p>
            Versión actual: **{{ version }}**
        </p>
    {% endblock %}
    ```

-----

### 5\. Prueba Final

1.  Asegúrate de que el servidor de Django esté corriendo:

    ```bash
    python manage.py runserver
    ```

2.  Abre tu navegador y ve a `http://127.0.0.1:8000/`.

      * Deberías ver la **Página de Inicio** con el título y el mensaje dinámico.
      * Haz clic en el enlace **"Acerca de"** en el menú de navegación.
      * Deberías ser redirigido a `http://127.0.0.1:8000/acerca/`, mostrando la segunda plantilla y la información de la versión.

**Conceptos Clave de esta Práctica:**

  * **Vistas Múltiples:** Crear diferentes funciones en `views.py` para distintas páginas.
  * **Mapeo de URLs:** Conectar diferentes rutas de URL a diferentes vistas usando `urls.py`.
  * **Herencia de Plantillas:** Usar `{% extends "base.html" %}` para tener una estructura de navegación coherente en todo el sitio, evitando repetir código HTML.
  * **Contexto Dinámico:** Pasar datos de la vista a la plantilla (ej. `{{ nombre_sitio }}`).
  * **Lógica en Plantillas:** Usar etiquetas como `{% if es_alumno %}` y `{% else %}` para cambiar el contenido.
