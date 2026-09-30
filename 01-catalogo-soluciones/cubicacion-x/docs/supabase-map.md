# Mapa real de Supabase para Cubicar

Fuente: proyecto desplegado `cubicacionv4` (`edyjxpoulcufaxoqvduv`), inspeccionado 2026-09-04 y reconciliado con código y SQL versionado. No se modificó la base.

## Alcance y clasificación

Schemas: `public` es el núcleo de Cubicar; `pdesarrollo` es DEPENDENCIA INDIRECTA por la vista `public.productos` y dos FK. `auth`, `suite`, `costos`, `consumos`, `pintura`, `pilasia`, `solicitudmat`, `storage` y otros objetos compartidos son NO UTILIZADOS POR CUBICAR salvo futura evidencia.

## Tablas

| Grupo | Objetos | Consumidor / propósito |
|---|---|---|
| Operación base | `registros`, `registros_detalle` | Registro e inventario de tablas/estibas |
| Aserrío | `aserrio`, `aserrio_detalle_bloque`, `aserrio_detalle_dimensionada`, `aserrio_ajustes` | Entradas, producción, sobrantes y cierre |
| Consumos | `consumos`, `consumo_productos_rel`, `consumos_detalle` | Orden, productos y tablas consumidas |
| Maestros | `proveedores`, `bodegas`, `tipos_madera`, `largos`, `dimensiones`, `operadores` | Selectores y acceso por PIN |
| Costeo | `aserrio_factor_espesor`, `aserrio_precio_pie_bloque`, `aserrio_valorizacion`, `aserrio_informe_precios`, `aserrio_gasto_mensual`, `aserrio_valor_matriz_madera`, `aserrio_costo_real_mensual` | Factores, vigencias, valorización y costo mensual |
| Indirecta | `pdesarrollo.productos` y catálogos enlazados | Fuente de `public.productos`; FK por `cod_interno` |
| Legacy dudoso | `productos_old` | No consumida por el código actual |

La definición de columnas y constraints equivalente queda materializada en `sqlserver/01_schema`. PK operativas: UUID salvo maestros/consumos detalle identity. Claves de negocio únicas: `id_registro`, `id_aserrio`, `id_consumo`, nombres de maestros, `(id_consumo_f,cod_producto)` y `(idaserrio,espesor_mm,version_calculo)`. FK principales enlazan cabecera-detalle con borrado cascada; consumos enlaza al producto compartido.

## Vistas

- UTILIZADO: `public.productos` (proyección de múltiples catálogos `pdesarrollo`).
- DEPENDENCIA INDIRECTA/reportes: `reporte_merma_view`, `reporte_min_max`, `analisis_rendimiento_espesor`.
- Costeo: `v_aserrio_valorizacion_detalle`, `v_aserrio_valorizacion_resumen_periodo`, `v_aserrio_costo_proceso`, `v_aserrio_costo_real_vs_matriz`, `v_aserrio_gasto_mensual_resumen`, `v_aserrio_indicadores_mes`.
- No se hallaron materialized views de Cubicar.

## Funciones/RPC

| Objeto | Consumidor | Función y dependencias | Destino candidato |
|---|---|---|---|
| `get_next_id(seq_name,prefix)` | `src/lib/services/consecutivos.service.ts` | Consecutivos dinámicos sobre `seq_*`; usa SQL dinámico | Validar allow-list en Supabase |
| `get_estibas_consumo_disponibles` | Consumos | Agrupa `registros` + detalle disponible y devuelve JSON | procedure/consulta backend |
| `valorizar_idaserrio` | Aserrío/Admin | Precio vigente, factores, merma y snapshot por espesor | stored procedure transaccional |
| `calcular_costo_real_aserrio_mensual` | Admin | Valida gastos/precios/matriz, valoriza faltantes y reemplaza resumen mensual | stored procedure transaccional |
| `corregir_espesor_estiba_aserrio` | Admin/GAS potencial | Bloquea estiba, recalcula pies y actualiza | stored procedure transaccional |
| `calcular_factores_aserrio`, `valorizar_periodo_aserrio` | GAS/admin | Recalculo masivo | job/backend con procedure |
| tres `aserrio_upsert_*` | GAS | Vigencias y gastos | procedures |
| `get_next_costo_madera_id` | GAS | consecutivo `CM-` | sequence/procedure |
| `aserrio_set_updated_at` | triggers | sello `updated_at` | trigger o backend |

## Triggers, sequences y enums

Triggers `trg_aserrio_{factor,precio,gasto,matriz}_updated_at` ejecutan `aserrio_set_updated_at` antes de UPDATE. Sequences utilizadas: `seq_madera_registro`, `seq_estiba`, `seq_aserrio`, `seq_consumo`, `seq_costo_madera` y sequences identity de maestros/detalles. No hay enums PostgreSQL propios de Cubicar; los dominios son texto + checks.

## RLS, policies y grants

RLS está habilitado en tablas operativas, pero las policies permiten lectura o `ALL` a `anon`/`public` con predicado `true`; esto equivale a autenticación/autorización débil. Siete tablas de costeo tienen RLS deshabilitado: `aserrio_factor_espesor`, `aserrio_precio_pie_bloque`, `aserrio_valorizacion`, `aserrio_informe_precios`, `aserrio_gasto_mensual`, `aserrio_valor_matriz_madera`, `aserrio_costo_real_mensual`. Varias RPC son `SECURITY DEFINER`. Riesgo existente: acceso Data API amplio con clave pública. No se cambió para no romper producción. Destino: `AUTHORIZATION_TO_BE_DEFINED_BY_CORPORATE_BACKEND`.

## Drift código / versionado / desplegado

El desplegado contiene `get_next_id`, múltiples RPC de costeo y vistas que no tienen archivo propio versionado. El archivo `aserrio_valorizacion.sql` sí cubre gran parte del costeo; los SQL “TEMPORAL” corresponden a vistas realmente desplegadas. `productos` ya no es la tabla legacy: es una vista sobre `pdesarrollo`, detalle relevante para migración.
