## 🚀 Práctica Guiada: Mi Primer Proyecto Django en VS Code

### Paso 1: Instalación y Configuración del Entorno

#### 1.1. Instalar Python

Asegúrate de que Python esté instalado en tu sistema.

1.  Ve al sitio oficial de [Python](https://www.python.org/downloads/).
2.  Descarga e instala la versión más reciente (se recomienda la versión 3.x).
3.  **MUY IMPORTANTE:** Durante la instalación, marca la casilla **"Add Python to PATH"** (Agregar Python a PATH).

#### 1.2. Instalar Visual Studio Code

1.  Descarga e instala [VS Code](https://code.visualstudio.com/) desde el sitio oficial.

#### 1.3. Extensiones de VS Code

Abre VS Code e instala las siguientes extensiones (usa el ícono de extensiones en la barra lateral izquierda 📦):

1.  **Python** (por Microsoft): Esencial para el soporte de Python.
2.  **Pylance** (por Microsoft): Mejora el autocompletado y análisis de código.

-----

### Paso 2: Configuración del Proyecto

#### 2.1. Crear y Abrir la Carpeta del Proyecto

1.  Crea una nueva carpeta en tu escritorio o donde prefieras, por ejemplo, `ProyectoDjango3er`.
2.  Abre VS Code y haz clic en **Archivo \> Abrir Carpeta** y selecciona la carpeta que acabas de crear.

#### 2.2. Crear un Entorno Virtual (Recomendado)

Un **entorno virtual** aísla las dependencias de tu proyecto para que no interfieran con otros proyectos o la instalación global de Python.

1.  En VS Code, abre la **Terminal** (**Terminal \> Nueva Terminal**).

2.  Ejecuta el siguiente comando para crear el entorno virtual (llamado `venv`):

    ```bash
    python -m venv venv
    ```

3.  **Activar el Entorno Virtual:**

      * **Windows (PowerShell):**
        ```bash
        .\venv\Scripts\Activate.ps1
        ```
      * **Linux/macOS (Bash/Zsh):**
        ```bash
        source venv/bin/activate
        ```

    Verás que el nombre `(venv)` aparece al inicio de tu línea de comandos, indicando que está activo.

#### 2.3. Instalar Django

Con el entorno virtual activado, instala el framework Django:

```bash
pip install django
```

-----

### Paso 3: Crear el Proyecto y la Aplicación

En Django, un **Proyecto** es la configuración completa (bases de datos, ajustes generales) y una **Aplicación** es un módulo que hace una cosa específica (por ejemplo, una aplicación de "Blog", una de "Usuarios").

#### 3.1. Crear el Proyecto Django

Desde la terminal (y con `(venv)` activo), ejecuta:

```bash
django-admin startproject mi_sitio .
```

  * `mi_sitio`: Es el nombre del proyecto principal.
  * `.`: Indica que se cree el proyecto en la carpeta actual.

Ahora verás una nueva carpeta `mi_sitio` con archivos de configuración y un archivo `manage.py` en la raíz.

#### 3.2. Crear la Aplicación (App)

Ahora crearemos la aplicación que contendrá nuestra página web. La llamaremos `pagina_inicio`.

```bash
python manage.py startapp pagina_inicio
```

[Image of the Django project structure]

#### 3.3. Registrar la Aplicación

Para que Django sepa que existe tu nueva app, debes registrarla en el archivo de configuración del proyecto:

1.  Abre el archivo **`mi_sitio/settings.py`**.

2.  Busca la lista `INSTALLED_APPS` y agrega el nombre de tu aplicación:

    ```python
    # mi_sitio/settings.py

    INSTALLED_APPS = [
        # ... otras apps de Django
        'pagina_inicio',  # ¡Añade esta línea!
    ]
    ```

-----

### Paso 4: Creación de la Página Web

#### 4.1. Definir la Vista (View)

La **vista** es una función de Python que recibe una solicitud web y devuelve una respuesta (en nuestro caso, una página HTML).

1.  Abre el archivo **`pagina_inicio/views.py`**.

2.  Reemplaza el contenido con el siguiente código:

    ```python
    # pagina_inicio/views.py

    from django.shortcuts import render
    from django.http import HttpResponse

    # Definimos la función de la vista
    def inicio(request):
        # Esta función busca y renderiza la plantilla 'index.html'
        # que crearemos en el siguiente paso.
        return render(request, 'index.html', {})
    ```

#### 4.2. Crear la Plantilla (Template)

La **plantilla** es el archivo HTML que contiene la estructura y el contenido que el usuario verá.

1.  Dentro de la carpeta `pagina_inicio`, crea una nueva carpeta llamada **`templates`**.

2.  Dentro de la carpeta `templates`, crea un nuevo archivo llamado **`index.html`**.

    La estructura de archivos debe ser: `pagina_inicio/templates/index.html`

3.  Pega el siguiente código HTML en **`pagina_inicio/templates/index.html`**:

    ```html
    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <title>Mi Primera Web con Django</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                text-align: center;
                margin-top: 50px;
                background-color: #f4f4f4;
            }
            .container {
                background-color: white;
                padding: 30px;
                border-radius: 8px;
                box-shadow: 0 4px 8px rgba(0,0,0,0.1);
                display: inline-block;
            }
            h1 {
                color: #007bff; /* Azul de Django */
            }
        </style>
    </head>
    <body>
        <div class="container">
            <h1>¡Hola, 3er Semestre de Bachillerato!</h1>
            <p>🎉 Has configurado y ejecutado tu primera página web con Django y Python en VS Code. 🎉</p>
            <p>¡Este es el inicio de tu camino como desarrollador web!</p>
        </div>
    </body>
    </html>
    ```

#### 4.3. Mapear las URLs (El camino)

Necesitamos decirle a Django qué URL debe ejecutar la función de vista que creamos. Lo haremos en dos partes:

**a) URLs de la Aplicación (pagina\_inicio)**

1.  Dentro de la carpeta `pagina_inicio`, crea un nuevo archivo llamado **`urls.py`**.

2.  Pega este código:

    ```python
    # pagina_inicio/urls.py

    from django.urls import path
    from . import views

    urlpatterns = [
        # La ruta vacía '' (la raíz) se mapea a la función views.inicio
        path('', views.inicio, name='inicio'),
    ]
    ```

**b) URLs del Proyecto (mi\_sitio)**

1.  Abre el archivo **`mi_sitio/urls.py`** (el del proyecto).

2.  Modifica el archivo para **incluir** las URLs de tu aplicación:

    ```python
    # mi_sitio/urls.py

    from django.contrib import admin
    from django.urls import path, include  # Importa 'include'

    urlpatterns = [
        path('admin/', admin.site.urls),
        # Añade la línea para incluir las URLs de tu app
        path('', include('pagina_inicio.urls')),
    ]
    ```

-----

### Paso 5: Ejecutar el Servidor Web

¡Todo está listo\! Es momento de probar tu trabajo.

1.  Asegúrate de que la terminal en VS Code esté activa y el entorno virtual `(venv)` esté activo.

2.  Ejecuta el siguiente comando:

    ```bash
    python manage.py runserver
    ```

3.  El servidor se iniciará y verás un mensaje similar a este:

    ```
    Starting development server at http://127.0.0.1:8000/
    Quit the server with CONTROL-C.
    ```

4.  Abre tu navegador web y ve a la dirección: **`http://127.0.0.1:8000/`**

¡Deberías ver la página de bienvenida que creaste\! 🎉

Para detener el servidor, presiona **Ctrl + C** en la terminal. 
¡Felicidades a tus estudiantes\!
