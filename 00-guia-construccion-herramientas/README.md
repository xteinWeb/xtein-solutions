# Guía Oficial para la Construcción de Herramientas 🛠️

> **Estándar Metodológico y Técnico de Desarrollo en ARTDECON**  
> Elaborado por: **Equipo XTEIN** | Programa PILAS IA

---

## 📌 Introducción y Propósito

El propósito de esta guía es establecer las **reglas del taller digital**: la forma oficial en que se conciben, diseñan, programan, documentan y despliegan las soluciones tecnológicas en ARTDECON.

El objetivo no es frenar la agilidad ni la creatividad de los equipos, sino **asegurar que las piezas encajen**, que el código sea mantenible en el tiempo, seguro frente a fugas de información y fácilmente integrable con **XTEIN ONE**.

---

## 📚 Índice de la Guía

| Capítulo | Título | Descripción |
| :--- | :--- | :--- |
| **01** | [Ciclo de Vida de una Solución](./01-ciclo-de-vida.md) | Las 5 fases desde la fricción en el puesto de trabajo hasta producción. |
| **02** | [Patrones de Arquitectura y Código](./02-patrones-arquitectura.md) | Desacoplamiento, Strangler Fig, Gateways y prohibición de acople legacy. |
| **03** | [Seguridad, Datos y Gobernanza](./03-seguridad-y-datos.md) | El Semáforo PILAS IA, segregación OLTP/OLAP y gestión de secretos (`.env`). |
| **04** | [Kit Documental Obligatorio](./04-plantilla-documentacion.md) | Los 5 documentos canónicos que debe entregar cada solución. |
| **05** | [Checklist de Aprobación XTEIN](./05-checklist-aprobacion.md) | Criterios estrictos para recibir luz verde y pasar a producción. |

---

## ⚡ Los 4 Principios Innegociables de XTEIN

1. **La innovación nace del puesto de trabajo:** No construimos software por moda. Toda herramienta debe eliminar tiempos muertos, fricciones o errores en una tarea real de ARTDECON.
2. **Inviolabilidad del Legacy sin contrato:** Ninguna solución nueva debe modificar código legacy destructivamente. Se aplican fachadas, adaptadores y gateways (como se implementó en `Cubicacion_X`).
3. **Frontend desacoplado de la Base de Datos:** Todo acceso a datos se hace mediante backend tipado con contratos claros (RFC 7807). Queda prohibido consultar directamente bases transaccionales desde el cliente web.
4. **Documentación viva antes de desplegar:** El código sin documentación es deuda técnica que frena a la empresa. Toda solución debe registrar su mapa de aplicación y sus contratos de dependencias.
