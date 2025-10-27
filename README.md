# Sistema de Atención al Cliente

Este proyecto implementa un Agente de Inteligencia Artificial diseñado para automatizar y mejorar la atención al cliente en el Hospital Clínico San Borja Arriarán. El agente utiliza una arquitectura modular (Agente Coordinador, LLM y RAG) para manejar solicitudes administrativas comunes (estado de horas, farmacia, reclamos)

## Arquitectura y Frameworks

El diseño se basa en la **orquestación de herramientas**, un patrón clave en los **Frameworks de Agentes** (ej. LangChain, Autogen). Esta arquitectura garantiza escalabilidad y compatibilidad técnica al separar las responsabilidades de cada componente.

| Componente | Framework Simulado | Función (Herramienta) | Tipo de Integración |
| :--- | :--- | :--- | :--- |
| **Agente Coordinador** | Python/LangChain Agent | **Razonamiento** y **Planificación** | Orquesta el flujo de trabajo (decide clasificar, usar RAG o derivar). |
| **Clasificación/LLM** | GPT-3.5/Gemini | **Escritura** y **Razonamiento** | Interpreta el lenguaje natural, genera respuestas claras. |
| **RAG Pipeline** | ChromaDB + Sentence Transformer | **Consulta** y **Recuperación** | Accede a información contextual (protocolos, normativas) del hospital. |

---

## Diagrama de Orquestación de Componentes

El siguiente diagrama visualiza el flujo de información y la integración modular del agente, mostrando cómo el Agente Coordinador gestiona las herramientas y la memoria para tomar decisiones.



**Flujo de Orquestación Clave:**
1.  **Clasificación (Razonamiento):** El Agente clasifica la consulta para determinar la prioridad de la tarea.
2.  **Consulta (RAG):** Se activa la **Recuperación Semántica** para obtener contexto relevante de la Base de Conocimiento.
3.  **Toma de Decisiones (IE6):** Basado en la clasificación y el éxito/falla del RAG, se decide el flujo: Respuesta Automática o Derivación Humana.
4.  **Memoria:** Se registra la interacción para asegurar la coherencia en la siguiente pregunta.

---

## Integración de Herramientas

El Agente Coordinador integra las siguientes herramientas funcionales para operar con autonomía:

1.  **Herramienta de Razonamiento (`clasificacion`):** Identifica la intención de la consulta para derivar el flujo de manera autónoma.
    * *Ejemplo de Decisión:* Si detecta "cambiar hora", activa el flujo de reprogramación.
2.  **Herramienta de Consulta (`contexto` - RAG):** Busca contexto específico en la base de conocimiento para responder preguntas frecuentes y complejas, asegurando precisión.
    * *Simulación:* Busca `horarios_visita` o `farmacia_disponibilidad`.
3.  **Herramienta de Escritura (`generador_respuesta`):** Utiliza el contexto del RAG y el LLM para formular una respuesta amigable, simulando un "diálogo humano".

---

## Mecanismos de Memoria y Contexto

Para mantener la coherencia en tareas prolongadas, el agente integra dos tipos de memoria:

### Memoria de Corto Plazo
* **Mecanismo:** `self.memory_buffer` (Simulación de *Conversation Buffer*).
* **Función:** Almacena los últimos $K$ turnos de la conversación. Esto permite al agente mantener el hilo de un reclamo o una secuencia de preguntas sobre un mismo tema, asegurando la continuidad efectiva del flujo.

### Memoria de Largo Plazo
* **Mecanismo:** **Pipeline RAG** (Simulación de **Recuperación Semántica**).
* **Función:** Accede a la `self.knowledge_base`) para recuperar fragmentos de texto basados en la similitud semántica con la consulta del paciente, garantizando que la respuesta sea precisa, contextual y verificable según los protocolos del hospital.

---

## Decisiones de Diseño Clave

La elección de los componentes del agente está alineada con los requerimientos de reducir la carga administrativa y mejorar la precisión:

* **Implementación del RAG:** Es fundamental para garantizar que las respuestas sean **verificables** y basadas en la **normativa vigente**, superando las limitaciones de la memoria de entrenamiento del LLM.
* **Agente Coordinador:** Necesario para **separar la lógica de negocio** (escalamiento, trazabilidad) de la lógica lingüística, facilitando el mantenimiento y la auditoría.
* **Derivación Condicional:** La decisión de derivar automáticamente los `reclamos` (independientemente del RAG) es una política de diseño para **garantizar la trazabilidad** y liberar al funcionario solo para tareas de gestión crítica.

---

## 🚀 Instalación y Ejecución

**Prerrequisitos:** Python 3.9+
