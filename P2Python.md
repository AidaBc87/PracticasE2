## 📝 Práctica: Gestor de Tareas Semanales (Listas y Bucles)

Esta práctica te permitirá simular la gestión de una lista de tareas (`listas`) y usar bucles (`for` y `while`) para interactuar con esa lista.

### 1\. 📋 Inicialización (Creación de la Lista)
Una **lista** es una colección ordenada y mutable (editable) de elementos.

# Lista inicial de tareas (strings)
tareas_pendientes = [
    "Estudiar para el examen de Matemáticas",
    "Terminar el ensayo de Historia",
    "Comprar materiales para el proyecto de Arte",
    "Revisar la práctica de Django"
]

print("--- Tareas Iniciales ---")
print(tareas_pendientes)
print(f"Tienes {len(tareas_pendientes)} tareas por hacer.") # len() da la longitud de la lista

## 🔄 2. Bucle `for` (Recorrer y Mostrar)
El **bucle `for`** es ideal para recorrer todos los elementos de una lista, uno por uno, sin necesidad de saber cuántos hay.

print("\n--- Tareas Organizadas ---")
# Usamos un bucle for para mostrar cada tarea con su número de índice.
# enumerate() nos da el índice (i) y el valor (tarea) simultáneamente.
for indice, tarea in enumerate(tareas_pendientes):
    # Sumamos 1 al índice porque las listas inician en 0, pero queremos que se vea bien para el usuario.
    print(f"Tarea #{indice + 1}: {tarea}")

## ➕ 3. Añadir una Tarea (Método `.append()`)
Usamos el método **`.append()`** para agregar un elemento al final de la lista.

# Pedir al usuario que añada una nueva tarea
nueva_tarea = input("\nIngresa una nueva tarea para agregar a la lista: ")

# Añadir la tarea al final de la lista
tareas_pendientes.append(nueva_tarea)

print(f"¡'{nueva_tarea}' ha sido añadida!")
print(f"Total de tareas ahora: {len(tareas_pendientes)}")

## ✅ 4. Bucle `while` (Eliminar una Tarea)
El **bucle `while`** es ideal cuando la condición de salida no es fija (es decir, el usuario puede querer eliminar varias tareas o ninguna) y se basa en una condición lógica.

# Bucle while para permitir eliminar tareas hasta que el usuario decida parar
while True:
    print("\n--- Menú de Eliminación ---")
    
    # 1. Mostrar la lista actual con sus índices
    for indice, tarea in enumerate(tareas_pendientes):
        print(f"[{indice}]: {tarea}") # Mostramos el índice real para que el usuario lo use.
        
    print("\n[Escribe 'fin' para terminar]")
    
    # 2. Obtener la entrada del usuario
    entrada = input("Ingresa el NÚMERO DE ÍNDICE de la tarea que completaste: ")
    
    # 3. Condición de Salida del Bucle
    if entrada.lower() == 'fin':
        print("Saliendo del gestor de tareas...")
        break # Esta instrucción rompe el bucle while y continúa el programa.
        
    # 4. Procesamiento de la Eliminación
    try:
        indice_a_eliminar = int(entrada)
        
        # Validación: Revisar si el índice está dentro del rango de la lista
        if 0 <= indice_a_eliminar < len(tareas_pendientes):
            
            # Usamos el método .pop() para eliminar el elemento por su índice
            tarea_eliminada = tareas_pendientes.pop(indice_a_eliminar)
            print(f"✅ ¡Tarea eliminada: '{tarea_eliminada}'!")
            
        else:
            print("❌ Error: Índice fuera de rango. Intenta con un número de la lista.")
            
    except ValueError:
        print("❌ Error: Debes ingresar un número o la palabra 'fin'.")

## 5\. 🥳 Resultado Final
print("\n" + "=" * 40)
print("¡Felicidades! Tareas Restantes:")

# Usamos el bucle for final para mostrar lo que queda
for indice, tarea in enumerate(tareas_pendientes):
    print(f"{indice + 1}. {tarea}")

if not tareas_pendientes: # Una forma elegante de verificar si la lista está vacía
    print("✨ ¡Lista de tareas completada!")
print("=" * 40)
```

### Conceptos Clave Repasados:

  * **Listas (`[]`)**: Almacenamiento de múltiples datos.
  * **Bucles `for`**: Recorrer elementos de una lista.
  * **Bucles `while`**: Ejecutar código repetidamente hasta que una condición se cumpla.
  * **Métodos de Lista (`.append()`, `.pop()`)**: Añadir y eliminar elementos.
  * **Manejo de Errores (`try`/`except`)**: Para que el programa no falle si el usuario ingresa texto en lugar de un número.

¿Quieres intentar un ejercicio que combine el uso de **diccionarios** con listas? Los diccionarios son perfectos para almacenar información con *llaves* y *valores*.
