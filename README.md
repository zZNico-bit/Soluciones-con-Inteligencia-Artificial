# Sistema de Atención al Cliente

Este proyecto implementa un Agente de Inteligencia Artificial diseñado para automatizar y mejorar la atención al cliente en el Hospital Clínico San Borja Arriarán. El agente utiliza una arquitectura modular (Agente Coordinador, LLM y RAG) para manejar solicitudes administrativas comunes (estado de horas, farmacia, reclamos)

## Arquitectura y Frameworks

El diseño se basa en la orquestación de herramientas, un patrón clave en los **Frameworks de Agentes**.

| Componente | Framework Simulado | Función (Herramienta) | Tipo de Integración |
| :--- | :--- | :--- | :--- |
| **Agente Coordinador** | Python/LangChain Agent | **Razonamiento** y **Planificación** | Orquesta el flujo de trabajo (decide clasificar, usar RAG o derivar). |
| **Clasificación/LLM** | GPT-3.5/Gemini | **Escritura** y **Razonamiento** | Interpreta el lenguaje natural, genera respuestas claras. |
| **RAG Pipeline** | ChromaDB + Sentence Transformer | **Consulta** y **Recuperación** | Accede a información contextual (protocolos, normativas) del hospital. |

## Integración de Herramientas

El Agente Coordinador integra las siguientes herramientas funcionales:

1.  **Herramienta de Razonamiento (`clasificacion`):** Identifica la intención de la consulta para derivar el flujo de manera autónoma.
    * *Ejemplo de Decisión:* Si detecta "cambiar hora", activa el flujo de reprogramación.
2.  **Herramienta de Consulta (`contexto`):** Busca contexto específico en la base de conocimiento para responder preguntas frecuentes y complejas, asegurando precisión.
    * *Simulación:* Busca `horarios_visita` o `farmacia_disponibilidad`.
3.  **Herramienta de Escritura (`generador_respuesta`):** Utiliza el contexto del RAG y el LLM para formular una respuesta amigable, simulando un "diálogo humano".

## Instalación y Ejecución

**Prerrequisitos:** Python 3.9+
