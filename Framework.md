¿Qué es un framework?
Imagina que quieres construir una casa. Puedes empezar desde cero: cavar los cimientos, mezclar cemento, cortar cada ladrillo, etc. Esto toma mucho tiempo y esfuerzo.
Ahora, imagina que tienes un kit de construcción que ya incluye los planos, una estructura prefabricada, y herramientas especializadas. Este kit te permite concentrarte en los detalles únicos de tu casa (diseño interior, colores, etc.) en lugar de las tareas básicas.
En programación, un framework (marco de trabajo) es ese "kit de construcción". Es una estructura predefinida, un conjunto de herramientas, librerías y convenciones que te dan una base sólida para desarrollar software. Te ayuda a ser más rápido, eficiente y a seguir las mejores prácticas de la industria.
________________________________________
Diferencias entre librerías y frameworks
Esta es una de las preguntas más comunes. Piensa en la dirección del control.
•	Librería: Tú controlas la librería. Cuando la necesitas, llamas a una de sus funciones para que haga algo específico. Por ejemplo, una librería para manipular imágenes. Tú decides cuándo y cómo usarla. Es como ir a una ferretería y comprar una sierra. Tú la usas cuando la necesitas.
•	Framework: El framework te controla a ti. Él decide cuándo y qué funciones de tu código se ejecutan. El framework define la estructura de tu proyecto y tú "llenas los huecos" con tu lógica de negocio. Es como un guion de película; el director (el framework) tiene la trama principal, y tú (el programador) escribes los diálogos (el código) en los lugares que él te indica.
________________________________________
Tipos de frameworks según el dominio
Los frameworks están diseñados para tipos específicos de proyectos.
•	Frontend: Se centran en la interfaz de usuario y lo que el usuario ve en su navegador. Ejemplos: React, Angular y Vue.js. Se encargan de la interactividad, la presentación de datos y la experiencia visual.
•	Backend: Manejan la lógica del servidor, la base de datos, la seguridad y la autenticación. Ejemplos: Django (Python), Ruby on Rails (Ruby) y Express.js (Node.js). Son la "cocina" del sitio web; todo lo que sucede detrás de cámaras.
•	Móvil: Se usan para crear aplicaciones para celulares. Ejemplos: Flutter (para Android y iOS) y React Native (para Android y iOS).
•	Datos: Están orientados al análisis de datos y aprendizaje automático. Ejemplos: TensorFlow y PyTorch.
________________________________________
Selección adecuada de un framework: El caso de Django
Elegir un framework es como elegir la herramienta adecuada para un trabajo. Para un proyecto web de backend, Django es una excelente opción. ¿Por qué?
•	Es robusto y seguro: Lo usan empresas como Instagram, Spotify y Pinterest. Su seguridad integrada es una de sus mayores fortalezas.
•	Es un "kit completo" (baterías incluidas): Django viene con muchas funcionalidades ya listas para usar, como un panel de administración, un ORM (para interactuar con la base de datos sin escribir SQL puro) y un sistema de enrutamiento.
•	Favorece el desarrollo rápido: Te ayuda a construir aplicaciones funcionales en muy poco tiempo, siguiendo el principio de "convención sobre configuración". Esto significa que ya tiene un camino establecido para la mayoría de las tareas, y si lo sigues, todo funciona sin que tengas que configurarlo manualmente.
________________________________________
Arquitectura interna de un framework (Django)
Django sigue el patrón de diseño MVT (Model-View-Template), que es una variación del famoso MVC (Model-View-Controller).
•	Modelo (Model): Es el cerebro de los datos. Define la estructura de tu base de datos (tablas, campos, relaciones). Representa la información de tu aplicación. Por ejemplo, un modelo Usuario con campos como nombre, email y contraseña.
•	Vista (View): Es la lógica de negocio. Recibe una petición del usuario, interactúa con el Modelo para obtener o modificar datos, y decide qué información enviar a la plantilla. Es como el mesero que toma tu pedido (la petición) y le pide a la cocina (el Modelo) que prepare la comida (los datos).
•	Plantilla (Template): Es la presentación. Es un archivo HTML con "marcadores de posición" que la Vista llena con los datos del Modelo. Es la página web que el usuario ve en su navegador.
________________________________________
Estructura de directorios típica de un proyecto Django
Cuando creas un proyecto con Django, él te da una estructura base que debes respetar. Esto es parte de la "convención sobre configuración".
mi_proyecto/
├── manage.py              # Herramienta de línea de comandos para administrar el proyecto.
├── mi_proyecto/           # Directorio principal del proyecto.
│   ├── __init__.py        # Indica que es un paquete de Python.
│   ├── settings.py        # Archivo de configuración global.
│   ├── urls.py            # Mapea las URLs a las Vistas.
│   └── wsgi.py            # Interfaz para el servidor web.
├── mi_app/                # Una "app" es un módulo reutilizable dentro de tu proyecto.
│   ├── migrations/        # Archivos que gestionan los cambios en la base de datos.
│   ├── __init__.py
│   ├── admin.py           # Registra tus modelos en el panel de administración.
│   ├── apps.py
│   ├── models.py          # Aquí defines tus Modelos (tablas de la base de datos).
│   ├── tests.py           # Aquí escribes tus pruebas.
│   └── views.py           # Aquí defines tus Vistas (lógica de negocio).
└── templates/             # Aquí se guardan los archivos HTML (Plantillas).
Entender esta estructura es el primer paso para dominar Django. Con esta base, puedes empezar a construir tu propio software, aprovechando el poder y la eficiencia de los frameworks.
________________________________________ ________________________________________ ________________________________________ ________________________________________ ________________________________________

