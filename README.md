# Triador de reclamos de soporte al cliente con escalamiento

> Mini-proyecto de prompt engineering — Desafío final, AI Certs Prompt Engineer Level 2 (Sesión 7)

**Línea elegida:** Opción A — AI-driven customer support
**Caso de uso:** Customer support (clasificación de urgencia + detección de intención + escalamiento humano)
**Técnica principal:** Salida estructurada (Structured Output), apoyada por role-based, contextual, conditional y few-shot prompting.

---

## 1. Problema

Una tienda de e-commerce recibe reclamos por múltiples canales (email, chat, redes y formulario)
y el equipo de soporte no logra priorizarlos de forma consistente: casos críticos quedan en cola
detrás de consultas menores y algunos reclamos sensibles (amenazas de denuncia, problemas legales)
no se escalan a tiempo. Se necesita un asistente que, dado **un reclamo**, devuelva una clasificación
**accionable y uniforme** para priorizar y enrutar la atención.

## 2. Usuario objetivo

Agente de soporte de primer nivel y líder del equipo de atención. El asistente **no responde al cliente**:
produce metadatos de triaje que alimentan la cola de prioridades y la regla de enrutamiento.

## 3. Propósito de la salida

Apoyar dos decisiones operativas concretas:

1. **Priorizar** el reclamo (P1–P4) según impacto y urgencia reales.
2. **Decidir el enrutamiento**: si requiere escalamiento humano inmediato y cuál es la próxima acción interna.

La salida debe ser **estructurada (JSON)** para integrarse a un flujo automatizado y poder evaluarse de forma objetiva.

## 4. Técnica seleccionada y justificación

**Técnica principal: Structured Output (salida estructurada en JSON).**

Justificación: el resultado del triaje no es para leerse, es para **consumirse por un sistema** (cola de
prioridades, ruteo) y para **evaluarse de forma comparable** entre casos. Una salida en prosa libre sería
inconsistente, difícil de parsear y casi imposible de medir con una matriz. Un esquema JSON fijo garantiza
campos siempre presentes, valores acotados (enums) y evaluación objetiva del cumplimiento de formato.

Técnicas de apoyo, cada una atada a una debilidad concreta del prompt inicial:

- **Role-based** → define que el modelo es un triador interno, no un agente que conversa con el cliente.
- **Contextual** → entrega negocio, canales y SLA para que "urgente" tenga un significado operativo.
- **Conditional** → reglas explícitas de cuándo `escala_humano = true` (P1, amenaza legal, daño, reincidencia).
- **Few-shot** → un ejemplo de entrada/salida fija el estilo y reduce variabilidad.

## 5. Estructura del repositorio

```
prompt-final/
├── README.md          ← este archivo (visión general, técnica, reflexión, evaluación)
├── prompt-inicial.md  ← prompt v0 + diagnóstico de sus debilidades
├── prompt-mejorado.md ← evolución paso a paso del prompt (v0 → v1 → v2) con changelog
├── casos-prueba.md    ← 3 casos (claro / ambiguo / riesgoso) y resultados obtenidos
├── evaluacion.md      ← matriz de evaluación + comparación inicial vs mejorado
└── riesgos.md         ← riesgos, límites y mejora futura
```

## 6. Cómo se documentó la evolución del prompt (Git)

El cambio del prompt se registra **paso a paso** como commits, de modo que el historial de Git
*sea* la documentación de la evolución:

```bash
git init
git add README.md prompt-inicial.md
git commit -m "v0: prompt inicial + diagnóstico de debilidades"

git add prompt-mejorado.md
git commit -m "v1: agrega rol, contexto/SLA y formato de salida JSON"

git commit -am "v2: agrega reglas condicionales de escalamiento, manejo de ambiguedad, no-inventar y few-shot"

git add casos-prueba.md evaluacion.md
git commit -m "Pruebas con 3 casos y matriz de evaluacion"

git add riesgos.md
git commit -m "Riesgos, limites y mejora futura"
```

Luego se publica en GitHub:

```bash
git branch -M main
git remote add origin https://github.com/<tu-usuario>/triaje-soporte-prompt.git
git push -u origin main
```

> Tip: si quieres dejar la trazabilidad aún más explícita, puedes etiquetar versiones del prompt
> con `git tag prompt-v0`, `git tag prompt-v1`, `git tag prompt-v2`.

## 7. Reflexión final

**¿Qué cambió entre el prompt inicial y el mejorado?**
El inicial pedía una opinión ("dime cuáles son urgentes") sin rol, sin criterios y sin formato. El mejorado
define un rol, entrega contexto de negocio y SLA, fija criterios de prioridad P1–P4, reglas condicionales de
escalamiento, manejo de casos incompletos y una salida JSON con valores acotados.

**¿Por qué la nueva versión es más útil, evaluable o segura?**
- *Más útil*: cada salida incluye prioridad, intención y acción sugerida → es directamente accionable y ruteable.
- *Más evaluable*: al ser JSON con enums, el cumplimiento de formato y la precisión se miden objetivamente.
- *Más segura*: prohíbe inventar datos, obliga a marcar `confianza: baja` e `informacion_faltante` cuando el
  caso es ambiguo, y escala automáticamente los casos sensibles.

**¿Qué aspecto seguiría siendo débil?**
La clasificación depende del texto del cliente: un caso crítico redactado con calma podría subestimarse, y uno
trivial con tono agresivo podría sobreestimarse. La decisión de impacto real sigue necesitando juicio humano en
casos límite, por eso el escalamiento es conservador.

### Preguntas de reflexión del documento

- **Decisión técnica más importante:** fijar un esquema de salida JSON con criterios P1–P4 explícitos; sin eso, nada es evaluable ni ruteable.
- **Problema más crítico del prompt inicial:** la tarea ambigua ("urgentes" sin definición), que hacía la salida no reproducible.
- **Técnica que aportó más valor:** structured output, porque convierte la respuesta en datos consumibles y medibles.
- **Cómo sé que el mejorado funciona mejor:** la matriz de evaluación (ver `evaluacion.md`) sube en formato, precisión, utilidad y control de riesgo respecto al inicial.
- **Riesgo que persiste:** confundir tono emocional con impacto real; mala clasificación de casos ambiguos.
- **Qué probar antes de producción:** un set de casos reales anonimizados (golden set) y un A/B test entre variantes del prompt.
