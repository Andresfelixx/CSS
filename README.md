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
   - **Colores:** `--color-primario` (#4f46e5), `--color-secundario` (#10b981), `--color-fondo-principal` (#f3f4f6), `--color-fondo-tarjeta` (#ffffff) y `--color-texto` (#1f2937).
   - **Tipografía:** `--fuente-principal` ('Inter', sans-serif).
   - **Espaciado:** `--espaciado-pequeno` (8px), `--espaciado-medio` (16px) y `--espaciado-grande` (24px).

2. **La ventaja de reutilizar medidas de margen y relleno:**
   Permite mantener una consistencia visual estricta en toda la interfaz sin depender de valores arbitrarios. Si en el futuro se requiere ajustar el espaciado global, solo es necesario modificar el valor en el `:root` en lugar de buscar y cambiar cada selector de manera individual.

3. **De qué manera la centralización en `:root` previene colisiones visuales:**
   Al depender de una fuente única de verdad para los tokens de diseño, se evitan inconsistencias accidentales, facilitando el mantenimiento y garantizando la armonía y escala visual a medida que la hoja de estilos crece y se agregan nuevos componentes.

## Hallazgos: Pseudoclases y Pseudoelementos

1. **La diferencia funcional entre una pseudoclase y un pseudoelemento:**
   - **Pseudoclase (Ej. `:hover`, `:focus`):** Su función principal es reaccionar a estados o eventos dinámicos de un elemento existente en el DOM, definiendo cómo debe comportarse o lucir cuando el usuario interactúa con él o según su posición en el árbol.
   - **Pseudoelemento (Ej. `::before`, `::after`):** Su propósito es inyectar contenido y estilizar partes específicas de un elemento sin alterar el marcado HTML original, creando nodos virtuales que el navegador renderiza a nivel visual.

2. **La importancia técnica de la pseudoclase `:focus` para cumplir con buenas prácticas de accesibilidad web:**
   - Permite a los usuarios que dependen del teclado (tecla `Tab`) o de tecnologías de asistencia identificar de manera clara e inequívoca qué elemento interactivo tiene el foco actual (botones, enlaces, campos de formulario). Previene la desorientación y garantiza una experiencia inclusiva y conforme a los estándares WCAG.

3. **Por qué es una buena práctica inyectar elementos decorativos (como etiquetas de oferta o iconos) desde CSS con `::before`/`::after` en lugar de ensuciar el archivo HTML con etiquetas vacías:**
   - Permite mantener un HTML semántico y limpio, separando por completo la presentación del contenido estructurado. Además, facilita un mantenimiento escalable, ya que cualquier modificación o eliminación de un elemento decorativo se centraliza directamente en la hoja de estilos.

## Hallazgos: Arquitectura BEM y Modularidad

1. **Qué significa la sigla BEM y cómo se escribe visualmente:**
   - **BEM** responde a la nomenclatura de **Bloque, Elemento y Modificador** (*Block, Element, Modifier*). Su objetivo es estructurar el código CSS mediante clases predecibles y desacopladas.
   - **Sintaxis visual:** Se compone utilizando un bloque base, doble guion bajo (`__`) para conectar los elementos internos y doble guion medio (`--`) para los modificadores o variantes de estado. Por ejemplo:
     ```css
     .tarjeta { }
     .tarjeta__titulo { }
     .tarjeta--destacada { }
     ```

2. **Por qué dividir el CSS en varios archivos facilita el trabajo colaborativo:**
   - Permite organizar el código de manera modular (por ejemplo, un archivo independiente por cada componente dentro de una estructura de carpetas). Al trabajar en equipo mediante Git, esto reduce drásticamente los conflictos de *merge*, ya que cada desarrollador puede modificar los estilos del componente específico en el que está trabajando sin colisionar con el archivo monolítico de sus compañeros.

3. **Cómo esta metodología evita la guerra de especificidad (Cascada) al mantener un peso plano:**
   - BEM elimina el uso de selectores anidados complejos (como `.menu ul li a`) o el abuso de IDs, manteniendo la especificidad uniforme y baja en todo el proyecto (un peso plano basado exclusivamente en clases de nivel único). De este modo, la cascada deja de ser un problema de pesos incontrolables y las reglas se aplican de forma predecible según su orden de declaración.

## Hallazgos: Arquitectura Total con Flexbox

1. **Por qué fue crucial aplicar `min-height: 100vh` y `flex-direction: column` al contenedor global para controlar el pie de página:**
   - Permite implementar de forma limpia el patrón de diseño conocido como *Sticky Footer* (pie de página anclado al fondo). Al establecer `min-height: 100vh`, nos aseguramos de que el contenedor principal ocupe al menos la altura total de la ventana gráfica (*viewport*). Al cambiar la dirección del flujo a columna con `flex-direction: column`, organizamos los elementos verticalmente; esto, combinado con el crecimiento flexible del contenido principal, empuja automáticamente el pie de página hacia el borde inferior de la pantalla incluso cuando la página tiene poco contenido.

2. **Cómo la propiedad `gap` reemplazó el uso excesivo de márgenes laterales en los menús de navegación:**
   - La propiedad `gap` simplifica y moderniza la distribución del espacio entre elementos flexibles. A diferencia de los márgenes tradicionales —que requerían aplicar separaciones individuales y lidiar con el elemento final usando selectores complejos como `:not(:last-child)`—, `gap` aplica el espaciado de manera uniforme y exclusiva *entre* los elementos adyacentes, sin afectar los bordes externos del contenedor. Esto reduce la cantidad de código, mejora la legibilidad y previene errores de diseño.

3. **Cómo la unión de BEM, Custom Properties y Flexbox te permitió crear una tarjeta de producto resistente a diferentes longitudes de texto:**
   - La metodología **BEM** (Block, Element, Modifier) aporta una arquitectura modular y predecible que facilita la estructuración limpia de los componentes de la tarjeta de producto sin problemas de especificidad. Las **Custom Properties** (variables CSS) centralizan los valores de diseño (como espaciados, colores y tamaños), garantizando consistencia. Por último, **Flexbox** gestiona la alineación y distribución interna de los elementos de forma fluida (por ejemplo, estirando o fijando los bloques para que el precio o el botón de compra queden alineados al fondo), logrando que la tarjeta se adapte perfectamente a títulos o descripciones de cualquier longitud sin romperse visualmente.