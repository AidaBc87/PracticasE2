Siguiente paso: **Crear una Plantilla HTML Básica**. 🎨

-----

## 🎨 Paso 9: Usar Plantillas (Templates) para HTML

En Django, una **Plantilla** es un archivo HTML que tiene marcadores especiales de Django.

### A. Crear la Carpeta de Plantillas

1.  **Crea una Carpeta:** Dentro de la carpeta de tu aplicación (`app_principal/`), crea una nueva carpeta llamada **`templates`**.

2.  **Crea una Subcarpeta:** Dentro de **`templates/`**, crea otra carpeta con el mismo nombre de tu aplicación, **`app_principal`**.

      * **Estructura de Carpetas (Deberías tener):**
        ```
        app_principal/
        ├── templates/
        │   └── app_principal/
        │       └── (aquí irá el archivo HTML)
        ├── views.py
        └── urls.py
        ```

### B. Crear el Archivo HTML de la Plantilla

1.  **Crear el Archivo:** Dentro de la carpeta `app_principal/templates/app_principal/`, crea un nuevo archivo llamado **`inicio.html`**.

2.  **Pegar el Siguiente Código en `inicio.html`:**

    ```html
    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <title>Mi Página Principal</title>
        <style>
            body { font-family: sans-serif; text-align: center; margin-top: 50px; background-color: #f4f4f9; }
            h1 { color: #007bff; }
            p { font-size: 1.2em; }
        </style>
    </head>
    <body>
        <h1>¡Bienvenido a la Web de Django!</h1>
        <p>Esta página fue creada usando una plantilla HTML.</p>
        <p>¡El siguiente paso es añadir una imagen!</p>
    </body>
    </html>
    ```

### C. Modificar la Vista para Usar la Plantilla

Ahora, cambia la función de la Vista para que cargue y muestre este archivo HTML en lugar del simple texto.

1.  **Abrir `app_principal/views.py`** y modificarlo:

    ```python
    from django.shortcuts import render # Importamos la función render

    # Esta función ahora usa render para cargar la plantilla
    def hello_world(request):
        # La función render busca 'app_principal/inicio.html'
        # en las carpetas de 'templates' que configuramos en el Paso 6.
        return render(request, 'app_principal/inicio.html') 
    ```

### D. Ver el Resultado

1.  **Ejecutar el Servidor:** Si lo detuviste, vuelve a la terminal y ejecuta:

    ```bash
    python manage.py runserver
    ```

2.  **Ver tu Página:** Ve a `http://127.0.0.1:8000/`.

    **Resultado Esperado:** Ahora verás una página con un **título grande, texto centrado y un fondo de color** gracias al código HTML y CSS de tu plantilla.

-----

**Siguiente Reto:** ¿Quieres aprender a usar la base de datos de Django para guardar información, como un listado de tareas? 💾
¡Claro\! El siguiente ejercicio fundamental en Django es **trabajar con la base de datos** para crear una aplicación funcional, como una lista de tareas (To-Do List). Esto involucra los conceptos de **Modelos** y el panel de **Administración** de Django. 💾

Aquí tienes el reto: **Crear un Modelo y Acceder al Panel de Administración.**

-----

## 💾 Paso 10: Configurar la Base de Datos

Django usa por defecto **SQLite**, que es una base de datos ligera que no requiere instalación adicional.

1.  **Ejecutar Migraciones:** Las *migraciones* son comandos que le dicen a Django que configure la base de datos con las tablas iniciales que necesita el *framework*.
    Asegúrate de estar en el directorio `MiProyectoDjango/` con el entorno virtual activado y ejecuta:
    ```bash
    python manage.py migrate
    ```
    *Verás muchos mensajes de `OK` a la derecha. Esto creó el archivo `db.sqlite3` en tu carpeta.*

-----

## 👤 Paso 11: Crear un Superusuario (Administrador)

Necesitas una cuenta para acceder al panel de administración de Django, donde podrás gestionar los datos de tu aplicación.

1.  **Crear Superusuario:** Ejecuta el siguiente comando y sigue las instrucciones (te pedirá un nombre de usuario, email y contraseña):

    ```bash
    python manage.py createsuperuser
    ```

      * **Recomendación:** Usa `admin` como nombre de usuario y una contraseña simple para este ejercicio.\*

2.  **Verificar el Panel de Administración:**

      * Ejecuta el servidor: `python manage.py runserver`
      * Abre tu navegador y ve a la dirección: `http://127.0.0.1:8000/admin/`
      * Ingresa con las credenciales que acabas de crear. ¡Verás el panel de administración de Django\!

-----

## 📋 Paso 12: Crear el Modelo (La Estructura de Datos)

Un **Modelo** es una clase de Python que representa una tabla en la base de datos. Definiremos la estructura para una Tarea.

1.  **Abrir `app_principal/models.py`** y pega el siguiente código:

    ```python
    from django.db import models

    # Definimos la tabla Tarea
    class Tarea(models.Model):
        # Campos de la tabla:
        
        # Un campo de texto corto, obligatorio
        titulo = models.CharField(max_length=200) 
        
        # Un campo booleano (verdadero/falso)
        completada = models.BooleanField(default=False) 
        
        # Método que define cómo se muestra el objeto en el Admin
        def __str__(self):
            return self.titulo
    ```

-----

## 🔄 Paso 13: Migrar el Nuevo Modelo

Cada vez que cambies el archivo `models.py`, debes decirle a Django que actualice la base de datos en dos pasos:

1.  **Crear la Migración:** Le dice a Django cómo actualizar la base de datos.

    ```bash
    python manage.py makemigrations app_principal
    ```

    *Verás un mensaje diciendo que se creó un archivo de migración.*

2.  **Aplicar la Migración:** Ejecuta los cambios en la base de datos real.

    ```bash
    python manage.py migrate
    ```

    *Verás un mensaje de `OK` en `app_principal`.*

-----

## 🛠️ Paso 14: Registrar el Modelo en el Panel de Administración

Para que puedas agregar y modificar tareas usando el panel que acabas de ver, debes registrar tu modelo.

1.  **Abrir `app_principal/admin.py`** y edítalo de esta manera:

    ```python
    from django.contrib import admin
    from .models import Tarea # Importa el modelo Tarea que creaste

    # Registra el modelo para que aparezca en el panel de administración
    admin.site.register(Tarea)
    ```

-----

## ✅ Paso 15: Probar y Agregar Datos

1.  **Ejecutar el Servidor:** `python manage.py runserver`
2.  **Acceder al Admin:** Ve a `http://127.0.0.1:8000/admin/` e inicia sesión.
3.  **Ver tu Modelo:** Ahora verás una sección llamada **App Principal** y dentro el enlace **Tareas**.
4.  **Agregar una Tarea:**
      * Haz clic en **"Añadir Tarea"** (o "Add Tarea").
      * Escribe un **título** (ej: "Estudiar Django").
      * Deja **Completada** sin marcar.
      * Haz clic en **"Guardar"**.
      * Repite y añade una segunda tarea, marcando esta vez **Completada**.

¡Felicidades\! Has creado tu primer modelo de base de datos y has gestionado datos usando el panel de administración de Django.

El siguiente paso sería **mostrar esas tareas en la página web** que creaste con la plantilla. ¿Quieres continuar?
