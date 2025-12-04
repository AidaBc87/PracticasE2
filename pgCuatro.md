La base de datos es el último componente esencial de una aplicación web, y esta práctica es clave para que los alumnos entiendan cómo funciona una aplicación completa.

## 💾 Práctica 4: Lista de Tareas Pendientes (To-Do List)

Esta práctica introduce los **Modelos (Models)** de Django, que permiten interactuar con una **base de datos SQLite** (incluida en Django), lo que es perfecto para empezar.

-----

### Fase 1: Creación del Modelo (La Base de Datos)

Definiremos qué tipo de datos queremos guardar. En este caso, serán tareas.

#### 1\. Definir la Estructura de la Tarea

  * Abre el archivo: **`saludos/models.py`**
  * Reemplaza el contenido con la definición de la clase `Tarea`:

<!-- end list -->

```python
# saludos/models.py

from django.db import models

class Tarea(models.Model):
    # Campo para guardar la descripción de la tarea (texto)
    descripcion = models.CharField(max_length=200) 
    
    # Campo para indicar si la tarea está completada (verdadero o falso)
    completada = models.BooleanField(default=False) 

    # Esto define cómo se mostrará el objeto en el panel de administrador
    def __str__(self):
        return self.descripcion
```

#### 2\. Crear las Tablas en la Base de Datos

Cada vez que modificas el archivo `models.py`, debes ejecutar dos comandos en la terminal (asegúrate de estar en la carpeta `mi_proyecto`):

1.  **Crear la migración (el "plan" de cambio):**
    ```bash
    python manage.py makemigrations saludos
    ```
2.  **Aplicar la migración (ejecutar el plan en la base de datos):**
    ```bash
    python manage.py migrate
    ```

-----

### Fase 2: Lógica de la Aplicación (CRUD: Crear y Leer)

Necesitamos una vista para mostrar todas las tareas y un formulario para añadir una nueva.

#### 1\. Modificar la Vista (View)

  * Abre el archivo: **`saludos/views.py`**
  * Reemplaza el contenido con el siguiente código que maneja la lógica de la To-Do List:

<!-- end list -->

```python
# saludos/views.py

from django.shortcuts import render, redirect # Importamos 'redirect' para redirigir después de guardar
from .models import Tarea # Importamos nuestra clase Tarea

def lista_tareas(request):
    # Lógica para manejar la adición de una nueva tarea
    if request.method == 'POST':
        # 1. Obtener la descripción del formulario
        descripcion_nueva = request.POST.get('descripcion')
        
        # 2. Crear y guardar un nuevo objeto Tarea en la base de datos
        Tarea.objects.create(descripcion=descripcion_nueva)
        
        # 3. Redirigir a la misma página para ver la lista actualizada
        return redirect('lista_tareas') # El 'name' que definiremos en urls.py

    # Lógica para mostrar la lista
    else:
        # 4. Obtener TODAS las tareas de la base de datos, ordenadas por ID
        todas_las_tareas = Tarea.objects.all().order_by('id')
        
        # 5. Preparar el contexto
        contexto = {
            'tareas': todas_las_tareas
        }
        
        # 6. Renderizar la plantilla
        return render(request, 'saludos/lista.html', contexto)
```

#### 2\. Crear la Plantilla HTML

  * Crea el archivo **`lista.html`** dentro de la carpeta `saludos/templates/saludos/`.

<!-- end list -->

```html
<!DOCTYPE html>
<html>
<head>
    <title>Lista de Tareas Pendientes</title>
    <style>
        body { font-family: sans-serif; background-color: #ffe6e6; padding: 30px; }
        .container { background: white; padding: 30px; border-radius: 10px; max-width: 600px; margin: auto; box-shadow: 0 4px 12px rgba(0,0,0,0.1); }
        h2 { color: #d9534f; }
        ul { list-style: none; padding: 0; }
        li { padding: 10px; border-bottom: 1px solid #eee; display: flex; justify-content: space-between; align-items: center; }
        li:last-child { border-bottom: none; }
        .completada { text-decoration: line-through; color: #aaa; }
    </style>
</head>
<body>
    <div class="container">
        <h2>📋 Mi Lista de Tareas Django</h2>

        <form method="POST">
            {% csrf_token %}
            <input type="text" name="descripcion" placeholder="Escribe una nueva tarea..." required>
            <button type="submit">Añadir Tarea</button>
        </form>

        <hr>

        <ul>
            {% for tarea in tareas %}
                <li class="{% if tarea.completada %}completada{% endif %}">
                    {{ tarea.descripcion }}
                </li>
            {% empty %}
                <li>¡No hay tareas pendientes!</li>
            {% endfor %}
        </ul>
    </div>
</body>
</html>
```

> **Nota Clave:** Los bloques `{% for %}`, `{% endfor %}` y `{% if %}` son constructores lógicos de Django que permiten iterar y tomar decisiones dentro del HTML.

-----

### Fase 3: Conexión URL y Prueba

#### 1\. Mapear la URL

  * Abre el archivo: **`saludos/urls.py`**
  * Modifica el contenido para que apunte a la nueva función, dándole el nombre `lista_tareas`:

<!-- end list -->

```python
# saludos/urls.py

from django.urls import path
from . import views

urlpatterns = [
    # El 'name'='lista_tareas' es el que usamos en el redirect de la vista
    path('', views.lista_tareas, name='lista_tareas'),
]
```

#### 2\. Ejecutar y Probar

  * Asegúrate de que estás en la carpeta `mi_proyecto`.

  * Ejecuta el servidor:

    ```bash
    python manage.py runserver
    ```

  * Abre tu navegador y visita la URL: **`http://127.0.0.1:8000/saludo/`**

**Resultado:** Podrás escribir tareas y ver cómo se añaden a la lista, **persisten** incluso si reinicias el servidor, ya que se están guardando en la base de datos.

### 💡 Desafío para el Alumno (CRUD Completo)

Para un desafío real, pídeles que añadan la funcionalidad para **marcar una tarea como completada (Update)**:

1.  Añadir un botón o checkbox junto a cada tarea en `lista.html`.
2.  Crear una nueva URL en `saludos/urls.py` (ej: `path('completar/<int:tarea_id>/', views.completar_tarea, name='completar_tarea')`). El `<int:tarea_id>` captura el ID de la tarea a actualizar.
3.  Crear la función `completar_tarea` en `saludos/views.py` que:
      * Busque la tarea por su ID: `tarea = Tarea.objects.get(id=tarea_id)`
      * Cambie el estado: `tarea.completada = True`
      * Guarde el cambio: `tarea.save()`
      * Redirija a la lista: `return redirect('lista_tareas')`

Con esta práctica, han tocado los 4 pilares de Django: **URLs, Vistas, Plantillas y Modelos**.
