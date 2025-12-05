## 🚀 Práctica: Mi Primera Aplicación Django (Hola Mundo)

Esta práctica se divide en tres fases: **Configuración**, **Creación del Proyecto**, y **Ejecución**.

-----

### Fase 1: Configuración del Entorno

Asegúrate de que los estudiantes tengan **Python** y **VS Code** instalados.
Crear un Entorno Virtual (Recomendado)
Un entorno virtual aísla las dependencias de tu proyecto para que no interfieran con otros proyectos o la instalación global de Python.
    En VS Code, abre la Terminal (Terminal > Nueva Terminal).

    Ejecuta el siguiente comando para crear el entorno virtual (llamado venv):

    python -m venv .venv

Activar el Entorno Virtual:

    .venv\Scripts\Activate.ps1
Verás que el nombre (.venv) aparece al inicio de tu línea de comandos, indicando que está activo.

#### 1\. Instalar Django

Abre la **Terminal** dentro de VS Code (o la terminal del sistema) y ejecuta el siguiente comando para instalar Django:

```bash
pip install django
```

#### 2\. Crear una Carpeta para el Proyecto

Crea una carpeta donde se guardará todo el proyecto (ejemplo: `ProyectoDjangoBachillerato`) y ábrela en VS Code.

-----

### Fase 2: Creación y Configuración del Proyecto

#### 1\. Crear el Proyecto Base

En la terminal de VS Code, dentro de la carpeta que creaste, ejecuta el comando para crear la estructura inicial del proyecto:

```bash
django-admin startproject mi_proyecto
```

Esto crea una carpeta llamada `mi_proyecto`. Entra en ella:

```bash
cd mi_proyecto
```

#### 2\. Crear la Aplicación "Saludos"

Un proyecto Django puede tener varias "apps". Vamos a crear una app específica para nuestros saludos:

```bash
python manage.py startapp saludos
```

Ahora la estructura de archivos es más compleja, con una nueva carpeta `saludos`.

#### 3\. Registrar la Aplicación

Necesitas decirle a Django que la aplicación `saludos` existe.

  * Abre el archivo: `mi_proyecto/settings.py`
  * Busca la lista `INSTALLED_APPS` y añade `'saludos',` dentro de ella.

<!-- end list -->

```python
# mi_proyecto/settings.py
...
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # NUEVA LINEA: Registrar nuestra app
    'saludos',
]
...
```

-----

### Fase 3: Lógica y Visualización (El Hola Mundo)

#### 1\. Definir la Vista (View)

Una **vista** es una función en Python que recibe una solicitud web y devuelve una respuesta.

  * Abre el archivo: `saludos/views.py`
  * Reemplaza su contenido con la siguiente función simple:

<!-- end list -->

```python
# saludos/views.py

from django.http import HttpResponse

def hola_mundo(request):
    """
    Esta es nuestra vista. Cuando se solicite esta URL,
    devolverá la respuesta '¡Hola, Mundo desde Django!'.
    """
    html = "<h1>¡Hola, **Mundo desde Django**!</h1>"
    html += "<p>¡Felicidades! Acabas de crear tu primera página web con el framework Django.</p>"
    return HttpResponse(html)
```

#### 2\. Mapear la URL (URLs)

Necesitamos decirle a Django qué URL debe ejecutar la función `hola_mundo`.

  * Crea un **nuevo archivo** dentro de la carpeta `saludos` llamado `urls.py`.
  * Añade el siguiente código en el nuevo archivo:

<!-- end list -->

```python
# saludos/urls.py

from django.urls import path
from . import views # Importamos las vistas de nuestra app

urlpatterns = [
    # Cuando la URL esté vacía (''), ejecuta la función views.hola_mundo
    path('', views.hola_mundo, name='hola_mundo'),
]
```

#### 3\. Conectar las URLs Principales

Finalmente, conecta el archivo `saludos/urls.py` al archivo principal de URLs del proyecto.

  * Abre el archivo: `mi_proyecto/urls.py`
  * Asegúrate de importar `include` y añade la línea de `path('saludo/', include('saludos.urls'))`:

<!-- end list -->

```python
# mi_proyecto/urls.py

from django.contrib import admin
from django.urls import path, include # Asegúrate de que 'include' esté importado

urlpatterns = [
    path('admin/', admin.site.urls),
    # NUEVA LINEA: Cualquier URL que empiece con 'saludo/' va a la app 'saludos'
    path('saludo/', include('saludos.urls')),
]
```

-----

### Fase 4: Ejecución y Prueba

#### 1\. Ejecutar el Servidor

En la terminal de VS Code (asegúrate de estar en la carpeta `mi_proyecto` donde está `manage.py`), ejecuta el servidor de desarrollo:

```bash
python manage.py runserver
```

#### 2\. Ver el Resultado

  * El servidor te indicará una dirección (normalmente: `http://127.0.0.1:8000/`).
  * Abre tu navegador y navega a la URL completa que definiste: **`http://127.0.0.1:8000/saludo/`**

¡Deberías ver el mensaje **"¡Hola, Mundo desde Django\!"**\!

-----

### ✅ Pasos Siguientes para el Alumno

Para desafiar un poco más a los estudiantes, pídeles que intenten lo siguiente:

1.  **Cambiar el mensaje:** Modificar la función `hola_mundo` en `saludos/views.py` para que muestre el nombre del alumno.
2.  **Nueva URL:** Crear una segunda función en `views.py` (ej: `despedida`) y mapearla a una nueva URL (ej: `http://127.0.0.1:8000/despedida/`) en `saludos/urls.py`.

¿Te gustaría que generara la misma práctica utilizando plantillas HTML (Templates) para hacerla más visual?