1. Introducción a Python: Los cimientos de Django
Antes de usar un framework, necesitas conocer el lenguaje en el que está construido. Python es un lenguaje de programación de propósito general, conocido por ser fácil de leer y escribir. 

2. El Entorno de Desarrollo para Django
Creación del Entorno Virtual (¡Esencial!)
Imagina que tienes varios proyectos de programación en tu computadora. Cada uno necesita versiones diferentes de librerías. Si las instalas todas en el mismo lugar, podrían entrar en conflicto. Un entorno virtual crea un espacio aislado para cada proyecto. Es como tener una caja de herramientas separada para cada uno.
Pasos:
1.	Abre tu terminal o línea de comandos.
2.	Crea un nuevo directorio para tu proyecto:
mkdir mi_proyecto_django
3.	Entra en el directorio:
cd mi_proyecto_django
4.	Crea el entorno virtual (la "caja"):
python -m venv venv
5.	Activa el entorno virtual (ponte los guantes de la "caja" para trabajar):
o	En Windows: venv\Scripts\activate
o	En macOS/Linux: source venv/bin/activate

Instalación de Django
Una vez que el entorno virtual está activo, las librerías que instales solo se guardarán en esta "caja".
•	Instala Django usando pip, el gestor de paquetes de Python:
pip install django
________________________________________

3. Creación y Configuración del Proyecto
Comandos Esenciales
Aquí tienes los comandos más importantes que usarás con Django.
•	Para crear un nuevo proyecto: django-admin startproject <nombre_del_proyecto>
•	Para crear una nueva aplicación dentro de tu proyecto: python manage.py startapp <nombre_de_la_app>
•	Para migrar la base de datos (crear tablas): python manage.py migrate
•	Para ejecutar el servidor de desarrollo: python manage.py runserver
•	Para crear un superusuario (admin): python manage.py createsuperuser

Creación del Proyecto y Ejecución del Servidor
1.	Asegúrate de estar en el directorio de tu proyecto y con el entorno virtual activo.
2.	Crea el proyecto:
django-admin startproject mi_proyecto_web . (El punto . crea el proyecto en el directorio actual).
3.	Ejecuta el servidor de desarrollo:
python manage.py runserver
Verás que el servidor se inicia en la dirección http://127.0.0.1:8000/. Abre esta URL en tu navegador y verás la página de bienvenida de Django.

Archivos Clave
•	settings.py: Es el archivo de configuración global de tu proyecto. Aquí defines la base de datos, las aplicaciones instaladas, las rutas de las plantillas y archivos estáticos, etc.
•	urls.py: Es el mapa de tu sitio web. Aquí defines las rutas (URLs) que los usuarios pueden visitar y qué función (vista) de tu código debe manejar cada una de esas rutas.
________________________________________

