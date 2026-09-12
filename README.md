## Para qué sirve

Le mandas el código de barras de un producto y te dice si es sano o no.

## Cómo funciona

1. Le mandas el código de barras.
2. Revisa que el código esté bien escrito.
3. Busca el producto en una base de datos.
4. Si no lo encuentra, te avisa.
5. Si no tiene datos de nutrición, te avisa.
6. Si tiene datos, mira si tiene mucho azúcar, sal o grasa.
7. Con eso decide: saludable, moderado o no saludable.
8. Una IA escribe un texto corto explicándolo.
9. Te devuelve todo junto: un título, los números, y el texto.

## Cómo está configurado

- Recibe peticiones en `/nutrition-check`.
- Solo necesita la clave de Groq (para el texto de la IA).

## Cómo se usa

Le mandas esto:

“barcode”: “5449000000996”

Y te devuelve un texto con el resultado dependiendo del producto.

## Manejo de errores

- Si no mandas código: te explica cómo usarlo.
- Si el código está mal escrito: te avisa.
- Si no encuentra el producto: te avisa.
- Si no tiene datos: te avisa.

## Limitaciones

- Solo funciona con un producto a la vez.
- No todos los productos están en la base de datos.
- Si falta un dato, igual intenta adivinar con lo que tiene.
- La IA puede cambiar de modelo y dejar de funcionar sin avisar.
- No recuerda nada de una vez a otra.
