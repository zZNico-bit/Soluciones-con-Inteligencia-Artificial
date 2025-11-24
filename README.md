# Agente de IA para Atención al Cliente

## Descripción del Proyecto

Este proyecto implementa un **Agente de Inteligencia Artificial Modular** diseñado para optimizar la atención al cliente en el **Hospital Clínico San Borja Arriarán**. La solución se centra en la orquestación de herramientas, la gestión de memoria y la toma de decisiones adaptativa, garantizando la **trazabilidad** completa de las interacciones.

---

## 1. Arquitectura y Componentes del Agente

La arquitectura se basa en un patrón de orquestación donde el Agente Coordinador dirige el flujo de trabajo, asegurando que se utilicen las herramientas correctas en cada etapa.

### 1.1. Estructura de Componentes

| Componente | Función Principal | Rol en el Flujo |
| :--- | :--- | :--- |
| **Agente Coordinador** | Control de Flujo y Planificación | Decide la ruta. |
| **LLM / Clasificación** | Razonamiento | Categoriza la intención de la consulta. |
| **Pipeline RAG** | Consulta y Recuperación | Accede a la Base de Conocimiento verificada para soporte contextual. |

### 1.2. Herramientas Funcionales

El sistema integra las siguientes herramientas programáticas:

1.  **`clasificacion()`**: Identifica la intención para la planificación.
2.  **`contexto()`**: Recupera información específica de la Base de Conocimiento (Memoria de Largo Plazo).
3.  **`generador_respuesta()`**: Formula la respuesta final, usando contexto RAG y memoria.

**Diagrama de Orquestación de Componentes**


---

## 2. Mecanismos de Inteligencia y Planificación

### 2.1. Gestión de Memoria

| Mecanismo | Implementación | Propósito |
| :--- | :--- | :--- |
| **Memoria de Corto Plazo** | `self.memory_buffer` (Buffer de los últimos 3 turnos) | Mantiene la **coherencia** de la conversación en flujos prolongados. |
| **Memoria de Largo Plazo** | `self.knowledge_base` (Base RAG) | Asegura la **precisión** y la verificabilidad de las respuestas con protocolos hospitalarios. |

### 2.2. Planificación Adaptativa

El Agente ajusta su **comportamiento adaptativo** basándose en la clasificación y el resultado de la búsqueda RAG:

| Condición | Decisión de Planificación | Justificación |
| :--- | :--- | :--- |
| **pregunta_frecuente** + Contexto | **Respuesta Autónoma** | Alta confianza, eficiencia. |
| **reclamo** | **Derivación Obligatoria** | Política de **trazabilidad** y registro legal. |
| **otra_consulta** + Sin Contexto | **Derivación Condicional** | Complejidad o límite del conocimiento del sistema. |

---

## 3. Observabilidad y Trazabilidad

La monitorización continua es vital para la fiabilidad operativa del Agente.

### 3.1. Métricas Implementadas

Las siguientes métricas se rastrean en `self.metrics` para evaluar el desempeño:

1.  **Latencia Promedio (ms)**: Mide la velocidad de respuesta (Rendimiento).
2.  **Precisión de Respuesta Autónoma (%)**: Mide la efectividad del Agente sin intervención humana.
3.  **Tasa de Derivación Humana (%)**: Mide la frecuencia de escalamiento.

### 3.2. Dashboards de Monitoreo

Se requiere un dashboard visual (ej. Grafana, Streamlit) para visualizar el comportamiento del Agente.



### 3.3. Análisis de Logs y Trazabilidad

Cada interacción genera un log de trazabilidad que captura la ruta de decisión y el rendimiento (`turn_latency_ms`), esencial para la auditoría:

**Hallazgo Típico:** La alta tasa de derivación humana en categorías ambiguas indica un **déficit en la Base de Conocimiento RAG**, justificando la necesidad de expansión y curación de datos.

---

## 4. Propuesta de Recomendaciones de Optimización

Las siguientes recomendaciones están justificadas por el análisis de métricas y la trazabilidad operativa:

| Objetivo | Recomendación Práctica | Justificación |
| :--- | :--- | :--- |
| **Aumentar Precisión** | Expandir el RAG con consultas que resultaron en derivación. | Reducir la **Tasa de Derivación Humana**. |
| **Mejorar Rendimiento** | Implementar **Caching de Respuestas** para consultas frecuentes. | Reducir la **Latencia Promedio** y el consumo de recursos. |
| **Mejorar Razonamiento** | Refinar el clasificador con técnicas de *Few-Shot Prompting*. | Minimizar la **Tasa de Error de Clasificación** en el log. |

---

## 5. Instalación y Ejecución

El código fuente del Agente se encuentra en `HospitalAIAgent.py`.

### 5.1. Requisitos
* Python 3.9

### 5.2. Comando de Ejecución
Ejecute el script para iniciar la simulación de turnos y generar el reporte final de métricas:

```bash
python HospitalAIAgent.py
