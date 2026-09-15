# Tío Navaja · Menú Navideño

Brochure interactivo de los dos packs de Navidad. Misma identidad que el
brochure corporativo (`tio-navaja-corporativo`): mismos tokens de color,
mismas tipografías y los mismos activos de marca.

**Publicado en:** https://claude.ai/artifact/PrMLoHVm9814WHJiKKePo9

## Qué hay aquí

- `index.html` — la pieza completa: estilos, contenido y lógica en un solo
  archivo. Se abre con doble clic, funciona sin conexión y sin servidor.
- `fonts/` — Chrone, DM Sans y Michigan Signature (copiadas del corporativo).
- `brand/` — logotipos, el Tío, la firma y los motivos de fondo.
- `photos/` — las tres fotos reales que coinciden con platos de este menú.

## Qué se toca

**El contacto.** El número vive en dos sitios: como `const WA` en el script
(de ahí sale el mensaje armado) y como `href` de los cuatro botones en el
HTML, que son el respaldo por si el JS no corre. Buscar `50763608156` y
reemplazar en todos.

**Los packs.** En el bloque `const PACKS`: precio, nombre y cuántas opciones
entran por tiempo. Cambiar un número recalcula solo los contadores, la
bandeja y los avisos.

**Los platos.** En `const DISHES`. Cada uno lleva `course` (entrada,
especialidad, guarnicion, postre) y `art`, que es el motivo ilustrado.

## El mensaje de WhatsApp

Los cuatro botones de cotización (barra, bandeja, cierre y pie) llevan
`data-quote`. En cada cambio de pack o de plato, `updateQuoteLinks()` les
reescribe el `href` con el mensaje ya redactado, así que a Tío Navaja no le
llega un "hola, información" sino la mesa completa:

```
Hola, quiero cotizar el Menú Navideño de Tío Navaja.

Pack $50 · La mesa de Nochebuena

ENTRADA
- Canoas de Tamal de Olla con Pork Belly

ESPECIALIDADES
- Pernil de Cerdo al Horno Glaseado con Piña y Especias
- Pavo al Horno con Relleno Criollo

...

Incluye tamal y rosca navideña.
```

Si la selección va a medias, cierra con una línea de lo que falta
("Me falta elegir: 2 guarniciones, 1 postre."), que le sirve al
restaurante para saber por dónde seguir la conversación.

El texto se arma en `buildMessage()`. Los `href` del HTML son `wa.me`
pelado a propósito: si el JS no corre, los botones siguen funcionando,
solo que sin mensaje.

## Las fotografías

Solo tres platos de este menú tienen foto real del cliente, y las tres
coinciden de verdad con lo que ofrece el menú navideño:

| Plato | Archivo | Por qué coincide |
|---|---|---|
| Mini Carimañolas Rellenas de Queso | `photos/carimanola.webp` | son las carimañolas con queso derretido |
| Flan de Coco | `photos/flan.webp` | el flan lleva coco rallado encima |
| Cheesecake de Maracuyá o Café | `photos/cheesecake.webp` | es la versión de maracuyá |

Los otros 16 platos van con lámina vectorial de la casa — el mismo sistema
del brochure corporativo. No se usó fotografía de archivo: o es el plato del
restaurante, o es ilustración declarada.

Para sumar una foto nueva: guardarla en `photos/` (4:5, 800×1000 basta) y
añadir `photo: 'photos/archivo.webp'` al plato en `DISHES`. La tarjeta cambia
sola de ilustración a fotografía.

## El giro navideño

No hay copos de nieve ni abetos: esto es Navidad panameña. El giro se
sostiene sobre cuatro cosas, y todas salen de la marca menos una.

**La guirnalda.** La bombilla de los fondos oficiales, encendida de verdad:
cada bombillo es un elemento con su vidrio, su casquillo y su halo, y titila
con su propio desfase para que la ristra nunca parpadee a la vez. Se arma en
JS (`buildGarlands`) porque el número de vanos depende del ancho. Cuelga bajo
la barra, sobre la banda de regalo, sobre los packs, sobre el menú y sobre el
cierre. Sobre fondo claro el cable se oscurece y el vidrio deja de irradiar.

**La luz.** Antes todo era campo plano de color y por eso no se leía la
temporada: la Navidad se lee por la luz. Ahora la portada tiene un foco
cálido tras el Tío, un rescoldo dorado arriba y una viñeta que da
profundidad. Los packs, el menú y el cierre tienen su propio resplandor.

**El dorado.** Es el único elemento que NO estaba en el manual: `--gold`
(#E3B25B) es un metálico **de temporada**, no un color nuevo de marca. Vive
solo en esta campaña y carga el titular, el símbolo de dólar, el sello, los
marcos y el estado elegido. Ningún sistema navideño se sostiene sin metálico.

**El titular.** "NAVIDAD" en Chrone, grande y dorado, con el logotipo arriba
en lockup. Antes la temporada era un renglón de 14px debajo del logo.

**Palmeras abajo, bombillos encima.** La portada se tapiza con palmeras —el
lugar— y lleva bombillos sueltos encima —la temporada—. Cada motivo dice una
cosa. El átomo se probó como destello y se descartó: con 17 % de trazo sobre
su lienzo, a 40 px desaparece.

## Lo que el PDF no traía

El brochure del cliente no especifica fechas disponibles, mínimo de personas,
impuestos ni condiciones de servicio. No se inventaron: el pie remite a
confirmarlos al cotizar. Cuando el cliente los dé, van en `.foot__legal`.
