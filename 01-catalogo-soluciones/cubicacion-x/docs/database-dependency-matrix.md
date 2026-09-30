# Matriz de dependencias de datos

| Objeto | Tipo | Usado por | Depende de | Función |
|---|---|---|---|---|
| `registros` | tabla | Registro, Consumos, Informes | proveedores, bodegas | Cabecera de recepción/inventario |
| `registros_detalle` | tabla | Registro, Consumos | registros | Tablas físicas por estiba y estado |
| `aserrio` | tabla | Aserrío, Informes, Admin | bodegas | Lote/ticket de transformación |
| `aserrio_detalle_bloque` | tabla | Aserrío, costeo | aserrio | Materia prima cargada |
| `aserrio_detalle_dimensionada` | tabla | Aserrío, costeo | aserrio | Producción por dimensión/estiba |
| `aserrio_ajustes` | tabla | Aserrío, costeo | aserrio | Ajustes/sobrantes de entrada |
| `consumos` | tabla | Consumos | sequence | Orden de consumo |
| `consumo_productos_rel` | tabla | Consumos | consumos, pdesarrollo.productos | Productos de la orden |
| `consumos_detalle` | tabla | Consumos | pdesarrollo.productos, registros_detalle (lógica) | Historial de tablas consumidas |
| `productos` | vista | Consumos | pdesarrollo.productos + catálogos | Maestro consolidado de productos |
| `get_estibas_consumo_disponibles` | RPC | Consumos | registros, registros_detalle | Inventario disponible agrupado |
| `get_next_id` | RPC | todos los flujos | `seq_*` | Consecutivos legibles |
| `valorizar_idaserrio` | RPC | Aserrío/Admin | aserrio + detalles, precios, factores, valorización | Snapshot de costo por espesor |
| `calcular_costo_real_aserrio_mensual` | RPC | Admin | gastos, matriz, precios, valorización | Costo mensual real |
| `reporte_merma_view`, `reporte_min_max` | vistas | GAS/reportes | aserrio + detalles + ajustes | Rendimiento y merma |
| vistas `v_aserrio_*` | vistas | Admin/GAS | tablas de costeo | Lectura analítica |
| maestros | tablas | todos | — | Proveedores, bodegas, madera, dimensiones, operadores |

## Candidatos atómicos

- `ATOMIC_OPERATION_CANDIDATE crearRegistro`: reservar consecutivo + insertar cabecera.
- `ATOMIC_OPERATION_CANDIDATE cerrarRegistro`: vaciar cola + validar detalle + cerrar cabecera + generar evento de reporte (GAS no puede formar parte de la misma transacción DB).
- `ATOMIC_OPERATION_CANDIDATE cerrarAserrio`: persistir bloque/dimensionada/ajustes + cierre + valorización.
- `ATOMIC_OPERATION_CANDIDATE consumirEstiba`: insertar consumos detalle + marcar cada `registros_detalle` CONSUMIDO + actualizar/cerrar orden; requiere locks para impedir doble consumo.
- `ATOMIC_OPERATION_CANDIDATE calcularCostoMensual`: validar insumos, valorizar faltantes y reemplazar snapshot del período.
