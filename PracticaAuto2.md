Esta práctica se centrará en el flujo básico de **Vista** y **Plantilla**, que es lo primero que se aprende.

### Activar Scripts en Windows
Ejecutar como administrador el PowerShell Escribir el comando: Set-ExecutionPolicy RemoteSigned y presiona Enter 
Luego Escribir: S y presiona Enter 
Escribe: exit y presiona Enter

## 🚀 Práctica Rápida: "Mi Primer Mensaje" en Django (Paso a Paso)

### Paso 1: Configuración Inicial en VS Code

1.  **Crea una Carpeta de Proyecto:** Abre VS Code, ve a `Archivo` \> `Abrir Carpeta` y crea o selecciona una carpeta vacía (por ejemplo, `HolaDjango`).

2.  **Abre el Terminal:** Ve a `Terminal` \> `Nuevo Terminal`. Todos los comandos se ejecutarán aquí.

3.  **Crea el Entorno Virtual:**

    ```bash
    python -m venv .venv
    ```

4.  **Activa el Entorno:**

      * **Windows (PowerShell):** `.venv\Scripts\Activate`
      * **macOS/Linux:** `source .venv/bin/activate`

5.  **Instala Django:**

    ```bash
    pip install django
    ```

-----

### Paso 2: Creación del Proyecto y la Aplicación

1.  **Crea el Proyecto Principal (`myproject`):**
    ```bash
    django-admin startproject myproject .
    ```
    > **Nota:** El punto (`.`) es para crear el proyecto en la carpeta actual.
2.  **Crea la Aplicación (`hello`):**
    ```bash
    python manage.py startapp hello
    ```

-----

### Paso 3: Configuración y Registro

1.  **Registra la Aplicación:** Abre **`myproject/settings.py`** y añade `'hello.apps.HelloConfig'` (o solo `'hello'`) a la lista `INSTALLED_APPS`.

    ```python
    # myproject/settings.py
    INSTALLED_APPS = [
        # ... otras apps ...
        'hello',  # ¡Añade esto!
    ]
    ```

-----

### Paso 4: Creación de la Vista (Lógica Python)

La **Vista** es la función que recibe una solicitud y genera una respuesta.

1.  Abre **`hello/views.py`** y define una función de vista que renderizará una plantilla HTML.

    ```python
    # hello/views.py
    from django.shortcuts import render

    def welcome_view(request):
        # Datos dinámicos a enviar a la plantilla
        context = {
            'message': '¡Hola desde Django y VS Code!',
            'author': 'Práctica Sencilla'
        }
        # La función render busca 'hello/welcome.html' en la carpeta de plantillas
        return render(request, 'hello/welcome.html', context)
    ```

-----

### Paso 5: Definición de URLs (Ruteo)

Para que la vista sea accesible, debemos mapearla a una URL.

1.  **Crea `hello/urls.py`:** Dentro de la carpeta `hello/`, crea un archivo llamado **`urls.py`**.

    ```python
    # hello/urls.py
    from django.urls import path
    from . import views

    urlpatterns = [
        # Asocia la URL raíz ('') a la función welcome_view
        path('', views.welcome_view, name='welcome'),
    ]
    ```

2.  **Incluye las URLs de la App en el Proyecto:** Abre **`myproject/urls.py`** e incluye el archivo `urls.py` de la aplicación `hello`.

    ```python
    # myproject/urls.py
    from django.contrib import admin
    from django.urls import path, include # Importa 'include'

    urlpatterns = [
        path('admin/', admin.site.urls),
        # Cuando alguien acceda a la URL raíz del proyecto, usa las URLs de la app 'hello'
        path('', include('hello.urls')), 
    ]
    ```

-----

### Paso 6: Creación de la Plantilla HTML

Las plantillas definen la estructura HTML y usan datos dinámicos.

1.  **Crea la Estructura de Plantillas:** Dentro de la carpeta `hello/`, crea la ruta: **`hello/templates/hello/`**.

2.  **Crea `welcome.html`:** Dentro de `hello/templates/hello/`, crea el archivo **`welcome.html`**.

    ```html
    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <title>Mi Primer Django</title>
        <style>
            body { font-family: Arial, sans-serif; background-color: #f0f0f0; padding: 20px; }
            h1 { color: #4CAF50; }
            footer { margin-top: 20px; font-size: 0.8em; color: #777; }
        </style>
    </head>
    <body>
        <h1>{{ message }}</h1> 
        <p>¡Este contenido está siendo generado y renderizado por tu aplicación Django!</p>

        <footer>
            Creado por: {{ author }}
        </footer>
    </body>
    </html>
    ```

    > **Nota:** La sintaxis `{{ variable }}` permite mostrar el valor de las variables pasadas desde la vista.

