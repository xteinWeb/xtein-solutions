# 05. Checklist de Aprobación XTEIN

> **Criterios de Aceptación para Pase a Producción en ARTDECON**  
> Ninguna solución puede ser desplegada a usuarios finales sin superar esta lista de verificación.

---

## ✅ Lista de Verificación Oficial

Antes de fusionar el código al repositorio central o publicar la herramienta para los colaboradores, el desarrollador o líder de proyecto debe verificar los siguientes 5 bloques:

---

### Bloque 1: Arquitectura y Código
- [ ] La solución sigue el patrón Gateway / Fachada (el frontend no conoce la infraestructura de BD).
- [ ] No se modificaron destructivamente archivos funcionales de sistemas legacy (patrón Strangler Fig).
- [ ] El código compila sin errores ni advertencias críticas (`ng build` o `tsc`).
- [ ] No existen dependencias globales innecesarias que choquen con otras herramientas.

---

### Bloque 2: Seguridad y Datos (Gobernanza)
- [ ] **Cero credenciales quemadas:** No hay contraseñas, tokens JWT fijos ni cadenas de conexión en el repositorio Git.
- [ ] Existe un archivo `.env.example` actualizado con nombres de variables claras.
- [ ] El archivo `.env` está explícitamente incluido en `.gitignore`.
- [ ] Las consultas a base de datos utilizan parámetros tipados o SPs (protegidos contra inyección SQL).
- [ ] Si la herramienta usa IA, cumple con el Semáforo Verde/Amarillo (no procesa contraseñas ni datos sensibles sin cifrar).

---

### Bloque 3: Documentación Canónica
- [ ] Existe la carpeta `/docs` en el proyecto.
- [ ] Se incluyó el `application-map.md` con el stack y módulos explicados.
- [ ] Se incluyó el `database-dependency-matrix.md` con tablas y tipos de acceso.
- [ ] Se incluyó el `backend-operation-catalog.md` con los endpoints y contratos.
- [ ] Se incluyó el `parity-matrix.md` asegurando que no se pierden reglas de negocio anteriores.
- [ ] Se incluyó el `execution-report.md` con el balance de pruebas.

---

### Bloque 4: Validación con el Usuario del Taller/Oficina
- [ ] La herramienta fue probada por al menos 1 usuario real del área correspondiente (planta, compras, ventas, etc.).
- [ ] El usuario entendió cómo ingresar y operar la herramienta sin requerir asistencia continua.
- [ ] Los mensajes de error de la interfaz son claros y comprensibles (no muestran errores técnicos tipo `500 Internal Server Error`).

---

### Bloque 5: Adopción y Comunicación PILAS IA
- [ ] La solución fue registrada en el Catálogo de Soluciones de `xtein-solutions`.
- [ ] Se preparó una breve ficha para el **Boletín PILAS IA de WhatsApp** (explicando qué hace en 3 líneas, enlace de acceso y tiempo estimado ahorrado).

---

## 🎯 Dictamen XTEIN

| Estado | Significado | Acción |
| :--- | :--- | :--- |
| 🟢 **APROBADO** | Cumple los 5 bloques al 100%. | Pase a producción y difusión en el boletín. |
| 🟡 **OBSERVADO** | Funcional, pero falta documentación o ajustes de seguridad menores. | Se concede plazo de 3 días para subsanar antes del despliegue masivo. |
| 🔴 **RECHAZADO** | Vulnerabilidad de seguridad crítica o acople destructivo a sistemas legados. | No se permite despliegue en ARTDECON. |
