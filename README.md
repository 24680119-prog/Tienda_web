## Tienda web Aplicacion 
El sigueinte proyecto consiste en el desarrollo de una aplicación interactiva utilizando el lenguaje de programación Python junto con el framework Flet, el cual permite la creación de interfaces gráficas modernas de manera sencilla. La aplicación simula una tienda de tecnología donde se muestran diversos productos organizados en tarjetas visuales, cada una con información detallada como nombre, descripción, precio e imagen.

El sistema permite al usuario interactuar con los productos mediante diferentes funcionalidades, como marcar artículos como favoritos, agregarlos a un carrito de compras y realizar búsquedas dinámicas a través de un campo de texto. Para lograr una estructura ordenada y reutilizable, se implementó una clase personalizada que representa cada producto, aplicando el concepto de Programación Orientada a Objetos (POO), específicamente el uso de herencia.

De
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
        )

