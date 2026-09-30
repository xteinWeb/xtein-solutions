# Solución: Cubicación X (Aserrío y Madera) 🪵

> **Módulo de Gestión de Aserrío, Registro de Bloques, Consumos y Proveedores**  
> **Estado:** 🟢 *Caso Modelo de Documentación Técnica XTEIN*  
> **Ubicación en desarrollo:** `C:\Users\admin_artdecon\Documents\desarrollo\Cubicacion_X`

---

## 📋 Resumen de la Solución

**Cubicación X** es el sistema crítico para el control de la materia prima principal en ARTDECON: la madera. Gestiona desde la recepción de madera en bloque, su paso por el aserrío, el control de espesores y mermas, hasta el consumo en líneas de producción y la liquidación de proveedores.

Se convirtió en el **proyecto modelo de XTEIN** porque implementó exitosamente el patrón de migración **Strangler Fig**: modularizando la lógica en Angular 15.2 y Node.js sin alterar destructivamente el legacy ni la base de datos de Supabase.

---

## 📚 Documentación Técnica Canónica

Los 10 documentos técnicos oficiales de esta solución han sido centralizados en la carpeta [`/docs`](./docs/):

| Documento | Descripción |
| :--- | :--- |
| **[application-map.md](./docs/application-map.md)** | Mapa canónico: stack Angular/Node, entry points, vistas y módulos. |
| **[angular-module-map.md](./docs/angular-module-map.md)** | Mapeo detallado de componentes, rutas y servicios en Angular. |
| **[database-dependency-matrix.md](./docs/database-dependency-matrix.md)** | Matriz de dependencias de tablas, vistas y RPCs en Supabase. |
| **[backend-operation-catalog.md](./docs/backend-operation-catalog.md)** | Catálogo de operaciones backend y procedimientos almacenados (SPs). |
| **[node-endpoints.md](./docs/node-endpoints.md)** | Especificación de los endpoints Node para transporte seguro. |
| **[observed-rules-maestros-proveedores.md](./docs/observed-rules-maestros-proveedores.md)** | Reglas de negocio observadas para maestros y proveedores. |
| **[parity-matrix.md](./docs/parity-matrix.md)** | Matriz de paridad comparativa contra el proceso anterior. |
| **[first-corporate-execution.md](./docs/first-corporate-execution.md)** | Reporte de la primera ejecución corporativa y pruebas de validación. |
| **[pending-corporate-integration.md](./docs/pending-corporate-integration.md)** | Tareas pendientes para la integración definitiva a XTEIN ONE. |
| **[supabase-map.md](./docs/supabase-map.md)** | Mapeo exhaustivo de tablas, constraints y tipos en Supabase. |
