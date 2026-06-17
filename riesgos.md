# Riesgos y mejoras a futuro

## Qué puede salir mal

1.  **Confundir tono con urgencia real**: El riesgo que más me preocupa es que la IA confunda el tono del mensaje con la urgencia real. Un reclamo escrito con mucha rabia pero por un problema menor podría ser priorizado incorrectamente, y viceversa, un problema grave contado con calma podría pasar desapercibido. Intenté mitigar esto indicándole en el prompt que clasifique por el **impacto real** y no por lo enojado que suene el mensaje, pero es algo que conviene vigilar.

2.  **Casos ambiguos**: Cuando el cliente proporciona poca información, la clasificación puede ser imprecisa. Para manejar esto, le pedí a la IA que, en esos casos, marque la confianza como "baja", sea prudente con la prioridad y especifique qué información falta, en lugar de adivinar.

3.  **Invención de datos**: Siempre existe la posibilidad de que la IA invente información, como un monto o un plazo que el cliente nunca mencionó. La instrucción de no inventar ayuda, pero no elimina el riesgo por completo.

4.  **Casos sensibles**: Hay situaciones, sobre todo legales o delicadas, en las que la IA no debería tener la última palabra. Por eso, establecí reglas de escalamiento para que estos casos siempre lleguen a una persona.

## Qué mejoraría después

Si tuviera que seguir trabajando en esto, mis próximos pasos serían:

-   **Realizar un A/B test**: Crearía dos versiones del prompt mejorado, una con el ejemplo y otra sin él. Les pasaría los mismos casos y compararía cuál clasifica mejor para entender el impacto del ejemplo.

-   **Ampliar el conjunto de datos de prueba**: Juntaría un conjunto más grande de reclamos reales (anonimizados y etiquetados a mano por el equipo) para medir con mayor precisión la tasa de acierto y no basarme solo en tres casos.

-   **Implementar un flujo de varios pasos para casos dudosos**: En lugar de clasificar a ciegas, la IA podría primero solicitar los datos que faltan y, solo después de recibirlos, asignar la prioridad.

-   **Validación técnica del formato**: Por el lado más técnico, implementaría una validación para asegurar que la respuesta siempre cumpla con el formato esperado. Si la respuesta no es correcta, el sistema debería pedirle a la IA que lo reintente, para evitar que un error en el formato afecte al sistema que procesa la respuesta.