-----

### Paso 7: Ejecución y Verificación

1.  **Ejecuta el Servidor de Desarrollo:**
    ```bash
    python manage.py runserver
    ```
2.  **Verifica en el Navegador:** Abre `http://127.0.0.1:8000/`.

Deberías ver tu página HTML con el mensaje **¡Hola desde Django y VS Code\!** y el texto del autor, confirmando que el flujo **URL $\rightarrow$ Vista $\rightarrow$ Plantilla** está funcionando correctamente.

-----
Si este flujo fue claro, el siguiente paso lógico es aprender a integrar archivos **CSS** externos y el concepto de **Archivos Estáticos**.
La integración de archivos estáticos (como CSS, JavaScript o imágenes) es esencial para que un sitio web tenga estilo y funcionalidad avanzada.
Continuaremos con el proyecto "Mi Primer Mensaje" (myproject/hello).
🎨 Integración de Archivos Estáticos (CSS)
En este ejercicio, utilizaremos la carpeta static que creaste en el Ejercicio 3 para darle un mejor estilo a tu página welcome.html.
________________________________________
Paso 1: Configurar la Carpeta static
Aunque Django busca automáticamente dentro de las carpetas static de cada aplicación, es una buena práctica configurarlas.
1.	Abre myproject/settings.py.
2.	Asegúrate de que las siguientes líneas existen al final del archivo para definir cómo manejar los archivos estáticos:
Python
# myproject/settings.py

import os 
from pathlib import Path

# ... (al inicio)
BASE_DIR = Path(__file__).resolve().parent.parent
# ...

# URL base para servir archivos estáticos (ej. /static/css/style.css)
STATIC_URL = 'static/'

# Directorios donde Django buscará archivos estáticos adicionales (como la carpeta 'static' global)
STATICFILES_DIRS = [
    BASE_DIR / 'static', 
]
3.	Crea la Carpeta static Global: En la raíz de tu proyecto (HolaDjango), crea una nueva carpeta llamada static.
________________________________________
Paso 2: Crear el Archivo CSS
1.	Dentro de la carpeta static/ que acabas de crear, crea una subcarpeta para organizar tus archivos (por ejemplo, css).
2.	Dentro de static/css/, crea un archivo llamado main.css.
3.	HolaDjango/
4.	├── static/
5.	│   └── css/
6.	│       └── main.css  <-- Archivo a crear
7.	└── ...
8.	Abre static/css/main.css y añade algunos estilos:
CSS
/* static/css/main.css */
body {
    font-family: 'Verdana', sans-serif;
    background-color: #e0f7fa; /* Azul muy claro */
    color: #004d40; /* Verde oscuro */
    margin: 40px;
    text-align: center;
}

h1 {
    color: #00796b; /* Un tono de verde/azul más fuerte */
    border-bottom: 3px solid #004d40;
    padding-bottom: 10px;
    display: inline-block;
}
________________________________________
Paso 3: Enlazar el CSS en la Plantilla
Para que Django pueda encontrar y servir el archivo CSS, debes usar las etiquetas especiales de plantillas de Django.
1.	Abre hello/templates/hello/welcome.html.
2.	Agrega la Etiqueta de Carga: Añade {% load static %} al comienzo del archivo.
3.	Usa la Etiqueta static: Reemplaza la etiqueta <style> con un enlace al archivo main.css.
HTML
{% load static %} <!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Mi Primer Django</title>
    <link rel="stylesheet" href="{% static 'css/main.css' %}">
    </head>
<body>
    <h1>{{ message }}</h1> 
    <p>¡Este contenido está siendo generado y renderizado por tu aplicación Django!</p>

    <footer>
        Creado por: {{ author }}
    </footer>
