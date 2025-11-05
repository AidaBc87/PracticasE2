Recordando Python

-----

## 💻 Práctica: Generador de Biografías Digitales

El objetivo es usar variables, *inputs*, operaciones básicas y condicionales para crear una pequeña ficha de presentación.

### Requisitos

Abre tu entorno de Python (VS Code, IDLE, o terminal) para escribir y ejecutar el código.

-----

## 📝 1. Recolección de Datos (Variables y `input()`)

En este primer paso, usarás el comando **`input()`** para pedir información al usuario y la almacenarás en **variables**.

# Generador de Biografías Digitales

# 1. Variables de entrada (Input)
print("¡Bienvenido al Generador de Biografías! Por favor, responde las siguientes preguntas:")

# Uso de variables de tipo string (texto)
nombre = input("Ingresa tu nombre completo: ")
materia_favorita = input("¿Cuál es tu materia favorita en el bachillerato?: ")
habilidad = input("Menciona una habilidad que tengas (Ej: dibujar, programar, tocar guitarra): ")

# Uso de variables de tipo entero (número)
# Es necesario usar int() para convertir el texto ingresado a un número.
try:
    edad = int(input("¿Cuántos años tienes?: "))
    semestre = int(input("¿En qué semestre estás (debería ser 3)?: "))
except ValueError:
    print("Error: Por favor, ingresa solo números para la edad y el semestre.")
    exit() # Detiene el programa si hay un error de tipo


-----

## 🧮 2. Procesamiento Básico (Operaciones y Tipos)
Ahora realizarás una operación sencilla y usarás la conversión de tipos, que es un concepto fundamental en Python.

# 2. Procesamiento de datos

# Determinar el tiempo de estudio restante
# Si el bachillerato dura 6 semestres:
semestres_restantes = 6 - semestre

# Determinar el año de nacimiento (aproximado)
# Usaremos 2024 como año actual para el cálculo
año_actual = 2024
año_nacimiento = año_actual - edad

# Crear un eslogan usando f-strings (una forma moderna de formatear texto)
eslogan = f"Hola, soy {nombre} y mi objetivo es dominar {materia_favorita}."

## 🚦 3. Condicionales Simples (`if`, `elif`, `else`)
Usarás estructuras condicionales para que el programa tome decisiones y personalice la biografía.

# 3. Condicionales para la personalización
# Condicional basada en el semestre
if semestre == 3:
    mensaje_semestre = "¡Estás justo a la mitad de tu bachillerato!"
elif semestre < 3:
    mensaje_semestre = "Estás empezando, ¡mucho éxito!"
else: # Si el semestre es mayor a 3 (4, 5, 6)
    mensaje_semestre = f"¡Ya casi terminas! Solo te quedan {semestres_restantes} semestres. ¡Ánimo!"

# Condicional basada en la habilidad
if "programar" in habilidad.lower(): # Usamos .lower() para aceptar mayúsculas/minúsculas
    mensaje_habilidad = "¡Excelente! La programación es el futuro."
elif "dibujar" in habilidad.lower():
    mensaje_habilidad = "¡Qué bien! La creatividad es un gran activo."
else:
    mensaje_habilidad = "Tu habilidad te hará destacar."

## 🖼️ 4. Salida del Resultado (`print()`)
Finalmente, presentarás toda la información recolectada y procesada de forma clara usando el comando **`print()`** y los *f-strings*.

# 4. Salida de la Biografía (Output)
print("\n" + "=" * 50) # Imprime una línea de 50 guiones para separar
print("           FICHA DE PRESENTACIÓN GENERADA           ")
print("=" * 50)

print(f"👤 Nombre: {nombre.upper()}") # Usamos .upper() para resaltar el nombre
print(f"🎂 Edad: {edad} años (Naciste aproximadamente en {año_nacimiento})")
print(f"📚 Estado: {semestre}° Semestre | {mensaje_semestre}")
print(f"⭐ Lema: {eslogan}")
print(f"🛠️ Habilidad: {habilidad.capitalize()} | {mensaje_habilidad}") # Usamos .capitalize()
print("-" * 50)
```

### 📋 Código Completo para Ejecutar

Para que sea más fácil, aquí está todo el código junto:

```python
# Generador de Biografías Digitales - Código Completo

# 1. Variables de entrada (Input)
print("¡Bienvenido al Generador de Biografías! Por favor, responde las siguientes preguntas:")
nombre = input("Ingresa tu nombre completo: ")
materia_favorita = input("¿Cuál es tu materia favorita en el bachillerato?: ")
habilidad = input("Menciona una habilidad que tengas (Ej: dibujar, programar): ")

try:
    edad = int(input("¿Cuántos años tienes?: "))
    semestre = int(input("¿En qué semestre estás?: "))
except ValueError:
    print("Error: Por favor, ingresa solo números para la edad y el semestre.")
    exit()

# 2. Procesamiento de datos
semestres_restantes = 6 - semestre
año_actual = 2024
año_nacimiento = año_actual - edad
eslogan = f"Hola, soy {nombre} y mi objetivo es dominar {materia_favorita}."

# 3. Condicionales para la personalización
if semestre == 3:
    mensaje_semestre = "¡Estás justo a la mitad de tu bachillerato!"
elif semestre < 3:
    mensaje_semestre = "Estás empezando, ¡mucho éxito!"
else:
    mensaje_semestre = f"¡Ya casi terminas! Solo te quedan {semestres_restantes} semestres. ¡Ánimo!"

if "programar" in habilidad.lower():
    mensaje_habilidad = "¡Excelente! La programación es el futuro."
elif "dibujar" in habilidad.lower():
    mensaje_habilidad = "¡Qué bien! La creatividad es un gran activo."
else:
    mensaje_habilidad = "Tu habilidad te hará destacar."

# 4. Salida de la Biografía (Output)
print("\n" + "=" * 50)
print("           FICHA DE PRESENTACIÓN GENERADA           ")
print("=" * 50)
print(f"👤 Nombre: {nombre.upper()}")
print(f"🎂 Edad: {edad} años (Naciste aproximadamente en {año_nacimiento})")
print(f"📚 Estado: {semestre}° Semestre | {mensaje_semestre}")
print(f"⭐ Lema: {eslogan}")
print(f"🛠️ Habilidad: {habilidad.capitalize()} | {mensaje_habilidad}")
print("-" * 50)
```