4. Creación de una Aplicación (App)
Un proyecto de Django se divide en aplicaciones (apps) que son módulos reutilizables. Cada app tiene su propia lógica. Por ejemplo, una app para el blog, una para la tienda, etc.
1.	Crea una app (asegúrate de estar en el directorio principal):
python manage.py startapp blog
2.	Registra la app en settings.py agregándola a la lista INSTALLED_APPS.

Archivos de la App
•	models.py: Aquí defines tus modelos de datos. Por ejemplo, un modelo Post para tu blog, con campos como titulo, contenido y fecha.
•	views.py: Aquí escribes la lógica de tu aplicación. Una vista recibe una solicitud web y devuelve una respuesta, como una página HTML.
•	urls.py: Debes crear este archivo manualmente dentro de tu app (blog/urls.py). Servirá para mapear las URLs específicas de tu blog a las vistas correspondientes. Luego lo "incluyes" en el urls.py principal del proyecto.
•	admin.py: Aquí registras tus modelos para que aparezcan en el panel de administración de Django, que es muy útil para gestionar tus datos.

Carpetas Especiales
Para que Django funcione correctamente, debes crear carpetas específicas con estos nombres dentro de tu aplicación:
•	templates/: Aquí se guardan los archivos HTML de tu proyecto. Django busca automáticamente las plantillas en esta carpeta.
•	static/: Aquí se guardan los archivos CSS, JavaScript e imágenes que no cambian (archivos estáticos).
•	media/: Aquí se guardan los archivos que los usuarios suben (como fotos de perfil).
Con esta estructura, ya estás listo para empezar a construir tu primera aplicación web con Django. El siguiente paso es escribir tu primer código en los archivos que acabas de crear.

________________________________________ ________________________________________ ________________________________________ ________________________________________ ________________________________________

Práctica 1: Configuración del Entorno Virtual y Creación del Proyecto Básico
Objetivo: Aprender a usar la terminal integrada de VS Code para crear y configurar un entorno de desarrollo.

Paso 1: Abrir VS Code y la Terminal
1.	Abre Visual Studio Code.
2.	Ve a Archivo > Abrir Carpeta y crea una carpeta vacía para tu proyecto (por ejemplo, mi_proyecto_django). Selecciona esa carpeta.
3.	Abre la terminal integrada de VS Code. Puedes hacerlo yendo al menú superior a Terminal > Nueva Terminal o usando el atajo de teclado: Ctrl + Ñ (en Windows) o Ctrl + Shift + ~ (en Mac). La terminal se abrirá en la parte inferior de la ventana, ya ubicada en la carpeta que abriste.

Paso 2: Crear y Activar el Entorno Virtual
1.	En la terminal, crea el entorno virtual (la "caja de herramientas" aislada):
python -m venv venv
Esto creará una carpeta llamada venv en tu proyecto.
2.	Activa el entorno virtual. ¡Esto es crucial!
o	En Windows:
venv\Scripts\activate
o	En macOS/Linux:
source venv/bin/activate
3.	Verás que el nombre de tu entorno ((venv)) aparece al inicio de la línea de comandos, indicando que está activo.

Paso 3: Instalar Django y Crear el Proyecto
1.	Con el entorno virtual activo, instala Django:
pip install django
Esto descargará e instalará todas las librerías necesarias.
2.	Ahora, crea tu proyecto Django. El punto (.) es importante para que los archivos se creen en la carpeta actual:
django-admin startproject mi_blog .
Verás que se generan varias carpetas y archivos en tu explorador de archivos de VS Code.

Paso 4: Ejecutar el Servidor
1.	En la misma terminal, ejecuta el servidor de desarrollo de Django:
python manage.py runserver
Verás un mensaje que te indica que el servidor se está ejecutando en http://127.0.0.1:8000/.
2.	Abre esa dirección en tu navegador. Si todo ha ido bien, verás la página de bienvenida de Django, un cohete despegando.
3.	Para detener el servidor, regresa a la terminal y presiona Ctrl + C.

________________________________________ ________________________________________ ________________________________________ ________________________________________ ________________________________________

Práctica 2: Creación de la Aplicación y una Primera Página
Objetivo: Crear una aplicación, definir una vista y un urls.py para mostrar tu primera página web.

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
Bash
python manage.py runserver
3.	Ve a http://127.0.0.1:8000/ en tu navegador. En lugar del cohete de Django, ahora deberías ver el mensaje: "¡Hola, soy tu primera página web con Django!".