</body>
</html>
Explicación: La etiqueta {% static 'css/main.css' %} le pide a Django que genere la URL completa (/static/css/main.css) y busque el archivo en todas las carpetas static configuradas.
________________________________________
Paso 4: Probar y Verificar
1.	Asegúrate de que tu servidor esté ejecutándose:
Bash
python manage.py runserver
2.	Ve a http://127.0.0.1:8000/.
Ahora verás tu página con el nuevo fondo azul claro y el texto en verde oscuro, confirmando que Django está sirviendo correctamente el archivo main.css desde la carpeta static.
________________________________________
El siguiente paso fundamental en la práctica de Django es el manejo de imágenes subidas por los usuarios, que utiliza un concepto diferente: Archivos Media. ¿Te gustaría continuar con ese ejercicio?
--
El manejo de archivos Media es fundamental porque son los archivos que los usuarios suben (fotos de perfil, imágenes de proyectos, documentos), a diferencia de los archivos Static (CSS, JS) que son fijos y subidos por el desarrollador.
Para este ejercicio, simularemos la subida de una imagen de proyecto.
🖼️ Manejo de Archivos Media (Imágenes Subidas por Usuarios)
Este proceso requiere configurar dónde se guardarán los archivos y cómo Django los servirá en el entorno de desarrollo.
________________________________________
Paso 1: Configurar Media en settings.py
Debemos decirle a Django dónde guardar los archivos que sube el usuario y bajo qué URL se accederán.
1.	Abre myproject/settings.py y añade estas líneas al final del archivo:
Python
# myproject/settings.py (al final)

# 1. Definición de la URL base para archivos subidos por usuarios
MEDIA_URL = '/media/'

# 2. Definición de la ruta ABSOLUTA donde se guardarán físicamente los archivos
MEDIA_ROOT = BASE_DIR / 'media' 
2.	Crea la Carpeta media: En la raíz de tu proyecto (HolaDjango), crea una nueva carpeta llamada media.
3.	HolaDjango/
4.	├── media/  <-- Carpeta para archivos subidos por usuarios
5.	├── static/
6.	└── ...
________________________________________
Paso 2: Configurar las URLs para Servir Archivos Media (¡Solo en Desarrollo!)
El servidor de desarrollo de Django no sirve archivos media automáticamente. Debemos añadir reglas de URL para que lo haga.
1.	Abre myproject/urls.py y realiza las siguientes modificaciones. Necesitas importar settings y static para esta configuración.
Python
# myproject/urls.py
from django.contrib import admin
from django.urls import path, include
# Importaciones necesarias para MEDIA
from django.conf import settings 
from django.conf.urls.static import static 

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('hello.urls')),
]

# ¡IMPORTANTE! Solo servir archivos media cuando DEBUG=True (entorno de desarrollo)
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
Explicación: Esta línea le dice a Django: "Si la URL empieza por /media/, busca el archivo en la ruta definida por MEDIA_ROOT."
________________________________________
Paso 3: Modificar el Modelo (Solo una Vista Previa)
En el Ejercicio 4, creamos un modelo Project. Vamos a añadir un campo para la imagen.
1.	Abre hello/models.py (si usaste el nombre hello para tu aplicación; si usaste projects, abre ese archivo) y añade el campo image.
Python
# hello/models.py (o projects/models.py)
from django.db import models

class Project(models.Model):
    title = models.CharField(max_length=100)
    # Añade este campo de imagen
    image = models.ImageField(upload_to='project_images/') 
    description = models.TextField()
    technology = models.CharField(max_length=50)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.title
Nota: upload_to='project_images/' hace que las imágenes se guarden en media/project_images/.
Requisito: El campo ImageField requiere que instales la librería de procesamiento de imágenes Pillow:
Bash
pip install Pillow
2.	Crear y Aplicar Migraciones: El modelo ha cambiado, debemos actualizar la base de datos.
Bash
python manage.py makemigrations
python manage.py migrate
________________________________________
Paso 4: Subir una Imagen y Usarla en la Plantilla
1.	Sube una Imagen de Prueba:
o	Ejecuta el servidor: python manage.py runserver
o	Ve a http://127.0.0.1:8000/admin/.
o	Edita uno de tus proyectos existentes o crea uno nuevo.
o	Ahora verás el campo Image. Sube cualquier imagen de tu computadora.
o	Una vez guardado, revisa tu carpeta local media/project_images/. ¡Tu imagen se guardó allí!
2.	Modificar la Plantilla para Mostrar la Imagen:
Abre hello/templates/hello/welcome.html (o donde listaste tus proyectos) y añade la etiqueta <img>.
HTML
{% for project in projects %}
    <div class="project-card">
        <h2>{{ project.title }}</h2>

        {% if project.image %}
        <img src="{{ project.image.url }}" alt="{{ project.title }} preview" 
             style="max-width: 100%; height: auto; border-radius: 5px;">
        {% endif %}

        <p>{{ project.description }}</p>
        </div>
{% empty %}
    {% endfor %}
3.	Verificación: Recarga http://127.0.0.1:8000/. Ahora verás la imagen que subiste a través del administrador en tu página principal.
¡Con esto, has cubierto todo el ciclo de archivos: static para el CSS del sitio, y media para las imágenes de contenido subidas por el usuario!
