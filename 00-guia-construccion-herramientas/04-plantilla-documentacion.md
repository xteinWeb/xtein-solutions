# 04. Kit Documental Canónico de una Solución

> **Estructura Estándar de Documentación Técnica en ARTDECON**  
> Todo proyecto en el catálogo debe incluir estos 5 documentos en su carpeta `/docs`.

---

## 📑 Los 5 Documentos Obligatorios

Inspirado en el estándar exitoso de `Cubicacion_X`, cada solución debe documentarse con estos cinco archivos:

```text
mi-solucion/
└── docs/
    ├── application-map.md
    ├── database-dependency-matrix.md
    ├── backend-operation-catalog.md
    ├── parity-matrix.md
    └── execution-report.md
```

---

### 1. `application-map.md` (Mapa Canónico de la Aplicación)
* **Objetivo:** Dar una visión clara y rápida de qué hace la herramienta, qué tecnologías usa y cómo se entra a ella.
* **Contenido obligatorio:**
  * Stack tecnológico (versión de Angular, Node, base de datos).
  * Entry points (archivos principales de arranque, `main.ts`, `AppModule`, rutas).
  * Módulos reales y vistas (tabla con: Módulo, Componente/Vista, Tablas vinculadas y Reglas clave).
  * Dependencias externas y servicios auxiliares.

---

### 2. `database-dependency-matrix.md` (Matriz de Dependencias de BD)
* **Objetivo:** Conocer con precisión quirúrgica qué tablas se leen o modifican para evitar bloqueos y corrupción de datos.
* **Contenido obligatorio:**
  * Tabla con: Nombre de la tabla / vista, Tipo de acceso (`Lectura`, `Escritura`, `RPC`), Esquema de BD, Criticidad y Observaciones.
  * Riesgos de concurrencia identificados.

---

### 3. `backend-operation-catalog.md` (Catálogo de Operaciones Backend)
* **Objetivo:** Describir los contratos de comunicación entre el frontend y el backend.
* **Contenido obligatorio:**
  * Listado de Endpoints REST / GraphQL o Procedimientos Almacenados (SPs).
  * Por cada operación:
    * Método HTTP y URL (`POST /api/v1/maestros/productos`).
    * Parámetros de entrada esperados (JSON schema o TypeScript interface).
    * Respuestas de éxito (HTTP 200/201 con payload).
    * Respuestas de error tipadas (RFC 7807 con código y mensaje).

---

### 4. `parity-matrix.md` (Matriz de Paridad Operativa)
* **Objetivo:** Garantizar que la nueva herramienta no pierda ninguna funcionalidad que el usuario ya tenía en el sistema anterior o en Excel.
* **Contenido obligatorio:**
  * Tabla comparativa:
    * *Funcionalidad en el proceso anterior / legacy.*
    * *Cómo se resuelve en la nueva herramienta.*
    * *Estado de paridad (`Completo`, `Parcial`, `Mejorado`).*
    * *Diferencias o mejoras de tiempo observadas.*

---

### 5. `execution-report.md` (Reporte de Ejecución y Pruebas)
* **Objetivo:** Dejar constancia formal de qué pruebas se corrieron, qué funcionó y qué quedó pendiente antes del despliegue.
* **Contenido obligatorio:**
  * Resultado general del pase a pruebas.
  * Validaciones realizadas (compilación, pruebas unitarias, validación de contratos, pruebas con usuarios de taller).
  * Alertas de dependencias o vulnerabilidades conocidas (`npm audit`).
  * Estado final (`LISTO PARA PRODUCCIÓN` o `PARCIAL - PENDIENTE INTEGRACIÓN`).
