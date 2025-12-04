**Formularios** y la captura de datos del usuario.

## 📝 Práctica 3: Generador de Carta de Presentación Simple

Esta práctica enseña a los estudiantes cómo usar formularios HTML para capturar datos y cómo procesar esos datos en Python (Django) para generar una respuesta dinámica.

-----

### Fase 1: Configuración de Plantillas y Vistas

Asumiremos que ya tienes el proyecto base (`mi_proyecto`) y la aplicación (`saludos`) de las prácticas anteriores.

#### 1\. Crear la Plantilla del Formulario

Esta plantilla tendrá el formulario para que el estudiante ingrese sus datos.

  * Crea el archivo **`formulario.html`** dentro de la carpeta `saludos/templates/saludos/`.

<!-- end list -->

```html
<!DOCTYPE html>
<html>
<head>
    <title>Generador de Carta</title>
    <style>
        body { font-family: sans-serif; background-color: #e6f7ff; padding: 20px; }
        .container { background: white; padding: 25px; border-radius: 8px; max-width: 500px; margin: auto; box-shadow: 0 4px 8px rgba(0,0,0,0.1); }
        h2 { color: #007bff; }
        label { display: block; margin-top: 10px; font-weight: bold; }
        input[type="text"] { width: 95%; padding: 8px; margin-top: 5px; border: 1px solid #ccc; border-radius: 4px; }
        button { background-color: #007bff; color: white; padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; margin-top: 20px; }
    </style>
</head>
<body>
    <div class="container">
        <h2>🛠️ Crea tu Carta de Presentación</h2>
        <form method="post">
            {% csrf_token %} 
            
            <label for="nombre">Tu Nombre Completo:</label>
            <input type="text" id="nombre" name="nombre" required>

            <label for="carrera">Carrera o Puesto al que Aspiras:</label>
            <input type="text" id="carrera" name="carrera" required>
            
            <button type="submit">Generar Carta</button>
        </form>
    </div>
</body>
</html>
```

> **Nota Clave:** La etiqueta `{% csrf_token %}` es fundamental en Django por seguridad. El atributo `method="post"` indica que se enviarán datos al servidor.

-----

### Fase 2: Lógica de la Aplicación (Manejo del Formulario)

Modificaremos la vista para que pueda manejar dos situaciones:

1.  **GET:** Mostrar el formulario vacío por primera vez.
2.  **POST:** Recibir y procesar los datos enviados por el usuario.

#### 1\. Modificar la Vista (View)

  * Abre el archivo: **`saludos/views.py`**
  * Reemplaza el contenido con la siguiente función:

<!-- end list -->

```python
# saludos/views.py

from django.shortcuts import render

def generador_carta(request):
    # 1. Verificar el método de solicitud: ¿Es GET o POST?
    
    if request.method == 'POST':
        # Si es POST, significa que el usuario envió el formulario
        
        # Obtener los datos del formulario (el 'name' de los inputs)
        nombre = request.POST.get('nombre') 
        carrera = request.POST.get('carrera')
        
        # 2. Lógica para generar la carta
        carta_generada = f"""
        Estimado/a Reclutador/a,
        
        Me dirijo a usted con gran entusiasmo para expresar mi interés en la posición de **{carrera}**. 
        
        Aunque soy un estudiante, mi nombre es **{nombre}** y estoy comprometido/a a aplicar mis conocimientos y mi deseo de aprender en su equipo.
        
        Espero tener la oportunidad de discutir cómo mis habilidades pueden beneficiar a su organización.
        
        Atentamente,
        {nombre}
        """
        
        # 3. Preparar el contexto para la plantilla de RESULTADO
        contexto = {
            'carta': carta_generada.replace('\n', '<br>'), # Reemplazamos saltos de línea por <br> para HTML
            'nombre_user': nombre
        }
        
        # Renderizar una plantilla de resultado, no la del formulario
        return render(request, 'saludos/resultado.html', contexto)

    else:
        # Si es GET, significa que es la primera vez que se visita la página
        # Simplemente muestra la plantilla del formulario
        return render(request, 'saludos/formulario.html')
```

#### 2\. Crear la Plantilla de Resultados

Ahora necesitamos una plantilla para mostrar la carta generada.

  * Crea el archivo **`resultado.html`** dentro de la carpeta `saludos/templates/saludos/`.

<!-- end list -->

```html
<!DOCTYPE html>
<html>
<head>
    <title>Carta Generada</title>
    <style>
        body { font-family: sans-serif; background-color: #f7e6ff; padding: 20px; }
        .container { background: white; padding: 30px; border-radius: 8px; max-width: 700px; margin: auto; box-shadow: 0 4px 8px rgba(0,0,0,0.1); }
        h2 { color: #8e44ad; }
        .carta-box { border: 1px solid #ccc; padding: 20px; white-space: pre-wrap; margin-top: 15px; background-color: #f9f9f9; text-align: left; }
    </style>
</head>
<body>
    <div class="container">
        <h2>🎉 ¡Carta Generada con Éxito, {{ nombre_user }}!</h2>
        <div class="carta-box">
            <p>{{ carta|safe }}</p> 
        </div>
        <a href="/saludo/">Generar otra carta</a>
    </div>
</body>
</html>
```

> **Nota Clave:** El filtro `|safe` le dice a Django que el contenido de `carta` es "seguro" y que no debe escapar el código HTML (`<br>`) que introdujimos en la vista.

-----

### Fase 3: Conexión URL y Prueba

#### 1\. Mapear la URL

  * Abre el archivo: **`saludos/urls.py`**
  * Modifica el contenido para que apunte a la nueva función:

<!-- end list -->

```python
# saludos/urls.py

from django.urls import path
from . import views

urlpatterns = [
    # Esta URL manejará tanto la visualización del formulario (GET) como el envío (POST)
    path('', views.generador_carta, name='generador_carta'),
]
```

#### 2\. Ejecutar y Probar

  * Asegúrate de que estás en la carpeta `mi_proyecto`.

  * Ejecuta el servidor:

    ```bash
    python manage.py runserver
    ```

  * Abre tu navegador y visita la URL: **`http://127.0.0.1:8000/saludo/`**

**Resultado:**

1.  Verás el formulario.
2.  Al llenarlo y hacer clic en **"Generar Carta"**, verás una nueva página con la carta dinámica.

### 💡 Desafío para el Alumno

Para llevarlo un paso más allá, pídeles que añadan otro campo al formulario, por ejemplo:

1.  Un campo llamado **"Empresa"**.
2.  Modificar la vista (`views.py`) para capturar este nuevo dato (`request.POST.get('empresa')`).
3.  Modificar la carta generada para incluir el nombre de la empresa.

¿Quieres una práctica final que incorpore modelos y bases de datos (aunque muy sencilla)?
