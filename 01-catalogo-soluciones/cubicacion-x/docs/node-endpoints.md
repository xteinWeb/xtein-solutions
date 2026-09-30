# Endpoints Node candidatos

Todos son `POST`, reciben el envelope corporativo y fijan internamente SP/acción. `prmAccion` que no coincida con la ruta, JSON inválido o envelope incompleto devuelve HTTP 400 con `ErrMensaje`; fallo de conexión/ejecución devuelve HTTP 500. Los errores funcionales de SQL viajan dentro de `DATOS`.

| URL relativa | Módulo | ACCION | SP | Payload `prmDatos` | Respuesta `DATOS` |
|---|---|---|---|---|---|
| `/api/cubicar/maestros/listar` | Maestros | `LISTAR MAESTROS` | `cubicar.spCubicarMaestros` | `{}` | objeto con proveedores y cuatro listas maestras |
| `/api/cubicar/proveedores/listar` | Proveedores | `LISTAR PROVEEDORES` | `cubicar.spCubicarProveedores` | `{}` | lista ordenada |
| `/api/cubicar/proveedores/crear` | Proveedores | `CREAR PROVEEDOR` | mismo | `{nombre,nit}` | lista con fila creada o `{ErrMensaje}` |
| `/api/cubicar/proveedores/actualizar` | Proveedores | `ACTUALIZAR PROVEEDOR` | mismo | `{id,nombre,nit}` | lista con fila; vacía si no existe |
| `/api/cubicar/proveedores/eliminar` | Proveedores | `ELIMINAR PROVEEDOR` | mismo | `{id}` | lista vacía o `{ErrMensaje}` si está referenciado |

La URL base, middleware de identidad, logging corporativo y función real `getConnection` son `PENDIENTE_DE_DEFINICION`.
