## Activar los Script en Windows
1.  Ejecutar como administrador el **PowerShell**
2.  Escribir el comando: Set-ExecutionPolicy RemoteSigned y presiona `Enter`
3.  Luego Escribir: S y presiona `Enter`
4.  Escribe: exit y presiona `Enter`

## 🚀 1. Configuración Inicial (¡Solo por Primera Vez\!)
Antes de empezar, asegúrate de tener **Python 3** instalado en tu computadora.

### A. Verificar la Instalación de Python
1.  Abre el **Símbolo del Sistema (CMD)** o **PowerShell**.
2.  Escribe el siguiente comando y presiona `Enter`:
    python --version
    Deberías ver un número de versión (ej. `Python 3.10.6`). Si obtienes un error, necesitas instalar Python primero.

### B. Crear la Carpeta del Proyecto
1.  En la misma ventana de comandos, navega hasta una ubicación donde quieras guardar tus proyectos (por ejemplo, el escritorio o una carpeta de documentos). Puedes usar el comando `cd` (Change Directory).
   *Ejemplo:*
    cd C:\Users\TuUsuario\Desktop
2.  Crea la carpeta de tu proyecto y entra en ella:
    mkdir proyecto_django_win
    cd proyecto_django_win
-----

## 🐍 2. Entorno Virtual e Instalación de Django
Es una **buena práctica** aislar los archivos de Django de tu instalación principal de Python.

### A. Crear el Entorno Virtual
1.  Crea un entorno virtual llamado `venv`:
    python -m venv venv

### B. Activar el Entorno Virtual
1.  **Activa** el entorno (notarás que aparece `(venv)` al inicio de tu línea de comandos):
    .\venv\Scripts\activate

### C. Instalar Django
1.  Una vez activado el entorno, instala Django usando `pip` (el gestor de paquetes de Python):
   pip install django
*Espera a que termine la instalación. ¡Ya tienes Django\!*

## 🛠️ 3. Crear el Proyecto Base y la Aplicación
En Django, un **Proyecto** es la configuración global, y una **Aplicación** (`App`) es un módulo con funcionalidades específicas (ej. "Blog", "Usuarios").

### A. Crear el Proyecto Django
1.  Asegúrate de estar en la carpeta principal (`proyecto_django_win`). Ejecuta el comando para crear la estructura del proyecto:
    django-admin startproject mi_sitio .
`
      * El comando crea la configuración base llamada `mi_sitio`.
      * El punto (`.`) es importante para que los archivos se creen en la carpeta actual.

### B. Crear la Aplicación "Hello World"
1.  Ahora, crea tu primera aplicación llamada `principal`:
    python manage.py startapp principal

    *Se creará una nueva carpeta llamada `principal` con archivos esenciales.*

## 🧩 4. Configurar la Aplicación (El **Mínimo Necesario**)
Para que Django sepa que existe tu nueva App, debes registrarla y definir qué mostrará.

### A. Registrar la Aplicación
1.  Abre la carpeta del proyecto en **VS Code** (escribe `code .` en la terminal para abrirlo rápidamente).
2.  Abre el archivo de configuración: **`mi_sitio/settings.py`**.
3.  Busca la lista `INSTALLED_APPS` y **añade** el nombre de tu aplicación (`'principal'`) al final:
    ```python
    # mi_sitio/settings.py

    INSTALLED_APPS = [
        # ... otras apps de Django
        'django.contrib.staticfiles',
        'principal',  # <--- ¡Añade tu app aquí!
    ]
    ```

### B. Definir la Vista (`View`)
La **Vista** es una función que procesa una solicitud y devuelve una respuesta.
1.  Abre el archivo: **`principal/views.py`**.
2.  Modifícalo para que devuelva un simple "Hola Mundo":
    ```python
    # principal/views.py
    from django.http import HttpResponse

    def saludo_principal(request):
        """Devuelve un saludo simple como respuesta HTTP."""
        return HttpResponse("<h1>¡Hola, Bachillerato! Este es tu primer Django con Windows.</h1>")
    ```

### C. Definir las Rutas (`URLs`) de la Aplicación
Necesitas decirle a la aplicación qué URL ejecutará la función `saludo_principal`.
1.  Dentro de la carpeta **`principal`**, crea un **nuevo archivo** llamado **`urls.py`**.
2.  Pega el siguiente código en el nuevo archivo:
    ```python
    # principal/urls.py
    from django.urls import path
    from . import views

    urlpatterns = [
        # La ruta principal de la app (la URL vacía '') ejecutará views.saludo_principal
        path('', views.saludo_principal, name='inicio'),
    ]
    ```
### D. Conectar las Rutas al Proyecto Global
Finalmente, dile al proyecto principal que use las rutas de tu aplicación.
1.  Abre el archivo **`mi_sitio/urls.py`** (el de la carpeta de configuración).
2.  Importa la función `include` y añade una ruta que apunte a las URLs de tu App:

    ```python
    # mi_sitio/urls.py
    from django.contrib import admin
    from django.urls import path, include # <--- Importa 'include'

    urlpatterns = [
        path('admin/', admin.site.urls),
        # Cuando alguien entre a http://127.0.0.1:8000/, irá a principal.urls
        path('', include('principal.urls')), 
    ]
    ```

## 🌐 5. Ejecutar el Proyecto
### A. Ejecutar el Servidor
1.  Vuelve al **Símbolo del Sistema** (asegúrate de que `(venv)` esté activo y de estar en la carpeta `proyecto_django_win`).
2.  Ejecuta el servidor de desarrollo:
    python manage.py runserver

### B. Ver el Resultado
1.  Abre tu navegador web.
2.  Accede a la dirección que te indica el terminal: **`http://127.0.0.1:8000/`**
3.  **¡Éxito\!** Deberías ver tu mensaje de **"Hola, Bachillerato..."**

Para detener el servidor, presiona `Ctrl + C` en la ventana del terminal.

