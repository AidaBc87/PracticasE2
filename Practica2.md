# Creación de la Aplicación y una Primera Página
## Objetivo: Crear una aplicación, definir una vista y un urls.py para mostrar tu primera página web.
Paso 1: Crear una Aplicación (App)
1.	Con la terminal de VS Code en el directorio principal y el entorno virtual activo, crea una aplicación (en Django, las apps son módulos de funcionalidad):
python manage.py startapp blog
Esto creará una nueva carpeta llamada blog con los archivos esenciales.

Paso 2: Configurar la App y Crear una Vista
1.	Abre el archivo mi_blog/settings.py y busca la sección INSTALLED_APPS. Agrega tu nueva aplicación a la lista para que Django la reconozca:
Python
INSTALLED_APPS = [
    # ... otras apps
    'blog',
]

2.	Abre el archivo blog/views.py y agrega el siguiente código. Esta es tu vista; es una función que procesa la solicitud y devuelve una respuesta.
Python
from django.shortcuts import render
from django.http import HttpResponse

def inicio(request):
    return HttpResponse("<h1>¡Hola, soy tu primera página web con Django!</h1>")

Paso 3: Mapear la URL
1.	Abre el archivo mi_blog/urls.py (el del proyecto, no el de la app). Aquí "dirás" a Django qué URLs deben ir a qué vistas.
2.	Modifícalo para que se vea así:

Python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('blog.urls')), # Incluye las URLs de tu app 'blog'
]
Ahora, necesitas crear el archivo de URLs de tu app.

3.	En la carpeta blog/, crea un nuevo archivo llamado urls.py.

4.	Agrega el siguiente código a este nuevo archivo:
Python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio, name='inicio'),
]
Esto le dice a Django: "Cuando alguien visite la URL base (''), usa la función inicio que está en el archivo views.py."

Paso 4: Ejecutar y Ver los Resultados
1.	Asegúrate de haber guardado todos los archivos.
2.	En la terminal, ejecuta de nuevo el servidor de Django:
python manage.py runserver    
3.	Ve a http://127.0.0.1:8000/ en tu navegador. En lugar del cohete de Django, ahora deberías ver el mensaje: "¡Hola, soy tu primera página web con Django!".
¡Felicidades! Acabas de completar tu primer ciclo de desarrollo con Django. Ahora entiendes cómo se conectan las URLs, las vistas y los archivos en un proyecto web.
