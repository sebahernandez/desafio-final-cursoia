## Prompt inicial y sus problemas

Esta es la primera versión del prompt, escrita de forma simple como punto de partida para la comparación.

> Analiza estos reclamos y dime cuáles son urgentes.

A primera vista, parece que pide lo correcto, pero tiene varios problemas:

1.  **La tarea es ambigua**: El problema más grave es que la tarea es ambigua. La instrucción "cuáles son urgentes" no significa nada concreto, ya que no define qué hace que un reclamo sea urgente ni distingue grados de urgencia. Para un modelo de IA, un caso sería simplemente "urgente" o "no urgente", cuando en la práctica existen reclamos críticos, medios y menores.

2.  **No le da contexto**: El segundo problema es que no proporciona contexto. La IA no sabe que trabaja para una tienda, ni qué tiempos de respuesta maneja el equipo, ni qué tipos de reclamo existen. Sin esa información, el concepto de "urgente" queda librado a la suposición del modelo.

3.  **No pide ningún formato de respuesta**: El tercer problema es que no solicita un formato de respuesta específico. La IA contestará en texto suelto, con un formato que puede variar cada vez, lo que impide integrar la respuesta en un sistema de colas o comparar casos entre sí.

### Otras debilidades

También vale la pena nombrar otras debilidades menores:

-   No se le especificó a la IA qué rol cumple (¿debe responderle al cliente o solo clasificar?).
-   No se le dieron criterios claros para clasificar.
-   No se le explicó qué hacer si el reclamo viene incompleto.
-   No se le prohibió inventar datos.
-   La respuesta no termina siendo accionable, porque aunque diga "es urgente", no especifica qué hay que hacer ni si conviene pasarlo a una persona.

De todos estos, los tres que realmente rompen el prompt son la **tarea ambigua**, la **falta de criterios** y la **falta de formato**. Esos tres puntos juntos hacen que la respuesta sea impredecible y que no se pueda medir ni utilizar. La mejora del prompt apunta principalmente a resolverlos.