# 01. Ciclo de Vida de una Solución XTEIN

> **Metodología Oficial de Transformación en ARTDECON**  
> Basado en el Círculo de Transformación de PILAS IA (Temporada 2).

---

## 🔄 El Flujo de 5 Fases

Toda herramienta, script o módulo desarrollado en ARTDECON debe transitar por 5 fases claras:

```text
[1. Fricción / Dolor] ➡️ [2. Arquitectura & Contratos] ➡️ [3. Construcción & IA] ➡️ [4. Documentación Canónica] ➡️ [5. Despliegue XTEIN]
```

---

### Fase 1: Descubrimiento y Alcance (Foco en el Colaborador)

* **Origen:** Identificar una tarea manual repetitiva, lenta o propensa a errores en planta, taller u oficina (ej. cotizaciones, cubicación de madera, filtrado de hojas de vida, registro de asistencia).
* **El Círculo de los 7 Pasos:**
  1. *Simplificar:* Eliminar pasos innecesarios antes de programar.
  2. *Estandarizar:* Definir la regla de negocio clara en papel o Excel.
  3. *Digitalizar:* Llevar los datos a una estructura limpia.
  4. *Automatizar:* Crear el flujo o script.
  5. *Potenciar con IA:* Agregar modelos de lenguaje o visión donde aporten valor diferencial.
  6. *Integrar:* Conectar con el ecosistema ARTDECON.
  7. *Escalar:* Llevar la solución a otras áreas.
* **Entregable de Fase 1:** Documento breve de alcance con: usuario objetivo, dolor actual, tiempo ahorrado estimado y fuentes de datos requeridas.

---

### Fase 2: Arquitectura y Definición de Contratos

Antes de tirar la primera línea de código:
* **Identificar dependencias:** ¿Qué bases de datos toca? (SQL Server local, Supabase, Google Sheets, archivos locales).
* **Definir el Contrato Gateway:** Ningún componente visual debe acoplarse directamente a la lógica de base de datos.
* **Elegir el Stack Homologado:**
  * *Frontend:* Angular (versión estandarizada en XTEIN) o interfaces web ligeras.
  * *Backend / Middleware:* Node.js / TypeScript con Express o Fastify.
  * *IA / Automatización:* APIs oficiales de Google Gemini / Workspace o scripts Python controlados.

---

### Fase 3: Construcción y Buenas Prácticas

* **Estructura Modular:** El código nuevo debe residir en carpetas aisladas (ej. `corporate/` o `features/`) sin contaminar archivos existentes.
* **Manejo Seguro de Secretos:** Prohibido quemar tokens, contraseñas o URLs de base de datos en el código fuente. Usar archivos `.env` (excluidos en `.gitignore`) y `.env.example` documentado.
* **Manejo de Errores Estandarizado:** Toda respuesta de error en APIs debe seguir la convención corporativa (código de error, mensaje comprensible para el usuario y detalle técnico en logs).

---

### Fase 4: Documentación Canónica (Obligatoria)

Ningún desarrollo se considera terminado si no cuenta con sus **5 documentos canónicos** dentro de la carpeta `/docs`:
1. `application-map.md` (Mapa funcional y stack).
2. `database-dependency-matrix.md` (Tablas y permisos).
3. `backend-operation-catalog.md` (Endpoints y llamadas).
4. `parity-matrix.md` (Validación de reglas contra el proceso anterior).
5. `execution-report.md` (Pruebas ejecutadas y estado de integración).

---

### Fase 5: Validación XTEIN y Despliegue

* **Revisión por XTEIN:** Se audita el cumplimiento del checklist de seguridad y arquitectura.
* **Integración a GitHub:** Merge al repositorio central `xtein-solutions`.
* **Cápsula de Adopción (Boletín PILAS IA):** Se genera la infografía y el mensaje de WhatsApp para que los usuarios finales conozcan y comiencen a usar la herramienta.
