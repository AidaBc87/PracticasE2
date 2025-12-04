**Álbum de Fotos Digital Básico**.
Este proyecto les permitirá entender el ciclo completo de una aplicación web, desde la base de datos hasta la interfaz del usuario.

## 📸 Proyecto: Álbum de Fotos Digital Básico

Este proyecto permitirá a los alumnos subir, mostrar y etiquetar (opcionalmente) fotos simples, enfocándose en la interacción entre Django (backend/lógica) y HTML (frontend/presentación).

### 🎯 Objetivos de Aprendizaje

  * **Configuración del Entorno:** Usar VS Code, instalar Python y Django.
  * **Modelo (Django):** Definir una estructura de datos simple para las fotos.
  * **Vistas (Django):** Manejar la lógica para subir y mostrar imágenes.
  * **URLs (Django):** Mapear rutas web a las funciones de vista.
  * **Plantillas (HTML):** Usar el motor de plantillas de Django para renderizar HTML y mostrar datos (imágenes).
  * **Manejo de Archivos:** Configurar Django para servir archivos estáticos y multimedia (las imágenes subidas).

-----

### 📝 Estructura y Pasos del Proyecto

Aquí te dejo los pasos clave, que pueden ser divididos en sesiones para los estudiantes:

### 1\. 🛠️ Configuración Inicial

1.  **Instalar Python y VS Code:** Asegurarse de que ambos estén instalados.
2.  **Entorno Virtual:** Crear y activar un entorno virtual (muy importante para la gestión de dependencias).
    ```bash
    python -m venv venv
    # En Windows
    venv\Scripts\activate
    # En macOS/Linux
    source venv/bin/activate
    ```
3.  **Instalar Django:**
    ```bash
    pip install django pillow  # 'pillow' es necesario para manejar imágenes
    ```
4.  **Crear el Proyecto de Django:**
    ```bash
    django-admin startproject AlbumProject
    cd AlbumProject
    python manage.py startapp fotos
    ```

### 2\. 🖼️ Configuración de Archivos Multimedia (Media)

Los alumnos deben modificar `AlbumProject/settings.py` para decirle a Django dónde guardar y buscar las imágenes subidas.

```python
# AlbumProject/settings.py

# ... al final del archivo

MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

Luego, deben configurar las URLs para que Django pueda servir estos archivos en `AlbumProject/urls.py`.

```python
# AlbumProject/urls.py
from django.contrib import admin
from django.urls import path, include
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('fotos.urls')), # Incluir las URLs de la app 'fotos'
]

# **IMPORTANTE:** Solo para desarrollo. Permite servir archivos MEDIA.
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

### 3\. 💾 Definición del Modelo de Datos (fotos/models.py)

El modelo más simple para una foto.

```python
# fotos/models.py
from django.db import models

class Foto(models.Model):
    titulo = models.CharField(max_length=100)
    imagen = models.ImageField(upload_to='album_fotos/')
    fecha_subida = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.titulo
```

  * **`ImageField`** es la clave aquí, usando `upload_to` para especificar la carpeta dentro de `MEDIA_ROOT`.

### 4\. 🔗 Migraciones

Aplicar los cambios del modelo a la base de datos (SQLite por defecto).

```bash
python manage.py makemigrations fotos
python manage.py migrate
```

### 5\. 💻 Lógica de la Aplicación (fotos/views.py)

Necesitamos una vista para **mostrar** las fotos y una para **subir** una nueva.

```python
# fotos/views.py
from django.shortcuts import render, redirect
from .models import Foto
from .forms import FotoForm # Esto lo crearemos en el siguiente paso

# Vista para mostrar todas las fotos
def lista_fotos(request):
    fotos = Foto.objects.all().order_by('-fecha_subida')
    return render(request, 'fotos/lista_fotos.html', {'fotos': fotos})

# Vista para subir una nueva foto
def subir_foto(request):
    if request.method == 'POST':
        form = FotoForm(request.POST, request.FILES) # request.FILES es crucial para imágenes
        if form.is_valid():
            form.save()
            return redirect('lista_fotos') # Redirigir a la lista
    else:
        form = FotoForm()
    
    return render(request, 'fotos/subir_foto.html', {'form': form})
```

### 6\. 📝 Creación del Formulario (fotos/forms.py)

Este archivo no existe por defecto, los alumnos deben crearlo.

```python
# fotos/forms.py
from django import forms
from .models import Foto

class FotoForm(forms.ModelForm):
    class Meta:
        model = Foto
        fields = ['titulo', 'imagen']
        # widgets opcionales para personalizar la apariencia en el formulario
```

### 7\. 🌐 Definición de URLs (fotos/urls.py)

Crear este archivo para mapear las vistas.

```python
# fotos/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.lista_fotos, name='lista_fotos'), # Página principal
    path('subir/', views.subir_foto, name='subir_foto'),
]
```

### 8\. 🎨 Plantillas HTML

Crear la carpeta `fotos/templates/fotos/` dentro de la app `fotos`.

#### a) Plantilla de Lista (lista\_fotos.html)

Esta plantilla debe iterar sobre la lista de fotos y mostrar la imagen usando la URL configurada.

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Mi Álbum Digital</title>
</head>
<body>
    <h1>Álbum de Fotos de Bachillerato</h1>
    <p><a href="{% url 'subir_foto' %}">Sube una nueva foto aquí</a></p>

    <div class="fotos-container">
        {% for foto in fotos %}
        <div>
            <h2>{{ foto.titulo }}</h2>
            <img src="{{ foto.imagen.url }}" alt="{{ foto.titulo }}" style="max-width:300px; height:auto;">
            <p>Subida el: {{ foto.fecha_subida|date:"d M Y" }}</p>
        </div>
        <hr>
        {% empty %}
        <p>Aún no hay fotos en el álbum.</p>
        {% endfor %}
    </div>
</body>
</html>
```

#### b) Plantilla de Subida (subir\_foto.html)

Esta plantilla renderiza el formulario y es **CRUCIAL** usar `enctype="multipart/form-data"` para que el navegador pueda enviar archivos de imagen.

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Subir Foto</title>
</head>
<body>
    <h1>Subir una nueva Foto</h1>
    <a href="{% url 'lista_fotos' %}">← Volver al Álbum</a>
    
    <form method="POST" enctype="multipart/form-data"> 
        {% csrf_token %} {{ form.as_p }} <button type="submit">Guardar Foto</button>
    </form>
</body>
</html>
```

### 9\. 🚀 Ejecución del Proyecto

1.  Crear un superusuario (opcional, pero útil para ver las fotos en el admin de Django).
    ```bash
    python manage.py createsuperuser
    ```
2.  Ejecutar el servidor:
    ```bash
    python manage.py runserver
    ```
3.  Acceder a `http://127.0.0.1:8000/` y probar la subida de imágenes.

Este proyecto toca los puntos esenciales de una aplicación web real (Modelo, Vista, Plantilla, URLs y Manejo de Archivos) de una forma que es fácil de visualizar y depurar en **Visual Studio Code**.
