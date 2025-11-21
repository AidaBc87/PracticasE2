# Blog-publicaciones-en-django
## 📚 **Guía Paso a Paso: Crear un Proyecto Básico en Django (Nivel Principiante)**

---
Activar los Script en Windows
    Ejecutar como administrador el PowerShell
    Escribir el comando: Set-ExecutionPolicy RemoteSigned y presiona Enter
    Luego Escribir: S y presiona Enter
    Escribe: exit y presiona Enter

### ✅ Requisitos previos
- Tener instalado **Python 3.6 o superior**.
- Tener instalado **Visual Studio Code (VS Code)**.
- Conexión a internet.

---

### 🔹 Paso 1: Abrir la consola "cmd" de Windows

1. Presiona la tecla **Windows** del teclado.
2. Escribe: `cmd`
3. Haz clic en **Símbolo del sistema** o **Command Prompt**.
4. Se abrirá una ventana negra (la terminal).

> ✅ Ahora estás en la consola de Windows.

---

### 🔹 Paso 2: Crear carpeta de trabajo `Guia_Django`

En la consola `cmd`, escribe:

```bash
mkdir Guia_Django
```

Luego, entra a la carpeta:

```bash
cd Guia_Django
```

> ✅ Ahora estás dentro de tu carpeta de trabajo.

---

### 🔹 Paso 3: Abrir VS Code desde la terminal

En la misma terminal, escribe:

```bash
code .
```

> ✅ Esto abrirá VS Code en la carpeta actual (`Guia_Django`).

---

### 🔹 Paso 4: Abrir la terminal de VS Code

1. En VS Code, haz clic en el menú **Terminal**.
2. Selecciona **Nuevo terminal**.
3. Aparecerá una nueva terminal dentro de VS Code.

> ✅ Ahora puedes ejecutar comandos desde VS Code.

---

### 🔹 Paso 5: Ver la versión de Python

En la terminal de VS Code, escribe:

```bash
python --version
```

> ✅ Debe aparecer algo como `Python 3.x.x`. Si no, instala Python desde [python.org](https://www.python.org/downloads/).

---

### 🔹 Paso 6: Crear un entorno virtual llamado `.venv`

En la terminal:

```bash
python -m venv .venv
```

> ✅ Se creó una carpeta `.venv` con tu entorno virtual.

---

### 🔹 Paso 7: Activar el entorno virtual

En la terminal de VS Code:

```bash
.venv\Scripts\activate
```

> ✅ Verás que el nombre `(.venv)` aparece al inicio de la línea. ¡Estás en el entorno!

---

### 🔹 Paso 8: Instalar Django

Con el entorno activado, escribe:

```bash
pip install django
```

> ✅ Django se instalará. Espera a que termine.

---

### 🔹 Paso 9: Ver las herramientas disponibles de Django

Escribe:

```bash
django-admin --help
```

> ✅ Verás una lista de comandos que Django puede hacer.

---

### 🔹 Paso 10: Crear el proyecto `backend_blog` sin duplicar carpetas

Ejecuta este comando:

```bash
django-admin startproject backend_blog .
```

> ⚠️ El punto `.` al final evita crear una carpeta extra.

---

### 🔹 Paso 11: Estructura de carpetas y archivos del proyecto

Después de crear el proyecto, tu estructura debe verse así:

```
Guia_Django/
│
├── .venv/                  ← Entorno virtual
├── backend_blog/           ← Carpeta del proyecto Django
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── manage.py
└── (otros archivos ocultos)
```

> ✅ `manage.py` es clave para ejecutar comandos.

---

### 🔹 Paso 12: Ejecutar el servidor Django

En la terminal (con el entorno activado):

```bash
python manage.py runserver
```

> ✅ Verás un mensaje diciendo que el servidor está en `http://127.0.0.1:8000/`

---

### 🔹 Paso 13: Ver la página de bienvenida

Abre tu navegador (Chrome, Edge, etc.) y escribe:

```
http://127.0.0.1:8000
```

> ✅ Deberás ver la página de bienvenida de Django: "The install worked successfully!"

---

### 🔹 Paso 14: Detener el servidor

En la terminal, presiona:

```
Ctrl + C
```

> ✅ El servidor se detiene.

---

### 🔹 Paso 15: Crear la aplicación `app_blog`

En la terminal:

```bash
python manage.py startapp app_blog
```

> ✅ Se crea la carpeta `app_blog` con archivos como `models.py`, `views.py`, etc.

---

### 🔹 Paso 16: Estructura completa del proyecto

Ahora tu estructura debe ser:

```
Guia_Django/
│
├── .venv/
├── backend_blog/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── app_blog/
│   ├── migrations/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── views.py
│   └── ...
├── manage.py
└── ...
```

---

### 🔹 Paso 17: Agregar `app_blog` en `settings.py`

1. Abre en VS Code: `backend_blog/settings.py`
2. Busca la lista `INSTALLED_APPS`
3. Agrega `'app_blog'` al final:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'app_blog',  # ← Agrega esta línea
]
```

> ✅ Guarda el archivo.

---

### 🔹 Paso 18: Crear la primera vista basada en funciones

Abre el archivo: `app_blog/views.py`

Reemplaza su contenido con:

```python
from django.http import HttpResponse

