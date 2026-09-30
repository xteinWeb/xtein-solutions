# Matriz de paridad

Clasificación global: `PARCIAL - PENDIENTE INTEGRACION CORPORATIVA`.

| Función legacy | Nueva función | Estado | Validación |
|---|---|---|---|
| Cargar bodegas/maderas/largos/dimensiones | `MaestrosService` + `spCubicarMaestros` | PARCIAL | contrato y compilación; falta SQL Server real |
| Listar/buscar proveedores | componente/service + acción LISTAR | PARCIAL | fixture lista vacía, filtro preservado; falta DB real |
| Crear proveedor | acción CREAR | PARCIAL | trim, null, caracteres especiales y duplicado cubiertos |
| Actualizar proveedor | acción ACTUALIZAR | PARCIAL | fila y entidad inexistente cubiertas |
| Eliminar proveedor | acción ELIMINAR | PARCIAL | caso libre y FK referenciada cubiertos |
| Error de payload | handler Node + validación `ISJSON` | OK en harness | pruebas automatizadas |
| Error técnico | handler Node | OK en harness | respuesta 500 sin detalle sensible |
| Identidad/autorización | token `CUBICAR_USER` / host | PENDIENTE | requiere integración corporativa |

Fixtures: `corporate/parity/fixtures/maestros-proveedores.json`. No contienen datos productivos; cada expectativa deriva de código o constraints observados.
