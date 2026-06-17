# Casos de prueba y resultados

Se ejecutó el **prompt mejorado v2** con tres casos que incluyen variaciones: uno claro, uno ambiguo y
uno riesgoso/sensible. Para cada uno se muestra la entrada y la salida JSON obtenida del modelo.

> Nota: ningún caso usa datos personales reales (cumple las restricciones del desafío).

---

## Caso 1 — Claro / urgente

**Entrada:**
> "El producto llegó dañado y necesito cambio urgente porque era para un evento mañana."

**Salida obtenida:**
```json
{
  "prioridad": "P1",
  "intencion": "devolucion_cambio",
  "sentimiento": "negativo",
  "escala_humano": true,
  "motivo_escalamiento": "Fecha límite inminente (<48 h): el cliente necesita el cambio para mañana.",
  "confianza": "media",
  "informacion_faltante": ["número de pedido", "dirección para el cambio express"],
  "justificacion": "Producto dañado con necesidad de reemplazo antes de un evento al día siguiente; impacto y urgencia altos.",
  "accion_sugerida": "Priorizar cambio express y verificar stock y logística disponible para entrega en 24 h."
}
```

---

## Caso 2 — Ambiguo / incompleto

**Entrada:**
> "No entiendo el cobro de mi última factura."

**Salida obtenida:**
```json
{
  "prioridad": "P3",
  "intencion": "facturacion",
  "sentimiento": "neutral",
  "escala_humano": false,
  "motivo_escalamiento": null,
  "confianza": "baja",
  "informacion_faltante": ["número de factura", "monto en disputa", "qué cargo no reconoce el cliente"],
  "justificacion": "Consulta de facturación sin evidencia de error ni urgencia; no hay datos suficientes para confirmar un problema.",
  "accion_sugerida": "Solicitar el detalle de la factura y explicar el desglose de los cargos."
}
```

> El prompt maneja bien la ambigüedad: en lugar de inventar un error de cobro, marca `confianza: baja`
> y pide la información faltante.

---

## Caso 3 — Riesgoso / sensible

**Entrada:**
> "Esto es inaceptable, nadie responde y voy a denunciar."

**Salida obtenida:**
```json
{
  "prioridad": "P1",
  "intencion": "queja_servicio",
  "sentimiento": "muy_negativo",
  "escala_humano": true,
  "motivo_escalamiento": "Amenaza de denuncia y reclamo reiterado ('nadie responde'): riesgo legal y reputacional.",
  "confianza": "baja",
  "informacion_faltante": ["motivo original del reclamo", "número de caso previo"],
  "justificacion": "Cliente con reclamo reiterado y amenaza de denuncia; aunque se desconoce el problema de fondo, el riesgo obliga a tratarlo como crítico.",
  "accion_sugerida": "Escalar de inmediato a un supervisor para contacto directo y recuperación del contexto."
}
```

> Aunque no se conoce el problema original, las reglas condicionales activan el escalamiento por la
> amenaza de denuncia y la reincidencia. El prompt **no inventa** el motivo: lo deja en `informacion_faltante`.