def index(request):
    return HttpResponse("<h1>Bienvenido al Blog</h1>")
```

> ✅ Esta vista muestra un mensaje simple.

---

### 🔹 Paso 19: Crear el archivo `urls.py` en `app_blog`

1. Dentro de la carpeta `app_blog`, crea un nuevo archivo llamado `urls.py`.

---

### 🔹 Paso 20: Código de `app_blog/urls.py` (una sola ruta)

Pega este código:

```python
from django.urls import path
from . import views  # Importa las vistas de esta misma app

urlpatterns = [
    path('', views.index, name='index'),  # Ruta raíz de la app
]
```

> ✅ Define una ruta que llama a la vista `index`.

---

### 🔹 Paso 21: Incluir `app_blog.urls` en `backend_blog/urls.py`

Abre `backend_blog/urls.py` y modifícalo así:

```python
from django.contrib import admin
from django.urls import path, include  # ← Asegúrate de importar 'include'

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app_blog.urls')),  # ← Incluye las rutas de app_blog
]
```

> ✅ Ahora el proyecto sabe que debe usar las rutas de `app_blog`.

---

### 🔹 Paso 22: Ejecutar el servidor

En la terminal:

```bash
python manage.py runserver
```

---

### 🔹 Paso 23: Detener el servidor

Presiona `Ctrl + C` cuando quieras detenerlo.

---

### 🔹 Paso 24: Crear el modelo `Publicacion`

Abre `app_blog/models.py` y escribe:

```python
from django.db import models

class Publicacion(models.Model):
    titulo = models.CharField(max_length=200)  # Título de la publicación
    contenido = models.TextField()             # Contenido
    fecha_de_creacion = models.DateTimeField(auto_now_add=True)  # Fecha automática

    def __str__(self):
        return self.titulo  # Muestra el título en el admin
```

> ✅ Este modelo representa una entrada de blog.

---

### 🔹 Paso 25: Realizar migraciones (crear archivo de migración)

En la terminal:

```bash
python manage.py makemigrations
```

> ✅ Django crea un archivo en `app_blog/migrations/` que describe los cambios en la base de datos.

---

### 🔹 Paso 26: Migrar (aplicar cambios a la base de datos)

```bash
python manage.py migrate
```

> ✅ La tabla `Publicacion` se crea en la base de datos (por defecto: SQLite).

---

### 🔹 Paso 27: Registrar el modelo en `admin.py`

Abre `app_blog/admin.py` y escribe:

```python
from django.contrib import admin
from .models import Publicacion  # Importa el modelo

