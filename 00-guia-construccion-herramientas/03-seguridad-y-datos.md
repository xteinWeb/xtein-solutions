# 03. Seguridad, Datos y Gobernanza

> **Estándar de Protección de Información y Datos en ARTDECON**  
> Aplicación técnica del Semáforo de Gobernanza PILAS IA.

---

## 🚦 1. El Semáforo Técnico XTEIN

| Nivel | Clasificación | Reglas Técnicas |
| :--- | :--- | :--- |
| 🟢 **Verde** | **Permitido y Promovido** | • Uso de cuentas institucionales autorizadas (@artdecon.com).<br>• Procesamiento de manuales técnicos, procedimientos, catálogos y reportes operativos.<br>• Consultas a APIs oficiales de Google Workspace y Gemini dentro del tenant corporativo. |
| 🟡 **Amarillo** | **Revisión Humana Obligatoria** | • Operaciones con impacto en costos, cubicación de madera, pago de nómina o compras.<br>• Todo cálculo generado por modelos de IA debe ser validado por un operador antes de impactar inventario o contabilidad.<br>• Auditoría obligatoria de citas y fuentes de datos. |
| 🔴 **Rojo** | **Estrictamente Prohibido** | • *Shadow AI:* Uso de herramientas no aprobadas con cuentas personales.<br>• Almacenar secretos, tokens de API o contraseñas en repositorios Git.<br>• Subir bases de datos completas con información médica, bancaria o datos personales de colaboradores a plataformas externas. |

---

## 🔑 2. Gestión de Secretos y Variables de Entorno

* **Prohibición de Hardcoding:** Nunca incluir URLs de bases de datos, contraseñas o tokens en archivos `.ts`, `.js` o `.html`.
* **Uso de `.env`:**
  * Cada proyecto debe tener un archivo `.env.example` en el repositorio con las claves requeridas pero valores vacíos o de ejemplo.
  * El archivo `.env` real debe estar explícitamente listado en el `.gitignore`.
  * En ambientes de producción o staging, los secretos se configuran mediante variables de entorno del servidor o gestor de secretos corporativo.

---

## 🗄️ 3. Segregación de Datos: OLTP vs. OLAP (ADR-002)

Para proteger la operación diaria de la fábrica:
* **Bases Transaccionales (OLTP):**
  * SQL Server / Supabase transaccional.
  * Diseñadas para registrar pedidos, despachos, asistencia y movimientos de inventario en tiempo real.
  * **Regla:** Ningún reporte pesado, consulta analítica o proceso de machine learning debe ejecutarse directamente sobre las tablas transaccionales en horas pico de producción.
* **Bases Analíticas / Reportes (OLAP):**
  * Réplicas o almacenes de consulta periódica donde se corren dashboards, reportes mensuales y análisis de IA.
