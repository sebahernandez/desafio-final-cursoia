# Prompt inicial (v0) y diagnóstico

## Prompt inicial — versión 0

Esta es la primera versión, intencionalmente simple e imperfecta. Sirve como punto de comparación.

```text
Analiza estos reclamos y dime cuáles son urgentes.
```

## Diagnóstico del prompt inicial

Se identifican las siguientes debilidades (más de las tres mínimas que pide el desafío):

| # | Debilidad | Por qué es un problema |
|---|-----------|------------------------|
| 1 | **Sin rol definido** | El modelo no sabe si responde al cliente, asesora al agente o produce metadatos. La respuesta varía en cada ejecución. |
| 2 | **Sin contexto de negocio ni SLA** | "Urgente" no tiene un significado operativo. No hay canales, ni niveles de prioridad, ni tiempos de respuesta. |
| 3 | **Tarea ambigua** | "Cuáles son urgentes" es binario y subjetivo; no distingue grados de prioridad ni intención del cliente. |
| 4 | **Sin formato de salida** | La respuesta es prosa libre: no se puede parsear, integrar a una cola ni comparar entre casos. |
| 5 | **Sin criterios de clasificación** | No existen reglas de qué hace urgente a un reclamo (impacto, fecha límite, riesgo legal). |
| 6 | **Sin manejo de casos incompletos o ambiguos** | Frente a un reclamo vago, el modelo decidirá por su cuenta y probablemente inventará contexto. |
| 7 | **Riesgo de alucinación** | Nada le prohíbe inventar montos, números de pedido o políticas que no están en el texto. |
| 8 | **Salida no accionable** | Aunque diga "es urgente", no indica qué hacer ni si debe escalar a un humano. |
| 9 | **Sin instrucción de escalamiento** | No detecta casos sensibles (amenazas legales, daño, reincidencia) que requieren intervención humana. |

> Las tres debilidades más críticas son la **#3 (tarea ambigua)**, la **#4 (sin formato)** y la **#5 (sin criterios)**:
> juntas hacen que la salida sea no reproducible, no evaluable y no integrable. La mejora del prompt se centra en resolver estas.
