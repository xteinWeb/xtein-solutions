# Reglas observadas: Maestros y Proveedores

Fecha de inspección: 2026-09-07. Los contratos se conservan en servicios Angular y en constraints/policies/estadísticas de Supabase `cubicacionv4`. La consulta remota fue exclusivamente de lectura.

## Maestros

| Regla observada | Evidencia | Estado |
|---|---|---|
| Cubicar consume bodegas, tipos de madera, largos, dimensiones y proveedores como catálogos. | `loadMaestrosFirestore` | CONFIRMADA |
| La nueva primera entrega expone Maestros solo para lectura. | El legacy no crea/edita estos cuatro catálogos desde sus pantallas operativas. | CONFIRMADA |
| Bodega entrega `id_db,nombre`; tipo de madera entrega nombre; largo entrega valor; dimensión entrega tipo/valor. | Selects explícitos de `MaestrosService`. | CONFIRMADA |
| Los largos se ordenan ascendentemente; los demás selectores se ordenan por texto en cliente. | `.order('valor')`, `fillSelect` y `fillSelectId`. | CONFIRMADA |
| Dimensiones se separan en `PLG` y `MM`; Registro compra usa PLG y dimensionada usa MM. | `window.maestros.dims` y `populateEspesor`. | CONFIRMADA |
| Nombres de bodega, tipo de madera y valores de largo son únicos en base. | Constraints desplegados. | CONFIRMADA |
| La edición corporativa futura de estos catálogos y sus permisos. | No existe comportamiento equivalente en Cubicar. | PENDIENTE_DE_DEFINICION |

## Proveedores

| Regla observada | Evidencia | Estado |
|---|---|---|
| Listar `id,nombre,nit` por nombre ascendente; lista vacía es válida. | `cargarProveedores` / `renderProveedores`. | CONFIRMADA |
| Buscar localmente por coincidencia parcial, sin distinguir mayúsculas, en nombre o NIT. | `renderProveedores`. | CONFIRMADA |
| Nombre obligatorio y recortado; NIT recortado, opcional y persistido como `null` si queda vacío. | `guardarProveedor`; columna `nit` nullable. | CONFIRMADA |
| Se rechaza otro nombre igual tras `trim().toLowerCase()`. | Validación de cache; `UNIQUE(nombre)` en PostgreSQL. | CONFIRMADA EN UI; collation SQL Server debe preservar equivalencia |
| NIT no es único. | No hay constraint; hay al menos un NIT no vacío repetido en producción. | CONFIRMADA |
| Caracteres especiales son admitidos y escapados al renderizar. | `escapeHtml`; 8 de 14 nombres desplegados contienen caracteres fuera de ASCII alfanumérico/espacio. | CONFIRMADA |
| Actualizar conserva el ID y reemplaza nombre/NIT. | `.update(payload).eq('id',id)`. | CONFIRMADA |
| Eliminar es físico y requiere confirmación UI. | `confirm` + `.delete().eq('id',id)`. | CONFIRMADA |
| Un proveedor referenciado por `registros.proveedor_id` no puede eliminarse. | FK sin `ON DELETE`; UI traduce el fallo a “puede estar asociado”. | CONFIRMADA |
| Un ID inexistente produce cero filas afectadas sin error de Supabase. | Semántica de update/delete filtrado y ausencia de `.select()`/validación de conteo. | CONFIRMADA; se preserva como resultado vacío |
| Longitud máxima corporativa definitiva. | PostgreSQL usa `text`; datos actuales: nombre máximo 40, NIT máximo 2. | PENDIENTE_DE_DEFINICION; candidato técnico `nvarchar(250)`/`nvarchar(80)` |
| Autorización para crear/editar/eliminar. | Legacy expone acciones sin control de rol en el módulo. | PENDIENTE_DE_DEFINICION; debe suministrarla el host |

## Perfil leído, sin copiar datos productivos

14 proveedores: 5 referenciados y 9 no referenciados; no hay nombres duplicados normalizados; NIT admite repetición; 5 bodegas, 5 tipos de madera, 8 largos y 19 dimensiones. Estos conteos son evidencia temporal, no reglas ni seed.
