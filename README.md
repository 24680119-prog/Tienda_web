## Tienda web Aplicacion 
El sigueinte proyecto consiste en el desarrollo de una aplicación interactiva utilizando el lenguaje de programación Python junto con el framework Flet, el cual permite la creación de interfaces gráficas modernas de manera sencilla. La aplicación simula una tienda de tecnología donde se muestran diversos productos organizados en tarjetas visuales, cada una con información detallada como nombre, descripción, precio e imagen.

El sistema permite al usuario interactuar con los productos mediante diferentes funcionalidades, como marcar artículos como favoritos, agregarlos a un carrito de compras y realizar búsquedas dinámicas a través de un campo de texto. Para lograr una estructura ordenada y reutilizable, se implementó una clase personalizada que representa cada producto, aplicando el concepto de Programación Orientada a Objetos (POO), específicamente el uso de herencia.

## Definición y Configuración de la Clase ProductCard
En esta parte del código se define una clase llamada ProductCard, la cual hereda de la clase Container del framework Flet. Esto significa que ProductCard es un componente visual personalizado que se utiliza para representar cada producto dentro de la interfaz gráfica de la aplicación. Dentro del método constructor (init), se inicializan los atributos del objeto. Se recibe como parámetro un diccionario llamado "producto", que contiene la información del producto (como nombre, precio, descripción e imagen), y una función llamada "agregar_carrito", que permite añadir el producto al carrito de compras.

La instrucción super().init() se utiliza para llamar al constructor de la clase padre (Container), lo que permite que el componente herede todas sus propiedades visuales y de comportamiento. Posteriormente, se almacenan los datos del producto en la variable self.producto, y se crea una variable booleana llamada self.favorito, que inicialmente se establece en False para indicar que el producto no está marcado como favorito.

Luego, se configuran las propiedades visuales del componente, como el ancho (width), el espacio interno (padding), el margen externo (margin), el redondeo de las esquinas (border_radius) y el color de fondo (bgcolor). Estas propiedades permiten definir la apariencia de la tarjeta del producto.

Finalmente, se agrega una sombra al componente mediante la propiedad self.shadow, utilizando la clase BoxShadow. Esta sombra tiene un nivel de desenfoque (blur_radius), un color suave (BLACK12) y un desplazamiento (offset), lo que genera un efecto visual que hace que la tarjeta resalte sobre el fondo.

```python
class ProductCard(ft.Container):

    def __init__(self, producto, agregar_carrito):
        super().__init__()

        self.producto = producto
        self.favorito = False

        self.width = 260
        self.padding = 15
        self.margin = 10
        self.border_radius = 15
        self.bgcolor = ft.Colors.WHITE

        self.shadow = ft.BoxShadow(
            blur_radius=15,
            color=ft.Colors.BLACK12,
            offset=ft.Offset(2, 2)

```

## Funcionalidad del Botón de Favorito
En esta sección del código se implementa la funcionalidad que permite marcar un producto como favorito mediante un botón con ícono de corazón, primero, se define la función toggle_favorito, la cual se ejecuta cada vez que el usuario hace clic en el botón. Dentro de esta función, se cambia el estado de la variable self.favorito utilizando una negación lógica (not), lo que permite alternar entre verdadero (True) y falso (False).
Si el producto se marca como favorito (True), el ícono del botón cambia a un corazón lleno y se colorea de rojo, indicando visualmente que el producto ha sido seleccionado como favorito. En caso contrario, si el producto deja de ser favorito (False), el ícono cambia a un corazón vacío y se elimina el color.

La instrucción e.control.update() se encarga de actualizar el botón en la interfaz para reflejar los cambios realizados de manera inmediata. Posteriormente, se crea un botón de tipo IconButton llamado "corazon", el cual inicialmente muestra un corazón vacío. Este botón tiene asignado el evento on_click, que ejecuta la función toggle_favorito cuando el usuario interactúa con él.

De esta forma, se logra una interacción dinámica que permite al usuario marcar y desmarcar productos como favoritos dentro de la aplicación.

