Las **Plantillas (Templates)**.

Esta práctica sigue siendo adecuada para bachillerato, pero introduce un nivel más avanzado de estructura web.

## 🌟 Práctica 2: Generador de Frases Motivacionales

El objetivo es crear una página que muestre frases motivacionales y use una plantilla HTML para el diseño.

-----

### Fase 1: Preparación de la Aplicación

Si los alumnos completaron la práctica anterior, ya tienen la estructura base (`mi_proyecto` y la app `saludos`). Seguiremos trabajando en la app `saludos`.

#### 1\. Crear la Carpeta de Plantillas

Django busca los archivos HTML (plantillas) en una subcarpeta específica dentro de cada aplicación.

  * Dentro de la carpeta `saludos/`, crea una nueva carpeta llamada **`templates`**.
  * Dentro de la carpeta `templates/`, crea otra carpeta llamada **`saludos`** (esto es una buena práctica para evitar conflictos).

Estructura deseada: `mi_proyecto/saludos/templates/saludos/`

#### 2\. Crear la Plantilla HTML

Ahora creamos el archivo HTML que servirá como nuestra página web.

  * Crea el archivo **`frase.html`** dentro de la última carpeta (`saludos/templates/saludos/`).

<!-- end list -->

```html
<!DOCTYPE html>
<html>
<head>
    <title>Frase Motivacional</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f4f9;
            padding: 50px;
        }
        .container {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            max-width: 600px;
            margin: auto;
        }
        h2 {
            color: #333;
        }
        .frase {
            font-size: 1.5em;
            color: #5cb85c;
            margin-top: 20px;
            font-style: italic;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>✨ La Frase del Día ✨</h2>
        <p class="frase">"{{ frase_elegida }}"</p> 
        <p>— Generado por tu aplicación Django</p>
    </div>
</body>
</html>
```

> **Nota clave:** La sintaxis `{{ frase_elegida }}` es el **Lenguaje de Plantillas de Django (DTL)**, y permite inyectar datos dinámicos desde Python.

-----

### Fase 2: Lógica de la Aplicación (La Vista)

Ahora modificaremos la vista para que seleccione una frase al azar y la envíe a la plantilla HTML.

#### 1\. Modificar la Vista (View)

  * Abre el archivo: **`saludos/views.py`**
  * Reemplaza la función anterior con el siguiente código:

<!-- end list -->

```python
# saludos/views.py

from django.shortcuts import render # Importamos la función para renderizar plantillas
import random # Lo usaremos para elegir una frase al azar

def generar_frase(request):
    # 1. Lista de frases que la app puede mostrar
    frases = [
        "El éxito es la suma de pequeños esfuerzos repetidos día tras día.",
        "No te rindas, cada dificultad es una oportunidad disfrazada.",
        "Cree en ti mismo y todo será posible.",
        "La mejor forma de predecir el futuro es creándolo.",
        "Tu actitud, no tu aptitud, determinará tu altitud."
    ]

    # 2. Elegir una frase al azar de la lista
    frase_seleccionada = random.choice(frases)

    # 3. Preparar los datos que enviaremos a la plantilla
    contexto = {
        'frase_elegida': frase_seleccionada,
    }

    # 4. Renderizar (dibujar) la plantilla 'saludos/frase.html'
    #    y enviarle los datos guardados en 'contexto'
    return render(request, 'saludos/frase.html', contexto)
```

-----

### Fase 3: Conexión URL y Prueba

#### 1\. Mapear la URL

Actualiza el archivo de URLs de la aplicación para que la URL principal ejecute esta nueva función.

  * Abre el archivo: **`saludos/urls.py`**
  * Modifica el contenido para que apunte a `generar_frase`:

<!-- end list -->

```python
# saludos/urls.py

from django.urls import path
from . import views

urlpatterns = [
    # Cuando la URL esté vacía (''), ejecuta la nueva función views.generar_frase
    path('', views.generar_frase, name='generar_frase'),
]
```

#### 2\. Ejecutar y Probar

  * Asegúrate de que estás en la carpeta `mi_proyecto`.

  * Ejecuta el servidor:

    ```bash
    python manage.py runserver
    ```

  * Abre tu navegador y visita la URL: **`http://127.0.0.1:8000/saludo/`**

**Resultado:** ¡Verás la plantilla HTML estilizada y una frase motivacional diferente cada vez que recargues la página\!

-----

### 💡 Desafío para el Alumno (Opcional)

Pídeles que intenten **enviar la hora actual** a la plantilla:

1.  En `saludos/views.py`, importa `datetime` y añade la hora al contexto:
    ```python
    import datetime
    # ...
    contexto = {
        'frase_elegida': frase_seleccionada,
        'hora_actual': datetime.datetime.now().strftime("%H:%M:%S")
    }
    # ...
    ```
2.  En `saludos/templates/saludos/frase.html`, añaden una línea para mostrarla:
    ```html
    <p>Hora de generación: **{{ hora_actual }}**</p>
    ```

