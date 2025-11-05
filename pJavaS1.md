Ejercicio: Cambiador de Título al Instante
Este ejercicio usa JavaScript para cambiar el contenido de un título (<h1>) por el texto que el usuario ingrese en un campo de texto, de forma inmediata.
1. 📂 Configuración en VS Code
Necesitarás tu archivo index.html y tu archivo script.js en la misma carpeta.

2. 📝 Código HTML (index.html)
Definiremos los tres elementos clave: el título que va a cambiar, el campo de entrada, y la vinculación a nuestro script.
HTML
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Cambiador de Texto</title>
</head>
<body>
    
    <h1 id="titulo-principal">Escribe algo en la caja de abajo</h1>
    <hr>
    
    <p>Ingresa un nuevo título:</p>
    <input type="text" id="campo-texto" placeholder="Tu nuevo título aquí">

    <script src="script.js"></script>
</body>
</html>

3. 🧩 Código JavaScript (script.js)
Aquí usaremos un "escuchador de eventos" diferente: input, que es perfecto para detectar cambios en campos de texto.
JavaScript
// script.js

// 1. Seleccionar los dos elementos del HTML por su ID
// El elemento que mostrará el nuevo texto (el <h1>)
const titulo = document.getElementById('titulo-principal');

// El elemento que proveerá el nuevo texto (el <input>)
const campoTexto = document.getElementById('campo-texto');

// 2. Definir la función que cambia el texto
function actualizarTitulo() {
    // a. Obtener el texto actual del campo de entrada.
    // La propiedad .value de un <input> contiene lo que el usuario ha escrito.
    const nuevoTexto = campoTexto.value;
    
    // b. Cambiar el texto del título (<h1>).
    // Usamos .textContent para reemplazar el texto dentro de la etiqueta <h1>.
    titulo.textContent = nuevoTexto;
}
// 3. Asignar la función al evento 'input' del campo de texto.
// El evento 'input' se dispara inmediatamente cada vez que el valor del campo cambia.
campoTexto.addEventListener('input', actualizarTitulo);

// Opcional: Establecer un mensaje inicial al cargar la página
// Esto asegura que el campo no esté vacío cuando el usuario inicie
campoTexto.value = "¡Empecemos!";
titulo.textContent = campoTexto.value;


Explicación de las Instrucciones Clave
1.	const campoTexto = document.getElementById('campo-texto');: Seleccionamos el campo de entrada. Este es nuestro origen de datos.
2.	const nuevoTexto = campoTexto.value;: La propiedad clave aquí es .value. En un elemento de entrada (<input>), .value siempre contiene el texto que el usuario ha escrito. Este valor se lee cada vez que se ejecuta la función.
3.	titulo.textContent = nuevoTexto;: Usamos la propiedad .textContent del <h1> para reemplazar su contenido con el nuevoTexto obtenido.
4.	campoTexto.addEventListener('input', actualizarTitulo);: El evento 'input' es la magia. A diferencia de 'click', este evento se dispara automáticamente cada vez que se pulsa una tecla en el campo, creando una sensación de "tiempo real".

4. 🏃 Ejecución
1.	Abre el archivo index.html en tu navegador.
2.	Comienza a escribir en la caja de texto.
3.	Observa cómo el texto del título principal (<h1>) se actualiza inmediatamente con lo que estás escribiendo.
Este ejercicio te enseña la relación fundamental entre lo que el usuario ingresa (.value) y cómo eso modifica lo que se muestra en la página (.textContent).
--


.value y .textContent: La Diferencia Clave
Ambas son propiedades de los elementos HTML que JavaScript puede leer o modificar, pero se usan en contextos diferentes:
Propiedad	Se Usa Principalmente en:	Función (Analogía)	Ejemplo Típico (Elemento HTML)
.value	Elementos de Formulario (Interactivos)	Lo que está dentro de la caja (lo que escribes).	<input>, <textarea>, <select>
.textContent	Elementos de Contenido (Visuales)	Lo que está escrito en el cartel (lo que el usuario ve).	<h1>, <p>, <div>, <span>

📝 Explicación Detallada

1. .value (El Contenido del Usuario)
El término value se traduce como "valor".
•	¿Qué es? Es la información dinámica o editable que un usuario introduce o selecciona en un elemento de formulario.
•	Para Leer: Si quieres saber qué escribió un usuario en un campo de texto, usas miCampo.value.
•	Para Escribir: Si quieres pre-llenar un campo de texto, usas miCampo.value = "Texto predefinido".
•	Analógicamente: Imagina un formulario de pedido. El .value es el texto que has escrito en la casilla de "Nombre" o el número que has elegido en el menú desplegable de "Cantidad".
Ejemplo en Código (Lectura):
JavaScript
// Obtener lo que el usuario escribió
const nombreUsuario = document.getElementById('mi-input').value; 
// nombreUsuario contendrá el texto de la caja

2. .textContent (El Contenido Visible)
El término textContent se refiere al "contenido de texto".
•	¿Qué es? Es todo el texto visible que se encuentra entre la etiqueta de apertura y la etiqueta de cierre de un elemento, ignorando cualquier formato HTML que pudiera haber dentro.
•	Para Leer: Si quieres saber qué dice actualmente tu título, usas miTitulo.textContent.
•	Para Escribir: Si quieres cambiar el texto del título, usas miTitulo.textContent = "Nuevo Texto".
•	Analógicamente: Imagina un letrero o cartel. El .textContent es el texto que está impreso o escrito directamente en ese cartel para que todos lo vean.

Ejemplo en Código (Escritura):
JavaScript
// Cambiar el texto que está dentro de la etiqueta <h1>
document.getElementById('mi-titulo').textContent = "¡Mi nuevo título!"; 
// El <h1> ahora mostrará "¡Mi nuevo título!"

Un Último Ejemplo: El Cambio de Estado
En el último ejercicio que hicimos, el Cambiador de Título al Instante, usamos ambos conceptos:
1.	Lectura con .value: Cuando escribías, JavaScript leía el texto del campo de entrada:
const nuevoTexto = campoTexto.**value**;
2.	Escritura con .textContent: Inmediatamente después, JavaScript escribía ese texto en el encabezado visible:
titulo.**textContent** = nuevoTexto;
Al dominar estas dos propiedades, ya tienes la base para hacer que tus páginas web sean interactivas y respondan a las acciones del usuario. ¡Sigue así!

