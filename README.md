# Catálogo Semántico Web

Proyecto de maquetación HTML semántica y aplicación de estilos CSS enfocada en la gestión de la cascada, herencia y especificidad.

## Resumen del Cálculo de Puntos de Especificidad

La especificidad determina qué regla CSS se aplica cuando múltiples reglas coinciden con el mismo elemento. Se calcula asignando un valor ponderado a cada tipo de selector:

- **Etiquetas (Elementos) ($1$ pt):** Selectores básicos como `p`, `a`, `header`, `article`. Tienen el peso más bajo.
- **Clases ($10$ pts):** Selectores basados en clases (`.btn-comprar`), multiplican por $10$ el peso de una etiqueta.
- **IDs ($100$ pts):** Selectores basados en identificadores (`#btn-destacado`), multiplican por $10$ el peso de una clase y dominan cualquier regla basada en el orden de la cascada.

_Nota:_ Se evita el uso de IDs para estilos y la regla `!important` para mantener un sistema plano, predecible y fácil de mantener.

## Hallazgos: El Modelo de Caja

1. **La diferencia práctica entre Margin y Padding:**
   El _padding_ es el espacio interno que se genera entre el contenido de un elemento y su propio borde (crece por dentro de la caja). El _margin_ es el espacio externo que se genera alrededor del elemento, separándolo de las demás cajas vecinas.

2. **Por qué es obligatorio usar `box-sizing: border-box`:**
   Porque por defecto el navegador utiliza `content-box`, lo que significa que al sumar un _padding_ o un borde, las dimensiones totales del elemento aumentan sumando esos valores, rompiendo los diseños y desalineando los contenedores. `border-box` obliga a que el tamaño total declarado incluya el relleno y el borde, haciendo que crezcan hacia adentro.

3. **Cómo se ven afectados los elementos hermanos cuando le aplicas un margen grande a uno de ellos:**
   Los elementos hermanos se empujan y se alejan manteniendo la distancia configurada. Además, los márgenes verticales de elementos adyacentes pueden fusionarse en un fenómeno conocido como _margin collapsing_ (colapso de márgenes), donde el espacio entre ellos no se suma, sino que toma el valor del margen más grande.

## Hallazgos: Centralización de Identidad Visual y Espaciado

1. **La lista completa de variables declaradas:**
   - **Colores:** `--color-primario` (#007bff), `--color-secundario` (#28a745), `--color-fondo-principal` (#f8f9fa), `--color-fondo-tarjeta` (#ffffff) y `--color-texto` (#333333).
   - **Tipografía:** `--fuente-principal` ('Inter', sans-serif).
   - **Espaciado:** `--espaciado-pequeno` (8px), `--espaciado-medio` (16px) y `--espaciado-grande` (24px).

2. **La ventaja de reutilizar medidas de margen y relleno:**
   Permite mantener una consistencia visual estricta en toda la interfaz sin depender de valores arbitrarios. Si en el futuro se requiere ajustar el espaciado global, solo es necesario modificar el valor en el `:root` en lugar de buscar y cambiar cada selector de manera individual.

3. **De qué manera la centralización en `:root` previene colisiones visuales:**
   Al depender de una fuente única de verdad para los tokens de diseño, se evitan inconsistencias accidentales, facilitando el mantenimiento y garantizando la armonía y escala visual a medida que la hoja de estilos crece y se agregan nuevos componentes.
