# Catálogo Semántico Web

Proyecto de maquetación HTML semántica y aplicación de estilos CSS enfocada en la gestión de la cascada, herencia y especificidad.

## Resumen del Cálculo de Puntos de Especificidad

La especificidad determina qué regla CSS se aplica cuando múltiples reglas coinciden con el mismo elemento. Se calcula asignando un valor ponderado a cada tipo de selector:

- **Etiquetas (Elementos) ($1$ pt):** Selectores básicos como `p`, `a`, `header`, `article`. Tienen el peso más bajo.
- **Clases ($10$ pts):** Selectores basados en clases (`.btn-comprar`), multiplican por $10$ el peso de una etiqueta.
- **IDs ($100$ pts):** Selectores basados en identificadores (`#btn-destacado`), multiplican por $10$ el peso de una clase y dominan cualquier regla basada en el orden de la cascada.

_Nota:_ Se evita el uso de IDs para estilos y la regla `!important` para mantener un sistema plano, predecible y fácil de mantener.
