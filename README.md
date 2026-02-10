# Pol-gono
Polígono 2d en Blender

1. Objetivo de la práctica

El objetivo de esta práctica es aprender a utilizar **Python dentro de Blender** para crear de manera programada un **polígono regular en 2D**, aplicando conceptos básicos de programación, matemáticas y modelado 3D.

En esta práctica se genera un polígono (por ejemplo, un hexágono) mediante código, sin usar las herramientas manuales de dibujo de Blender.

2. Requisitos

Antes de iniciar la práctica es necesario contar con lo siguiente:

* Blender instalado en el equipo
* Conocimientos básicos de Python
* Comprender que la librería bpy solo funciona dentro de Blender


3. Acceso al entorno de scripting en Blender

1. Abrir Blender.
2. En la pantalla inicial seleccionar General.
3. En la barra superior de Blender, cambiar al espacio de trabajo llamado Scripting.
4. En el área izquierda aparecerá el Editor de Texto, que es donde se escribe el código Python.
5. Borrar cualquier texto existente en el editor.

Este entorno permite ejecutar scripts de Python que interactúan directamente con Blender.

4. Código utilizado en la práctica

```python
import bpy
import math


def crear_poligono_2d(nombre, lados, radio):
    # Crear una nueva malla y un nuevo objeto
    malla = bpy.data.meshes.new(nombre)
    objeto = bpy.data.objects.new(nombre, malla)

    # Vincular el objeto a la escena actual
    bpy.context.collection.objects.link(objeto)

    vertices = []
    aristas = []

    # Cálculo de vértices usando coordenadas polares a cartesianas
    for i in range(lados):
        angulo = 2 * math.pi * i / lados
        x = radio * math.cos(angulo)
        y = radio * math.sin(angulo)
        vertices.append((x, y, 0))  # Z = 0 para mantenerlo en 2D

    # Definir las conexiones (aristas) entre los vértices
    for i in range(lados):
        aristas.append((i, (i + 1) % lados))

    # Cargar los datos en la malla
    malla.from_pydata(vertices, aristas, [])
    malla.update()


# Limpiar la escena antes de empezar
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# Llamada a la función: un hexágono de radio 5
crear_poligono_2d("Poligono2D", lados=6, radio=5)
```

5. Explicación detallada del código

Importación de librerías

```python
import bpy
import math
```

* **bpy**: Librería propia de Blender que permite crear y modificar objetos, mallas y escenas.
* **math**: Librería de Python utilizada para funciones matemáticas como seno, coseno y pi.

Definición de la función

```python
def crear_poligono_2d(nombre, lados, radio):
```

Esta función permite crear un polígono 2D.

Parámetros:

* **nombre**: Nombre del objeto y la malla.
* **lados**: Número de lados del polígono.
* **radio**: Distancia del centro a cada vértice.

Creación de la malla y el objeto

```python
malla = bpy.data.meshes.new(nombre)
objeto = bpy.data.objects.new(nombre, malla)
```

* Se crea una nueva malla vacía.
* Se crea un objeto que utiliza esa malla.

Vinculación del objeto a la escena

```python
bpy.context.collection.objects.link(objeto)
```

Esta línea hace que el objeto aparezca en la escena actual de Blender.

Listas para vértices y aristas

```python
vertices = []
aristas = []
```

* **vertices**: Guardará las coordenadas de cada punto del polígono.
* **aristas**: Guardará las conexiones entre vértices.

Cálculo de los vértices

```python
for i in range(lados):
    angulo = 2 * math.pi * i / lados
    x = radio * math.cos(angulo)
    y = radio * math.sin(angulo)
    vertices.append((x, y, 0))
```

* Se recorre cada lado del polígono.
* Se calcula el ángulo correspondiente a cada vértice.
* Se convierten coordenadas polares a cartesianas.
* El valor **Z = 0** mantiene el polígono en dos dimensiones.

Creación de las aristas

```python
for i in range(lados):
    aristas.append((i, (i + 1) % lados))
```

* Se conectan los vértices uno con otro.
* El operador módulo (%) permite cerrar el polígono uniendo el último vértice con el primero.

Carga de datos en la malla

```python
malla.from_pydata(vertices, aristas, [])
malla.update()
```

* Se cargan los vértices y aristas en la malla.
* Se actualiza la malla para que Blender la muestre.

Limpieza de la escena

```python
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
```

Estas instrucciones eliminan todos los objetos de la escena antes de crear el polígono.

Llamada a la función

```python
crear_poligono_2d("Poligono2D", lados=6, radio=5)
```

* Se crea un **hexágono**.
* Se puede modificar el número de lados para crear otras figuras como triángulos o cuadrados.

6. Resultado

Al ejecutar el script en Blender, se obtiene un **polígono regular 2D** centrado en el origen del plano, generado completamente mediante Python.

En esta práctica aprendí que Python puede utilizarse dentro de Blender para crear figuras geométricas de manera automática. Me pareció interesante ver cómo las matemáticas y la programación se combinan para generar modelos gráficos, además de que facilita el dibujo preciso de figuras sin necesidad de hacerlo manualmente.

<img width="566" height="407" alt="image" src="https://github.com/user-attachments/assets/403cae5d-6714-414c-9411-347a49b87c0c" />
<img width="1371" height="731" alt="image" src="https://github.com/user-attachments/assets/3f5cc6e6-0942-4c6e-bf32-f30a0f5d7291" />






