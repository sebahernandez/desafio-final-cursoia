# Riesgos, límites y mejora futura

## Riesgos y límites

| # | Riesgo / Límite | Mitigación actual | Mitigación pendiente |
|---|-----------------|-------------------|----------------------|
| 1 | **Confundir tono con impacto:** un mensaje agresivo pero trivial puede sobreestimarse, y uno crítico redactado con calma puede subestimarse. | Instrucción explícita de clasificar por impacto real, no por tono. | Calibrar con ejemplos few-shot de ambos tipos. |
| 2 | **Mala clasificación de casos ambiguos:** sin datos suficientes, la prioridad puede quedar mal asignada. | `confianza: baja` + `informacion_faltante` + prioridad conservadora. | Flujo multi-turn que pida los datos antes de clasificar. |
| 3 | **Riesgo de alucinación residual:** el modelo podría inferir montos, plazos o políticas no presentes. | Restricción "no inventes datos". | Validación posterior del JSON contra reglas de negocio. |
| 4 | **Dependencia del juicio humano en casos legales/sensibles.** | Reglas condicionales de escalamiento automático. | Revisión humana obligatoria para todo `escala_humano: true`. |
| 5 | **Deriva del esquema:** el modelo podría devolver texto fuera del JSON o un enum inválido. | Instrucción de responder solo con JSON válido. | Validar con un esquema JSON (schema) y reintentar si falla. |

> El desafío pide al menos dos riesgos; aquí se documentan cinco para cubrir el caso de forma realista.

## Mejora futura

En una próxima iteración se proponen, en orden de prioridad:

1. **A/B testing** entre dos variantes del prompt mejorado (por ejemplo, con y sin few-shot) usando los
   mismos casos de prueba y comparándolas con la misma matriz.
2. **Validación de esquema JSON**: validar cada salida contra un JSON Schema y reintentar automáticamente
   si no cumple, para garantizar integración segura al flujo.
3. **Flujo multi-turn** para casos de `confianza: baja`: que el asistente pida la información faltante antes
   de entregar la clasificación definitiva.
4. **Golden set anonimizado**: armar un conjunto de casos reales anonimizados etiquetados por un humano para
   medir precisión de forma sistemática (y no solo en 3 casos).
5. **Rúbrica más específica** por intención (facturación, envío, producto) con criterios de prioridad propios
   de cada categoría.
