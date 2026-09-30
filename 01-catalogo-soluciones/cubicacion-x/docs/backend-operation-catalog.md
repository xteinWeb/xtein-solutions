# Catálogo funcional para futuro backend

Tecnología no definida. Los nombres expresan acciones de negocio, no CRUD de tablas.

| Operación | Módulo | Entrada → salida | Reglas / datos actuales | Transacción y errores |
|---|---|---|---|---|
| `identificarOperador` | Login | PIN → operador/rol | `operadores`; hoy compara en cliente | Autorización corporativa pendiente; PIN inválido/inactivo |
| `listarMaestrosCubicar` | Shell | — → proveedores, bodegas, maderas, largos, dimensiones | tablas maestras | Solo lectura |
| `listarProveedores` | Proveedores | filtro → lista | proveedores | Solo lectura |
| `crearProveedor` / `actualizarProveedor` / `eliminarProveedor` | Proveedores | nombre,NIT,id → proveedor | nombre único; referencias desde registros | Tx simple; duplicado/en uso |
| `crearRegistro` | Registro | operador, cabecera → id | `get_next_id`, `registros` | Sí; consecutivo seguro |
| `obtenerRegistroAbierto` | Registro | operador → cabecera+detalle | estado ABIERTO | Multiplicidad inesperada |
| `agregarTablaRegistro` / `eliminarTablaRegistro` | Registro | dimensiones/estiba → totales | fórmula pies; máximo dos espesores/estiba | Sí por lote; dimensión inválida |
| `cerrarRegistro` | Registro | id → resumen/reporte pendiente | detalle + cabecera; GAS PDF | Sí para DB; reporte asíncrono/reintentable |
| `crearAserrio` / `obtenerAserrioAbierto` | Aserrío | turno,bodega,madera,operador → id/estado | aserrio + consecutivo | Sí |
| `registrarBloque` / `registrarDimensionada` / `registrarAjuste` | Aserrío | lote y medidas → línea | tres detalles; fórmula pies | Sí por lote/cola |
| `cerrarAserrio` | Aserrío | id,tipo cierre → resumen | solo con producción válida | Sí; incluye persistencia y cierre |
| `valorizarAserrio` | Aserrío/Admin | id → snapshot/advertencias | `valorizar_idaserrio`; cerrado, precios/factores vigentes, histórico inmutable | Sí; faltan precio/datos |
| `corregirEspesorEstiba` | Admin | estiba,actual,nuevo → filas/pies | RPC con lock y recálculo | Sí serializable por estiba |
| `obtenerEstibasDisponibles` | Consumos | bodega,inventario → estibas/items | RPC actual | Lectura consistente |
| `crearConsumo` | Consumos | operador,productos → id | consumos + relación | Sí; producto inexistente |
| `consumirTablas` | Consumos | orden,estiba,ids → resultado | detalle + estado de inventario | Sí con locks; ya consumida/conflicto |
| `guardarProgresoConsumo` / `cerrarConsumo` | Consumos | orden → estado | múltiples escrituras actuales | Sí |
| `listarReportes` / `generarInforme` | Informes | origen,ids,formato → job/archivo | Supabase + GAS | BACKEND_CANDIDATE; fallo externo/reintento |
| `configurarCostosAserrio` | Admin/GAS | período,precios,gastos,matriz → versión | upsert RPC y vigencias | Sí; período/concepto/valor inválido |
| `calcularCostoMensualAserrio` | Admin | período → snapshot | RPC actual | Sí; faltantes y división por cero |
