# Casos de prueba

Probé el prompt final con tres reclamos distintos: uno claro, uno ambiguo y uno delicado. Ninguno usa datos reales de clientes. Para cada uno, dejo el reclamo y la respuesta de la IA.

## Caso 1: Claro

**Reclamo:** "El producto llegó dañado y necesito cambio urgente porque era para un evento mañana."

**Respuesta de la IA:**
```json
{
  "prioridad": "P1",
  "intencion": "devolucion_cambio",
  "sentimiento": "negativo",
  "escala_humano": true,
  "motivo_escalamiento": "Hay una fecha límite muy cercana: el cliente lo necesita para mañana.",
  "confianza": "media",
  "informacion_faltante": ["número de pedido", "dirección para el cambio"],
  "justificacion": "Producto dañado que hay que reemplazar antes de un evento al día siguiente; urgencia alta.",
  "accion_sugerida": "Priorizar un cambio express y revisar si hay stock y logística para entregar mañana."
}
```
**Análisis:** La IA acertó al marcarlo como crítico por la fecha límite y sugirió una acción concreta y adecuada.

---

## Caso 2: Ambiguo

**Reclamo:** "No entiendo el cobro de mi última factura."

**Respuesta de la IA:**
```json
{
  "prioridad": "P3",
  "intencion": "facturacion",
  "sentimiento": "neutral",
  "escala_humano": false,
  "motivo_escalamiento": null,
  "confianza": "baja",
  "informacion_faltante": ["número de factura", "qué cargo no reconoce", "monto en duda"],
  "justificacion": "Es una consulta de facturación sin señales de error ni de urgencia, y falta información para confirmar si hay un problema.",
  "accion_sugerida": "Pedir el detalle de la factura y explicar el desglose de los cargos."
}
```
**Análisis:** Lo interesante es que no inventó un error de cobro. Como no tenía datos suficientes, marcó la confianza como baja y solicitó la información faltante, que es exactamente lo que debía hacer según las instrucciones.

---

## Caso 3: Delicado

**Reclamo:** "Esto es inaceptable, nadie responde y voy a denunciar."

**Respuesta de la IA:**
```json
{
  "prioridad": "P1",
  "intencion": "queja_servicio",
  "sentimiento": "muy_negativo",
  "escala_humano": true,
  "motivo_escalamiento": "Amenaza con denunciar y dice que nadie le responde; hay riesgo legal y de imagen.",
  "confianza": "baja",
  "informacion_faltante": ["cuál era el reclamo original", "número de caso anterior"],
  "justificacion": "Cliente con reclamo repetido y amenaza de denuncia; aunque no se sabe el problema de fondo, el riesgo obliga a tratarlo como crítico.",
  "accion_sugerida": "Escalar de inmediato a un supervisor para que lo contacte y recupere el contexto."
}
```
**Análisis:** Aunque no conoce el problema original, las reglas de escalamiento hicieron que lo clasificara correctamente debido a la amenaza y al ser un reclamo repetido. De nuevo, no inventó el motivo del problema, sino que lo registró como información faltante.