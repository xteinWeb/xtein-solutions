# 02. Patrones de Arquitectura y Buenas Prácticas

> **Estándares Técnicos Oficiales de ARTDECON**  
> Inspirado en los aprendizajes de `Cubicacion_X` y la macroarquitectura de `XTEIN ONE`.

---

## 🏛️ 1. Patrón Strangler Fig (Migración Segura sin Romper el Legacy)

En ARTDECON existen sistemas históricos (scripts en Google Apps Script, hojas de cálculo, sistemas legados en Vite/React o bases de datos compartidas).

* **Regla de Oro:** **Nunca reescribir un sistema desde cero borrando el anterior**.
* **Cómo se aplica:**
  1. El sistema legacy sigue operando normalmente.
  2. La nueva solución se construye en una capa aislada (ej. `corporate/`).
  3. Se interceptan gradualmente las operaciones (primero lectura, luego catálogos maestros y finalmente transacciones críticas).
  4. Ambas versiones conviven hasta que la nueva solución demuestre 100% de paridad operativa.

---

## 🚪 2. Patrón Gateway / Fachada (Desacoplamiento)

* **Problema:** En desarrollos no estandarizados, el frontend invoca directamente consultas SQL, nombres de esquemas internos (ej. `pdesarrollo`) o endpoints cambiantes.
* **Solución XTEIN:**
  * Toda comunicación pasa por una interfaz de contrato (`Gateway`).
  * En Angular: Crear un servicio abstracto (ej. `ProductoGateway`) que defina los métodos (`obtenerMaestros()`, `registrarOperacion()`).
  * El componente visual solo conoce el contrato, nunca los detalles de infraestructura o de la base de datos subyacente.

---

## 🚫 3. Prohibición de Acceso Directo a Base de Datos (ADR-004)

* **Mandato XTEIN:** Queda estrictamente prohibido que un cliente web (Angular, React, HTML) tenga credenciales de base de datos o ejecute consultas directas a SQL Server o Supabase.
* **Flujo Obligatorio:**
  ```text
  [Cliente Web / Frontend] 
         ⬇️ (HTTP REST tipado con Token JWT / API Key interna)
  [Backend Node.js / XTEIN Gateway]
         ⬇️ (Validación de reglas, permisos y auditoría)
  [Base de Datos: SQL Server / Supabase / Postgres]
  ```

---

## 📦 4. Microfrontends y Modularidad (Alineación XTEIN ONE)

* Las herramientas departamentales deben diseñarse como módulos independientes capaces de federarse dentro del **Shell Host de XTEIN ONE**.
* **Principios de módulo:**
  * Auto-contenido: Tiene sus propias rutas, componentes y modelos.
  * Dependencias acotadas: No depende de librerías globales que generen colisión de versiones.
  * Tokens de diseño compartidos: Respetar la paleta de colores corporativa (azul marino `#0F1E2E`, dorado `#C8963E`, crema `#F4F3EE`).
