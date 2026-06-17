Triador de reclamos de soporte al cliente

Este es mi mini-proyecto para el desafío final del curso de Prompt Engineer Level 2. Elegí la línea de customer support porque es un caso con el que cualquiera se topa: una empresa que recibe muchos reclamos y no da abasto para ordenarlos.

El problema

Una tienda online recibe reclamos de clientes por todos lados (correo, chat, redes, formulario) y el equipo de soporte no logra atenderlos en orden. Pasa que un caso grave queda esperando detrás de una consulta menor, y a veces un reclamo delicado (alguien que amenaza con denunciar, por ejemplo) no llega a tiempo a una persona que pueda resolverlo. La idea es que una IA lea cada reclamo y diga qué tan urgente es y si conviene pasarlo de inmediato a un humano.

Quién lo usa y para qué

Lo usa el equipo de soporte, sobre todo el agente que recibe los casos y el líder que reparte la carga. La IA no le responde al cliente; solo entrega una especie de "ficha" del reclamo para que la persona decida a qué cola va y qué hacer primero. O sea, la salida ayuda a dos decisiones concretas: cuánta prioridad darle y si hay que escalarlo.

La técnica que elegí

Usé principalmente salida estructurada, es decir, que la IA responda siempre en un formato fijo (JSON) en vez de texto suelto. Lo elegí porque el resultado del triaje no es para leerlo y ya, sino para meterlo en el sistema de colas y para poder compararlo entre casos. Si la respuesta viene en prosa libre cada vez sale distinta y no se puede medir ni automatizar. Sobre esa base le agregué un rol claro, contexto del negocio, reglas de cuándo escalar y un ejemplo, pero la decisión de fondo fue esa: que la salida sea ordenada y predecible.

Cómo están organizados los archivos

El desafío sugería esta estructura de repositorio y la seguí tal cual:


prompt-inicial.md — el primer prompt, malo a propósito, y por qué no servía.
prompt-mejorado.md — cómo lo fui arreglando, versión por versión.
casos-prueba.md — los tres reclamos de prueba y lo que respondió la IA.
evaluacion.md — la nota que le puse a las respuestas.
riesgos.md — qué puede salir mal y qué mejoraría después.


Reflexión final

Entre el prompt inicial y el final cambió casi todo. El primero solo pedía una opinión ("dime cuáles son urgentes") sin decirle a la IA quién era, qué significaba urgente ni cómo contestar. El final tiene un rol, el contexto de la empresa, reglas claras de prioridad, qué hacer cuando falta información y un formato de respuesta cerrado.

La versión nueva es mejor por tres razones. Sirve más, porque cada respuesta ya viene con prioridad, intención y qué acción tomar. Se puede evaluar, porque al venir siempre en el mismo formato es fácil revisar si está bien o mal. Y es más segura, porque le prohibí inventar datos y la obligué a avisar cuando no está segura en vez de adivinar.

Lo que sigue débil es que todo depende de cómo escribió el cliente. Un caso grave redactado con calma podría quedar subestimado, y uno sin importancia pero con tono agresivo podría parecer más urgente de lo que es. Por eso dejé el escalamiento bastante conservador: ante la duda, que lo vea una persona.

Respondiendo las preguntas del desafío: la decisión más importante fue exigir un formato de salida fijo con criterios de prioridad claros, porque sin eso nada se puede medir ni automatizar. El peor problema del prompt inicial era que la tarea era ambigua. La técnica que más aportó fue la salida estructurada. Sé que el mejorado funciona mejor porque en la matriz de evaluación sube en formato, utilidad y control de riesgo. El riesgo que va a seguir ahí es confundir el tono con la urgencia real. Y antes de usarlo en serio probaría con muchos casos reales anonimizados y haría un A/B test entre dos versiones del prompt.