# Evaluación de las respuestas

Le puse nota a las respuestas del prompt final usando los criterios que pide el desafío, con una escala de 1 a 5. A continuación, presento la tabla de puntajes y luego explico qué significa cada criterio.

| Criterio                | Caso claro | Caso ambiguo | Caso delicado |
| ----------------------- | :--------: | :----------: | :-----------: |
| Claridad                |     5      |      5       |       5       |
| Precisión               |     5      |      4       |       4       |
| Cumplimiento del formato |     5      |      5       |       5       |
| Utilidad                |     5      |      4       |       5       |
| Control de riesgo       |     4      |      5       |       5       |

---

### Análisis de los resultados

-   **Claridad y Formato:** En ambos criterios, la IA obtiene un puntaje perfecto en los tres casos. Las respuestas siempre se presentan en el formato JSON solicitado, lo que las hace ordenadas y fáciles de leer.

-   **Precisión:** La precisión baja ligeramente en los casos ambiguo y delicado. Esto no se debe a un error de la IA, sino a que la información proporcionada por el cliente era insuficiente, obligando al modelo a clasificar con datos limitados.

-   **Utilidad:** La utilidad de las respuestas es alta, ya que cada una sugiere una acción concreta. Incluso en el caso ambiguo, la acción recomendada (pedir más datos) es la correcta.

-   **Control de riesgo:** Aquí es donde se nota la mayor mejora. En ningún caso la IA inventó montos, números de pedido ni políticas. Además, indicó correctamente cuándo no estaba segura de la clasificación.

### Comparación con el prompt inicial

Si comparo el prompt inicial con el final, la diferencia es notable. El prompt inicial habría obtenido calificaciones muy bajas, especialmente en **formato** (porque no pedía ninguna estructura) y en **control de riesgo** (porque nada le impedía inventar datos). El prompt final mejora significativamente en estos dos aspectos, que eran los que lo hacían inservible para un sistema real.

### Metodología de evaluación

Para que la evaluación no parezca solo una opinión, aclaro cómo medí cada criterio:

-   **Cumplimiento del formato:** Es un criterio objetivo. O la respuesta es un JSON válido con los valores permitidos, o no lo es. En los tres casos, lo fue.
-   **Precisión:** La comparé contra la prioridad que correspondía según las reglas que yo mismo definí en el prompt.
-   **Control de riesgo:** Lo verifiqué buscando si aparecían datos inventados y si los casos delicados activaban correctamente el escalamiento a un humano.