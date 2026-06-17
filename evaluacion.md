# Evaluación de resultados

Se evalúa la salida del **prompt mejorado v2** con la matriz de criterios del desafío (escala 1 a 5)
y se compara contra el prompt inicial v0.

## Matriz de evaluación — prompt mejorado (v2)

Puntaje por caso (1 = muy deficiente, 5 = excelente):

| Criterio | Caso 1 (claro) | Caso 2 (ambiguo) | Caso 3 (riesgoso) | Observación |
|----------|:---:|:---:|:---:|-------------|
| **Claridad** (¿se entiende?) | 5 | 5 | 5 | JSON legible, campos autoexplicativos. |
| **Precisión** (¿responde bien al caso?) | 5 | 4 | 4 | Clasifica correcto; en ambiguo/riesgoso acierta el nivel conservador, pero sin contexto completo. |
| **Cumplimiento del formato** | 5 | 5 | 5 | JSON válido con enums respetados en los tres casos. |
| **Utilidad** (¿permite decidir/actuar?) | 5 | 4 | 5 | Acción sugerida concreta; en el ambiguo la acción es "pedir info", igualmente accionable. |
| **Control de riesgo** (¿evita inventar/asumir?) | 4 | 5 | 5 | No inventa datos; marca `confianza` e `informacion_faltante`; escala lo sensible. |
| **Promedio** | **4.8** | **4.6** | **4.8** | Promedio global ≈ **4.7 / 5** |

## Comparación inicial (v0) vs mejorado (v2)

| Criterio | v0 (inicial) | v2 (mejorado) | Cambio |
|----------|:---:|:---:|:---:|
| Claridad | 3 | 5 | ▲ |
| Precisión | 2 | 4–5 | ▲▲ |
| Cumplimiento del formato | 1 | 5 | ▲▲▲▲ |
| Utilidad | 2 | 4–5 | ▲▲ |
| Control de riesgo | 1 | 4–5 | ▲▲▲ |

**Lectura:** la mejora más fuerte está en **cumplimiento de formato** y **control de riesgo**, justamente las
dimensiones que hacían inservible al prompt inicial para un flujo automatizado. La precisión sube pero no llega
a 5 en casos ambiguos/riesgosos porque depende de información que el cliente no entregó — un límite real, no un
defecto del prompt, y por eso esos casos se marcan con `confianza: baja`.

## Cómo se midió

- **Cumplimiento de formato** es objetivo: ¿la salida es JSON válido y respeta los enums? (sí en los 3 casos).
- **Precisión** se contrastó contra la prioridad esperada definida por las reglas P1–P4 del prompt.
- **Control de riesgo** se verificó comprobando que no aparecieran datos inventados (montos, n.º de pedido,
  políticas) y que los casos sensibles activaran `escala_humano`.