admin.site.register(Publicacion)  # Registra el modelo
```

> ✅ Ahora podrás ver `Publicacion` en el panel de administración.

---

### 🔹 Paso 28: Crear superusuario

En la terminal:

```bash
python manage.py createsuperuser
```

Te pedirá:

- **Username**: `admin`
- **Email address**: `elisa@gmail.com`
- **Password**: `admin`
- **Password (again)**: `admin`

> ✅ Usuario administrador creado.

---

### 🔹 Paso 29: Ejecutar el servidor

```bash
python manage.py runserver
```

---

### 🔹 Paso 30: Detener el servidor

`Ctrl + C` cuando quieras.

---

### 🔹 Paso 31: Crear la carpeta `templates` dentro de `app_blog`

En VS Code, dentro de `app_blog`, crea una carpeta llamada `templates`.

---

### 🔹 Paso 32: Crear subcarpeta `app_blog` dentro de `templates`

Dentro de `templates`, crea otra carpeta llamada `app_blog`.

> ✅ Así: `app_blog/templates/app_blog/`

> ✅ Esto evita conflictos si hay otras apps con archivos `index.html`.

---

### 🔹 Paso 33: Crear `index.html` en `app_blog/templates/app_blog/`

Crea el archivo `index.html` y escribe:

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Blog</title>
</head>
<body>
    <h1>Entradas del blog</h1>
    
    <!-- Lista de publicaciones -->
    <ul>
        <!-- Recorre cada publicación en el contexto -->
        {% for publicacion in publicaciones %}
            <li>
                <!-- Muestra el título y la fecha de creación -->
                <strong>{{ publicacion.titulo }}</strong> 
                ({{ publicacion.fecha_de_creacion|date:"d/m/Y" }})
            </li>
        {% endfor %}
    </ul>
</body>
</html>
```

> ✅ Los `{% %}` son etiquetas de Django para lógica en plantillas.

---

### 🔹 Paso 34: Actualizar `views.py` para mostrar publicaciones

Abre `app_blog/views.py` y reemplaza con:

```python
from django.shortcuts import render
from .models import Publicacion  # Importa el modelo

def index(request):
    # Obtener todas las publicaciones de la base de datos
    publicaciones = Publicacion.objects.all()
    # Renderiza la plantilla y pasa los datos
    return render(request, 'app_blog/index.html', {'publicaciones': publicaciones})
```

> ✅ `render` combina la vista con la plantilla y los datos.

---

### 🔹 Paso 35: Crear archivo de requerimientos (`requirements.txt`)

En la terminal:

```bash
pip freeze > requirements.txt
```

> ✅ Crea un archivo con todas las librerías instaladas (útil para compartir el proyecto).

---

### 🔹 Paso 36: Ejecutar el servidor (¡proyecto funcionando!)

```bash
python manage.py runserver
```

---

### 🔹 Paso 37: Proyecto funcionando 🎉

1. Abre el navegador y ve a:
   ```
   http://127.0.0.1:8000
   ```

   > ✅ Verás "Entradas del blog" y si ya agregaste publicaciones, se mostrarán.

2. Ve al panel de administración:
   ```
   http://127.0.0.1:8000/admin
   ```

   - Inicia sesión con:
     - Usuario: `admin`
     - Contraseña: `admin`
   - Agrega una o más publicaciones en `Publicacions`.

3. Vuelve a la página principal para verlas.

---

## ✅ ¡Felicidades! Has creado tu primer proyecto en Django.

### 🧠 ¿Qué aprendiste?
- Usar la terminal.
- Trabajar con entornos virtuales.
- Crear un proyecto y una app en Django.
- Hacer modelos, vistas, URLs y plantillas.
- Usar la base de datos y el panel de administración.

---

## 📌 Consejos finales
- Guarda siempre tus archivos en VS Code (`Ctrl + S`).
- Activa el entorno virtual cada vez que abras el proyecto.
- Usa `requirements.txt` para reinstalar Django si cambias de computadora.

---

¿Quieres continuar? Puedes agregar:
- Formularios.
- Estilos con CSS.
- Más modelos (como Categorías o Autores).

¡Sigue aprendiendo! 🚀

--- 

📌 **Guía creada para estudiantes de preparatoria – Nivel principiante – Windows**  