```python
        def toggle_favorito(e):
            self.favorito = not self.favorito

            if self.favorito:
                e.control.icon = ft.Icons.FAVORITE
                e.control.icon_color = ft.Colors.RED
            else:
                e.control.icon = ft.Icons.FAVORITE_BORDER
                e.control.icon_color = None

            e.control.update()

        corazon = ft.IconButton(
            icon=ft.Icons.FAVORITE_BORDER,
            on_click=toggle_favorito
        )
```

##  Estructura del Contenido de la Tarjeta de Producto
En esta parte del código se define el contenido visual de la tarjeta del producto mediante la propiedad self.content. Para organizar los elementos, se utiliza un componente Column del framework Flet, el cual permite distribuir los elementos de forma vertical. El parámetro spacing=10 establece un espacio entre cada uno de los elementos dentro de la columna, logrando una mejor organización visual. Dentro de la lista controls se agregan los distintos componentes que representan la información del producto. En primer lugar, se muestra el identificador (ID) del producto utilizando un componente Text, el cual incluye formato en negrita y color negro para resaltar la información.

Posteriormente, se incluye una imagen del producto mediante el componente Image. La imagen se carga desde la carpeta de recursos "assets", utilizando la ruta especificada en los datos del producto. Además, se definen dimensiones específicas (ancho y alto) para mantener un diseño uniforme. 

A continuación, se muestra el nombre del producto con un tamaño de texto mayor y en negrita, lo que permite destacarlo como el elemento principal de la tarjeta, finalmente, se presenta la descripción del producto mediante otro componente Text, con un tamaño más pequeño pero también en negrita, proporcionando información adicional de forma clara.

```python
        self.content = ft.Column(
            spacing=10,
            controls=[

                ft.Text(
                    f"ID: {producto['id']}",
                    size=12,
                    weight=ft.FontWeight.BOLD,
                    color=ft.Colors.BLACK
                ),

                ft.Image(
                    src=f"assets/{producto['ruta_imagen']}",
                    width=230,
                    height=150
                ),

                ft.Text(
                    producto["nombre"],
                    size=18,
                    weight=ft.FontWeight.BOLD,
                    color=ft.Colors.BLACK
                ),

                ft.Text(
                    producto["descripcion"],
                    size=12,
                    weight=ft.FontWeight.BOLD,
                    color=ft.Colors.BLACK
                ),


```

## Visualización del Precio y Acciones del Producto

En esta sección del código se completa la estructura visual de la tarjeta del producto, mostrando el precio y los botones de interacción disponibles para el usuario. Primero, se utiliza un componente Text para mostrar el precio del producto. Este se presenta con un formato que incluye el símbolo de moneda ($) y separadores de miles, lo que mejora la legibilidad. Además, el texto tiene un tamaño mayor y está en negrita, con el objetivo de destacarlo dentro de la tarjeta.

Posteriormente, se utiliza un componente Row para organizar horizontalmente los elementos de interacción. El parámetro alignment=SPACE_BETWEEN permite distribuir los elementos con espacio entre ellos, ubicando uno a la izquierda y otro a la derecha. Dentro de esta fila se incluyen dos elementos principales. El primero es el botón de favorito (corazon), que permite al usuario marcar o desmarcar el producto como favorito. El segundo es un botón de tipo ElevatedButton con el texto "Agregar al carrito" y un ícono de carrito de compras.

Este botón tiene asociado un evento on_click que ejecuta una función anónima (lambda). Cuando el usuario hace clic, se llama a la función agregar_carrito y se envía como argumento el producto actual, permitiendo así añadirlo al carrito de compras.


```python
                ft.Text(
                    f"${producto['precio']:,}",
                    size=18,
                    weight=ft.FontWeight.BOLD,
                    color=ft.Colors.BLACK
                ),

                ft.Row(
                    alignment=ft.MainAxisAlignment.SPACE_BETWEEN,
                    controls=[
                        corazon,

                        ft.ElevatedButton(
                            "Agregar al carrito",
                            icon=ft.Icons.SHOPPING_CART,
                            on_click=lambda e: agregar_carrito(self.producto)
                        )
                    ]
                )
            ]
        )
```

## Configuración Inicial de la Página y Variables del Carrito
En esta parte del código se define la función principal de la aplicación llamada main, la cual recibe como parámetro un objeto page de tipo Page proporcionado por el framework Flet. Esta función es la encargada de configurar toda la interfaz gráfica y la lógica principal del programa.

Primero, se establecen algunas propiedades de la página. Se define el título de la aplicación como "Tienda de Tecnología", se asigna un color de fondo mediante un código hexadecimal y se habilita el desplazamiento automático (scroll), lo que permite visualizar todos los elementos aunque excedan el tamaño de la pantalla. Posteriormente, se crea una estructura de datos llamada carrito, la cual es un diccionario vacío. Este diccionario se utiliza para almacenar los productos que el usuario agregue al carrito, junto con la cantidad de cada uno.

Luego, se define un componente de texto llamado contador, el cual se inicializa con el valor "0". Este elemento se utiliza para mostrar en pantalla la cantidad total de productos agregados al carrito. Además, se le aplican estilos como tamaño de texto, negrita y color.Finalmente, se crea otro componente de texto llamado texto_carrito, que inicialmente muestra el mensaje "Carrito vacío". Este elemento servirá para mostrar posteriormente la lista de productos que el usuario agregue al carrito, funcionando como un resumen de la compra.

```python

def main(page: ft.Page):

    page.title = "Tienda de Tecnología"
    page.bgcolor = "#CFEFFF"
    page.scroll = "auto"

    carrito = {}
    contador = ft.Text(
        "0",
        size=20,
        weight=ft.FontWeight.BOLD,
        color=ft.Colors.BLACK
    )

    texto_carrito = ft.Text(
        "Carrito vacío",
        size=16,
        weight=ft.FontWeight.BOLD,
        color=ft.Colors.BLACK
    )
```

## Función para Agregar Productos al Carrito
En esta sección del código se define la función agregar_carrito, la cual se encarga de gestionar la lógica para añadir productos al carrito de compras.

La función recibe como parámetro un objeto llamado producto, que contiene la información del artículo seleccionado. A partir de este objeto, se obtiene el nombre del producto, el cual se utiliza como clave dentro del diccionario carrito. Luego, se verifica si el producto ya existe en el carrito. Si el nombre del producto ya está presente, se incrementa su cantidad en uno. En caso contrario, si es la primera vez que se agrega, se crea una nueva entrada en el diccionario con valor inicial de uno.

Posteriormente, se actualiza el contador visual del carrito. Para ello, se suman todas las cantidades almacenadas en el diccionario carrito utilizando la función sum, y el resultado se convierte a texto para mostrarlo en el componente contador. Finalmente, se utiliza page.update() para refrescar la interfaz gráfica, asegurando que los cambios realizados se reflejen inmediatamente en pantalla.

```python
    def agregar_carrito(producto):

        nombre = producto["nombre"]

        if nombre in carrito:
            carrito[nombre] += 1
        else:
            carrito[nombre] = 1

        contador.value = str(sum(carrito.values()))
        page.update()

```

## Función para Mostrar el Contenido del Carrito
En esta parte del código se define la función mostrar_carrito, la cual se encarga de mostrar en pantalla los productos que el usuario ha agregado al carrito de compras. La función recibe un parámetro llamado e, que corresponde al evento generado al hacer clic en el botón del carrito. Aunque no se utiliza directamente dentro de la función, es necesario para manejar el evento en Flet.

Primero, se inicializa una variable llamada lista como una cadena de texto vacía. Esta variable se utilizará para construir el contenido que se mostrará al usuario. Luego, se recorre el diccionario carrito utilizando un ciclo for. En cada iteración, se obtienen el nombre del producto y la cantidad correspondiente. Estos valores se concatenan en la variable lista en un formato legible, por ejemplo: "Computadora x2", seguido de un salto de línea para separar cada producto.

Después, se verifica si la variable lista sigue vacía. Esto significa que no hay productos en el carrito. En ese caso, se asigna el mensaje "El carrito está vacío" para informar al usuario.Finalmente, el contenido de la variable lista se asigna al componente de texto texto_carrito, y se utiliza page.update() para actualizar la interfaz y mostrar los cambios en pantalla.

De esta manera, esta función permite visualizar de forma clara y organizada los productos seleccionados por el usuario dentro del carrito.


```python

    def mostrar_carrito(e):

        lista = ""

        for nombre, cantidad in carrito.items():
            lista += f"{nombre} x{cantidad}\n"

        if lista == "":
            lista = "El carrito está vacío"

        texto_carrito.value = lista
        page.update()
```



